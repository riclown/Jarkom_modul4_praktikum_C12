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

* IP
* IP

## Soal 1

## CIDR
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



## Soal 2

Sintaks untuk **topo.sh**

```
# Switch

# Router

# Server

# Klien
```
![BELUM TERSEDIA](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/100.0.jpg)

Lalu  jalankan `bash topo.sh` pada *putty* dan masukkan *username* dan *password* default. Pada router **SURABAYA** lakukan setting `sysctl` dengan mengetikkan perintah `nano /etc/sysctl.conf`, dan tambahkan `net.ipv4.conf.all.accept_source_route = 1`.

![BELUM TERSEDIA](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/100.0.jpg)

Lalu setting IP pada setiap *interfaces* uml dengan mengetikkan `nano /etc/network/interfaces` sebagai berikut:

**SURABAYA (Sebagai Router)**

```
auto lo
```

![BELUM TERSEDIA](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/100.0.jpg)

**MALANG (Sebagai Server)**

```
auto lo

```

![BELUM TERSEDIA](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/100.0.jpg)

**MOJOKERTO (Sebagai Server)**

```
auto lo
```

![BELUM TERSEDIA](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/100.0.jpg)

**TUBAN (Sebagai )**

```
auto lo
```

![BELUM TERSEDIA](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/100.0.jpg)

**SIDOARJO (Sebagai )**

```
auto lo
```

![BELUM TERSEDIA](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/100.0.jpg)

**GRESIK (Sebagai )**

```
auto lo
```

![BELUM TERSEDIA](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/100.0.jpg)

**BANYUWANGI (Sebagai )**

```
auto lo
```

![BELUM TERSEDIA](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/100.0.jpg)

**MADIUN (Sebagai )**

```
auto lo
```

![BELUM TERSEDIA](https://github.com/riclown/Jarkom_modul4_praktikum_C12/blob/main/img/100.0.jpg)


### Kendala
* S
