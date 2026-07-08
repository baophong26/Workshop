---
title: "Creating DynamoDB Tables"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

#### Introduction to DynamoDB

Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability.

In the ITCoach system, we need to create **8 DynamoDB tables**:

| # | Table Name | Purpose |
|---|-----------|---------|
| 1 | `itcoach-users` | User information, profile |
| 2 | `itcoach-questions` | Question bank (Quiz + Essay) |
| 3 | `itcoach-sessions` | Mock Interview sessions |
| 4 | `itcoach-answers` | Answers + AI feedback |
| 5 | `itcoach-history` | Learning history |
| 6 | `itcoach-topics` | Topics by specialty |
| 7 | `itcoach-quiz-attempts` | Spaced Repetition SM-2 |
| 8 | `itcoach-gamification` | XP, level, streak, badge |


#### Content

1. [Create Users Table](5.5.1-users/)
2. [Create Questions Table](5.5.2-questions/)
3. [Create Sessions Table](5.5.3-sessions/)
4. [Create Answers Table](5.5.4-answers/)
5. [Create History Table](5.5.5-history/)
6. [Create Topics Table](5.5.6-topics/)
7. [Create Quiz Attempts Table](5.5.7-quiz-attempts/)
8. [Create Gamification Table](5.5.8-gamification/)
