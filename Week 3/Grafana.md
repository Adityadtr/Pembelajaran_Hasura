# Grafana

Grafana adalah platform open-source yang digunakan untuk memvisualisasikan, memantau, dan menganalisis data dalam bentuk grafik, dashboard, dan alerting.

Grafana memungkinkan pengguna untuk mengambil data dari berbagai sumber, seperti database, aplikasi, dan layanan lainnya, dan menampilkan data tersebut dalam bentuk visualisasi interaktif yang mudah dipahami.

# Fungsi dan Fitur Grafana

- Visualisasi: Menyajikan data dalam bentuk grafik, diagram, heatmaps, dan tabel.
- Dashboard: Membuat dashboard yang terdiri dari berbagai panel untuk menampilkan data dari berbagai sumber secara bersamaan.
- Alerting: Membuat notifikasi berbasis kondisi data yang dipantau. Misalnya, jika suatu metrik mencapai ambang batas tertentu, Grafana dapat mengirimkan notifikasi via email, Slack, atau sistem lain.
- Integrasi Multi-Source: Grafana dapat mengambil data dari berbagai sumber data seperti Prometheus, InfluxDB, MySQL, PostgreSQL, Elasticsearch, dan banyak lagi.
- Querying: Memungkinkan pengguna untuk menulis dan menjalankan kueri data langsung dari interface-nya untuk mendapatkan hasil yang sesuai dengan kebutuhan.
- User Management: Memungkinkan kolaborasi tim dengan fitur manajemen pengguna dan akses yang berbeda.

# HIT API 

"Hit API" berarti mengirimkan permintaan (request) ke suatu API endpoint. Dalam hal ini, dapat melakukan request ke API Hasura GraphQL di endpoint yang diberikan. 

Proses ini biasanya melibatkan mengirimkan query atau mutation melalui metode HTTP POST ke endpoint tersebut.

Untuk "hit" API, dapat menggunakan alat seperti Postman, cURL, atau GraphQL Playground untuk mengirimkan permintaan dan menerima respon dari API.

# Melakukan Hit API menggunakan Postman 

Disini saya melakukan HIT API menggunakan Postman dengan URL API ``http://10.100.13.24/v1/graphql`` dengan sebagai berikut:

- Membuka postman terlebih dahulu
- Kemudian pilih metode HTPP Request untuk mengirim query graphql
- Masukkan URL API yang diberikan. disini saya menggunakan API ``http://10.100.13.24/v1/graphql``
- Di Tab body, pilih format graphql dan masukkan query graphql yang ingin dijalankan.

query yang saya jalankan: 

```
query MyQuery {
  todosGraphql {
    todo(id: "1") {
      id
      done
      text
      user {
        id
        name
      }
    }
  }
}
```
- Kemudian kirimkan(SEND) request dan lihat apakah responnya berhasil (data dikembalikan oleh API). Jika sukses, artinya telah "menghit" API tersebut.

![image](https://github.com/user-attachments/assets/fcb885b6-b33f-4a96-ac23-c65b4c36314c)

# Bagaimana hasil “Hit API” terbaca di Grafana

Setelah API di-"hit", Grafana memonitor dan menampilkan metrik terkait API tersebut, termasuk:

- **Jumlah** request yang dikirim ke API Hasura GraphQL.
- **Durasi** waktu yang dihabiskan oleh setiap request (latency).
- **Status respon** (apakah ada error atau semua berjalan sukses).
- **Kesehatan** dari server dan layanan yang terkait dengan Hasura (hasura-health).

![image](https://github.com/user-attachments/assets/9a20ea00-46f4-4b2c-a626-c682f40abe6b)

# Fitur Kontrol Grafana dalam Pengaturan Data

Pada dashboard Grafana, di bagian pojok tengah kanan terdapat beberapa pilihan atau kontrol untuk menyesuaikan tampilan dan pengaturan data yang ingin ditampilkan. 

![image](https://github.com/user-attachments/assets/9f93144c-87a4-4f3d-bc83-e67c03661360)

Berikut adalah beberapa opsi tersedia:

1. Add (Tambah)

   Fungsi: Untuk menambahkan elemen baru ke dashboard
   
   Pilihan:
   - Visualization: Menambahkan panel visualisasi baru ke dashboard. Panel ini bisa berupa grafik garis, bar, gauge, pie chart, dll.
   - Row: Membuat baris baru untuk mengelompokkan beberapa panel visualisasi. 
   - Import from Library: dapat mengimpor panel atau elemen yang sudah dibuat sebelumnya dari pustaka atau template lain.
  
2. Save Dashboard

   Fungsi: Menyimpan perubahan yang sudah dilakukan di dashboard.
   
   Pilihan:
   Setelah mengedit atau menambahkan panel, bisa dapat menyimpan dashboard agar modifikasi yang dilakukan tidak hilang. Biasanya diberi pilihan untuk memberikan deskripsi pada perubahan yang dilakukan (misalnya "Added new latency graph").


3. Dashboard Settings

   Fungsi: Untuk mengakses pengaturan dashboard, di mana bisa dapat menyesuaikan tata letak atau metrik yang digunakan.
   
   Pilihan:
   - General settings: Mengubah nama, tag, atau deskripsi dashboard.
   - Time settings: Menyesuaikan format waktu yang digunakan di dashboard.
   - Variables: Menambah atau mengedit variabel yang mempengaruhi bagaimana data disaring atau ditampilkan.

4. Time Range Selector

   Fungsi: Untuk memilih rentang waktu data yang ingin ditampilkan di dashboard.
   
   Pilihan:  terdapat beberapa opsi seperti
   
   - Last 5 minutes
   - Last 15 minutes
   - Last 1 hour
   - Last 24 hours
   - Last 7 days
   - Custom range (untuk menentukan rentang waktu spesifik)
     
5. Refresh Interval Selector

   Fungsi: Untuk menentukan seberapa sering dashboard harus memuat ulang data secara otomatis.
   
   Pilihan: Biasanya interval ini dapat diatur dari:
   - Off (tidak ada refresh otomatis)
   - 5 seconds
   - 10 seconds
   - 30 seconds
   - 1 minute
   - Custom interval (bisa dapat menentukan interval manual)
  
# Filter Grafana

![image](https://github.com/user-attachments/assets/07658472-8236-4bd9-89e3-b4ecc4aeea93)

Pada Grafana, bagian pojok kiri biasanya menyediakan berbagai filter atau variabel yang bisa digunakan untuk menyaring data yang ditampilkan pada dashboard. 

Dalam dashboard Hasura, pilihan seperti source, job, instance, operation type, operation name, dan query hash membantu mempersempit analisis metrik. Berikut adalah penjelasan setiap pilihan tersebut:

1. Source

   Fungsi: Menentukan sumber data atau database yang digunakan untuk menjalankan query.

   jika memantau beberapa database atau kluster Hasura, bisa memilih source yang sesuai untuk melihat metrik terkait database tertentu.

   Analisa: Bisa membandingkan performa antara database lokal dengan database produksi, atau antara beberapa kluster Hasura yang berbeda.

2. Job

   Fungsi: Menunjukkan "job" yang sedang dipantau. Dalam Grafana, job mengacu pada proses atau layanan yang sedang berjalan.

   bisa memilih job tertentu, seperti hasuraferdy, untuk fokus pada metrik yang terkait dengan layanan atau instance Hasura yang sedang dijalankan.
   
   Analisa: jika ada job yang terkait dengan API GraphQL, bisa memantau berapa banyak request atau mutasi yang dijalankan oleh job tersebut.
   
3. Instance

   Fungsi: Menentukan server atau instance Hasura di mana operasi sedang terjadi.

   Analisa:  Opsi ini berguna jika menjalankan Hasura di beberapa server atau instance, bisa memilih instance yang spesifik untuk melihat metrik performa, latency, dan request rate yang relevan dengan instance tersebut.

4. Operation Type

   Fungsi: Memfilter jenis operasi yang dijalankan melalui GraphQL, seperti query atau mutation.

   Analisa: Query dan mutation memiliki pola penggunaan resources yang berbeda misalnya, query biasanya membutuhkan lebih banyak pembacaan dari database, sedangkan mutation cenderung menulis atau memperbarui data.

5. Operation Name

   Fungsi: Memfilter berdasarkan nama operasi GraphQL yang dijalankan, jika operasi tersebut diberi nama dalam query GraphQL.

   Analisa: Menyaring berdasarkan nama operasi memungkinkan untuk fokus pada request tertentu yang mungkin bermasalah. bisa menyaring operasi ini untuk melihat berapa lama waktu yang dibutuhkan untuk menyelesaikan query dan  apakah ada error.

6. Query Hash

   Fungsi: Menyaring berdasarkan hash unik dari query yang dijalankan. Setiap query GraphQL yang dijalankan dapat memiliki hash unik, terutama jika nama operasinya sama tetapi parameternya berbeda.

   Menyaring dengan query hash berguna untuk melakukan troubleshooting pada query spesifik, terutama jika banyak request serupa dijalankan tetapi dengan parameter yang berbeda.
  
   Analisa: Jika menjalankan query yang menghasilkan hash tertentu, dapat menyaring metrik yang hanya terkait dengan query tersebut untuk melihat performa spesifik atau memeriksa apakah ada kesalahan.
