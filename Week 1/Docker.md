# Pembuatan Dokumen Tentang Docker

Pengenalan Docker

Docker adalah platform yang memungkinkan bertugas untuk mengembangkan, mengirim, dan menjalankan aplikasi di dalam container. 

Container adalah unit standar perangkat lunak yang mengemas kode dan semua dependensinya sehingga aplikasi dapat dijalankan dengan konsisten di berbagai lingkungan.

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

Langkah 5: Update Daftar Paket dan Install Docker

```
sudo apt update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Perintah pertama memperbarui daftar paket untuk menyertakan repositori Docker yang baru saja ditambahkan. 

Perintah kedua digunakan untuk menginstal Docker dan beberapa komponen terkait di sistem Ubuntu.

Langkah 6: Verifikasi Instalasi

```
sudo systemctl status docker
```
Perintah ini memeriksa status layanan Docker untuk memastikan bahwa Docker sudah berjalan dengan benar.

Langkah 7: Menampilkan Versi Docker

```
docker --version
```
Perintah ini digunakan untuk melihat versi docker yang di instal

# Membangun Docker Image dan Menjalankan Container

Dalam membangun docker image dan menjalankan container dapat melakukan perintah ini :

```
sudo docker run hello-world
```
Perintah ini akan mengunduh gambar pengujian dan menjalankannya dalam kontainer. Ketika kontainer berjalan, ia mencetak pesan konfirmasi dan keluar.

Hasil Outputnya:

![image](https://github.com/user-attachments/assets/5d58f00f-b53f-43bc-b031-fd390233ac8b)

Dapat juga membangun docker image dan menjalankan container dengan cara:

Langkah 1 : Membuat Direktori Proyek

Buat direktori (folder) baru, misalkan dengan nama "hello-world-docker":

```
mkdir hello-world-docker
```
Gunakan perintah cd untuk masuk ke dalam direktori yang baru saja dibuat dengan perintah :

```
cd hello-world-docker
```
Hasil Outputnya:

![image](https://github.com/user-attachments/assets/9a50e8e3-201b-429d-9275-361853b0cf5e)

Langkah 2: Membuat Dockerfile

Buat file bernama 'Dockerfile'  didalam direktori proyek dengan perintah:

```
touch Dockerfile
```
`Dockerfile` adalah file teks yang berisi instruksi untuk Docker tentang cara membangun image.

Langkah 3: Mengedit Dockerfile

Edit Dockerfile dengan menggunakan editor teks, dengan perintah :

```
nano Dockerfile
```
Kemudian isi file dengan :

```
# Gunakan image dasar dari Docker Hub
FROM alpine:latest

# Setel perintah yang akan dijalankan ketika container dijalankan
CMD ["echo", "Hello World"]
```

Penjelasan:

FROM alpine:

Menggunakan image dasar alpine yang sangat ringan dari Docker Hub.

`CMD ["echo", "Hello World"]`: 

Menetapkan perintah echo "Hello World" yang akan dijalankan ketika container berjalan.

Simpan dan keluar dari editor (untuk nano, tekan CTRL+O lalu Enter untuk menyimpan, dan CTRL+X untuk keluar).

Hasil Output:

![image](https://github.com/user-attachments/assets/616bcea2-2c1c-4cba-b075-26cc9f9d1d16)


Langkah 4: Membangun Docker Image

Membangun Docker image menggunakan Dockerfile yang telah Anda buat.

```
sudo docker build -t hello-world-image .
```
Penjelasan:

docker build: Perintah untuk membangun Docker image.

-t hello-world-image: Memberikan tag hello-world-image pada image yang dibangun.

. (titik): Menunjukkan bahwa Dockerfile berada di direktori saat ini.

Hasil Output:

![image](https://github.com/user-attachments/assets/781584ae-8bc1-421d-9710-49daf70a6208)


Langkah 5: Menjalankan Docker Container

Menjalankan container dari image yang telah Anda buat.

```
sudo docker run hello-world-image
```
docker run: Perintah untuk menjalankan container.

hello-world-image: Nama image yang ingin Anda jalankan.

Hasil Outputnya:

![image](https://github.com/user-attachments/assets/5e0ee4d1-a3d2-4805-ae05-0d5bd990c784)


Langkah 6: Verifikasi Container yang sedang berjalan

Periksa container yang sedang berjalan, dengan perintah:

```
docker ps
```

Perintah ini menampilkan semua container yang sedang berjalan di sistem.

Hasil Output:

![image](https://github.com/user-attachments/assets/806a750c-6934-4f89-9ae8-cdd35c450ea9)


Langkah 7: Melihat semua container 

Periksa semua container, termasuk yang telah berhenti.

```
sudo docker ps -a
```
Ini akan menampilkan daftar lengkap semua container yang pernah dijalankan, termasuk yang sudah selesai menjalankan perintahnya dan berhenti.

Hasil Output:

![image](https://github.com/user-attachments/assets/1943bff1-f016-43f8-a3eb-72166dd7d770)


Langkah 8 : Menghapus Container (Jika sudah tidak diperlukan)

```
sudo docker rm <container_id>
```
<container_id>: Ganti dengan ID container yang ingin dihapus.

Langkah 9: Hapus Docker Image (Jika sudah tidak diperlukan)

Jika ingin menghapus image yang telah dibuat, gunakan perintah berikut:

```
sudo docker rmi hello-world-image
```
docker rmi: Perintah untuk menghapus Docker image.

hello-world-image: Nama image yang ingin dihapus.




