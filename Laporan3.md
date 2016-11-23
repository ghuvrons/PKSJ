# Laporan 3

## Pendahuluan

### Latar Belakang



### Rumusan Masalah

* Bagaimana cara ...?
* Bagaimana cara ...?

### Tujuan Penulisan

* Untuk mengetahui cara ....
* Untuk menguji penetrasi jaringan .....

## Dasar Teori

### Cuckoo Sandbox

Cuckoo Sandbox adalah suatu applikasi untuk mempermudah kita melakukan analisa suatu malware. Aplikasi ini mencatat suatu perubahan-perubahan yang dilakukan oleh suatu malware sehingga kita bisa menarik sebuah kesimpulan terhadap malware tersebut.


## Instalasi Cuckoo Sandbox

### Install Virtual Box

```
# apt-get install virtualbox
```

### Install Python, PIP, GIT, dan beberapa library yang 

```
# apt-get install python git
# apt-get install python-sqlalchemy python-bson
# apt-get install python-pip
# pip install sqlalchemy bson
# apt-get install python-dpkt python-jinja2 python-magic python-pymongo python-gridfs python-libvirt python-bottle python-pefile python-chardet python-dev
# pip install jinja2 pymongo bottle pefile cybox==2.0.1.4
# pip install maec==4.0.1.0 django chardet
```

### Install ssdeep

```
# tar xvfz ssdeep-2.12.tar.gz
# cd ssdeep
# ./configure
# make
# make install
```

### Install pydeep

```
# cd /opt
# git clone https://github.com/kbandla/pydeep.git pydeep 
# cd /opt/pydeep/
# python setup.py build
# sudo python setup.py install
```

### Install yara

```
# apt-get install automake libtool
# tar xvfz yara-3.1.0.tar.gz
# cd yara-3.1.0
# ./bootstrap.sh
# ./configure 
# make
# make install
# cd yara-ptyhon
# python setup.py build
# python setup.py install
# apt-get install python-yara
```

### Install tcpdump

```
# apt-get install tcpdump
# setcap cap_net_raw,cap_net_admin=eip /usr/sbin/tcpdump
```

### Install Cuckoo

```
# adduser cuckoo
# addgroup cuckoo vboxusers
# cd ~
# git clone git://github.com/cuckoobox/cuckoo.git
```

## Analisis Malware

## Kesimpulan dan Saran

## Source

http://hacktr.org/2014/11/12/cuckoo-sandbox-installation/
