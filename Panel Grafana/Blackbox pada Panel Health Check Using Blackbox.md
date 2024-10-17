# Penjelasan Umum

- Blackbox dalam umum digunakan dalam dunia pengujian untuk menggambarkan pendekatan di mana sistem diuji tanpa mengetahui detail internalnya.
- Dalam konteks monitoring, Blackbox digunakan untuk memantau performa layanan dari luar, dengan berfokus pada keluaran yang dihasilkan oleh sistem.
- Di Grafana, Blackbox digunakan bersama Prometheus Blackbox Exporter untuk melakukan berbagai jenis pemeriksaan kesehatan terhadap aplikasi atau layanan.

# Blackbox

- Blackbox adalah komponen penting yang digunakan untuk memantau kesehatan layanan dengan cara melakukan probe(pengujian) dari luar(eksternal) tanpa masuk ke dalam sistem itu sendiri.
- Blackbox Exporter merupakan sebuah Prometheus Exporter yang digunakan untuk menjalankan berbagai macam probe (pengujian dari luar) untuk memeriksa apakah aplikasi atau layanan Anda berjalan dengan baik.

Dengan Blackbox, dapat melakukan monitoring untuk:

- Layanan HTTP atau HTTPS.
- Layanan TCP.
- Layanan DNS.
- ICMP ping (untuk memeriksa apakah host merespons).

Ini sangat berguna dalam konteks health check di mana, jika ingin tahu apakah layanan tersedia dan merespons dengan benar dari perspektif pengguna.

# Blackbox Bekerja Dalam Grafana

- Dalam panel Health Check using Blackbox, berarti digunakan untuk memeriksa apakah sistem (misalnya server, API, atau layanan lain) berjalan dengan benar dengan cara mensimulasikan permintaan yang akan dilakukan oleh pengguna nyata. Jika respons yang diberikan sistem sesuai dengan yang diharapkan, berarti sistem sehat (healthy).

- Di Grafana, panel Health Check using Blackbox mengintegrasikan Blackbox Exporter dari Prometheus untuk melakukan pemeriksaan berkelanjutan pada endpoint seperti GraphQL, REST API, atau layanan lainnya yang berjalan di server Anda. Blackbox Exporter akan memeriksa endpoint ini dan melaporkan hasilnya ke Prometheus, yang kemudian divisualisasikan di dashboard Grafana.

# Alur Kerja Blackbox Exporter

![image](https://github.com/user-attachments/assets/3bc9944d-cd69-46f7-a460-eb08e619375f)


Gambar diatas tersebut menunjukkan alur kerja Blackbox Exporter dalam sistem monitoring menggunakan Prometheus. Berikut adalah penjelasan mengenai alur di gambar tersebut:

1. Prometheus: Prometheus adalah sistem monitoring yang melakukan scraping data dari berbagai exporter (termasuk Blackbox Exporter) untuk memantau metrik dari layanan atau sistem yang dipantau. Pada gambar ini, Prometheus mengirimkan HTTP request ke Blackbox Exporter.

2. HTTP Request (module, target): Prometheus mengirimkan HTTP request ke Blackbox Exporter, yang berisi informasi mengenai modul dan target yang akan diuji. Modul di sini menentukan jenis probe yang akan dilakukan (misalnya HTTP, ICMP, DNS), dan target adalah layanan atau endpoint yang akan diuji.

3. Blackbox Exporter: Blackbox Exporter melakukan probe ke target berdasarkan instruksi yang diberikan oleh Prometheus. Ini dapat berupa tes HTTP (untuk melihat apakah suatu endpoint tersedia), ICMP (ping untuk memeriksa apakah host aktif), atau jenis tes lainnya.

4. Probe is launched against target: Blackbox Exporter meluncurkan probe atau pengujian terhadap target yang diminta. Target ini bisa berupa layanan, server, API, atau endpoint lain yang ingin diuji kesehatannya.

5. Probe returns data: Setelah probe dilakukan, Blackbox Exporter mengumpulkan data dari target, seperti status respon (misalnya kode status HTTP 200, jika sukses), waktu respon (latency), atau informasi lainnya tergantung pada jenis probe yang digunakan.

6. HTTP Response (in Prometheus format): Setelah mendapatkan data dari probe, Blackbox Exporter mengirimkan hasilnya kembali ke Prometheus dalam format yang dimengerti oleh Prometheus, biasanya berupa metrik yang dapat di-scrape dan disimpan oleh Prometheus untuk analisis lebih lanjut.

7. Target: Target yang diuji bisa berupa aplikasi, API, layanan, atau infrastruktur lainnya yang ingin dipantau kesehatannya. Blackbox Exporter melakukan probe untuk mengumpulkan informasi terkait performa target tersebut.

Kesimpulan alurnya:

- Prometheus menginisiasi probe melalui Blackbox Exporter untuk memonitor status kesehatan suatu target.
- Blackbox Exporter melakukan pengujian eksternal terhadap target tersebut.
- Data hasil pengujian dikembalikan ke Prometheus dalam format metrik untuk dianalisis dan divisualisasikan di dashboard monitoring seperti Grafana.

# Integrasi Blackbox dengan Grafana

Anda bisa melakukan integrasi blackbox pada grafana, dengan melakukan penginstalan blackbox exporter terlebih dahulu. atau bisa juga dengan mengikuti panduan penginstalan dari web https://geekflare.com/monitor-website-with-blackbox-prometheus-grafana/

Secara ringkas, tahapan umumnya ialah:

- Install Prometheus Blackbox Exporter
- Konfigurasi Prometheus untuk Blackbox: Tambahkan pengaturan Blackbox Exporter di file konfigurasi Prometheus
- Visualisasi di Grafana: Setelah Prometheus mengumpulkan data dari Blackbox Exporter, anda dapat menampilkan metrik ini di Grafana. Misalnya, Anda bisa menampilkan grafik uptime, latency, atau status HTTP dari endpoint yang dipantau.

