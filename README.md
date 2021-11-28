# Jarkom-Modul-4-E13-2021

Kelompok E13

|NRP           |Nama                   |
|:------------:|:---------------------:|
|05111940000090|Ihsannur Rahman Qalbi|
|05111940000003|Fairuz Hasna Rofifah|
|05111940000164|Ahmad Aunul Ma`bud|

# VLSM (**Variable Length Subnet Masking)**

### Topologi dan Pembagian Subnet di CPT

![subnetting.jpg](Jarkom-E13-Modul-4%20ddca130ac5de47ccb3fb3f7d35341588/subnetting.jpg)

### Menentukan jumlah IP yang dibutuhkan

| Subnet | Kebutuhan IP | Prefix Length | NID |
| --- | --- | --- | --- |
| A4 | 2021 | 21 | 192.206.24.0 |
| A3 | 701 | 22 | 192.206.4.0 |
| A7 | 521 | 22 | 192.206.8.0 |
| A8 | 1001 | 22 | 192.206.12.0 |
| A13 | 721 | 22 | 192.206.16.0 |
| A11 | 502 | 23 | 192.206.2.0 |
| A5 | 252 | 24 | 192.206.1.0 |
| A1 | 101 | 25 | 192.206.0.128 |
| A12 | 13 | 28 | 192.206.0.8 |
| A2 | 2 | 30 | 192.206.0.0 |
| A6 | 2 | 30 | 192.206.0.4 |
| A9 | 2 | 30 | 192.206.0.8 |
| A10 | 2 | 30 | 192.206.0.12 |
| A14 | 2 | 30 | 192.206.0.32 |
| A15 | 2 | 30 | 192.206.0.36 |
| Total | 5841 | 19 |  |

### Melakukan Pembagian IP

Subnet besar yang dibentuk memiliki NID **192.206.0.0** dengan netmask **/19**. Kemudian dihitung pembagian IP berdasarkan NID dan netmask tersebut menggunakan pohon seperti gambar di bawah.

![vlsm_tree.jpg](Jarkom-E13-Modul-4%20ddca130ac5de47ccb3fb3f7d35341588/vlsm_tree.jpg)

### Routing Pada CPT

Kemudian dilakukan konfigurasi static routing pada setiap router yang sudah dibuat berdasarkan dengan konfigurasi sebagai berikut:

- **FOOSHA**
    ```
    192.206.24.0/21 via 192.206.0.6
    192.206.4.0/22 via 192.206.0.6
    192.206.8.0/22 via 192.206.0.10
    192.206.16.0/22 via 192.206.0.10
    192.206.12.0/22 via 192.206.12.2
    192.206.2.0/23 via 192.206.0.10
    192.206.1.0/24 via 192.206.0.10
    192.206.0.128/25 via 192.206.0.6
    192.206.0.16/28 via 192.206.0.10
    192.206.0.12/30 via 192.206.0.10
    192.206.0.8/30 via 192.206.0.10
    192.206.0.0/30 via 192.206.0.6
    192.206.0.4/30 via 192.206.0.6
    192.206.0.32/30 via 192.206.0.34
    192.206.0.36/30 via 192.206.0.10
    
    ```
- **WATER7**
    ```
    192.206.0.128/25 via 192.206.0.2
    192.206.24.0/21 via 192.206.0.2
    0.0.0.0/0 via 192.206.0.5
    ```
- **PUCCI**
    ```
    > 0.0.0.0/0 via 192.206.0.1
    ```
- **GUANHAO**
    
    ```
    0.0.0.0/0 via 192.206.0.9
    192.206.0.8/30 via 192.206.2.2
    192.206.0.16/28 via 192.206.2.2
    192.206.0.12/30 via 192.206.0.14
    192.206.1.0/24 via 192.206.0.14
    192.206.16.0/22 via 192.206.0.14
    192.206.0.36/30 via 192.206.0.14
    ```
- **OIMO**
    ```
    0.0.0.0/0 via 192.206.0.13
    192.206.16.0/22 via 192.206.1.3
    ```
- **SEASTONE**
    ```
    0.0.0.0/0 via 192.206.1.1
    ```
- **ALABASTA**
    ```
    0.0.0.0/0 via 192.206.2.1
    ```

# CIDR (**Classless Inter Domain Routing)**

### Topologi dan Pembagian Subnet di GNS3

![subnetting-baru-oni-revisi.jpg](Jarkom-E13-Modul-4%20ddca130ac5de47ccb3fb3f7d35341588/subnetting-baru-oni-revisi.jpg)

Dengan kebutuhan IP dan netmask yang sama seperti VLSM, kemudian diberlakukan pengelompokan subnet seperti gambar dibawah ini:

![Untitled](Jarkom-E13-Modul-4%20ddca130ac5de47ccb3fb3f7d35341588/Untitled.png)

Subnet besar yang dibentuk memiliki netmask **/15**. Kemudian dihitung pembagian IP berdasarkan pengelompokan dan netmask tersebut menggunakan pohon seperti gambar di bawah.

![Untitled](Jarkom-E13-Modul-4%20ddca130ac5de47ccb3fb3f7d35341588/Untitled%201.png)

Berdasarkan pohon diatas, didapatkan NID dan netmask untuk setiap subnet sebagai berikut:

![Untitled](Jarkom-E13-Modul-4%20ddca130ac5de47ccb3fb3f7d35341588/Untitled3.png)

### Network Configuration Setiap Node

---

Foosha

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
address 192.207.128.1
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.207.64.1
netmask 255.255.255.252

auto eth3
iface eth3 inet static
address 192.206.64.1
netmask 255.255.255.252

auto eth4
iface eth4 inet static
address 192.206.128.1
netmask 255.255.252.0
```

Blueno (1000 Host)

```
auto eth0
iface eth0 inet static
address 192.206.128.2
netmask 255.255.252.0
gateway 192.206.128.1
```

Water7

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.206.64.2
netmask 255.255.255.252
gateway 192.206.64.1

auto eth1
iface eth1 inet static
address 192.206.16.1
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.206.32.1
netmask 255.255.252.0
```

Cipher (700 Host)

```
auto eth0
iface eth0 inet static
address 192.206.32.2
netmask 255.255.252.0
gateway 192.206.32.1
```

Pucci

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.206.16.2
netmask 255.255.255.252
gateway 192.206.16.1

auto eth1
iface eth1 inet static
address 192.206.0.1
netmask 255.255.248.0

auto eth2
iface eth2 inet static
address 192.206.8.1
netmask 255.255.255.128
```

Cambelt (1000 Host)

```
auto eth0
iface eth0 inet static
address 192.206.0.2
netmask 255.255.248.0
gateway 192.206.0.1
```

Couryard (1020 Host)

```
auto eth0
iface eth0 inet static
address 192.206.0.3
netmask 255.255.248.0
gateway 192.206.0.1
```

Jipangu (100 Host)

```
auto eth0
iface eth0 inet static
address 192.206.8.2
netmask 255.255.255.128
gateway 192.206.8.1
```

Doriki (Server)

```
auto eth0
iface eth0 inet static
address 192.207.128.2
netmask 255.255.255.252
gateway 192.207.128.1
```

Guanhao

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.207.64.2
netmask 255.255.255.252
gateway 192.207.64.1

auto eth1
iface eth1 inet static
address 192.207.32.1
netmask 255.255.254.0

auto eth2
iface eth2 inet static
address 192.207.16.1
netmask 255.255.255.252

auto eth3
iface eth3 inet static
address 192.207.36.1
netmask 255.255.252.0
```

Maingate (500 Host)

```
auto eth0
iface eth0 inet static
address 192.207.32.2
netmask 255.255.254.0
gateway 192.207.32.1
```

Alabasta

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.207.32.3
netmask 255.255.254.0
gateway 192.207.32.1

auto eth1
iface eth1 inet static
address 192.207.34.1
netmask 255.255.255.240
```

Jorge (12 Host)

```
auto eth0
iface eth0 inet static
address 192.207.34.2
netmask 255.255.255.240
gateway 192.207.34.1
```

Jabra (520 Host)

```
auto eth0
iface eth0 inet static
address 192.207.36.2
netmask 255.255.252.0
gateway 192.207.36.1
```

Oimo

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.207.16.2
netmask 255.255.255.252
gateway 192.207.16.1

auto eth1
iface eth1 inet static
address 192.207.8.1
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.207.4.1
netmask 255.255.255.0
```

Fukurou (Server)

```
auto eth0
iface eth0 inet static
address 192.207.8.2
netmask 255.255.255.252
gateway 192.207.8.1
```

EniesLobby (250 Host)

```
auto eth0
iface eth0 inet static
address 192.207.4.2
netmask 255.255.255.0
gateway 192.207.4.1
```

Seastone

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.207.4.3
netmask 255.255.255.0
gateway 192.207.4.1

auto eth1
iface eth1 inet static
address 192.207.0.1
netmask 255.255.252.0
```

Elena (720 Host)

```
auto eth0
iface eth0 inet static
address 192.207.0.2
netmask 255.255.252.0
gateway 192.207.0.1
```

## Kendala

1. Lupa memberikan IP kepada server saat melakukan subnetting menggunakan metode VLSM
2. Kebingungan waktu membuat pohon untuk melakukan subnetting menggunakan metode CIDR


### Pembagian Tugas
|Nama|Pengerjaan|
|:------------:|:---------------------:|
|Fairuz Hasna Rofifah|Topologi GNS3, Topologi CPT|
|Ahmad Aunul Ma`bud|Topologi GNS3, Pembagian Subnet GNS3|
|Ihsannur Rahman Qalbi|Routing CPT,Pembagian Subnet CPT|
