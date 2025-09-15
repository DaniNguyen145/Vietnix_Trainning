# TOPIC 4:
## Xây dựng mô hình reverse proxy kết hợp giữa 2 webserver 'Nginx' và 'Apache': 
### Cài đặt apache:
- Cập nhật hệ thống và cài Apache:
    ```
    sudo apt update && sudo apt upgrade -y      #Cập nhật hệ thống
    sudo apt install apache2 -y                 #Cài Apache
    sudo systemctl status apache2               #Kiểm tra trạng thái ApacheApache
    ```
- Sau khi kiểm tra trạng thái nếu màn hình hiển thị Active: failed
    ```
     × apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: failed (Result: exit-code) since Fri 2025-09-12 10:33:53 +07; 20min ago
       Docs: https://httpd.apache.org/docs/2.4/
        CPU: 13ms

    Sep 12 10:33:53 dian-aapanel-training systemd[1]: Starting The Apache HTTP Server...
    Sep 12 10:33:53 dian-aapanel-training apachectl[166388]: (98)Address already in use: AH00072: make_sock: could not bind to address [::]:80
    Sep 12 10:33:53 dian-aapanel-training apachectl[166388]: (98)Address already in use: AH00072: make_sock: could not bind to address 0.0.0.0:80
    ```
- Apache không khởi động được vì cổng 80 đã bị Nginx chiếm (Address already in use).
  Đây là lý do khi xây dựng mô hình reverse proxy thì:
  - **Nginx** đứng trước, chiếm cổng 80/443 để nhận request từ client. Nginx có thể xử lý hàng chục nghìn kết nối đồng thời, phục vụ nội dung tĩnh (CSS, JS, hình ảnh, video) cực nhanh và giảm tải đáng kể cho backend. Và những request động sẽ được Nginx proxy_pass về Apache
  - **Apache** chạy sau, . Khi đó, Apache chỉ tập trung xử lý các ứng dụng web như PHP, WordPress hay Laravel, thay vì phải gánh toàn bộ kết nối và file tĩnh. Và trả response lại cho Nginx, rồi Nginx trả kết quả đó lại cho client.
  - Apache tốt hơn Nginx trong việc phục vụ các trang web động, nhưng Nginx lại tốt hơn Apache trong việc phục vụ các trang web tĩnh. Do đó, để tận dụng ưu thế của cả 2 web server này, khái niệm reverse proxy đã ra đời.
    
    
- Để apache chạy được thì chúng ta phải đổi port để 2 webserver không trùng nhau
    ![Thay đổi port](/Chụp20%màn20%hình/2025-09-12_15-11.png)
- Khởi động lại apache:
    ```
     sudo systemctl restart apache2
     sudo systemctl status apache2
    ```
    ```
        ● apache2.service - The Apache HTTP Server
         Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor>
         Active: active (running) since Fri 2025-09-12 11:22:20 +07; 3h 55min>
           Docs: https://httpd.apache.org/docs/2.4/
        Process: 168386 ExecStart=/usr/sbin/apachectl start (code=exited, sta>
        Main PID: 168390 (apache2)
          Tasks: 55 (limit: 11924)
         Memory: 9.4M
            CPU: 1.054s
         CGroup: /system.slice/apache2.service
                 ├─168390 /usr/sbin/apache2 -k start
                 ├─168391 /usr/sbin/apache2 -k start
                 └─168392 /usr/sbin/apache2 -k start

    ```
    Nếu thấy hiển thị active(running) thì apache đã chạy rồi, có thể truy cập vào Ip để kiểm tra
    ![Truy cập lại IP](/Chụp20%màn20%hình/2025-09-12_11-23.png)
    
### Sử dụng Vhost để xây dựng 2 website
- Cấu hình Apache: 
    - **WordPress** – /etc/apache2/sites-available/wp.conf
    ```
    <VirtualHost *:8080>
        ServerName wp.dian.vietnix.tech
        DocumentRoot /var/www/wp.dian.vietnix.tech

        SetEnvIf X-Forwarded-Proto "https" HTTPS=on

        <Directory /var/www/wp.dian.vietnix.tech>
            Options Indexes FollowSymLinks
            AllowOverride All
            Require all granted
        </Directory>

        # PHP-FPM handler
        <FilesMatch \.php$>
            SetHandler "proxy:unix:/run/php/php8.1-fpm.sock|fcgi://localhost/"
        </FilesMatch>

        ErrorLog ${APACHE_LOG_DIR}/wp_http_error.log
        CustomLog ${APACHE_LOG_DIR}/wp_http_access.log combined
    </VirtualHost>
    <VirtualHost *:8888>
        ServerName wp.dian.vietnix.tech
        DocumentRoot /var/www/wp.dian.vietnix.tech

        SSLEngine on
        SSLCertificateFile /etc/nginx/ssl/wp.dian.vietnix.tech/fullchain.crt
        SSLCertificateKeyFile /etc/nginx/ssl/wp.dian.vietnix.tech/private.key

        <Directory /var/www/wp.dian.vietnix.tech>
            Options Indexes FollowSymLinks
            AllowOverride All
            Require all granted
        </Directory>

        # PHP-FPM handler
        <FilesMatch \.php$>
            SetHandler "proxy:unix:/run/php/php8.1-fpm.sock|fcgi://localhost/"
        </FilesMatch>
      ErrorLog ${APACHE_LOG_DIR}/wp_https_error.log
        CustomLog ${APACHE_LOG_DIR}/wp_https_access.log combined
    </VirtualHost>

    ```
    - **Laravel** - /etc/apache2/sites-available/laravel.conf
    ```
    <VirtualHost *:8080>
        ServerName laravel.dian.vietnix.tech
        DocumentRoot /var/www/laravel.dian.vietnix.tech

        SetEnvIf X-Forwarded-Proto "https" HTTPS=on

        <Directory /var/www/laravel.dian.vietnix.tech>
            Options Indexes FollowSymLinks
            AllowOverride All
            Require all granted
        </Directory>

        # PHP-FPM handler
        <FilesMatch \.php$>
            SetHandler "proxy:unix:/run/php/php8.1-fpm.sock|fcgi://localhost/"
        </FilesMatch>

        ErrorLog ${APACHE_LOG_DIR}/laravel_http_error.log
        CustomLog ${APACHE_LOG_DIR}/laravel_http_access.log combined
    </VirtualHost>
    <VirtualHost *:8888>
        ServerName laravel.dian.vietnix.tech
        DocumentRoot /var/www/laravel.dian.vietnix.tech

        SSLEngine on
        SSLCertificateFile /etc/nginx/ssl/laravel.dian.vietnix.tech/fullchain.crt
        SSLCertificateKeyFile /etc/nginx/ssl/laravel.dian.vietnix.tech/private.key

        <Directory /var/www/laravel.dian.vietnix.tech>
            Options Indexes FollowSymLinks
            AllowOverride All
            Require all granted
        </Directory>

        # PHP-FPM handler
        <FilesMatch \.php$>
            SetHandler "proxy:unix:/run/php/php8.1-fpm.sock|fcgi://localhost/"
        </FilesMatch>
      ErrorLog ${APACHE_LOG_DIR}/wp_https_error.log
        CustomLog ${APACHE_LOG_DIR}/laravel_https_access.log combined
    </VirtualHost>

    ```
- Enable site và Reload Apache
    ```
    sudo a2ensite wp.dian.vietnix.tech.conf
    sudo systemctl reload apache2

    ```
    
- Cấu hình Apache lắng nghe port 8080 và 8888: '/etc/apache2/ports.conf'
    ```
            Listen 8080

        <IfModule ssl_module>
                Listen 8888
        </IfModule>

        <IfModule mod_gnutls.c>
                Listen 8888
        </IfModule>
    ```
- Cấu hình Nginx:
    - **Wordpress** - /etc/nginx/sites-available/wordpress
    ```
            server {
            listen 80;
            server_name wp.dian.vietnix.tech;

            location / {
                proxy_pass http://103.90.225.246:8080;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
            }
        }

        server {
            listen 443 ssl;
            server_name wp.dian.vietnix.tech;

            ssl_certificate /etc/ssl/wp/fullchain.crt;
            ssl_certificate_key /etc/ssl/wp/private.key;

            location / {
                proxy_pass http://103.90.225.246:8081;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
            }
        }

    ```
    - **Laravel** - /etc/nginx/sites-available/laravel
    ```
            server {
            listen 80;
            server_name laravel.dian.vietnix.tech;

            location / {
                proxy_pass http://103.90.225.246:8080;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
            }
        }

        server {
            listen 443 ssl;
            server_name laravel.dian.vietnix.tech;

            ssl_certificate /etc/ssl/laravel/fullchain.crt;
            ssl_certificate_key /etc/ssl/laravel/private.key;

            location / {
                proxy_pass http://103.90.225.246:8081;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
            }
        }

    ```
- Enable site và reload Nginx:
    ```
    sudo ln -s /etc/nginx/sites-available/wp.dian.vietnix.tech /etc/nginx/sites-enabled/
    sudo nginx -t
    sudo systemctl reload nginx

    ```
- Kiểm thử website Wordpress:
  - http://wp.dian.vietnix.tech:8080 → WordPress chạy
  - https://wp.dian.vietnix.tech:8888 → WordPress chạy với SSL (cảnh báo Không bảo mật)

  ![Wp1](Chụp20%màn20%hình/2025-09-13_11-55.png)
  ![Wp](Chụp20%màn20%hình/2025-09-13_11-55_1.png)
