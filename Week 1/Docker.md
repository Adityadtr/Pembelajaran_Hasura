# Pembuatan Dokumen Tentang Docker

Pengenalan Docker

Docker adalah platform yang memungkinkan bertugas untuk mengembangkan, mengirim, dan menjalankan aplikasi di dalam container. Container adalah unit standar perangkat lunak yang mengemas kode dan semua dependensinya sehingga aplikasi dapat dijalankan dengan konsisten di berbagai lingkungan.

Docker Engine: 

Ini adalah komponen utama dari Docker yang menjalankan container. Docker Engine menyediakan lingkungan yang diperlukan untuk membangun dan menjalankan container di atas sistem operasi host.

Docker Image: 

Sebelum menjalankan container, harus memiliki Docker image. Docker image adalah cetak biru dari container yang berisi semua komponen yang diperlukan untuk menjalankan aplikasi.

Container: 

Ketika menjalankan Docker image, Docker akan menciptakan container dari image tersebut. Container ini berisi semua yang diperlukan untuk menjalankan aplikasi dengan cara yang terisolasi dan konsisten.

# Instalasi Docker

Langkah 1 : Update Sistem

Melakukan update sistem terlebih dahulu, dengan perintah :

```
sudo apt update
sudo apt upgrade
```
Perintah ini memperbarui daftar paket dan meng-upgrade semua paket yang terinstal ke versi terbaru yang tersedia. perintah ini untuk memastikan sistem siap untuk menginstal perangkat lunak baru seperti Docker.

Langkah 2 : Instalasi paket paket yang diperlukan

Melakukan proses instalasi paket-paket yang diperlukan dapat menggunakan perintah :

```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```
Paket-paket ini diperlukan untuk mengunduh perangkat lunak melalui HTTPS dan menambahkan repositori pihak ketiga.

apt-transport-https:

Fungsi: Paket ini memungkinkan apt untuk mengunduh paket melalui HTTPS, yang lebih aman dibandingkan HTTP.
Proses: Setelah diinstal, sistem dapat mengakses repositori perangkat lunak yang menggunakan protokol HTTPS.

ca-certificates:

Fungsi: Paket ini berisi sertifikat CA (Certificate Authorities) yang digunakan untuk memverifikasi keamanan koneksi HTTPS. Ini memastikan bahwa sistem hanya terhubung ke server yang terpercaya.
Proses: Dengan menginstal sertifikat CA, sistem dapat memverifikasi keaslian sertifikat dari server yang dikunjungi, seperti repositori Docker.

curl:

Fungsi: curl adalah alat command-line yang digunakan untuk mentransfer data dari atau ke server. digunakan untuk mengunduh file atau mengirim permintaan HTTP.
Proses: curl digunakan untuk mengunduh kunci GPG dari Docker, memastikan bahwa paket yang akan diinstal berasal dari sumber yang tepercaya.

software-properties-common:

Fungsi: Paket ini menyediakan perintah add-apt-repository yang digunakan untuk menambahkan repositori baru ke sistem. Ini juga mengelola dan mengkonfigurasi sumber perangkat lunak secara lebih mudah.
Proses: Setelah diinstal, bisa dapat menambahkan repositori Docker ke sistem dengan perintah yang lebih sederhana dan terintegrasi.

Langkah 3: Tambahkan gpg key docker
melakukan proses pengamanan dengan menambahkan kunci GPG (GNU Privacy Guard) resmi dari Docker ke sistem:

```
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
```
digunakan untuk mengunduh kunci GPG resmi dari Docker dan menyimpannya di direktori /etc/apt/keyrings/ dengan nama docker.asc.
`sudo`: Memberikan hak akses administrator untuk menjalankan perintah, yang diperlukan untuk mengubah file sistem.

`curl`: Alat command-line untuk mengunduh data dari URL yang ditentukan.

`-fsSL`: Beberapa opsi untuk curl:

`-f`: Jika terjadi kesalahan (misalnya, jika URL tidak ditemukan), curl akan gagal dengan status error daripada mencoba melanjutkan.

`-s`: Menjalankan curl dalam mode "silent", sehingga tidak menampilkan pesan kemajuan (progress) atau pesan kesalahan.

`-S`: Jika ada error, opsi ini akan menampilkan pesan error meskipun mode silent diaktifkan.

`-L`: Jika URL diarahkan ke lokasi lain, curl akan mengikuti pengalihan tersebut.

https://download.docker.com/linux/ubuntu/gpg: URL tempat kunci GPG Docker di-hosting.

-o /etc/apt/keyrings/docker.asc: Menyimpan hasil unduhan (kunci GPG) ke lokasi tertentu di sistem, dalam hal ini direktori /etc/apt/keyrings/ dengan nama file docker.asc.

Langkah 4:Tambahkan Repository Docker

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Perintah ini menambahkan repositori Docker resmi ke sistem, memungkinkan untuk menginstal Docker dari sumber yang terpercaya.

Langkah 5: 

network docker ada 3
docker volume terkait:
statefull
stateless
