<p align = center>
LAPORAN RESMI <br>
WORKSHOP ADMINISTRASI JARINGAN <br>
Domain Name Service (DNS) <br>

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

## Domain Name Service (DNS) <br>
Domain Name Service (DNS) adalah layanan Internet yang memetakan alamat IP dan nama domain yang memenuhi syarat (FQDN) satu sama lain. Dengan cara ini, DNS mengurangi kebutuhan untuk mengingat alamat IP. Komputer yang menjalankan DNS disebut name servers. Ubuntu dilengkapi dengan BIND (Berkley Internet Naming Daemon), program yang paling umum digunakan untuk mengelola name servers di Linux.<br><br>

## Overview <br>
File konfigurasi DNS disimpan di direktori /etc/bind. File konfigurasi utama adalah /etc/ bind/named.conf, yang dalam tata letak yang disediakan oleh paket menyertakan berkas-berkas berikut:<br>

- /etc/bind/named.conf.options: opsi DNS global
- /etc/bind/named.conf.local: untuk zona User
- /etc/bind/named.conf.default-zones: zona default seperti localhost.<br><br>

## Caching Name Server<br>
Konfigurasi default bertindak sebagai caching server. Cukup hapus komentar dan edit bagian forwarders di **/etc/bind/named.conf.** untuk mengatur alamat IP server DNS ISP Anda.<br>
![](konjar/named.conf.options.png)<br><br>
Untuk mengaktifkan konfigurasi baru, mulai ulang server DNS. Dari prompt terminal dengan perintah berikut:<br>

**sudo systemctl restart bind9.service**<br><br>

## Instalasi
Untuk menginstall BIND9, pada terminal jalankan perintah berikut:<br>
**sudo apt install bind9**<br>
![](konjar/Install_Bind9.png)<br><br>
Selanjutnya gunakan perintah<br>
**sudo apt install dnsutils**
![](konjar/Install_DNS_Utils.png)<br><br>

## Forward Zone File (Domain ke IP)<br>
Untuk menambahkan zona DNS ke BIND9 dan mengubah BIND9 menjadi server Primer, gunakan perintah <br>
**/etc/bind/named.conf.local**<br>
![](konjar/named.conf.local.png)<br><br>
Gunakan zone file yang sudah ada sebagai template untuk membuat berkas /etc/bind/db.example.com dengan menggunakan perintah <br>
**sudo cp /etc/bind/db.local /etc/bind/db.example.com**<br>
Forward Zone File (Setelah dilakukan pengeditan)
![](konjar/ubahdb.domain.png)<br><br>

## Reverse Zone File (IP ke Domain)
edit /etc/bind/db.192 dengan mengubah opsi yang sama dengan menjalankan perintah <br>
**/etc/bind/db.example.com**<br>
![](konjar/ubahdb.ip.png)<br><br>
Setelah membuat Reverse Zone File, mulai ulang BIND9:<br>
**sudo systemctl restart bind9.service**<br><br>

## Testing
Langkah pertama dalam menguji BIND9 adalah menambahkan Alamat IP nameserver ke host resolver. Nameserver utama harus dikonfigurasi seperti halnya host lain untuk memeriksa ulang berbagai hal. Buka DNS client untuk mengetahui detail tentang cara menambahkan alamat nameserver ke network client. Edit nameserver dan parameter untuk domain pada file /etc/resolv.conf<br>
![](konjar/testing.png)<br><br>
Terdapat banyak cara untuk melakukan testing, pada kali ini kelompok kami menggunakan metode ping untuk mengetahui apakah konfigurasi sudah berhasil atau belum. Command yang diperlukan:<br>
**ping www.example.com**<br>
![](konjar/Cobaping.png)<br><br>


