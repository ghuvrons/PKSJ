# Laporan 4

## Pendahuluan
Dalam merancang sebuah sistem atau jaringan yang aman, pemilik melakukan berbagai usaha untuk menjamin sistem atau jaringan tersebut benar benar aman. Salah satu cara untuk menjamin keamanan tersebut adalah dengan menyerang sistem atau jaringan itu sendiri, dengan mengetahui cara menyerang sistem atau jaringan tersebut diharapkan pengembang sistem dapat melakukan pencegahan agar sistem tidak bisa diserang dengan cara yang sama.

Kali ini, penulis akan mengulas tentang bagaimana sebuah sistem dapat diserang dengan brute force attack, dimana kemudian akan dilakukan usaha penganalisaan penyerangan tersebut dengan membuat suatu sistem palsu yang disebut honeypot.

Sistem yang menjadi bahan percobaan kali ini adalah Ubuntu Server yang telah terinstall Kippo Honeypot. Penulis menggunakan Kali Linux untuk menyerang Ubuntu Server tersebut.

Pada tulisan kali ini, akan dijelaskan secara bertahap dimulai dari penjelasan tahap persiapan, dimulai dari instalasi Ubuntu Server, instalasi OS Kali Linux untuk penetrasi, instalasi Kippo Honeypot beserta konfigurasi, hingga uji penetrasi dengan SSH brute force tools. Pada akhir tulisan ini akan terdapat kesimpulan dan saran.
## Dasar Teori

### Ubuntu Server

Ubuntu Server adalah salah satu varian dari distro linux Ubuntu yang didesain untuk diinstall di server. Ubuntu Server tidak menyediakan GUI, yang ada hanya CLI (Comand Line Interface). Ubuntu Server digunakan untuk menangani memori sampai puluhan Giga ataupun menangani Multicore CPU.

### Kali Linux

Kali Linux adalah penerus distro BackTrack. Sama seperti BackTrack, distro ini dilengkapi dengan berbagai tools Linux untuk melakukan penetration testing. Dengan Kali Linux, pengguna yang melakukan pengujian keamanan tidak perlu repot men-install atau membuat kode program/script baru. Efek sampingnya: distro Linux seperti ini juga kerap disalahgunakan oleh script kiddie. Istilah script kiddie adalah sebutan untuk orang yang menjalankan tool dan mengikuti panduan tanpa memahami apa yang dilakukan oleh dirinya. Hal ini berbeda dari hacker yang memahami setiap aksi yang dilakukannya dan mampu membuat tool/script-nya sendiri.

### Brute Force Attack

Brute Force Attack adalah metode untuk meretas password (password cracking) dengan cara mencoba semua kemungkinan kombinasi yang ada pada “wordlist“. Metode ini dijamin akan berhasil menemukan password yang ingin diretas. Namun, proses untuk meretas password dengan menggunakan metode ini akan memakan banyak waktu.

### Kippo Honeypot

Honeypot adalah suatu sistem palsu yang sengaja dibuat untuk menjebak attacker menyerang sistem yang aslinya. Apabila attacker berhasil masuk ke honeypot, sistem yang aslinya tetap aman tak terpengaruh sedikit pun.

### Persiapan Uji Penetrasi

Instalasi Ubuntu Server

### Instalasi Kippo Honeypot pada Ubuntu Server

Pertama lakukan update pada Ubuntu Server
```
apt-get update
```
Kemudian ganti port (defaultnya port 22) dengan port 2222 pada file sshd_config, caranya ketikkan perintah ini:
```
nano /etc/ssh/sshd_config
```
lalu edit port yang tertera di sana dengan port 2222. Jika sudah lakukan perintah restart
```
/etc/init.d/ssh restart
```
Selanjutnya, download semua kebutuhan untuk Kippo dengan mengetikkan perintah:
```
apt-get install python-dev openssl python-openssl python-pyasn1 python-twisted
```
Sebelum melangkah lebih lanjut, install git pada Ubuntu Server terlebih dahulu
```
apt-get install git
```
Ketikkan perintah ini untuk menjalankan honeypot pada port 22
```
apt-get install authbind
```
Sebelum memulai Kippo, tambahkan user Kippo pada Ubuntu server dengan mengetikkan perintah di bawah ini
```
adduser ggg
```
Tambahkan user ggg pada list user yang dapat mengakses perintah sudo dengan mengetikkan perintah ini
```
sudo visudo
```
masuk ke file /etc/sudoers.tmp dengan mengetikkan perintah ini
```
nano /etc/sudoers.tmp
```
setelah masuk ke file /etc/sudoers.tmp ketikkan `kippo ALL=(ALL:ALL) ALL` dibawah `root    ALL=(ALL:ALL) ALL`
Untuk menyelesaikan settingan Kippo lakukan perintah di bawah ini
```
touch /etc/authbind/byport/22
```
```
chown kippo:kippo /etc/authbind/byport/22
```
```
chmod 777 /etc/authbind/byport/22
```
Selanjutnya lakukan perintah ini untuk mendowload Kippo versi terbaru
```
git clone https://github.com/desaster/kippo.git
```
Copy dan edit file konfigurasi Kippo dari port 2222 menjadi port 22
```
cp kippo.cfg.dist.kippo.cfg
```
```
nano kippo.cfg
```
Kemudian edit file start.sh dengan mengetikkan:
```
nano start.sh
```
ubah line ini
`twistd -y kippo.tac -l log/kippo.log --pidfile kippo.pid`
menjadi
`authbind --deep twistd -y kippo.tac -l log/kippo.log --pidfile kippo.pid`

nyalakan honeypot
```
./start.sh
```
untuk mengecek status kippo telah listening ketikken perintah berikut
```
sudo netstat -antp_
```
## Analisis Malware

## Kesimpulan dan Saran
Kesimpulan:

Dari percobaan yang telah dilakukan, dapat disimpulkan bahwa:

1. Kippo SSH honeypot dapat digunakan untuk mengelabui Attacker dengan memanipulasi port dari SSH dan port dari kippo honeypotnya, yang membuat kippo diakses melalui port default SSH yaitu 22 2. Ditujukan untuk seakan akan sistem dapat dibobol agar dapat melihat aktivitas Attacker saat masuk dalam sistem 3.

Saran:

Dalam hal mengelabui Attacker yang pake brute force attack, dan kita pake Kippo SSH Honeypot, pada database password yang bisa diserang brute force attack,
