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
   
   - Arti: Menunjukkan laju permintaan ke cache.
   - Kegunaan: Ini membantu melihat seberapa efektif cache digunakan. Tingkat penggunaan cache yang tinggi bisa meningkatkan performa, sementara tingkat rendah bisa menunjukkan bahwa cache tidak digunakan secara optimal.
     
3. HTTP Data Transfer:
   
   - Arti: Menampilkan jumlah data yang ditransfer melalui koneksi HTTP.
   - Kegunaan: Ini berguna untuk memonitor seberapa banyak data yang dipindahkan dari/ke server. Peningkatan signifikan dapat menjadi indikator peningkatan trafik atau beban.

4. Action Data Transfer:
   
   - Arti: Menampilkan jumlah data yang ditransfer melalui action.
   - Kegunaan: Ini membantu memantau performa action yang mungkin digunakan dalam aplikasi. Banyaknya data yang diproses oleh action bisa menunjukkan seberapa sering mereka dipanggil dan seberapa intensif penggunaannya.
