---
title: "Tạo 8 Lambda Functions"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.8.1. </b> "
---

#### Quy trình tạo 1 Lambda (lặp lại 8 lần)

Tôi sẽ hướng dẫn chi tiết cho function đầu tiên, các function còn lại làm tương tự.

#### Tạo Function 1: itcoach-auth-handler

**1. Truy cập Lambda Console**

- Tìm kiếm **Lambda** trong thanh tìm kiếm
- Click vào **AWS Lambda**

**2. Create Function**

- Click **Create function**

**3. Cấu hình Function**

- Chọn **Author from scratch**
- Function name: `itcoach-auth-handler`
- Runtime: **Python 3.12**

**4. Permissions - QUAN TRỌNG**

- Kéo xuống phần **Permissions**
- Click **▶ Additional settings** để mở rộng
- Execution role: chọn **Use an existing role**
- Existing role: chọn **`itcoach-lambda-role`** (đã tạo ở bước 5.3)

![Create Function](/images/5-Workshop/5.8-lambda/001-create-function.png)

- Click **Create function**

**5. Deploy Placeholder Code**

Sau khi function được tạo:

- Tab **Code** → Xóa code mặc định
- Dán code placeholder sau:

```python
import json

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'headers': {
            'Content-Type': 'application/json',
            'Access-Control-Allow-Origin': '*',
            'Access-Control-Allow-Headers': 'Content-Type,Authorization',
            'Access-Control-Allow-Methods': 'GET,POST,PUT,DELETE,OPTIONS'
        },
        'body': json.dumps({'message': 'itcoach-auth-handler placeholder'})
    }
```

![Placeholder Code](/images/5-Workshop/5.8-lambda/002-placeholder-code.png)

- Click **Deploy**

**6. Configuration - Timeout và Memory**

- Tab **Configuration** → **General configuration** → **Edit**
- Timeout: `30` seconds
- Memory: `256` MB
- Click **Save**

#### Lặp lại cho 7 functions còn lại

Làm tương tự các bước trên cho 7 functions:

| # | Function Name | Code placeholder message |
|---|--------------|--------------------------|
| 2 | `itcoach-question-handler` | 'itcoach-question-handler placeholder' |
| 3 | `itcoach-session-handler` | 'itcoach-session-handler placeholder' |
| 4 | `itcoach-answer-handler` | 'itcoach-answer-handler placeholder' |
| 5 | `itcoach-ai-processor` | 'itcoach-ai-processor placeholder' |
| 6 | `itcoach-result-handler` | 'itcoach-result-handler placeholder' |
| 7 | `itcoach-quiz-handler` | 'itcoach-quiz-handler placeholder' |
| 8 | `itcoach-gamification-handler` | 'itcoach-gamification-handler placeholder' |


#### Kiểm tra đã tạo đủ 8 functions

Quay lại Lambda Dashboard, bạn sẽ thấy 8 functions.

#### Kết quả

✅ Đã tạo 8 Lambda functions với:
- Runtime: Python 3.12
- Role: itcoach-lambda-role
- Timeout: 30s
- Memory: 256 MB
- Placeholder code với CORS headers

#### Tiếp theo

Chuyển sang bước tiếp theo để cấu hình Environment Variables cho từng function.

