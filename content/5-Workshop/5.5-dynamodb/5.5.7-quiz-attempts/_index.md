---
title: "Create Quiz Attempts Table"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.5.7. </b> "
---

#### Purpose

The `itcoach-quiz-attempts` table stores quiz attempt history and parameters for the **Spaced Repetition SM-2** algorithm (interval, easeFactor, repetitions, nextReviewDate).

#### Table Configuration

- Table name: `itcoach-quiz-attempts`
- Partition key: `userId` - **String**
- Sort key: `questionId` - **String**
- Capacity mode: **On-demand**

#### No Global Secondary Index Needed

No GSI needed because queries are always by `userId + questionId`.

#### Sample Data Structure

```json
{
  "userId": "user-123456",
  "questionId": "q_fe_001",
  "lastAttemptDate": "2026-07-05",
  "lastResult": "correct",
  "totalAttempts": 3,
  "correctCount": 2,
  "interval": 7,
  "easeFactor": 2.5,
  "repetitions": 2,
  "nextReviewDate": "2026-07-12"
}
```

**SM-2 Field Explanations:**
- `interval`: Number of days until next review
- `easeFactor`: Difficulty coefficient (2.5 is default)
- `repetitions`: Number of consecutive correct reviews
- `nextReviewDate`: Date when this question should be reviewed

#### Result

✅ Table `itcoach-quiz-attempts` supporting Spaced Repetition
