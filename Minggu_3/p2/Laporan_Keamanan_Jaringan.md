<p align=center>
LAPORAN RESMI <br>
WORKSHOP ADMINISTRASI JARINGAN </br>
PRAKTIKUM 2 : KEAMANAN JARINGAN

<p align=center>
Dosen Pengampu:<br>
Dr. Ferry Astika Saputra ST, M.Sc	

<p align=center>
Disusun Oleh:<br>
Ratri Maria Manik
<br> 3121600039
<br> 2 D4 IT B

<p align=center>
PROGRAM STUDI TEKNIK INFORMATIKA<br>
POLITEKNIK ELEKTRONIKA NEGERI SURABAYA<br>
TAHUN 2023
</p>
<br><br><br>

## Memastikan IP Address
Dengan menggunakan perintah “dhclient -v” pengguna dapat mengetahui informasi alamat IP dari server DHCP secara verbose, yakni dengan menampilkan informasi lebih detail mengenai proses yang sedang berjalan <br>
**Langkah - Langkah menggunakan perintah dhclient -v:**<br>
1. Pada ubuntu pergi ke terminal<br>
2. Ketikkan **sudo dhclient -v**<br>
3. Enter
![g1](p2/sudo_dhclient.jpg)
<br>
Dalam menjalankan perintah dhclient -v gunakan sudo dikarenakan perintah tersebut memerlukan hak sebagai superuser. Seperti pada gambar diatas, perintah dhclient -v telah berjalan.<br>
Terdapat beberapa informasi rinci, seperti:<br>
1. Mendapatkan informasi tentang IP Address<br>
2. Menerima respon dari server DHCP<br>
3. Memindai jaringan untuk pencarian server dhcp<br>

## Install WINBOX.EXE
**Langkah - Langkah :** <br>
1. Melakukan instalasi aplikasi wine, sehingga pengguna dapat menjalankan program Windows pada Linux menggunakan perintah sudo apt-get install wine
![g2](p2/sudo_apt-get_install_wine.jpg)
<br>
2. Selanjutnya pergi ke https://mikrotik.com/download untuk mendownload winbox.exe, sedangkan winbox sendiri adalah sebuah aplikasi yang digunakan untuk memanajemen router mikrotik<br>
3. Setelah melakukan download buka file winbox64.exe dan click kanan "open in terminal" <br>

![g3](p2/repo.jpg)
<br>
5. Lakukan akses Router RB3011 dengan menggunakan **wine winbox64.exe**<br>
6. Setelah winbox muncul pada dekstop<br>
![g4](p2/winboxexe.jpeg)

## Akses Router RB 3011 menggunakan winbox.exe via wine
Setelah melakukan step sebelumnya, selanjutnya lakukan pengaksesan dengan cara:
Muncul pada tabel lalu click setelah itu connect<br>
7. Setelah itu akan muncul menu yang dinamakan RouterOS<br>
![g4](p2/PergiKeIP.jpeg)<br>
9. Lakukan penambahan static route dengan menggunakan menu **IP** yang terdapat pada mikrotik kemudian, masuk pada bagian **Routes** yang akan menampilkan list route yang telah terhubung ke PC yang kita gunakan, selanjutnya dapat melakukan penambahan routes terhadap PC lainnya.<br>

![g4](p2/masukanip.jpeg)

## Tambahkan Routing Table Pada Router
9. Inputkan “Destination Address” yang terdapat pada ethernet 2 dari tiap PC “192.168.x.x” kemudian pada bagian “Gateway” diisi dengan network yang terdapat pada ethernet 1 dari tiap PC “10.252.x.x” yang ingin dituju.<br>

![g4](p2/TambahIP.jpeg)

10. Setelah dilakukan setting routing terhadap PC, maka dapat dilakukan Ping dengan menggunakan destination address “Ping 192.168.x.x” untuk nge ping PC yang ingin dituju.<br>
![g4](p2/ping.jpg)

## INSTALL VIRTUAL BOX
1. Update System sudo apt update && sudo apt -y upgrade dan lakukan reboot menggunakan [ -f /var/run/reboot-required ] && sudo reboot -f
2. Lakukan import virtual box apt repository
<br>![VirtualBox](p2/vb1dan2.jpeg)<br>
3. Tambahkan virtual box repository
4. Install Virtualbox dan paket existensi
<br>![VirtualBox](p2/vb4.jpeg)<br>
<br>![VirtualBox](p2/vb5.jpeg)<br>
<br>![VirtualBox](p2/vb6.jpeg)<br>
<br>![VirtualBox](p2/vb7.jpeg)<br>
<br>![VirtualBox](p2/vb8.jpeg)<br>
5. Jalankan virtual box<br>
6. Tentukan lokasi folder penyimpanan
<br>![VirtualBox](p2/vb9.jpeg)<br>
7. Masukkan username serta password dengan password admin
<br>![VirtualBox](p2/vb10.jpeg)<br>
8. Tentukan memori penyimpanan
<br>![VirtualBox](p2/vb11.jpeg)<br>
9. Lalu summary instalasi telah selesai dilakukan
<br>![VirtualBox](p2/vb14.jpeg)<br>
