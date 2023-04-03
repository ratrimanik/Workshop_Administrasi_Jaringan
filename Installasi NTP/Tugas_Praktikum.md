<p align = center>
LAPORAN RESMI <br>
WORKSHOP ADMINISTRASI JARINGAN <br>
Installasi NTP <br>

<br><br>
<p align=center>
Dosen Pengampu:<br>
Dr. Ferry Astika Saputra ST, M.Sc	

<p align=center>
Ratri Maria Manik (3121600039) <br>

<p align=center>
PROGRAM STUDI TEKNIK INFORMATIKA<br>
POLITEKNIK ELEKTRONIKA NEGERI SURABAYA<br>
TAHUN 2023
</p>
<br><br>

## Setup NTP Client<br>
### 1. Change system clock settings<br>
Atur zona waktu sistem ke zona waktu Anda. Untuk melihat daftar zona waktu, gunakan perintah :<br>
- sudo timedatectl set-timezone Asia/Jakarta
- sudo timedatectl set-local-rtc false<br>
![](ss/tahap(1).png)<br><br>

### 2. Configure NTP Client<br>
Aktifkan klien NTP untuk sinkronisasi waktu, menggunakan perintah :<br>
- sudo timedatectl set-ntp true
- sudo nano /etc/systemd/timesyncd.conf<br>
![](ss/tahap(2).png)<br><br>
Restart layanan sinkronisasi waktu, dengan menggunakan perintah<br>
- sudo systemctl restart systemd-timesyncd<br>
Dan lakukan konfirmasi terhadap layanan sinkronisasi waktu telah aktif, dengan menggunakan perintah<br>
- systemctl status systemd-timesyncd<br>
![](ss/tahap(2b).png)<br><br>

### 3. Check Time and Date<br>
Lakukan pengecekan terhadap pengaturan waktu dan tanggal, dengan menggunakan perintah<br>
- timedatectl<br>
![](ss/tahap(1a).png)<br><br>

## Build and Local NTP Server<br>
### 1. Change system clock settings<br>
Untuk melihat daftar zona waktu gunakan kembali perintah : <br>
- sudo timedatectl set-timezone Asia/Jakarta
- sudo timedatectl set-local-rtc false<br>

### 2. Check time and date
Gunakan kembali perintah : <br>
- timedatectl<br>
![](ss/tahap(5).png)<br><br>

### 3. Install NTP Server
Untuk menginstall NTP Server gunakan perintah berikut : <br>
- sudo apt update && sudo apt -y upgrade
- sudo apt -y install ntp<br>
![](ss/tahap(6).png)<br><br>
![](ss/tahap(7).png)<br><br>

### 4. Configure NTP Server
Lakukan konfigurasi terhadap NTP server, dengan menggunakan perintah <br>
- sudo nano /etc/ntp.conf<br>
Dikarenakan terdapat kesalahan, maka dilakukan konfigurasi NTP server menggunakan akun root<br>
![](ss/tahap(9).png)<br><br>

### 5. Restart NTP Service
Lakukan restart NTP service dengan menggunakan perintah berikut : <br>
- sudo systemctl restart ntp
- systemctl status ntp<br>
![](ss/tahap(10).png)<br><br>
- ntpq -p<br>
![](ss/tahap(11).png)<br><br>
