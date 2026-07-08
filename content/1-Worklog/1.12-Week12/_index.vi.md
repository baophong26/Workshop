---
title: "Worklog Tuần 12"
date: 2026-07-03
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

### Mục tiêu tuần 12:
* Thực hiện kiểm thử toàn bộ hệ thống (End-to-End Testing) và khắc phục các lỗi phần mềm phát sinh (Bug fixing).
* Hoàn thiện đầy đủ nội dung nhật ký công việc (Worklog) 12 tuần trên trang báo cáo Hugo.
* Chuẩn bị tài liệu kỹ thuật, slide thuyết trình cho buổi Workshop chia sẻ kiến thức dự án Web IT Coach.
* Soạn thảo và hoàn thành báo cáo kỹ thuật/báo cáo tổng kết thực tập tại doanh nghiệp.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 5 | - Chạy kiểm thử toàn trình E2E trên hệ thống live, phát hiện và lập danh sách các lỗi UI/UX và logic | 03/07/2026 | 03/07/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | - Tập trung sửa các lỗi liên quan đến định dạng thời gian đặt lịch, xử lý biệt lệ kết nối database | 04/07/2026 | 04/07/2026 | https://cloudjourney.awsstudygroup.com/ |
| 2 | - Tổng kết, viết và hoàn thiện toàn bộ hệ thống Nhật ký công việc (Worklog) trên trang Hugo | 06/07/2026 | 06/07/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Thiết kế slide thuyết trình, chuẩn bị tài liệu kỹ thuật và chạy thử demo ứng dụng phục vụ buổi Workshop | 07/07/2026 | 07/07/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Soạn thảo văn bản báo cáo kết quả thực tập, hoàn thiện các tài liệu đánh giá và nộp báo cáo tổng kết | 08/07/2026 | 09/07/2026 | https://cloudjourney.awsstudygroup.com/ |

### Kết quả đạt được tuần 12:
* **Kiểm thử & Sửa lỗi (QA/Bug Fixing):**
  - Thực hiện thành công các ca kiểm thử E2E mô phỏng hành trình học viên tìm kiếm coach, đặt lịch hẹn và thanh toán.
  - Sửa các lỗi nghiêm trọng về sai lệch múi giờ (Timezone offset) giữa máy khách và cơ sở dữ liệu PostgreSQL để đảm bảo lịch hẹn hiển thị chính xác.
  - Khắc phục lỗi tràn kết nối (Connection pool exhaustion) của database bằng cách tinh chỉnh tham số kết nối tối đa trong ORM.
* **Hoàn thiện tài liệu & Báo cáo:**
  - Hoàn thiện toàn bộ các trang Worklog từ Tuần 1 đến Tuần 12 trên hệ thống Hugo báo cáo.
  - Chuẩn bị đầy đủ tài liệu hướng dẫn vận hành, Slide PowerPoint phục vụ cho buổi Workshop kết thúc chương trình First Cloud AI Journey.
  - Hoàn thành bản Báo cáo tốt nghiệp thực tập chi tiết về thiết kế phần mềm, kiến trúc hạ tầng AWS và các bài học kinh nghiệm đạt được, sẵn sàng nộp cho đơn vị thực tập và nhà trường.
