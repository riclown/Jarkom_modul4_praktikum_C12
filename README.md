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
