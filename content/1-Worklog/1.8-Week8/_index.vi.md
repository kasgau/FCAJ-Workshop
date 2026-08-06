---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Quản lý thông tin cấu hình nhạy cảm (API Keys, DB Credentials) an toàn bằng AWS Systems Manager Parameter Store.
* Tìm hiểu nhiều hơn về WAF
* Tìm hiểu dịch vụ Amazon ElastiCache để tối ưu chi phí.
### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ----------| ------------ | --------------- | -------------- |
| 2,3   | - Nghiên cứu cơ chế hoạt động của tường lửa ứng dụng web và thực hiện các bài lab kèm theo | 20/07/2026   | 21/07/2026  |[AWS Web Application Firewall](https://000026.awsstudygroup.com/vi/)|
| 4, 5 | - Nghiên cứu về dịch vụ Amazon ElastiCache và cách triển khai trong project.  | 22/07/2026 | 23/07/2026 | [Amazon ElastiCache - Redis](https://000061.awsstudygroup.com/vi/)|
| 6 | - Tìm hiểu và áp dụng dịch vụ lưu trữ thông tin bảo mật AWS Secrets Manager.  | 24/07/2026 | 24/07/2026      | [Sử dụng AWS Secrets Manager với Amazon RDS và AWS Fargate](https://000096.awsstudygroup.com/vi/)|


### Kết quả đạt được tuần 8:

* Biết cách thiết lập các luật chặn lọc mã độc và truy cập trái phép bằng AWS WAF để bảo vệ an toàn cho các đầu cuối Web API.
* Nắm vững phương pháp bảo mật thông tin cấu hình ứng dụng bằng AWS Secrets Manager, loại bỏ hoàn toàn việc hardcode các thông tin đăng nhập trong mã nguồn.
* Hiểu được cơ chế của Amazon ElastiCache