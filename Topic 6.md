# TOPIC 6:
## Cài AAPanel lên VPS:
- Cập nhật hệ thống và cài AAPanel:
    ```
    sudo apt update && sudo apt upgrade -y
    
    wget -O install.sh http://www.aapanel.com/script/install-ubuntu_6.0_en.sh
    sudo bash install.sh

    ```
    
- Sau khi cài xong màn hình sẽ hiển thị đường dẫn và thông tin để đăng nhập vào AAPanel:
    
   ![](Chup_man_hinh/2025-09-16_14-56.png)

- Truy cập vào đường dẫn sẽ hiện thi ra trang đăng nhập:

   ![](Chup_man_hinh/2025-09-17_15-35.png)

   
- Đăng nhập và tải các gói cần thiết


   ![](Chup_man_hinh/2025-09-17_10-04.png)
## Tạo website wordpress trên AAPanel
- Add site và Upload source code:


   ![](Chup_man_hinh/2025-09-17_10-20.png)
- Điền các thông tin cần thiết:
  
   ![](Chup_man_hinh/2025-09-17_16-06.png)

- Upload source code: 
   ![](Chup_man_hinh/2025-09-17_10-27.png)
   ![](Chup_man_hinh/2025-09-17_10-27_1.png)
   ![](Chup_man_hinh/2025-09-17_16-25.png)
  - Xóa file index mặc định.
   ![](Chup_man_hinh/2025-09-17_10-26.png)
- Cài SSL cho domain:
  - Nhập các thông tin cần thiết:
   ![](Chup_man_hinh/2025-09-17_16-28.png)
   ![](Chup_man_hinh/2025-09-17_10-43.png)
- Cấu hình lại file config và .env cho 2 website:
  - .env:
    ![](Chup_man_hinh/2025-09-18_12-04.png)
    ![](Chup_man_hinh/2025-09-18_12-04_1.png)
