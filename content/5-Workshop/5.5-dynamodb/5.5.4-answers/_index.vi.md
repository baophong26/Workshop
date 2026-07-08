---
title: "Tạo bảng Answers"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.5.4. </b> "
---

#### Mục đích

Bảng `itcoach-answers` lưu câu trả lời tự luận của người dùng, điểm số AI, feedback chi tiết, và URL audio Polly.

#### Cấu hình Table

- Table name: `itcoach-answers`
- Partition key: `answerId` - **String**
- Sort key: *(không có)*
- Capacity mode: **On-demand**

#### Tạo Global Secondary Index

Sau khi table Active:

1. Tab **Indexes** → **Create index**
2. Partition key: `sessionId` - **String**
3. Index name: `sessionId-index`
4. **Create index**


#### Cấu trúc dữ liệu mẫu

```json
{
  "answerId": "ans-xyz789",
  "sessionId": "session-abc123",
  "userId": "user-123456",
  "questionId": "e_fe_001",
  "answerText": "Virtual DOM là...",
  "answerAudioUrl": "s3://itcoach-audio-upload/ans-xyz789.mp3",
  "aiScore": 8.5,
  "aiFeedback": "Câu trả lời tốt, tuy nhiên...",
  "feedbackAudioUrl": "s3://itcoach-audio-upload/feedback-xyz789.mp3",
  "submittedAt": "2026-07-05T10:15:00Z"
}
```

#### Kết quả

✅ Bảng `itcoach-answers` với GSI `sessionId-index`

