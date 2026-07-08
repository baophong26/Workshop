---
title: "Worklog Tuần 8"
date: 2026-06-05
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:
* Học cách quản trị hệ điều hành Windows Server chạy trên nền tảng AWS EC2.
* Tìm hiểu giải pháp quản lý định danh doanh nghiệp với dịch vụ AWS Directory Service (AWS Managed Microsoft Active Directory).
* Thiết kế và xây dựng một kiến trúc Web có độ sẵn sàng cao, chịu lỗi tốt (Fault-Tolerant) dựa trên các nguyên tắc thiết kế tối ưu của AWS.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 5 | - Khởi tạo máy chủ EC2 Windows Server, cấu hình Security Group và giải mã mật khẩu Administrator qua Key Pair | 05/06/2026 | 05/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | - Thực hành Remote Desktop (RDP) truy cập máy chủ Windows, cấu hình dịch vụ IIS Web Server | 06/06/2026 | 06/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 2 | - Tìm hiểu AWS Managed Microsoft AD: Khởi tạo thư mục Active Directory trên AWS | 08/06/2026 | 08/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Gia nhập máy chủ Windows EC2 vào Domain vừa tạo, quản lý User/Group tập trung | 09/06/2026 | 09/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Tích hợp toàn diện kiến trúc Web sẵn sàng cao: ALB, ASG chạy trên 2 Availability Zones, RDS Multi-AZ | 10/06/2026 | 11/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| - | - Kiểm thử tắt một máy chủ web ngẫu nhiên hoặc giả lập mất một AZ để xác minh tính ổn định | 11/06/2026 | 11/06/2026 | https://cloudjourney.awsstudygroup.com/ |

### Kết quả đạt được tuần 8:
* **Ứng dụng Windows trên AWS:**
  - Khởi chạy thành công Windows Server, biết cách dùng Remote Desktop Connection truy cập và thiết lập IIS (Internet Information Services) để host ứng dụng Windows.
* **AWS Managed Microsoft AD:**
  - Khởi tạo thư mục Active Directory doanh nghiệp chạy dưới dạng dịch vụ quản lý hoàn toàn trên AWS.
  - Cấu hình Domain Controller liên kết và phân quyền các tài khoản quản trị hệ thống Windows tập trung.
* **Xây dựng ứng dụng web có tính sẵn sàng cao:**
  - Triển khai thành công kiến trúc chuẩn: Người dùng -> Route 53 -> Application Load Balancer (ALB) -> Auto Scaling Group (các instances chạy trên 2 Availability Zones khác nhau) -> RDS Multi-AZ Database.
  - Khi giả lập tắt một máy chủ Web, Load Balancer tự động phát hiện lỗi và định tuyến 100% traffic sang máy chủ còn lại. Đồng thời Auto Scaling tự động tạo mới máy chủ thay thế để đảm bảo hệ thống luôn hoạt động bình thường.
