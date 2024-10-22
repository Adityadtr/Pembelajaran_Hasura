# Federasi Arsitektur di Hasura DDN

Federasi dalam Hasura DDN adalah pendekatan untuk mengintegrasikan berbagai subgraph menjadi satu supergraph yang kohesif. Ini memungkinkan berbagai tim untuk bekerja pada bagian-bagian yang berbeda dari arsitektur API, tanpa mengganggu satu sama lain, dan menyatukan hasilnya dalam satu endpoint API.

# Komponen Utama dalam Arsitektur Federasi

![image](https://github.com/user-attachments/assets/efb08889-2e80-4a54-a343-29596f1a9492)

1. **Supergraph**:
   - Supergraph adalah lapisan utama yang menyatukan semua subgraph. Ia menyatukan berbagai model data, operasi, dan metadata dari subgraph ke dalam satu API yang konsisten.
   - Klien hanya perlu berinteraksi dengan supergraph untuk mengakses seluruh sumber data dan operasi yang disediakan oleh subgraph.

2. **Subgraph**:
   - Setiap subgraph adalah unit modular yang menangani bagian tertentu dari domain aplikasi. Setiap subgraph berisi model, operasi, dan metadata yang relevan dengan domain tersebut.
   - Subgraph dikembangkan secara independen oleh tim berbeda dan dapat terhubung dengan berbagai sumber data, seperti database, API eksternal, atau layanan lainnya.

3. **Connector**:
   - Connector adalah komponen yang menjembatani subgraph dengan **data source** (sumber data). Setiap subgraph memiliki konektor yang mengatur bagaimana data diakses dan dimutasi.
   - Connectors mendukung berbagai jenis sumber data seperti database relasional (PostgreSQL, MySQL), NoSQL, API, atau layanan cloud, sehingga memungkinkan integrasi yang fleksibel.

4. **Data Source (Sumber Data)**:
   - **Data source** adalah tempat subgraph mendapatkan atau menyimpan datanya. Ini bisa berupa berbagai jenis database, API eksternal, atau layanan penyimpanan lainnya.
   - Setiap data source bisa diakses oleh beberapa subgraph melalui **connector**. Hasura memungkinkan konfigurasi yang fleksibel untuk menghubungkan subgraph dengan data source yang relevan.
   - Data source bisa berupa layanan cloud, penyimpanan internal, atau API REST, tergantung pada kebutuhan sistem.

5. **Metadata**:
   - Metadata adalah kumpulan informasi mengenai struktur dan konfigurasi dari subgraph. Metadata ini meliputi definisi model, hubungan antar model, izin akses, serta operasi yang diizinkan (queries/mutations).
   - Metadata penting untuk membangun skema GraphQL yang digenerate Hasura, memungkinkan supergraph untuk mengelola dan mengontrol akses serta query terhadap subgraph yang berbeda.

6. **Querying dan Mutations**:
   - Klien dapat mengirimkan query atau mutation ke supergraph, yang kemudian diteruskan ke subgraph terkait melalui konektor. Supergraph menangani penggabungan data dari berbagai sumber secara efisien.
   - Query dan mutation memanfaatkan struktur federasi untuk mengambil data dari berbagai subgraph yang mungkin memiliki sumber data yang berbeda, memberikan hasil yang terintegrasi kepada klien.

# Arsitektur 

![Screenshot 2024-10-22 102455](https://github.com/user-attachments/assets/14b6ca90-74b9-4b3d-92cf-baf8a17e8284)

Gambar tersebut menunjukkan arsitektur Hasura v3.

**Developer Machine**
   - Menjalankan kode lokal.
   - Menyiapkan metadata Hasura, yang menjelaskan bagaimana data dalam database berhubungan dengan skema GraphQL.

**Control Plane**
   - Metadata Builder: Memproses metadata Hasura dan membangun konfigurasi Hasura.
   - Monitoring/Analytics: Melacak kesehatan dan performa sistem Hasura.

**CI/DD Pipeline**
   - Clone Repo: Menyalin kode dari repositori Git.
   - Create Cloud Build: Membangun docker image untuk Hasura.
   - Build Docker Image: Membangun docker image untuk Hasura.
   - Deploy Containers: Menyebarkan container Hasura ke Kubernetes.
     
**Data Plane**
   - Hasura: Menyediakan API GraphQL dan menangani permintaan.
   - Connectors: Menghubungkan Hasura dengan sumber data seperti Elastic dan REST API.
   - Otel Connector: Mengirimkan metrik dan trace ke sistem monitoring.
     
**Data Sources**
   - Elastic: Sumber data elasticsearch.
   - REST APIs: Sumber data dari REST API.

### Alur Arsitektur

**Developer melakukan perubahan pada kode**
   - Pengembang membuat perubahan pada kode di mesin pengembangan mereka.
   - Perubahan kode ini biasanya disimpan dalam repository Git (misalnya, GitHub, GitLab).
     
**Pembangunan (build) Metadata**
   -  Pembangunan lokal pengembang kemungkinan besar menyertakan kode untuk membangun Metadata Hasura.
   -  Metadata ini kemudian diunggah ke Metadata Storage Bucket, biasanya sebagai bagian dari proses Continuous Integration/Continuous Deployment (CI/CD).

**Source Control Memantau Perubahan Kode**

   - Setiap perubahan kode yang dilakukan oleh developer akan diawasi oleh sistem source control.
   - Sistem source control seperti Git akan merekam perubahan kode ini dan menyimpannya dalam repositori kode.

**Trigger Deployment**

   - Ketika pengembang menyelesaikan perubahan dan siap untuk deployment, mereka akan mengirimkan permintaan ke sistem source control untuk membangun dan deploying versi aplikasi yang baru.
   - Biasanya, ini dilakukan dengan membuat "commit" baru di Git dan "pushing" commit itu ke repository.

**CI/CD Pipeline dimulai**

   - Sistem CI/CD akan memonitor repositori kode untuk perubahan terbaru.
   - Ketika ada perubahan baru, sistem CI/CD akan memulai pipeline deployment.

**Kode Clone**

   - Pipeline CI/CD akan mengkloning repositori kode ke server build.

**Pembuatan Build**

   - Pipeline akan menjalankan langkah-langkah yang diperlukan untuk membangun aplikasi, seperti kompilasi kode, menjalankan pengujian, dan mengemas aplikasi ke dalam container.

**Image Docker Dibangun**

   - Pipeline CI/CD akan membangun image Docker yang berisi aplikasi yang sudah dibangun.

**Deployment ke Kubernetes**

   - Image Docker yang sudah dibangun kemudian akan di-deploy ke Kubernetes. Kubernetes akan menjalankan container aplikasi yang sudah dideploy.

**Hasura Mengakomodasi Database**

   - Hasura adalah layanan database yang digunakan untuk menyimpan data aplikasi. Ketika aplikasi di-deploy ke Kubernetes, Hasura akan menyediakan akses ke database untuk aplikasi tersebut.

**Connectors Menjembatani Data**

   - Connectors digunakan untuk menghubungkan Hasura ke sumber data lainnya, seperti ElasticSearch atau REST APIs.

**Data Diambil dari Sumber Data**

   - Aplikasi dapat mengambil data dari sumber data melalui connectors.

**Monitoring dan Analytics**

   - Alur kerja juga mencakup monitoring dan analytics. Data tentang kinerja aplikasi dan penggunaan sumber daya akan dikumpulkan dan diproses oleh sistem monitoring.

**Klien GraphQL Akses Data**

   - Klien GraphQL dapat mengakses data melalui API GraphQL yang disediakan oleh Hasura.

**Hasil Query Dikembalikan ke Klien**

   - Hasil query akan dikembalikan ke klien GraphQL.
