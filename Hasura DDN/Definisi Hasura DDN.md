# Apa itu Hasura DDN

Hasura DDN (Data Delivery Network) adalah teknologi terbaru yang dikembangkan oleh Hasura untuk mempercepat pengiriman dan distribusi data ke aplikasi yang menggunakan GraphQL. 

Hasura DDN bekerja seperti Content Delivery Network (CDN) untuk data, dengan tujuan utama meningkatkan performa aplikasi, mengurangi latensi, dan memberikan pengalaman pengguna yang lebih responsif, terutama untuk aplikasi yang melayani pengguna di berbagai lokasi geografis.

# Fungsi Utama Hasura DDN:

- **Pengoptimalan Kinerja**: DDN membantu mengurangi waktu respon saat mengirim data dari database ke pengguna.
- **Caching Data**: DDN menyimpan data di server yang lebih dekat dengan pengguna, sehingga mempercepat pengiriman data yang sering diminta.
- **Distribusi Global**: Memungkinkan data diakses dari lokasi terdekat pengguna di seluruh dunia melalui node distribusi yang tersebar secara global.
- **Auto-scaling**: DDN mampu mengelola peningkatan jumlah permintaan secara otomatis, menjaga performa aplikasi tetap stabil meskipun beban meningkat.

# Cara Kerja Hasura DDN:

Hasura DDN terdiri dari beberapa komponen inti yang bekerja bersama untuk memastikan data didistribusikan secara efisien ke seluruh dunia. Berikut adalah cara kerjanya:

- **Edge Nodes**: Ini adalah server yang ditempatkan di berbagai wilayah geografis, yang berfungsi untuk menyimpan dan menyajikan data dari cache yang lebih dekat ke pengguna akhir.
- **Caching Layer**: Setiap edge node memiliki lapisan cache yang menyimpan data yang sering diakses, sehingga query tidak selalu harus mencapai database utama. Hal ini mengurangi waktu respons.
- **Load Balancing**: Untuk memastikan bahwa beban permintaan query terdistribusi secara merata ke berbagai node, load balancing dilakukan secara otomatis, sehingga tidak ada satu server yang mengalami overload.
- **Real-time Data Sync**: Hasura DDN juga menyinkronkan data secara real-time antara edge nodes dan database utama, memastikan data yang diberikan selalu konsisten dan terbaru.
