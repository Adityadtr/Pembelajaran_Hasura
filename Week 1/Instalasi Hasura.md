# Hasura

Hasura adalah platform yang memungkinkan untuk membuat GraphQL API secara otomatis dari database relasional seperti PostgreSQL. Dengan Hasura, bisa dengan cepat dan mudah mengakses data dari database menggunakan GraphQL, yang merupakan query language untuk API. Hasura mengotomatiskan pembuatan GraphQL API dan mengelola alur kerja backend, sehingga pengembang dapat fokus pada logika bisnis daripada mengelola API secara manual.

Hasura dikenal karena kemampuannya untuk menghasilkan GraphQL API secara otomatis berdasarkan skema database yang ada. Ini sangat berguna untuk membangun aplikasi dengan stack modern di mana GraphQL digunakan untuk berkomunikasi antara frontend dan backend

Hasura juga menyediakan fitur seperti:

Real-time Queries: Mendukung subscription GraphQL yang memungkinkan pembaruan real-time.

Authorization Rules: Memungkinkan Anda untuk mengatur aturan akses data yang ketat berdasarkan user roles.

Integrasi yang Mudah: Mudah diintegrasikan dengan alat-alat lain seperti server authentication atau event triggers.

# Penginstalan Hasura dengan Memakai Docker

Langkah 1: Menjalankan Container PostgreSql

Hasura membutuhkan database PostgreSQL untuk berfungsi. dengan menjalankan PostgreSQL di container Docker dengan perintah berikut:

```
docker run -d --name postgres \
-e POSTGRES_PASSWORD=mypw123 \
-p 5432:5432 postgres
```
-d: Menjalankan container di background (detached mode).

--name postgres: Memberi nama container PostgreSQL sebagai postgres.

-e POSTGRES_PASSWORD=mypw123: Mengatur password untuk user postgres di database PostgreSQL. dapat mengganti mypw123 dengan password yang Anda inginkan.

-p 5432:5432: Memetakan port 5432 di container ke port 5432 di host. Ini memungkinkan akses ke PostgreSQL dari luar container, seperti aplikasi lain atau alat pengelola database.

postgres: Nama image yang digunakan untuk menjalankan container.

Langkah 2: Mengunduh Image Hasura

```
docker pull hasura/graphql-engine:v2.0.10
```
docker pull hasura/graphql-engine:v2.0.10:

Mengunduh image Hasura GraphQL Engine dari Docker Hub. Versi v2.0.10 adalah contoh versi; bisa memilih versi lain jika diperlukan.

Langkah 3: Menjalankan Container Hasura

```
docker run -d --name hasura \
-p 8080:8080 \
-e HASURA_GRAPHQL_DATABASE_URL=postgres://postgres:mypw123@172.17.0.1:5432/postgres \
-e HASURA_GRAPHQL_ADMIN_SECRET=mysecret123 \
hasura/graphql-engine:v2.0.10
```
-d: Menjalankan container di background (detached mode).

--name hasura: Memberi nama container Hasura sebagai hasura.

-p 8080:8080: Memetakan port 8080 di container ke port 8080 di host. Ini memungkinkan akses ke Hasura dari luar container, seperti melalui browser.

-e: Menetapkan variabel lingkungan.

HASURA_GRAPHQL_DATABASE_URL: URL koneksi ke database PostgreSQL.

postgres://postgres:mypw123@postgres:5432/postgres: 

Format URL koneksi. dan postgres adalah nama container PostgreSQL yang digunakan sebagai hostname.

-e HASURA_GRAPHQL_ADMIN_SECRET=mysecret123:

HASURA_GRAPHQL_ADMIN_SECRET: Kunci rahasia admin untuk Hasura.

mysecret123: 

Gantilah dengan kunci rahasia yang Anda pilih untuk mengakses Hasura Console dan API.

hasura/graphql-engine:v2.0.10: Nama image Hasura yang digunakan untuk menjalankan container.

Langkah 4: Memverifikasi Instalasi

Buka browser dan akses http://localhost:8080 untuk membuka antarmuka pengguna Hasura.

Akan diminta memasukkan HASURA_GRAPHQL_ADMIN_SECRET. Masukkan kunci rahasia yang telah di pilih.

Langkah 5: Mengakses Hasura Console

Setelah membuka antarmuka pengguna Hasura di browser.

Dapat Membuat dan Mengelola Skema GraphQL: 

Menggunakan Hasura Console untuk membuat tabel, menyusun skema GraphQL, dan mengelola data.



