---
title: "Prerequisites"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

#### Requirements before starting

To complete this workshop, you need:

1. **AWS Account** with Administrator privileges or sufficient permissions to create the following services:
   - IAM, S3, DynamoDB, Cognito, SQS, Lambda, API Gateway, WAF, CloudFront, Route 53, ACM, CloudWatch, SNS

2. **OpenAI API Key**: Register at [platform.openai.com](https://platform.openai.com/) to use Speech-to-Text and GPT evaluation

3. **Region**: This workshop uses **ap-southeast-1 (Singapore)** for most services
   - **Important**: ACM SSL Certificate must be created in **us-east-1** for use with CloudFront

4. **Alert email**: To receive notifications from SNS

5. **(Optional) Custom domain**: If you want to use a domain like `itcoach24h.xyz` instead of CloudFront's default domain
   - Can purchase domain at Namecheap, GoDaddy, or Route 53 (~$2-3/year)

#### Progress Checklist

In this workshop, you will create the following resources:

| # | Service | Details | Status |
|---|---------|---------|--------|
| 1 | IAM Role | `itcoach-lambda-role` | ⬜ |
| 2 | S3 - Static Assets | `itcoach-static-assets` | ⬜ |
| 3 | S3 - Audio Upload | `itcoach-audio-upload` | ⬜ |
| 4 | DynamoDB | 8 tables | ⬜ |
| 5 | Cognito | User Pool + App Client | ⬜ |
| 6 | SQS | 2 queues (Main + DLQ) | ⬜ |
| 7 | Lambda | 8 functions | ⬜ |
| 8 | API Gateway | 8 endpoints + Throttling | ⬜ |
| 9 | AWS WAF | 2 Web ACLs (CloudFront + API Gateway) | ⬜ |
| 10 | CloudFront | Distribution + Error Pages | ⬜ |
| 11 | Route 53 | DNS + Domain `itcoach24h.xyz` | ⬜ |
| 12 | ACM | SSL Certificate | ⬜ |
| 13 | SNS + CloudWatch | Monitoring + Alerts | ⬜ |

#### Important Information to Save

During the workshop, you will need to save the following information for use in subsequent steps:

| Information | Created in Step | Used For |
|-------------|----------------|----------|
| **IAM Role ARN** | 5.3 - IAM Role | Lambda functions |
| **S3 Static Bucket Name** | 5.4 - S3 Buckets | CloudFront origin |
| **S3 Audio Bucket Name** | 5.4 - S3 Buckets | Lambda env vars |
| **DynamoDB Table Names** | 5.5 - DynamoDB | Lambda env vars (8 tables) |
| **Cognito User Pool ID** | 5.6 - Cognito | API Gateway authorizer |
| **Cognito App Client ID** | 5.6 - Cognito | Frontend config |
| **SQS Queue URL** | 5.7 - SQS | Lambda env vars |
| **Lambda Function ARNs** | 5.8 - Lambda | API Gateway integration |
| **API Gateway URL** | 5.9 - API Gateway | Frontend config |
| **CloudFront Domain** | 5.10 - CloudFront | Cognito callback URL |
| **ACM Certificate ARN** | 5.11 - Route 53 | CloudFront SSL |
| **Route 53 Hosted Zone** | 5.11 - Route 53 | DNS management |


#### Cost Estimation

For trial usage (< 1000 requests/month), estimated cost:

| Service | Cost/month | Notes |
|---------|-----------|-------|
| AWS Lambda | ~$0.00 | Free tier: 1M requests |
| DynamoDB | ~$0.00 | Free tier: 25GB |
| S3 | ~$0.05 | Static + audio files |
| API Gateway | ~$0.01 | ~1,000 requests |
| CloudFront | $0.00 | Free tier |
| AWS WAF – CloudFront | $0.00 | Included in 5 free rules with CloudFront Free plan |
| AWS WAF – API Gateway | ~$10–15 | Regional Web ACL, not covered by any free tier |
| Cognito | $0.00 | Free tier: 50,000 MAU |
| SQS | ~$0.00 | Free tier: 1M requests |
| Polly | ~$0.04 | ~100,000 characters |
| CloudWatch | ~$1–5 | Logs + Alarms |
| SNS | ~$0.00 | Free tier |
| Route 53 | ~$0.50 | Hosted Zone $0.50/month |
| ACM | $0.00 | Completely free |
| **Total AWS** | **~$12–20/month** | |
| **OpenAI API** | ~$1–$5 | Depends on evaluation volume |
| **Total with OpenAI** | **~$13–25/month** | |

**One-time cost:**
- Domain `itcoach24h.xyz`: ~$2-3/year (if purchasing custom domain)


#### Ready to Start

After you have prepared everything, move to the next step to start creating IAM Role.

