# cli.aws.lambda

You can use it deploy and configure lambda functions from the command line

## Synopsis

It interacts with the `lambda` API

```sh
aws lambda [sub-comands] [options]
```

## Overview

### Options

- `create-function`: The sub-command to create a new lambda function
  - `--function-name`: The `aws` name of the new function
  - `--zip-file`: The source [zip](./kg1a.md) file for the lambda code
  - `--handler`: The name for the entry point function handler
  - `--runtime`: The language runtime on which the function will run
  - `--role`: The `ARN` of the role to be assigned to the lambda

- `invoke`: Calls for the execution of an `aws` lambda function
  - `--function-name`: The `aws` name of the function to be called
  - `--log-type`: ?
  - `--query`: ?
  - `--output`: In what format to output the response

- `update-function-configuration`: Update the configuration of an exiting lambda
  - `--function-name`: The `aws` name of the lambda function to update
  - `--memory-size`: Update the memory size to the specified value

- `delete-function`: Delete an exiting lambda function
  - `--function-name`: The `aws` name of the lambda to be deleted

## Cookbook

### Create a new function based on zip file

You can create a new function with the `create-function` sub-command, this
will create a new lambda function from an exiting `zip`, it will upload it
to [s3](./2s8v.md) and make it ready to be invoked

```sh
aws lambda create-function 
  --function-name my-new-function \
  --zip-file ./function.zip \
  --handler index.handler \
  --runtime nodejs18.x \
  --role arn:aws:iam:9783923742:role/my-new-role
```

### Invoke the execution of an existing lambda

You can execute a lambda function using the `invoke` sub-command, you only need
to pass it the `aws` lambda name of the function and a response output file

- In this case we decode the logs as [base64](./nlre.md) encoded text

```sh
aws lambda invoke \
  --function-name my-new-function out \
  --log-type Tail \
  --query 'LogResult' \
  --output text | base64 -d
```

### Update the configuration of an existing lambda

You can use the `update-function-configuration` sub-command to update the configuration of a
of an existing function, you just pass the parameters to configure as `flag options`

- For example in this case we increase the memory of a lambda to `256` megabytes

```sh
aws lambda update-function-configuration \
  --function-name my-new-function \
  --memory-size 256
```

### Delete an exiting function

You can delete an exiting function with the `delete-function` sub-command, you just
need to pass it the `aws` lambda name

> Be careful when deleting functions not to delete a running function or one
> in a production environment

```sh
aws lambda delete-function --function-name my-new-function
``` 
