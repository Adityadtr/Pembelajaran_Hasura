# Arsitektur Hasura DDN 

Arsitektur Hasura DDN dirancang untuk memastikan distribusi data yang cepat dan efisien melalui jaringan global. Konsep utamanya mirip dengan cara kerja CDN (Content Delivery Network), namun berfokus pada pengiriman dan sinkronisasi data melalui GraphQL.

# Komponen Arsitektur Hasura DDN

**1. Hasura Core (GraphQL Engine)**

   - Merupakan inti dari Hasura yang mengelola query dan mutation melalui GraphQL.
   - Berfungsi sebagai interface utama untuk menghubungkan aplikasi frontend dengan database backend, menjalankan query dan mutation, serta memberikan respons dalam format JSON.
   - Hasura Core ini tetap menjadi komponen sentral baik di Hasura DDN maupun versi tradisional Hasura tanpa DDN.

**2. Edge Nodes**

   - Edge Nodes adalah server yang ditempatkan di berbagai lokasi geografis untuk menyimpan salinan data cache yang lebih dekat dengan pengguna akhir.
   - Setiap kali permintaan query dilakukan oleh pengguna, Edge Node terdekat akan melayani permintaan tersebut, sehingga mengurangi latensi.
   - Jika data yang diminta tidak tersedia di cache Edge Node, server akan melakukan query ke database pusat atau cache di node lain.

**3. Caching Layer**

   - Lapisan cache ini berada di Edge Nodes dan dirancang untuk menyimpan data sementara yang sering diakses oleh pengguna.
   - Ketika permintaan query GraphQL dilakukan, caching layer akan memeriksa apakah data tersebut sudah ada di cache. Jika ada, data tersebut langsung dikirimkan ke pengguna, tanpa harus query ke database.
   - Caching policy diatur agar data yang lebih sering diakses tetap segar dan valid dengan sinkronisasi otomatis ke database pusat.

**4. Global Load Balancer**

   - Untuk mendistribusikan permintaan secara merata di antara Edge Nodes, Hasura DDN menggunakan load balancing. Ini memastikan bahwa permintaan data didistribusikan ke node yang paling sedikit bebannya dan paling dekat secara geografis dengan pengguna.
   - Load balancer ini bekerja secara otomatis dan dinamis berdasarkan kondisi traffic dan ketersediaan data di berbagai Edge Nodes.

**5. Real-time Sync**

   - Real-time synchronization adalah proses sinkronisasi otomatis antara data yang disimpan di Edge Nodes dengan database pusat.
   - Setiap perubahan yang dilakukan pada database utama akan segera direplikasi ke Edge Nodes agar data yang disajikan tetap mutakhir.
   - Hal ini memastikan bahwa data yang di-cache selalu konsisten dan sesuai dengan kondisi terbaru dari database pusat.

**6. Origin Database (Database Pusat)**

   - Origin database adalah sumber utama data yang diakses oleh GraphQL Engine dan Edge Nodes.
   - Meskipun Edge Nodes menangani sebagian besar permintaan, setiap query yang tidak bisa dilayani oleh cache akan diteruskan ke database pusat untuk pemrosesan lebih lanjut.
   - Arsitektur ini mendukung berbagai jenis database, seperti PostgreSQL, dengan integrasi penuh ke dalam stack Hasura.
  
# Cara Kerja Hasura DDN:

Berikut adalah langkah-langkah operasional cara kerja Hasura DDN saat permintaan data dilakukan:

**1. Pengguna Mengirim Query**

   - Aplikasi frontend mengirimkan query GraphQL dari pengguna ke Hasura DDN. Query ini dapat berupa permintaan data (query) atau pengubahan data (mutation).

**2. Edge Node Memproses Permintaan**

   - Edge Node terdekat memeriksa apakah data yang diminta sudah ada di cache lokal. Jika ada, data dikirim langsung dari cache kepada pengguna, mengurangi waktu respon secara signifikan.
   - Jika tidak ada data di cache, Edge Node akan meneruskan query tersebut ke database pusat atau ke Edge Node lain yang memiliki cache yang relevan.

**3. Load Balancer Memilih Node Terdekat**

   - Jika satu Edge Node tidak mampu melayani query, Load Balancer akan memilih node terdekat lainnya dengan beban yang lebih rendah.
   - Permintaan ini kemudian dialihkan ke Edge Node lain yang memiliki kapasitas dan data yang dibutuhkan.

**4. Caching dan Sinkronisasi**

   - Setelah query berhasil dijalankan oleh database pusat atau Edge Node lain, hasil query tersebut akan disimpan (di-cache) di Edge Node yang melakukan permintaan. Hal ini memastikan bahwa permintaan serupa di masa depan dapat dilayani dari cache tanpa harus mengakses database pusat lagi.
   - Sinkronisasi real-time memastikan bahwa data di cache selalu terbaru, terutama jika terjadi perubahan di database pusat.
     
**5. Pengiriman Data ke Pengguna**

   - Setelah data diperoleh dari cache atau database pusat, Edge Node akan mengirimkan respons JSON kembali ke aplikasi frontend melalui GraphQL.
