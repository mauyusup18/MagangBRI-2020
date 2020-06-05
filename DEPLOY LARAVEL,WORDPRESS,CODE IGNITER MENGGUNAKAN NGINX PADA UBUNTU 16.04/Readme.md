# CARA DEPLOY LARAVEL,WORDPRESS,CODE IGNITER MENGGUNAKAN NGINX PADA UBUNTU

## A. DEPLOY LARAVEL MENGGUNAKAN NGINX PADA UBUNTU 16.04

### 1. Update ubuntu dan lakukan install nginx

    sudo apt update
    sudo apt install nginx
### 2. Install PHP 7.2-FPM dan Module Pendukung

    sudo apt install php7.2-fpm php7.2-mbstring php7.2-xmlrpc php7.2-soap php7.2-gd php7.2-xml php7.2-cli php7.2-zip
### 3. Setelah menginstal PHP, jalankan perintah di bawah ini untuk membuka file default PHP-FPM.

    sudo nano /etc/php/7.2/fpm/php.ini
Kemudian buat perubahan baris berikut di bawah dalam file dan simpan.

    memory_limit = 256M
    upload_max_filesize = 64M
    cgi.fix_pathinfo=0
### 4. Instal Komposer untuk Mengunduh Laravel

    curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
Selanjutnya Ubah ke direktori Laravel dan jalankan perintah di bawah ini untuk mengunduh dan menginstal Laravel untuk proyek yang ingin Anda buat ... beri nama proyek apa pun yang Anda inginkan . Saya membuat dengan nama MyProject .

    cd /var/www/html
    sudo composer create-project laravel/laravel MyProject --prefer-dist
Setelah menjalankan perintah di atas, direktori proyek baru akan dibuat ... Jalankan perintah di bawah ini untuk mengatur izin yang benar untuk direktori itu.

    sudo chown -R www-data:www-data /var/www/html/MyProject/
    sudo chmod -R 755 /var/www/html/MyProject/
###  5. Melakukan Konfigurasi Nginx

    sudo nano /etc/nginx/sites-available/laravel
Kemudian salin dan tempel konten di bawah ini ke dalam file dan simpan. Ganti baris yang disorot dengan nama domain dan lokasi root direktori Anda sendiri.

    server {
        listen 80;
        listen [::]:80;
        root /var/www/html/MyProject/public;
        index  index.php index.html index.htm;
        server_name  webshopucup.id;
    
        location / {
            try_files $uri $uri/ /index.php?$query_string;        
        }
    
      
        location ~ \.php$ {
           include snippets/fastcgi-php.conf;
           fastcgi_pass             unix:/var/run/php/php7.2-fpm.sock;
           fastcgi_param   SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }
    
    }
Save file dan exit.

### 6. Mengaktifkan Laravel
Setelah mengkonfigurasi VirtualHost di atas, aktifkan dengan menjalankan perintah di bawah ini

    sudo ln -s /etc/nginx/sites-available/laravel /etc/nginx/sites-enabled/
### 7. Restart Nginx
Untuk memuat semua pengaturan di atas, restart Nginx dengan menjalankan perintah di bawah ini.

    sudo systemctl restart nginx.service
### 8. Ubah File Host Lokal Untuk Pengujian
Untuk melakukan perubahan pada file host, jalankan perintah dibawah ini :

    sudo nano /etc/hosts
<img src="pict/L2.PNG">


### 9.  Melakukan pengetesan
Kemudian buka browser Anda dan browse ke nama domain server. Anda akan melihat halaman Laravel.
http://webshopucup.id

<img src="pict/L1.PNG">

