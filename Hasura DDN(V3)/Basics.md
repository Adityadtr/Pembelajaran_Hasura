# Overview

**Hasura DDN** menghubungkan sumber data Anda ke Hasura Engine dengan lancar menggunakan standar metadata yang fleksibel dan konsep yang disebut konektor data asli(native data connectors).

Dengan Hasura DDN, Anda dapat dengan mudah menghubungkan dan menggabungkan data dari semua sumber, sehingga dapat memecah data silos (kumpulan data yang dimiliki oleh satu kelompok yang tidak mudah atau sepenuhnya dapat diakses oleh kelompok lain dalam organisasi yang sama).

Beberapa fitur utama dari **Hasura DDN** termasuk:

- Visibilitas yang Jelas (clear visibility): mendapatkan pemahaman yang lebih baik tentang kueri yang dijalankan.
- Kontrol Keamanan yang Kuat (Strong Security Controls): Memberikan kontrol keamanan untuk melindungi data.
- Sistem yang Andal dan Tahan Lama (reliable and resilient system): Memastikan keandalan dan ketahanan sistem dalam pengoperasian.
- Fleksibilitas untuk Skala (Flexibility to Scale): Dapat diskalakan sesuai kebutuhan
- Alat CI/CD yang Kuat (Powerful CI/CD Tools): Meningkatkan alur kerja pengembangan dengan alat CI/CD yang Kuat
- Optimasi Kinerja dengan Native Queries (optimize performance with native queries): optimasi kinerja dengan penggunaan kueri asli, menjaga keamanan data dan logika bisnis tetap terpusat.

# Background

**A. Mengapa Hasura DDN Dibangun?**

  Hasura DDN dibangun untuk mengatasi hambatan dalam pengembangan aplikasi modern, seperti:

- Pengembangan produk yang lambat
- Federasi sumber data yang sulit
- Sprawl mikroservis yang tidak terkelola. (penyebaran layanan mikro yang tidak terkendali.)
- Kendala kolaborasi dan tata kelola
- Keamanan yang kompleks  
- Skalabilitas yang sulit dicapai
- Kendala kolaborasi dan tata kelola
- Pengamatan kueri yang tidak jelas.

Hasura DDN menggunakan arsitektur data supergraph yang meningkatkan produktivitas pengembang dan tim.

**B. Untuk Penulis API (For API Authors)**

Manfaat utama untuk pengembang API meliputi:

- Pemodelan domain data yang fleksibel
- Kemudahan integrasi berbagai sumber data
- Izin dan keamanan yang mudah diterapkan
- Pengalaman Pengembang (DX) yang lebih cepat dengan alat-alat produktif
- Fleksibilitas pemilihan bahasa pemrograman

**C. Untuk Pemelihara API (For API Maintainers)**

Pemeliharaan API menjadi lebih mudah dengan:

- Kinerja dan efisiensi operasional yang lebih baik
- Peluncuran tanpa downtime dan perubahan yang aman
- CI/CD yang terdistribusi untuk independensi tim
- Skalabilitas global dengan topologi edge
- Onboarding cepat untuk pengembang dan penemuan domain

**D. Untuk Konsumen API (For API Consumers)**

Bagi konsumen API, Hasura DDN memberikan:

- Keandalan: API yang stabil dan terdokumentasi dengan baik
- Konsistensi: API yang tetap seragam terlepas dari sumber data
- Kemudahan penemuan: Memungkinkan pengguna untuk dengan mudah menemukan dan mencoba API

**E. Apa itu Hasura DDN?**

Hasura DDN adalah pendekatan baru dalam pembuatan dan pengelolaan API, memungkinkan penyebaran API yang lebih cepat, fleksibel, dan skalabel. Hasura DDN mendukung pengembangan mikroservis yang lebih cepat dan efisien dengan terhubung ke berbagai sumber data.

# Core Concepts

**A. Core Concepts**

Dalam pengembangan aplikasi modern, lapisan data semakin kompleks karena terdiri dari berbagai database, layanan, dan API. Hasura DDN memperkenalkan konsep data supergraph untuk membantu mengelola kompleksitas ini dalam menghubungkan berbagai sumber data.

**B. Keadaan Lapisan Data**

Contoh tim dalam sebuah perusahaan hipotetis yang menggunakan berbagai teknologi untuk kebutuhan yang berbeda:

- Tim Manajemen Produk: Mengelola basis data relasional (PostgreSQL) untuk katalog produk dan inventaris.
- Tim Pengalaman Pengguna(UX): Menyimpan data pengguna di MongoDB dan mengelola privasi data.
- Tim Optimasi Pencarian: Menggunakan Algolia untuk meningkatkan hasil pencarian produk.
- Tim Keuangan dan Transaksi: Mengintegrasikan Stripe untuk pembayaran dan menjaga keamanan transaksi.
- Tim Logistik dan Pengiriman: Mengelola pengiriman melalui layanan ShipStation.
- Tim Data Science dan Rekomendasi: Menggunakan basis data vektor Weaviate untuk personalisasi rekomendasi produk.
  
Masing-masing tim menggunakan API, skema, dan layanan yang berbeda, yang menciptakan tantangan dalam pengelolaan dan integrasi data.

**C. Subgraph**

Setiap layanan dalam aplikasi e-commerce mewakili sebuah subgraph. 

Subgraph adalah entitas mandiri yang mencakup semua metadata dan dapat diintegrasikan dalam API secara terpisah. 

Pengembang dapat membangun API yang terdiri dari berbagai sumber data secara deklaratif, dengan aturan kontrol akses, otentikasi, dan logika bisnis yang berbeda untuk setiap subgraph.

**D. Cara Membangun Subgraph**

Subgraph dibangun dari sumber data yang terkait, seperti database tradisional atau logika bisnis khusus. 

Hasura DDN menggunakan data connectors yang terhubung dengan berbagai layanan dan database populer. Anda juga bisa menambahkan logika bisnis menggunakan fungsi TypeScript melalui API GraphQL. Metadata untuk subgraph dapat ditulis menggunakan Hasura CLI dan ekstensi VS Code.

**E. Supergraph**

Supergraph adalah kerangka kerja yang menggabungkan semua subgraph menjadi satu API yang aman dan terpadu. 

Ini memungkinkan aplikasi untuk mengakses berbagai sumber data dan layanan dengan satu API holistik, memudahkan pengelolaan dan pemeliharaan lapisan data, serta memungkinkan pipeline CI/CD dan observabilitas yang lebih baik.

**F. Cara Membangun Supergraph**

Supergraph dibuat otomatis ketika Anda menambahkan subgraph ke dalam proyek Hasura. Anda dapat mendefinisikan hubungan antara sumber data dan menerapkan kontrol akses yang mendetail untuk menghubungkan berbagai sumber data secara logis sesuai kebutuhan aplikasi Anda.

# Before Hasura DDN

Sebelum adanya Hasura Data Delivery Network (DDN), perusahaan yang sedang melakukan modernisasi menghadapi tantangan dalam menyajikan pengalaman digital secara cepat dan hemat biaya. Tim pengembangan produk sering kali terhambat karena harus menunggu tim backend untuk menyediakan akses data yang aman dan efisien. Akibatnya, banyak waktu dan upaya dihabiskan untuk:

- Implementasi API Kustom Secara Manual: Tim pengembangan membutuhkan lebih banyak waktu dan sumber daya untuk membangun API sendiri untuk berbagai sumber data.
- Penyebaran Berlebih Microservices: Karena banyaknya microservices yang harus diatur dan dihubungkan, manajemen dan orkestrasi menjadi sangat sulit.
- Orkestrasi Kebijakan Keamanan: Setiap microservice dan API harus diatur dengan kebijakan keamanan yang spesifik, yang menyulitkan integrasi antar layanan.
- Waktu Terbuang dan Inovasi Terhambat: Waktu yang seharusnya digunakan untuk inovasi produk malah terbuang untuk menyelesaikan masalah teknis dalam pengelolaan dan akses data.

![image](https://github.com/user-attachments/assets/5fa2c308-0376-491e-90e5-30588a19ed21)

## Penjelasan Gambar

- Lapisan Aplikasi

Terdiri dari berbagai aplikasi: Client Apps (web, mobile, desktop), Public APIs, dan Internal Apps. Semua aplikasi ini membutuhkan akses ke backend yang berisi produk API/microservices untuk mengambil data dan menjalankan logika bisnis. Setiap aplikasi bergantung pada API dan microservices yang terhubung ke sumber data.

- Product API/Microservice

Ini adalah lapisan yang menangani akses aplikasi ke data. Setiap API produk menghubungkan aplikasi ke microservice di bawahnya, yang secara khusus menangani permintaan data dan logika bisnis.

- Data API/Microservice

Berfungsi sebagai lapisan yang menghubungkan microservices produk dengan sumber data. Microservices ini berperan dalam pengaturan data, kebijakan keamanan, dan pengambilan data dari sumber yang relevan.

- Data Source (Sumber Data)

Ini adalah lapisan terakhir, yang menyimpan data yang digunakan oleh seluruh sistem. Setiap data source bisa berupa database, layanan cloud, atau penyimpanan data lainnya.
