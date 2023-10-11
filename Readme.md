# E-commerce Data Warehouse Implementation

## Project Based Virtual Internship Program | Data Engineer ID/X Partners
## Table of Contents

- [Introduction](#introduction)
- [CV](#cv)
- [Background](#background)
- [Solution](#solution)
- [Outline](#outline)
- [Import/Restore Database](#importrestore-database)
- [Create Data Warehouse](#create-data-warehouse)
- [Database Connection](#database-connection)
- [ETL Process with Talend Jobs](#etl-process-with-talend-jobs)
- [Store Procedure](#store-procedure)
- [Next Project](#next-project)

## Introduction

Halo semua, selamat datang di presentasi Data Engineering Test untuk program Project-Based Internship dari Rakamin Academy dan ID/X Partners.

Pada project kali ini, kita akan implementasi Data Warehouse pada E-commerce.

## CV

Perkenalkan, nama saya Yogi Fitriadi Rakhim. Saya freshgraduate di bidang teknik, memiliki semangat yang kuat dalam dunia data engineering. Saya juga sangat antusias untuk memulai karier saya di bidang ini.

Saat ini, saya tengah menjalani perjalanan Data Fellowship di IYKRA, di mana saya terus-menerus belajar dan mengaplikasikan keterampilan saya disana.

## Background

**Problem Statement**

Salah satu klien ID/X Partners yang beroperasi di sektor e-commerce memiliki kebutuhan untuk membuat Data Warehouse yang bersumber dari beberapa tabel dalam database sumber mereka.

**Challange**

- **Database Restoration (Pemulihan Database):** Proses pemulihan database menjadi tahap awal dalam proyek ini.
- **Penyiapan Tabel (Table Setup):** Membangun tabel-tabel yang diperlukan untuk Data Warehouse.
- **Pengembangan Proses ETL (Extract, Transform, Load):** Menciptakan alur kerja ETL yang efisien dan andal untuk menggabungkan data dari berbagai sumber ke dalam Data Warehouse.
- **Pembuatan Stored Procedures (SP Creation):** Membuat stored prosedur untuk mengelola dan mengakses data dengan efektif.

## Solution

**Output**

Proyek ini berhasil memberikan solusi Data Warehouse yang terstruktur dengan baik bagi klien e-commerce ID/X Partners.

**Objectives Key**

1. **Pemulihan Database** Berhasil dilakukan
2. Tabel-tabel yang terstruktur dengan rapi untuk mendukung penyimpanan data yang efisien.
3. Sudah terbangun alur kerja ETL yang efisien dan andal untuk mengintegrasikan data dari sumber ke dalam Data Warehouse.
4. **Stored Procedure sudah dibuat** untuk menghasilkan ringkasan data yang berguna.
    1. Sehingga Meningkatkan efisiensi dalam proses pelaporan.

**Teknologi**

Pada project ini dipakai teknologi servis dari Microsoft SQL Server Management, dan Talend.

**Pipeline**

Untuk pipeline data warehousenya adalah sebagai berikut:

Diawali dari database staging yang sudah di-restore dikoneksikan ke Talend untuk dilakukan beberapa rangkaian job ETL yang menginput data ke data warehouse yang sudah dibuat, sehingga bisa memberikan akses store procedure untuk menghasilkan summary sales order dari e-commerce client.

## Outline

Berikut adalah outline pembahasan untuk project ini dimulai dari Import/Restore database hingga dokumentasi terkait project ini yang bisa diakses secara publik.

## Import/Restore Database

Pada tahapan restore database:

Staging Database berfungsi sebagai database sumber utama projek ini dan mencakup beragam tabel, seperti:

- **`customer`** → yang berisi **Informasi tentang pelanggan.**
- **`product`** → yang berisi **Detail produk yang tersedia.**
- **`sales_order`** → yang berisi **Catatan transaksi pelanggan.**
- **`status_order`** → yang berisi **Deskripsi status pesanan pelanggan.**

## Create Data Warehouse

Lanjut ke tahapan membuat data warehouse:

Data Warehouse yang kita beri nama DWH_Project berperan sebagai destinasi data yang diekstrak sebelumnya dari Staging Database.

Proyek ini mengadopsi struktur data Star Schema, yang terdiri dari tiga dimension tabel dan satu fact table.

- Tabel Fakta berisi data numerik,
- sementara tabel dimensi memberikan konteks dan informasi yang mendeskripsikan tabel faktual.

Star Schema memberikan struktur yang efisien dan efektif untuk menyimpan dan mengakses data dalam lingkup Data Warehouse.

## Database Connection

Setelah database sumber dan tujuan sudah dibuat, waktunya kita mengkoneksikan kedua database tersebut ke Talend.

Untuk mengkoneksikan database dalam Talend, kita perlu mengonfigurasi komponen-komponen database dalam Talend Metadata.

Biasanya, ini melibatkan parameter:

- Jenis Database yang dipakai (contohnya: MySQL, SQL Server)
- Detail Koneksi (hostname, port, username, password)

Nah setelah koneksi telah terbentuk, kita dapat menggunakan komponen-komponen ini untuk integrasi dan transformasi data yang lancar dalam proses ETL kita di Talend.

## ETL Process with Talend Jobs

Pembuatan pekerjaan ETL melibatkan tiga langkah penting:

1. **Extract** - Mengambil data dari Staging Database.
    - Menggunakan komponen tMSSqlInput untuk mengambil data sumber dari tabel.
2. **Transform** - Melakukan transformasi data sesuai kebutuhan.
    - Dalam kasus tertentu, seperti tabel pada customer, kami menggunakan komponen **tMap** untuk mengubah nilai kolom first_name dan last_name agar bisa digabungkan menjadi satu nilai yaitu Customername.
3. **Load** - Memuat data yang telah diubah ke Data Warehouse yang telah ada.
    - Komponen tMSSqlOutput digunakan untuk menentukan target penyimpanan database.

## Store Procedure

Setelah semua tabel pada data warehouse telah terisi, kita perlu membuat sebuah stored procedure yang diberi nama "summary_order_status." yang bertujuan untuk memudahkan analisis pesanan berdasarkan kriteria status pesanannya.

Stored procedure ini juga memungkinkan pengambilan informasi yang disummary tentang pesanan penjualan, memungkinkan analisis efisien tentang status pesanan.

- **StatusID = 1**: Menunggu Pembayaran (Awaiting Payment)
- **StatusID = 2**: Menunggu Pengiriman (Awaiting Shipment)
- **StatusID = 3**: Telah Dikirim (Shipped)
- **StatusID = 4**: Selesai (Completed)
- **StatusID = 5**: Dibatalkan (Cancelled)

Bisa dilihat bahwa tidak ada data status pesanan yang dibatalkan oleh pelanggan, sebagaimana ditunjukkan oleh Status ID 5.

## Next Project

Dalam proyek mendatang, ada beberapa rekomendasi penting yang perlu dipertimbangkan:

1. **Automatisasi Proses ETL**
    - Automatisasi proses Ekstraksi, Transformasi, dan Pemuatan (ETL) akan meningkatkan efisiensi.
    - Gunakan alat otomatisasi ETL seperti Apache NiFi, Talend, atau Apache Airflow untuk menjadwalkan dan menjalankan tugas ETL.
2. **Implementasikan Kerangka Manajemen Kualitas Data yang Kuat**
    - Memastikan kualitas data yang tinggi penting untuk analisis dan pelaporan yang andal.
    - Gunakan alat seperti Apache Nutch atau Trifacta untuk mengidentifikasi dan memperbaiki masalah kualitas data, seperti duplikat, nilai yang hilang, dan ketidaksesuaian.
3. **Eksplorasi Integrasi Data Real-Time**
    - Pertimbangkan integrasi data real-time jika proyek melibatkan data kritis yang memerlukan pemrosesan segera.
    - Manfaatkan teknologi seperti Apache Kafka atau Confluent untuk menangani streaming data real-time.
4. **Pertimbangkan Implementasi Arsitektur Skalabel dengan Integrasi Cloud**
    - Ini memungkinkan peningkatan sumber daya yang mudah berdasarkan permintaan dan memberikan efisiensi biaya.
    - Contoh penyedia awan yang dapat digunakan adalah AWS, Azure, atau GCP.

Rekomendasi ini bertujuan untuk meningkatkan efisiensi dan kualitas dalam proyek mendatang. Pastikan untuk mempertimbangkan dengan cermat setiap saran ini dalam perencanaan proyek.

Terima kasih!
