# Install DDN CLI

### Unduh DDN CLI

- Membuka terminal atau VM ubuntu linux terlebih dahulu
- Kemudia jalankan perintah berikut dibawah ini, untuk mengunduh DDN CLI dari situs resmi Hasura (https://hasura.io/docs/3.0/getting-started/quickstart).
  
  ``curl -L https://graphql-engine-cdn.hasura.io/ddn/cli/v4/get.sh | bash``
  
![image](https://github.com/user-attachments/assets/936e92e6-a9c7-4262-9931-0b223342a88c)

Dalam gambar tersebut, terlihat proses instalasi DDN yang outputnya menunjukkan suatu tabel result dari criteria yang dimana docker available dan docker compose available belum terjalankan atau belum terinstall.

solusinya harus menginstall docker dan docker compose selanjutnya.

# Verifikasi Instalasi

Setelah menginstal DDN CLI, pastikan instalasi berhasil dengan menjalankan perintah berikut untuk melihat versi DDN CLI:

``ddn --version```

Jika instalasi berhasil, Anda akan melihat output berupa nomor versi DDN CLI yang terinstal.

![image](https://github.com/user-attachments/assets/7ee19248-5533-45b4-8842-991144e01d26)

# Install Docker

- Anda dapat menginstall docker dengan mengikuti panduan penginstalan di dokumentasi hasura atau di dokumentasi pembelajaran https://github.com/Adityadtr/Pembelajaran_Hasura/blob/main/Week%201/Instalasi%20Hasura.md.
- Kemudian, instalasi docker hingga selesai
- setelah instalasi docker sudah selesai, verifikasi penginstalan menggunakan perintah ``docker --version``. perintah tersebut akan menunjukkan versi docker yang terinstall

![image](https://github.com/user-attachments/assets/03c41c1c-c295-4ccc-bf06-d1fbd2ce0f77)

# Install Docker Compose

- Anda dapat menginstall docker-compose dengan mengikuti panduan penginstalan di dokumentasi hasura atau di dokumentasi pembelajaran https://github.com/Adityadtr/Pembelajaran_Hasura/blob/main/Week%201/Instalasi%20Hasura.md.
- Kemudian, instalasi docker-compose hingga selesai
- setelah instalasi docker-compose sudah selesai, verifikasi penginstalan menggunakan perintah ``docker compose version``. perintah tersebut akan menunjukkan versi docker yang terinstall

![image](https://github.com/user-attachments/assets/e54fd563-65a4-4c06-85d8-ae7550beb137)

# Verifikasi Kembali Penginstallan

Setelah berhasil menginstall DDN CLI, Docker dan Docker compose, verifikasi penginstalan kembali dengan menggunakan perintah

``ddn doctor``

![image](https://github.com/user-attachments/assets/225d399d-1e2c-4669-8c58-bacc0badf84b)

dalam gambar tersebut, menunjukkan bahwa criteria (DDN CLI, Docker dan Docker compose) telah terinstal atau telah dijalankan.

# Login untuk masuk Hasura DDN melalui CLI

Setelah DDN CLI berhasil diinstal, Anda perlu login atau melakukan autentikasi untuk menggunakan layanan Hasura DDN. Berikut adalah langkah-langkahnya.

#### **Langkah 1: Masuk dengan Perintah `ddn auth login`**

1. **Buka terminal atau VM** di Linux Anda.
2. Jalankan perintah berikut untuk memulai proses autentikasi:

   ```
   ddn auth login
   ```
   > Perintah ini akan mengarahkan Anda untuk melakukan login ke akun Hasura yang terkait dengan DDN CLI.

#### **Langkah 2: Ikuti Instruksi di Terminal**

1. **Setelah menjalankan perintah di atas**, terminal akan memberikan sebuah URL yang perlu Anda buka di browser. URL ini mengarahkan Anda ke halaman login Hasura untuk proses otorisasi.
   
   Contoh output di terminal:

   ```
   Please open the following URL in your browser to complete login:
   https://auth.hasura.io/cli/authorize?token=xxxx
   ```

2. **Salin URL** tersebut dan buka di browser Anda.

![image](https://github.com/user-attachments/assets/c9a894ad-0493-42ec-8072-15ff7adb136b)

#### **Langkah 3: Login di Halaman Hasura**

1. Setelah URL tersebut terbuka di browser, Anda akan diminta untuk **login menggunakan akun Hasura** Anda. Jika belum memiliki akun, Anda harus mendaftar terlebih dahulu.
   
2. Setelah login, Anda mungkin akan diminta untuk memberikan izin akses bagi DDN CLI. Klik **Authorize** atau **Allow** untuk melanjutkan proses autentikasi.

![image](https://github.com/user-attachments/assets/e0c1694d-13e1-43c2-8b9c-adf8dedc4201)

![image](https://github.com/user-attachments/assets/526eec0c-f0eb-45b0-86c2-2ad0aad59adc)

3. Jika terdapat kendala atau eror dalam login, seperti digambar bawah ini,

![image](https://github.com/user-attachments/assets/4e2c5630-ae65-48bd-871b-8c547d7fb16a)

dikarenakan ip nya tidak sesuai dengan ip address di hostname linux anda, jadi solusinya anda dapat mengubah ip di link tersebut dengan menyesuaikan ip address kalian.

contoh ip address saya 192.168.1.14 maka ip di link tersebut saya ubah dengan sesuai ip saya

![image](https://github.com/user-attachments/assets/cede342a-4d48-4c94-8f58-063037829cc5)

#### **Langkah 4: Kembali ke Terminal untuk Konfirmasi**

1. Setelah memberikan izin akses di browser, kembali ke terminal. DDN CLI akan otomatis menerima otorisasi dan menampilkan pesan yang mengonfirmasi bahwa Anda telah berhasil login.

   Contoh output konfirmasi di terminal:

   ```
   Successfully authenticated as [username].
   ```

   Ini menunjukkan bahwa Anda sekarang telah terautentikasi dan dapat mulai menggunakan perintah DDN CLI untuk mengelola proyek Hasura DDN Anda.

![image](https://github.com/user-attachments/assets/5c831891-edd5-4096-a5a6-a9071cb6dbfa)

# Inisialisasi Supergraf Baru di Direktori Baru

# Inisialisasi Supergraf Baru di Direktori Baru

### Prasyarat

- **DDN CLI** harus sudah terinstal di sistem Anda.
- Pastikan Anda berada di dalam direktori tempat Anda ingin membuat proyek supergraph baru.

### Langkah-Langkah

1. **Buat Direktori Baru**
   Buat direktori baru untuk proyek *supergraph* Anda, dan masuk ke dalam direktori tersebut. Anda bisa mengganti nama direktori dengan nama proyek Anda.

   ```
   mkdir my_hasura_project && cd my_hasura_project
   ```
   disini saya menamakan project saya yaitu my_hasura_project

2. **Inisialisasi Proyek Supergraf**
   Jalankan perintah berikut untuk menginisialisasi proyek *supergraph* di direktori ini. Gantilah `<path-to-project-dir>` dengan nama direktori yang sesuai jika Anda menggunakan direktori lain.

   ```
   ddn supergraph init .
   ```

   > **Catatan**: Tanda titik (`.`) pada akhir perintah menunjukkan bahwa Anda ingin menginisialisasi proyek di direktori saat ini.

Keterangan: 
   - `ddn`: Menjalankan **DDN CLI** yang memungkinkan Anda mengelola proyek Hasura DDN.
   - `supergraph init`: Menginisialisasi proyek supergraph baru.
   - `.` : Menentukan bahwa proyek akan dibuat di direktori saat ini.

4. **Memverifikasi Proyek Supergraf**
   Setelah menjalankan perintah di atas, beberapa file dan folder akan dibuat dalam direktori proyek Anda. Struktur direktori dasar biasanya berisi file konfigurasi yang diperlukan untuk mengelola *supergraph* Anda.

5. **Langkah Selanjutnya**
   Setelah inisialisasi selesai, Anda dapat melanjutkan untuk menambahkan *connector* dan melakukan introspeksi database, serta membangun dan menjalankan proyek supergraph Anda.

---

### Contoh Tampilan Struktur Direktori Setelah Inisialisasi

Setelah Anda menyelesaikan langkah-langkah di atas, berikut adalah contoh tampilan struktur direktori proyek supergraph:

```
my_supergraph_project/
├── connectors/
├── supergraph.yaml
├── models/
└── README.md
```

- **connectors/** : Folder ini berisi konfigurasi untuk konektor yang terhubung ke berbagai sumber data.
- **supergraph.yaml** : File utama untuk konfigurasi supergraph Anda.
- **models/** : Folder ini akan berisi model data yang digunakan dalam proyek supergraph Anda.
- **README.md** : (Opsional) Dokumentasi proyek.

### Troubleshooting

- **Error**: `ERR Expected 1 argument "path-to-project-dir"; usage "ddn supergraph init <path-to-project-dir>"`

  Jika Anda menemui error ini, pastikan Anda memberikan argumen path yang sesuai, seperti `.` untuk direktori saat ini, atau nama direktori lain yang Anda inginkan.

---

Dengan mengikuti panduan di atas, Anda sekarang telah berhasil menginisialisasi proyek supergraph baru di direktori Anda dan siap untuk melanjutkan konfigurasi dan pengembangan lebih lanjut.

---

Silakan menambahkan dokumentasi ini ke dalam file README.md atau dokumen di repositori GitHub Anda agar memudahkan tim dalam memahami proses inisialisasi supergraph.





