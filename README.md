# AWS Cloud Formation Deployment for Subscriber Validation and Processing
This repository contains the Template and codes for deploying a serverless application that validates and processes subscriber data using API Gateway, Lamba Functions, SQS, S3 and DynamoDB. 

## Architecture Overview
1. API Gateway: Accepts incoming subscriber data via a POST request.
2. LambdaFunction1: 'validateSubscribers': Validates the schema ofincoming subscribers data
    * Valid Data: sent to SQS queue
    * Invalid Data: stored in s3 bucket for further processing
4. LambdaFunction2: ProcessValidSubscribers': Pool the SQS queue, checks for duplicate and insert new entries into DynamoDB
5. ![arichtectural diagram.drawio](https://hackmd.io/_uploads/r18zd6h5C.png)

## Prerequisites
Ensure you have the following installed and configured:
* [AWS CLI](https://aws.amazon.com/cli/)
* [AWS Account](https://aws.amazon.com) "you need to have the necessary IAM permission to create and manage resources"

## Permissions to have
1. write logs to cloudwatch (for Lamda functions, it will help you debug)
2. put and read from SQS
3. put into s3 bucket (you could include an optional read from s3bucket if you want to append current file with newer information)
4. read and put into dynamoDB


