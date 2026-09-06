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

| Nama Subnet / Segmen | Network ID | Subnet Mask | CIDR | Rentang IP yang Bisa Dipakai | Default Gateway |
| :--- | :--- | :--- | :---: | :--- | :--- |
| Subnet Lantai 1 | `192.168.5.96` | `255.255.255.224` | `/27` | `192.168.5.97 – 192.168.5.126` | `192.168.5.97` |
| Subnet Lantai 2 | `192.168.5.64` | `255.255.255.224` | `/27` | `192.168.5.65 – 192.168.5.94` | `192.168.5.65` |
| Subnet Lantai 3 | `192.168.5.0` | `255.255.255.240` | `/28` | `192.168.5.1 – 192.168.5.14` | `192.168.5.1` |
| Subnet Server | `192.168.5.128` | `255.255.255.252` | `/30` | `192.168.5.129 – 192.168.5.130` | `192.168.5.129` |
| P2P Ruter Lantai 1 – Utama | `192.168.5.132` | `255.255.255.252` | `/30` | `192.168.5.133 – 192.168.5.134` | - |
| P2P Ruter Lantai 2 – Utama | `192.168.5.136` | `255.255.255.252` | `/30` | `192.168.5.137 – 192.168.5.138` | - |
| P2P Ruter Lantai 3 – Utama | `192.168.5.140` | `255.255.255.252` | `/30` | `192.168.5.141 – 192.168.5.142` | - |

## Penamaan Perangkat Standar

| Nama Bawaan Packet Tracer | Nama Standar Perangkat | Tipe Perangkat | Peran / Lokasi Perangkat |
| :--- | :--- | :--- | :--- |
| Router3 | `R-CORE-01` | Cisco Router | Ruter Pusat / Core Router |
| Router0 | `R-LANTAI1-01` | Cisco Router | Ruter Distribusi Lantai 1 |
| Router2 | `R-LANTAI2-01` | Cisco Router | Ruter Distribusi Lantai 2 |
| Router1 | `R-LANTAI3-01` | Cisco Router | Ruter Distribusi Lantai 3 |
| Switch0 | `SW-LANTAI1-01` | Cisco Switch | Switch Akses Lantai 1 |
| Switch1 | `SW-LANTAI2-01` | Cisco Switch | Switch Akses Lantai 2 |
| Switch2 | `SW-LANTAI3-01` | Cisco Switch | Switch Akses Lantai 3 |
| Server0 | `SRV-MAIN-01` | Dedicated Server | Server Data & Web Utama |

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
