# Hasura

Hasura adalah platform yang memungkinkan untuk membuat GraphQL API secara otomatis dari database relasional seperti PostgreSQL. Dengan Hasura, bisa dengan cepat dan mudah mengakses data dari database menggunakan GraphQL, yang merupakan query language untuk API. Hasura mengotomatiskan pembuatan GraphQL API dan mengelola alur kerja backend, sehingga pengembang dapat fokus pada logika bisnis daripada mengelola API secara manual.

Hasura dikenal karena kemampuannya untuk menghasilkan GraphQL API secara otomatis berdasarkan skema database yang ada. Ini sangat berguna untuk membangun aplikasi dengan stack modern di mana GraphQL digunakan untuk berkomunikasi antara frontend dan backend

# Fitur Utama dalam Hasura

1. Real-time GraphQL API:

Hasura menyediakan API GraphQL secara real-time, yang berarti klien dapat menerima pembaruan langsung dari server saat data diubah. Ini sangat berguna untuk aplikasi seperti obrolan, dasbor, atau sistem notifikasi yang memerlukan data terbaru secara real-time.

2. Auto-generated API:

Hasura secara otomatis menghasilkan API GraphQL berdasarkan skema database. Ini berarti tidak perlu menulis kode untuk endpoint API, karena Hasura langsung membuatnya.

3. Role-based Access Control (RBAC):

Hasura dilengkapi dengan sistem kontrol akses berbasis peran (RBAC), yang memungkinkan untuk mengatur izin akses data dengan detail yang tinggi, baik itu berdasarkan pengguna, peran, atau kondisi tertentu.

4. Event Triggers:

Fitur ini memungkinkan untuk mengeksekusi fungsi atau layanan eksternal (seperti serverless functions) ketika terjadi perubahan data pada database. Misalnya, bisa dalam memicu fungsi setelah sebuah catatan ditambahkan, diubah, atau dihapus dari tabel tertentu.

5. Remote Schemas & REST Endpoints:

menggabungkan skema GraphQL dari layanan lain atau membuat endpoint REST dari query GraphQL yang sudah ada, sehingga memungkinkan integrasi yang lebih mudah dengan API eksternal.

# Keunggulan Hasura

1. Kecepatan Pengembangan:

Hasura mengurangi waktu pengembangan secara signifikan dengan menyediakan API yang siap digunakan berdasarkan database yang ada.

2. Real-time Capabilities:

Salah satu keunggulan utama Hasura adalah dukungan untuk real-time melalui subscriptions di GraphQL. Ini memungkinkan aplikasi untuk menerima pembaruan langsung dari server tanpa perlu terus-menerus melakukan polling.

3. Scalability:

Hasura dirancang untuk skalabilitas tinggi. Dengan Hasura, bisa dapat mengatur sistem distribusi data yang kompleks dengan mudah dan mendukung beban kerja yang besar tanpa mempengaruhi kinerja.

4. Security:

Dengan fitur RBAC dan integrasi dengan sistem autentikasi yang ada, Hasura menawarkan kontrol keamanan yang kuat untuk mengatur siapa yang bisa mengakses data tertentu. Ini memastikan bahwa aplikasi tetap aman dan sesuai dengan kebijakan akses data.

5. Extensibility:

Hasura bisa diintegrasikan dengan berbagai layanan dan alat lain melalui remote schemas, event triggers, dan webhooks. Ini memungkinkan untuk memperluas fungsionalitas Hasura sesuai dengan kebutuhan aplikasi.

6. Open-source dan Komunitas yang Kuat:

Hasura adalah proyek open-source dengan komunitas pengguna dan pengembang yang aktif. Ini berarti dapat mendapatkan dukungan dari komunitas, serta berkontribusi pada pengembangan fitur baru.

# Docker Compose 

Docker Compose adalah alat yang digunakan untuk mendefinisikan dan menjalankan aplikasi yang terdiri dari beberapa container Docker. Docker Compose memungkinkan digunakan untuk mengelola dan menjalankan semua container yang dibutuhkan oleh aplikasi  dengan menggunakan satu file konfigurasi, yang disebut docker-compose.yml.

Dengan Docker Compose, dapat mengatur layanan, jaringan, dan volume untuk aplikasi dengan cara yang mudah dan efisien, tanpa perlu menjalankan perintah Docker secara manual untuk setiap container. Docker Compose sangat berguna dalam pengembangan, pengujian, dan penyebaran aplikasi yang kompleks.

Komponen Utama Docker Compose:

docker-compose.yml File: File konfigurasi ini berisi definisi semua container yang diperlukan untuk menjalankan aplikasi. di file tersebut bisa dapat mendefinisikan image Docker, environment variables, port yang perlu dipetakan,dan lainnya.

Services: Dalam konteks Docker Compose, sebuah "service" mengacu pada container Docker yang didefinisikan di dalam file docker-compose.yml.

Networks: Docker Compose mengelola jaringan antar-container untuk memungkinkan komunikasi antar-container.

Volumes: Docker Compose juga mendukung volume yang memungkinkan untuk menyimpan data di luar container, sehingga data tetap ada meskipun container dihentikan atau dihapus.

# Penginstalan Hasura dengan Memakai Docker

Langkah 1: Instalasi Docker Compose

Docker Compose adalah alat untuk mendefinisikan dan menjalankan aplikasi multi-container. dapat menginstalnya dengan perintah:

```
sudo mkdir -p /usr/local/lib/docker/cli-plugins

sudo curl -SL https://github.com/docker/compose/releases/download/v2.29.1/docker-compose-linux-x86_64 -o /usr/local/lib/docker/cli-plugins/docker-compose
```
Perintah sudo mkdir -p /usr/local/lib/docker/cli-plugins:

Perintah ini membuat direktori /usr/local/lib/docker/cli-plugins jika belum ada. -p berarti jika direktori induk tidak ada, perintah ini akan membuatnya juga.

Tujuan: Docker Compose akan diunduh dan ditempatkan di direktori ini, dan Docker CLI akan mencari plugin di lokasi ini.

Perintah sudo curl -SL https://github.com/docker/compose/releases/download/v2.29.1/docker-compose-linux-x86_64 -o /usr/local/lib/docker/cli-plugins/docker-compose:

Perintah ini mengunduh file Docker Compose dari URL yang ditentukan dan menyimpannya di lokasi /usr/local/lib/docker/cli-plugins/docker-compose.

Hasil Outputnya :

![image](https://github.com/user-attachments/assets/7cf7390b-06ab-4feb-95cd-924e47277e02)

Langkah 2: Memberikan Izin Eksekusi (Jika diperlukan)

Terapkan izin yang dapat dieksekusi ke biner:

```
sudo chmod +x /usr/local/lib/docker/cli-plugins/docker-compose
```
Perintah ini memberikan izin eksekusi pada file Docker Compose yang baru diunduh.

Tujuan: Memastikan file Docker Compose dapat dijalankan sebagai program oleh sistem operasi.

Langkah 3: Verifikasi Instalasi

Setelah instalasi selesai, pastikan Docker Compose terinstal dengan benar, dengan perintah:

```
docker-compose --version
```
atau

```
docker compose version
```
Perintah ini akan menampilkan versi Docker Compose yang terinstal di sistem.

Hasil Output :

![image](https://github.com/user-attachments/assets/662949b0-6c4f-46dd-a58d-cdc42ac60852)

Langkah 4: Unduh dan Edit File `docker-compose.yaml`

Kemudian, menyiapkan file konfigurasi Docker Compose untuk mengatur Hasura dan PostgreSQL.

1. Unduh File `docker-compose.yaml`:

Mengunduh file docker-compose.yaml dari repository resmi Hasura, dengan menggunakan perintah :

```
wget https://raw.githubusercontent.com/hasura/graphql-engine/stable/install-manifests/docker-compose/docker-compose.yaml
```
File ini berisi konfigurasi untuk menjalankan Hasura dan PostgreSQL sebagai layanan yang terpisah di dalam container.

Hasil Output:

![image](https://github.com/user-attachments/assets/ee085bd5-c832-4bfb-a5a9-ee89fd9dafb6)

2. Periksa File `docker-compose.yaml`:

Lihat isi file docker-compose.yaml untuk memastikan konfigurasinya:

```
cat docker-compose.yaml
```
Hasil Output:

![image](https://github.com/user-attachments/assets/0fa66882-b8e8-498a-a915-f8ab9e2f571e)

3. Edit File `docker-compose.yaml`:

Untuk mengedit atau menambahkan konfigurasi yang diperlukan dapat membuka file `docker-compose.yaml` dan mengeditnya

Sebagai Contoh, saya ingin mengganti HASURA_GRAPHQL_ADMIN_SECRET keynya yang tadinya myadminsecretkey menjadi `newsecreatkey`, dengan menggunakan perintah:

```
nano docker-compose.yaml
```

Hasil Output:

![image](https://github.com/user-attachments/assets/712e451b-a9c4-44c1-9e83-6725b2a77cb7)

Langkah 4: Jalankan Docker Compose

untuk menjalankan Docker Compose, yang akan memulai semua layanan yang didefinisikan dalam file docker-compose.yaml,Gunakan perintah berikut :

```
sudo docker-compose up -d
```
atau

```
docker compose up -d
```

`-d` berarti layanan akan berjalan di background.

Hasil outputnya:

![image](https://github.com/user-attachments/assets/87e886a4-5c27-45fa-aa25-995372271242)


Langkah 5: Akses Hasura Console

Buka browser dan akses http://192.168.1.9:8080/console/ untuk membuka antarmuka pengguna Hasura.

Akan diminta memasukkan HASURA_GRAPHQL_ADMIN_SECRET. Masukkan kunci rahasia yang telah di pilih.

Hasil Outputnya:

![image](https://github.com/user-attachments/assets/a983462c-21af-45d6-b9e3-857e84fde069)

Tampilan berhasil masuk console hasura:

![image](https://github.com/user-attachments/assets/f1c69c41-6099-4071-ad03-e9daa0ce093d)

# Connect Database MySql dan Mariadb

Untuk menghubungkan hasura ke database mariadb dan MySql, 

langkah 1: diperlukan adalah membuat instance mariadb dan MySql. Dapat dilakukan menggunakan Docker untuk membuat container dari image Mariadb dan MySq, seperti contoh yang saya buat dibawah ini dengan mengisi di file docker-compose.yaml: 

```
version: '3.8'
services:
  mariadb:
    image: mariadb:latest
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: pw123
      MYSQL_DATABASE: adityadutar
      MYSQL_USER: adityadutar
      MYSQL_PASSWORD: adityadutar
      MYSQL_AUTHENTICATION_PLUGIN: mysql_native_password
    ports:
      - "3307:3306"

  mysql:
    image: mysql:latest
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: pw123
      MYSQL_DATABASE: adityadutar
      MYSQL_USER: adityadutar
      MYSQL_PASSWORD: adityadutar
      MYSQL_AUTHENTICATION_PLUGIN: mysql_native_password
    ports:
      - "3306:3306"
```
version: '3.8' : Menggunakan versi 3.8 dari Docker Compose, yang mendukung fitur-fitur terbaru.

Services: Bagian ini mendefinisikan dua layanan (services) yang akan berjalan dalam container: mariadb dan mysql.

Image: Menggunakan image versi terbaru dari MariaDB dan MySQL dari Docker Hub (mariadb:latest dan mysql:latest).

Restart: Dikonfigurasi untuk selalu restart (restart: always) agar tetap berjalan meskipun terjadi kegagalan atau jika Docker di-restart.

Environment Variables:

MYSQL_ROOT_PASSWORD: Password untuk user root (pw123).

MYSQL_DATABASE: Nama database yang akan dibuat secara otomatis (adityadutar).

MYSQL_USER: User tambahan yang akan dibuat (adityadutar).

MYSQL_PASSWORD: Password untuk user tambahan (adityadutar).

MYSQL_AUTHENTICATION_PLUGIN: Plugin autentikasi yang digunakan (mysql_native_password) untuk kompatibilitas yang lebih baik.

Ports:

MariaDB memetakan port 3307 di host ke port 3306 di container, sedangkan MySQL menggunakan port 3306 baik di host maupun di container. Ini memungkinkan kedua layanan berjalan bersamaan tanpa konflik port.

Langkah 2: Jalankan Kembali Container

Jalankan docker-compose.yaml dengan perintah :

```
sudo docker compose up -d
```
Hasi Output :

![image](https://github.com/user-attachments/assets/a540e5ab-90ca-47c5-bd38-44dc1a601d89)

Jika terjadi warning seperti di hasil output itu dikarenakan versi tertentu dari Docker Compose, atribut version di dalam file docker-compose.yml dianggap sudah tidak diperlukan lagi dan menjadi usang (obsolete). Docker Compose secara otomatis mengatur versi yang diperlukan untuk menjalankan konfigurasi tanpa perlu mencantumkan atribut version.

Untuk memperbaikinya : bisa dengan  menghapus atribut version dari file docker-compose.yml. Setelah dihapus, Docker Compose akan tetap berfungsi dengan baik dan tidak akan menampilkan peringatan tersebut lagi.

Langkah 3: Melihat kembali isi docker-compose.yaml 

Lihatlah kembali isi docker-compose.yaml apakah perubahan sudah tersimpan, dapat melakukan dengan perintah : 

```
cat docker-compose.yaml
```
Hasil Output:

![image](https://github.com/user-attachments/assets/60535409-654b-49ef-b709-0071b43aab92)

Langkah 4 : Pastikan Container Berjalan

Pastikan kembali apakah container sedang berjalan, dengan melakukan perintah : 

```
sudo docker ps -a
```
Hasil Output:

![image](https://github.com/user-attachments/assets/7b296e02-6f55-4318-8531-820fdb206396)

Langkah 5: Connect Database di Console Hasura

Sebelum Masuk kedalam console hasura, lakukan restart image hasura di docker, dengan perintah :

```
sudo docker restart dutar-graphql-engine-1
```
Kemudian masuk kedalam hasura console, untuk mengconnect database mysql dan mariadb, dengan langkah :

1. Dalam console hasura, klik `data` tab
2. Connect postgres,
3. Connect database mysql dan mariadb terlebih dahulu
4. Kemudian masukkan nama tampilan untuk database dan atur URL Koneksi JDBC untuk MySQL
5. Untuk dasar JDBC Mysql: jdbc:mysql://<hostname>:<port>/<database name>?user=<username>&password=<password>
6. Untuk Dasar JDBC Mariadb: jdbc:mariadb://<hostname>:<port>/<database name>?user=<username>&password=<password>
7. Masukkan JDBC Mariadb: jdbc:mariadb://dutar-mysql-1:3306/adityadutar?user=adityadutar&password=adityadutar
8. Masukkan JDBC MySql: jdbc:mysql://dutar-mysql-1:3306/adityadutar?user=adityadutar&password=adityadutar
9. Kemudian Submit Connect
10. Tampilan Database di hasura sudah terlihat

Hasil Output : 

![image](https://github.com/user-attachments/assets/b0b1cdc0-37f6-4fdd-9f8c-ce2e61f764dc)

# Kesimpulan 

Hasura adalah platform open-source yang menyediakan layanan backend instan yang memungkinkan pengembang untuk membuat aplikasi yang kuat dengan cepat. Hasura menyediakan GraphQL engine yang otomatis menghasilkan API GraphQL berdasarkan skema database yang ada, memungkinkan pengembang untuk mengakses dan mengelola data dengan cara yang efisien dan terstruktur. Hasura adalah platform yang kuat untuk membangun backend aplikasi dengan cepat dan efisien

Sumber referensi : Dokumentasi Hasura.io, Dokumentasi Docker Resmi

