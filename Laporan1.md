# Laporan 1

## Pendahuluan

### Latar Belakang

Banyak sekali di era yang serba teknologi ini kejahatan semakin ramai. Jaman sekarang segala sesuatu bisa diakses dari tempat manapun negara manapun. Bahkan kita bisa me-*remote* komputer dari negara lain menggunakan *openSSH*. Kemudahan ini dimanfaatkan oleh para *Penetration Developer* untuk me-*remote* komputer orang lain lewar port yang terbuka menggunakan port SSH. Teknik ini terkenal dengan nama SSH brute force attack. Software yang peling terkenal untuk melakukan SSH brute force attack antara lain Hydra, Ncrack, dan medusa.

### Rumusan Masalah

* Bagaimana cara menggunakan software openSSH?
* Bagaimana cara hacker mencoba untuk memenetrasi jaringan yang terbuka port SSH-nya?
* Bagaimana cara mengatasai SSH brute fore attack?

### Tujuan Penulisan

* Untuk mengetahui cara menggunakan software openSSH.
* Untuk menguji penetrasi jaringan yang terbuka port SSH-nya.
* Untuk mengetahui cara mengatasai SSH brute fore attack.

## Dasar Teori

### OS Ubuntu Server

Ubuntu Server adalah system operasi turunan dari Linux Ubuntu yang di desain khusus dengan kernel yang telah dikustomisasi untuk bekerja sebagai system operasi server. Kernel Linux Ubuntu Server di desain khusus untuk bisa bekerja dengan lebih dari satu proses (multiprocessor) dengan dukungan NUMA pada 100Hz internal timer frequency dan menggunakan pennjadwalan deadline I/O.


### Software openSSH

SSH sebagai tool untuk melakukan konektivitas pada jaringan. Jika anda menggunakan telnet, rlogin, dan ftp mungkin tanpa anda sadari bahwa password yang terkirim tanpa melalui enkripsi. Sedangkan dengan menggunakan OpenSSH melakukan enkripsi kepada semua trafik (termasuk password) secara efektif untuk menghindari hal-hal yang tidak diinginkan. Secara tambahan, OpenSSH memiliki tunneling yang aman dan beberapa metode autentikasi, dan juga mendukung semua versi protokol SSH.

### Software Ncrack

Ncrack adalah alat otentikasi jaringan kecepatan tinggi. Dibuat untuk membantu perusahaan mengamankan jaringan mereka secara proaktif dengan menguji semua host dan perangkat untuk password yang kurang bagus. Keamanan juga bergantung pada Ncrack ketika mengaudit klien mereka. Ncrack dirancang menggunakan pendekatan modular, sintaks baris perintah mirip dengan Nmap dan mesin dinamis yang dapat beradaptasi berdasarkan feedback jaringan. Hal ini memungkinkan kecepatan tinggi, juga audit skala besar dari beberapa host.

## Uji Penetrasi 1

### Instalasi Ubuntu Server di vmware

* Pertama download Ubuntu Server di http://www.ubuntu.com/download/server
* Buka vmware kemudian ctrl+N untuk membuat virtual mechine baru. pilih image ubuntu server yang baru di download.
* ikuti perintah-perintah yang ada di vmware sampai instalisasi selesai

### Instalasi kali linux di vmware

* Pertama download image iso kali linux di http://cdimage.kali.org/kali-2016.2/
* Buka vmware kemudian ctrl+N untuk membuat virtual mechine baru. pilih image ubuntu server yang baru di download.
* ikuti perintah-perintah yang ada di vmware sampai instalisasi selesai

### Instalasi software openSSH

* Untuk mengintall openSSH di OS Ubuntu server ketik 

```
~$ sudo apt-get update && apt-get install openssh-server
```

* Masukkan password server. kemudian klik enter.
* Tunggu sampai proses download dan instalisasi selesai
* Kemudian jalankan *openssh-server*

```
~$ sudo systemctl start sshd.service
```


### Uji penetrasi menggunakan Ncrack

* Di OS kali linux sudah tersedia tool ncrack untuk memenetrasi ssh server
* syntax ncrack adalah

```
~$ ncrack [Option] (target and service specification)
```

* Untuk melakukan uji penetrasi pada server uji coba, kita perlu mengetahui IPnya. di sini sudah diketahui IP server target adalah 192.168.145.132.

```
~$ ncrack -p 22 -user ggg -P password-lib-list.txt 192.168.145.132

Starting Ncrack 0.4ALPHA ( http://ncrack.org ) at 2016-07-01 23:21 WIB

Discovered credentials for ssh on 192.168.145.132 22/tcp:
192.168.145.132 22/tcp ss: 'ggg' 'ggg'

Ncrack done:1 service scanner in 24.14 seconds.

Ncrack finished.
```

* dari penetrasi di atas diketahui bahwa server dengan nama 'ggg' memiliki password 'ggg'



## Uji Penetrasi 2

### Konfigurasi sofware Fail2ban

* Pertama intall fail2ban di os ubuntu server

```
~$ sudo apt-get install fail2ban
```

* Tunggu sampai proses download dan instalisasi selesai
* Kemudian jalankan *fail2ban*

```
~$ sudo systemctl start fail2ban.service
```

### Konfigurasi openSSH

* Untuk konfigurasi openSSH, bisa mengedit file konfigurasi di /etc/ssh/sshd_config

```
~$ sudo nano /etc/ssh/sshd_config
```

* Di file ini bisa untuk merubah port ssh yang biasanya 22 menjadi berapapun.
* tidak hanya port juga masih banyak configurasi yang lainnya.

### Uji penetrasi menggunakan Ncrack

* Untuk melakukan uji penetrasi pada server uji coba, kita perlu mengetahui IPnya. di sini sudah diketahui IP server target adalah 192.168.145.132.

```
~$ ncrack -p 22 -user ggg -P password-lib-list.txt 192.168.145.132

Starting Ncrack 0.4ALPHA ( http://ncrack.org ) at 2016-07-01 23:21 WIB

Discovered credentials for ssh on 192.168.145.132 22/tcp:


Ncrack done:1 service scanner in 24.14 seconds.

Ncrack finished.
```

* dari penetrasi di atas tidak terlihat password seperti penetrasi yang sebelumnya.

## Kesimpulan dan Saran

Dari uji penetrasi yang pertama dan kedua, dapat ditarik kesimpulan bahwa kita perlu menambah software untuk SSH brute force countermeasure salah satunya adalah fail2ban. Selain itu kita juga mengkonfigurasi SSH agar tidak default. Supaya susah untuk diserang.
