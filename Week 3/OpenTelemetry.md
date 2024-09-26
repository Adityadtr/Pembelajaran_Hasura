# Pengertian OpenTelemetry (OTel)

**OpenTelemetry (OTel)** adalah proyek open-source yang menyediakan kerangka kerja untuk mengumpulkan, memproses, dan mengirimkan data observabilitas seperti traces, metrics, dan logs dari aplikasi. OTel mendukung berbagai bahasa pemrograman dan platform, memungkinkan pengembang untuk mengintegrasikan observabilitas ke dalam aplikasi mereka dengan mudah.

**Fitur Utama OTel:**
- Traces: Mencatat perjalanan dan waktu eksekusi fungsi dalam aplikasi.
- Metrics: Mengumpulkan data statistik tentang performa aplikasi, seperti latensi dan throughput.
- Logs: Menyediakan informasi terkait kejadian yang terjadi dalam aplikasi.

# Kegunaan OpenTelemetry pada Hasura

**Integrasi OpenTelemetry dalam Hasura memungkinkan pengembang untuk:**

- Memantau Performa: Mengidentifikasi bottleneck dan masalah kinerja dengan analisis trace dan metrics.
- Debugging: Melihat logs untuk mendiagnosis masalah saat menjalankan query atau mutasi.
- Optimasi: Menggunakan data yang dikumpulkan untuk mengoptimalkan performa aplikasi.

# OTel Exporter pada Hasura

![image](https://github.com/user-attachments/assets/657befa3-b33e-487d-8772-22c282038f19)

Exporter di Hasura berfungsi untuk mengirim data yang dikumpulkan ke sistem pemantauan eksternal seperti Jaeger atau Prometheus. Dengan mengkonfigurasi OTel exporter, dapat mengarahkan data observabilitas ke sistem yang lebih kompleks untuk analisis lebih lanjut.

# Endpoint Traces, Metrics, dan Logs

![image](https://github.com/user-attachments/assets/99daeaaa-89b4-45e3-b629-d13c16572901)

untuk melakukan pengisian endpoint pada traces, metrics dan logs, dapat membukanya di halaman setting hasura yang ada simbol roda bergerigi, diklik lalu lihat tulisan atau pilihan opentelemetry exporter. kemudian isikan endpoint pada traces, metric dan logs. jika sudah isikan batch size, trace propagations, headers(optional), attribute(optional). Penjelasan dibawah ini: 

1. Traces Endpoint

   Pengertian: Endpoint traces digunakan untuk mengumpulkan informasi tentang query yang dijalankan oleh Hasura. Ini membantu dalam memahami performa query dan menemukan bottleneck.

   Pengisian: http://10.100.13.205:4318/v1/traces

   Perkiraan/Menduga/seharusnya: Endpoint ini dapat terhubung ke alat pemantauan seperti OpenTelemetry atau Jaeger.

2. Metrics Endpoint

   Pengertian: Endpoint metrics memberikan informasi statistik tentang penggunaan dan performa Hasura, seperti jumlah query yang dieksekusi, latensi, dan penggunaan resource.

   Pengisian: http://10.100.13.205:4318/v1/metrics

   Perkiraan/Menduga/seharusnya: Endpoint ini dapat dihubungkan dengan sistem monitoring seperti Prometheus untuk mengumpulkan dan menganalisis metrik.

3. Logs Endpoint

   Pengertian: Endpoint logs menangkap log dari Hasura, yang bisa membantu dalam debugging dan analisis kesalahan.

   Pengisian: http://10.100.13.205:4318/v1/logs

   Perkiraan/Menduga/seharusnya: mengarahkan logs ke sistem log management seperti Elasticsearch, Grafana Loki, atau sistem logging lainnya.

4. Batch Size

   Pengertian: digunakan untuk mengontrol berapa banyak data yang akan dikirimkan dalam satu batch.

   Pengisian: 512 (default)

   Perkiraan/Menduga/seharusnya: Semakin besar batch size, semakin banyak data yang dikirim sekaligus. Ini dapat mempengaruhi performa dan latensi pengiriman data observabilitas.

5. trace propagations

   Pengertian: Ini adalah format untuk menyebarkan trace antara layanan yang berbeda. Pilih salah satu dari B3 atau tracecontext. 

   Pengisian:

   - B3 sering digunakan dalam sistem observasi seperti Zipkin.
   - tracecontext lebih umum digunakan dalam konteks distribusi trace antar layanan dalam OpenTelemetry.

7. Headers (optional)

   Pengertian: dapat menambahkan headers jika diperlukan, misalnya untuk otentikasi ke OpenTelemetry endpoint atau collector.

5. Attributes (Optional)

   Pengertian: dapat menambahkan atribut khusus untuk tracing, logs, atau metrics yang dikirimkan. Atribut ini biasanya berupa metadata yang relevan untuk operasi yang sedang dilakukan, seperti nama layanan atau informasi pengguna.
   
# Menganalisis config.yaml

Pengertian: File config.yaml adalah konfigurasi utama untuk OpenTelemetry Collector, yang mendefinisikan cara penerimaan, pemrosesan, dan pengiriman data observabilitas.

Untuk melihat konfigurasi isi pada Otel: 

- Saya perlu masuk ke server dengan menggunakan ssh dengan ``ssh root@10.100.13.205``.
  
  ![image](https://github.com/user-attachments/assets/c1fcf95e-a915-4a7d-973e-ce3652bccd6a)

- Selanjutnya, masuk ke direktori konfigurasi OpenTelemetry dengan perintah ``cd /etc/otelcol``.

  ![image](https://github.com/user-attachments/assets/8667c9ed-231e-416f-876c-77140067010b)

- Setelah berada di direktori /etc/otelcol, dapat menggunakan perintah cat untuk melihat isi file konfigurasi. dengan perintah ``cat config.yaml``
- Lalu Hasil outputnya menampilkan isi file konfigurasi otel tersebut.

  ![image](https://github.com/user-attachments/assets/3aba7c8f-2cdb-49a8-8722-417f8f5ddc10)

  Pastikan untuk memeriksa bagian seperti:

  - Receivers: Menentukan bagaimana data diterima.
  - Processors: Menentukan bagaimana data diproses.
  - Exporters: Menentukan ke mana data akan diekspor.

1. Analisa Extensions

```
extensions:
  health_check:
  pprof:
    endpoint: 0.0.0.0:1777
  zpages:
    endpoint: 0.0.0.0:55679
```
  - health_check: Mengaktifkan pemeriksaan kesehatan untuk memastikan bahwa collector berfungsi dengan baik.
  - pprof: Endpoint ini digunakan untuk profiling kinerja aplikasi. 
  - zpages: Menyediakan endpoint untuk pengumpulan z-pages yang berguna untuk pemantauan kinerja secara real-time.

2. Analisa Receivers

```
receivers:
  otlp:
    protocols:
      grpc:
        endpoint: 0.0.0.0:4317
      http:
        endpoint: 0.0.0.0:4318

  opencensus:
    endpoint: 0.0.0.0:55678

  # Collect own metrics
  prometheus:
    config:
      scrape_configs:
      - job_name: 'otel-collector'
        scrape_interval: 10s
        static_configs:
        - targets: ['0.0.0.0:8888']

  jaeger:
    protocols:
      grpc:
        endpoint: 0.0.0.0:14250
      thrift_binary:
        endpoint: 0.0.0.0:6832
      thrift_compact:
        endpoint: 0.0.0.0:6831
      thrift_http:
        endpoint: 0.0.0.0:14268

  zipkin:
    endpoint: 0.0.0.0:9411
```
  - OTLP: Menerima data observabilitas melalui protokol gRPC dan HTTP pada port 4317 dan 4318.
  - OpenCensus: Menerima data pada port 55678.
  - Prometheus: Mengumpulkan metrics dari target yang ditentukan pada port 8888 setiap 10 detik.
  - Jaeger dan Zipkin: Menyediakan beberapa protokol untuk menerima data traces pada port-port yang telah ditentukan.

3. Analisa Processors

```
processors:
  batch:
```
  - Batch Processor: Mengelompokkan data sebelum diekspor, mengurangi overhead dari banyak pengiriman data kecil.

4. Analisa Exporters

```
exporters:
  debug:
    verbosity: detailed
```
  - Debug Exporter: Menampilkan data yang dikumpulkan untuk tujuan debugging. Ini berguna untuk melihat data mentah yang masuk ke collector.

5. Analisa Services

```
service:
  pipelines:
    traces:
      receivers: [otlp, opencensus, jaeger, zipkin]
      processors: [batch]
      exporters: [debug]

    metrics:
      receivers: [otlp, opencensus, prometheus]
      processors: [batch]
      exporters: [debug]

    logs:
      receivers: [otlp]
      processors: [batch]
      exporters: [debug]

  extensions: [health_check, pprof, zpages]
```
  - Pipelines: Menentukan alur data observabilitas. Setiap pipeline memiliki bagian penerima, pemroses, dan pengeksport. Ini memungkinkan Anda untuk mengatur bagaimana data ditangani:
  - traces: Menerima data traces dari berbagai sumber dan mengekspornya setelah diproses.
  - metrics: Mengumpulkan metrics dari berbagai sumber dan mengirimkannya untuk analisis.
  - logs: Menangani logs dari sumber yang ditentukan dan mengekspornya setelah pemrosesan.

# journalctl

Pengertian:

``journalctl`` adalah alat baris perintah yang digunakan untuk melihat log dari sistem yang menggunakan systemd sebagai sistem init. Ini sangat berguna untuk menganalisis status dan keluaran log dari layanan yang berjalan di server, termasuk OpenTelemetry Collector

Berikut adalah langkah-langkah untuk menganalisis dengan journalctl:

1. Melihat Log Layanan

   Untuk melihat log dari OpenTelemetry Collector, dapat menggunakan perintah berikut:

```
journalctl -u otelcol -f
```
  - -u otelcol: Mengindikasikan bahwa Anda ingin melihat log untuk unit layanan yang bernama otelcol (pastikan nama unit layanan sesuai dengan yang digunakan di sistem Anda).
  - -f: Mengikuti log secara real-time, sehingga Anda dapat melihat log terbaru saat mereka muncul.

  ![image](https://github.com/user-attachments/assets/4c54ffac-0a21-4b3f-9a44-bf003d8e925b)

2. Filter Berdasarkan Waktu

   **Bisa dapat memfilter log berdasarkan waktu. Misalnya, untuk melihat log dari hari ini:**

```
journalctl -u otelcol --since "today"
```
  ![image](https://github.com/user-attachments/assets/cf2e4be8-c474-489c-a4b4-8fcaebd85624)

  **Atau untuk melihat log selama 1 jam terakhir:**

```
journalctl -u otelcol --since "1 hour ago"
```
  ![image](https://github.com/user-attachments/assets/3d121852-aa8d-41f6-bdc2-c703c5778145)
