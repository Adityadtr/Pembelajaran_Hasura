# Hasura

Hasura adalah platform yang memungkinkan untuk membuat GraphQL API secara otomatis dari database relasional seperti PostgreSQL. Dengan Hasura, bisa dengan cepat dan mudah mengakses data dari database menggunakan GraphQL, yang merupakan query language untuk API. Hasura mengotomatiskan pembuatan GraphQL API dan mengelola alur kerja backend, sehingga pengembang dapat fokus pada logika bisnis daripada mengelola API secara manual.

Hasura dikenal karena kemampuannya untuk menghasilkan GraphQL API secara otomatis berdasarkan skema database yang ada. Ini sangat berguna untuk membangun aplikasi dengan stack modern di mana GraphQL digunakan untuk berkomunikasi antara frontend dan backend

Hasura juga menyediakan fitur seperti:

Real-time Queries: Mendukung subscription GraphQL yang memungkinkan pembaruan real-time.

Authorization Rules: Memungkinkan Anda untuk mengatur aturan akses data yang ketat berdasarkan user roles.

Integrasi yang Mudah: Mudah diintegrasikan dengan alat-alat lain seperti server authentication atau event triggers.

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


