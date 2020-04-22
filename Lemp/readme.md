## Menginstall Nginx, Mariadb, PHP (Lemp) di Ubuntu

## A. Menginstall nginx dan memperbarui firewall

### 1. Melakukan update dan upgrade pada ubuntu 
Pertama, yang perlu Anda lakukan adalah meng-update dan upgrade Ubuntu menggunakan perintah berikut :

    sudo apt-get update && apt-get upgrade

### 2. Install Nginx
Kemudian, mulai proses dengan instalasi Nginx menggunakan perintah berikut.

    sudo apt-get install nginx

### 3. Cek instalasi nginx
Setelah proses instalasi Nginx selesai, kini saatnya memastikan bahwa Nginx sudah benar-benar terpasang. Anda dapat melakukan proses pengecekan ini menggunakan browser.
Tuliskan alamat _Internet Protocol (IP)_ pada browser seperti di bawah ini:
*ex : http://ip_anda*
<img src="pict/1.PNG">

## B. Menginstall Mariadb

### 1. Untuk memulai instalasi MariaDB, gunakan perintah berikut

    sudo apt install mariadb-server

   Perintah ini juga akan menampilkan daftar paket yang akan diinstall bersama dengan jumlah ruang disk yang akan digunakan. Tekan **Y** untuk melanjutkan
<img src="pict/2.PNG">

