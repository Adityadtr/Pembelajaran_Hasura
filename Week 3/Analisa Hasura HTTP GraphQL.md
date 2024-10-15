# Dashboard hasura-http-graphq

Dashboard "Hasura HTTP GraphQL" di Grafana adalah tampilan visual yang memonitor performa dan metrik operasional dari API Hasura GraphQL. 
Dashboard ini digunakan untuk melacak berbagai aspek penting dari bagaimana API beroperasi, seperti jumlah query, waktu respons (latency), kesalahan (error), dan data transfer.

# Elemen Dashboard Hasura HTTP Graphql

![image](https://github.com/user-attachments/assets/48294381-fd24-4f15-b82a-b49a3850c0d8)

Dalam dashboard hasura-http-graphql mencakup tiga bagian, yaitu: Overview, GraphQL Metrics, dan General Metrics. Berikut analisis dan penjelasan untuk tiap panel dalam last:

A. Overview : memiliki 7 panel

1. Total Queries:
   
   - Arti: Menampilkan jumlah total query GraphQL yang dikirim ke Hasura dari waktu ke waktu.
   - Kegunaan: Ini berguna untuk melihat seberapa sering API GraphQL digunakan. Metrik ini membantu mengukur penggunaan API oleh aplikasi atau user.
     
2. Query Latency:
   
   - Arti: Mengukur waktu respons rata-rata yang dibutuhkan oleh query GraphQL untuk mendapatkan jawaban(response) dari Hasura.
   - Kegunaan: Berguna untuk memantau performa API, terutama dalam hal waktu respon. Latency yang tinggi mungkin menunjukkan masalah performa, seperti server yang overload atau database yang lambat.
     
3. Total Mutations:
   
   - Arti: Menampilkan jumlah total mutation yang dikirim ke Hasura. Mutation adalah operasi GraphQL untuk melakukan perubahan data.
   - Kegunaan: Berguna untuk melihat aktivitas write (penulisan data) ke server melalui mutation GraphQL, yang memberikan gambaran tentang seberapa sering data dimodifikasi.

4. Mutation Latency:
   
   - Arti: Mengukur waktu respons rata-rata untuk setiap mutation yang dijalankan.
   - Kegunaan: Latency tinggi pada mutation bisa mengindikasikan masalah pada proses penulisan data, seperti bottleneck di sisi server atau database.
     
5. Top Queries:
   
   - Arti: Menampilkan daftar query yang paling sering dijalankan dalam sistem.
   - Kegunaan: Berguna untuk memahami pola penggunaan API. Query yang sering digunakan bisa dioptimalkan jika performanya lambat.

6. Top Mutations:
   
   - Arti: Menampilkan daftar mutation yang paling sering dijalankan.
   - Kegunaan: Sama seperti "Top Queries", tetapi fokus pada operasi write. Mutations ini penting untuk dipantau, terutama jika mereka mempengaruhi performa penulisan data.

7. Top Error Rate:
   
   - Arti: Menampilkan query atau mutation yang paling sering gagal (error).
   - Kegunaan: Sangat penting untuk mengidentifikasi masalah dalam API. Jika satu query atau mutation sering menghasilkan error, ini menunjukkan adanya bug atau masalah validasi.
  
B. GraphQL Metrics : memiliki 6 panel

1. Query Request Rate:
   
   - Arti: Menampilkan laju (rate) request query per detik.
   - Kegunaan: Berguna untuk mengetahui seberapa sering query dikirimkan ke Hasura dalam waktu tertentu. Peningkatan signifikan bisa menjadi tanda lonjakan trafik atau beban tinggi.
     
2. Mutation Request Rate:
   
   - Arti: Menampilkan laju (rate) request mutation per detik.
   - Kegunaan: Memberikan wawasan tentang seberapa sering mutation dikirimkan. Ini membantu memonitor aktivitas penulisan data dan memberikan pemahaman tentang intensitas operasi write di sistem.
     
3. Query Error Rate:
   
   - Arti: Menunjukkan persentase query yang gagal atau menghasilkan error.
   - Kegunaan: Sangat penting untuk mengetahui tingkat kegagalan query. Jika error rate tinggi, mungkin ada masalah dalam kode atau server yang memerlukan investigasi.

4. Mutation Error Rate:
   
   - Arti: Menunjukkan persentase mutation yang gagal.
   - Kegunaan: Mirip dengan query error rate, tetapi fokus pada mutation. Kegagalan mutation bisa berarti ada masalah dalam proses penulisan data, seperti kesalahan validasi input atau masalah pada server.
     
5. Query Latency (p95):
   
   - Arti: Menampilkan persentase ke-95 (p95) dari latency query.
   - Kegunaan: p95 berarti 95% dari query diselesaikan dalam waktu yang lebih cepat atau sama dengan angka yang ditampilkan. Ini adalah metrik yang penting untuk mengidentifikasi outlier latency yang mungkin hanya dialami oleh sedikit query tetapi bisa berdampak signifikan.

6. Mutation Latency (p95):
   
   - Arti: Menampilkan persentase ke-95 (p95) dari latency mutation.
   - Kegunaan: Memberikan pemahaman yang sama seperti query latency (p95), tetapi fokus pada operasi penulisan data. Latency tinggi di sini bisa menandakan adanya bottleneck dalam proses penulisan data.

C. General Metrics : memiliki 4 panel

1. HTTP Connections:
   
   - Arti: Menunjukkan jumlah koneksi HTTP yang sedang aktif di server.
   - Kegunaan: Berguna untuk memantau beban yang sedang dihadapi server dari sisi koneksi. Lonjakan jumlah koneksi bisa menjadi tanda meningkatnya beban atau potensi masalah jika kapasitas server terbatas.
     
2. Cache Request Rate:

   cache: penyimpanan sementara. dan memakai nya pakai redis.

   - Arti: Menunjukkan laju permintaan ke cache.
   - Kegunaan: Ini membantu melihat seberapa efektif cache digunakan. Tingkat penggunaan cache yang tinggi bisa meningkatkan performa, sementara tingkat rendah bisa menunjukkan bahwa cache tidak digunakan secara optimal.
     
3. HTTP Data Transfer:
   
   - Arti: Menampilkan jumlah data yang ditransfer melalui koneksi HTTP.
   - Kegunaan: Ini berguna untuk memonitor seberapa banyak data yang dipindahkan dari/ke server. Peningkatan signifikan dapat menjadi indikator peningkatan trafik atau beban.

4. Action Data Transfer:
   
   - Arti: Menampilkan jumlah data yang ditransfer melalui action.
   - Kegunaan: Ini membantu memantau performa action yang mungkin digunakan dalam aplikasi. Banyaknya data yang diproses oleh action bisa menunjukkan seberapa sering mereka dipanggil dan seberapa intensif penggunaannya.

# Menu titik di pojok kanan atas panel

Setiap panel di Grafana memiliki menu dengan ikon tiga titik di pojok kanan atas. Berikut adalah fungsi-fungsi yang terdapat di dalamnya:

![image](https://github.com/user-attachments/assets/cb3ef02c-8e40-4509-af3e-e058dbe1335f)


1. **View**:

   ![image](https://github.com/user-attachments/assets/b652b12a-83f2-472d-aa68-3b387265ee08)

   - Arti: Membuka panel dalam mode layar penuh untuk melihat lebih jelas tanpa gangguan dari panel lain.

   - Kegunaan: Berguna ketika Anda ingin fokus pada satu panel spesifik atau melakukan analisis mendalam pada data yang ditampilkan.

2. **Edit**:

   ![image](https://github.com/user-attachments/assets/e1424640-7580-470b-ae08-340b2645f3e8)

   - Arti: Membuka pengaturan panel di mode edit, di mana dapat mengubah query, visualisasi, dan pengaturan lainnya.

   - Kegunaan: Berguna untuk melakukan perubahan pada data yang ditampilkan atau cara data tersebut divisualisasikan.

3. **Share**:

   ![image](https://github.com/user-attachments/assets/3fbf0c5c-fb68-4cff-aadc-a568f8280f96)

   - Arti: Membagikan tautan ke panel atau mengekspor data dari panel dalam format gambar atau CSV.

   - Kegunaan: Berguna ketika ingin berbagi visualisasi atau data dengan orang lain, baik dalam tim maupun di luar Grafana.

4. **Explore**:

   ![image](https://github.com/user-attachments/assets/e58caa96-1582-4334-b5b3-e97d35a695a1)

   - Arti: Memasukkan data panel ke dalam mode eksplorasi, di mana dapat melihat data secara mendetail dan mengujinya lebih lanjut.

   - Kegunaan: Berguna untuk debugging atau investigasi mendalam terhadap data atau query yang digunakan di panel.

5. **Inspect (Data, Query, Panel JSON)**:

   ![image](https://github.com/user-attachments/assets/afcee971-ccc1-4409-a3ec-85948c3ad89d)

   - Data: Menampilkan data mentah yang digunakan di panel, baik dalam bentuk tabel atau JSON.

   - Query: Memperlihatkan query yang digunakan untuk mendapatkan data di panel.

   - Panel JSON: Memperlihatkan konfigurasi panel dalam format JSON.

6. **More (Duplicate, Copy, Create)**:

   ![image](https://github.com/user-attachments/assets/16f4e0a2-2de0-4437-91d5-f781f7bcd8bb)

   - Duplicate:
     
     Arti: Membuat salinan dari panel saat ini dengan semua konfigurasi yang sama, termasuk query, visualisasi, dan pengaturan lainnya.

     Kegunaan: Berguna saat anda ingin membuat panel baru yang sangat mirip dengan yang ada, tetapi dengan beberapa perubahan kecil.

   - Copy:
     
     Arti: Menyalin konfigurasi panel ke clipboard.

     Kegunaan: Berguna jika Anda ingin menempelkan konfigurasi panel di tempat lain, seperti dalam JSON untuk pengeditan manual atau jika Anda ingin memindahkan panel ini ke dashboard lain.
     
   - Create:
     
     Arti: Biasanya ini mengacu pada opsi untuk membuat panel baru berdasarkan beberapa template atau fitur, meskipun fitur ini bisa berbeda tergantung pada versi Grafana.

     Kegunaan: Digunakan saat Anda ingin memulai membuat panel baru dari awal, tetapi dengan dasar-dasar yang mungkin serupa dengan panel yang sedang Anda lihat,
     atau dalam konteks pembuatan elemen baru berdasarkan data yang ada.

7. **Remove**:

   - Arti: Menghapus panel saat ini dari dashboard.

   - Kegunaan: Fitur ini digunakan untuk menghapus panel yang tidak lagi dibutuhkan dari dashboard.
   
   **Noted: Perlu hati-hati saat menggunakan fitur ini karena jika panel dihapus, semua data dan konfigurasi terkait akan hilang dari dashboard, kecuali Anda memiliki cadangannya atau telah menduplikasi panel sebelumnya.**
