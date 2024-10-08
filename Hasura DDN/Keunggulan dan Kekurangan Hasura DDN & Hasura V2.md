# Keunggulan 

**A. Hasura V2**

1. Antarmuka Pengguna yang Ramah:

   - Console menyediakan antarmuka grafis yang intuitif untuk mengonfigurasi dan mengelola API dan sumber data, memudahkan pengguna tanpa pengalaman teknis yang mendalam.

2. Migrasi Database Terintegrasi:

   - Mendukung migrasi database secara langsung melalui CLI, memungkinkan pengelolaan skema dan metadata yang lebih mudah dan terorganisir.

3. Monitoring dan Pemberitahuan:

   - Integrasi dengan Prometheus untuk monitoring dan alerting, memungkinkan pengguna mendapatkan wawasan yang lebih baik mengenai performa API.

4. OpenTelemetry untuk Observabilitas:

   - Tersedia untuk edisi Cloud dan Enterprise, memberikan kemampuan pelacakan terdistribusi yang berguna untuk aplikasi skala besar.
  
**B. Hasura DDN (V3)**

1. Perbaikan Console:

   - Console berfungsi lebih sebagai alat eksplorasi dan manajemen, dengan fitur analitik granular dan kemampuan untuk menambahkan kolaborator dengan status baca-saja, mempercepat proses kolaborasi.

2. CLI yang Kuat:

   - CLI menjadi alat utama untuk membangun API, memberikan kemampuan untuk menyusun metadata dan menciptakan build yang tidak dapat diubah, memudahkan otomatisasi dan integrasi ke dalam CI/CD.

3. Integrasi IDE:

   - Memperkenalkan dukungan untuk integrasi IDE (seperti VS Code), yang memungkinkan pengembang bekerja dengan metadata dan API langsung dari dalam editor, meningkatkan produktivitas.

4. Dukungan untuk Monitoring dan Observabilitas:

   - Menyediakan dukungan native untuk Prometheus dan OpenTelemetry, memungkinkan pemantauan dan pelacakan yang lebih baik secara gratis.

# Kekurangan 

**A. Hasura V2**

1. Keterbatasan Integrasi IDE:

   - Tidak adanya integrasi IDE membuat proses pengembangan lebih sulit bagi pengembang yang terbiasa dengan alat pengembangan modern.

2. Kurangnya Fleksibilitas dalam Pengelolaan API:

   - Penggunaan console sebagai alat utama untuk pengaturan API membatasi kemampuan pengguna untuk melakukan perubahan besar dalam skema dan struktur API.

3. Fitur Monitoring Terbatas pada Edisi Tertentu:

   - Beberapa fitur seperti Prometheus dan OpenTelemetry hanya tersedia di edisi berbayar, membatasi akses untuk pengguna di edisi gratis.
  
**B. Hasura DDN (V3)**

1. Tidak Ada Dukungan untuk Migrasi Database Terintegrasi:

   - Migrasi database tidak didukung secara langsung, mengharuskan pengguna untuk bergantung pada alat pihak ketiga seperti Flyway atau Liquibase.

2. Perubahan Paradigma Penggunaan Console:

   - Meskipun memperbaiki fungsi, perubahan fokus dari pengeditan ke eksplorasi bisa menjadi kendala bagi pengguna yang terbiasa dengan cara kerja sebelumnya.

3. Kurva Pembelajaran untuk Pengguna Baru:

   - Perubahan dalam struktur dan cara penggunaan CLI dan console kemungkinan memerlukan waktu adaptasi bagi pengguna baru yang tidak terbiasa dengan model baru.
