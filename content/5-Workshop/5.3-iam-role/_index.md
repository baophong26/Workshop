---
title: "Create IAM Role for Lambda"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

#### Introduction to IAM Role

IAM Role is an identity in AWS with permission policies that determine what that identity can and cannot do in AWS. Lambda functions need an IAM Role to access other AWS services like DynamoDB, S3, SQS, Polly, and CloudWatch.

In this step, we will create a single IAM Role that all 8 Lambda functions will share.

#### Steps to Perform

**1. Access IAM Console**

- Log in to AWS Console
- Search for **IAM** service in the search bar
- Click on **IAM** to open IAM Dashboard

**2. Create New Role**

- In the left menu, click on **Roles**
- Click **Create role** button

**3. Select Trusted Entity Type**

- Trusted entity type: select **AWS service**
- Use case: select **Lambda**
- Click **Next**

**4. Add Permissions Policies**

On the Add permissions page, search and check the following 6 policies:

| Policy Name | Purpose |
|------------|---------|
| `AWSLambdaBasicExecutionRole` | Write logs to CloudWatch |
| `AmazonDynamoDBFullAccess` | Read/write DynamoDB |
| `AmazonS3FullAccess` | Upload/download S3 |
| `AmazonSQSFullAccess` | Send/receive SQS messages |
| `AmazonPollyFullAccess` | Text-to-Speech |
| `CloudWatchFullAccess` | Monitoring and logs |

Quick search method:
- Type policy name in **Search** box
- Check the checkbox next to policy name
- Repeat for all 6 policies

![Add Permissions](/images/5-Workshop/5.3-iam-role/001-add-permissions.png)

After selecting all 6 policies, click **Next**

**5. Name and Create Role**

- Role name: `itcoach-lambda-role`
- Description: `IAM role for ITCoach Lambda functions with access to DynamoDB, S3, SQS, Polly, and CloudWatch`
- Review the 6 selected policies
- Click **Create role**

**6. Save Role ARN Information**

After creation, you will see a success message.

- Click on the newly created role name `itcoach-lambda-role`
- Copy **Role ARN** (format: `arn:aws:iam::ACCOUNT_ID:role/itcoach-lambda-role`)
- Save this ARN, it will be used when creating Lambda functions

![Role ARN](/images/5-Workshop/5.3-iam-role/002-role-arn.png)

#### Result

✅ You have successfully created IAM Role `itcoach-lambda-role` with all necessary permissions.

#### Information to Save

```
Role Name: itcoach-lambda-role
Role ARN: arn:aws:iam::[ACCOUNT_ID]:role/itcoach-lambda-role
```


#### Explanation of Permissions

| Permission | Why Needed |
|-----------|-----------|
| **LambdaBasicExecutionRole** | Allows Lambda to write logs to CloudWatch Logs for debugging |
| **DynamoDBFullAccess** | Lambda needs to read/write 8 DynamoDB tables (users, questions, sessions, etc.) |
| **S3FullAccess** | Lambda needs to create Presigned URLs for S3 audio bucket |
| **SQSFullAccess** | Lambda sends messages to SQS queue for asynchronous AI processing |
| **PollyFullAccess** | Lambda `itcoach-ai-processor` needs to call Polly for text-to-speech |
| **CloudWatchFullAccess** | Lambda writes metrics and creates custom alarms |


#### Next Step

Move to the next step to create S3 Buckets.

