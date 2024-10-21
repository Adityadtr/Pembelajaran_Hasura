# Overview

Hasura memberikan fleksibilitas untuk mengotentikasi pengguna dengan berbagai layanan otentikasi populer atau solusi khusus yang di-hosting di tempat lain(secara terpisah).

Dengan menggunakan session variables yang dikirim melalui JWT (JSON Web Token) atau webhook dari layanan otentikasi, Anda dapat membuat aturan kontrol akses yang terperinci. Ini memungkinkan Anda untuk menentukan dengan tepat data apa yang dapat diakses oleh pengguna

# Authentication

**A. JWT**

   - Hasura DDN dapat dikonfigurasi untuk menggunakan JSON Web Tokens (JWTs) dalam proses otentikasi permintaan masuk.

   - Proses ini dimulai dengan layanan otentikasi yang mengembalikan JWT kepada klien. Klien kemudian mengirimkan token tersebut ke Hasura Engine melalui header dari permintaan.

   - Hasura akan memverifikasi dan mendekode JWT untuk mengekstrak nilai session variable yang dimulai dengan x-hasura-*, terutama x-hasura-role yang diperlukan untuk menentukan peran pengguna. Selain itu, informasi penting seperti   user id dan data lain yang relevan juga digunakan untuk mengatur akses terhadap data.

![image](https://github.com/user-attachments/assets/b7f0b0a0-5e0c-40a6-8f1f-982fbb8c49d7)

### Penjelasan Gambar

Gambar diatas tersebut menjelaskan bagaimana proses otentikasi menggunakan JWT dilakukan di Hasura, mulai dari aplikasi klien hingga permintaan ke sumber data. Berikut penjelasan langkahnya:

**1. Layanan Otentikasi (Authentication Service):**

   - Layanan otentikasi (misalnya, Firebase, Auth0, atau layanan kustom) mengeluarkan JWT yang berisi klaim dengan prefiks x-hasura-*.
   - Klaim ini diterbitkan ketika pengguna mendaftar, login, atau melakukan refresh token.
   - Klaim ini mencakup informasi seperti **x-hasura-role** yang menentukan peran pengguna.

**2. Aplikasi Klien (Client App):**

   - Setelah menerima JWT dari layanan otentikasi, aplikasi klien mengirimkan permintaan ke Hasura dengan menyertakan JWT di dalam **header** permintaan.
   - Permintaan ini berisi data yang akan diakses atau diolah.

**3. Hasura & Verifikasi JWT:**

   - Hasura menerima permintaan dengan JWT di dalam header.
   - Hasura kemudian melakukan proses **validasi dan decoding token** untuk mengekstrak variabel sesi (session variables) yang dihasilkan dari klaim JWT tersebut.
   - Variabel ini digunakan untuk mengatur aturan akses.
   - Misalnya, variabel **x-hasura-role** menentukan apakah pengguna memiliki akses tertentu, dan **x-hasura-user-id** digunakan untuk menentukan identitas pengguna.

**4. Aturan Akses & Permintaan Data (Permission Rules):**

   - Berdasarkan variabel sesi yang dihasilkan, Hasura menerapkan aturan berbasis peran **(role-based access control)** untuk menentukan data apa yang dapat diakses oleh pengguna.
   - Setelah itu, Hasura mengirimkan permintaan tunggal ke **sumber data** (data source) sesuai dengan hak akses yang diberikan berdasarkan peran pengguna.

**B. Webhook**

   - Hasura dapat dikonfigurasi untuk menggunakan mode webhook dalam melakukan otentikasi permintaan yang masuk. 
   - Dalam proses ini, Hasura memerlukan URL webhook yang ditentukan. Setiap kali ada permintaan yang masuk ke Hasura, Hasura akan memanggil URL tersebut dengan menyertakan header permintaan asli.
   - Webhook kemudian akan mengembalikan respons yang berisi informasi pengguna dalam bentuk variabel sesi (session variables). 
   - Informasi tersebut akan digunakan oleh Hasura untuk menentukan akses data yang sesuai berdasarkan aturan otentikasi dan otorisasi yang telah diatur.

![image](https://github.com/user-attachments/assets/8cb7eafb-39be-445b-8b81-91aef689e52c)

### Penjelasan Gambar

Gambar diatas tersebut menggambarkan alur otentikasi menggunakan webhook di Hasura, dan berikut dibawah ini untuk penjelasan setiap tahapnya:

**1. Permintaan dari Aplikasi Klien (Client App):** 

   - Aplikasi klien mengirim permintaan yang masuk ke Hasura dengan headers yang mengandung informasi seperti token otentikasi dan data lainnya.

**2. Headers Permintaan Dikirim ke Webhook:** 

   - Setelah permintaan diterima, Hasura meneruskan headers asli tersebut ke URL webhook yang sudah dikonfigurasi di sistem otentikasi. 
   - Webhook ini berfungsi untuk memvalidasi permintaan dan mengekstraksi informasi otentikasi yang dibutuhkan.

**3. Respon dari Webhook:** 

   - Webhook akan merespons dengan mengirimkan variabel sesi pengguna, termasuk informasi seperti peran (role) dan ID pengguna.
   - Contohnya, variabel sesi dapat berisi informasi seperti:
   - ``X-Hasura-Role = "customer"``
   - ``X-Hasura-User_ID = 3``

**4. Akses Terbatas Berdasarkan Role:** 

   - Berdasarkan informasi yang diterima dari webhook, Hasura akan memproses permintaan ke sumber data dengan kontrol akses yang dibatasi sesuai dengan peran pengguna.
   - Jadi, hanya data yang sesuai dengan peran pengguna yang dapat diakses.

# Authorization

Otorisasi di Hasura menentukan apa yang bisa diakses oleh pengguna yang telah diverifikasi, dan izin dapat ditetapkan pada berbagai tingkat dalam struktur data Anda.

Terdapat 3 jenis perizinan (permissions):

**1. Izin Tipe (Type Permissions):** Menentukan bidang mana dalam sebuah ObjectType yang dapat diakses oleh peran (role) tertentu.

**2. Izin Model (Model Permissions):** Menentukan baris mana dari sebuah Model yang dapat diakses oleh peran tertentu.

**3. Izin Perintah (Command Permissions):** Mengontrol apakah perintah tertentu dapat dijalankan oleh sebuah peran.

Peran (Roles) didefinisikan berdasarkan izin dalam salah satu dari tiga kategori ini. Setiap permintaan ke Hasura harus menyertakan variabel sesi atau peran dari sistem autentikasi Anda. Peran-peran ini menentukan izin apa yang akan diterapkan pada permintaan tersebut.

- Hasura tidak memiliki peran admin bawaan; izin dikelola langsung dengan mendefinisikan peran.
- Peran dan izin diimplementasikan pada lapisan Hasura Engine dan tidak berhubungan langsung dengan pengguna atau peran dari sumber data.
  
### Izin Pengujian

Anda dapat menguji perizinan (permission) menggunakan Hasura Console:

- Tentukan izin yang dibutuhkan untuk tipe, model, atau perintah tertentu.
- Gunakan antarmuka GraphiQL API di Hasura Console dengan token autentikasi yang mengandung variabel sesi.
- Verifikasi data yang dikembalikan untuk memastikan bahwa data tersebut sesuai dengan konfigurasi izin yang telah ditetapkan.



