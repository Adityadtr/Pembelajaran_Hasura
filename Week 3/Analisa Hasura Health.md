# Dashboard Hasura Health

Dashboard Hasura Health adalah panel pemantauan yang memberikan informasi tentang kondisi kesehatan dan kinerja server Hasura GraphQL. 
Bertujuan untuk memantau berbagai aspek operasional penting dari server Hasura, termasuk integrasi dengan database, status metadata, latensi, dan kesehatan keseluruhan dari sistem yang digunakan.

# Komponen Panel Hasura Health

![image](https://github.com/user-attachments/assets/925fc8d3-bff2-4732-927f-12d2cf1f4166)

1. **Metadata Status**

   ![image](https://github.com/user-attachments/assets/c091bb68-d622-49ac-9cd9-9f6d0694f234)

   - Arti: Panel ini menunjukkan status metadata di Hasura. Metadata di Hasura mencakup semua konfigurasi seperti permission, custom logic, remote schemas, dan event triggers. Status ini biasanya menampilkan apakah metadata berhasil dimuat, mengalami error, atau dalam status lain yang relevan.

   - Analisa: Dari panel status metadata menunjukkan **Consistent**, yang artinya bahwa konfigurasi metadata di Hasura telah dimuat dengan benar dan tidak ada inkonsistensi atau kesalahan yang terjadi.

2. **Health check using infinity**

   ![image](https://github.com/user-attachments/assets/6770d018-e78b-40a4-86cb-f39ff66602c5)

   - Arti: Infinity mungkin mengacu pada pengukuran kesehatan server melalui ping atau heartbeat yang berkelanjutan. Ini biasanya mengukur apakah server masih merespons dengan benar dan dalam jangka waktu yang diharapkan. Jika server tidak merespons dalam jangka waktu tertentu, ini bisa menunjukkan masalah dengan server atau jaringannya.

   - Analisa: Hasil **OK** dari "Health check using infinity" menandakan bahwa server atau endpoint yang dimonitor dapat merespons dengan benar dan dalam jangka waktu yang wajar.

3. **Health Check using Blackbox**

   ![image](https://github.com/user-attachments/assets/7d7e1c87-e066-436e-8e45-19515160f5d7)

   - Arti: Blackbox adalah alat yang digunakan untuk memonitor endpoint atau layanan dari luar (seperti status HTTP atau jaringan). Panel ini memantau apakah endpoint Hasura dapat diakses dari perspektif eksternal. 

   - Analisa: Dari panel status health check using Blackbox menunjukkan no data(tidak ada data), yang berarti blackbox monitoring belum dikonfigurasi atau tidak mengirimkan hasil apa pun.

4. **Source health check**

   ![image](https://github.com/user-attachments/assets/54b9a7e9-6810-4bee-99b7-d94f9d8e181c)

   - Arti: Panel ini mengecek kesehatan sumber data yang terhubung ke Hasura, seperti database (misalnya, PostgreSQL, mysql). Jika sumber data tidak sehat, Hasura tidak akan dapat memproses permintaan query atau mutation dengan benar.

   - Analisa:

     default (hasura ferdy) : OK
   
     testsejuta (hasura ferdy) : OK

   - Penjelasan : Kedua sumber data (database) yang terhubung ke Hasura, yaitu default dan testsejuta, berstatus OK. Ini menunjukkan bahwa koneksi ke database berfungsi dengan baik dan Hasura dapat mengaksesnya tanpa masalah. Database ini adalah sumber data utama yang mendukung operasi query dan mutation pada Hasura.

5. **Metadata Version**

   ![image](https://github.com/user-attachments/assets/8ca9fa35-8c3e-4c80-bc9f-93cc75120227)

   - Arti: Ini menampilkan versi metadata yang sedang digunakan oleh Hasura. Metadata versi ini penting untuk memastikan bahwa konfigurasi yang digunakan oleh sistem Hasura up-to-date dan sesuai dengan ekspektasi tim.
   
   - Analisa: Versi metadata yang tercatat adalah 294, yang berarti metadata yang digunakan saat ini adalah versi ke-294 dari sistem. 

6. **Health Check Latency**

   ![image](https://github.com/user-attachments/assets/2d22e4d8-364b-440e-85d9-7607bde519bc)

   - Arti: Ini mengukur latensi (atau jeda waktu) untuk setiap permintaan kesehatan yang dikirimkan ke Hasura. Ini membantu memonitor seberapa cepat Hasura dapat merespons health check request.
   
   - Analisa: Tidak adanya data (No data) untuk Health Check Latency menunjukkan bahwa belum ada pengukuran yang berhasil untuk latensi health check.

7. **Postgres Connections**

   ![image](https://github.com/user-attachments/assets/db236bbd-cc40-4eb4-b4e6-03c85edb5264)

   - Arti: Panel ini menampilkan jumlah koneksi aktif yang terhubung ke database PostgreSQL yang digunakan oleh Hasura. Ini sangat penting untuk memonitor apakah ada koneksi yang terlalu banyak atau overload yang bisa menyebabkan masalah pada kinerja database.
