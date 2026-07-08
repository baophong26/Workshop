---
title: "Worklog Tuần 4"
date: 2026-05-08
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:
* Tìm hiểu giải pháp cấp quyền bảo mật IAM Roles dành cho các tài nguyên AWS EC2.
* Thực hành tạo lập, quản lý và sử dụng kho lưu trữ đối tượng Amazon S3 để phân phối Website tĩnh.
* Cấu hình dịch vụ phân phối nội dung CDN Amazon CloudFront để tối ưu hóa hiệu năng, giảm độ trễ truy cập và tích hợp điện toán biên Lambda@Edge.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 5 | - Học về IAM Roles cho EC2; tạo Role có quyền đọc dữ liệu từ S3 và gán vào EC2 | 08/05/2026 | 08/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | - Kiểm thử gọi API S3 từ bên trong EC2 instance sử dụng quyền hạn của IAM Role | 09/05/2026 | 09/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 2 | - Tìm hiểu Amazon S3: khởi tạo Bucket, tải lên các file source HTML/CSS/JS tĩnh | 11/05/2026 | 11/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Bật tính năng Static website hosting trên S3, thiết lập Bucket Policy cho phép truy cập công khai | 12/05/2026 | 12/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Tạo phân phối Amazon CloudFront CDN, trỏ Origin về S3 Bucket, thiết lập OAI/OAC để bảo mật | 13/05/2026 | 14/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| - | - Viết hàm Lambda@Edge đơn giản để sửa đổi Header HTTP phản hồi tại Edge Locations | 14/05/2026 | 14/05/2026 | https://cloudjourney.awsstudygroup.com/ |

### Kết quả đạt được tuần 4:
* **IAM Roles for EC2:**
  - Gán IAM Role cho EC2 instance thành công. Không cần lưu trữ cứng AWS Access Key/Secret Key trong code ứng dụng chạy trên máy chủ ảo, giúp tuân thủ tuyệt đối quy định bảo mật.
* **Amazon S3 Static Website Hosting:**
  - Tạo bucket S3, tải mã nguồn giao diện HTML tĩnh lên, bật tính năng hosting và truy cập website qua liên kết endpoint dạng: `http://<bucket-name>.s3-website-<region>.amazonaws.com`.
* **Amazon CloudFront & Lambda@Edge:**
  - Triển khai thành công phân phối CloudFront CDN.
  - Sử dụng Origin Access Control (OAC) để giới hạn người dùng truy cập trực tiếp URL của S3 bucket, bắt buộc mọi lượt truy cập phải đi qua CloudFront.
  - Tích hợp thành công Lambda@Edge để tùy biến header trả về của trình duyệt, nâng cao bảo mật hệ thống từ các trạm biên.
