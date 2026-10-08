# Spring Boot Database & Systemd Configuration - Session 07 - Bài 3

## 1. Mục tiêu
- Khởi tạo cơ sở dữ liệu MySQL và cấu hình phân quyền người dùng bảo mật (springboot_db, spring-admin).
- Tạo tài khoản hệ thống giới hạn (spring-runner) không có shell login.
- Viết tệp tin cấu hình dịch vụ Systemd hoàn chỉnh để quản lý tiến trình Spring Boot ứng dụng.

## 2. Tệp cấu hình Systemd Service (spring-app.service)
Được đặt tại /etc/systemd/system/spring-app.service:
- Chạy dưới user: spring-runner
- Lệnh thực thi: /usr/bin/java -jar /opt/spring-app/app.jar
- Tự động restart sau 10 giây khi crash (Restart=on-failure, RestartSec=10).

## 3. Kết quả kiểm tra
- Trạng thái dịch vụ: sudo systemctl status spring-app.service (active running)
- Kiểm tra cổng lắng nghe: ss -tlnp | grep 8082 (Port 8082 đang lắng nghe bởi Java dưới user spring-runner)