---
title: "Blog 3 - AWS Security Analytics"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# AWS SECURITY ANALYTICS – XÂY DỰNG HỆ THỐNG SIEM ĐÁM MÂY VỚI AMAZON OPENSEARCH VÀ SECURITY LAKE

Trong môi trường điện toán đám mây hiện đại, việc thu thập, chuẩn hóa và phân tích log bảo mật từ nhiều nguồn khác nhau (VPC Flow Logs, CloudTrail, DNS Logs) luôn là một bài toán nan giải. Việc tự thiết lập và duy trì các hệ thống SIEM (Security Information and Event Management) truyền thống thường đòi hỏi cấu hình máy chủ phức tạp và rất khó mở rộng khi lượng log mạng tăng đột biến.

Vào giữa năm 2024, AWS đã giới thiệu một hướng tiếp cận tối ưu: kết hợp **Amazon Security Lake** với cụm **Amazon OpenSearch**. Kiến trúc này cung cấp một giải pháp phân tích an ninh mạng (Security Analytics) hoàn toàn trên đám mây, tự động chuẩn hóa dữ liệu theo định dạng chung và phân tích mối đe dọa theo thời gian thực mà không cần bảo trì hạ tầng vật lý.

## KIẾN TRÚC TỔNG QUAN

Trong kiến trúc này, quy trình xử lý sự kiện an ninh được tự động hóa xuyên suốt từ khâu thu thập đến khâu cảnh báo.

Toàn bộ log từ cơ sở hạ tầng mạng sẽ được đẩy về Amazon Security Lake. Thay vì sử dụng các công cụ chuyển đổi dữ liệu phức tạp, hệ thống tận dụng **OpenSearch Ingestion Pipeline** để đẩy trực tiếp dữ liệu vào cụm Amazon OpenSearch Service. Cụm máy chủ này được đặt an toàn trong một VPC, trải dài qua 3 Availability Zones để đảm bảo tính sẵn sàng cao (High Availability). Toàn bộ hạ tầng mạng và các thiết lập tự động hóa được triển khai tự động qua CloudFormation kết hợp với AWS Lambda.

![Kiến trúc AWS Security Analytics](/images/blog3.jpg)

## AMAZON OPENSEARCH SECURITY ANALYTICS – TRUNG TÂM SOC ĐÁM MÂY

Thành phần cốt lõi của giải pháp là **OpenSearch Security Analytics**.

Vượt ra ngoài khả năng của một công cụ tìm kiếm log đơn thuần, dịch vụ này cung cấp sẵn các bộ quy tắc (rules) bảo mật theo chuẩn ngành và các bảng điều khiển (dashboard) theo dõi trực quan.

Giải pháp mang lại nhiều lợi ích vượt trội:

* **Không cần ETL thủ công** - Không tốn công sức xây dựng hay duy trì các đường ống ETL
* **Tự động chuẩn hóa** - Chuẩn hóa mọi định dạng log về ngôn ngữ OCSF (Open Cybersecurity Schema Framework)
* **Phát hiện thời gian thực** - Detect rủi ro mạng và các hoạt động dị thường gần như ngay lập tức (Near Real-time)
* **Zero-ETL** - Truy vấn trực tiếp kho dữ liệu cũ lưu trong Security Lake mà không cần sao chép dữ liệu
* **Dễ dàng cảnh báo** - Định tuyến cảnh báo sự cố qua Amazon SQS hoặc SNS

## TRẢI NGHIỆM THỰC TẾ

Khi từng trực tiếp thiết lập dự án hệ thống tường lửa giám sát tập trung SIEM với bộ ba **pfSense, Suricata và ELK Stack**, mình hiểu rõ những vất vả trong việc cấu hình pipeline phân tích từng dòng log hay việc phải liên tục tối ưu hóa tài nguyên cho các node Elasticsearch.

Tiếp cận kiến trúc Security Analytics mà AWS đẩy mạnh từ năm 2024 mang lại một sự nâng cấp đáng giá. Về bản chất, OpenSearch là sự kế thừa trực tiếp từ hệ sinh thái ELK quen thuộc, nên các khái niệm quản trị rất gần gũi. Tuy nhiên, sự kết hợp với Security Lake và AWS Lambda đã biến nó thành một luồng xử lý tự động hoàn toàn. 

Không còn nỗi lo máy chủ ảo bị thắt cổ chai khi lượng cảnh báo từ hệ thống IDS/IPS đổ về quá lớn; thay vào đó, kiến trúc cloud-native này tự động giãn nở, cho phép đội ngũ vận hành tập trung tối đa vào việc phân tích và phản ứng với các mối đe dọa mạng.

## KẾT LUẬN

Xây dựng hệ thống giám sát an ninh tập trung không còn đồng nghĩa với việc "lắp ráp" từng thành phần mã nguồn mở và bảo trì máy chủ thủ công. Với sự kết hợp của Amazon OpenSearch và Security Lake, các hệ thống mạng quy mô lớn sở hữu một nền tảng SIEM vững chắc, có khả năng xử lý hàng Terabyte log mỗi ngày.

Bằng cách tận dụng triệt để sức mạnh mở rộng của AWS, việc thiết lập một trung tâm phân tích bảo mật toàn diện nay có thể hoàn thành nhanh chóng và tinh gọn hơn bao giờ hết.

**Link bài viết gốc:** [How to Deploy an Amazon OpenSearch Cluster to Ingest Logs from Amazon Security Lake](https://aws.amazon.com/blogs/security/how-to-deploy-an-amazon-opensearch-cluster-to-ingest-logs-from-amazon-security-lake/)
