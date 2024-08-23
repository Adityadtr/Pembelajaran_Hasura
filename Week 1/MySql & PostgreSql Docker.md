# MySql

MySQL adalah sistem manajemen basis data relasional (RDBMS) yang populer, dikembangkan oleh Oracle. MySQL menggunakan SQL (Structured Query Language) sebagai bahasa untuk mengelola dan memanipulasi data dalam basis data. MySQL biasanya digunakan untuk aplikasi web dan merupakan komponen penting dalam tumpukan perangkat lunak seperti LAMP (Linux, Apache, MySQL, PHP/Python/Perl).

# apa itu Primary Key dan Foreign Key

Primary Key:

Primary Key adalah kolom atau sekelompok kolom dalam tabel yang digunakan untuk secara unik mengidentifikasi setiap baris dalam tabel tersebut. 

Misal kolom `id` adalah primary key, yang berarti setiap nilai di kolom id harus unik dan tidak boleh NULL. MySQL akan otomatis mengindeks kolom Primary Key untuk mempercepat proses pencarian dan memastikan keunikan setiap nilai.

Foreign Key:

Foreign Key adalah kolom atau sekelompok kolom dalam suatu tabel yang digunakan untuk membuat hubungan antara dua tabel. 

Kolom Foreign Key mengacu pada kolom Primary Key di tabel lain. Foreign Key digunakan untuk menjaga integritas referensial dalam database, yaitu memastikan bahwa nilai di kolom Foreign Key harus sesuai dengan nilai di kolom Primary Key di tabel yang dirujuk. Ini berguna untuk mempertahankan konsistensi data antar tabel yang berhubungan.

# Proses Instalasi MySql DAN Membuat Database di Docker 

Langkah 1: Pull Image MySql di Docker Hub

Ambil image MySql dari Docker Hub, denga perintah:

```
docker pull mysql:latest
```
Perintah ini akan mengunduh image MySQL versi terbaru dari Docker Hub. 

mysql adalah nama image, dan

latest menunjukkan versi terbaru.

Docker Hub:  

repositori online yang menyediakan berbagai image Docker yang siap digunakan. 

Anggap Seperti Toko, yang dapat menemukan dan mengambil (pull) berbagai aplikasi dan layanan dalam bentuk containerized, seperti MySQL, PostgreSQL, Nginx, Redis, dan banyak lagi. Docker Hub memudahkan pengembang untuk membagikan aplikasi mereka dengan menggunakan image yang dapat diunduh oleh siapa saja.

Langkah 2: Jalankan Container MySql 

Jalankan container MySQL dengan perintah berikut:

```
docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=mypw123 -d mysql:latest
```
`docker run`: Perintah untuk menjalankan container
.
`--name mysql-container`: Memberi nama container sebagai mysql-container.

`-e MYSQL_ROOT_PASSWORD=mypw123`: Mengatur password root MySQL. (Bisa Pakai password sendiri)

`-d`: Menjalankan container di background.

`mysql:latest`: Menentukan image yang digunakan, dalam hal ini mysql versi latest.

Langkah 3: Hubungkan ke Database dalam container

Untuk mengelola database, perlu terhubung ke shell database di dalam container.

```
docker exec -it mysql-container mysql -u root -p
```
`docker exec`: Perintah untuk menjalankan command di dalam container.

`-it`: Membuka sesi interaktif (interactive terminal).

`mysql-container`: Nama container yang ingin diakses.

`mysql -u root -p`: Perintah untuk masuk ke shell MySQL dengan user root

 Akan diminta memasukkan password, dan setelah berhasil, Akan masuk ke shell MySQL.

 Langkah 4 : Membuat Database Baru

 Disini saya akan membuat sample sederhana database, dengan membuat nama database nya my_biodata :

 ```
CREATE DATABASE my_biodata;
```
Membuat database bernama my_biodata di MySQL.

Langkah 5: Verifikasi Database

Memeriksa apakah database berhasil dibuat, dengan perintah:

```
SHOW DATABASES;
```
Langkah 6: Buat Tabel Database

Masuk kedalam database yang baru dibuat dan buat tabel baru:

```
USE my_biodata;
CREATE TABLE personal_data (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(100),
    jenis_kelamin VARCHAR(10),
    tanggal_lahir DATE,
    email VARCHAR(100)
);
```
Membuat tabel users dengan kolom id, nama, jenis_kelamin, tanggal_lahir dan email di MySQL.

Langkah 7: Masukkan Data Ke Tabel

Masukkan data ke dalam tabel yang baru dibuat.

```
INSERT INTO personal_data (nama, jenis_kelamin,tanggal_lahir, email) VALUES ('Ramadhan', 'Laki-Laki', '2002-11-24', 'adityadtr24@gmail.com');
INSERT INTO personal_data (nama, jenis_kelamin,tanggal_lahir, email) VALUES ('Sarah', 'Perempuan', '2000-09-24', 'sarahhh@gmail.com');
```
Langkah 8: Menampilkan Data dari Tabel:

```
SELECT * FROM personal_data;
```
Menampilkan semua data dalam tabel personal_data.

# Proses Instalasi PostgreSql DAN Membuat Database di Docker 

Langkah 1: Pull Image PostgreSql di Docker Hub

```
docker pull postgres:latest
```
perintah ini mengunduh image PostgreSQL versi terbaru dari Docker Hub.

Langkah 2: Jalankan Container PostgreSql

```
docker run --name postgres-container -e POSTGRES_PASSWORD=mypw123 -d postgres:latest
```
Docker akan memberikan ID container yang berjalan. dapat memverifikasi bahwa container sedang berjalan dengan menggunakan perintah `docker ps`.

Langkah 3: Hubungkan ke Database di dalam Container

```
docker exec -it postgres-container psql -U postgres
```
`docker exec`: Perintah untuk menjalankan command di dalam container.

`-it`: Membuka sesi interaktif (interactive terminal).

`postgres-container`: Nama container yang ingin diakses.

`psql -U postgres`: Perintah untuk masuk ke shell Postgres dalam container.

Langkah 4: Buat Database Baru

Setelah masuk ke shell database, dapat membuat database baru.

```
CREATE DATABASE my_biodata;
```
Membuat database bernama my_database di PostgreSQL.

Langkah 5: Verifikasi Database

```
\l
```
Menampilkan daftar database yang ada di PostgreSQL.

Langkah 6: Membuat Tabel di Database

Masuk ke database yang baru dibuat dan buat tabel baru.

```
\c my_biodata
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    nama VARCHAR(100),
    jenis_kelamin VARCHAR(10),
    tanggal_lahir DATE,
    email VARCHAR(100)
);
```
Langkah 7: Masukkan data ke tabel

Masukkan data ke dalam tabel yang baru dibuat.

```
INSERT INTO personal_data (nama, jenis_kelamin,tanggal_lahir, email) VALUES ('Ramadhan', 'Laki-Laki', '2002-11-24', 'adityadtr24@gmail.com');
INSERT INTO personal_data (nama, jenis_kelamin,tanggal_lahir, email) VALUES ('Sarah', 'Perempuan', '2000-09-24', 'sarahhh@gmail.com');
```
akan melihat pesan Query OK atau INSERT 0 1 yang menunjukkan bahwa data telah berhasil dimasukkan.

Langkah 8: Tampilkan data dari tabel

Periksa data yang telah dimasukkan ke dalam tabel.

```
SELECT * FROM personal_data;
```
akan melihat data yang telah dimasukkan

# Kesimpulan

MySQL sering dipilih karena kemudahan penggunaan, kecepatan untuk aplikasi baca-tulis ringan, dan popularitas di kalangan pengembang web.

PostgreSQL lebih cocok untuk aplikasi yang memerlukan operasi data yang kompleks, integritas data yang kuat, dan kemampuan untuk menangani beban kerja yang lebih berat dengan fitur yang kaya dan fleksibilitas tinggi.








