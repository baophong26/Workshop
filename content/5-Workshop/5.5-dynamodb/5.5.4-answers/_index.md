---
title: "Create Answers Table"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.5.4. </b> "
---

#### Purpose

The `itcoach-answers` table stores essay answers from users, AI scores, detailed feedback, and Polly audio URLs.

#### Table Configuration

- Table name: `itcoach-answers`
- Partition key: `answerId` - **String**
- Sort key: *(none)*
- Capacity mode: **On-demand**

#### Create Global Secondary Index

After table is Active:

1. **Indexes** tab → **Create index**
2. Partition key: `sessionId` - **String**
3. Index name: `sessionId-index`
4. **Create index**

#### Sample Data Structure

```json
{
  "answerId": "ans-xyz789",
  "sessionId": "session-abc123",
  "userId": "user-123456",
  "questionId": "e_fe_001",
  "answerText": "Virtual DOM is...",
  "answerAudioUrl": "s3://itcoach-audio-upload/ans-xyz789.mp3",
  "aiScore": 8.5,
  "aiFeedback": "Good answer, however...",
  "feedbackAudioUrl": "s3://itcoach-audio-upload/feedback-xyz789.mp3",
  "submittedAt": "2026-07-05T10:15:00Z"
}
```

#### Result

✅ Table `itcoach-answers` with GSI `sessionId-index`
