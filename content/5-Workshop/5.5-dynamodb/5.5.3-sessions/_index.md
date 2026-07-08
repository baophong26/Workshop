---
title: "Create Sessions Table"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.5.3. </b> "
---

#### Purpose

The `itcoach-sessions` table stores Mock Interview session data. Each session saves configuration (specialty, level, duration) and the list of questions selected by AI.

#### Table Configuration

- Table name: `itcoach-sessions`
- Partition key: `sessionId` - **String**
- Sort key: *(none)*
- Capacity mode: **On-demand**

#### Create Global Secondary Index

After table is Active:

1. **Indexes** tab → **Create index**
2. Partition key: `userId` - **String**
3. Index name: `userId-index`
4. **Create index**

#### Sample Data Structure

```json
{
  "sessionId": "session-abc123",
  "userId": "user-123456",
  "specialty": "frontend",
  "level": "fresher",
  "duration": 30,
  "questions": ["q_fe_001", "q_fe_002", "q_fe_003"],
  "status": "in_progress",
  "startedAt": "2026-07-05T10:00:00Z",
  "totalScore": 75
}
```

#### Result

✅ Table `itcoach-sessions` with GSI `userId-index`
