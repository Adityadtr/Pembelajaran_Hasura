# Plugin Hasura DDN

- Hasura DDN Plugin adalah fitur yang memungkinkan pengguna untuk memperluas fungsionalitas dari Hasura Data Delivery Network (DDN) dengan cara mengintegrasikan kemampuan tambahan.
- Plugin ini memudahkan pengguna untuk menambahkan berbagai jenis layanan atau fungsi eksternal ke dalam alur kerja Hasura tanpa mengubah struktur inti Hasura.
- Dengan memanfaatkan plugin, developer dapat menyesuaikan sistem mereka untuk memenuhi kebutuhan spesifik bisnis, meningkatkan fleksibilitas, dan menambahkan fungsionalitas khusus.

# Arsitektur Plugin

![image](https://github.com/user-attachments/assets/f7bca1ab-f8c0-4d39-8fb2-30cc0ae79170)

Gambar arsitektur diatas, menggambarkan alur kerja dan interaksi dari komponen-komponen yang ada dalam sistem 
**Hasura DDN Plugin**. 

Berikut adalah penjelasan dari tiap komponen dan bagaimana alur permintaan (request) dan tanggapan (response) bekerja dalam sistem ini:

### **Penjelasan Komponen Arsitektur**:

1. **Client**: 
   - **Client** adalah aplikasi atau pengguna akhir yang mengirimkan permintaan (request) ke server. Client ini bisa berupa aplikasi web, mobile, atau API client lainnya.
   
2. **Request**: 
   - Permintaan dari client yang dikirim ke sistem untuk diproses. Ini adalah awal dari interaksi di mana client meminta operasi tertentu (seperti menjalankan query atau mutasi data) melalui Hasura.

3. **Authentication**:
   - Sebelum permintaan diproses lebih lanjut, **authentication** atau otentikasi memastikan bahwa permintaan tersebut berasal dari sumber yang valid. Sistem otentikasi dapat menggunakan berbagai metode seperti token JWT, API key, OAuth, atau mekanisme otentikasi lainnya.
   
4. **Pre-parse hooks**:
   - **Pre-parse hooks** adalah mekanisme tambahan yang memungkinkan Anda menambahkan logika sebelum permintaan query diproses lebih lanjut. Ini dapat digunakan untuk memvalidasi, memodifikasi, atau mengatur permintaan sebelum parsing dan perencanaan query.
   
5. **Query Parsing and Planning**:
   - Setelah melewati otentikasi, sistem akan masuk ke tahap **query parsing and planning** di mana permintaan query diuraikan dan diproses untuk memahami struktur dan logika query. Ini termasuk merencanakan bagaimana query tersebut akan dieksekusi.
   
6. **Execute query**:
   - Setelah parsing dan perencanaan selesai, sistem akan mengeksekusi query dengan mengakses sumber data yang diperlukan. Proses ini melibatkan pengambilan data dari **Data Connector** yang terhubung ke sumber data (database, API eksternal, dll.).

7. **Data Connector**:
   - **Data connector** adalah komponen yang menghubungkan engine Hasura dengan sumber data seperti database (PostgreSQL, MySQL, dsb.) atau sumber eksternal lainnya. Ini adalah tempat di mana query dijalankan dan data yang dibutuhkan dikembalikan ke sistem.

8. **Post-processing**:
   - Setelah query dieksekusi dan data diambil, hasilnya akan masuk ke tahap **post-processing**. Pada tahap ini, data yang diterima dari sumber data dapat diproses lebih lanjut (misalnya, format ulang, agregasi, atau transformasi data) sebelum dikirim kembali ke client.
   
9. **Pre-response hooks**:
   - Sebelum respons dikirim kembali ke client, **pre-response hooks** dapat digunakan untuk memodifikasi atau memvalidasi respons terakhir. Ini memberikan fleksibilitas tambahan bagi developer untuk menambahkan logika tambahan pada output.
   
10. **Response**:
    - Setelah semua proses selesai, respons akan dikirim kembali ke **client** dengan data yang diminta atau hasil dari query yang dieksekusi.

### **Ringkasan Alur Kerja**:
- **Client** mengirimkan request ke sistem. 
- Request melalui proses **authentication** untuk memastikan keamanan.
- Jika ada **pre-parse hooks**, query akan diproses melalui hook ini sebelum dilanjutkan.
- Kemudian, request diparsing dan direncanakan oleh modul **query parsing and planning**.
- Setelah rencana dieksekusi, **data connector** mengakses data dari sumber yang diperlukan.
- Data hasil eksekusi diproses dalam **post-processing**.
- **Pre-response hooks** memberikan kesempatan terakhir untuk modifikasi sebelum data dikirim kembali ke client sebagai **response**.
