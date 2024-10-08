# Arsitektur dan Desain

**A. Hasura DDN:**

  - Dirancang untuk distribusi data yang cepat dan efisien melalui jaringan global dengan menggunakan konsep Edge Nodes.
  - Memungkinkan caching dan sinkronisasi real-time, sehingga meningkatkan kinerja dan mengurangi latensi untuk aplikasi yang melayani pengguna di berbagai lokasi.
  - Memanfaatkan load balancer untuk mendistribusikan permintaan secara dinamis di antara Edge Nodes.

**B. Hasura V2:**

  - Memiliki arsitektur monolitik yang lebih tradisional dan fokus pada pengelolaan query dan mutation di satu titik pusat.
  - Meskipun sudah mendukung pengelolaan data yang efisien, V2 tidak memiliki kemampuan distribusi data yang seefisien DDN.
  - V2 lebih cocok untuk aplikasi dengan pengguna yang terpusat di satu lokasi atau negara.

# Fitur Caching

**A. Hasura DDN:**

  - Memiliki caching layer yang kuat di Edge Nodes, memungkinkan pengambilan data yang lebih cepat untuk permintaan yang berulang.
  - Data yang sering diakses dapat disimpan di cache, sehingga mengurangi beban pada database pusat dan meningkatkan waktu respon.
    
**B. Hasura V2:**

  - Tidak memiliki fitur caching yang terdistribusi. Semua permintaan data dilakukan langsung ke database pusat, yang dapat menyebabkan latensi lebih tinggi jika banyak pengguna yang mengakses data secara bersamaan.
  - V2 masih dapat melakukan caching dalam konteks tertentu, tetapi tidak seefisien DDN dalam pengelolaan dan distribusi data.

# Sinkronisasi Data

**A. Hasura DDN:**

  - Menyediakan sinkronisasi real-time antara data yang disimpan di Edge Nodes dan database pusat, memastikan data yang disajikan selalu mutakhir.
  - Memungkinkan pembaruan otomatis data di cache setiap kali terjadi perubahan di database pusat.
    
**B. Hasura V2:**

  - Meskipun mendukung pembaruan data melalui mutasi GraphQL, tidak ada mekanisme sinkronisasi otomatis untuk menjaga data tetap segar seperti yang terdapat di DDN.
  - Pembaruan data harus dilakukan secara manual melalui query atau mutasi oleh pengembang.

# Kinerja dan Latensi

**A. Hasura DDN:**

  - Mampu mengurangi latensi secara signifikan dengan menyajikan data dari Edge Nodes terdekat dan caching yang efisien.
  - Didesain untuk menghadapi skenario dengan traffic tinggi, menjadikannya pilihan yang baik untuk aplikasi global.
    
**B. Hasura V2:**

  - Latensi lebih tinggi karena semua permintaan data diproses melalui database pusat tanpa memanfaatkan caching terdistribusi.
  - Kinerja mungkin menurun jika ada lonjakan permintaan dari banyak pengguna secara bersamaan.

# Kesimpulan:
Hasura DDN dan Hasura V2 memiliki tujuan yang berbeda sesuai dengan kebutuhan penggunanya. 

DDN adalah pilihan yang tepat untuk aplikasi global yang memerlukan pengiriman data yang cepat dan efisien, 

sedangkan V2 lebih baik untuk aplikasi yang lebih kecil atau yang beroperasi dalam konteks yang lebih terpusat. Pemilihan antara keduanya tergantung pada skala aplikasi, kebutuhan latensi, dan arsitektur yang diinginkan.
