---
title: "Create 8 Resources and Methods"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.9.3. </b> "
---

#### Process to Create 1 Endpoint (repeat 8 times)

**Step 1: Create Resource**
- Select root `/` → **Create resource**
- Resource name: e.g., `auth`
- Resource path: `/auth`
- ✅ Enable CORS
- **Create resource**

**Step 2: Create Method**
- Select the newly created resource → **Create method**
- Method type: e.g., `POST`
- Integration type: **Lambda function**
- Lambda function: select corresponding function
- **Create method**

**Step 3: Configure Authorization**
- Click on the newly created method
- **Method request** tab → **Edit**
- Authorization: select `itcoach-cognito-auth` (except `/auth` use NONE)
- **Save**

**Step 4: Enable CORS**
- Select resource → **Enable CORS** → **Save**

#### List of 8 Endpoints to Create

| Resource | Method | Lambda | Authorization | CORS |
|----------|--------|--------|--------------|------|
| `/auth` | POST | `itcoach-auth-handler` | **NONE** | ✅ |
| `/questions` | GET | `itcoach-question-handler` | `itcoach-cognito-auth` | ✅ |
| `/topics` | GET | `itcoach-question-handler` | `itcoach-cognito-auth` | ✅ |
| `/sessions` | POST | `itcoach-session-handler` | `itcoach-cognito-auth` | ✅ |
| `/answers` | POST | `itcoach-answer-handler` | `itcoach-cognito-auth` | ✅ |
| `/results` | GET | `itcoach-result-handler` | `itcoach-cognito-auth` | ✅ |
| `/quiz` | POST | `itcoach-quiz-handler` | `itcoach-cognito-auth` | ✅ |
| `/leaderboard` | GET | `itcoach-gamification-handler` | `itcoach-cognito-auth` | ✅ |

![Create Resource Method](/images/5-Workshop/5.9-api/003-create-resource-method.png)


#### Result

✅ Created 8 resources with methods and CORS
