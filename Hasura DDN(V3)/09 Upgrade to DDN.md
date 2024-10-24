 # Pendahuluan
 
Hasura Data Delivery Network (DDN) menawarkan cara baru untuk membangun aplikasi dengan Hasura. Panduan ini membantu memahami perbedaan antara versi lama Hasura dengan Hasura DDN serta proses upgrade dan migrasi aplikasi yang ada.

# Alasan untuk Upgrade ke Hasura DDN

- Hasura DDN memberikan banyak fitur baru yang mempercepat pengembangan aplikasi.
- Dokumentasi ini menyediakan informasi untuk mengeksplorasi lebih dalam keunggulan Hasura DDN.

# Bagi Pengembang Individu

Hasura DDN menyediakan hosting API gratis bagi pengembang individu yang bekerja pada proyek kecil atau hobi.

- **Sebelum**: Terbatas pada model metadata Hasura v2 yang terikat dengan PostgreSQL dan GraphQL, dengan tantangan infrastruktur server dan biaya.
- **Sesudah**: Hasura DDN menangani hosting tanpa biaya, memberikan kemampuan untuk menambahkan logika bisnis dengan Typescript, Python, dan Go, serta menghilangkan masalah infrastruktur.

**Untuk Tim Kecil**:
Tim kecil dapat memanfaatkan Hasura DDN untuk mempercepat proses pengembangan dan mengurangi overhead dengan build yang tidak dapat diubah dan siklus pengembangan yang lebih sederhana.

- **Sebelum**: Hasura v2 menghambat proses deployment dan tidak ada kemampuan untuk preview atau rollback API.
- **Sesudah**: Hasura DDN memungkinkan prototipe cepat dengan build immutable dan deployment yang lebih konsisten.

**Untuk Tim Dewasa**:
Tim yang lebih besar dapat memanfaatkan Hasura DDN untuk menskalakan aplikasi dengan federasi bawaan dan lapisan akses data berbasis metadata, memungkinkan integrasi data tanpa perlu penulisan ulang yang signifikan.

- **Sebelum**: Metadata monolitik Hasura v2 memperlambat kolaborasi dan integrasi sumber data baru.
- **Sesudah**: Hasura DDN menyederhanakan integrasi sumber data dan pengelolaan API dengan lapisan metadata deklaratif yang mengelola kontrol di berbagai lingkungan.

**Kesimpulan**: Hasura DDN membantu pengembang dan tim dari semua ukuran dengan mengatasi masalah infrastruktur, meningkatkan fleksibilitas, dan menyediakan cara yang lebih efisien untuk mengelola API di berbagai lingkungan.
