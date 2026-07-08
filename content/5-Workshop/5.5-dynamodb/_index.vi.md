---
title: "Tạo DynamoDB Tables"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

#### Giới thiệu về DynamoDB

Amazon DynamoDB là dịch vụ cơ sở dữ liệu NoSQL được quản lý hoàn toàn, cung cấp hiệu năng nhanh và có thể dự đoán với khả năng mở rộng liền mạch.

Trong hệ thống ITCoach, chúng ta cần tạo **8 bảng DynamoDB**:

| # | Tên bảng | Mục đích |
|---|---------|----------|
| 1 | `itcoach-users` | Thông tin người dùng, profile |
| 2 | `itcoach-questions` | Ngân hàng câu hỏi (Quiz + Tự luận) |
| 3 | `itcoach-sessions` | Phiên Mock Interview |
| 4 | `itcoach-answers` | Câu trả lời + AI feedback |
| 5 | `itcoach-history` | Lịch sử học tập |
| 6 | `itcoach-topics` | Chủ đề theo chuyên ngành |
| 7 | `itcoach-quiz-attempts` | Spaced Repetition SM-2 |
| 8 | `itcoach-gamification` | XP, level, streak, badge |


#### Nội dung

1. [Tạo bảng Users](5.5.1-users/)
2. [Tạo bảng Questions](5.5.2-questions/)
3. [Tạo bảng Sessions](5.5.3-sessions/)
4. [Tạo bảng Answers](5.5.4-answers/)
5. [Tạo bảng History](5.5.5-history/)
6. [Tạo bảng Topics](5.5.6-topics/)
7. [Tạo bảng Quiz Attempts](5.5.7-quiz-attempts/)
8. [Tạo bảng Gamification](5.5.8-gamification/)

