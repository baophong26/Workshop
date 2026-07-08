---
title: "Cleaning up Resources"
date: 2024-01-01
weight: 15
chapter: false
pre: " <b> 5.15. </b> "
---

#### Why cleanup?

After completing the workshop, you should clean up resources to:
- Avoid unexpected charges
- Keep AWS account clean
- Learn how to manage resource lifecycle


#### Cleanup Order

### 1. Delete CloudFront Distribution

- CloudFront → Distributions
- Select `itcoach-distribution`
- **Disable** distribution first (wait 5-10 minutes)
- After disabled → **Delete**


### 2. Delete AWS WAF Web ACLs (2 Web ACLs)

**⚠️ Important:** Must delete WAF **after** disabling CloudFront and before deleting API Gateway

**2.1. Delete WAF CloudFront (us-east-1):**
- Switch region to **us-east-1**
- WAF & Shield → Web ACLs
- Select `itcoach-cloudfront-waf`
- **Delete**

**2.2. Delete WAF API Gateway (ap-southeast-1):**
- Switch region to **ap-southeast-1**
- WAF & Shield → Web ACLs
- Select `itcoach-api-waf`
- **Delete**


### 3. Delete API Gateway

- API Gateway → APIs
- Select `itcoach-api`
### 3. Delete API Gateway

- API Gateway → APIs
- Select `itcoach-api`
- **Actions** → **Delete API**
- Confirm deletion


### 4. Delete Lambda Functions (8 functions)

- Lambda → Functions
- Select each function → **Actions** → **Delete**
- Repeat for all 8 functions


### 5. Delete SQS Queues (2 queues)

- SQS → Queues
- Select `itcoach-processing-queue` → **Delete**
- Select `itcoach-dlq` → **Delete**


### 6. Delete Cognito User Pool

- Cognito → User pools
- Select user pool → **Delete**
- Enter pool name to confirm


### 7. Delete DynamoDB Tables (8 tables)

- DynamoDB → Tables
- Select each table → **Delete**
- Repeat for all 8 tables



### 8. Delete S3 Buckets (2 buckets)

**Important:** Must **empty bucket first** before deleting

- S3 → Buckets
- Select `itcoach-static-assets`
- **Empty** bucket (delete all objects)
- After empty → **Delete** bucket
- Repeat for `itcoach-audio-upload`



### 9. Delete IAM Role

- IAM → Roles
- Find `itcoach-lambda-role`
- **Delete** role


### 10. Delete SNS Topic and Subscription

- SNS → Topics
- Select `itcoach-alerts` → **Delete**
- Subscriptions will be automatically deleted


### 11. Delete CloudWatch Alarms (if created)

- CloudWatch → Alarms
- Select all related alarms → **Delete**

#### Cleanup Checklist

| # | Resource | Status |
|---|----------|--------|
| 1 | CloudFront Distribution | ⬜ |
| 2 | AWS WAF Web ACLs (2) | ⬜ |
| 3 | API Gateway | ⬜ |
| 4 | Lambda Functions (8) | ⬜ |
| 5 | SQS Queues (2) | ⬜ |
| 6 | Cognito User Pool | ⬜ |
| 7 | DynamoDB Tables (8) | ⬜ |
| 8 | S3 Buckets (2) | ⬜ |
| 9 | IAM Role | ⬜ |
| 10 | SNS Topic | ⬜ |
| 11 | CloudWatch Alarms | ⬜ |

#### Verify Cleanup Complete

Check each service to ensure no remaining resources:

```
✅ CloudFront: 0 distributions
✅ WAF: 0 Web ACLs
✅ API Gateway: 0 APIs
✅ Lambda: 0 functions (except your other functions)
✅ SQS: 0 related queues
✅ Cognito: 0 related user pools
✅ DynamoDB: 0 related tables
✅ S3: 0 related buckets
✅ IAM: Role itcoach-lambda-role deleted
✅ SNS: Topic itcoach-alerts deleted
```

#### Conclusion

Congratulations! You have completed the ITCoach workshop on AWS Serverless! 🎉

What you have learned:
- ✅ Set up IAM roles and permissions
- ✅ Configure S3 for static hosting and private storage
- ✅ Create and manage 8 DynamoDB tables
- ✅ User authentication with Cognito
- ✅ Asynchronous processing with SQS
- ✅ Build 8 serverless Lambda functions
- ✅ Create REST API with API Gateway
- ✅ Global CDN distribution with CloudFront
- ✅ Monitoring with CloudWatch and SNS
- ✅ Proper resource cleanup

**This knowledge can be applied to many other Serverless projects!**
