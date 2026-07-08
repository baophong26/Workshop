---
title: "Worklog Tuần 1"
date: 2026-04-17
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu tuần 1:
* Đăng ký tài khoản AWS Free Tier để chuẩn bị môi trường thực hành.
* Hiểu cách quản lý và giám sát chi phí để tránh phát sinh hóa đơn không mong muốn.
* Tìm hiểu hệ thống hỗ trợ (AWS Support) để xử lý các vấn đề kỹ thuật khi cần.
* Nắm vững các khái niệm cơ bản và cách thiết lập bảo mật định danh tài khoản bằng AWS IAM.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 5 | - Đăng ký tài khoản AWS Free Tier mới <br>- Cấu hình bảo mật cơ bản cho tài khoản Root | 17/04/2026 | 17/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | - Thiết lập ngân sách và cảnh báo chi phí với AWS Budgets <br>- Tìm hiểu các gói hỗ trợ kỹ thuật của AWS Support | 18/04/2026 | 18/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 2 | - Tìm hiểu dịch vụ IAM: Users, Groups, Policies, Roles <br>- Thực hành tạo tài khoản IAM User phục vụ công việc hàng ngày | 20/04/2026 | 20/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Phân quyền chi tiết cho IAM User bằng Customer Managed Policies <br>- Kích hoạt Multi-Factor Authentication (MFA) bảo mật | 21/04/2026 | 21/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Kiểm tra bảo mật định kỳ và tổng kết kiến thức tuần 1 | 22/04/2026 | 23/04/2026 | https://cloudjourney.awsstudygroup.com/ |

### Kết quả đạt được tuần 1:
* **Tạo mới tài khoản AWS:** Đăng ký thành công tài khoản Free Tier, hiểu cách liên kết thẻ thanh toán và xác minh danh tính.
* **AWS Budgets:** Tạo thành công các cảnh báo ngân sách (Budget Alarms) khi chi phí đạt ngưỡng 80% và 100% của hạn mức tự đặt ra (ví dụ: $5/tháng), giúp kiểm soát chi phí tối đa.
* **AWS Support:** Hiểu rõ sự khác biệt giữa các gói Basic, Developer, Business và Enterprise. Biết cách mở ticket hỗ trợ kỹ thuật khi gặp sự cố dịch vụ.
* **AWS IAM:**
  - Không sử dụng tài khoản Root cho các tác vụ hàng ngày theo khuyến nghị bảo mật (Best Practices).
  - Tạo nhóm người dùng (Groups) như *Admins*, *Developers* và phân quyền thông qua Policies.
  - Thiết lập và kích hoạt MFA thành công cho tài khoản Root và các IAM User quan trọng.
  - Hiểu cách viết cấu trúc JSON Policy gồm các thành phần: Effect (Allow/Deny), Action, Resource, và Condition.
