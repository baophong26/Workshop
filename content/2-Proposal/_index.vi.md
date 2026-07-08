---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# ITCoach – Nền Tảng Luyện Phỏng Vấn IT Thông Minh Ứng Dụng AI
## Giải pháp AWS Serverless cho sinh viên IT luyện tập kỹ năng phỏng vấn

## 1. Tóm Tắt Điều Hành

ITCoach là nền tảng web hỗ trợ sinh viên IT và người mới đi làm ôn luyện kiến thức chuyên môn, rèn luyện kỹ năng trả lời phỏng vấn và mô phỏng môi trường phỏng vấn thực tế với sự hỗ trợ của AI. Mục tiêu là giúp sinh viên tăng khả năng vượt qua các vòng tuyển dụng Internship, Fresher và Junior tại các công ty công nghệ.

Nền tảng hỗ trợ đa dạng hình thức luyện tập: trắc nghiệm một hoặc nhiều lựa chọn với cơ chế Spaced Repetition (SM-2), tự luận ghi âm giọng nói, và mô phỏng buổi phỏng vấn thực tế. AI đánh giá chi tiết từng câu trả lời, chỉ ra điểm thiếu, gợi ý cải thiện và phản hồi bằng giọng nói qua Amazon Polly. Hệ thống Gamification với XP, level, streak và bảng xếp hạng giúp tăng động lực học tập.

Hệ thống được xây dựng hoàn toàn trên Amazon Web Services theo mô hình Serverless Architecture. Frontend sử dụng React + TypeScript phân phối qua Amazon CloudFront, backend xử lý bởi AWS Lambda, dữ liệu lưu trữ trên Amazon DynamoDB, tích hợp OpenAI API để đánh giá câu trả lời và Amazon Polly để tạo giọng nói.

## 2. Tuyên Bố Vấn Đề

### Vấn đề hiện tại

Sinh viên IT và người mới đi làm thường thiếu môi trường thực hành phỏng vấn thực tế:

- Các website trắc nghiệm thông thường chỉ kiểm tra lý thuyết, không đánh giá khả năng diễn đạt
- Không có công cụ đánh giá câu trả lời tự luận hoặc giọng nói với phản hồi AI chi tiết
- Không có môi trường mô phỏng phỏng vấn thực tế theo từng chuyên ngành
- Khó nhận biết điểm yếu cá nhân để tập trung ôn luyện đúng chỗ
- Nền tảng nước ngoài có rào cản ngôn ngữ, chi phí cao, không phù hợp thị trường IT Việt Nam

### Giải pháp

ITCoach giải quyết các vấn đề trên với các tính năng cốt lõi:

- **Ngân hàng câu hỏi đa chuyên ngành:** 10 chuyên ngành IT, mỗi chuyên ngành chia thành nhiều chủ đề
- **Trắc nghiệm thông minh:** Quiz 1 hoặc nhiều đáp án, áp dụng Spaced Repetition SM-2 nhắc lại đúng thời điểm
- **Tự luận bằng giọng nói:** Ghi âm giọng nói, AI đánh giá và phản hồi câu trả lời mẫu bằng giọng nói
- **Luyện tập linh hoạt:** Chọn luyện 1 câu hỏi tự luận hoặc 1 chuyên ngành (3-5 câu hỏi ngẫu nhiên), thời lượng mỗi câu mặc định
- **Dashboard & Gamification:** Theo dõi tiến độ, hệ thống XP, level, badge, streak và bảng xếp hạng cập nhật liên tục theo thời gian thực

### Hạ tầng AWS

- **Amazon CloudFront + S3** phân phối React + TypeScript tốc độ cao toàn cầu
- **Amazon Cognito** xác thực người dùng an toàn
- **Amazon API Gateway + AWS Lambda** xử lý toàn bộ nghiệp vụ serverless
- **Amazon DynamoDB** lưu trữ toàn bộ dữ liệu hệ thống (8 bảng)
- **Amazon S3 (Audio)** lưu trữ file ghi âm và audio Polly qua Presigned URL
- **Amazon SQS** xử lý bất đồng bộ tác vụ AI nặng
- **OpenAI API** Speech-to-Text + đánh giá chất lượng câu trả lời
- **Amazon Polly** phản hồi câu trả lời mẫu bằng giọng nói
- **AWS WAF** bảo vệ CloudFront và API Gateway khỏi tấn công web (SQLi, XSS, DDoS)
- **Amazon CloudWatch + SNS** giám sát hệ thống và cảnh báo tự động
- **Amazon Route 53 + ACM** quản lý DNS và SSL certificate cho tên miền `itcoach24h.xyz`

### Lợi ích

- Sinh viên có môi trường luyện phỏng vấn IT thực tế, phản hồi AI tức thời như một mentor
- Spaced Repetition giúp ghi nhớ hiệu quả, bảng xếp hạng theo thời gian thực tạo động lực học tập
- Không cần quản lý server, tự động mở rộng theo nhu cầu nhờ kiến trúc Serverless
- Chi phí vận hành thấp, dễ bổ sung chuyên ngành và câu hỏi mới trong tương lai

## 3. Kiến Trúc Giải Pháp

Nền tảng áp dụng kiến trúc AWS Serverless với AWS Lambda là trung tâm xử lý nghiệp vụ.

![ITCoach Architecture](/images/ITCoachArchitecture.png)

*Lưu ý: Sơ đồ trên đã gộp các Lambda functions theo nhóm logic để dễ nhìn:*
- *"**AWS Lambda (8 functions)**" trong sơ đồ đại diện cho 7 Lambda sync: `auth-handler`, `question-handler`, `session-handler`, `answer-handler`, `quiz-handler`, `gamification-handler`, `leaderboard-handler`*
- *"**itcoach-ai-processor**" là Lambda async thứ 8, xử lý tác vụ AI nặng qua SQS*
- *Trong thực tế triển khai, mỗi function được tạo riêng biệt (best practice: least privilege, cold start optimization, dễ debug)*

### Luồng xử lý chính

```
User (Browser)
    ↓ HTTPS – itcoach24h.xyz
Amazon Route 53 (DNS)
    ↓
Amazon CloudFront (CDN) ←→ S3 Static (React + TypeScript)
    ↓
Amazon API Gateway (8 endpoints, Throttling: 100 req/s)
    ↓ Cognito Authorizer
AWS Lambda (8 functions)
    ├──→ Amazon DynamoDB (8 tables)
    ├──→ Amazon S3 Audio (Presigned URL Upload)
    ├──→ Amazon SQS (Async Processing)
    │         ↓
    │    itcoach-ai-processor
    │         ├──→ OpenAI API (STT + AI Evaluation)
    │         └──→ Amazon Polly (Text-to-Speech)
    └──→ Amazon CloudWatch → Amazon SNS (Alerts)
```

### Dịch vụ AWS sử dụng

| Dịch vụ | Mục đích |
|---------|---------|
| Amazon CloudFront | CDN phân phối React + TypeScript toàn cầu qua HTTPS |
| Amazon S3 (Static) | Lưu trữ file build React + TypeScript |
| Amazon S3 (Audio) | Lưu trữ file ghi âm và audio Polly |
| Amazon API Gateway | 8 endpoints, tích hợp Cognito Authorizer, Throttling (100 req/s) |
| Amazon Cognito | Đăng ký, đăng nhập, quản lý phiên người dùng |
| AWS Lambda | 8 functions xử lý toàn bộ nghiệp vụ backend |
| Amazon DynamoDB | 8 bảng lưu trữ toàn bộ dữ liệu hệ thống |
| Amazon SQS | Hàng đợi xử lý bất đồng bộ AI và audio |
| Amazon Polly | Phản hồi câu trả lời mẫu bằng giọng nói |
| OpenAI API | Speech-to-Text + đánh giá chất lượng câu trả lời |
| AWS WAF | Bảo vệ CloudFront và API Gateway khỏi tấn công web |
| Amazon CloudWatch | Giám sát logs, metrics, hiệu năng hệ thống |
| Amazon SNS | Gửi cảnh báo email khi hệ thống có lỗi |
| Amazon Route 53 | Quản lý DNS cho tên miền `itcoach24h.xyz` |
| AWS ACM | Chứng chỉ SSL miễn phí cho HTTPS |

## 4. Tính Năng Chi Tiết

### 4.1. Đối Tượng Người Dùng

- Sinh viên năm 2, năm 3, năm cuối ngành CNTT
- Sinh viên chuẩn bị ứng tuyển Internship/Fresher
- Người chuyển ngành muốn luyện phỏng vấn kỹ thuật
- Người đi làm muốn ôn lại kiến thức trước khi phỏng vấn

### 4.2. Các Chuyên Ngành Hỗ Trợ

| # | Chuyên ngành |
|---|-------------|
| 1 | Front-end Developer |
| 2 | Back-end Developer |
| 3 | Full-stack Developer |
| 4 | DevOps Engineer |
| 5 | Mobile Developer |
| 6 | QA/QC Engineer |
| 7 | Data Engineer |
| 8 | Data Analyst |
| 9 | AI/Machine Learning Engineer |
| 10 | Cyber Security |

### 4.3. Hình Thức Luyện Tập

**Trắc nghiệm (Quiz):**
- Chọn 1 đáp án đúng hoặc nhiều đáp án đúng
- Thuật toán Spaced Repetition SM-2 tự động tính `nextReviewDate` để nhắc lại đúng thời điểm
- Cộng XP sau mỗi câu trả lời đúng

**Tự luận:**
- Ghi âm giọng nói
- OpenAI STT chuyển giọng nói thành text
- AI chấm điểm, chỉ ra ý thiếu, gợi ý cải thiện, đưa câu trả lời mẫu
- Polly đọc câu trả lời mẫu bằng giọng nói

### 4.4. Module Luyện Tập Giọng Nói

- Chọn 1 câu hỏi tự luận hoặc chọn 1 chuyên ngành (3-5 câu hỏi ngẫu nhiên)
- Thời lượng mỗi câu hỏi mặc định
- Người dùng trả lời bằng giọng nói
- AI đánh giá và đọc câu trả lời mẫu bằng giọng nói (Polly)

### 4.5. Dashboard & Gamification

- Tiến độ học theo từng chủ đề, tỷ lệ hoàn thành, điểm trung bình
- Chuỗi ngày học liên tiếp (streak), lịch sử hàng ngày
- Hệ thống XP, Level, Badge thành tích
- Bảng xếp hạng cập nhật liên tục theo thời gian thực

## 5. Triển Khai Kỹ Thuật

### Lambda Functions – 8 functions

| Function | Nhiệm vụ |
|----------|----------|
| `itcoach-auth-handler` | Đăng ký, đăng nhập, quản lý profile |
| `itcoach-question-handler` | Lấy câu hỏi tự luận + danh sách topics theo chuyên ngành |
| `itcoach-session-handler` | Tạo và quản lý phiên Mock Interview |
| `itcoach-answer-handler` | Nhận câu trả lời tự luận, tạo Presigned URL upload audio |
| `itcoach-ai-processor` | OpenAI STT + đánh giá + Polly TTS (async từ SQS) |
| `itcoach-result-handler` | Trả kết quả, điểm số, lịch sử, thống kê dashboard |
| `itcoach-quiz-handler` | Quiz trắc nghiệm, SM-2, cộng XP vào gamification |
| `itcoach-gamification-handler` | XP, level, streak, bảng xếp hạng leaderboard |

### DynamoDB – 8 bảng

| Bảng | Partition Key | Sort Key | Index | Dùng cho |
|------|--------------|----------|-------|---------|
| `itcoach-users` | `userId` | - | - | Thông tin người dùng |
| `itcoach-questions` | `questionId` | - | `category-index` | Quiz + Tự luận chung |
| `itcoach-sessions` | `sessionId` | - | `userId-index` | Phiên Mock Interview |
| `itcoach-answers` | `answerId` | - | `sessionId-index` | Câu trả lời + AI feedback |
| `itcoach-history` | `userId` | `timestamp` | - | Lịch sử học tập |
| `itcoach-topics` | `specialty` | `topicId` | - | Chủ đề theo chuyên ngành |
| `itcoach-quiz-attempts` | `userId` | `questionId` | - | Spaced Repetition SM-2 |
| `itcoach-gamification` | `userId` | - | `xp-index` | XP, level, streak, badge |

### API Gateway – 8 endpoints

| Endpoint | Method | Dùng cho |
|----------|--------|---------|
| `/auth` | POST | Đăng nhập/đăng ký (public) |
| `/questions` | GET | Lấy câu hỏi tự luận |
| `/topics` | GET | Lấy chủ đề theo chuyên ngành |
| `/sessions` | POST | Tạo phiên Mock Interview |
| `/answers` | POST | Nộp câu trả lời tự luận |
| `/results` | GET | Xem kết quả + lịch sử |
| `/quiz` | POST | Nộp bài quiz + Spaced Repetition |
| `/leaderboard` | GET | Bảng xếp hạng XP |

## 6. Lộ Trình & Mốc Triển Khai

### Giai đoạn 1 – Hạ tầng & Backend
Dựng toàn bộ hạ tầng AWS, viết 8 Lambda functions, tích hợp OpenAI và Polly.

### Giai đoạn 2 – Frontend & Tích hợp
Xây dựng giao diện React + TypeScript: auth, quiz, tự luận, ghi âm, Mock Interview, dashboard, gamification.

### Giai đoạn 3 – Dữ liệu & Hoàn thiện
Nhập ngân hàng câu hỏi (ưu tiên Frontend, Backend, Kiến thức nền), test toàn bộ luồng, sửa lỗi, deploy chính thức.

| Giai đoạn | Thời gian | Nội dung |
|-----------|-----------|---------|
| Chuẩn bị | Trước thực tập | Thành lập nhóm, phân công vai trò |
| Tháng 1 – Tháng 2 | Thực tập | Học lý thuyết, nắm vững kiến thức AWS, Serverless, React + TypeScript |
| Tháng 3 – Tuần 1 | Thực tập | Dựng hạ tầng AWS: S3, DynamoDB, API Gateway, Cognito |
| Tháng 3 – Tuần 2 | Thực tập | Dev backend: 8 Lambda functions + OpenAI + Polly |
| Tháng 3 – Tuần 3 | Thực tập | Dev frontend: auth, quiz, tự luận, Mock Interview, dashboard, gamification |
| Tháng 3 – Tuần 4 | Thực tập | Tích hợp, test toàn bộ luồng, sửa lỗi, nhập dữ liệu câu hỏi, deploy, demo |

## 7. Ước Tính Ngân Sách

### Chi phí AWS/tháng

| Dịch vụ | Ước tính | Ghi chú |
|---------|---------|---------|
| AWS Lambda | ~$0.00 | Free tier 1M requests + 400.000 GB-s/tháng (vĩnh viễn) |
| Amazon DynamoDB | ~$0.00–1 | On-demand, free tier 25GB |
| Amazon S3 | ~$0.05–1 | Static + audio files, tăng dần theo dung lượng audio tích lũy |
| Amazon API Gateway | ~$0.01–2 | $3.5/triệu request |
| Amazon CloudFront | $0.00 | Free plan (1TB + 10 triệu request/tháng) |
| AWS WAF – CloudFront | $0.00 | Nằm trong 5 rule miễn phí kèm CloudFront Free plan |
| AWS WAF – API Gateway | ~$10–15 | ⚠️ Web ACL Regional (bảo vệ endpoint /auth public) — không nằm trong gói miễn phí nào |
| Amazon Cognito | $0.00 | Free tier 50.000 MAU |
| Amazon SQS | ~$0.00 | Free tier 1M requests |
| Amazon Polly | ~$0.04–5 | ~100.000 ký tự, free tier 5 triệu ký tự Standard/tháng (năm đầu) |
| Amazon SNS | ~$0.00 | Free tier |
| Amazon CloudWatch | ~$1–5 | Logs + Alarms — dịch vụ quan trọng để monitoring hệ thống |
| Amazon Route 53 | ~$0.50 | Hosted Zone $0.50/tháng |
| AWS ACM | $0.00 | Miễn phí hoàn toàn |
| **Tổng AWS** | **~$12–30/tháng** | |
| **OpenAI API** | **~$5–50+** | Biến động theo lượng đánh giá thật, chi phí ngoài AWS |
| **Tổng cả OpenAI** | **~$17–80/tháng** | |

### Chi phí một lần

| Khoản | Chi phí |
|-------|---------|
| Domain `itcoach24h.xyz` (Namecheap) | ~$2–3/năm |

### Tổng kết chi phí

- **Chi phí khởi động:** ~$2–3 (domain)
- **Chi phí vận hành hàng tháng:** ~$17–80 (AWS $12–30 + OpenAI $5–50+, tuỳ traffic thật)
- **Chi phí năm đầu tiên:** ~$200–1.000 (domain + AWS × 12 tháng + OpenAI × 12 tháng)
- **Từ năm thứ 2 trở đi:** tương đương chi phí vận hành hàng năm, cộng thêm gia hạn domain (~$2–3/năm)

### Lưu ý kiểm soát chi phí

💡 **Các yếu tố biến động lớn:**
- **OpenAI API**: Chi phí chính, phụ thuộc vào số lượng đánh giá thật. Cần đặt **Usage Limits** trên OpenAI dashboard
- **AWS WAF (API Gateway)**: Chi phí cố định ~$10–15/tháng, cần thiết để bảo vệ endpoint `/auth` công khai khỏi brute-force attacks

**Khuyến nghị:**
- Đặt **AWS Budget Alert** cảnh báo khi chi phí vượt $50/tháng
- Giới hạn **OpenAI Usage Cap** để tránh chi phí vượt ngân sách
- Theo dõi **CloudWatch Metrics** để tối ưu số lượng request

## 8. Đánh Giá Rủi Ro

### Ma trận rủi ro

| Rủi ro | Ảnh hưởng | Xác suất | Giải pháp |
|--------|-----------|---------|---------|
| OpenAI API rate limit / outage | Cao | Thấp | Cache kết quả vào DynamoDB |
| Chất lượng ngân hàng câu hỏi chưa đủ | Cao | Trung bình | Nhập dữ liệu song song với phát triển |
| Lambda cold start chậm | Trung bình | Trung bình | Tối ưu package size |
| Chi phí OpenAI vượt dự kiến | Trung bình | Trung bình | Đặt giới hạn budget, tối ưu prompt |
| Lỗi CORS hoặc Cognito auth | Trung bình | Thấp | Test kỹ trên môi trường dev |

## 9. Kết Quả Kỳ Vọng

### Tiêu chí thành công
- ✅ Đăng ký, đăng nhập, luyện tập quiz và tự luận hoạt động đầy đủ
- ✅ Ghi âm, STT, AI đánh giá và phản hồi giọng nói hoạt động ổn định
- ✅ Spaced Repetition SM-2 tự động tính lịch ôn tập đúng
- ✅ Module Mock Interview chạy đúng luồng từ đầu đến cuối
- ✅ Dashboard, gamification, bảng xếp hạng hiển thị đầy đủ
- ✅ Hệ thống ổn định, CloudWatch không có alarm nghiêm trọng

### Giá trị dài hạn
- Ngân hàng câu hỏi tích lũy, dễ bổ sung chuyên ngành mới
- Dữ liệu luyện tập cá nhân hóa, AI ngày càng đánh giá chính xác hơn
- Kiến trúc Serverless dễ mở rộng, tái sử dụng cho dự án tương lai
- Nhóm tích lũy kinh nghiệm thực tế AWS Serverless, AI integration, full-stack

*ITCoach – Nền Tảng Luyện Phỏng Vấn IT Thông Minh Ứng Dụng AI trên AWS*

*Serverless | React + TypeScript | 8 Lambda | 8 DynamoDB | 8 API Endpoints | OpenAI | Polly | Spaced Repetition SM-2*
