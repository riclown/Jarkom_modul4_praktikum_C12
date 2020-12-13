# Jarkom_modul4_praktikum_C12

## Kelompok C12
* 05111840000146 - [I Kadek Ricky Suirta](https://github.com/riclown)
* 05111840000162 - [Fransiskus Xaverius Kevin Koesnadi](https://github.com/fxkevink)

## Daftar Isi
* [Menggunakan VLSM](#vlsm)
* [Soal 1](#soal-1)
* [Menggunakan CIDR](#cidr)
* [Soal 2](#soal-2)


## VLSM

![soal](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/soal.jpg)


* **CLOUD** diberikan IP TUNTAP.
* **Server** diberikan IP DMZ.
* Berikan memori sebesar **64MB** pada setiap UML.


## Soal 1

Menentukan subnet pada topologi yang disediakan:

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/vlsmsubnet.jpg)

Menentukan jumlah IP serta submask yang di tiap subnet, setelah itu dapat ditemukan jumlah IP dan submask yang dibutuhkan:

 ________ ___________ _________ 
| Subnet |    Host   | Length  |
|--------|-----------|---------|
| A1     | SERVER    | 30      |
| A2     | 1001      | 22      |
| A3     | 2         | 30      |
| A4     | 2         | 30      |
| A5     | 101       | 25      |
| A6     | 13        | 28      |
| A7     | 502       | 23      |
| A8     | 2         | 30      |
| A9     | 701       | 22      |
| A10    | 2021      | 21      |
| A11    | 521       | 22      |
| A12    | 2         | 30      |
| A13    | SERVER    | 30      |
| A14    | 252       | 24      |
| A15    | 272       | 22      | 
|Total   | 5841      | 19      |
--------------------------------

Setelah mendapatkan jumlah IP dan submask, maka tree VLSM dapat dibuat, dalam hal ini dimulai dari `/19 = 8192`, yang dibagi menjadi 2 yaitu = 4096. Angka 4096 dibagi dengan jumlah IP maksimal yaitu 256, sehingga `4096/256 = 16`. Sehingga diperoleh `192.168.0.0/20` dan `192.168.0.16/20`. Hal ini akan berlangsung sampai seterusnya pada pohon pembagian IP.

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/vlsmtree.png)

Sehingga dari hasil yang ditemukan, akan diperoleh NID untuk setiap subnet. Netmask diambil dari ketentuan modul dan broadcast ID diperoleh dari hitungan `NID + (2^(32-Submask))-1`: (A1 - **MALANG**, A13 - **MOJOKERTO**)

 ________ ___________ _________ ______________ ________________ ______________ 
| Subnet | Jumlah IP | Submask |      NID     |     Netmask    | Broadcast ID |
|--------|-----------|---------|--------------|----------------|--------------|
| A1     | SERVER    | 30      |10.151.77.104 |255.255.255.252 |10.151.77.107 |
| A2     | 1001      | 22      |192.168.8.0   |255.255.252.0   |192.168.11.255|
| A3     | 2         | 30      |192.168.27.192|255.255.255.252 |192.168.27.195|
| A4     | 2         | 30      |192.168.27.196|255.255.255.252 |192.168.27.199|
| A5     | 101       | 25      |192.168.27.0  |255.255.255.128 |192.168.27.127|
| A6     | 13        | 28      |192.168.27.208|255.255.255.240 |192.168.27.236|
| A7     | 502       | 23      |192.168.24.0  |255.255.254.0   |192.168.27.255|
| A8     | 2         | 30      |192.168.27.200|255.255.255.252 |192.168.27.203|
| A9     | 701       | 22      |192.168.12.0  |255.255.252.0   |192.168.15.255|
| A10    | 2021      | 21      |192.168.0.0   |255.255.248.0   |192.168.7.255 |
| A11    | 521       | 22      |192.168.16.0  |255.255.252.0   |192.168.19.255|
| A12    | 2         | 30      |192.168.27.204|255.255.255.252 |192.168.27.207|
| A13    | SERVER    | 30      |10.151.77.108 |255.255.255.252 |10.151.77.111 |
| A14    | 252       | 24      |192.168.26.0  |255.255.255.0   |192.168.26.255|
| A15    | 272       | 22      |192.168.20.0  |255.255.252.0   |192.168.23.255|
-------------------------------------------------------------------------------

Setelah itu dapat dibuat bentuk topologinya pada *Cisco (CPT)*.

* **Konfigurasi Interface Router - Router**

Dalam hal ini akan dilakukan konfigurasi interface untuk **SURABAYA** dan **PASURUAN** (Subnet A3). Hal pertama yang dilakukan yaitu melihat ethernet pada **SURABAYA** dan **PASURUAN**. Melalui gambar topologi, keduanya terhubung oleh **SURABAYA** (Fa 0/1) dan **PASURUAN** (Fa 0/0).

Pada **SURABAYA**, buka router **SURABAYA** dan pilih tab Config. Pada bagian Interface (0/1), masukkan `NID Subnet A3 + 1` dan Netmask berdasarkan NID dan Netmask yang ditemukan:

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/sbyfe01.jpg)

Berikutnya pada **PASURUAN**, pilih tab Config, dan pada bagian Interface (0/0), masukkan `NID Subnet A3 + 2` dan Netmask:

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/pasuruanfe00.jpg)

Sehingga akan diperoleh hasil sebagai berikut:

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/surabayapasuruan.jpg)

Lakukan Ping dengan memilih Simple PDU dari **SURABAYA** ke **PASURUAN**.

* **Konfigurasi Interface Router - Client**

Lakukan konfigurasi interface untuk **PASURUAN** dan **SIDOARJO** (Subnet A9). Hal pertama yang dilakukan yaitu melihat ethernet pada **PASURUAN** dan **SIDOARJO**. Melalui gambar topologi, keduanya terhubung oleh **PASURUAN** (Fa 1/0) dan **SIDOARJO** (Fa 0).

Pada **PASURUAN**, buka router **PASURUAN** dan pilih tab Config. Pada bagian Interface (1/0), masukkan `NID Subnet A9 + 2` dan Netmask berdasarkan NID dan Netmask yang ditemukan:

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/pasuruanfe10.jpg)

Berikutnya pada **SIDOARJO**, pilih tab DESKTOP. Pada IP Configuration, masukkan `NID Subnet A9 + 1` dan Netmask:

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/sidoarjo.jpg)

Sehingga akan diperoleh hasil sebagai berikut:

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/pasuruansidoarjo.jpg)

Lakukan Ping dengan memilih Simple PDU dari **PASURUAN** DAN **SIDOARJO**.

* **Konfigurasi Interface Router - Server**

Hal yang sama pada interface Router - Server seperti halnya Router - Client

Lakukan konfigurasi interface untuk **SURABAYA** dan **MOJOKERTO** (Subnet A1 - Server). Hal pertama yang dilakukan yaitu melihat ethernet pada **SURABAYA** dan **MOJOKERTO**. Melalui gambar topologi, keduanya terhubung oleh **SURABAYA** (Fa 1/1) dan **MOJOKERTO** (Fa 0).

Pada **SURABAYA**, buka router **SURABAYA** dan pilih tab Config. Pada bagian Interface (1/1), masukkan `NID Subnet A1 + 1` dan Netmask berdasarkan NID dan Netmask yang ditemukan:

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/sbyfe11.jpg)

Berikutnya pada **MOJOKERTO**, pilih tab DESKTOP. Pada IP Configuration, masukkan `NID Subnet A1 + 1` dan Netmask:

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/mojokerto.jpg)

Sehingga akan diperoleh hasil sebagai berikut:

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/surabayamojokerto.jpg)

Lakukan Ping dengan memilih Simple PDU dari **SURABAYA** ke **MOJOKERTO**.

* **Subnet Routing**

Routing ini diterapkan pada antar hardware yang tidak saling berhubungan secara langsung.

Contoh routing ini berupa dari **SURABAYA** ke **SIDOARJO**. Buka router **SURABAYA** dan masukkan pda tab Config, lalu buka static, dan lakukan konfigurasi seperti berikut

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/surabayastatic.jpg)

Maksud pada gambar di atas yaitu *Network* dan *Mask* diisi dengan tujuan Subnet A9, Next Hop diisi dengan IP Interface **PASURUAN**, dikarenakan untuk menuju subnet A9, terlebih dahulu melalui router **PASURUAN**. Maka subnet routing telah selesai.

Lakukan Ping dengan memilih Simple PDU dari **SURABAYA** ke **SIDOARJO**.

* **Default Routing**

Routing ini diterapkan pada hardware yang memiliki default dan tidak terhubung ke cloud. contohnya dalam hal ini **PASURUAN**.

Buka **PASURUAN** dan buka tab Config pilih Static dan masukkan Network, Mask, Next Hop sebagai berikut:

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/passtatic.jpg)

Default berarti Network dan Mask dimasukkan nilai `0.0.0.0` dan `0.0.0.0` dan Next Hop dimasukkan IP Interface menuju router **SURABAYA** dengan Etehernet (0/1). Router **SURABAYA** memiliki tampilan sebagai berikut:

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/sbydefault.jpg)

Lakukan Ping dengan memilih Simple PDU dari **PASURUAN** ke **SURABAYA**

*Cisco file* topologi dapat diakses pada link [berikut](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/C12_Topologi%20Modul%204.pkt).

## CIDR

![soal](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/soal.jpg)

* **CLOUD** diberikan IP TUNTAP.
* **Server** diberikan IP DMZ.
* Berikan memori sebesar **64MB** pada setiap UML.

## Soal 2

Hal yang sama pada soal ini, yaitu menentukan subnet pada topologi dan memberikan label pada subnet tersebut sampai subnet terbesar yang mencakup 1 topologi sehingga akan diperoleh NID:

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/cidra.png)

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/cidrb.jpg)

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/cidrc.jpg)

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/cidrd.jpg)

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/cidre.jpg)

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/cidrf.jpg)

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/cidrg.jpg)


Berikutnya membuat pohon topologi CIDR berdasarkan labelling subnet:

![img](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/cidrtree.jpg)

Melalui pohon di atas, dapat diperoleh NID dan Netmasknya serta lakukan pencarian Broadcast ID pada rumus yang tertera sebelumnya:

 ________ ___________ _________ ______________ ________________ _______________
| Subnet | Jumlah IP | Submask |      NID     |     Netmask    | Broadcast ID  |
|--------|-----------|---------|--------------|----------------|---------------|
| A2     | 1001      | 22      |192.168.132.0 |255.255.252.0   |192.168.135.255|
| A3     | 2         | 30      |192.168.0.4   |255.255.255.254 |192.168.0.7    |
| A4     | 2         | 30      |192.168.0.12  |255.255.255.254 |192.168.0.15   |
| A5     | 101       | 25      |192.168.0.128 |255.255.255.128 |192.168.0.255  |
| A6     | 13        | 28      |192.168.140.0 |255.255.255.240 |192.168.140.31 |
| A7     | 502       | 23      |192.168.142.0 |255.255.254.0   |192.168.143.255|
| A8     | 2         | 30      |192.168.128.8 |255.255.255.254 |192.168.128.11 |
| A9     | 701       | 22      |192.168.16.0  |255.255.252.0   |192.168.19.255 |
| A10    | 2021      | 21      |192.168.0.0   |255.255.248.0   |192.168.7.255  |
| A11    | 521       | 22      |192.168.136.0 |255.255.252.0   |192.168.136.3  |
| A12    | 2         | 30      |192.168.128.4 |255.255.255.252 |192.168.128.7  |
| A14    | 252       | 24      |192.168.129.0 |255.255.255.0   |192.168.129.255|
| A15    | 721       | 22      |192.168.128.0 |255.255.252.0   |192.168.131.255|
|MOJOKERTO| SERVER   | 30      |10.151.77.104 |255.255.255.252 |10.151.77.107  |
|MALANG   | SERVER   | 30      |10.151.77.108 |255.255.255.252 |10.151.77.111  |
|CLOUD    | CLOUD    | 30      |10.151.76.52  |255.255.255.252 |10.151.76.55   |
--------------------------------------------------------------------------------

Berikutnya, dapat membuat topologi pada UML sesuai dengan modul UML.

Sintaks untuk **topo.sh**

```# Switch
uml_switch -unix switch1 > /dev/null < /dev/null & 
uml_switch -unix switch2 > /dev/null < /dev/null & 
uml_switch -unix switch3 > /dev/null < /dev/null & 
uml_switch -unix switch7 > /dev/null < /dev/null & 
uml_switch -unix switch11 > /dev/null < /dev/null & 
uml_switch -unix switch13 > /dev/null < /dev/null & 
uml_switch -unix switch15 > /dev/null < /dev/null & 
uml_switch -unix switch16 > /dev/null < /dev/null & 
uml_switch -unix switch17 > /dev/null < /dev/null & 
uml_switch -unix switch18 > /dev/null < /dev/null & 
uml_switch -unix switch19 > /dev/null < /dev/null & 
uml_switch -unix switch21 > /dev/null < /dev/null & 
uml_switch -unix switch20 > /dev/null < /dev/null & 
uml_switch -unix switch22 > /dev/null < /dev/null & 
uml_switch -unix switch25 > /dev/null < /dev/null & 


# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.76.52 eth1=daemon,,,switch1 eth2=daemon,,,switch2 eth3=daemon,,,switch7 eth4=daemon,,,switch13 mem=64M &
xterm -T PASURUAN -e linux ubd0=PASURUAN,jarkom umid=PASURUAN eth0=daemon,,,switch2 eth1=daemon,,,switch3 eth2=daemon,,,switch19 mem=64M &
xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch3 eth1=daemon,,,switch15 eth2=daemon,,,switch16 mem=64M &
xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch7 eth1=daemon,,,switch11 eth2=daemon,,,switch21 eth3=daemon,,,switch22 mem=64M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch22 eth1=daemon,,,switch25 mem=64M &
xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch11 eth1=daemon,,,switch17 eth2=daemon,,,switch18 mem=64M &
xterm -T BLITAR -e linux ubd0=BLITAR,jarkom umid=BLITAR eth0=daemon,,,switch17 eth1=daemon,,,switch20 mem=64M &


# Server
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch18 mem=64M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch13 mem=64M &

# Klien
xterm -T SAMPANG -e linux ubd0=SAMPANG,jarkom umid=SAMPANG eth0=daemon,,,switch1 mem=64M &
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch19 mem=64M &
xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI,jarkom umid=BANYUWANGI eth0=daemon,,,switch16 mem=64M &
xterm -T JEMBER -e linux ubd0=JEMBER,jarkom umid=JEMBER eth0=daemon,,,switch16 mem=64M &
xterm -T BONDOWOSO -e linux ubd0=BONDOWOSO,jarkom umid=BONDOWOSO eth0=daemon,,,switch15 mem=64M &
xterm -T JOMBANG -e linux ubd0=JOMBANG,jarkom umid=JOMBANG eth0=daemon,,,switch22 mem=64M &
xterm -T BOJONEGORO -e linux ubd0=BOJONEGORO,jarkom umid=BOJONEGORO eth0=daemon,,,switch25 mem=64M &
xterm -T NGANJUK -e linux ubd0=NGANJUK,jarkom umid=NGANJUK eth0=daemon,,,switch21 mem=64M &
xterm -T LUMAJANG -e linux ubd0=LUMAJANG,jarkom umid=LUMAJANG eth0=daemon,,,switch17 mem=64M &
xterm -T TULUNGAGUNG -e linux ubd0=TULUNGAGUNG,jarkom umid=TULUNGAGUNG eth0=daemon,,,switch20 mem=64M &
```

Lalu  jalankan `bash topo.sh` pada *putty* dan masukkan *username* dan *password* default. Pada router **SURABAYA** lakukan setting `sysctl` dengan mengetikkan perintah `nano /etc/sysctl.conf`, dan Hilangkan tanda pagar (#) pada bagian `net.ipv4.ip_forward=1`.

Lalu setting IP pada setiap *interfaces* uml dengan mengetikkan `nano /etc/network/interfaces` sebagai berikut:

**SURABAYA**

```
auto lo
iface lo inet loopback

#cloud
iface eth0 inet static
address 10.151.76.54
netmask 255.255.255.252
gateway 10.151.76.53
 
#sampang – A2
auto eth1
iface eth1 inet static
address 192.168.132.1
netmask 255.255.252.0
 
#pasuruan – A3
auto eth2
iface eth2 inet static
address 192.168.0.5
netmask 255.255.255.254
 
#batu – A8
auto eth3
iface eth3 inet static
address 192.168.128.9
netmask 255.255.255.254
 
#mojokerto - server
auto eth4
iface eth4 inet static
address 10.151.77.105
netmask 255.255.255.252

```

**PASURUAN**

```
auto lo
iface lo inet loopback
 
#surabaya – A3
auto eth0
iface eth0 inet static
address 192.168.0.6
netmask 255.255.255.254
 
#probolinggo – a4
auto eth1
iface eth1 inet static
address 192.168.0.13
netmask 255.255.255.254
 
#sidoarjo – A9
auto eth2
iface eth1 inet static
address 192.168.16.1
netmask 255.255.252.0

```

**PROBOLINGGO**

```
auto lo
iface lo inet loopback
 
#pasuruan – A4
auto eth0
iface eth0 inet static
address 192.168.0.14
netmask 255.255.255.254
 
#bondowoso – A5
auto eth1
iface eth1 inet static
address 192.168.0.129
netmask 255.255.255.128
 
#jember&banyuwangi – A10
auto eth2
iface eth2 inet static
address 192.168.0.1
netmask 255.255.248.0
```

**BATU**

```
auto lo
iface lo inet loopback
 
#surabaya – A8
auto eth0
iface eth0 inet static
address 192.168.128.10
netmask 255.255.255.254
  
#jombang – A7
auto eth1
iface eth1 inet static
address 192.168.142.1
netmask 255.255.254.0

#nganjuk – A11
auto eth2
iface eth2 inet static
address 192.168.136.1
netmask 255.255.252.0

#kediri – A12
auto eth3
iface eth3 inet static
address 192.168.128.5
netmask 255.255.255.252
```


**MADIUN**

```
auto lo
iface lo inet loopback
  
#batu – A7
auto eth0
iface eth0 inet static
address 192.168.142.2
netmask 255.255.254.0

#bojonegoro – A6
auto eth1
iface eth1 inet static
address 192.168.140.1
netmask 255.255.255.240
```

**KEDIRI**

```
auto lo
iface lo inet loopback
 
#batu – A12
auto eth0
iface eth0 inet static
address 192.168.128.6
netmask 255.255.255.252
 
#lumajang – A14
auto eth1
iface eth1 inet static
address 192.168.129.1
netmask 255.255.255.0
 
#malang - server
auto eth2
iface eth2 inet static
address 10.151.77.109
netmask 255.255.255.252

```

**BLITAR**

```
auto lo
iface lo inet loopback
 
#kediri – A14
auto eth0
iface eth0 inet static
address 192.168.129.2
netmask 255.255.255.0

#tulungagung – A15
auto eth1
iface eth1 inet static
address 192.168.128.1
netmask 255.255.252.0
```

**SAMPANG**

```
auto lo
iface lo inet loopback
 
#surabaya – A2
auto eth0
iface eth0 inet static
address 192.168.132.2
netmask 255.255.252.0
gateway 192.168.132.1
```


**BONDOWOSO**

```
auto lo
iface lo inet loopback
 
#probolinggo – A5
auto eth0
iface eth0 inet static
address 192.168.0.130
netmask 255.255.255.128
gateway 192.168.0.129
```


**JEMBER**

```
auto lo
iface lo inet loopback
 
#probolinggo – A10
auto eth0
iface eth0 inet static
address 192.168.0.3
netmask 255.255.248.0
gateway 192.168.0.1
```

**BANYUWANGI**

```
auto lo
iface lo inet loopback
 
#probolinggo – A10
auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.248.0
gateway 192.168.0.1
```

**SIDOARJO**

```
iface lo inet loopback
 
#pasuruan – A9
auto eth0
iface eth0 inet static
address 192.168.16.2
netmask 255.255.252.0
gateway 192.168.16.1
```

**JOMBANG**

```
auto lo
iface lo inet loopback
 
#batu – A7
auto eth0
iface eth0 inet static
address 192.168.142.3
netmask 255.255.254.0
gateway 192.168.142.1
```


**BOJONEGORO**

```
auto lo
iface lo inet loopback
 
#madiun – A6
auto eth0
iface eth0 inet static
address 192.168.140.2
netmask 255.255.255.240
gateway 192.168.140.1
```


**NGANJUK**

```
auto lo
iface lo inet loopback
 
#batu – A11
auto eth0
iface eth0 inet static
address 192.168.136.2
netmask 255.255.252.0
gateway 192.168.136.1
```


**LUMAJANG**

```
auto lo
iface lo inet loopback
 
#kediri – A14
auto eth0
iface eth0 inet static
address 192.168.129.3
netmask 255.255.255.0
gateway 192.168.129.1
```


**TULUNGAGUNG**

```
auto lo
iface lo inet loopback
 
#blitar – A15
auto eth0
iface eth0 inet static
address 192.168.128.2
netmask 255.255.252.0
gateway 192.168.128.1
```

**MOJOKERTO**

```
#surabaya – server mojokerto
auto eth0
iface eth0 inet static
address 10.151.77.106
netmask 255.255.255.252
gateway 10.151.77.105
```

**MALANG**

```
#kediri – server malang
auto eth0
iface eth0 inet static
address 10.151.77.110
netmask 255.255.255.252
gateway 10.151.77.109
```

**ROUTING**

* SURABAYA

```
route add -net 192.168.16.0 netmask 255.255.252.0 gw 192.168.0.5 #SBY- SIDOARJO
route add -net 192.168.0.0 netmask 255.255.248.0 gw 192.168.0.5 #SBY-JEMBER&BANYU
route add -net 192.168.0.128 netmask 255.255.255.128 gw 192.168.0.5 #SBY-BONDO
route add -net 192.168.0.12 netmask 255.255.255.254 gw 192.168.0.5 #SBY-PROBO

route add -net 192.168.128.4 netmask 255.255.255.252 gw 192.168.128.9 #SBY-KEDIRI
route add -net 192.168.136.0 netmask 255.255.252.0 gw 192.168.128.9 #SBY-NGANJUK
route add -net 192.168.142.0 netmask 255.255.254.0 gw 192.168.128.9  #SBY-JOMBANGdanMADIUN
route add -net 192.168.140.0 netmask 255.255.255.240 gw 192.168.128.9 #SBY-BOJO
route add -net 10.151.77.108 netmask 255.255.255.252 gw 192.168.128.9 #SBY-MLG
route add -net 192.168.129.0 netmask 255.255.255.0 gw 192.168.128.9 #SBY-BTR&LMJ
```

* PASURUAN

```
route add -net 192.168.0.128 netmask 255.255.255.128 gw 192.168.0.13 # PAS - BDW
route add -net 192.168.0.0 netmask 255.255.248.0 gw 192.168.0.13 # PAS - Banyu
route add -net 192.168.0.0 netmask 255.255.248.0 gw 192.168.0.13
```

* BATU

```
route add -net 10.151.77.108 netmask 255.255.255.252 gw 192.168.128.5 # Batu - MLG
route add -net 192.168.129.0 netmask 255.255.255.0 gw 192.168.128.5 # Batu – LMJ dan Blitar
route add -net 192.168.128.0 netmask 255.255.252.0 gw 192.168.128.5 # Batu – TLA
```

* KEDIRI

```
route add -net 192.168.128.0 netmask 255.255.252.0 gw 192.168.129.1 # Kediri - TLA
```



### Kendala
* Masih terkendala pada PING di CIDR UML, akibat address dan gateway yang keliru.
* File *Cisco* yang sering corrupt dan menyebabkan sulitnya ping antar hardware. Sehingga file CPT harus sering diubuat ulang, serta hardware yang ada pada CPT juga sering terkendala tidak bisa digunakan.
