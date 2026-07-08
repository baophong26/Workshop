---
title: "Tạo bảng Topics"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.5.6. </b> "
---

#### Mục đích

Bảng `itcoach-topics` lưu danh sách chủ đề theo từng chuyên ngành (Frontend → JavaScript, React, CSS; Backend → Node.js, Python, Database; v.v.)

#### Cấu hình Table

- Table name: `itcoach-topics`
- Partition key: `specialty` - **String**
- Sort key: `topicId` - **String**
- Capacity mode: **On-demand**

![Topics Composite](/images/5-Workshop/5.5-dynamodb/005-table-topics-composite.png)


#### Không cần Global Secondary Index

Không cần GSI vì `specialty` đã là Partition Key.

#### Cấu trúc dữ liệu mẫu

```json
{
  "specialty": "frontend",
  "topicId": "topic-fe-js",
  "topicName": "JavaScript Fundamentals",
  "description": "Biến, hàm, scope, closure, v.v.",
  "order": 1,
  "totalQuestions": 45
}
```

```json
{
  "specialty": "frontend",
  "topicId": "topic-fe-react",
  "topicName": "React Basics",
  "description": "Component, Props, State, Hooks",
  "order": 2,
  "totalQuestions": 38
}
```

#### Kết quả

✅ Bảng `itcoach-topics` với Composite Key

