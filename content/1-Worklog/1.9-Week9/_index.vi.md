---
title: "Worklog Tuần 9"
date: 2026-06-12
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

### Mục tiêu tuần 9:
* Phân tích yêu cầu nghiệp vụ và xác định các tính năng cốt lõi cho dự án Web IT Coach.
* Thiết kế kiến trúc hệ thống tổng thể và mô hình kết nối hạ tầng mạng bảo mật (VPC).
* Thiết kế sơ đồ cơ sở dữ liệu quan hệ (ERD) cho việc quản lý người dùng, huấn luyện viên (coach) và lịch đặt hẹn.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 5 | - Nghiên cứu yêu cầu nghiệp vụ, định hình các tính năng cốt lõi của nền tảng Web IT Coach | 12/06/2026 | 12/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | - Thiết kế kiến trúc tổng thể ứng dụng: Next.js (Frontend), Node.js/Express (Backend), S3 (Media), RDS PostgreSQL (Database) | 13/06/2026 | 13/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 2 | - Thiết kế kiến trúc hạ tầng mạng AWS VPC bảo mật với Public Subnet và Private Subnet | 15/06/2026 | 15/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Thiết kế sơ đồ cơ sở dữ liệu quan hệ ERD, định nghĩa các bảng và mối quan hệ thực thể | 16/06/2026 | 16/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Đánh giá giải pháp bảo mật hạ tầng (Security Groups, IAM Roles) và khởi tạo repository Git mẫu cho dự án | 17/06/2026 | 18/06/2026 | https://cloudjourney.awsstudygroup.com/ |

### Kết quả đạt được tuần 9:
* **Thiết kế hệ thống:**
  - Hoàn thành tài liệu phân tích yêu cầu nghiệp vụ cho Web IT Coach bao gồm: quản lý tài khoản, danh sách coach, tìm kiếm/lọc coach theo kỹ năng, đặt lịch hẹn (booking) và hệ thống đánh giá (reviews).
  - Thống nhất mô hình kiến trúc: Client -> Application Load Balancer -> Web Server (EC2) -> Database Server (RDS PostgreSQL).
* **Thiết kế hạ tầng mạng:**
  - Thiết kế sơ đồ AWS VPC chia thành 2 Availability Zones để tăng tính chịu lỗi.
  - Phân vùng Public Subnets (chứa ALB, NAT Gateway) và Private Subnets (chứa EC2 Backend và RDS Database) để ngăn chặn truy cập trực tiếp từ Internet vào dữ liệu nhạy cảm.
* **Thiết kế cơ sở dữ liệu & Dự án:**
  - Hoàn thiện sơ đồ ERD với các thực thể chính: `Users`, `Coaches`, `Bookings`, `Reviews`, `Transactions`.
  - Khởi tạo thành công kho mã nguồn Git và phân chia các nhánh phát triển cho Frontend và Backend.
