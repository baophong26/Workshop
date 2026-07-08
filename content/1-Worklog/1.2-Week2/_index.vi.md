---
title: "Worklog Tuần 2"
date: 2026-04-24
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:
* Tìm hiểu các khái niệm nền tảng về mạng trên AWS (VPC, Subnet, Route Table, v.v.).
* Thiết lập cấu trúc mạng đa vùng (Multi-AZ VPC) để đảm bảo độ tin cậy và khả năng chịu lỗi.
* Thực hành tạo lập, kết nối và định tuyến giữa nhiều mạng VPC khác nhau.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 5 | - Học lý thuyết về Amazon VPC, CIDR block, Subnets (Public/Private) | 24/04/2026 | 24/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | - Thực hành tạo VPC thủ công, cấu hình Internet Gateway, Route Tables | 25/04/2026 | 25/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 2 | - Triển khai NAT Gateway, thiết lập định tuyến cho Private Subnet truy cập Internet | 27/04/2026 | 27/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Tham gia Workshop về mạng trên AWS: tạo Multi-VPC và kết nối VPC Peering | 28/04/2026 | 28/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Cấu hình định tuyến định hướng cho VPC Peering và kiểm tra kết nối mạng | 29/04/2026 | 30/04/2026 | https://cloudjourney.awsstudygroup.com/ |

### Kết quả đạt được tuần 2:
* **Amazon VPC:**
  - Thiết kế và khởi tạo thành công một VPC tùy chỉnh với dải IP CIDR phù hợp (ví dụ: `10.0.0.0/16`).
  - Chia nhỏ VPC thành các Public Subnets (kết nối trực tiếp với Internet qua Internet Gateway) và Private Subnets (chỉ giao tiếp nội bộ hoặc truy cập ra ngoài gián tiếp).
  - Tạo và định cấu hình Route Tables để kiểm soát lưu lượng mạng định tuyến đi qua Internet Gateway hoặc NAT Gateway.
  - Cài đặt NAT Gateway tại Public Subnet để cho phép các tài nguyên trong Private Subnet tải bản cập nhật từ Internet mà không bị bên ngoài truy cập trực tiếp.
* **AWS Network Workshop:**
  - Xây dựng mô hình Multi-VPC gồm ít nhất 2 VPC khác nhau để giả lập hai phân vùng hệ thống biệt lập.
  - Thiết lập kết nối VPC Peering kết nối chéo giữa 2 VPC, cho phép các tài nguyên sử dụng địa chỉ IP nội bộ để giao tiếp an toàn, bảo mật và có độ trễ cực thấp.
  - Cập nhật chính xác bảng định tuyến (Route Table) của cả hai VPC để chỉ định lưu lượng dữ liệu đi qua liên kết Peering.
