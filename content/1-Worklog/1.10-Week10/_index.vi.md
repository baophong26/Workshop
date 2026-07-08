---
title: "Worklog Tuần 10"
date: 2026-06-19
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

### Mục tiêu tuần 10:
* Thiết kế và phát triển giao diện Web (Next.js) và các API dịch vụ backend (Node.js/Express hoặc NestJS).
* Triển khai hệ thống Authentication an toàn với JWT và phân quyền người dùng (User, Coach).
* Tích hợp kết nối cơ sở dữ liệu Amazon RDS PostgreSQL và lưu trữ tệp tin trên Amazon S3 từ ứng dụng.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 5 | - Lập trình giao diện Frontend (Landing Page, bảng điều khiển tìm kiếm Coach) bằng Next.js và Tailwind CSS | 19/06/2026 | 19/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | - Xây dựng các RESTful API Backend: Đăng nhập/Đăng ký với mã hóa mật khẩu bcrypt, JWT Auth | 20/06/2026 | 20/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 2 | - Thiết lập kết nối từ Backend đến database RDS PostgreSQL (nằm trong Private Subnet) và chạy migration tạo bảng | 22/06/2026 | 22/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Xây dựng các API nghiệp vụ cốt lõi: Lấy danh sách Coach, lọc theo kỹ năng (skills), và đặt lịch hẹn | 23/06/2026 | 23/06/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Tích hợp thư viện AWS SDK vào Backend để thực hiện upload ảnh đại diện và tài liệu chứng chỉ của Coach lên Amazon S3 | 24/06/2026 | 25/06/2026 | https://cloudjourney.awsstudygroup.com/ |

### Kết quả đạt được tuần 10:
* **Phát triển Web & API:**
  - Hoàn thành giao diện Landing Page hiển thị danh sách Coach sinh động và các bộ lọc tìm kiếm theo chuyên môn.
  - Xây dựng luồng Authentication hoàn chỉnh sử dụng JWT, phân quyền truy cập giữa học viên và Coach trên hệ thống.
  - Thiết lập thành công các APIs CRUD danh sách Coach và tạo yêu cầu đặt lịch hẹn (Booking Session).
* **Kết nối hạ tầng phần mềm:**
  - Kết nối ứng dụng Backend với cơ sở dữ liệu quan hệ RDS PostgreSQL thông qua Prisma/TypeORM, cấu hình connection pool tối ưu.
  - Tích hợp thành công chức năng upload file trực tiếp lên Amazon S3 thông qua SDK, sử dụng IAM Role (không cần lưu Access Key trong mã nguồn) để lưu trữ avatar người dùng và chứng chỉ kỹ năng của Coach.
