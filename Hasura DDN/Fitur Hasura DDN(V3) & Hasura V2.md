# Fitur Hasura V2 dan Hasura DDN(V3)

### Tabel dari segi API:

| Fitur                                   | Hasura v2  | Hasura DDN (v3) |
|-----------------------------------------|------------|-----------------|
| Instant GraphQL API                     | Ada        | Ada             |
| Multiple Data Sources                   | Ada        | Ada             |
| Query                                   | Ada        | Ada             |
| Mutation                                | Ada        | Ada (C)            |
| Subscription                             | Ada        | WIP             |
| Streaming                                | Ada        | WIP             |
| Aggregate Query                         | Ada        | Ada (C)          |
| Native Query                            | Ada        | Ada             |
| Native Mutation                         | Tidak Ada  | Ada             |
| Action                                  | Ada        | Ada (Digantikan oleh Lambda Connectors) |
| Event Trigger                           | Ada        | WIP             |
| Cron Trigger                            | Ada        | Tidak Ada       |
| Remote Schema                           | Ada        | Ada (Lebih mudah dikelola) |
| CI/CD                                   | Ada        | Ada (Sepenuhnya didukung) |
| Federation                               | Ada        | Ada (Sepenuhnya didukung) |
| Apollo Federation                       | Ada        | Ada             |
| API Limits                              | Ada        | WIP       |
| Allow Lists                             | Ada        | Ada             |
| Permissions                              | Ada        | Ada             |
| Authentication Integrations             | Ada        | Ada             |
| Admin Secret                            | Ada        | Tidak Ada (diganti dengan admin-level token) |
| Relay API                               | Ada        | Ada             |
| RESTified Endpoints                     | Ada        | WIP             |
| Schema Registry                         | Ada        | Ada             |
| Read Replica                            | Ada (EE) (Cloud dan Enterprise) | Ada             |
| Caching                                 | Ada (EE) (Cloud dan Enterprise) | WIP             |

### Keterangan:
- **WIP**: Work In Progress, fitur ini sedang dalam pengembangan dan mungkin belum sepenuhnya tersedia.
- **Tidak Ada**: Fitur ini tidak didukung dalam versi tersebut.
- **EE**: Tersedia hanya pada edisi Cloud dan Enterprise.
- **C**: Didukung oleh masing-masing konektor.

### Penjelasan:

- Instant GraphQL API
  - V2: Menghasilkan GraphQL API secara instan dengan menambahkan connection string ke proyek.
  - V3: Menggunakan pengalaman deklaratif berbasis kode yang dibantu oleh CLI untuk menghasilkan API, memberikan fleksibilitas lebih dalam iterasi dan pengembangan.

- Multiple Data Sources
  - V2: Menghubungkan sumber data melibatkan konfigurasi di konsol, menghasilkan API GraphQL berdasarkan skema database.
  - V3: Menghubungkan sumber data menjadi lebih sederhana dan fleksibel dengan dukungan untuk berbagai jenis sumber data (database relasional, REST API, dan layanan GraphQL lainnya) melalui native data connectors.

- Query
  - V2: Memungkinkan pengambilan data melalui API GraphQL yang dihasilkan secara otomatis.
  - V3: Proses pengambilan data ditingkatkan dengan fitur dan optimasi tambahan, membuat pengambilan data lebih cepat dan efisien.

- Mutation
  - V2: Memungkinkan modifikasi data menggunakan API GraphQL yang dihasilkan.
  - V3: Mempertahankan mutasi sebagai fitur penting, dengan beberapa konektor yang menyediakan mutasi yang dihasilkan secara otomatis.

- Subscription
  - V2: Menyediakan pembaruan real-time dengan mengirimkan perubahan data secara otomatis.
  - V3: Masih dalam tahap pengembangan, dengan desain ulang untuk meningkatkan kemampuan real-time dan fleksibilitas integrasi.

- Streaming
  - V2: Mengizinkan pengambilan data secara terus-menerus untuk kasus penggunaan real-time.
  - V3: Juga dalam tahap pengembangan untuk meningkatkan kemampuan streaming dan pengiriman data real-time.

- Aggregate Query
  - V2: Memungkinkan operasi agregasi seperti menghitung, menjumlahkan, dan merata-ratakan data.
  - V3: Mendukung query agregat sepenuhnya dengan sedikit perbedaan dari API agregat v2.

- Native Query
  - V2: Memungkinkan interaksi langsung dengan database melalui SQL kustom.
  - V3: Mendukung native queries, memungkinkan operasi pengambilan data yang kompleks.

- Native Mutation
  - V2: Tidak mendukung mutasi langsung.
  - V3: Mendukung native mutations, memberikan fleksibilitas lebih untuk operasi data lanjutan.

- Action
  - V2: Mengintegrasikan REST APIs atau logika bisnis kustom sebagai bagian dari API GraphQL.
  - V3: Menggantikan Actions dengan lambda connectors, memungkinkan definisi logika bisnis yang lebih kompleks.

- Event Trigger
  - V2: Memungkinkan pemicu otomatis untuk webhook berdasarkan perubahan dalam database.
  - V3: Masih dalam tahap pengembangan untuk mendukung plugin dan pemicu yang lebih dapat disesuaikan.

- Cron Trigger
  - V2: Memungkinkan penjadwalan tugas berkala.
  - V3: Tidak mendukung cron triggers.

- Remote Schema
  - V2: Mengizinkan penggabungan beberapa skema GraphQL menjadi API yang terpadu.
  - V3: Memudahkan manajemen dan integrasi skema GraphQL jarak jauh menggunakan konektor API GraphQL.

- CI/CD
  - V2: Didukung melalui Hasura CLI dan integrasi GitHub.
  - V3: Mendukung CI/CD dengan konsep immutable builds, memungkinkan pengembangan dan pengujian API secara iteratif.

- Federation
  - V2: Memungkinkan melalui berbagai metode termasuk penggabungan instansi Hasura.
  - V3: Mendukung federasi sepenuhnya, memungkinkan pembuatan API terpadu melalui subgraphs.

- API Limits
  - V2: Tersedia untuk mengelola penggunaan API.
  - V3: Tidak mendukung batasan API.

- Allow Lists
  - V2: Tersedia untuk membatasi akses ke query dan mutasi tertentu.
  - V3: Masih dalam tahap pengembangan dengan rencana untuk memperkenalkan mekanisme otorisasi yang lebih canggih.

- Permissions
  - V2: Tersedia untuk mengontrol akses ke data dan operasi.
  - V3: Mendukung definisi izin pada model, field, dan level perintah.

- Authentication Integrations
  - V2: Tersedia untuk mengautentikasi pengguna dengan berbagai penyedia.
  - V3: Mendukung integrasi otentikasi sepenuhnya melalui webhook atau JWT.

- Admin Secret
  - V2: Digunakan untuk mengautentikasi permintaan ke API Hasura.
  - V3: Tidak mendukung admin secret; sebagai gantinya, menggunakan token tingkat admin.

- Relay API
  - V2: Didukung untuk menggunakan fitur Relay di API GraphQL.
  - V3: Sepenuhnya mendukung Relay API.

- RESTified Endpoints
  - V2: Tersedia untuk mengekspos API GraphQL sebagai REST API.
  - V3: Masih dalam tahap pengembangan untuk kemampuan REST API yang lebih maju.

- Schema Registry
  - V2: Tersedia untuk melacak perubahan pada skema API.
  - V3: Mendukung registry skema dengan fitur diffing skema.

- Read Replica
  - V2: Hanya tersedia pada edisi Cloud dan Enterprise.
  - V3: Sepenuhnya mendukung read replicas.

- Caching
  - V2: Tersedia hanya di Cloud dan Enterprise Editions.
  - V3: Saat ini dalam tahap pengembangan untuk mekanisme caching yang lebih canggih.

### Tabel dari segi Tooling:

| Fitur                                   | Hasura v2  | Hasura DDN (v3) |
|-----------------------------------------|------------|-----------------|
| The Hasura console	                    | Ada        | Ada             |
| The Hasura CLI	                        | Ada        | Ada             |
| IDE Integrations	                      | Tidak Ada  | Ada             |
| Database Migrations	                    | Ada        | Tidak Ada       |
| Prometheus                              | Ada (EE)   | Ada             |
| OpenTelemetry                           | Ada (EE)   | Ada             |

### Keterangan:
- **EE**: Tersedia hanya pada edisi Cloud dan Enterprise.

### Penjelasan:

- The Hasura Console
  - V2:
    - Console berfungsi sebagai antarmuka utama untuk mengarang dan mengedit API GraphQL serta sumber data yang mendasarinya.
    - Menyediakan antarmuka grafis yang ramah pengguna untuk berbagai tugas, sehingga memudahkan konfigurasi dan interaksi dengan instance Hasura tanpa perlu menulis kode atau perintah kompleks.
  - V3:
    - Console berfungsi sebagai alat eksplorasi dan manajemen.
    - Mengizinkan pengguna untuk memvisualisasikan, mengeksplorasi, menguji, dan menyebarkan API.
    - Tidak digunakan untuk mengarang atau mengedit API, tetapi telah diperluas untuk mencakup analitik granular dan kemampuan untuk menambahkan kolaborator dengan status baca-saja.

- The Hasura CLI
  - V2:
    - CLI digunakan untuk berbagai tugas seperti mengelola metadata, menerapkan migrasi, dan bekerja dengan konfigurasi lingkungan.
    - Menyediakan antarmuka baris perintah untuk mengotomatisasi dan menskrip operasi ini, memudahkan integrasi Hasura ke dalam pipeline CI/CD.
  - V3:
    - CLI menjadi alat utama untuk membangun API.
    - Digunakan untuk membuat proyek lokal dan cloud, menyusun metadata, dan menciptakan build yang iteratif dan tidak dapat diubah dari API.
    - Memfasilitasi pekerjaan deklaratif dengan metadata Hasura dan menyediakan struktur folder dan file metadata baru untuk navigasi yang lebih intuitif.
      
- IDE Integrations
  - V2:
    - Integrasi IDE tidak tersedia, menyulitkan untuk bekerja dengan metadata dan file konfigurasi Hasura dalam editor kode favorit.
  - V3:
    - Integrasi IDE diperkenalkan untuk memudahkan bekerja dengan metadata Hasura dan mengarang API dari dalam editor.
    - Saat ini mendukung VS Code melalui ekstensi, dengan rencana untuk diperluas ke editor lainnya di masa depan

- Database Migrations
  - V2:
    - Migrasi database didukung melalui Hasura CLI, memungkinkan pengelolaan perubahan pada skema database dan metadata.
  - V3:
    - Migrasi database tidak didukung secara langsung. Namun, alternatif gratis seperti Flyway dan Liquibase dapat digunakan untuk mengelola perubahan skema database.

- Prometheus
  - V2:
    - Integrasi Prometheus hanya tersedia di edisi Cloud dan Enterprise untuk pemantauan dan pemberitahuan berdasarkan metrik API.
  - V3:
    - Ekspor Prometheus didukung secara native dan gratis untuk digunakan dengan mesin Hasura dan konektor data.

- The Hasura Console
  - V2:
    - OpenTelemetry hanya tersedia di edisi Cloud dan Enterprise untuk pelacakan terdistribusi dan observabilitas.
  - V3:
    - OpenTelemetry didukung secara native dan gratis untuk digunakan dengan mesin Hasura dan konektor data.
