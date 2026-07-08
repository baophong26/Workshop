---
title: "Blog 1 - AWS Systems Manager"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AWS SYSTEMS MANAGER – GIẢI PHÁP QUẢN LÝ TẬP TRUNG CHO MÔI TRƯỜNG HYBRID CLOUD

Khi doanh nghiệp vận hành đồng thời hạ tầng trên AWS và hệ thống On-Premises, việc quản lý máy chủ thường trở nên phức tạp do phải sử dụng nhiều công cụ khác nhau, mở các cổng SSH hoặc RDP để truy cập từ xa và thực hiện nhiều tác vụ vận hành thủ công.

Để giải quyết vấn đề này, AWS cung cấp **AWS Systems Manager (SSM)** – một dịch vụ giúp quản lý tập trung các tài nguyên trên AWS cũng như các máy chủ nằm ngoài AWS từ một nền tảng duy nhất.

## KIẾN TRÚC TỔNG QUAN

Trong kiến trúc này, AWS Systems Manager đóng vai trò là trung tâm điều phối. Quản trị viên có thể sử dụng AWS Console, AWS CLI, SDK hoặc PowerShell để quản lý các EC2 Windows, Linux, macOS cũng như các máy chủ vật lý hoặc máy ảo trong môi trường On-Premises.

![Kiến trúc AWS Systems Manager](/images/blog1.jpg)

## SESSION MANAGER – TRUY CẬP MÁY CHỦ AN TOÀN

Một trong những tính năng nổi bật nhất của AWS Systems Manager là **Session Manager**. Thay vì phải mở cổng SSH hoặc RDP để truy cập máy chủ, người dùng có thể kết nối trực tiếp thông qua AWS Console hoặc AWS CLI mà không cần mở bất kỳ cổng inbound nào trên hệ thống.

Giải pháp này mang lại nhiều lợi ích:

* **Tăng cường bảo mật** - Không cần mở cổng SSH/RDP ra Internet
* **Không cần Bastion Host** - Tiết kiệm chi phí và giảm độ phức tạp
* **Không cần quản lý SSH Key** - Đơn giản hóa quản lý access
* **Ghi lại lịch sử truy cập** - Audit trail đầy đủ với CloudTrail
* **Giảm rủi ro bị tấn công từ Internet** - Không expose cổng quản trị

## PATCH MANAGER – TỰ ĐỘNG HÓA CẬP NHẬT HỆ THỐNG

Ngoài Session Manager, AWS Systems Manager còn cung cấp **Patch Manager** giúp tự động hóa quá trình cập nhật hệ điều hành.

Dịch vụ hỗ trợ:

* Quét các bản vá còn thiếu
* Cập nhật hệ thống tự động
* Lập lịch bảo trì định kỳ
* Theo dõi trạng thái cập nhật

## TRẢI NGHIỆM THỰC TẾ

Trong quá trình học tập, mình đã có cơ hội triển khai AWS Systems Manager trên Windows EC2, thực hiện cấu hình SSM Agent, gán IAM Role, kết nối bằng Session Manager và thiết lập Port Forwarding để truy cập Remote Desktop.

Qua quá trình thực hành, mình nhận thấy đây là một giải pháp rất hữu ích giúp đơn giản hóa việc quản trị máy chủ đồng thời nâng cao tính bảo mật cho hệ thống.

## KẾT LUẬN

AWS Systems Manager là một dịch vụ mạnh mẽ giúp doanh nghiệp quản lý môi trường Hybrid Cloud một cách tập trung, an toàn và hiệu quả. Với các tính năng như Session Manager, Patch Manager cùng khả năng tích hợp với CloudWatch, CloudTrail và Amazon S3, đây là một trong những dịch vụ đáng chú ý khi triển khai hạ tầng trên AWS.

**Link bài viết gốc:** [Using AWS Systems Manager in Hybrid Cloud Environments](https://aws.amazon.com/blogs/architecture/using-aws-systems-manager-in-hybrid-cloud-environments/)