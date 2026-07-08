---
title: "Introduction"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

#### Introduction to ITCoach

ITCoach is an AI-powered intelligent IT interview practice platform that helps IT students and entry-level professionals develop real interview skills. The platform is built entirely on AWS Serverless architecture, ensuring:

- **No server management**: Lambda automatically processes and scales
- **Low cost**: Pay-per-use, only pay when used
- **High performance**: CloudFront global distribution
- **Strong security**: Cognito and IAM access management

#### Prerequisites

To complete this workshop, you need:

1. **AWS Account** with Administrator privileges or sufficient permissions to create the following services:
   - IAM, S3, DynamoDB, Cognito, SQS, Lambda, API Gateway, CloudFront, Route 53, ACM, CloudWatch, SNS

2. **OpenAI API Key**: Register at [platform.openai.com](https://platform.openai.com) to use Speech-to-Text and GPT evaluation (**Important**: must have at least **$5** credit)

3. **Region**: This workshop uses **ap-southeast-1 (Singapore)** for most services
   - **Important**: ACM SSL Certificate must be created in **us-east-1** for use with CloudFront

#### Key Features

**1. Diverse practice formats:**
- Multiple-choice quizzes with Spaced Repetition SM-2
- Essay text input or voice recording
- Real interview simulation with AI

**2. Smart AI evaluation:**
- OpenAI API converts speech to text
- AI scores and provides detailed feedback
- Amazon Polly reads feedback with voice

**3. Gamification:**
- XP, level, badge system
- Continuous learning streaks
- Competitive leaderboard

**4. Personal dashboard:**
- Track learning progress
- Analyze weaknesses
- Recommend priority review content

#### System Architecture

In this workshop, you will build a system with the following components:

- **Frontend**: React + TypeScript on S3 + CloudFront
- **Backend**: 8 Lambda functions
- **Database**: 8 DynamoDB tables
- **Authentication**: Amazon Cognito
- **Message Queue**: Amazon SQS
- **Security**: AWS WAF (2 Web ACLs for CloudFront and API Gateway)
- **DNS & SSL**: Route 53 + ACM
- **Monitoring**: CloudWatch + SNS

![ITCoach Architecture](/images/ITCoachArchitecture.png)

*Note: The diagram groups Lambda functions logically for clarity:*
- *"**AWS Lambda (8 functions)**" in the diagram represents 7 sync Lambda functions: `auth-handler`, `question-handler`, `session-handler`, `answer-handler`, `quiz-handler`, `gamification-handler`, `leaderboard-handler`*
- *"**itcoach-ai-processor**" is the 8th async Lambda function, processing heavy AI tasks via SQS*
- *In actual deployment, each function is created separately (best practice: least privilege, cold start optimization, easier debugging)*

#### Main Processing Flow

```
User (Browser)
    ↓ HTTPS – itcoach24h.xyz
Amazon Route 53 (DNS)
    ↓
AWS WAF (CloudFront - Global) ← Block SQL Injection, XSS, DDoS
    ↓
Amazon CloudFront (CDN) ←→ S3 Static (React + TypeScript)
    ↓
AWS WAF (API Gateway - Regional) ← Rate limiting /auth endpoint
    ↓
Amazon API Gateway (8 endpoints, Throttling: 100 req/s)
    ↓ Cognito Authorizer
AWS Lambda (8 functions)
    ├──→ DynamoDB (8 tables)
    ├──→ S3 Audio (Presigned URL)
    ├──→ SQS (Async Processing)
    │      ↓
    │   itcoach-ai-processor
    │      ├──→ OpenAI API (STT + Evaluation)
    │      └──→ Amazon Polly (Text-to-Speech)
    └──→ CloudWatch → SNS (Alerts)
```

#### Estimated Time

- **AWS infrastructure setup**: 1-2 hours
- **Code deployment (after development)**: 30 minutes
- **Testing and verification**: 30 minutes

**Total time**: 2-3 hours

