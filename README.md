# BAO_CodeChallenge
This is a repository to implement messaging subscribers validation and processing using AWS serverless services for validating entry and processing entry
AWS CloudFormation Deployment for Subscriber Validation and Processing
This repository contains the CloudFormation template for deploying a serverless application that validates and processes subscriber data using API Gateway, Lambda functions, SQS, S3, and DynamoDB.

Architecture Overview
API Gateway: Accepts incoming subscriber data via a POST request.
Lambda Function 1: validateSubscribers: Validates the schema of incoming subscriber data.
Valid Data: Sent to an SQS queue.
Invalid Data: Stored in an S3 bucket.
Lambda Function 2: processValidSubscribers: Polls the SQS queue, checks for duplicates, and inserts new entries into DynamoDB.
Prerequisites
Ensure you have the following installed and configured:

AWS CLI
AWS Account with the necessary IAM permissions to create and manage resources.
Deployment Instructions
Step 1: Upload the CloudFormation Template to S3
Upload the template.yaml file to an S3 bucket:
bash
Copy code
aws s3 cp template.yaml s3://your-bucket-name/
Replace your-bucket-name with the name of your S3 bucket.
Step 2: Create the CloudFormation Stack
Deploy the stack using the AWS CLI:

bash
Copy code
aws cloudformation create-stack --stack-name YourStackName \
--template-url https://s3.amazonaws.com/your-bucket-name/template.yaml \
--capabilities CAPABILITY_IAM CAPABILITY_NAMED_IAM
Replace YourStackName with your desired stack name and adjust the S3 URL accordingly.

Monitor the stack creation:

Use the AWS Management Console or the AWS CLI to monitor the progress:
bash
Copy code
aws cloudformation describe-stacks --stack-name YourStackName
Step 3: Retrieve Stack Outputs
After the stack is created, retrieve the outputs (API Gateway URL, SQS Queue URL, etc.) using:

bash
Copy code
aws cloudformation describe-stacks --stack-name YourStackName --query 'Stacks[0].Outputs'
This will provide all the necessary information to interact with your deployed resources.

Step 4: Testing the Application
Submit Subscriber Data:

Use an API client like Postman or curl to submit data to the API Gateway endpoint.
Example Request:
bash
Copy code
curl -X POST https://<API_ENDPOINT>/subscribe -H "Content-Type: application/json" -d '{"name": "John Doe", "email": "john.doe@example.com"}'
Monitor Lambda Logs:

View the logs of your Lambda functions using AWS CloudWatch to verify that data is processed correctly.
Step 5: Cleanup
To delete the stack and all associated resources, run:

bash
Copy code
aws cloudformation delete-stack --stack-name YourStackName
This will remove all the resources created by this stack.

License
This project is licensed under the MIT License. See the LICENSE file for details.
