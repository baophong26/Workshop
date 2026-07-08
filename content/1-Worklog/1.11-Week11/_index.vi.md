---
title: "Worklog Tuần 11"
date: 2026-06-26
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

### Mục tiêu tuần 11:
* Xây dựng các tính năng nâng cao (Thanh toán giả lập, Đánh giá dịch vụ) và tối ưu hóa hiệu năng ứng dụng.
* Đóng gói ứng dụng bằng Docker và cấu hình triển khai trên cụm máy chủ ảo EC2.
* Thiết lập phân phối tải (ALB), tự động co giãn (ASG), cấu hình tên miền bảo mật (HTTPS) và tích hợp CI/CD.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 5 | - Lập trình tính năng cổng thanh toán mô phỏng (Mock Payment Gateway) và hệ thống đánh giá sao (Reviews) cho Coach | 26/06/2026 | 26/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | - Tối ưu hiệu năng ứng dụng: Lập chỉ mục (Database Indexing) các trường hay tìm kiếm, nén bundle Next.js | 27/06/2026 | 27/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 2 | - Viết Dockerfile, docker-compose để đóng gói ứng dụng Frontend và Backend đồng bộ | 29/06/2026 | 29/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Triển khai Docker Container lên máy chủ EC2, thiết lập Application Load Balancer (ALB) và Auto Scaling Group (ASG) | 30/06/2026 | 30/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Trỏ tên miền Route 53 về ALB, cấu hình HTTPS qua ACM SSL và thiết lập CI/CD pipeline tự động hóa bằng GitHub Actions | 01/07/2026 | 02/07/2026 | https://cloudjourney.awsstudygroup.com/ |

### Kết quả đạt được tuần 11:
* **Tính năng Web nâng cao & Tối ưu:**
  - Hoàn thiện nghiệp vụ đặt lịch: Người dùng có thể thanh toán qua cổng giả lập và gửi đánh giá (Reviews) kèm số sao cho Coach sau mỗi buổi học.
  - Tối ưu hóa thời gian phản hồi API từ ~400ms xuống còn ~80ms nhờ đánh chỉ mục (Index) các cột `skills` và `booking_date` trong database PostgreSQL.
* **Đóng gói & Triển khai hạ tầng:**
  - Container hóa thành công ứng dụng với Docker, giúp quy trình chạy thử và triển khai đồng nhất trên mọi môi trường.
  - Triển khai thành công ứng dụng lên các máy chủ EC2 phía sau Application Load Balancer (ALB). Cấu hình Auto Scaling Group (ASG) tự động duy trì hoạt động máy chủ khi có lượng truy cập tăng.
  - Trỏ tên miền thông qua Route 53, bật HTTPS an toàn với chứng chỉ SSL được cấp phát miễn phí từ ACM.
  - Thiết lập pipeline CI/CD (GitHub Actions) tự động chạy kiểm thử, build Docker Image, đẩy lên Docker Registry và deploy trực tiếp lên các EC2 instance khi push code mới.
