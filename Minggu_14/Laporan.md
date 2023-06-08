<p align = center>
LAPORAN RESMI <br>
WORKSHOP ADMINISTRASI JARINGAN <br>
Mail Server <br>

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

## Requirement
1. Mail server adalah sebuah sistem yang membantu dalam pendistribusian email, baik dalam proses menerima atau mengirim. Secara sederhana, mail server adalah perantara dalam proses pengiriman dan penerimaan surat. Email yang dikirim akan disimpan pada mail server, kemudian selanjutnya diforward oleh mail server ke penerima.<br>

2. Postfix adalah mail transfer agent free dan open source. Postfix merupakan mail transfer agent default untuk sejumlah sistem operasi bertipe Unix. Postfix didistribusikan menggunakan Lisensi Umum IBM 1.0 yang merupakan lisensi perangkat lunak bebas tetapi tidak kompatibel dengan GPL. Salah satu ketangguhan Postfix adalah kemampuannya menahan “buffer overflow”. Ketangguhan lainnya adalah kesanggupan Postfix memproses surat elektronik dalam jumlah banyak.<br>

3. Dovecot adalah server email IMAP dan POP3 open source untuk sistem Linux / UNIX, yang ditulis dengan mengutamakan keamanan. Dovecot adalah pilihan yang sangat baik untuk instalasi kecil dan besar. Cepat, mudah diatur, tidak memerlukan administrasi khusus dan hanya menggunakan sedikit RAM/memori.<br>

4. Roundcube adalah email client IMAP berbasis web. Fitur Roundcube yang paling menonjol adalah penggunaan teknologi Ajax. Salah satu software open source yang berlisensi GNU General Public License (GPL).<br>

## Konfigurasi Postfix dan Dovecot
Sebelum memulai install mail server, ada baiknya siapkan domain khusus yang akan digunakan untuk konfigurasi mail server. Dalam contoh konfigurasi kali ini akan menggunakan nama domain mail.kampus-07.takehome.com yang dibuat menggunakan bind9 secara lokal.<br>
1. Update repository dan install package postfix, dengan menggunakan perintah<br>
**apt update**<br>
**apt install postfix dovecot-imapd dovecot-pop3d**<br>

2. Konfigurasi Postfix<br>
Setelah installasi selesai akan muncul message box, kemudian pilih internet site agar komunikasi email menggunakan protokol SMTP secara langsung.<br>
![](ss/1a.png)<br><br>

Selanjutnya masukkan nama domain yang ingin digunakan<br>
![](ss/1.png)<br><br>

Setelah itu, postfix akan menyelesaikan installasinya. Setelah Installasi selesai, edit file di /etc/postfix/main.cf dan tambahkan home_mailbox = Maildir/ pada baris paling bawah.<br>
**sudo nano /etc/postfix/main.cf**<br>

**inet_interfaces = all**<br>
**inet_protocols = all**<br>
#tambahkan baris berikut pada baris paling bawah home_mailbox = Maildir/<br>

buat mail directory di directory /etc/skel<br>
**maildirmake.dovecot /etc/skel/Maildir**<br>

Setelah itu masukkan perintah berikut<br>
**dpkg-reconfigure postfix**
Pilih beberapa pilihan dan isikan beberapa input yang akan muncul, sesuaikan dengan topology/konfigurasi sistem dan kebutuhan.<br>
![](ss/1a.png)<br><br>
![](ss/1.png)<br><br>
![](ss/2a.png)<br><br>
![](ss/2b.png)<br><br>
![](ss/3a.png)<br><br>
![](ss/3b.png)<br><br>
![](ss/4a.png)<br><br>
![](ss/4b.png)<br><br>
![](ss/5a.png)<br><br>

Restart postfix service, dengan menggunakan perintah<br>
**systemctl restart postfix**

3. Konfigurasi Dovecot<br>
Edit file konfigurasi /etc/dovecot/dovecot.conf.<br>
**sudo nano /etc/dovecot/dovecot.conf**<br>

Uncomment dan edit baris berikut.<br>

**# If you want to specify non-default ports or anything more complex,**
**# edit conf.d/master.conf.**
**listen = ***<br>
![](ss/9.png)<br><br>

Edit file konfigurasi /etc/dovecot/conf.d/10-auth.conf.<br>
**sudo nano /etc/dovecot/conf.d/10-auth.conf**<br>

Uncomment dan ganti dari yes ke no.<br>
**# connection is considered secure and plaintext authentication is allowed.**<br>
**# See also ssl=required setting.**<br>
**disable_plaintext_auth = no**<br>
![](ss/10.png)<br><br>

Edit file konfigurasi /etc/dovecot/conf.d/10-mail.conf.<br>
**sudo nano /etc/dovecot/conf.d/10-mail.conf**<br>

Uncomment pada baris berikut.<br>
**mail_location = maildir:~/Maildir**<br>
![](ss/11.png)<br><br>

Beri comment pada baris berikut.<br>
**# mail_location = mbox:~/mail:INBOX=/var/mail/%u**<br>

Restart dovesot service, dengan menggunakan perintah<br>
**systemctl restart dovecot**

## Konfigurasi RoundCube
1. Install Mariadb dan Roundcube
Install roundcube sebagai webmail yang akan digunakan oleh client, dan package mariadb yang nantinya akan digunakan sebagai database dari roundcube.
**apt install mariadb-server roundcube**
Pilih yes untuk membuat database secara otomatis oleh roundcube.<br>
![](ss/14.png)<br><br>

Masukkan password database roundcube.<br>
![](ss/15.png)<br><br>
![](ss/16.png)<br><br>

Edit file /etc/roundcube/config.inc.php.<br>
**sudo nano /etc/roundcube/config.inc.php**<br>

Isikan default host dengan nama domain mail server.<br>
**// For example %n = mail.domain.tld, %t = domain.tld**<br>
**$config['default_host'] = 'mail.kampus-02.takehome.com';**<br>

Ganti smtp server dengan nama domain mail server.<br>
**// For example %n = mail.domain.tld, %t = domain.tld**<br>
**$config['smtp_server'] = 'mail.kampus-02.takehome.com';**<br>

Ganti smtp port dari 587 ke 25.<br>
**// SMTP port. Use 25 for cleartext, 465 for Implicit TLS, or 587 for STARTTLS (default)**
**$config['smtp_port'] = 25;**

Kosongkan value dari smtp user.<br>
**// will use the current username for login**
**$config['smtp_user'] = '';**

Kosongkan value dari smtp password<br>
**// will use the current user's password for login**
**$config['smtp_pass'] = '';**

Configure ulang roundcube (langkah ini bisa dilewati).<br>
**dpkg-reconfigure roundcube-core**

Kosongkan karena kita tidak menggunakan tls.<br>
![](ss/17.png)<br><br>

Pilih bahasa untuk roundcube.<br>
![](ss/18.png)<br><br>

Pilih no jika tidak ingin reinstall database yang telah dibuat.<br>
![](ss/19.png)<br><br>

Check pada pilihan apache dan uncheck lighttpd.<br>

Pilih yes untuk merestart web server.<br>
![](ss/20.png)<br><br>

Keep local version jika tidak ingin merubah versi roundcube ke yang lebih terbaru.<br>
![](ss/21.png)<br><br>

Edit apache config untuk memasukkan konfigurasi tambahan dari roundcube ke apache config.<br>
**sudo nano /etc/apache2/apache2.conf**<br>
Tambahkan pada baris paling bawah.<br>
**Include /etc/roundcube/apache.conf**<br>
Selanjutnya, masuk ke directory website apache dan tambahkan file baru untuk mail server.<br>
**cd /etc/apache2/sites-available**
**touch mail.conf**
**vi mail.conf**
**<VirtualHost *:80>**
**ServerName mail.kampus-02.takehome.com**
**DocumentRoot /usr/share/roundcube**
</VirtualHost>

Disable apache default config dan enable kan mail config.
**a2dissite 000-default.conf**
**a2ensite mail.conf**<br>

Restart apache service.<br>
**sudo systemctl restart apache2**

## Testing
1. Buat user untuk mail terlebih dahulu
**adduser satu**
**adduser dua**

jangan lupa restart postfix dan dovecot<br>
**systemctl restart postfix dovecot**

2. Testing dengan telnet
**apt install telnet**

Test kirim file menggunakan perintah telnet dengan menggunakan port 25 (SMTP). Masukkan nama alamat pengirim menggunakan mail from:. Masukkan nama alamat penerima menggunakan rcpt to:. Ketikkan data lalu enter. Isikan subject dengan megetikkan Subject: . Lalu isikan pesan yang akan dikirim kemudian isikan titik (.) untuk mengakhiri pesan.<br>
**telnet mail.kampus-02.takehome.com 25**<br>

Melihat pesan menggunakan perintah telnet . Login user menggunakan user . Dan masukkan password menggunakan pass . Untuk melihat list pesan yang diterima menggunakan perintah list. Dan untuk membuka pesan yang diterima menggunakan perintah retr .
Perintah quit untuk keluar dari telnet.<br>
**telnet mail.kampus-02.takehome.com 110**

3. Selanjutnya buka web browser pada sisi client dan masukkan domain dari mail server (mail.kampus-02.takehome.com), maka akan muncul interface dari roundcube. Lalu login menggunakan salah satu user yang telah dibuat.<br>

Klik pada compose dan isikan pesan untuk user lainnya. Lalu klik send.<br>
![](ss/23.png)<br><br>