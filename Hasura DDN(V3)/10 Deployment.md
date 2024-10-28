# Pendahuluan

- Hasura DDN adalah produk SaaS yang sepenuhnya dikelola di cloud, di mana performa, ketersediaan, dan keamanan API Anda telah terjamin.
- API anda tersebut berjalan di infrastruktur serverless yang dioptimalkan oleh Hasura.

# Architecture Dalam Hasura DDN

Dibandingkan dengan Hasura v2, dalam Hasura v3 di mana waktu buildtime dan runtime dipisahkan menjadi komponen yang berbeda. Control plane membangun metadata proyek dan membuatnya tersedia untuk mesin Hasura v3 yang berjalan di Data Plane.

### Control Plane

![image](https://github.com/user-attachments/assets/0040d9f8-01a5-40d7-a45a-161d0eb7a1ad)

- **Fungsi Utama**: Developer berinteraksi dengan control plane untuk membuat *supergraph builds*, yang menghasilkan GraphQL API unik dan terisolasi. 
- **Hasura Console**: Menggunakan Hasura console, developer dapat memvisualisasikan *supergraph*, berkolaborasi dengan tim, dan membagikan GraphQL API ke konsumen.
- **Preview Deployment**: Control plane memungkinkan *preview deployment* melalui builds, dengan mengonversi metadata proyek ke format yang dioptimalkan untuk runtime Hasura v3 Engine.
- **Observability**: Mengumpulkan data pengamatan dari data plane, termasuk *trace* untuk setiap operasi GraphQL dan metrik penggunaan API, yang dapat diakses di console.

### **Data Plane**

![image](https://github.com/user-attachments/assets/8f6eea31-e7ee-47df-91af-5c540dc52208)

- **Fungsi Utama**: Menjalankan Hasura v3 Engine yang diperbarui untuk melayani beberapa GraphQL API sekaligus, dengan runtime *serverless-like* yang memuat konfigurasi GraphQL berdasarkan permintaan.
- **Konektivitas dan Efisiensi**: Menggunakan strategi *on-demand* untuk menangani *connection pools*, sehingga sumber daya teralokasi secara efisien.
- **Optimalisasi Latensi**: Mendukung *multi-region deployment*, memungkinkan permintaan API dialihkan ke lokasi klien terdekat untuk latensi optimal, menggunakan *Anycast IP*.
- **Kompatibilitas**: Tersedia pada GCP, AWS, dan Azure, serta pada Hasura DDN *self-hosted*, asalkan infrastruktur mendukung kemampuan jaringan yang diperlukan. 

# Analisis Struktur

![image](https://github.com/user-attachments/assets/54058757-dad5-429e-84b2-d8fd44e138a4)

Gambar tersebut menunjukkan arsitektur dari *Control Plane* dan *Data Plane* dalam sistem Hasura DDN, dan interaksi terhadap developer serta API GraphQL.

1. **Control Plane**:
   
   Control plane adalah tempat utama bagi developer untuk mengelola, membangun, dan mengamati API. Di sini, developer bisa menggunakan fitur-fitur berikut:
     - **API Explorer**: Untuk menguji dan mengeksplorasi query API secara langsung.
     - **Observability**: Untuk memantau kinerja API dan melihat metrik seperti latensi, jumlah query, dan penggunaan API.
     - **Builds & Deployments**: Tempat developer membuat dan mendistribusikan *supergraph builds*, yang menghasilkan API GraphQL baru yang unik.
     - **Auth/SSO Access Control**: Pengaturan akses dan otentikasi untuk keamanan, memungkinkan pengelolaan akses API melalui *single sign-on (SSO)* dan kontrol otorisasi.

2. **Data Plane**:
   
   Data plane menangani pemrosesan dan penyajian GraphQL API kepada pengguna. Ini terdiri dari:
     - **Hasura**: Mengelola dan menjalankan mesin Hasura versi 3 yang mampu melayani beberapa GraphQL API sekaligus dalam lingkungan *serverless-like*.
     - **Connectors**: Menghubungkan dan mengakses sumber data yang ada, baik dalam cloud maupun lokal, untuk menyediakan data yang diperlukan oleh API.

3. **Alur Kerja Developer**:
   - **Build Supergraph**: Developer menggunakan control plane untuk membuat *supergraph*, yang merupakan definisi dari API yang ingin dijalankan.
   - **GraphQL API**: Setelah build selesai, GraphQL API tersebut dapat diakses melalui data plane yang mengoptimalkan kinerja permintaan API dengan *load balancing* dan *on-demand configuration*.

4. **Interaksi Control Plane dan Data Plane**:
   - Control plane mengirimkan informasi konfigurasi dan metadata yang dibutuhkan oleh data plane untuk menjalankan setiap *supergraph build*. Data observability yang dihasilkan dari penggunaan API di data plane dikirim kembali ke control plane, memungkinkan developer untuk melihat metrik performa di panel observability.

# Serverless Edge Deployment

### Overview
- Serverless Edge  Hasura DDN memungkinkan anda menjalankan API GraphQL pada infrastruktur  global *Serverless Edge* yang dihosting oleh Hasura.
- Anda dapat mengonfigurasi instance untuk terhubung ke database, API, atau konektor lain  di infrastruktur Anda dengan berkomunikasi melalui internet publik.
- Untuk penerapan edge tanpa server, Hasura dan konektornya berjalan pada infrastruktur Hasura.
- Penskalaan, penerapan, pengoperasian, dan pemeliharaan terjadi secara otomatis, sehingga  API Anda tetap tersedia dan dapat beradaptasi dengan kebutuhan Anda tanpa pengelolaan manual.

![image](https://github.com/user-attachments/assets/4ddf6a23-3125-4b03-a7f9-1166ff78507c)

Gambar ini menggambarkan arsitektur Hasura DDN dengan *serverless edge*, memperlihatkan interaksi antara *Control Plane*, *Data Plane*, dan infrastruktur pengguna.

1. **Control Plane**:
   - Berada di infrastruktur Hasura, Control Plane menyediakan fitur *API Explorer*, *Observability*, *Builds & Deployments*, dan *Auth/SSO Access Control*.
   - Fungsi Control Plane adalah sebagai pusat manajemen, memungkinkan pengembang untuk membangun dan memantau API GraphQL dengan mudah.

2. **Data Plane**:
   - Juga berada di infrastruktur Hasura, Data Plane menjalankan Hasura dan konektor untuk mengelola permintaan API.
   - Data Plane terhubung dengan sumber data pengguna (misalnya, database, API lain, atau konektor) melalui konektor yang berjalan di Data Plane.

3. **Customer Infrastructure**:
   - Infrastruktur pengguna, yang berisi sumber data seperti *databases*, *other APIs*, dan konektor lain yang dikelola pengguna.
   - Data Plane berkomunikasi dengan infrastruktur pengguna melalui internet publik untuk mengakses sumber data ini, yang kemudian diolah dan disediakan melalui API GraphQL.

4. **Aliran Data**:
   - API GraphQL tersedia untuk *API Users* melalui Data Plane Hasura.
   - Control Plane mendukung pengembangan dan manajemen API yang ada di Data Plane.
   - Komunikasi antara Data Plane dan sumber daya pengguna dilakukan melalui koneksi internet publik untuk mengakses data yang dibutuhkan oleh API GraphQL.

### Multi Region (Wilayah)

- Hasura DDN digunakan di banyak wilayah di seluruh dunia.
- Model penyebaran ini memberikan latensi serendah mungkin untuk klien API.
- Endpoint API yang disediakan Hasura DDN didukung oleh alamat IP Anycast, di mana satu IP dialokasikan untuk melayani permintaan masuk dan permintaan dirutekan ke wilayah DDN Hasura terdekat.

![image](https://github.com/user-attachments/assets/5503965e-67e6-4fcd-8eea-143058b15988)

Gambar ini menunjukkan arsitektur *multi-region* Hasura DDN yang mendistribusikan lalu lintas API pengguna berdasarkan lokasi geografis mereka. Berikut analisis dalam gambar ini:

1. **Geo-Aware Load Balancing**:
   - Sistem ini mendistribusikan pengguna dari berbagai wilayah (AS, UE, dan India) ke server terdekat untuk mengurangi latensi.
   - Pengguna dari AS akan diarahkan ke *US West region*, pengguna dari Uni Eropa ke *EU Frankfurt region*, dan pengguna dari India ke *India - Bangalore region*.

2. **Regional Hasura Engines**:
   - Setiap wilayah memiliki instans Hasura Engine sendiri yang berjalan di *Hasura DDN Edge Network*.
   - Pengguna di wilayah tertentu berinteraksi langsung dengan Hasura Engine yang berada di wilayah terdekat. Misalnya, pengguna di UE berinteraksi dengan Hasura Engine di Frankfurt.

3. **PG Connector**:
   - Setiap wilayah juga memiliki konektor yang disebut *PG Connector* yang menghubungkan Hasura Engine dengan database.
   - *PG Connector* di setiap wilayah memastikan koneksi yang efisien antara Hasura Engine dan database terdekat (baik *primary* atau *read replica*).

4. **Database Replication**:
   - Database utama (primary) berada di Frankfurt (UE), sedangkan replika baca (read replica) berada di AS (US West).
   - Untuk permintaan yang membutuhkan akses data di wilayah UE, Hasura Engine di Frankfurt dapat mengakses database utama langsung di Frankfurt.
   - Permintaan dari AS dapat dilayani dari replika baca di US West, mengurangi latensi akses ke data yang sama.

5. **Routing Over Hasura DDN Backbone**:
   - Di wilayah India, Hasura Engine di Bangalore mengakses database di Frankfurt melalui jaringan *backbone* Hasura DDN untuk memastikan koneksi yang andal, meskipun jaraknya jauh.

6. **Keuntungan Multi-Region**:
   - Arsitektur ini memberikan latensi rendah dan kecepatan akses data yang lebih tinggi dengan melayani pengguna dari server yang paling dekat secara geografis.
   - *Failover* dan *disaster recovery* dapat lebih mudah diimplementasikan karena adanya replikasi data di berbagai wilayah.

# Private Deployment

### Pendahuluan

- Dengan penerapan Private untuk Hasura DDN, Anda dapat menjalankan Hasura dan konektor Anda baik di infrastruktur khusus yang dihosting oleh Hasura atau di infrastruktur Anda sendiri.
- Private Hasura DDN menawarkan keamanan dan isolasi yang ditingkatkan dengan mengaktifkan konektivitas pribadi untuk database, API, dan konektor lainnya.
- Hasura berkomunikasi dengan sumber Anda melalui jaringan pribadi khusus, melewati internet publik.

### Hasura Hosted (VPC)

- **Pengelolaan oleh Hasura**: Hasura mengelola deployment, uptime, dan ketersediaan data plane sepenuhnya.
- **Dukungan Cloud dan Regional**: Tersedia di GCP, AWS, dan Azure, dengan kemampuan memilih region sesuai kebutuhan. 
- **Keamanan dan Isolasi Infrastruktur**: Data plane dijalankan pada infrastruktur komputasi dan jaringan yang terisolasi untuk keamanan.
- **Konektivitas Jaringan Privat**: Mendukung opsi konektivitas privat, seperti VPC Network Peering, Private Link/Private Service Connect, Transit Gateway, atau opsi konektivitas setara yang disediakan oleh penyedia cloud.

### Self-Hosted (BYOC - Bring Your Own Cloud)

- **Kendali Penuh oleh Pengguna**: Pengguna dapat menjalankan Hasura DDN di infrastruktur mereka sendiri jika membutuhkan kontrol penuh atas infrastruktur.
- **Model Implementasi**:
  - **Hasura Mengelola Data Plane**: Data plane dijalankan di akun cloud pengguna (di Kubernetes cluster pilihan pengguna), dan Hasura menangani uptime, pembaruan, dll. Mirip dengan Hasura-Hosted DDN, namun tetap berada di infrastruktur pengguna.
  - **Pengguna Mengelola Data Plane Sendiri**: Pengguna mengatur uptime, pembaruan, dll., dan seluruh API tetap berada di jaringan pengguna, menjaga data agar tidak keluar dari sistem pengguna.

![image](https://github.com/user-attachments/assets/82e3e9b9-8dc3-4192-a27d-27c8a8c612a3)

Gambar tersebut menunjukkan arsitektur dari layanan Hasura sebagai solusi untuk API yang dapat di-host sendiri (BYOC). Berikut ini penjelasannya:

**A. Hasura Infrastructure**: Bagian ini merupakan layanan inti Hasura, yang mencakup:

  - **Control Plane**: Bertugas mengatur pengaturan, monitoring, dan manajemen umum terhadap Hasura.
  - **API Explorer**: Tool untuk menjelajahi API yang disediakan oleh Hasura.
  - **Observability**: Membantu dalam memantau dan menganalisis performa Hasura.
  - **Builds & Deployments**: Memungkinkan kamu untuk membangun dan menyebarkan perubahan ke aplikasi Hasura.
  - **Auth/SSO**: Menangani otentikasi dan otorisasi untuk mengakses API.
     
**B. Customer Infrastructure**: Bagian ini merepresentasikan infrastruktur yang kamu kontrol sendiri, tempat Hasura dijalankan:

  - **Data Plane**: Ini merupakan bagian penting dari arsitektur Hasura, yang berisi:
      - **Hasura**: Ini adalah engine utama Hasura, yang mengelola API berdasarkan data yang dihubungkan ke dalam layanan.
      - **Connectors**: Ini adalah komponen yang bertanggung jawab menghubungkan Hasura ke sumber data (database, API, dll.) yang kamu miliki.
      - **GraphQL API**: Hasura menyediakan API GraphQL untuk mengakses dan memanipulasi data dari sumber yang dihubungkan.
  - **Sources:** Sumber data yang kamu miliki sendiri, seperti:
      - **Databases**: Misalnya, database PostgreSQL, MySQL, atau MongoDB.
      - **Other APIs**: API eksternal yang ingin kamu hubungkan ke aplikasi Hasura.
      - **Connectors**: Komponen yang membantu menghubungkan Hasura ke sumber data.
  - **API Users**: Representasi pengguna yang mengakses dan menggunakan API yang dibangun oleh Hasura.
    
Dalam skema ini, Hasura bertindak sebagai jembatan antara sumber data yang kamu miliki sendiri dan pengguna yang ingin mengaksesnya. Dengan menggunakan Hasura BYOC, mendapatkan keunggulan seperti:

- Kontrol penuh atas data: Karena kamu mengontrol infrastruktur, data tetap di bawah kendalimu.
- Fleksibilitas: Kamu bebas memilih provider cloud, hardware, dan sistem operasi yang sesuai

### Keamanan dan Alur Data: 

- Operasi data kritis terjadi sepenuhnya dalam infrastruktur pengguna.
- Hasura menerima query GraphQL dan mengakses data langsung dalam infrastruktur pengguna dan menjaga kerahasiaan data.
- Komunikasi antara Control Plane (Hasura) dan Data Plane terbatas pada konfigurasi dan pengelolaan, tanpa melibatkan data atau respons API pengguna, sehingga keamanan data lebih terjamin.

# Interaksi dengan control plane

![image](https://github.com/user-attachments/assets/1580eb93-d9c2-487a-a3e7-fdf845f1c586)

Gambar tersebut menggambarkan interaksi berbagai komponen dengan control plane dalam pengaturan Hasura.

- Control plame menangani tugas-tugas seperti membangun dan menyimpan metadata Hasura. Prosesnya dimulai dengan file metadata Hasura (hml).
- File ini digunakan untuk membuat build, yang kemudian diproses oleh Metadata Builder dan disimpan di Build Artifact Storage.
- Metadata Builder kemudian menggunakan metadata yang dibangun untuk menghasilkan aturan perutean, yang kemudian digunakan oleh Gateway.
- Gateway ini bertindak sebagai jembatan antara control plane dan data plane, memungkinkan interaksi dengan Hasura.
- Control plane juga mengelola beban kerja, yang berarti menangani penerapan, penskalaan, dan aspek operasional lainnya dalam menjalankan Hasura di Kubernetes.

Penting untuk dicatat bahwa control plane berinteraksi dengan data plane melalui Gateway. Interaksi ini terutama melibatkan pembacaan metadata yang tersimpan untuk mengonfigurasi perilaku Hasura dan merutekan permintaan ke titik akhir yang sesuai.
Secara keseluruhan, control plane mengatur pembuatan dan pengelolaan konfigurasi Hasura, memastikan komunikasi yang lancar antara data plane dan aplikasi klien.

### Kesimpulan
Arsitektur ini memisahkan tugas pengelolaan API (control plane) dari eksekusi API (data plane), yang meningkatkan keamanan, efisiensi, dan skalabilitas. Developer memiliki kendali penuh dalam pembuatan dan pemantauan API melalui control plane, sedangkan data plane mengoptimalkan eksekusi API agar tetap responsif dan terdistribusi di berbagai lokasi.
