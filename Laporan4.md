# Laporan 4

## Pendahuluan

## Latar Belakang



## Rumusan Masalah

* Bagaimana cara ...?
* Bagaimana cara ...?

## Tujuan Penulisan

* Untuk mengetahui cara ....
* Untuk menguji penetrasi jaringan .....

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

## Analisis Malware

## Kesimpulan dan Saran
