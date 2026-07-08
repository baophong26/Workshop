---
title: "Worklog Tuần 3"
date: 2026-05-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:
* Nắm vững kiến thức cơ bản về máy chủ ảo EC2, cách quản lý lưu trữ với EBS và bảo mật truy cập.
* Làm quen và sử dụng thành thạo các câu lệnh điều khiển hệ thống thông qua AWS CLI.
* Làm việc với môi trường lập trình tích hợp trên đám mây (Cloud IDE) bằng AWS Cloud9.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 5 | - Tìm hiểu lý thuyết về Amazon EC2: Instance Types, AMI, Key Pairs, Security Groups | 01/05/2026 | 01/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | - Thực hành khởi tạo EC2 instance Linux, cấu hình EBS Volume và kết nối SSH | 02/05/2026 | 02/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 2 | - Cài đặt AWS CLI trên máy cá nhân, cấu hình IAM Credentials (Access/Secret Key) | 04/05/2026 | 04/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Thực hành truy vấn thông tin EC2, tạo & xoá tài nguyên thông qua AWS CLI | 05/05/2026 | 05/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Khởi tạo môi trường lập trình AWS Cloud9, tích hợp Git và viết mã trực tiếp | 06/05/2026 | 07/05/2026 | https://cloudjourney.awsstudygroup.com/ |

### Kết quả đạt được tuần 3:
* **Amazon EC2 & EBS:**
  - Khởi tạo thành công máy chủ ảo Linux (Amazon Linux 2 / Ubuntu), cấu hình Security Groups chỉ cho phép kết nối qua SSH (cổng 22) từ IP cá nhân.
  - Tạo, gắn (attach) và định dạng (mount) thêm EBS Volume vào EC2 để lưu trữ dữ liệu bền vững độc lập với vòng đời của Instance.
* **AWS CLI:**
  - Cấu hình thành công AWS CLI sử dụng các profile khác nhau.
  - Sử dụng các lệnh CLI thông dụng như `aws ec2 describe-instances`, `aws s3 ls`, `aws iam list-users` để quản lý tài nguyên hệ thống từ Terminal cá nhân.
* **AWS Cloud9:**
  - Tạo lập thành công một Cloud9 Development Environment giúp lập trình và chạy thử mã nguồn trực tiếp trên giao diện trình duyệt web mà không cần cài đặt môi trường phức tạp trên máy cục bộ.
