---
title: "Tạo bảng Users"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.5.1. </b> "
---

#### Mục đích

Bảng `itcoach-users` lưu trữ thông tin người dùng và profile.

#### Các bước thực hiện

**1. Truy cập DynamoDB Console**

- Tìm kiếm **DynamoDB** trong thanh tìm kiếm AWS Console
- Click vào **DynamoDB**

**2. Tạo Table mới**

- Click nút **Create table**

![Create Table](/images/5-Workshop/5.5-dynamodb/001-create-table.png)

**3. Cấu hình Table**

**Table details:**
- Table name: `itcoach-users`
- Partition key: `userId` - Type: **String**
- Sort key: *(để trống - không cần)*

**Table settings:**
- Chọn **Customize settings**

**Read/write capacity settings:**
- Capacity mode: chọn **On-demand**

**Secondary indexes:**
- Không cần tạo (để trống)

**Encryption at rest:**
- Giữ mặc định: **Owned by Amazon DynamoDB**

![Table Users](/images/5-Workshop/5.5-dynamodb/002-table-users.png)

- Click **Create table**

**4. Chờ table được tạo**

Quá trình tạo table mất khoảng 10-30 giây. Trạng thái sẽ chuyển từ **Creating** sang **Active**.

#### Kết quả

✅ Bảng `itcoach-users` đã được tạo thành công

#### Cấu trúc dữ liệu mẫu

```json
{
  "userId": "user-123456",
  "email": "student@example.com",
  "name": "Nguyễn Văn A",
  "specialty": "frontend",
  "level": "fresher",
  "createdAt": "2026-04-17T10:00:00Z",
  "lastLogin": "2026-07-05T08:30:00Z"
}
```

#### Thông tin cần lưu

```
Table Name: itcoach-users
Partition Key: userId (String)
Sort Key: None
Capacity Mode: On-demand
```

#### Tiếp theo

Chuyển sang bước tiếp theo để tạo bảng Questions.

