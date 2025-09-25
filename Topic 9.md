# Cấu hình Winfows Firewall
## Thực hiện allow port, allow ip trên window fw
![](Chup_man_hinh/2025-09-24_15-40.png)
![](Chup_man_hinh/2025-09-24_15-49.png)
![](Chup_man_hinh/2025-09-24_15-50.png)
![](Chup_man_hinh/2025-09-24_15-14.png)

## Thực hiện block port, block ip trên window fw
- Làm tương tự allow thay đổi sang block
![](Chup_man_hinh/2025-09-24_16-15_1.png)
![](Chup_man_hinh/2025-09-24_16-20.png)
![](Chup_man_hinh/2025-09-24_16-21.png)
## Thực hiện giới hạn port, giới hạn ip trên window fw chỉ cho phép ip chỉ định truy cập
![](Chup_man_hinh/2025-09-25_10-01.png)
# Thực hành cài đặt
## Webserver IIS, trên Webserver IIS+ Cài đặt website Wordpress mặc định+ Cài đặt SSL
- Vào server manager, chọn add roles and features
![](Chup_man_hinh/2025-09-24_16-56.png)
- Chọn các server roles và features cần thiết
![](Chup_man_hinh/2025-09-25_10-05.png)
![](Chup_man_hinh/2025-09-25_10-05_1.png)
![](Chup_man_hinh/2025-09-24_16-46.png)
![](Chup_man_hinh/2025-09-24_16-46_1.png)
- Tạo website mới  
![](Chup_man_hinh/2025-09-25_10-09.png)
![](Chup_man_hinh/2025-09-24_17-01.png)
- Download source code wordpress về và unzip vào thư mục của wp
![](Chup_man_hinh/2025-09-24_10-13.png)
- Download, unzip mysql và cài đặt mysql
![](Chup_man_hinh/2025-09-24_17-12.png)
-  Tạo database và user cho wp
![](Chup_man_hinh/2025-09-25_06-39-12.png)
- Chỉnh sửa file config:
![](Chup_man_hinh/2025-09-25_07-11.png)
- Add SSL cho website:
![](Chup_man_hinh/2025-09-25_10-21.png)
![](Chup_man_hinh/2025-09-25_10-22.png)
- Mặc định, IIS thường ưu tiên các file như index.html hoặc default.aspx khi người dùng truy cập vào thư mục gốc mà không chỉ định file cụ thể. Tuy nhiên, với WordPress thì file khởi đầu quan trọng lại là index.php. Vì vậy, ta phải vào mục Default Document trong IIS Manager và thêm index.php vào danh sách, đồng thời sắp xếp nó ở vị trí ưu tiên cao nhất.
![](Chup_man_hinh/2025-09-25_07-08.png)
- Add Handler Mapping
![](Chup_man_hinh/2025-09-25_06-47.png)
![](Chup_man_hinh/2025-09-25_07-06.png)

- Truy cập vào website để kiểm tra đã hoạt động chưa
![](Chup_man_hinh/2025-09-25_09-34.png)
## Cài đặt SQL Server: 2016
- Truy cập đường dẫn này "Link download: https://software.vietnix.tech/datastore/sources/SQL_Server/sql2016/" và tải về file .iso:
  ![](Chup_man_hinh/2025-09-25_10-50.png)
- Sau đó Mount và set up SQL Server:
  ![](Chup_man_hinh/2025-09-25_11-10.png)
