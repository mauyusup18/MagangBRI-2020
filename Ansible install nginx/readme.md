
# Instalasi nginx menggunakan ansible
## 1. Install ansible
### A. Melakukan installasi ansible
Berikut command untuk instalasi ansible

    $ sudo apt-get update
    $ sudo apt-get install software-properties-common
    $ sudo apt-add-repository ppa:ansible/ansible
    $ sudo apt-get update
    $ sudo apt-get install ansible

## 2. Menambahkan host 
 Setelah melakukan instalasi ansible, langkah selanjutnya yaitu mendaftarkan host pada ansible, host yang didaftarkan yaitu host server 

    sudo nano/etc/ansible/hosts

<img src="pict/11.PNG">

selanjutnya melakukan pengujian dengan melakukan ping ke host yang tadi di daftarkan


    ansible all -m ping --ask-pass



Jika berhasil, tampilan nya akan seperti ini


<img src="pict/4.PNG">


## 3. Menambahkan playbook
selanjutnya adalah menambahkan playbook 

    ---
    - name: Install nginx
      hosts: all
    
      become: true
    
      tasks:
      - shell: apt-get upgrade -y; apt-get update
    
      - name: Install nginx
        apt:
          name: nginx
          state: latest
    
      - name: Start NGiNX
        service:
          name: nginx
          state: started
    
      - name: Add PHP7 ppa repository
        apt_repository: repo='ppa:ondrej/php'
    
      - name: Install packages
        apt: pkg={{ item }} state=latest update_cache=yes
        with_items:
        - php7.0-cli
        - php7.0-fpm
        - php7.0-dev
        - php7.0-curl
        - php7.0-gd
        - php7.0-mbstring
        - php7.0-mcrypt
        - php7.0-mysql
        - php7.0-soap
        - php7.0-sqlite3
        - php7.0-xml
        - php7.0-zip
        - php7.0-bcmath
        - php7.0-ssh2
        - php-rrd
        - zlibc
    
      - name: Install MySQL DB server
        apt:
         name: mysql-server
         state: latest
    ...

Setelah menambahkan playbook, selanjutnya menjalankan playbook yang sudah dibuat tadi 

    ansible-playbook nginx-role.yml

<img src="pict/6.PNG">

selanjutnya melakukan pengecekan apakah aplikasi nya sudah terinstall atau belum
 
<img src="pict/7.PNG">
