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
