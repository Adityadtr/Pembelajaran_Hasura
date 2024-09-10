# Apa itu Redis

Redis adalah sebuah sistem penyimpanan data berbasis memori yang digunakan untuk menyimpan data dalam bentuk key-value. 

Artinya, Redis menyimpan data dengan cara mengasosiasikan nilai (value) dengan kunci (key) tertentu. Redis sering digunakan sebagai cache atau penyimpanan data sementara karena kecepatannya yang tinggi.

# Fitur Utama Redis

Penyimpanan di Memori: Redis menyimpan data di memori RAM, sehingga operasi baca dan tulis sangat cepat.

Struktur Data Beragam: Redis mendukung berbagai jenis struktur data, termasuk string, hash, list, set, dan sorted set.

Persistensi Data: Redis memiliki opsi untuk menyimpan data ke disk secara periodik untuk memastikan data tidak hilang meski server restart.

Replikasi dan Skalabilitas: Redis mendukung replikasi data untuk meningkatkan ketersediaan dan mendukung clustering untuk skalabilitas.

Contoh Penggunaan Redis:

Cache: Menyimpan data sementara seperti hasil query database untuk mempercepat akses data.

Session Storage: Menyimpan sesi pengguna dalam aplikasi web.

Queue: Mengelola antrean tugas yang harus diproses secara berurutan.

# Penggunaan Redis dalam Konteks Hasura

Cache untuk Query: Redis bisa digunakan untuk menyimpan cache hasil query GraphQL dari Hasura. Ini membantu mengurangi beban pada database dan mempercepat respons API.

Rate Limiting: Redis dapat digunakan untuk mengelola rate limiting API untuk membatasi jumlah permintaan yang dapat dilakukan oleh pengguna dalam periode waktu tertentu.

Session Management: Jika menggunakan Hasura untuk otentikasi, Redis dapat menyimpan sesi pengguna untuk autentikasi dan otorisasi.

# Replikasi dan Clustering

Replikasi :

Replikasi di Redis memungkinkan data dari satu server Redis (master) disalin ke satu atau lebih server Redis lainnya (slaves). Ini berguna untuk meningkatkan ketersediaan data dan menyeimbangkan beban baca. Berikut cara kerjanya:

Master dan Slave: Dalam arsitektur replikasi Redis, satu instance berfungsi sebagai master dan satu atau lebih instance berfungsi sebagai slave. Semua penulisan (write operations) terjadi pada master, dan slave hanya membaca (read operations) dari master.

Automatic Synchronization: Slave secara otomatis menyinkronkan data dari master ketika slave baru ditambahkan atau master di-restart.

Failover: Jika master gagal, salah satu slave dapat dipromosikan menjadi master untuk memastikan kelanjutan layanan. Proses ini sering dilakukan oleh alat seperti Redis Sentinel atau Redis Cluster.


Clustering:

Clustering di Redis adalah metode untuk membagi data ke beberapa node (shards) untuk skalabilitas horizontal. Dengan Redis Cluster, data dapat dipecah (sharded) ke beberapa server, dan Redis Cluster mengelola distribusi dan replikasi data.

Sharding: Data dibagi ke beberapa node berdasarkan hash slot. Redis Cluster membagi key menjadi 16.384 slot hash, dan setiap node menangani subset slot.

Replikasi dalam Cluster: Setiap node dalam cluster dapat memiliki satu atau lebih replika untuk meningkatkan ketersediaan. Data pada master disalin ke slave, mirip dengan replikasi di Redis.

# Perintah dan Manajemen

Perintah Dasar: Redis memiliki berbagai perintah untuk mengelola data. 

`SET key value`: Menyimpan nilai string pada kunci tertentu.

`GET key`: Mengambil nilai string dari kunci tertentu.

`DEL key`: Menghapus kunci dan nilai yang terkait.

`EXPIRE key seconds`: Mengatur waktu kadaluwarsa (TTL) untuk kunci.


Monitoring dan pengelolaan: Redis menyediakan berbagai perintah untuk memantau dan mengelola server:

`INFO`: Mengambil informasi status dari server Redis, termasuk statistik memori, replikasi, dan kinerja.

`MONITOR`: Menampilkan semua perintah yang diterima oleh server Redis secara real-time.

`SLOWLOG`: Memantau perintah yang memerlukan waktu lama untuk dieksekusi.


Manajemen memori:

`MEMORY STATS`: Menampilkan statistik penggunaan memori.

`CONFIG SET maxmemory`: Mengatur batas memori maksimum yang digunakan oleh Redis.


Keamanan:

`CONFIG SET requirepass`: Mengatur kata sandi untuk autentikasi.

`AUTH password`: Mengautentikasi pengguna dengan kata sandi.




