<p align = center>
LAPORAN RESMI <br>
WORKSHOP ADMINISTRASI JARINGAN <br>
Web Server <br>

<br><br>
<p align=center>
Dosen Pengampu:<br>
Dr. Ferry Astika Saputra ST, M.Sc	

<p align=center>
Disusun Oleh:<br>
Latifian Iman (3121600033) <br>
Ratri Maria Manik (3121600039) <br>
Dzikri Mutawakkil (3121600041) <br>

<p align=center>
PROGRAM STUDI TEKNIK INFORMATIKA<br>
POLITEKNIK ELEKTRONIKA NEGERI SURABAYA<br>
TAHUN 2023
</p>
<br><br>

## Installasi Apache2
Web Server yang akan digunakan adalah apache. Sehingga untuk melakukan instalasi menjalankan perintah<br>
**sudo apt install apache2**<br>
![](ss/apache2.png)<br><br>

Setelah Web Server berhasil diinstall, diperlukan perintah untuk memodifikasi pengaturan firewall untuk mengizinkan akses dari luar ke port web default. Ini dilakukan menggunakan UFW, apabila belum memiliki UFW kita bisa melakukan instalasi terlebih dahulu menggunakan perintah<br>
**sudo apt install ufw**<br>
![](ss/ufw.png)<br><br>

Selanjutnya, kita melihat list dari ufw application menggunakan perintah<br>
**sudo ufw app list**<br>
![](ss/ufw_list.png)<br><br>

Selanjutnya melakukan perintah untuk mengijinkan 'WWW' menggunakan perintah<br>
**sudo ufw allow 'WWW'**<br>
![](ss/ufw_www.png)<br><br>

Untuk melihat hasilnya enable ufw tersebut dan lihat statusnya, gunakan perintah<br>
**sudo ufw enable**<br>
**sudo ufw status**<br>
![](ss/ufw_enable_status.png)<br><br>

Proses instalasi terakhir adalah melakukan pengecekan terhadap status apache / web server menggunakan perintah<br>
**sudo systemctl status apache2**<br>
![](ss/status_apache2.png)<br><br>

Untuk memastikan berjalan, kita membuka server ip kita ke browser seperti chrome, mozilla atau edge. Berikut tampilan ketika web server sudah berjalan<br>
![](ss/localhost.png)<br><br>

## Installasi PROFTPD
Melakukan instalasi PROFTPD menggunakan perintah<br>
**sudo apt install proftpd -y**<br>
![](ss/install_proftpd.png)<br><br>

Kemudian menjalankan PROFTPD menggunakan perintah start dan status untuk melihatnya<br>
**systemctl start proftpd**<br>
**systemctl status proftpd**<br>
![](ss/status_proftpd.png)<br><br>

## Installasi PHP
Menggunakan perintah<br>
**sudo apt install php**<br>
**php -v**<br>
![](ss/install_php.png)<br><br>

## Installasi MySQL
Sebelum melakukan instalasi mysql, menambahkan repository mysql dengan cara<br>
**cd tmp**<br>
**wget https://dev.mysql.com/get/mysql-apt-config_0.8.22-1_all.deb**<br>
![](ss/install_mysql.png)<br><br>

Setelah itu, mysql sudah siap untuk diinstal menggunakan dpkg yang berfungsi untuk install, remove dan inspect software packages.<br>
**sudo dpkg -i mysql-apt-config**<br>
![](ss/mysql.png)<br><br>

Setelah itu, package siap diinstal menggunakan perintah<br>
**sudo apt install mysql-server**<br>
![](ss/install_mysql_server.png)<br><br>

Dan melakukan pengecekan menggunakan perintah systemctl status<br>
**sudo systemctl status mysql**<br>
![](ss/status_mysql.png)<br><br>

Terakhir, menjalankan perintah<br>
**mysqladmin -u root -p version**<br>
![](ss/mysql(2).png)<br><br>

## Installasi Laravel
Install curl untuk mengirim atau menerima data melalui protokol seperti HTTP, HTTPS, FTP<br>
**sudo apt install curl**<br>
Gunakan curl command berikut untuk mendownload file Composer<br>
**url -sS https://getcomposer.org/installer | php**<br>
Kemudian pindah composer.phar ke /usr/local/bin/composer<br>
**sudo mv composr.phar /usr/local/bin/composer**<br>
![](ss/install_laravel.png)<br><br>