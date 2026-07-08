---
title: "Worklog Tuần 5"
date: 2026-05-15
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:
* Tìm hiểu và triển khai hệ thống cơ sở dữ liệu quan hệ (Relational Database) trên AWS sử dụng Amazon RDS.
* Làm quen với CSDL phi quan hệ (NoSQL) có hiệu năng cao và khả năng mở rộng không giới hạn thông qua Amazon DynamoDB.
* Tìm hiểu giải pháp tối ưu hóa hiệu năng truy vấn cơ sở dữ liệu bằng bộ nhớ đệm (Caching) sử dụng Amazon ElastiCache.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 5 | - Khám phá dịch vụ Amazon RDS: Các DB Engines, Multi-AZ deployments, Read Replicas | 15/05/2026 | 15/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | - Khởi tạo Database Instance RDS MySQL/PostgreSQL trong Private Subnet và kiểm thử kết nối từ EC2 | 16/05/2026 | 16/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 2 | - Tìm hiểu CSDL NoSQL Amazon DynamoDB: Tables, Partition Key, Sort Key | 18/05/2026 | 18/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Thực hành tạo DynamoDB Table, thêm dữ liệu, thực hiện thao tác Query và Scan dữ liệu | 19/05/2026 | 19/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Tìm hiểu bộ nhớ đệm Amazon ElastiCache: Khởi tạo cluster Redis/Memcached | 20/05/2026 | 21/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| - | - Kết nối ứng dụng từ EC2 tới ElastiCache để lưu cache dữ liệu, giảm tải cho RDS | 21/05/2026 | 21/05/2026 | https://cloudjourney.awsstudygroup.com/ |

### Kết quả đạt được tuần 5:
* **Amazon RDS:**
  - Khởi tạo thành công database RDS nằm trong nhóm Private Subnets bảo mật.
  - Cấu hình Security Group cho phép chỉ các máy chủ ứng dụng chỉ định trong EC2 Security Group kết nối tới database.
  - Hiểu cách tối ưu hóa tính sẵn sàng cao bằng cấu hình Multi-AZ (sao chép dữ liệu đồng bộ sang AZ khác) và tối ưu khả năng đọc bằng Read Replicas.
* **Amazon DynamoDB:**
  - Tạo thành công bảng dữ liệu phi quan hệ, phân biệt rõ cơ chế hoạt động của Query (truy vấn theo Key, hiệu năng cao, tiết kiệm chi phí) và Scan (quét toàn bộ bảng, tốn tài nguyên).
* **Amazon ElastiCache:**
  - Triển khai thành công cluster ElastiCache Redis. Hiểu cơ chế hoạt động của Cache-aside pattern để giảm thời gian phản hồi cho các câu truy vấn SQL lặp đi lặp lại.
