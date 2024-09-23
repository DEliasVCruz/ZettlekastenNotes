# cloud.aws.lambda

An `aws` service to run code on the cloud withouth having to manage servers

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

Aws manages everything related to:
  - High availability and security
    - They run automatically acros multiple availabitily zones within a region
    - You don't have to manage multy `AZ` deployments
  - Automatic scalling to meed your needs

Most importantly you only pay for what's been used (`compute`) and get no charges
for idle instances
  - When the code is `invoked` you are billed in **1 milisecond** increments

The code that runs in your lambda is called a `lambda function`
  - You can run code in **any language** or provide a **custom runtime** to run on
  - Are automatically load balanced
  - They handle failures (retries)
  - Are isolated from each other in a secure way
  - They provide monitoring and logging

They run in response to events:
  - After you upload your code to lambda, you can configure an `event source`
  - There are over **200** integrations for event sources, like:
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

### The programing model of lambda functions

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
  - `event`: Contains all the data and metadata the lambda nees to run, depending
    on which source created it

    For example, an event created by `api gateway` contains details related to the
    request that the `api client` made, like the `path`, `query string` and `request body`

    Other event created by `s3` when a new object is created includes details about
    the bucket name and the new object

    It can then use this to handle the request, like access the path of the `s3`
    new object to donwload it

  - `context`: This allows to interact with the lambda execution environments and
    contains a number of properties and methods

    You can get information like the `name` and `version` of the function or
    things like `request id` to track especific invokatons, the amount of time
    in miliseconds remaining before a function time outs, `logs`, etc.
  

Subsequent invokations of a lambda that has already been initialized will not
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

### Deploying a (zip) lambda using the aws cli

You should first [create an iam execution role](./8o8o.md) to be `assumed` by the 
lambda when executing, so that it have permission to access `aws resources`,
you can do this with the `aim creat-role` comand

- In this example we use an inline trust policiy

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

Then you have to [zip](./kg1a.md) the lambda code along all it's dependecies, you have
to use your langugage of choice native package manager

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

Finally we can invoke our function and view it's response and logs with the
`invoke function` sub-command of the `lambda` command

- In this case we decode the logs as `base64` encoded text

```sh
aws lambda invoke \
  --function-name my-new-function out \
  --log-type Tail \
  --query 'LogResult' \
  --output text | base64 -d
```
