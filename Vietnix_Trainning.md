# I.XÂY DỰNG MÔ HÌNH LEMP, WEBSITE WORDPRESS, LARAVEL
=============================================================================
## Các thành phần cài đặt LEMP: 
- **L**inux
- **E**nginx làm webserver
- **M**ariaDB
- **P**HP 
- phpMyAdmin
### 1. SSH vào VPS:
    ssh [name_host]@[your_host_IP]
### 2. Cập nhật host:
    root@dian-aapanel-training:~# sudo apt-get update && apt-get upgrade -y
### 3. Cài đặt Nginx trên VPS:
- Cài đặt Nginx:
    ```
    sudo apt-get install nginx-y       #Cài Nginx
    ```
- Khởi động và kiểm tra trạng thái:
    ```
    root@dian-aapanel-training:~# sudo systemctl enable nginx      #Bật khởi động cùng hệ thống
    root@dian-aapanel-training:~# sudo systemctl start nginx       #Khởi động nginx
    root@dian-aapanel-training:~# sudo systemctl status nginx      #Kiểm tra trạng thái
    ```
- Nếu bạn thấy hiển thị trạng thái active (running), thì Ngin	inx đang hoạt động
    ```
     nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset:>
     Active: __active (running)__ since Thu 2025-09-11 08:41:41 +07; 27min ago
       Docs: man:nginx(8)
     Main PID: 130274 (nginx)
      Tasks: 7 (limit: 11924)
     Memory: 6.4M
        CPU: 37ms
     CGroup: /system.slice/nginx.service
             ├─130274 "nginx: master process /usr/sbin/nginx -g daemon on; mast>
             ├─130275 "nginx: worker process" "" "" "" "" "" "" "" "" "" "" "" >
             ├─130276 "nginx: worker process" "" "" "" "" "" "" "" "" "" "" "" >
             ├─130277 "nginx: worker process" "" "" "" "" "" "" "" "" "" "" "" >
             ├─130278 "nginx: worker process" "" "" "" "" "" "" "" "" "" "" "" >
             ├─130279 "nginx: worker process" "" "" "" "" "" "" "" "" "" "" "" >
             └─130280 "nginx: worker process" "" "" "" "" "" "" "" "" "" "" "" >
        
    ```
- Bây giờ bạn hãy truy cập IP trên trình duyệt. Nếu hiện như ảnh bên dưới là đã cài Nginx thành công.
  ![Đăng nhập Nginx thành công](/Chụp%20màn%20hình/2025-09-11_08-50.png)
	
### 4. Cài đặt MariaDB trên VPS:
- Cài đặt MariaDB:
```
	root@dian-aapanel-training:~# sudo apt install mariadb-server mariadb-client
```
- Khởi động và kiểm tra trạng thái:
```
	root@dian-aapanel-training:~# sudo systemctl enable mariadb    #Bật MariaDB
	root@dian-aapanel-training:~# sudo systemctl start mariadb     #Khởi động MariaDB
	root@dian-aapanel-training:~# sudo systemctl status mariadb     #Kiểm tra trạng thái
```
- Nếu bạn thấy hiển thị trạng thái active (running), thì MariaDB đang hoạt động
```
	● mariadb.service - MariaDB 10.6.22 database server
     Loaded: loaded (/lib/systemd/system/mariadb.service; enabled; vendor prese>
     Active: active (running) since Thu 2025-09-11 08:41:41 +07; 45min ago
       Docs: man:mariadbd(8)
             https://mariadb.com/kb/en/library/systemd/
   Main PID: 130328 (mariadbd)
     Status: "Taking your SQL requests now..."
      Tasks: 8 (limit: 78703)
     Memory: 61.4M
        CPU: 804ms
     CGroup: /system.slice/mariadb.service
             └─130328 /usr/sbin/mariadbd
```
- Cấu hình MariaDB:
```
	root@dian-aapanel-training:~# sudo mysql_secure_installation
```
```
    NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

    In order to log into MariaDB to secure it, we'll need the current
    password for the root user. If you've just installed MariaDB, and
    haven't set the root password yet, you should just press enter here.

    Enter current password for root (enter for none): 
    OK, successfully used password, moving on...

    Setting the root password or using the unix_socket ensures that nobody
    can log into the MariaDB root user without the proper authorisation.

    You already have your root account protected, so you can safely answer 'n'.

    Switch to unix_socket authentication [Y/n] __n__
     ... skipping.

    You already have your root account protected, so you can safely answer 'n'.

    Change the root password? [Y/n] __n__
     ... skipping.

    By default, a MariaDB installation has an anonymous user, allowing anyone
    to log into MariaDB without having to have a user account created for
    them.  This is intended only for testing, and to make the installation
    go a bit smoother.  You should remove them before moving into a
    production environment.

    Remove anonymous users? [Y/n] __Y__
     ... Success!

    Normally, root should only be allowed to connect from 'localhost'.  This
    ensures that someone cannot guess at the root password from the network.

    Disallow root login remotely? [Y/n] __Y__
     ... Success!

    By default, MariaDB comes with a database named 'test' that anyone can
    access.  This is also intended only for testing, and should be removed
    before moving into a production environment.

    Remove test database and access to it? [Y/n] __Y__
     - Dropping test database...
     ... Success!
     - Removing privileges on test database...
     ... Success!

    Reloading the privilege tables will ensure that all changes made so far
    will take effect immediately.

    Reload privilege tables now? [Y/n] __Y__
     ... Success!

    Cleaning up...

    All done!  If you've completed all of the above steps, your MariaDB
    installation should now be secure.

    Thanks for using MariaDB!
```
- Truy cập vào MariaDB monitor:
  ```
    root@dian-aapanel-training:~# __sudo mariadb -u root__ 
  ```
	- Vậy là bạn đã cài đặt MariaDB thành công.
### 5. Cài đặt PHP:
- Cài đặt PHP trên VPS (Khi chạy Wordpress hoặc Laravel)
    ```
     __sudo apt install php8.1 php8.1-fpm php8.1-mysql php-common php8.1-cli php8.1-common php8.1-opcache php8.1-readline php8.1-mbstring php8.1-xml php8.1-gd php8.1-curl php8.1-soap php8.1-mbstring -y__
    ```
    ```
    root@dian-aapanel-training:~# __systemctl enable php8.1-fpm__    #Bật PHP
    root@dian-aapanel-training:~# __systemctl start php8.1-fpm__     #Khởi động PHP
    root@dian-aapanel-training:~# __systemctl status php8.1-fpm__    #Kiểm tra PHP
    ```
- Nếu bạn thấy hiển thị trạng thái __active (running)__, thì PHP đang hoạt động
    ```
    ● php8.1-fpm.service - The PHP 8.1 FastCGI Process Manager
     Loaded: loaded (/lib/systemd/system/php8.1-fpm.service; enabled; vendor pr>
     Active: __active (running)__ since Thu 2025-09-11 10:11:26 +07; 25s ago
       Docs: man:php-fpm8.1(8)
    Process: 143413 ExecStartPost=/usr/lib/php/php-fpm-socket-helper install /r>
   Main PID: 143410 (php-fpm8.1)
     Status: "Processes active: 0, idle: 2, Requests: 0, slow: 0, Traffic: 0req>
      Tasks: 3 (limit: 11924)
     Memory: 9.6M
        CPU: 34ms
     CGroup: /system.slice/php8.1-fpm.service
             ├─143410 "php-fpm: master process (/etc/php/8.1/fpm/php-fpm.conf)">
             ├─143411 "php-fpm: pool www" "" "" "" "" "" "" "" "" "" "" "" "" ">
             └─143412 "php-fpm: pool www" "" "" "" "" "" "" "" "" "" "" "" "" ">
    ```
### 6. Cài đặt phpMyAdmin:
    ```
    root@dian-aapanel-training:~# __sudo apt-get install phpmyadmin -y__
    ```
- Sau khi chạy lệnh => chọn và điền các thông tin cần thiết. 
    
- Đăng nhập vào MariaDB và kiểm tra phpmyadmin:
    ```
    root@dian-aapanel-training:~# __mysql -u root__
    ```
    ```
    Welcome to the MariaDB monitor.  Commands end with ; or \g.
    Your MariaDB connection id is 49
    Server version: 10.6.22-MariaDB-0ubuntu0.22.04.1 Ubuntu 22.04

    Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

    Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

    MariaDB [(none)]> show grants for phpmyadmin@localhost;
    +-------------------------------------------------------------------------------------------------------------------+
    | Grants for phpmyadmin@localhost                                                                                   |
    +-------------------------------------------------------------------------------------------------------------------+
    | GRANT USAGE ON *.* TO `phpmyadmin`@`localhost` IDENTIFIED BY PASSWORD '*722F7CEC91B2938BC59A41ED5EA6001084C0302D' |
    | GRANT ALL PRIVILEGES ON `phpmyadmin`.* TO `phpmyadmin`@`localhost`                                                |
    +-------------------------------------------------------------------------------------------------------------------+
    2 rows in set (0.000 sec)
    ```
### 7. Cấu hình và cài đặt Wordpress và Lavarel:
#### 1. Cài đặt Wordpress:
- Tải và giải nén Wordpress:
    ```
     cd /tmp
    wget https://wordpress.org/latest.tar.gz
    tar -xzvf latest.tar.gz
    sudo mv /tmp/wordpress /var/www/wordpress
   ```
- Phân quyền:
    ```
    chown -R www-data:www-data /var/www/wordpress
    chmod -R 755 /var/www/wordpress
    ```
- Cấu hình cho Wordpress:
  ```
    nano /etc/nginx/sites-available/wordpress.conf
    ```
  ```
        server {
        listen 80;
        server_name wp.dian.vietnix.tech;
    tech
        root /var/www/wordpress;
        index index.php index.html;

        location / {
            try_files $uri $uri/ /index.php?$args;
        }

        location ~ \.php$ {
            include snippets/fastcgi-php.conf;
            fastcgi_pass unix:/run/php/php8.1-fpm.sock;   # đổi theo version PHP bạn đang dùng
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }

        location ~ /\.ht {
            deny all;
        }
    }
    ```
- Sau đó truy cập vào đường dẫn :'http://wp.dian.vietnix.tech/' sẽ hiện giao diện của Wordpress. 
    [Giao diện Wordpress](/Chụp%20màn%20hình/2025-09-11_11-20.png)
- Chọn ngôn ngữ và nhập thông tin chi tiết. 
    [Giao diện Wordpress](/Chụp%20màn%20hình/2025-09-11_11-35.png)
#### 2. Cài đặt Laravel:
    - Cài đặt Composer: 
    '''
    sudo apt install  composer php php-curl php-bcmath php-json php-mysql php-mbstring php-xml php-tokenizer php-zip git -y
    '''
    - Kiểm tra phiên bản Composer đã cài đặt:
    '''
    sudo -u www-data composer -v
    '''
          ______
      / ____/___  ____ ___  ____  ____  ________  _____
     / /   / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
    / /___/ /_/ / / / / / / /_/ / /_/ (__  )  __/ /
    \____/\____/_/ /_/ /_/ .___/\____/____/\___/_/
                        /_/
    Composer 2.2.6 2022-02-04 17:00:38
    '''
- Cấu hình cho Lavarel:
    '''
    sudo nano /etc/nginx/sites-available/laravel.tule.vietnix.tech
    '''
- Sao chép nội dung file cấu hình dưới đây vào:
    bash
        server {
        listen 80;
        server_name laravel.dian.vietnix.tech;  #Thay đổi bằng domain của bạn

        root /var/www/laravel/public;
        index index.php index.html;

        location / {
            try_files $uri $uri/ /index.php?$query_string;
        }

        location ~ \.php$ {
            include snippets/fastcgi-php.conf;
            fastcgi_pass unix:/run/php/php8.1-fpm.sock;   # đổi đúng version PHP bạn cài
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }

        location ~ /\.ht {
            deny all;
        }
        }
    
    - Kích hoạt site và khởi động lại Nginx:
    bash
    ln -s /etc/nginx/sites-available/laravel /etc/nginx/sites-enabled/
    nginx -t
    systemctl restart nginx
    
    - Sau khi khởi động lại, có thể kiểm tra lại bằng file info.php
    '''
    echo "<?php phpinfo();" > /var/www/laravel/public/info.php

    '''
    - Truy cập vào trang thử:'http://laravel.dian.vietnix.tech/info.php'
    ![Giao diện thử lavarel](/hChụp%20màn%20hình/2025-09-11_14-34.png)
    
    Nếu thấy có thông tin php thì chứng tỏ website laravel đã hoạt động.

    - Bạn có thể truy cập vào trang lavarel của bạn:'http://laravel.dian.vietnix.tech/'
    ![Giao diện lavarel](/Chụp%20màn%20hình/2025-09-11_14-21.png)
    
## Cài SSL cho 2 domain với ZeroSSL
- Truy cập vào'https://www.sslforfree.com/' để đăng ký tài khoản.
    ![Giao diện ZeroSSL](/Chụp%20màn%20hình/2025-09-11_14-51.png)
- Tạo Certificate và chọn thời hạn SSL:
    ![Giao diện ZeroSSL](/Chụp%20màn%20hình/2025-09-11_15-00.png)
- Xác thực tên miền bằng cách upload file: 
    ![Giao diện xác thực](/Chụp%20màn%20hình/1.png)
- Làm theo hướng dẫn và tải file chứng chỉ:
    ![Giao diện xác thực](/Chụp%20màn%20hình/2025-09-11_15-20.png)
- Giải nén file và tạo thư mục lưu chứng chỉ:
    ![Giao diện](/Chụp%20màn%20hình/2025-09-11_15-24.png)
    ```
    mkdir -p /etc/nginx/ssl/laravel

    ```
    - Copy 3 file vào thư mục:
  ```
    cp certificate.crt /etc/nginx/ssl/laravel/
    cp ca_bundle.crt /etc/nginx/ssl/laravel/
    cp private.key /etc/nginx/ssl/laravel/

  ```
    - Gộp 2 file certificate.crt và ca_bundle.crt thành 1 file '.crt'
    '''
    cat certificate.crt ca_bundle.crt > /etc/nginx/ssl/laravel/fullchain.crt

    '''
    - Chỉnh sửa config Nginx cho domain: 
    '''
    nano /etc/nginx/sites-available/laravel
    '''
    '''





