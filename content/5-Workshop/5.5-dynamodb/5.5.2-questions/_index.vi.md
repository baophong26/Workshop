---
title: "Tạo bảng Questions"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

#### Mục đích

Bảng `itcoach-questions` lưu trữ ngân hàng câu hỏi dùng chung cho cả **Quiz** và **Tự luận**. Phân biệt bằng field `type`: `"QUIZ"` hoặc `"ESSAY"`.

#### Cấu hình Table

- Table name: `itcoach-questions`
- Partition key: `questionId` - **String**
- Sort key: *(không có)*
- Capacity mode: **On-demand**

![Table Questions GSI](/images/5-Workshop/5.5-dynamodb/004-table-questions-gsi.png)

#### Tạo Global Secondary Index

Sau khi table được tạo (Status = Active):

1. Click vào table name `itcoach-questions`
2. Chọn tab **Indexes**
3. Click **Create index**

**Index configuration:**
- Partition key: `category` - **String**
- Sort key: *(không có)*
- Index name: `category-index`
- Attribute projections: **All**

![Create GSI](/images/5-Workshop/5.5-dynamodb/003-create-gsi.png)

4. Click **Create index**


#### Cấu trúc dữ liệu mẫu

**Câu hỏi Quiz:**
```json
{
  "questionId": "q_fe_001",
  "type": "QUIZ",
  "category": "frontend",
  "topicId": "topic-fe-js",
  "level": "fresher",
  "question": "Virtual DOM khác Real DOM như thế nào?",
  "options": ["Nhanh hơn", "Chậm hơn", "Giống nhau", "Không liên quan"],
  "correctAnswers": [0],
  "multiSelect": false
}
```

**Câu hỏi Tự luận:**
```json
{
  "questionId": "e_be_001",
  "type": "ESSAY",
  "category": "backend",
  "topicId": "topic-be-api",
  "level": "junior",
  "question": "Giải thích sự khác biệt giữa REST và GraphQL?",
  "sampleAnswer": "REST là..., GraphQL là..."
}
```

#### Kết quả

✅ Bảng `itcoach-questions` với GSI `category-index`

