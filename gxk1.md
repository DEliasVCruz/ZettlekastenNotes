# cli.aws.lambda

You can use it deploy and configure lambda functions from the comand line

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
  - `--handler`: The name for the entry point funciton handler
  - `--runtime`: The language runtime on which the function will run
  - `--role`: The `ARN` of the role to be assigned to the lambda

- `invoke`: Calls for the execution of an aws lambda function
  - `--function-name`: The `aws` name of the function to be called
  - `--log-type`: ?
  - `--query`: ?
  - `--output`: In what format to ouput the response

## Cookbook

### Create a new function based on zip file

You can create a new function with the `create-function` sub-command, this
will create a new lambda function from an exitign `zip`, it will upload it
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

You can execute a lambda funtion using the `invoke` subcommand, you only need
to pass it the `aws` lambda name of the function and a response output fiile

- In this case we decode the logs as `base64` encoded text

```sh
aws lambda invoke \
  --function-name my-new-function out \
  --log-type Tail \
  --query 'LogResult' \
  --output text | base64 -d
```
