# TOPIC 8
## VestaCP

### Cài đặt VestaCP
- Truy cập vào trang chủ vestaCP: https://vestacp.com/ và chọn Install
![](Chup_man_hinh/2025-09-22_11-15.png)
- Nhập các thông tin cần cho website của bạn, sẽ xuất hiện hướng dẫn cài đặt VestaCP:
![](Chup_man_hinh/2025-09-22_11-18.png)
- Sau khi cài đặt thành công sẽ hiện thông tin tài khoản và mật khẩu để đăng nhập

![](Chup_man_hinh/2025-09-22_11-55.png)

- Truy cập vào trình duyệt tại https://103.90.226.77:8083, đăng nhập bằng tài khoản vừa được tạo sau khi cài đặt.

![alt text](./image-topic8/image-5.png)
![alt text](image-6.png)

- Truy cập vào web để tạo một website mới cho wordpress (laravel cũng tương tự). Điền các thông tin liên quan tới domain, proxy, ip, ssl(crt, key).
![alt text](./image-topic8/image-7.png)
![alt text](./image-topic8/image-8.png)
![alt text](./image-topic8/image-10.png)

- Tạo database và điền các thông tin về cho Wordpress (Laravel cũng thực hiện tương tự). Sau đó truy cập phpmyadmin sử dụng tài khoản đã tạo để đăng nhập và import CSDL

![alt text](./image-topic8/image-11.png)
![alt text](./image-topic8/image-12.png)

- Upload Source code: tạo tài khoản ftp để đăng nhập và upload từ máy client. Sau đó chuyển source-code vào docRoot của web (`/home/admin/web/wp.chiennguyen.vietnix.tech/public_html`)

![alt text](./image-topic8/image-13.png)
![alt text](./image-topic8/image-14.png)

- Cấu hình wp-config.php theo thông tin database vừa tạo.

![alt text](./image-topic8/image-15.png)

- Truy cập website để kiểm thử web.

![alt text](./image-topic8/image-16.png)
