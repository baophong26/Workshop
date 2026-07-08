---
title: "Tạo IAM Role cho Lambda"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

#### Giới thiệu về IAM Role

IAM Role là một identity trong AWS có các permission policies xác định những gì identity đó có thể và không thể làm trong AWS. Lambda functions cần IAM Role để có quyền truy cập các dịch vụ AWS khác như DynamoDB, S3, SQS, Polly, và CloudWatch.

Trong bước này, chúng ta sẽ tạo một IAM Role duy nhất mà tất cả 8 Lambda functions sẽ sử dụng chung.

#### Các bước thực hiện

**1. Truy cập IAM Console**

- Đăng nhập vào AWS Console
- Tìm kiếm dịch vụ **IAM** trong thanh tìm kiếm
- Click vào **IAM** để mở IAM Dashboard

**2. Tạo Role mới**

- Ở menu bên trái, click vào **Roles**
- Click nút **Create role**

**3. Chọn Trusted Entity Type**

- Trusted entity type: chọn **AWS service**
- Use case: chọn **Lambda**
- Click **Next**

**4. Thêm Permissions Policies**

Trong trang Add permissions, tìm và tick chọn 6 policies sau:

| Policy Name | Mục đích |
|------------|----------|
| `AWSLambdaBasicExecutionRole` | Ghi logs vào CloudWatch |
| `AmazonDynamoDBFullAccess` | Đọc/ghi DynamoDB |
| `AmazonS3FullAccess` | Upload/download S3 |
| `AmazonSQSFullAccess` | Gửi/nhận message SQS |
| `AmazonPollyFullAccess` | Text-to-Speech |
| `CloudWatchFullAccess` | Monitoring và logs |

Cách tìm nhanh:
- Gõ tên policy vào ô **Search**
- Tick checkbox bên cạnh tên policy
- Lặp lại cho 6 policies

![Add Permissions](/images/5-Workshop/5.3-iam-role/001-add-permissions.png)

Sau khi đã chọn đủ 6 policies, click **Next**

**5. Đặt tên và tạo Role**

- Role name: `itcoach-lambda-role`
- Description: `IAM role for ITCoach Lambda functions with access to DynamoDB, S3, SQS, Polly, and CloudWatch`
- Kiểm tra lại 6 policies đã chọn
- Click **Create role**

**6. Lưu thông tin Role ARN**

Sau khi tạo xong, bạn sẽ thấy thông báo thành công.

- Click vào role name `itcoach-lambda-role` vừa tạo
- Copy **Role ARN** (dạng: `arn:aws:iam::ACCOUNT_ID:role/itcoach-lambda-role`)
- Lưu lại ARN này, sẽ dùng ở bước tạo Lambda functions

![Role ARN](/images/5-Workshop/5.3-iam-role/002-role-arn.png)

#### Kết quả

✅ Bạn đã tạo thành công IAM Role `itcoach-lambda-role` với đầy đủ quyền cần thiết.

#### Thông tin cần lưu

```
Role Name: itcoach-lambda-role
Role ARN: arn:aws:iam::[ACCOUNT_ID]:role/itcoach-lambda-role
```


#### Giải thích về các permissions

| Permission | Tại sao cần |
|-----------|-------------|
| **LambdaBasicExecutionRole** | Cho phép Lambda ghi logs vào CloudWatch Logs để debug |
| **DynamoDBFullAccess** | Lambda cần đọc/ghi 8 bảng DynamoDB (users, questions, sessions, v.v.) |
| **S3FullAccess** | Lambda cần tạo Presigned URLs cho S3 audio bucket |
| **SQSFullAccess** | Lambda gửi message vào SQS queue để xử lý AI bất đồng bộ |
| **PollyFullAccess** | Lambda `itcoach-ai-processor` cần gọi Polly để text-to-speech |
| **CloudWatchFullAccess** | Lambda ghi metrics và tạo custom alarms |


#### Tiếp theo

Chuyển sang bước tiếp theo để tạo S3 Buckets.

