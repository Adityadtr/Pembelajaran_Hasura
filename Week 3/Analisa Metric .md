# Penambahan Environment YAML pada Rancher

Untuk mengaktifkan pengukuran metrics di Hasura, perlu dilakukan penambahan variabel lingkungan pada file konfigurasi YAML di Rancher. Berikut ini adalah langkah-langkahnya:

- HASURA_GRAPHQL_ENABLED_APIS: Untuk mengaktifkan API yang diperlukan.
- HASURA_GRAPHQL_METRICS_SECRET: Untuk menetapkan secret yang digunakan dalam otorisasi akses ke endpoint metrics.

![image](https://github.com/user-attachments/assets/65f2aeea-e532-41db-a68e-0c26f0f7114d)

# Menjalankan Endpoint Metrics

Setelah konfigurasi di atas, selanjutnya dapat menjalankan endpoint metrics menggunakan Postman dengan langkah berikut:

- Membuka postman, lalu membuat request baru dengan permintaan http dan metode get. dan masukkan endpointnya. disini saya menggunakan: http://10.100.14.8:8083/v1/metrics
- Setelah memasukan endpoint nya, permintaan belum bisa dapat dikirimkan (send), perlu menambahkan header otorisasi di postman.

  disini saya menambahkan header nya itu:

  key : ``Authorization``

  Value: ``Bearer hasura-rama``
- Setelah memasukkan header otorisasi nya, permintaan sudah bisa dapat dikirimkan(send).

  Hasil Output:

  ![image](https://github.com/user-attachments/assets/44ac493f-79ee-4850-b93e-1f8941b2f802)

# Analisis Output Metrics

Setelah berhasil melakukan request ke endpoint, akan mendapatkan output metrics dalam format Prometheus. Berikut adalah analisis dari beberapa metrics yang saya peroleh:

- ``hasura_action_request_bytes_total 0.0``

  Penjelasan: Total ukuran badan permintaan HTTP yang dikirim melalui aksi (experimental). Nilai saat ini adalah 0, menunjukkan tidak ada permintaan yang dikirim melalui aksi.

- ``hasura_action_response_bytes_total 0.0``

  Penjelasan: Total ukuran badan respons HTTP yang diterima melalui aksi (experimental). Nilai saat ini juga 0.

- ``hasura_active_subscription_pollers``

  Penjelasan: Menunjukkan jumlah aktif subscription pollers yang berjalan. Semua nilai adalah 0, menunjukkan tidak ada pollers aktif saat ini.

  Pollers adalah komponen dalam sistem yang secara teratur memeriksa atau "memantau" status atau data dari sumber tertentu

- ``hasura_active_subscription_pollers_in_error_state``

  Penjelasan: Menunjukkan jumlah pollers dalam keadaan error. Semua nilai adalah 0, yang berarti tidak ada pollers dalam keadaan error.

- ``hasura_cache_request_count counter``

  Penjelasan: Total permintaan masuk untuk pencarian cache. Nilai untuk status "hit" dan "miss" keduanya 0, menunjukkan tidak ada pencarian cache yang dilakukan.

- ``hasura_cron_events_invocation_total``

  Penjelasan: Jumlah total event cron yang diinvokasi. Semua status adalah 0, menunjukkan tidak ada event yang berhasil atau gagal diinvokasi.

- ``hasura_graphql_execution_time_seconds``

  Penjelasan: Menunjukkan waktu eksekusi dari permintaan GraphQL yang berhasil. Untuk query, total waktu eksekusi adalah 0.479872996 detik dengan 31 permintaan yang berhasil, menunjukkan waktu respons yang baik.

- ``hasura_graphql_requests_total``

  Penjelasan: Jumlah permintaan GraphQL yang diterima. Beberapa status menunjukkan 5 permintaan gagal untuk query "getTodoById" dan lainnya menunjukkan jumlah sukses untuk berbagai query.

- ``hasura_http_connections``

  Penjelasan: Jumlah koneksi HTTP aktif, dengan nilai 1, menunjukkan adanya koneksi aktif saat ini.

- ``hasura_http_request_bytes_total``

  Penjelasan: Total ukuran badan permintaan HTTP yang diterima. Nilai saat ini adalah 27396.0 bytes.

- ``hasura_http_response_bytes_total``

  Penjelasan: Total ukuran badan respons HTTP yang dikirim. Nilai saat ini adalah 159438.0 bytes.
