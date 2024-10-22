# Business Logic

- Business logic pada Hasura DDN (Data Delivery Network) berperan penting dalam mengatur aturan dan proses yang diterapkan pada data sebelum data tersebut dikonsumsi oleh klien melalui API GraphQL.
- Dengan mengintegrasikan logika bisnis secara langsung di layer data, Hasura DDN memungkinkan pengembang untuk mengontrol dan memproses data sesuai dengan kebutuhan spesifik aplikasi, seperti validasi, transformasi, dan automasi tugas-tugas tertentu.

Hasura DDN mendukung berbagai cara untuk menerapkan logika bisnis, baik melalui penggunaan event triggers, actions, ataupun remote schemas. 

# Komponen Business Logic

#### Action

Actions adalah salah satu fitur penting Hasura yang memungkinkan developer mendefinisikan fungsi kustom atau logika bisnis yang tidak didukung secara native oleh database. Dengan actions, Anda dapat membuat endpoint GraphQL khusus (kustom) untuk kebutuhan tertentu yang mengintegrasikan logika bisnis spesifik.

- Query Actions: Endpoint ini digunakan untuk mengambil data yang sudah diproses oleh logika bisnis dari API atau layanan eksternal. 
- Mutation Actions: Endpoint ini memungkinkan Anda untuk memodifikasi data di database sambil menjalankan logika bisnis, seperti validasi, pengecekan izin, atau melakukan proses tambahan sebelum perubahan data diterapkan.

#### Event Triggers

Event triggers memungkinkan Hasura untuk merespon terhadap perubahan data di database. Ketika ada operasi insert, update, atau delete, Hasura dapat mengaktifkan event trigger yang memicu fungsi atau layanan eksternal untuk menjalankan logika bisnis tertentu.

Fitur ini cocok untuk:

- Menjalankan validasi atau persyaratan bisnis saat data diubah.
- Menyinkronkan data dengan sistem atau layanan eksternal.
- Memicu notifikasi atau automasi lainnya.
  
#### Remote Schemas

Remote schemas memungkinkan Anda untuk menggabungkan API GraphQL eksternal ke dalam API Hasura. Ini membuat Hasura dapat memproses dan mengelola data dari berbagai sumber API yang telah menerapkan logika bisnis mereka sendiri.

#### Custom Functions

Hasura juga mendukung fungsi SQL kustom yang dapat digunakan untuk menjalankan logika bisnis di tingkat database. Fungsi ini bisa dipanggil langsung dari GraphQL API, memungkinkan developer untuk menjalankan logika kompleks seperti agregasi data, kalkulasi, atau operasi data lainnya.

#### Role-based Access Control (RBAC)

RBAC adalah sistem kontrol akses berbasis peran yang memungkinkan Anda menerapkan logika bisnis terkait dengan izin dan otorisasi pengguna. Dengan RBAC, Anda bisa menentukan siapa yang dapat mengakses, membaca, menulis, atau memodifikasi data berdasarkan peran atau status mereka dalam sistem.

# Custom Business Logic Hasura V2

![image](https://github.com/user-attachments/assets/25c88118-b2de-4aff-aac5-d723f8449902)

Gambar tersebut menjelaskan bagaimana Hasura mengimplementasikan **Custom Business Logic** melalui mekanisme **Actions** pada versi 2.

1. **App (Aplikasi)**:
   - Aplikasi pengguna mengirimkan request melalui GraphQL ke Hasura.
   
2. **GraphQL (Hasura Gateway)**:
   - Hasura bertindak sebagai API Gateway yang menerima permintaan GraphQL dari aplikasi. Ini adalah bagian yang menghubungkan aplikasi dengan Hasura, di mana semua interaksi dilakukan dengan menggunakan query atau mutation GraphQL.

3. **Hasura (Actions)**:
   - Pada bagian **Actions**, Hasura memungkinkan Anda untuk memperluas fungsionalitas yang ada dengan menambahkan custom logic. Alih-alih hanya melakukan operasi CRUD sederhana ke database, Actions memungkinkan Anda menghubungkan request ke **HTTP endpoint** yang menjalankan logika bisnis spesifik. 
   
4. **HTTP Endpoint**:
   - Di sini, Anda dapat menjalankan **Custom Business Logic**, yang meliputi:
     - **Data Validation**: Validasi data dari klien untuk memastikan bahwa data yang dikirimkan valid sebelum diproses lebih lanjut.
     - **Data Enrichment and Transformation**: Melakukan pemrosesan tambahan pada data, seperti pengayaan (enrichment) atau transformasi sebelum data disimpan ke database atau diteruskan ke layanan lain.
     
5. **Postgres Database**:
   - Setelah melalui Hasura, aplikasi dapat melakukan operasi **CRUD** (Create, Read, Update, Delete) pada data di PostgreSQL, dan operasi ini juga mendukung fitur real-time dengan kontrol akses (RBAC). Ini artinya, Hasura memastikan bahwa hanya pengguna yang berwenang yang dapat menjalankan tindakan tertentu berdasarkan peran mereka dalam sistem.

#### Alur Kerja Singkat:
1. Aplikasi mengirim permintaan GraphQL ke Hasura.
2. Hasura memeriksa apakah permintaan tersebut melibatkan custom logic atau operasi langsung ke database.
3. Jika ada custom logic, Hasura meneruskan permintaan ke HTTP endpoint yang menjalankan logika bisnis, seperti validasi dan transformasi data.
4. Setelah logika bisnis diproses, data dapat diteruskan kembali ke Hasura dan kemudian diproses ke database PostgreSQL, dengan akses kontrol yang diterapkan.

# Custom Business Logic Hasura V3

![image](https://github.com/user-attachments/assets/03340442-dcb2-4ef7-888d-082820cb3a89)

Gambar ini menggambarkan arsitektur **Hasura DDN (Data Delivery Network)** yang berinteraksi dengan **business logic** dan database.

#### Penjelasan Elemen-elemen pada Gambar:

1. **Business Logic**:
   - Bagian yang ditunjukkan oleh ikon roda gigi (gear) ini menunjukkan bahwa ada **logika bisnis** yang dijalankan secara khusus. Logika bisnis ini mencakup aturan dan pemrosesan data yang biasanya disesuaikan berdasarkan kebutuhan aplikasi. 
   - **Business logic** ini bisa diimplementasikan sebagai layanan eksternal (misalnya microservices) atau fungsi tertentu yang dieksekusi dalam arsitektur.

2. **Hasura DDN (Data Delivery Network)**:
   - Hasura DDN bertindak sebagai penghubung antara logika bisnis dan berbagai sumber data. Hasura memproses permintaan dan meneruskan query ke sumber data yang sesuai.
   - DDN mengelola **federasi** data, yaitu cara mengakses beberapa database atau data source yang berbeda secara terkoordinasi. Dengan ini, pengembang dapat menggabungkan beberapa data source ke dalam satu API GraphQL.
   
3. **Databases (Postgres dan lainnya)**:
   - Hasura terhubung ke berbagai database di bagian ini. Bisa saja melibatkan PostgreSQL atau database lain yang mendukung arsitektur Hasura.
   - Hasura berfungsi untuk mengambil, memodifikasi, atau mengirimkan data ke database tersebut berdasarkan request yang dikirimkan oleh aplikasi pengguna atau melalui logika bisnis.

4. **Aplikasi atau Klien**:
   - Ini menunjukkan perangkat pengguna (ikon komputer di bawah) yang melakukan permintaan data ke Hasura. Permintaan ini bisa datang dari aplikasi web, mobile, atau bahkan aplikasi desktop yang menggunakan API GraphQL.

### Alur Kerja Singkat:
1. **Aplikasi** mengirimkan permintaan data melalui Hasura DDN.
2. **Hasura DDN** memproses permintaan dan mengirimkan request ke logika bisnis yang telah ditentukan.
3. **Logika bisnis** memproses data sesuai dengan kebutuhan, seperti melakukan validasi atau pengayaan data.
4. Hasil dari logika bisnis dikirim kembali ke **Hasura DDN**, yang kemudian meneruskannya ke database untuk mengambil, menyimpan, atau memodifikasi data.
5. Data dari database dikembalikan ke **Hasura**, yang kemudian dikirimkan kembali ke aplikasi atau klien.
