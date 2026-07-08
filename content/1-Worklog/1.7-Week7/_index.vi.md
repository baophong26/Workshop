---
title: "Worklog Tuần 7"
date: 2026-05-29
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:
* Tìm hiểu cơ chế tự động co giãn hệ thống máy chủ ảo thông qua EC2 Auto Scaling.
* Thiết lập hệ thống giám sát tài nguyên, thu thập log và cấu hình cảnh báo tự động bằng Amazon CloudWatch.
* Tìm hiểu dịch vụ phân giải tên miền (DNS) Amazon Route 53 và các quy tắc định tuyến thông minh.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 5 | - Học về Auto Scaling: Launch Templates, Auto Scaling Groups (ASG), Scaling Policies | 29/05/2026 | 29/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | - Thực hành tạo Launch Template, cấu hình ASG tự động thêm/bớt instance theo tải CPU | 30/05/2026 | 30/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 2 | - Tìm hiểu Amazon CloudWatch: Thu thập chỉ số hệ thống (Metrics) và cấu hình Alarms | 01/06/2026 | 01/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Cài đặt CloudWatch Agent trên EC2 để đẩy Log hệ thống lên CloudWatch Logs nhóm tập trung | 02/06/2026 | 02/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Tìm hiểu Amazon Route 53: Đăng ký domain, tạo Hosted Zone và quản lý bản ghi (A, CNAME) | 03/06/2026 | 04/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| - | - Cấu hình DNS Routing Policies (Weighted, Failover) kết hợp Health Checks của Route 53 | 04/06/2026 | 04/06/2026 | https://cloudjourney.awsstudygroup.com/ |

### Kết quả đạt được tuần 7:
* **EC2 Auto Scaling:**
  - Thiết lập thành công Auto Scaling Group (ASG) tự động duy trì số lượng máy chủ tối thiểu và tối đa tùy biến (ví dụ: Min: 1, Max: 3).
  - Giả lập tải CPU cao bằng công cụ `stress` để xác minh hệ thống kích hoạt tự động sinh thêm EC2 (Scale out) và xoá bớt EC2 khi hết tải (Scale in).
* **Amazon CloudWatch:**
  - Tạo thành công CloudWatch Alarm cảnh báo gửi thông báo qua email (Amazon SNS) khi CPU vượt quá 80% trong 5 phút.
  - Sử dụng CloudWatch Logs để phân tích log hệ điều hành tập trung trực tiếp từ Web Console.
* **Amazon Route 53:**
  - Hiểu cách hoạt động của hệ thống phân giải tên miền DNS.
  - Thiết lập thành công Health Checks để theo dõi trạng thái hoạt động của máy chủ web và cấu hình Failover Routing Policy để tự động chuyển hướng người dùng sang trang dự phòng khi máy chủ chính gặp sự cố.
