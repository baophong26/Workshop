---
title: "Tạo Cognito Authorizer"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.9.2. </b> "
---

#### Mục đích

Cognito Authorizer sẽ xác thực JWT token từ Cognito trước khi cho request vào Lambda. Chỉ `/auth` endpoint là public, 7 endpoints còn lại đều cần auth.

#### Các bước thực hiện

**1. Tạo Authorizer**

- Ở API `itcoach-api`, menu trái → **Authorizers**
- Click **Create authorizer**

**2. Cấu hình Authorizer**

- Authorizer name: `itcoach-cognito-auth`
- Type: **Cognito**
- Cognito user pool: chọn region `ap-southeast-1` → chọn User Pool đã tạo
- Token source: `Authorization` (giữ prefix `method.request.header.`)

![Cognito Authorizer](/images/5-Workshop/5.9-api/002-cognito-authorizer.png)

- Click **Create authorizer**

#### Kết quả

✅ Cognito Authorizer `itcoach-cognito-auth` đã được tạo

