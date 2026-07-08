---
title: "Blog 2 - AWS Agentic AI"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# AWS AGENTIC AI – ỨNG DỤNG AI THÔNG MINH TRONG HỆ THỐNG ERP SAP

Trong quá trình thực tập và tìm hiểu các dịch vụ AI trên nền tảng AWS, **Agentic AI** là một trong những chủ đề nổi bật liên quan đến việc ứng dụng Generative AI vào các hệ thống nghiệp vụ doanh nghiệp.

Theo bài viết "Transforming ERP with Agentic AI" được AWS và Accenture công bố, Agentic AI được xây dựng nhằm hỗ trợ xử lý các ngoại lệ (Exception Management) trong hệ thống SAP ERP, giúp đơn giản hóa quá trình phân tích dữ liệu, xác định nguyên nhân sự cố và hỗ trợ đưa ra các phương án xử lý phù hợp.

## KIẾN TRÚC TỔNG QUAN

Trong giải pháp này, Agentic AI hoạt động như một trợ lý thông minh có khả năng phân tích dữ liệu và hỗ trợ xử lý các vấn đề phát sinh trong quy trình ERP.

Người dùng có thể tương tác với hệ thống thông qua giao diện hội thoại tự nhiên. AI Agent sẽ truy xuất dữ liệu từ SAP S/4HANA, kết hợp với tài liệu SOP, dữ liệu nghiệp vụ và lịch sử xử lý trước đó để xác định nguyên nhân của sự cố cũng như đề xuất hướng giải quyết phù hợp.

![Kiến trúc AWS Agentic AI](/images/blog2.jpg)

Kiến trúc được xây dựng trên các dịch vụ AWS như:

* **Amazon Bedrock** - Nền tảng AI/ML
* **Bedrock AgentCore** - Orchestration và reasoning
* **AWS Lambda** - Serverless compute
* **Amazon RDS** - Database management
* **AWS Step Functions** - Workflow orchestration

Sự kết hợp giữa các dịch vụ này cho phép Agentic AI thực hiện quá trình truy xuất dữ liệu, suy luận và hỗ trợ người dùng trong việc giải quyết các vấn đề nghiệp vụ phức tạp.

## DIGITAL ASSISTANT – TRỢ LÝ AI TRONG ERP

Một trong những thành phần nổi bật của kiến trúc là **Digital Assistant**.

Thay vì phải tra cứu nhiều nguồn tài liệu hoặc phụ thuộc hoàn toàn vào kinh nghiệm của đội ngũ vận hành, người dùng có thể sử dụng ngôn ngữ tự nhiên để trao đổi với hệ thống.

Digital Assistant có khả năng:

* Truy xuất thông tin liên quan đến sự cố
* Tìm kiếm tài liệu hướng dẫn xử lý
* Tổng hợp dữ liệu từ nhiều nguồn
* Hỗ trợ giải thích nguyên nhân phát sinh lỗi
* Đề xuất các bước xử lý phù hợp

Mô hình này giúp đơn giản hóa quá trình tiếp cận thông tin và hỗ trợ nâng cao hiệu quả xử lý nghiệp vụ.

## AGENTIC AI – TỪ CHATBOT ĐẾN HỆ THỐNG CÓ KHẢ NĂNG SUY LUẬN

Điểm khác biệt của Agentic AI nằm ở khả năng thực hiện nhiều bước suy luận để giải quyết một mục tiêu cụ thể.

Khác với chatbot truyền thống chỉ cung cấp câu trả lời dựa trên nội dung được truy vấn, Agentic AI có thể:

* Phân tích dữ liệu nghiệp vụ
* Xác định nguyên nhân gây ra lỗi
* Liên kết dữ liệu từ nhiều hệ thống khác nhau
* Đề xuất phương án xử lý
* Hỗ trợ người dùng trong quá trình ra quyết định

Đây là một trong những hướng phát triển quan trọng của Generative AI khi AI không chỉ tạo nội dung mà còn tham gia hỗ trợ giải quyết các bài toán vận hành thực tế.

## Ý NGHĨA ĐỐI VỚI VIỆC TÌM HIỂU CÔNG NGHỆ AWS

Trong môi trường thực tập và học tập về AWS, Agentic AI là một ví dụ điển hình cho việc kết hợp giữa dịch vụ AI, dữ liệu nghiệp vụ và quy trình vận hành doanh nghiệp.

Thông qua kiến trúc này có thể thấy vai trò của các dịch vụ như Amazon Bedrock và Bedrock AgentCore không chỉ dừng lại ở việc triển khai mô hình ngôn ngữ lớn mà còn hỗ trợ xây dựng các AI Agent có khả năng xử lý các tác vụ phức tạp trong môi trường thực tế.

Đây cũng là một ví dụ tiêu biểu cho xu hướng phát triển của Generative AI trong các hệ thống ERP và Business Applications hiện nay.

## KẾT LUẬN

Agentic AI đang mở ra một hướng tiếp cận mới trong việc ứng dụng trí tuệ nhân tạo vào các hệ thống ERP. Thông qua khả năng phân tích dữ liệu, suy luận và hỗ trợ xử lý ngoại lệ, giải pháp này cho thấy tiềm năng lớn trong việc nâng cao hiệu quả vận hành và tối ưu hóa quy trình nghiệp vụ.

Bên cạnh đó, kiến trúc Agentic AI cũng cho thấy cách AWS đang kết hợp Amazon Bedrock, Bedrock AgentCore và các dịch vụ liên quan để xây dựng các hệ thống AI có khả năng hỗ trợ xử lý những bài toán thực tế thay vì chỉ dừng lại ở các ứng dụng chatbot truyền thống.

**Link bài viết gốc:** [Transforming ERP with Agentic AI](https://aws.amazon.com/vi/blogs/awsforsap/transforming-erp-with-agentic-ai/)