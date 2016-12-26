# Laporan 2

## Pendahuluan

### Latar Belakang
Di era moderen ini penyimpanan informasi dalam medium digital sudah merupakan hal yang bersifat esensial. Adanya internet memungkinkan terjadinya pertukaran informasi dari berbagai komputer yeng terhubung pada jaringan. Hal itu memungkinkan terjadinya penyerangan dari suatu komputer ke komputer lain yang terhubung pada jaringan yang sama. Penyerangan adalah tindakan untuk memusnahkan, mengubah, menyebarkan, melumpuhkan, dan mencuri aset data di luar wewenang.
SQL Injection adalah teknik penetrasi kode yang digunakan untuk melakukan penyerangan aplikasi berbasis data. Peneyerangan dilakukan dengan cara memasukkan SQL statement ke dalam data yang dieksekusi. SQL Injection mengeksploitasi celah keamanan di aplikasi, contohnya saat input user yang tidak difilter dengan baik sehingga bisa dimanipulasi untuk memasukkan SQL statement yang akan dieksekusi di luar perkiraan.


### Rumusan Masalah

* Bagaimana cara melakukukan SQL Injection pada Plugin WordPress yang memiliki celah keamanan
* Bagaimana cara ...?

### Tujuan Penulisan

* Mengetahui cara melakukan SQL Injection
* Mengetahui cara perlindungan dan pencegahan SQL Injection
## Langkah Instalasi

### Instalasi Wordpress

Sebelum komputer bisa digunakan wordpress komputer harus memiliki LAMP terlebih dahulu. LAMP adalah Linux, Apache, MySQL, dan PHP. Setelah LAMP terinstal, tahap berikutnya adalah instalasi Wordpress.
1. Membuat database dan user baru
login ke MySQL root account dengan menggunakan command:

```
mysql -u root -p
```

Setelah itu masukkan password untuk akses ke MySQL yang akan menampilkan command prompt untuk MySQL pada terminal. Setelah itu, buat database baru dengan cara:

```
CREATE DATABASE wordpress;
```

Setelah itu, buatlah user baru dengan cara memasukkan:

```
CREATE USER demo@localhost IDENTIFIED BY 'demopass';
```

User yang telah dibuat belum memiliki izin untuk mengakses database yang sebelumnya dibuat. Untuk itu berikan user izin dengan cara:

```
GRANT ALL PREVILEGES ON wordpress.* TO demo@localhost;
```

Lalu masukkan:

```
FLUSH PREVILEGES;
```

Konfigurasi MySQL telah selesai. Untuk mengakhiri masukkkan:

```
exit
```

2. Download Wordpress
Tahap pertama adalah download versi terbaru dari WordPress dengan cara:

```
cd ~
wget http://wordpress.org/latest.tar.gz
```

Lalu extract file dengan cara:

```
tar xzvf latest.tar.gz
```

Lalu, lakukan update package dengan cara:

```
sudo apt-get update
sudo apt-get install php5-gd libssh-php
```

3. Konfigurasi Wordpress

Masuk ke direktori wordpress

```
cd ~/wordpress
```

Lakukan copy configuration file

```
cp wp-config-sample.php wp-config.php
```

Buka config file

```
nano wp-config.php
```

Set informasi database dengan cara mengedit config file menjadi:

```
/** The name of the database for WordPress */
define('DB_NAME', 'wordpress');

/** MySQL database username */
define('DB_USER', 'demo');

/** MySQL database password */
define('DB_PASSWORD', 'demopass');
```

Lalu save dan exit file.

4. Copy file ke dokumen root

Setelah kita selesai membuat file konfigurasi, copy file-file tersebut ke dokumen root Apache

```
sudo rsync -avP ~/wordpress/ /var/www/html/
```

Lalu masuk ke direktori html pada dokumen Apache

```
cd /var/www/html/
```

Lalu berikan akses ownership dengan cara

```
sudo chown -R demo:www-data *
```

Buat direktori uploads sebagai parent direktori

```
mkdir /var/www/html/wp-content/uploads
```

Berikan ownership dengan cara

```
sudo chown -R :www-data /var/www/html/wp-content/uploads
```

5. Selesaikan instalasi melalui web interface

Wordpress sudah bisa diakses melalui web browser di alamat

```
http://localhost
```

Masukkan Site Title, Username, Password, E-mail, dan Privacy pada web interface dan klik Install Wordpress. Lalu login kembali menggunakan akun yang baru dibuat.
WordPress siap untuk digunakan

## Dasar Teori
OS yang digunakan

WordPress adalah alat blogging gratis dan open source dan sistem manajemen konten (CMS) berbasis PHP dan MySQL, yang berjalan pada layanan web hosting. Fitur termasuk plug-in arsitektur dan sistem template. WordPress digunakan oleh lebih dari 18,9 % dari 10 juta website pada Agustus 2013 WordPress adalah sistem blogging yang paling populer digunakan di Web, pada lebih dari 60 juta situs.

SQLMap adalah tool open source yang di jalankan menggunakan command dan support untuk data base MySQL, Oracle, PostgreSQL, Microsoft SQL Server, Microsoft Access, IBM DB2, SQLite, Firebird, Sybase and SAP MaxDB.
SQLMAP adalah penetrasi open source pengujian alat yang mengotomatisasi proses mendeteksi dan mengeksploitasi kelemahan SQL injection dan mengambil alih server database.



### 


## Uji Penetrasi

###

## Kesimpulan dan Saran

