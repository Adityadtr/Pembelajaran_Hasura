# Pengertian OSI Layer:
Pada tahun 1970, terdapat organisasi yang bernama International Organization for Standardization (ISO) yang berlokasi di eropa, telah mengembangkan sebuah model arsitektural jaringan yang diberi nama OSI Reference Model for Open Networking (Model Jaringan Terbuka OSI). OSI tersebut mempunyai 7 layer yang memiliki fungsi masing-masing. 
Open System Interconnection atau OSI adalah sebuah kerangka konseptual yang digunakan untuk memahami bagaimana berbagai protokol jaringan berinteraksi dalam sebuah sistem jaringan komputer.

![image](https://github.com/user-attachments/assets/2deedd06-5fbe-428a-a9d3-db5dc4fd78c6)

# 7 OSI LAYER

1. Application Layer (Lapisan Ke - 7)                                                                                             

   Application Layer adalah bagian dari jaringan yang paling dekat dengan pengguna. Di sinilah terjadinya pengguna berinteraksi      langsung dengan aplikasi yang memanfaatkan jaringan, seperti web browser atau email. Lapisan ini bertanggung jawab untuk          mengatur bagaimana aplikasi menggunakan jaringan dan memastikan bahwa aplikasi dapat berfungsi dengan baik menggunakan sumber     daya yang ada di jaringan.
   
   Jika terjadi masalah saat aplikasi mencoba menggunakan jaringan, lapisan ini juga bisa memberikan pesan kesalahan kepada          pengguna.

   Beberapa contoh layanan dan protokol yang beroperasi pada lapisan ini adalah HTTP (digunakan untuk browsing web), SMTP            (digunakan untuk email), dan FTP (digunakan untuk transfer file).
   
2. Presentation Layer (Lapisan Ke - 6)

   Presentation Layer bertugas untuk mengubah data dari aplikasi menjadi format yang bisa ditransmisikan melalui jaringan.           Lapisan ini memastikan bahwa data yang dikirimkan oleh aplikasi di satu perangkat bisa dipahami oleh aplikasi di perangkat        lain.Fungsi utama lapisan ini termasuk mengubah format data, mengenkripsi (mengamankan) data, dan mengompresi (mengurangi         ukuran) data.
   Beberapa contoh protokol di lapisan ini adalah SSL/TLS (yang digunakan untuk keamanan), serta format data seperti JPEG, PNG,      dan ASCII. Jadi, lapisan ini bertanggung jawab memastikan data yang dikirim bisa dibaca dengan benar dan aman oleh perangkat      lain.
   
3. Session Layer (Lapisan Ke - 5)
   
   Session Layer adalah lapisan yang bertanggung jawab untuk mengatur, mengelola, dan mengakhiri sesi komunikasi antara dua          perangkat di jaringan. Ini memastikan bahwa komunikasi bisa dimulai, diatur dengan baik, dan diakhiri dengan benar.
   Beberapa protokol yang bekerja di lapisan ini adalah NFS (untuk berbagi file di jaringan), SMB (untuk berbagi file di jaringan    Windows), dan RTP (untuk streaming media).
   
4. Transport Layer (Lapisan Ke - 4)
  
   Transport Layer bertugas untuk membagi data menjadi paket-paket kecil dan memberi nomor pada setiap paket sehingga bisa           disusun kembali dengan benar saat tiba di tujuan. Di lapisan ini, protokol seperti TCP dan UDP digunakan untuk mengirim data.
    * TCP (Transmission Control Protocol) memastikan bahwa setiap paket data sampai dengan benar dan lengkap. Jika ada paket yang       hilang atau rusak, TCP akan mengirimkannya kembali.
    * UDP (User Datagram Protocol) lebih cepat, tetapi tidak menjamin semua paket akan sampai.
      Lapisan ini juga memastikan data dikirimkan tanpa kesalahan, mengatur aliran data, dan memeriksa serta memperbaiki                kesalahan yang mungkin terjadi.
      
5. Network Layer (Lapisan Ke – 3)

   Network Layer bertanggung jawab untuk menambahkan header pada paket data yang berisi informasi alamat IP, termasuk IP             pengirim dan IP tujuan. Header ini membantu memastikan bahwa data dikirim ke tempat yang benar.
   Lapisan ini juga mengatur proses routing, yaitu memilih jalur terbaik untuk mengirimkan data melalui jaringan yang berbeda,       dengan bantuan perangkat seperti router dan switch pada lapisan ini.
   Contoh dari protokol dan perangkat di lapisan ini adalah IP (Internet Protocol) untuk pengalamatan, router untuk mengarahkan      data, dan penggunaan alamat IP untuk mengidentifikasi perangkat di jaringan.
   
6. Data-Link-Layer (Lapisan Ke – 2)

   Data Link Layer bertanggung jawab untuk transfer data antara dua perangkat yang terhubung langsung. Lapisan ini mengatur          bagaimana data dibingkai dalam format yang disebut frame, serta mendeteksi dan memperbaiki kesalahan yang mungkin terjadi pada    lapisan fisik.

   Komponen dan Protokol:
   MAC (Media Access Control): Mengatur akses ke media fisik dan menangani pengalamatan hardware. Contoh metode: 
      - CSMA/CD (Carrier Sense Multiple Access with Collision Detection): Digunakan di Ethernet. Memeriksa apakah jaringan                tersedia sebelum mengirim data. Jika terjadi tabrakan, pengiriman diulang secara acak.
      - CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance): Digunakan untuk menghindari tabrakan dengan                      menganalisis jaringan sebelum mengirim data dan menggunakan sinyal broadcast.
    Contoh perangkat:
      - Ethernet: Protokol untuk komunikasi data.
      - MAC Address: Alamat fisik perangkat.
      - Switch dan Bridge: Perangkat yang menghubungkan dan mengarahkan data dalam jaringan.
    Lapisan ini memastikan data dikirim dengan benar antar perangkat dan mengatur bagaimana perangkat seperti hub, repeater,          switch, dan bridge beroperasi pada level ini.
  
7. Physical Layer (Lapisan Ke – 1)

   Physical Layer adalah lapisan yang menangani semua aspek fisik dari koneksi jaringan. Ini termasuk kabel, sinyal, konektor,       dan media transmisi yang digunakan untuk mengirimkan data.
   Contoh perangkat:
      - Kabel Ethernet
      - Sinyal listrik
      - Konektor RJ45
      - Hub dan repeater
    Lapisan ini juga menjelaskan bagaimana perangkat seperti NIC (Network Interface Card) berinteraksi dengan media kabel atau        perangkat radio. Proses di layer ini mirip dengan mengirim surat, data dikodekan dalam format yang bisa dikirim melalui media     jaringan.

# Fungsi OSI Layer:

1. Fungsi Physical: 
    - Media Transmisi: Menentukan jenis kabel atau media lain yang digunakan (misalnya, kabel Ethernet).
    - Sinkronisasi Bit: Mengatur bagaimana bit data disinkronkan untuk transmisi.
    - Metode Pensinyalan: Mengatur cara sinyal dikirim melalui media.
    - Arsitektur Jaringan: Menentukan bagaimana kabel dan perangkat jaringan dihubungkan, seperti Ethernet dan topologi jaringan.
2. Data Link: 
    - Pembentukan Frame: Data diorganisir dalam frame untuk transmisi.
    - Koreksi Kesalahan: Mengidentifikasi dan memperbaiki kesalahan yang terjadi saat data dikirim.
    - Flow Control: Mengatur aliran data untuk mencegah overloading.
    - Pengalamatan Hardware: Menggunakan alamat MAC (Media Access Control) untuk mengidentifikasi perangkat di jaringan.
3. Network:
   Mampu menyediakan logical addressing dan menentukan rute tujuan secara tepat.
4. Transport:
   Menyediakan reliable atau unreliable delivery, serta mengecek terjadinya koneksi error sebelum melakukan transmisi data.
5. Session:
   Memisakan data dalam berbagai aplikasi.
6. Presentation:
   Mampu menyajikan data serta menangani enkripsi data dengan cepat.
7. Application:
   Menyediakan tampilan antarmuka (user interface) page pengguna.

# Alur Data

Alur Data dari Pengirim ke Penerima
1. Application Layer:
   Data dimulai dari aplikasi dan siap untuk dikirim.
2. Presentation Layer:
   Data diubah atau diubah formatnya agar dapat dipahami oleh penerima.
3. Session Layer:
   Mengelola sesi komunikasi dan memastikan sesi tetap terbuka selama transfer data.
4. Transport Layer:
   Data dipecah menjadi segmen dan dikendalikan alirannya untuk pengiriman yang andal.
5. Network Layer:
   Data dipaketkan dengan alamat IP dan dipilih jalurnya untuk dikirim melalui jaringan.
6. Data Link Layer:
    Data dibingkai dan dikendalikan kesalahannya dalam jaringan lokal.
7. Physical Layer:
    Data diubah menjadi sinyal fisik dan dikirim melalui media transmisi seperti kabel atau radio.
    
Alur Data dari Penerima ke Pengirim
1. Physical Layer:
   Menerima sinyal fisik dari media transmisi.
2. Data Link Layer:
   Menghilangkan frame dan memeriksa kesalahan.
3. Network Layer:
   Mengarahkan paket data ke tujuan yang benar.
4. Transport Layer:
   Menggabungkan segmen data menjadi data utuh.
5. Session Layer:
   Mengelola sesi komunikasi yang ada.
6. Presentation Layer:
   Mengubah format data agar dapat dipahami oleh aplikasi.
7. Application Layer:
   Data diterima oleh aplikasi dan digunakan oleh pengguna.

# Cara Memahami OSI Layer : 

Memahami OSI Layer dengan menggunakan analogi mengirim surat 
Analogi Mengirim Surat
1. Application Layer (Lapisan Aplikasi)

   Apa yang terjadi:
   Menulis surat dengan konten yang ingin di kirimkan, misalnya undangan untuk acara.

   Analoginya:
   Ini adalah aplikasi yang di gunakan untuk menulis pesan, seperti email atau aplikasi chat.
2. Presentation Layer (Lapisan Presentasi)

   Apa yang Terjadi:
   Setelah menulis surat, lalu memasukkan surat ke dalam amplop dan menulis informasi tambahan seperti format                        yang diinginkan (misalnya, apakah amplopnya berwarna atau ukuran khusus).

   Analoginya:
   Ini adalah tahap di mana data disiapkan dalam format yang sesuai untuk penerima. Misalnya, jika surat  harus                      dienkripsi, ini dilakukan di lapisan ini.
3. Session Layer (Lapisan Sesi)

   Apa yang Terjadi:
   Kemudian menyiapkan dan mengelola sesi komunikasi dengan kantor pos, memastikan bahwa mereka tahu surat ini                       bagian dari kiriman yang lebih besar atau sesi tertentu.

   Analoginya:
   Ini mengatur komunikasi dan memastikan bahwa koneksi antara pengirim dan penerima tetap aktif selama proses                       pengiriman.
4. Transport Layer (Lapisan Transport)

   Apa yang Terjadi:
   lalu, memberikan amplop kepada kantor pos, yang akan memutuskan bagaimana cara terbaik untuk mengirimkan surat                    itu dan memastikan bahwa surat sampai dengan aman.

   Analoginya:
   Ini memastikan bahwa data dibagi menjadi bagian-bagian kecil jika diperlukan dan dikirim dengan cara yang tepat.                  Misalnya, TCP memastikan pengiriman yang andal.
5. Network Layer (Lapisan Jaringan)

   Apa yang Terjadi:
   Kantor pos memutuskan rute terbaik untuk mengirimkan surat ke alamat tujuan, melalui berbagai kantor pos                          jika diperlukan.

   Analoginya:
   Ini mengatur rute dan alamat tujuan untuk data, seperti memilih jalan terbaik melalui jaringan untuk mencapai server              tujuan.
6. Data Link Layer (Lapisan Data Link)

   Apa yang Terjadi:
   Surat tiba di kantor pos lokal, dan kantor pos memastikan bahwa surat tersebut dikirim ke tempat yang tepat di                    dalam kantor pos lokal itu.

   Analoginya:
   Ini memastikan bahwa data yang dikirim melalui media transmisi lokal (seperti kabel) sampai ke perangkat yang benar               dalam jaringan lokal.
7. Physical Layer (Lapisan Fisik)

   Apa yang Terjadi:
   Surat akhirnya dikirim melalui truk atau kurir, bergerak secara fisik melalui berbagai media (jalan, rel, dll.)                   untuk sampai ke penerima.

   Analoginya:
   Ini adalah media fisik yang digunakan untuk mengirimkan sinyal data, seperti kabel Ethernet atau gelombang radio.

Proses Penerimaan Surat:
1. Physical Layer (Lapisan Fisik):

   Surat diterima secara fisik oleh penerima.
2. Data Link Layer (Lapisan Data Link):

   Kantor pos penerima memeriksa dan memastikan surat sampai dalam kondisi baik.
3. Network Layer (Lapisan Jaringan):

   Surat diterima dan dipastikan berada di alamat yang benar.
4. Transport Layer (Lapisan Transport):

   Surat disusun dengan benar dan siap untuk diserahkan.
5. Session Layer (Lapisan Sesi):

   Sesi komunikasi antara kantor pos dan penerima diatur untuk memastikan surat diterima.
6. Presentation Layer (Lapisan Presentasi):

   Amplop dibuka dan surat dibaca dalam format yang diinginkan.
7. Application Layer (Lapisan Aplikasi):

   Surat diterima dan dibaca oleh penerima.










