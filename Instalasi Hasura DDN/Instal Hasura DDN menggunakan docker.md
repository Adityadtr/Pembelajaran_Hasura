# Install DDN CLI

### Unduh DDN CLI

- Membuka terminal atau VM ubuntu linux terlebih dahulu
- Kemudia jalankan perintah berikut dibawah ini, untuk mengunduh DDN CLI dari situs resmi Hasura (https://hasura.io/docs/3.0/getting-started/quickstart).
  
  ``curl -L https://graphql-engine-cdn.hasura.io/ddn/cli/v4/get.sh | bash``
  
![image](https://github.com/user-attachments/assets/936e92e6-a9c7-4262-9931-0b223342a88c)

Dalam gambar tersebut, terlihat proses instalasi DDN yang outputnya menunjukkan suatu tabel result dari criteria yang dimana docker available dan docker compose available belum terjalankan atau belum terinstall.

solusinya harus menginstall docker dan docker compose selanjutnya.

### Verifikasi Instalasi

Setelah menginstal DDN CLI, pastikan instalasi berhasil dengan menjalankan perintah berikut untuk melihat versi DDN CLI:

``ddn --version```

Jika instalasi berhasil, Anda akan melihat output berupa nomor versi DDN CLI yang terinstal.

![image](https://github.com/user-attachments/assets/7ee19248-5533-45b4-8842-991144e01d26)

### Install Docker

- Anda dapat menginstall docker dengan mengikuti panduan penginstalan di dokumentasi hasura atau di dokumentasi pembelajaran https://github.com/Adityadtr/Pembelajaran_Hasura/blob/main/Week%201/Instalasi%20Hasura.md.
- Kemudian, instalasi docker hingga selesai
- setelah instalasi docker sudah selesai, verifikasi penginstalan menggunakan perintah ``docker --version``. perintah tersebut akan menunjukkan versi docker yang terinstall

![image](https://github.com/user-attachments/assets/03c41c1c-c295-4ccc-bf06-d1fbd2ce0f77)

### Install Docker Compose

- Anda dapat menginstall docker-compose dengan mengikuti panduan penginstalan di dokumentasi hasura atau di dokumentasi pembelajaran https://github.com/Adityadtr/Pembelajaran_Hasura/blob/main/Week%201/Instalasi%20Hasura.md.
- Kemudian, instalasi docker-compose hingga selesai
- setelah instalasi docker-compose sudah selesai, verifikasi penginstalan menggunakan perintah ``docker compose version``. perintah tersebut akan menunjukkan versi docker yang terinstall

![image](https://github.com/user-attachments/assets/e54fd563-65a4-4c06-85d8-ae7550beb137)




