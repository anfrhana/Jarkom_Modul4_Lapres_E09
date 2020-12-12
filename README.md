LAPRES JARKOM MODUL 4

Membuat subnet

![image](https://user-images.githubusercontent.com/61223768/101973147-62fdd600-3c68-11eb-801b-2d76d16f9163.png)

**1. VLSM - CPT**

Tentukan jumlah alamat IP yang dibutuhkan oleh tiap subnet dan lakukan labelling netmask berdasarkan jumlah IP yang dibutuhkan.
![image](https://user-images.githubusercontent.com/61223768/101973258-4f9f3a80-3c69-11eb-9334-debeb755c52f.png)

Berdasarkan total IP dan netmask yang dibutuhkan, maka kita dapat menggunakan netmask /19 untuk memberikan pengalamatan IP pada subnet.

Subnet besar yang dibentuk memiliki NID 192.168.0.0 dengan netmask /19. Hitung pembagian IP berdasarkan NID dan netmask tersebut menggunakan pohon seperti gambar di bawah.
![image](https://user-images.githubusercontent.com/61223768/101973295-9c831100-3c69-11eb-8e55-b016ac3cd1fb.png)

Subnet server tidak masuk kedalam pembagian alamat IP. Berikut untuk IP dari server dan cloud
![image](https://user-images.githubusercontent.com/61223768/101973322-d522ea80-3c69-11eb-8471-06c9b1a9f623.png)

**Praktik**

Buka aplikasi Cisco Packet Tracer, buat topologi baru.

**Routing**

![image](https://user-images.githubusercontent.com/61223768/101973407-7742d280-3c6a-11eb-85d7-e4d8ad2cfd3f.png)

**2. CIDR - UML**

Menggabungkan subnet-subnet mulai dari yang paling jauh dalam topologi, penggabungannya:

<img width="599" alt="cidr 1" src="https://user-images.githubusercontent.com/61228737/101979346-fcd87980-3c8e-11eb-91d1-57d4c5d33967.png">

<img width="550" alt="cidr 2" src="https://user-images.githubusercontent.com/61228737/101979348-019d2d80-3c8f-11eb-8027-100129093a48.png">

Diperoleh pohon pembagian IP berdasarkan penggabungan subnet yang telah dilakukan:

<img width="545" alt="ip cidr" src="https://user-images.githubusercontent.com/61228737/101979377-432dd880-3c8f-11eb-9068-8703b1103f3a.png">

NID dibagikan pada setiap subnet pada topologi, menjadi sebagai berikut:
SERVERS

``` 
A1/30 
Subnet Mask 255.255.255.252
Network ID 10.151.71.80
SURABAYA 10.151.71.81
MOJOKERTO 10.151.71.82

A2/30
Subnet Mask 255.255.255.252
Network ID 10.151.71.84
KEDIRI 10.151.71.85
MALANG 10.151.71.86
```
CLIENTS
```
A3/22
Subnet Mask 255.255.252.0
Network ID 192.168.0.0
BLITAR 192.168.0.1
TULUNGAGUNG 192.168.0.2

A4/24
Subnet Mask 255.255.255.0
Network ID 192.168.4.0
KEDIRI 192.168.4.1
BLITAR 192.168.4.2
LUMAJANG 192.168.4.3

A5/30 
Subnet Mask 255.255.255.252
Network ID 192.168.8.0
BATU 192.168.8.1
KEDIRI 192.168.8.2

A6/22
Subnet Mask 255.255.252.0
Network ID 192.168.20.0
BATU 192.168.20.1
NGANJUK 192.168.20.2

A7/28
Subnet Mask 255.255.255.240
Network ID 192.168.18.0
MADIUN 192.168.18.1
BOJONEGORO 192.168.18.2

A8/23
Subnet Mask 255.255.254.0
Network ID 192.168.16.0
BATU 192.168.16.1
MADIUN 192.168.16.2
JOMBANG 192.168.16.3

A9/30
Subnet Mask 255.255.255.252
Network ID 192.168.32.0
SURABAYA 192.168.32.1
BATU 192.168.32.2

A10/22
Subnet Mask 255.255.252.0
Network ID 192.168.160.0
PASURUAN 192.168.160.1
SIDOARJO 192.168.160.2

A11/21 
Subnet Mask 255.255.248.0
Network ID 192.168.128.0
PROBOLINGGO 192.168.128.1
BANYUWANGI 192.168.128.2
JEMBER 192.168.132.1

A12/25 
Subnet Mask 255.255.255.128
Network ID 192.168.136.0
PROBOLINGGO 192.168.136.1
BONDOWOSO 192.168.136.2

A13/30
Subnet Mask 255.255.255.252
Network ID 192.168.144.0
PASURUAN 192.168.144.1
PROBOLINGGO 192.168.144.2

A14/30
Subnet Mask 255.255.255.252
Network ID 192.168.192.0
SURABAYA 192.168.192.1
PASURUAN 192.168.192.2

A15/22
Subnet Mask 255.255.252.0
Network ID 192.168.64.0
SURABAYA 192.168.64.1
SAMPANG 192.168.64.2
```
Buat file topologi.sh dengan konfigurasi sebagai berikut:
```
# Switch
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch12 > /dev/null < /dev/null &
uml_switch -unix switch13 > /dev/null < /dev/null &
uml_switch -unix switch14 > /dev/null < /dev/null &
uml_switch -unix switch15 > /dev/null < /dev/null &
uml_switch -unix switch16 > /dev/null < /dev/null &
uml_switch -unix switch17 > /dev/null < /dev/null &
uml_switch -unix switch18 > /dev/null < /dev/null &
uml_switch -unix switch19 > /dev/null < /dev/null &
uml_switch -unix switch20 > /dev/null < /dev/null &
uml_switch -unix switch21 > /dev/null < /dev/null &
uml_switch -unix switch22 > /dev/null < /dev/null &
uml_switch -unix switch23 > /dev/null < /dev/null &
uml_switch -unix switch24 > /dev/null < /dev/null &
uml_switch -unix switch25 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.70.41 eth1=daemon,,,switch1 eth2=daemon,,,switch24 eth3=daemon,,,switch23 eth4=daemon,,,switch13 mem=64M &
xterm -T PASURUAN -e linux ubd0=PASURUAN,jarkom umid=PASURUAN eth0=daemon,,,switch24 eth1=daemon,,,switch14 eth2=daemon,,,switch19 mem=64M &
xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch14 eth1=daemon,,,switch15 eth2=daemon,,,switch16 mem=64M &
xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch23 eth1=daemon,,,switch12 eth2=daemon,,,switch21 eth3=daemon,,,switch22 mem=64M &
xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch12 eth1=daemon,,,switch17 eth2=daemon,,,switch18 mem=64M &
xterm -T BLITAR -e linux ubd0=BLITAR,jarkom umid=BLITAR eth0=daemon,,,switch17 eth1=daemon,,,switch20 mem=64M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch22 eth1=daemon,,,switch25 mem=64M &

# Server
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch18 mem=64M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch13 mem=64M &

# Client
xterm -T SAMPANG -e linux ubd0=SAMPANG,jarkom umid=SAMPANG eth0=daemon,,,switch1 mem=64M &
xterm -T BONDOWOSO -e linux ubd0=BONDOWOSO,jarkom umid=BONDOWOSO eth0=daemon,,,switch15 mem=64M &
xterm -T JEMBER -e linux ubd0=JEMBER,jarkom umid=JEMBER eth0=daemon,,,switch16 mem=64M &
xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI,jarkom umid=BANYUWANGI eth0=daemon,,,switch16 mem=64M &
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch19 mem=64M &
xterm -T LUMAJANG -e linux ubd0=LUMAJANG,jarkom umid=LUMAJANG eth0=daemon,,,switch17 mem=64M &
xterm -T TULUNGAGUNG -e linux ubd0=TULUNGAGUNG,jarkom umid=TULUNGAGUNG eth0=daemon,,,switch20 mem=64M &
xterm -T NGANJUK -e linux ubd0=NGANJUK,jarkom umid=NGANJUK eth0=daemon,,,switch21 mem=64M &
xterm -T BOJONEGORO -e linux ubd0=BOJONEGORO,jarkom umid=BOJONEGORO eth0=daemon,,,switch25 mem=64M &
xterm -T JOMBANG -e linux ubd0=JOMBANG,jarkom umid=JOMBANG eth0=daemon,,,switch22 mem=64M &
```
Siapkan juga file ```nano bye.sh``` sebagai berikut:
```
uml_mconsole SURABAYA halt
uml_mconsole PASURUAN halt
uml_mconsole PROBOLINGGO halt
uml_mconsole BATU halt
uml_mconsole KEDIRI halt
uml_mconsole BLITAR halt
uml_mconsole MADIUN halt
uml_mconsole MALANG halt
uml_mconsole MOJOKERTO halt
uml_mconsole SIDOARJO halt
uml_mconsole SAMPANG halt
uml_mconsole BANYUWANGI halt
uml_mconsole BONDOWOSO halt
uml_mconsole JEMBER halt
uml_mconsole LUMAJANG halt
uml_mconsole TULUNGAGUNG halt
uml_mconsole NGANJUK halt
uml_mconsole BOJONEGORO halt
uml_mconsole JOMBANG halt
```

Lakukan konfigurasi network interface pada setiap UML.
Sebelum itu, UML yang merupakan router, lakukan ```nano /etc/sysctl.conf``` uncomment pada ```net.ipv4.ip_forward=1``` agar dapat meneruskan route dan ```sysctl -p``` untuk mengaktifkan.
Jalankan ```nano /etc/network/interfaces``` pada tiap uml.
Kemudian buat konfigurasi seperti berikut:
SURABAYA (router)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.70.42
netmask 255.255.255.252
gateway 10.151.70.41

auto eth1
iface eth1 inet static
address 192.168.64.1
netmask 255.255.252.0

auto eth2
iface eth2 inet static
address 192.168.192.1
netmask 255.255.255.252

auto eth3
iface eth3 inet static
address 192.168.32.1
netmask 255.255.255.252

auto eth4
iface eth4 inet static
address 10.151.71.81
netmask 255.255.255.252
```

PASURUAN (router)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.192.2
netmask 255.255.255.252
gateway 192.168.192.1

auto eth1
iface eth1 inet static
address 192.168.144.1
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.168.160.1
netmask 255.255.252.0
```

PROBOLINGGO (router)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.144.2
netmask 255.255.255.252
gateway 192.168.144.1

auto eth1
iface eth1 inet static
address 192.168.136.1
netmask 255.255.255.128

auto eth2
iface eth2 inet static
address 192.168.128.1
netmask 255.255.248.0
```

BATU (router)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.32.2
netmask 255.255.255.252
gateway 192.168.32.1

auto eth1
iface eth1 inet static
address 192.168.8.1
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.168.20.1
netmask 255.255.252.0

auto eth3
iface eth3 inet static
address 192.168.16.1
netmask 255.255.254.0
```

KEDIRI (router)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.8.2
netmask 255.255.255.252
gateway 192.168.8.1

auto eth1
iface eth1 inet static
address 192.168.4.1
netmask 255.255.255.0

auto eth2
iface eth2 inet static
address 10.151.71.85
netmask 255.255.255.252
```

BLITAR (router)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.4.2
netmask 255.255.255.0
gateway 192.168.4.1

auto eth1
iface eth1 inet static
address 192.168.0.1
netmask 255.255.252.0
```

MADIUN (router)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.16.2
netmask 255.255.254.0
gateway 192.168.16.1

auto eth1
iface eth1 inet static
address 192.168.18.1
netmask 255.255.255.240
```

MALANG (server)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.71.86
netmask 255.255.255.252
gateway 10.151.71.85
```

MOJOKERTO (server)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.71.82
netmask 255.255.255.252
gateway 10.151.71.81
```

SAMPANG (client)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.64.2
netmask 255.255.252.0
gateway 192.168.64.1
```

BONDOWOSO (client)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.136.2
netmask 255.255.255.128
gateway 192.168.136.1
```

JEMBER (client)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.132.1
netmask 255.255.248.0
gateway 192.168.128.1
```

BANYUWANGI (client)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.128.2
netmask 255.255.248.0
gateway 192.168.128.1
```

SIDOARJO (client)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.160.2
netmask 255.255.252.0
gateway 192.168.160.1
```

LUMAJANG (client)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.4.3
netmask 255.255.255.0
gateway 192.168.4.1
```

TULUNGAGUNG (client)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.252.0
gateway 192.168.0.1
```

NGANJUK (client)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.20.2
netmask 255.255.252.0
gateway 192.168.20.1
```

BOJONEGORO (client)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.18.2
netmask 255.255.255.240
gateway 192.168.18.1
```

JOMBANG (client)
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 192.168.16.3
netmask 255.255.254.0
gateway 192.168.16.1
```

Pada UML SURABAYA lakukan perintah ```iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE –s 192.168.0.0/16```

Pada router SURABAYA, BATU, PASURUAN, dan KEDIRI ditambahkan route seperti berikut:
- **SURABAYA** = D1, Malang, D2
- **BATU** = A7, Malang, B1
- **PASURUAN** = B3
- **KEDIRI** = A3

Ketikkan perintah ```nano route.sh```.
Kemudian tambahkan route berikut:

SURABAYA
```
ip route add 192.168.0.0/19 via 192.168.32.2 dev eth3
ip route add 10.151.71.84/30 via 192.168.32.2 dev eth3
ip route add 192.168.128.0/18 via 192.168.192.2 dev eth2
```

BATU
```
ip route add 192.168.18.0/28 via 192.168.16.2 dev eth3
ip route add 10.151.71.84/30 via 192.168.8.2 dev eth1
ip route add 192.168.0.0/21 via 192.168.8.2 dev eth1
```
PASURUAN
```
ip route add 192.168.128.0/20 via 192.168.144.2 dev eth1
```

KEDIRI
```
ip route add 192.168.0.0/22 via 192.168.4.2 dev eth1
```
Jalankan file route.sh dengan perintah ```source route.sh```.

Cek apakah routing dan CIDR sudah berjalan dengan baik dengan melakukan beberapa tes.
PROBOLINGGO ping ke JOMBANG

<img width="365" alt="probolinggo ping jombang" src="https://user-images.githubusercontent.com/61228737/101981096-036ded80-3c9d-11eb-9e49-7230974b4093.png">

PROBOLINGGO ping ke MOJOKERTO

<img width="365" alt="probolinggo ping mojo" src="https://user-images.githubusercontent.com/61228737/101981099-08cb3800-3c9d-11eb-86c8-3e94a57a6d9c.png">

MALANG ping ke MOJOKERTO

<img width="366" alt="malang ping mojo" src="https://user-images.githubusercontent.com/61228737/101981107-18e31780-3c9d-11eb-85c2-cc26e2616d77.png">

MALANG ping ke BANYUWANGI

<img width="365" alt="malang ping banyuwangi" src="https://user-images.githubusercontent.com/61228737/101981110-1f718f00-3c9d-11eb-881b-8f1fb77b67f0.png">

KEDIRI ping ke PROBOLINGGO

<img width="363" alt="kediri ping probolinggo" src="https://user-images.githubusercontent.com/61228737/101981115-24364300-3c9d-11eb-9a35-30aab459cb79.png">

MOJOKERTO ping ke BOJONEGORO

<img width="364" alt="mojokerto ping bojonegoro" src="https://user-images.githubusercontent.com/61228737/101981120-27c9ca00-3c9d-11eb-9bcf-e320686f884e.png">

TULUNGAGUNG ping ke JEMBER

<img width="364" alt="tulungagung ping ke jember" src="https://user-images.githubusercontent.com/61228737/101981122-2ac4ba80-3c9d-11eb-8c68-3c7532d68ecd.png">

LUMAJANG ping ke JOMBANG

<img width="363" alt="lumajang ping jombang" src="https://user-images.githubusercontent.com/61228737/101981123-2dbfab00-3c9d-11eb-9350-11c7e54cc9fa.png">
