# Perancangan Topologi Jaringan Enterprise Multi-Lantai

## Ringkasan Proyek
Proyek ini merupakan simulasi infrastruktur jaringan LAN untuk gedung bertingkat menggunakan Cisco Packet Tracer. Perancangan ini menerapkan teknik Variable Length Subnet Masking (VLSM) untuk pengalamatan IP yang efisien, penamaan perangkat yang terstruktur, koneksi point-to-point antarruter, serta isolasi segmen server utama demi menjaga keamanan dan performa lalu lintas data.

## Arsitektur Jaringan
![Topologi Jaringan Enterprise](Gambar%20Topologi.PNG)

### Fitur Utama Jaringan
* Segmentasi Multi-Lantai: Pemisahan subnet untuk Lantai 1, Lantai 2, Lantai 3, dan segmen server terpisah.
* Efisiensi Pengalamatan IP (VLSM): Pembagian alokasi IP menggunakan subnet /27, /28, dan /30 dari blok IP dasar 192.168.5.0/24.
* Routing Antarruter: Komunikasi antar-ruter menggunakan koneksi Point-to-Point (P2P) berbasis subnet /30.
* Isolasi Server: Server diletakkan di segmen tersendiri agar seluruh lalu lintas akses data melewati ruter utama terlebih dahulu.

## Skema Pengalamatan IP dan Subnetting

* Subnet Lantai 1
  * Network ID: 192.168.5.96
  * Subnet Mask: 255.255.255.224 (/27)
  * Rentang IP usable: 192.168.5.97 – 192.168.5.126
  * Default Gateway: 192.168.5.97

* Subnet Lantai 2
  * Network ID: 192.168.5.64
  * Subnet Mask: 255.255.255.224 (/27)
  * Rentang IP usable: 192.168.5.65 – 192.168.5.94
  * Default Gateway: 192.168.5.65

* Subnet Lantai 3
  * Network ID: 192.168.5.0
  * Subnet Mask: 255.255.255.240 (/28)
  * Rentang IP usable: 192.168.5.1 – 192.168.5.14
  * Default Gateway: 192.168.5.1

* Subnet Server
  * Network ID: 192.168.5.128
  * Subnet Mask: 255.255.255.252 (/30)
  * Rentang IP usable: 192.168.5.129 – 192.168.5.130
  * Default Gateway: 192.168.5.129

* P2P Ruter Lantai 1 – Utama
  * Network ID: 192.168.5.132
  * Subnet Mask: 255.255.255.252 (/30)
  * Rentang IP usable: 192.168.5.133 – 192.168.5.134
  * Default Gateway: Tidak ada

* P2P Ruter Lantai 2 – Utama
  * Network ID: 192.168.5.136
  * Subnet Mask: 255.255.255.252 (/30)
  * Rentang IP usable: 192.168.5.137 – 192.168.5.138
  * Default Gateway: Tidak ada

* P2P Ruter Lantai 3 – Utama
  * Network ID: 192.168.5.140
  * Subnet Mask: 255.255.255.252 (/30)
  * Rentang IP usable: 192.168.5.141 – 192.168.5.142
  * Default Gateway: Tidak ada

## Penamaan Perangkat Standar

* Router3 (Packet Tracer)
  * Nama Standar: R-CORE-01
  * Tipe: Cisco Router
  * Peran: Ruter Pusat / Core Router

* Router0 (Packet Tracer)
  * Nama Standar: R-LANTAI1-01
  * Tipe: Cisco Router
  * Peran: Ruter Distribusi Lantai 1

* Router2 (Packet Tracer)
  * Nama Standar: R-LANTAI2-01
  * Tipe: Cisco Router
  * Peran: Ruter Distribusi Lantai 2

* Router1 (Packet Tracer)
  * Nama Standar: R-LANTAI3-01
  * Tipe: Cisco Router
  * Peran: Ruter Distribusi Lantai 3

* Switch0 (Packet Tracer)
  * Nama Standar: SW-LANTAI1-01
  * Tipe: Cisco Switch
  * Peran: Switch Akses Lantai 1

* Switch1 (Packet Tracer)
  * Nama Standar: SW-LANTAI2-01
  * Tipe: Cisco Switch
  * Peran: Switch Akses Lantai 2

* Switch2 (Packet Tracer)
  * Nama Standar: SW-LANTAI3-01
  * Tipe: Cisco Switch
  * Peran: Switch Akses Lantai 3

* Server0 (Packet Tracer)
  * Nama Standar: SRV-MAIN-01
  * Tipe: Dedicated Server
  * Peran: Server Data & Web Utama

## Langkah-Langkah Pengerjaan

### 1. Perencanaan Subnetting (VLSM)
Saya menghitung kebutuhan alamat IP berdasarkan jumlah perangkat di tiap lantai:
* Lantai 1 membutuhkan hingga 30 host (/27).
* Lantai 2 membutuhkan hingga 30 host (/27).
* Lantai 3 membutuhkan hingga 14 host (/28).
* Server khusus 1 host (/30).
* Jalur koneksi antar-ruter 2 host per alur (/30).

Semua alokasi dihitung dari blok alamat IP dasar 192.168.5.0/24 untuk menghindari pemborosan alokasi IP.

### 2. Penyusunan Topologi dan Perkabelan
* Menambahkan 4 ruter dan 3 switch ke dalam lembar kerja Cisco Packet Tracer.
* Menghubungkan PC dan Laptop ke switch di masing-masing lantai menggunakan kabel Straight-Through.
* Menghubungkan switch ke ruter lantai yang sesuai.
* Menghubungkan seluruh ruter distribusi lantai ke ruter pusat (R-CORE-01) menggunakan kabel Serial dan GigabitEthernet.

### 3. Konfigurasi Alamat IP
* Mengisikan IP statis, subnet mask, dan default gateway pada tiap PC dan Laptop di setiap lantai.
* Memasang alamat IP pada antarmuka (interface) LAN dan WAN di seluruh ruter.

### 4. Pengaturan Routing
* Mengkonfigurasi routing pada setiap ruter agar seluruh subnet di tiap lantai dapat saling berkomunikasi dan mengakses server utama.
* Memeriksa tabel routing di R-CORE-01 untuk memastikan seluruh rute telah aktif.

### 5. Pengujian dan Verifikasi
* Melakukan uji konektivitas ICMP ping antar-PC dari lantai yang berbeda (misalnya dari PC Lantai 1 ke Laptop Lantai 3).
* Menguji aksesibilitas dari PC ke server utama SRV-MAIN-01.
* Memeriksa rute lalu lintas data menggunakan perintah tracert / traceroute.

## Cara Menjalankan File Simulasi
1. Clone repositori ini ke komputer local:
   ```bash
   git clone [https://github.com/Verrypratama/cisco-enterprise-network.git](https://github.com/Verrypratama/cisco-enterprise-network.git)
