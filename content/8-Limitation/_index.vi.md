---
title: "Những hạn chế và hướng phát triển trong tương lai"
date: 2026-07-30
weight: 8
chapter: false
pre: " <b> 8. </b> "
---

----


Mặc dù hệ thống đã được triển khai thành công theo đúng mục tiêu của buổi Workshop, mô hình hiện tại vẫn gặp một số giới hạn do phụ thuộc vào chính sách tài khoản cũng như tối ưu hóa chi phí.

## 1. Hạn chế hiện tại

* **Rào cản từ giới hạn của tài khoản AWS Free Tier:** 
  * **Tên miền & SSL/TLS:** Tài khoản Free Tier không hỗ trợ đầy đủ các tính năng của **Amazon Route 53**, dẫn đến việc không thể đăng ký tên miền tùy chỉnh (custom domain) và khởi tạo chứng chỉ SSL/TLS miễn phí qua **AWS Certificate Manager (ACM)** để định tuyến traffic bảo mật qua cổng HTTPS (`443`).
  * **Cơ sở dữ liệu (Database):** Dịch vụ **Amazon RDS** chỉ triển khai ở chế độ Single-AZ. Cấu hình **Multi-AZ** (sao lưu đồng bộ sang Availability Zone khác) bị khóa h khiến hệ thống database chưa có khả năng tự động chuyển vùng dữ liệu khi gặp sự cố (Failover).

* **Áp lực truy vấn lên Database (RDS Bottleneck):** 
  * Do ứng dụng thương mại điện tử MonaPerfume chỉ truy xuất dữ liệu trực tiếp từ Amazon RDS, các hành động lặp đi lặp lại của người dùng như xem danh mục sản phẩm, duyệt chi tiết mặt hàng sẽ liên tục kích hoạt các câu lệnh `SELECT`. Khi lượng truy cập tăng cao, việc này không chỉ làm tăng độ trễ (latency) mà còn đẩy chi phí vận hành RDS lên rất cao.

---

## 2. Hướng giải quyết và Phát triển tương lai

* **Nâng cấp tài khoản & Hoàn thiện hạ tầng bảo mật:** 
  * Chuyển đổi sang tài khoản trả phí (Pay-As-You-Go) để mở khóa đầy đủ tính năng.
  * Tích hợp **Amazon Route 53** kết hợp **AWS ACM** để gắn tên miền chuyên nghiệp và bật mã hóa HTTPS (port 443) cho Application Load Balancer (ALB).
  * Kích hoạt chế độ **Multi-AZ** cho Amazon RDS để đảm bảo tính sẵn sàng cao (High Availability) và khôi phục sau thảm họa (Disaster Recovery).

* **Tích hợp Caching Layer với Amazon ElastiCache:** 
  * Triển khai dịch vụ **Amazon ElastiCache (Redis/Memcached)** làm bộ nhớ đệm trung gian trước Database.
  * Sử dụng ElastiCache để lưu trữ:
    * **User Sessions:** Giữ phiên đăng nhập của khách hàng ổn định khi Auto Scaling thêm/bớt các máy chủ EC2.
    * **Giỏ hàng tạm thời (Temporary Shopping Cart):** Giảm tải lưu trữ tức thì xuống cơ sở dữ liệu chính.
    * **Danh mục sản phẩm hot/truy cập nhiều:** Trả về kết quả ngay lập tức từ bộ nhớ RAM thay vì query lại