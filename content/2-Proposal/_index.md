---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# ITCoach – AI-Powered IT Interview Practice Platform
## AWS Serverless Solution for IT Students' Interview Skills Training

## 1. Executive Summary

ITCoach is a web platform that helps IT students and entry-level professionals practice technical knowledge, develop interview response skills, and simulate real interview environments with AI support. The goal is to help students increase their chances of passing Internship, Fresher, and Junior recruitment rounds at technology companies.

The platform supports diverse practice formats: single or multiple-choice quizzes with Spaced Repetition (SM-2) mechanism, essay-style voice recording answers, and simulated real interview sessions. AI provides detailed evaluation for each answer, points out gaps, suggests improvements, and responds with voice feedback via Amazon Polly. A Gamification system with XP, levels, streaks, and leaderboards helps increase learning motivation.

The system is built entirely on Amazon Web Services using Serverless Architecture. The frontend uses React + TypeScript distributed via Amazon CloudFront, backend processing by AWS Lambda, data storage on Amazon DynamoDB, and integrates OpenAI API for answer evaluation and Amazon Polly for voice generation.

## 2. Problem Statement

### Current Issues

IT students and entry-level professionals often lack realistic interview practice environments:

- Traditional quiz websites only test theory, do not evaluate articulation ability
- No tools evaluate essay or voice answers with detailed AI feedback
- No environment simulates real interviews by specialty
- Difficult to identify personal weaknesses to focus practice efforts properly
- Foreign platforms have language barriers, high costs, inadequate fit for Vietnamese IT market

### Solution

ITCoach addresses these issues with core features:

- **Multi-specialty Question Bank:** 10 IT specialties, each divided into multiple topics
- **Smart Quizzes:** Single or multiple-choice quizzes applying Spaced Repetition SM-2 for optimal review timing
- **Voice Essay Practice:** Voice recording, AI evaluates and provides sample answers with voice feedback
- **Flexible Practice:** Choose 1 essay question OR 1 specialty (3-5 random questions), default duration per question
- **Dashboard & Gamification:** Track progress, XP, level, badges, streaks, and real-time leaderboard to increase learning motivation

### AWS Infrastructure

- **Amazon CloudFront + S3** distributes React + TypeScript globally at high speed
- **Amazon Cognito** secures user authentication
- **Amazon API Gateway + AWS Lambda** processes all serverless business logic
- **Amazon DynamoDB** stores all system data (8 tables)
- **Amazon S3 (Audio)** stores audio recordings and Polly audio via Presigned URL
- **Amazon SQS** asynchronously processes heavy AI tasks
- **OpenAI API** Speech-to-Text + answer quality evaluation
- **Amazon Polly** reads questions and responds with voice feedback
- **AWS WAF** protects CloudFront and API Gateway from web attacks (SQLi, XSS, DDoS)
- **Amazon CloudWatch + SNS** monitors system and sends automatic alerts
- **Amazon Route 53 + ACM** manages DNS and SSL certificate for domain `itcoach24h.xyz`

### Benefits

- Students have realistic IT interview practice environment with instant AI feedback like a mentor
- Spaced Repetition enables effective memorization, system automatically identifies individual weaknesses
- No server management needed, automatically scales to demand thanks to Serverless architecture
- Low operational costs, easy to add new specialties and questions in the future

## 3. Solution Architecture

The platform applies AWS Serverless architecture with AWS Lambda as the business logic processing center.

![ITCoach Architecture](/images/ITCoachArchitecture.png)

*Note: The diagram groups Lambda functions logically for clarity:*
- *"**AWS Lambda (8 functions)**" in the diagram represents 7 sync Lambda functions: `auth-handler`, `question-handler`, `session-handler`, `answer-handler`, `quiz-handler`, `gamification-handler`, `leaderboard-handler`*
- *"**itcoach-ai-processor**" is the 8th async Lambda function, processing heavy AI tasks via SQS*
- *In actual deployment, each function is created separately (best practice: least privilege, cold start optimization, easier debugging)*

### Main Processing Flow

```
User (Browser)
    ↓ HTTPS – itcoach24h.xyz
Amazon Route 53 (DNS)
    ↓
Amazon CloudFront (CDN) ←→ S3 Static (React + TypeScript)
    ↓
Amazon API Gateway (8 endpoints, Throttling: 100 req/s)
    ↓ Cognito Authorizer
AWS Lambda (8 functions)
    ├──→ Amazon DynamoDB (8 tables)
    ├──→ Amazon S3 Audio (Presigned URL Upload)
    ├──→ Amazon SQS (Async Processing)
    │         ↓
    │    itcoach-ai-processor
    │         ├──→ OpenAI API (STT + AI Evaluation)
    │         └──→ Amazon Polly (Text-to-Speech)
    └──→ Amazon CloudWatch → Amazon SNS (Alerts)
```

### AWS Services Used

| Service | Purpose |
|---------|---------|
| Amazon CloudFront | CDN distributes React + TypeScript globally via HTTPS |
| Amazon S3 (Static) | Stores React + TypeScript build files |
| Amazon S3 (Audio) | Stores audio recordings and Polly audio files |
| Amazon API Gateway | 8 endpoints, integrates Cognito Authorizer, Throttling (100 req/s) |
| Amazon Cognito | Registration, login, user session management |
| AWS Lambda | 8 functions process all backend business logic |
| Amazon DynamoDB | 8 tables store all system data |
| Amazon SQS | Queue for asynchronous AI and audio processing |
| Amazon Polly | Responds with voice feedback for sample answers |
| OpenAI API | Speech-to-Text + answer quality evaluation |
| AWS WAF | Protects CloudFront and API Gateway from web attacks |
| Amazon CloudWatch | Monitors logs, metrics, system performance |
| Amazon SNS | Sends email alerts when system errors occur |
| Amazon Route 53 | Manages DNS for domain `itcoach24h.xyz` |
| AWS ACM | Free SSL certificate for HTTPS |

## 4. Detailed Features

### 4.1. Target Users

- IT students in year 2, 3, or final year
- Students preparing for Internship/Fresher applications
- Career changers wanting to practice technical interviews
- Working professionals reviewing knowledge before interviews

### 4.2. Supported Specialties

| # | Specialty |
|---|-----------|
| 1 | Front-end Developer |
| 2 | Back-end Developer |
| 3 | Full-stack Developer |
| 4 | DevOps Engineer |
| 5 | Mobile Developer |
| 6 | QA/QC Engineer |
| 7 | Data Engineer |
| 8 | Data Analyst |
| 9 | AI/Machine Learning Engineer |
| 10 | Cyber Security |

### 4.3. Practice Formats

**Quiz (Multiple Choice):**
- Single or multiple correct answers
- Spaced Repetition SM-2 algorithm automatically calculates `nextReviewDate` for optimal review timing
- Earn XP after each correct answer

**Essay:**
- Voice recording only
- OpenAI STT converts voice to text
- AI scores, points out missing ideas, suggests improvements, provides sample answers
- Polly reads sample answers with voice

### 4.4. Voice Practice Module

- Choose 1 essay question OR 1 specialty (3-5 random questions)
- Default duration per question
- User responds with voice
- AI evaluates and reads sample answers with voice (Polly)

### 4.5. Dashboard & Gamification

- Learning progress by topic, completion rate, average score
- Daily study streak, daily history
- XP, Level, Badge achievement system
- Real-time leaderboard updates

## 5. Technical Implementation

### Lambda Functions – 8 functions

| Function | Task |
|----------|------|
| `itcoach-auth-handler` | Registration, login, profile management |
| `itcoach-question-handler` | Retrieve essay questions + topic lists by specialty |
| `itcoach-session-handler` | Create and manage Mock Interview sessions |
| `itcoach-answer-handler` | Receive essay answers, create Presigned URL for audio upload |
| `itcoach-ai-processor` | OpenAI STT + evaluation + Polly TTS (async from SQS) |
| `itcoach-result-handler` | Return results, scores, history, dashboard statistics |
| `itcoach-quiz-handler` | Quiz multiple choice, SM-2, add XP to gamification |
| `itcoach-gamification-handler` | XP, level, streak, leaderboard management |

### DynamoDB – 8 tables

| Table | Partition Key | Sort Key | Index | Used For |
|-------|--------------|----------|-------|----------|
| `itcoach-users` | `userId` | - | - | User information |
| `itcoach-questions` | `questionId` | - | `category-index` | Quiz + Essay shared |
| `itcoach-sessions` | `sessionId` | - | `userId-index` | Mock Interview sessions |
| `itcoach-answers` | `answerId` | - | `sessionId-index` | Answers + AI feedback |
| `itcoach-history` | `userId` | `timestamp` | - | Learning history |
| `itcoach-topics` | `specialty` | `topicId` | - | Topics by specialty |
| `itcoach-quiz-attempts` | `userId` | `questionId` | - | Spaced Repetition SM-2 |
| `itcoach-gamification` | `userId` | - | `xp-index` | XP, level, streak, badge |

### API Gateway – 8 endpoints

| Endpoint | Method | Used For |
|----------|--------|----------|
| `/auth` | POST | Login/registration (public) |
| `/questions` | GET | Retrieve essay questions |
| `/topics` | GET | Retrieve topics by specialty |
| `/sessions` | POST | Create Mock Interview session |
| `/answers` | POST | Submit essay answer |
| `/results` | GET | View results + history |
| `/quiz` | POST | Submit quiz + Spaced Repetition |
| `/leaderboard` | GET | XP leaderboard |

## 6. Timeline & Milestones

### Phase 1 – Infrastructure & Backend
Build entire AWS infrastructure, write 8 Lambda functions, integrate OpenAI and Polly.

### Phase 2 – Frontend & Integration
Build React + TypeScript interface: auth, quiz, essay, recording, Mock Interview, dashboard, gamification.

### Phase 3 – Data & Finalization
Import question bank (prioritize Frontend, Backend, Foundation Knowledge), test entire flow, fix bugs, official deployment.

| Phase | Timeline | Content |
|-------|----------|---------|
| Preparation | Pre-internship | Form team, assign roles |
| Month 1 – Month 2 | Internship | Learn theory, master AWS, Serverless, React + TypeScript knowledge |
| Month 3 – Week 1 | Internship | Build AWS infrastructure: S3, DynamoDB, API Gateway, Cognito |
| Month 3 – Week 2 | Internship | Backend dev: 8 Lambda functions + OpenAI + Polly |
| Month 3 – Week 3 | Internship | Frontend dev: auth, quiz, essay, Mock Interview, dashboard, gamification |
| Month 3 – Week 4 | Internship | Integration, test entire flow, bug fixes, import question data, deploy, demo |

## 7. Budget Estimation

### AWS Costs/month

| Service | Estimate | Notes |
|---------|---------|-------|
| AWS Lambda | ~$0.00 | Free tier 1M requests + 400,000 GB-s/month (permanent) |
| Amazon DynamoDB | ~$0.00–1 | On-demand, free tier 25GB |
| Amazon S3 | ~$0.05–1 | Static + audio files, grows with accumulated audio storage |
| Amazon API Gateway | ~$0.01–2 | $3.5/million requests |
| Amazon CloudFront | $0.00 | Free plan (1TB + 10 million requests/month) |
| AWS WAF – CloudFront | $0.00 | Included in 5 free rules with CloudFront Free plan |
| AWS WAF – API Gateway | ~$10–15 | ⚠️ Regional Web ACL (protects public /auth endpoint) — not covered by any free tier |
| Amazon Cognito | $0.00 | Free tier 50,000 MAU |
| Amazon SQS | ~$0.00 | Free tier 1M requests |
| Amazon Polly | ~$0.04–5 | ~100,000 characters, free tier 5 million Standard characters/month (first year) |
| Amazon SNS | ~$0.00 | Free tier |
| Amazon CloudWatch | ~$1–5 | Logs + Alarms — essential service for system monitoring |
| Amazon Route 53 | ~$0.50 | Hosted Zone $0.50/month |
| AWS ACM | $0.00 | Completely free |
| **Total AWS** | **~$12–30/month** | |
| **OpenAI API** | **~$5–50+** | Varies with actual evaluation volume, cost outside AWS |
| **Total with OpenAI** | **~$17–80/month** | |

### One-time Costs

| Item | Cost |
|------|------|
| Domain `itcoach24h.xyz` (Namecheap) | ~$2–3/year |

### Cost Summary

- **Startup cost:** ~$2–3 (domain)
- **Monthly operational cost:** ~$17–80 (AWS $12–30 + OpenAI $5–50+, depending on actual traffic)
- **First year total:** ~$200–1,000 (domain + AWS × 12 months + OpenAI × 12 months)
- **From 2nd year onwards:** equivalent to annual operational cost, plus domain renewal (~$2–3/year)

### Cost Control Notes

💡 **High variability factors:**
- **OpenAI API**: Primary cost driver, depends on actual evaluation volume. Must set **Usage Limits** on OpenAI dashboard
- **AWS WAF (API Gateway)**: Fixed cost ~$10–15/month, necessary to protect public `/auth` endpoint from brute-force attacks

**Recommendations:**
- Set **AWS Budget Alert** to notify when costs exceed $50/month
- Configure **OpenAI Usage Cap** to prevent budget overruns
- Monitor **CloudWatch Metrics** to optimize request volume

## 8. Risk Assessment

### Risk Matrix

| Risk | Impact | Probability | Solution |
|------|--------|------------|----------|
| OpenAI API rate limit / outage | High | Low | Cache results in DynamoDB |
| Question bank quality insufficient | High | Medium | Import data parallel to development |
| Lambda cold start slow | Medium | Medium | Optimize package size |
| OpenAI costs exceed budget | Medium | Medium | Set budget limits, optimize prompts |
| CORS or Cognito auth errors | Medium | Low | Test thoroughly in dev environment |

## 9. Expected Results

### Success Criteria
- ✅ Registration, login, quiz and essay practice work fully
- ✅ Recording, STT, AI evaluation and voice feedback work stably
- ✅ Spaced Repetition SM-2 automatically calculates review schedule correctly
- ✅ Mock Interview module runs complete flow from start to finish
- ✅ Dashboard, gamification, leaderboard display completely
- ✅ System stable, CloudWatch has no critical alarms

### Long-term Value
- Question bank accumulates, easy to add new specialties
- Personalized practice data, AI evaluation becomes increasingly accurate
- Serverless architecture easy to expand, reusable for future projects
- Team accumulates practical experience with AWS Serverless, AI integration, full-stack

*ITCoach – AI-Powered IT Interview Practice Platform on AWS*

*Serverless | React + TypeScript | 8 Lambda | 8 DynamoDB | 8 API Endpoints | OpenAI | Polly | Spaced Repetition SM-2*
