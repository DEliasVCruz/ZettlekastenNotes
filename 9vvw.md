# cloud.aws.lambda

An `aws` service to run code on the cloud without having to manage servers

---
tags: @compute @serverless @aws @managed
---

## Synopsis

```sh
aws 
```

## Overview

With this you don't have to worry much about the infrastructure of your application
but rather only focus on creating the code that will be run

`AWS` manages everything related to:
  - High availability and security
    - They run automatically across multiple availability zones within a region
    - You don't have to manage multi `AZ` deployments
  - Automatic scaling to meed your needs

Most importantly you only pay for what's been used (`compute`) and get no charges
for idle instances
  - When the code is `invoked` you are billed in **1 millisecond** increments

The code that runs in your lambda is called a `lambda function`
  - You can run code in **any language** or provide a **custom runtime** to run on
  - Are automatically load balanced
  - They handle failures (retries)
  - Are isolated from each other in a secure way
  - They provide monitoring and logging

They run in response to events:
  - After you upload your code to lambda, you can configure an `event source`
  - There are over **200** integration's for event sources, like:
    - `API Gateway`, `S3`, `DynamoDB`, `SQS/SNS`
  - Instead of scaling by provisioning more servers, it scales in response to the
    events

### Author, build and deploy lambda functions

Lambda supports 2 types of deployment packages:
  - As a [zip](./kg1a.md) `archive`
  - As a [container](./xbcw.md) `image`

You can create `zip archive` of your function and it's dependencies; and upload
it to an [s3](./2s8v.md) bucket

You can also **build** your functions using `container images`, you define
your containers using the `OCI` spec (like a [docker file](./fm36.md)) that then
you have to push to **Amazon Elastic Container Registry** (`ECR`)

### The programming model of lambda functions

The lambda programming model is common to all of the runtimes, it defines the
interface between your code and the lambda service

When your function runs for the first time, it runs an initialization process
which you can use to:
  - Setup dependencies
  - Configurations
  - Common helper functions before an invoke
  - It runs only once when the lambda ins initialize

Then it handles the event that trigger the lambda through the `handler`, this
receives **2 objects** as parameters:
  - `event`: Contains all the data and metadata the lambda needs to run, depending
    on which source created it

    For example, an event created by `api gateway` contains details related to the
    request that the `api client` made, like the `path`, `query string` and `request body`

    Other event created by `s3` when a new object is created includes details about
    the bucket name and the new object

    It can then use this to handle the request, like access the path of the `s3`
    new object to download it

  - `context`: This allows to interact with the lambda execution environments and
    contains a number of properties and methods

    You can get information like the `name` and `version` of the function or
    things like `request id` to track specific invocations, the amount of time
    in milliseconds remaining before a function time outs, `logs`, etc.
  

Subsequent invocations of a lambda that has already been initialized will not
run the initialization code again and will only run the code inside the
`handler` function

When your `lambda code` finish processing, it sends it's response back to the
lambda service and is then available to process another invoke

```python
"""
Initialization:
  - Runed during initialization before invocation
  - Dependencies configuration
"""
# Init code, outside handler
import boto3 # AWS SDK for python
import cheeseburger # And external package dependency

cheeseburger.pre_handler_secret_getter()


"""
Handler function:
  - The entry point to the lambda function
  - The function to run during invocation
"""
def handler(event, context):
  # Inside handler code
  if cheeseburger.no_bacon(event["extras"]):
    add_bacon(event)

    return "warning"
  else:
    return "success"

"""
Initialization:
  - Comon helper functions
"""
# Init code, outside handler
def add_bacon(data):
  ...
```

## Cookbook

### Create and build a lambda function from the console

### Deploying a zip lambda using the aws cli

You should first [create an iam execution role](./8o8o.md) to be `assumed` by the 
lambda when executing, so that it have permission to access `aws resources`,
you can do this with the `aim creat-role` command

- In this example we use an inline trust policy

```sh
aws iam create-role \
  --role-name my-new-role \
  --asume-role-policie-document \
    '{ \
      "Version": "2012-10-17", \
      "Statement": [{ \
        "Effect": "Allow", \
        "Principal": { "Service": "lambda.amazonaws.com" }, \
        "Action": "sts:AsumeRole" \
      }] \
    }'
```

Then you have to [zip](./kg1a.md) the lambda code along all it's dependencies, you have
to use your languages of choice native package manager

For supported language runtimes, you only have to package the external
dependencies as all standard runtime dependencies are already installed

```sh
zip -q function.zip index.js
```

Now we can create our function with the [create function](./gxk1.md) 

```sh
aws lambda create-function 
  --function-name my-new-function \
  --zip-file ./function.zip \
  --handler index.handler \
  --runtime nodejs18.x \
  --role arn:aws:iam:9783923742:role/my-new-role
```

Then we can invoke our function and view it's response and logs with the
`invoke function` sub-command of the `lambda` command

- In this case we decode the logs as [base64](./nlre.md) encoded text

```sh
aws lambda invoke \
  --function-name my-new-function out \
  --log-type Tail \
  --query 'LogResult' \
  --output text | base64 -d
```

If you want to update the configuration of an exiting function you can use the
`update-function-configuration` command to set it's values

- For example in this case we increase the memory of a lambda to `256` megabytes

```sh
aws lambda update-function-configuration \
  --function-name my-new-function \
  --memory-size 256
```

Lastly, we can delete our recently created lambda function with the `delete-function`
sub-command

```sh
aws lambda delete-function --function-name my-new-function
``` 

### Deploying a container image as a lambda function

This enables you to pair the flexibility of containerinaztion with the operation
simplicity of lambdas, this hase some benefits:
  - You get to use your familiar container tooling
  - Dependency managment works by creating an inmutable container with all your
    wrapped dependencies
  - You can use your prefere based linux image (not only amazon linux)
  - Since container images are inmutable, you can feel confident that your
    functions are consistent amongst any enviroment you deploy to
    - With this comes more responsability, since `aws` can't perform automatic `os`
      and `runtime` updates and patching
    - Any change to the image requires a seperate re-deployment step
  - The deployment lambda can handle know up to `10G` for the container image
    - We optimize and cach the loading of the images to reduce cold starts
  - Your code now is more portable to use in multiple enviroments and `aws` services

You build your images and push them to the Amazon Elastic Container Registry (`ECR`)
which is a fully managed container registry

`AWS` lambda provides a variety of curated based images for each runtime, which
includes the code to make it work with lambda

In this example:
  - We use a node js base image
  - Copy the function code
  - Install dependecies
  - Set the handler method

```dockerfile
FROM public.ecr.aws/lambda/nodejs:18
COPY app.js package*.json ./
RUN npm install
CMD ["app.lambdaHandler"]
```

Having this base `docker file` we first start by building it

```sh
docker build -t my-docker-lambda:latest .
```

You can then use `docker run` to run the container locally to test the 
functionality, this runs a **local lambda emulator** which is included
as part of the lambda base image

```sh
docker run -p 9000:8080 my-docker-lambda:latest
```

We can then [curl](./frnd.md) this local endpoint to invoke the function and
see the hello world

```sh
curl -XPOST "http://localhost:9000/2015-03-31/functions/function/invocations" -d '{}'
```

Then, you have to upload the image to `ECR`, so use `docker tag` to set the image
information and then `docker push` to push the image to the registry

```sh
docker tag \
  my-docker-lambda \
  97848024274.dkr.ecr.us-east-1.amazonaws.com/my-docker-lambda:latest

docker push \
  97848024274.dkr.ecr.us-east-1.amazonaws.com/my-docker-lambda:latest
```

Finally, you can use the `create-function` comand from the `cli` to create a new
lambda function based on your recently pushed image, especifying the package type
as `Image` and pointed to the `ECR` image

```sh
aws lambda create-function \
  --region us-east-1 \
  --function-name my-docker-lambda \
  --package-type Image \
  --code ImageUri=97848024274.dkr.ecr.us-east-1.amazonaws.com/my-docker-lambda:latest \
  --role arn:aws:iam:9783923742:role/my-new-role
```

Now we can test it by invoking the function in the cloud and see the result

```sh
aws lambda invoke --function-name my-docker-lambda --region us-east-1 result.json
# {
#   "StatusCode": 200,
#   "ExecutedVersion": "$LATEST"
# }

cat ./result.json
# {"statusCode": 200, "body": "{\"message\": \"hello world\"}"}
```
