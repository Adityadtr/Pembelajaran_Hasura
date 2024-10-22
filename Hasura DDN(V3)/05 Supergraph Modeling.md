# Supergraph Modeling

- Supergraph modeling adalah konsep yang digunakan untuk menggabungkan berbagai subgraph (seperti API, data source, dan layanan) ke dalam satu API terpusat yang dapat diakses oleh berbagai aplikasi.
- Dalam konteks Hasura, supergraph membantu mengelola dan menyatukan berbagai konektor dan data source melalui metadata engine, yang mengatur model, relasi, perizinan, dan perintah.
- Setiap subgraph berisi metadata engine-nya sendiri, yang mengelola aspek-aspek sumber data yang terkait.

# Contoh Supergraph Modeling

![image](https://github.com/user-attachments/assets/92b4db6a-03f4-47a4-9ed9-4867f34ac5f0)

Gambar yang ditunjukkan mengilustrasikan struktur supergraph dalam proyek bernama my_project. Di dalam supergraph tersebut terdapat beberapa subgraph, masing-masing terhubung ke sumber data yang berbeda.

1. **Supergraph (`my_supergraph`)**:
   
   - Supergraph ini merupakan layer teratas yang menyatukan berbagai subgraph.
   - Supergraph bertindak sebagai penghubung utama yang memungkinkan berbagai data source dan layanan diakses melalui satu endpoint API yang konsisten.

2. **Subgraph**:
   
   - Terdapat beberapa subgraph dalam supergraph ini, seperti `my_subgraph`, `another_subgraph`, dan `yet_another_subgraph`.
   - Setiap subgraph berperan sebagai model terpisah yang menghubungkan ke satu atau lebih sumber data.
   - Setiap subgraph memiliki metadata engine sendiri, yang bertanggung jawab atas manajemen elemen-elemen penting seperti **Models** (model data), **Relationships** (hubungan antar-entitas/tabel), **Permissions** (izin akses pengguna), dan **Commands** (perintah atau operasi).

3. **ConnectorLink**:
   
   - **ConnectorLink** adalah penghubung antara subgraph dan konektor yang digunakan untuk mengakses sumber data.
   - Setiap subgraph terhubung ke sumber data melalui satu atau lebih ConnectorLink.
   - Konektor ini adalah alat yang memungkinkan subgraph mengakses data dari berbagai jenis source, seperti database SQL, API eksternal, atau layanan cloud.

4. **Sumber Data (Data Source)**:
   
   - Setiap subgraph terhubung ke berbagai sumber data melalui konektor.
   - Sumber data ini bisa berupa database relasional, API, atau layanan lain yang relevan dengan kebutuhan aplikasi.
   - Gambar menunjukkan bahwa subgraph dapat mengakses berbagai tipe sumber data, seperti database, layanan cloud

### Kesimpulan:

Supergraph modeling dalam konteks ini memberikan solusi bagi penggabungan beberapa sumber data melalui model-model subgraph yang terhubung secara terorganisir dan terstandarisasi. Dengan struktur ini, pengembang dapat dengan mudah mengelola banyak sumber data melalui satu API yang terpadu, mengurangi kompleksitas dalam pengelolaan izin, relasi, dan operasi di berbagai sumber data.
