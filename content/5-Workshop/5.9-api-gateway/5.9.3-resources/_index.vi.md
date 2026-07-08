---
title: "Tạo 8 Resources và Methods"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.9.3. </b> "
---

#### Quy trình tạo 1 endpoint (lặp lại 8 lần)

**Bước 1: Create Resource**
- Chọn root `/` → **Create resource**
- Resource name: ví dụ `auth`
- Resource path: `/auth`
- ✅ Enable CORS
- **Create resource**

**Bước 2: Create Method**
- Chọn resource vừa tạo → **Create method**
- Method type: ví dụ `POST`
- Integration type: **Lambda function**
- Lambda function: chọn function tương ứng
- **Create method**

**Bước 3: Cấu hình Authorization**
- Click vào method vừa tạo
- Tab **Method request** → **Edit**
- Authorization: chọn `itcoach-cognito-auth` (trừ `/auth` để NONE)
- **Save**

**Bước 4: Enable CORS**
- Chọn resource → **Enable CORS** → **Save**

#### Danh sách 8 endpoints cần tạo

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


#### Kết quả

✅ Đã tạo 8 resources với methods và CORS

