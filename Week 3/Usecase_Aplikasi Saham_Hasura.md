# USECASE APLIKASI SAHAM 

Saham adalah surat berharga yang memberikan hak kepemilikan kepada pemegangnya atas sebagian dari perusahaan yang menerbitkan saham tersebut.

Saham juga sering disebut sebagai ekuitas atau equity.

Bentuk Saham:

Dokumen Fisik: Dalam sejarah, saham bisa berupa dokumen fisik yang menunjukkan kepemilikan. Namun, di era modern, saham lebih sering diterbitkan dan diperdagangkan dalam bentuk elektronik.

Elektronik: Saat ini, saham biasanya berbentuk catatan elektronik di sistem bursa saham atau lembaga kustodian. Ini memungkinkan saham dipindahkan dan diperdagangkan dengan lebih efisien.

# Membuat Tabel dan Kolom Database 

Pembuatan tabel dan kolom database yang dibuat, menggunakan aplikasi dbever. 

Untuk menghubungkan dbever ke hasura console dapat melakukan connect terlebih dahulu di dbever, seperti gambar dibawah ini :

![image](https://github.com/user-attachments/assets/fc3108a9-31fd-4974-adc3-b314846b18be)

selanjutnya pilih database, disini saya mysql, kemudian pilih connect melalui host atau url, disini saya menggunakan host. 

![image](https://github.com/user-attachments/assets/f36ede77-c661-4c46-be4c-d2f497f02c05)

selanjutnya mengisi server host : 10.100.13.205, mengisi nama database dan user dan password, setelah itu klik test connect, kemudian klik finish

![image](https://github.com/user-attachments/assets/2a6639ab-2b9b-4499-877d-681265d0ef1e)

selanjutnya saya membuat 6 Tabel database beserta kolom di dbever terlebih dahulu.

jika sudah selesai, pergi ke hasura console dan reload terlebih dahulu dan tabel dan kolom sudah muncul ( terconnect)

![image](https://github.com/user-attachments/assets/ca8e73b1-b621-4384-b882-610ec3907e3d)

# Tabel usecase 

Terdapat 6 Tabel database beserta kolom dan fungsinya:

1. Tabel users :

![image](https://github.com/user-attachments/assets/fabe419d-3c80-4961-9446-2b8e5ddfd03b)

Kolom:

`id`: ID unik untuk setiap pengguna. (set primary key, tipe data:integer, not null)

`name`: Nama lengkap pengguna. (tipe data: varchar(255), not null)

`email`: Alamat email pengguna, yang digunakan untuk mengidentifikasi pengguna. Harus unik. (tipe data: varchar(255), not null, unique)

Fungsi : 
Menyimpan informasi tentang pengguna (investor) aplikasi saham.

Setiap pengguna dapat melakukan order saham, memiliki portofolio, dan memantau saham melalui watchlist.

2. Tabel stocks:

![image](https://github.com/user-attachments/assets/a5a0f877-6a2e-442b-9a67-979ee74f0b2f)

Kolom:

`id`: ID unik untuk setiap saham. (set primary key, tipe data:integer, not null)

`emiten_name`: Nama perusahaan yang terdaftar sebagai emiten di bursa saham (tipe data: varchar(255), not null)

`stock_symbol`:  Kode saham atau ticker simbol perusahaan. Harus Unik, karena digunakan di pasar saham untuk mengidentifikasi saham tersebut. (tipe data: varchar(10), not null, unique)

`stock_price`: Harga saham terkini dari emiten tersebut. Nilai ini akan berubah sesuai dengan harga pasar. (tipe data: decimal(30,2), not null)

`quantity`: Ini adalah jumlah saham yang diperdagangkan selama periode tertentu, seperti satu hari. Volume ini mencerminkan aktivitas perdagangan dan dapat berubah setiap hari. (tipe data:integer, not null)

`total_price`: Kolom quantity dalam konteks ini berfungsi untuk mencatat volume perdagangan, yaitu jumlah saham yang diperdagangkan dalam periode tertentu, seperti satu hari. (tipe data: decimal(30,2), not null)

`created_at`:  kolom ini berfungsi mencatat kapan data tentang saham baru dimasukkan ke dalam sistem. Misalnya, jika saham baru ditambahkan ke tabel, created_at akan mencatat tanggal dan waktu penambahan tersebut. (tipe data: timestamp)

Fungsi : Menyimpan informasi tentang emiten saham yang terdaftar.

Setiap saham dapat diorder oleh pengguna, masuk dalam watchlist, dan tercantum dalam portofolio pengguna.

3. Tabel orders:

![image](https://github.com/user-attachments/assets/7ae5b23b-f7ff-44d7-ac86-9737fed0c6ea)

Kolom:

`id`: ID unik untuk setiap order. Ini digunakan sebagai referensi di tabel transaksi. (set primary key, tipe data:integer, not null)

`user_id`: Merujuk ke pengguna yang melakukan order ini. (Foreign Key ke tabel users)

`stock_id`: Merujuk ke saham yang diorder. (Foreign Key ke tabel stocks)

`order_type':  Jenis order, apakah pengguna ingin membeli atau menjual saham. Nilainya bisa "BUY" atau "SELL"

Fungsi: Menyimpan order yang dilakukan oleh pengguna (beli atau jual saham).

Order dapat dieksekusi (dijadikan transaksi) atau tidak.

4. Tabel transactions:

![image](https://github.com/user-attachments/assets/9d6048fc-446d-4ca2-be56-03ce5089d0fe)

Kolom:

`id`:  ID unik untuk setiap transaksi. (set primary key, tipe data:integer, not null)

`order_id`: Merujuk ke order yang telah dieksekusi menjadi transaksi. (Foreign Key ke tabel orders)

`executed_at': Waktu kapan transaksi ini dilakukan di pasar saham. (tipe data: timestamp, default: current timestamp)

`executed_price`: Harga saham pada saat order dieksekusi. Harga ini bisa berbeda dari harga saat order dibuat. (tipe data: decimal(10,2), not null)

`executed_quantity`: Jumlah saham yang dieksekusi pada transaksi ini. (tipe data:integer, not null)

`total_amount`: Total nilai transaksi, dihitung dari `executed_price` dikali dengan `executed_quantity`

Fungsi : Menyimpan transaksi yang dieksekusi berdasarkan order yang sudah berhasil diproses.

Transaksi ini merupakan hasil dari order yang terealisasi di pasar saham.

5. Tabel portfolio:

![image](https://github.com/user-attachments/assets/b544c9d5-27b6-4ef2-ae5e-9db59462cc29)

Kolom:

`id`: ID unik untuk setiap portofolio. (set primary key, tipe data:integer, not null)

`user_id`: Merujuk ke pengguna yang memiliki portofolio ini.(Foreign Key ke tabel users)

`stock_id`: Merujuk ke saham yang dimiliki oleh pengguna.(Foreign Key ke tabel stocks)

`total_shares`: Jumlah total saham yang dimiliki pengguna untuk emiten tertentu. (tipe data:integer, not null)

`average_price`: Harga rata-rata pembelian saham tersebut, dihitung dari total pembelian saham. (tipe data: decimal(10,2), not null)

Fungsi : Menyimpan data portofolio saham yang dimiliki oleh pengguna.

Setiap pengguna dapat memiliki banyak saham dari berbagai emiten di dalam portofolionya.

6. Tabel watchlist:

![image](https://github.com/user-attachments/assets/50931327-a4da-43d5-bd07-682067ab0eb3)

Kolom: 

`id`: ID unik untuk setiap watchlist entry. (set primary key, tipe data:integer, not null)

`user_id`: Merujuk ke pengguna yang membuat watchlist ini.(Foreign Key ke tabel users)

`stock_id`: Merujuk ke saham yang ditambahkan ke watchlist. (Foreign Key ke tabel stocks)

`added_at`: Waktu kapan saham ini ditambahkan ke watchlist oleh pengguna.

Fungsi: Menyimpan daftar saham yang sedang dipantau oleh pengguna. (tipe data: timestamp, default: current timestamp)

Watchlist berguna untuk memantau saham tertentu tanpa harus membelinya.

# Action On Delete dan On Update pada Foreign Key

Dalam foreign key terdapat aturan dalam action On delete dan On update pada foreign key, seperti beberapa tabel dibawah ini :

1. Tabel orders :

Foreign key kolom `user_id` merujuk pada kolom `id` Tabel users

ON DELETE CASCADE: Jika pengguna dihapus, semua order yang dilakukan oleh pengguna tersebut juga akan dihapus. Ini karena jika pengguna tidak ada lagi, maka order-order terkait tidak relevan.

ON UPDATE CASCADE: Jika ID pengguna berubah, secara otomatis semua order yang dibuat oleh pengguna tersebut akan diperbarui untuk mencerminkan perubahan ID.

Foreign key kolom `stock_id` merujuk pada kolom `id` Tabel stocks

ON DELETE RESTRICT: Jangan hapus saham yang sudah ada order-nya. Ini untuk mencegah masalah konsistensi jika ada data order yang masih membutuhkan referensi ke saham tersebut.

ON UPDATE CASCADE: Jika simbol saham atau ID saham berubah, order terkait akan diperbarui secara otomatis.

2. Tabel transactions :

`Foreign key` kolom `order_id` merujuk pada kolom `id` Tabel orders

ON DELETE CASCADE: Jika order dihapus, transaksi terkait juga harus dihapus, karena transaksi ini didasarkan pada order tersebut.

ON UPDATE CASCADE: Jika ID order berubah, ID transaksi yang merujuk ke order tersebut juga harus diperbarui untuk mencerminkan perubahan ID.

3. Tabel portfolio :

Foreign key kolom `user_id` merujuk pada kolom `id` Tabel users

ON DELETE CASCADE: Jika pengguna dihapus, portofolio saham milik pengguna tersebut juga dihapus, karena portofolio tersebut tidak lagi memiliki pemilik.

ON UPDATE CASCADE: Jika ID pengguna berubah, referensi di portofolio akan diperbarui secara otomatis.

Foreign key kolom `stock_id` merujuk pada kolom `id` Tabel stocks

ON DELETE RESTRICT: Jangan hapus saham yang sudah ada di portofolio, karena pengguna mungkin masih memiliki saham tersebut.

ON UPDATE CASCADE: Jika ID saham berubah, data di portofolio yang merujuk ke saham tersebut akan diperbarui.

4. Tabel watchlist :

Foreign key kolom `user_id` merujuk pada kolom `id` Tabel users

ON DELETE CASCADE: Jika pengguna dihapus, watchlist pengguna tersebut juga dihapus, karena tidak lagi ada pemilik yang memantau saham-saham tersebut.

ON UPDATE CASCADE: Jika ID pengguna berubah, referensi di watchlist akan diperbarui secara otomatis.

Foreign key kolom `stock_id` merujuk pada kolom `id` Tabel stocks

ON DELETE CASCADE: Jika saham dihapus (misalnya, karena emiten keluar dari bursa), saham tersebut juga harus dihapus dari watchlist pengguna.

ON UPDATE CASCADE: Jika ID saham berubah, data watchlist akan diperbarui untuk mencerminkan perubahan ID saham.

# Relasi Antar Tabel

1. Relasi Tabel orders pada tabel users dan stocks

![image](https://github.com/user-attachments/assets/ced4b5f1-336c-4ceb-b2bc-07b0e70bf6be)

Relasi users-orders (1-to-many):

Penjelasan:

Seorang pengguna bisa membuat banyak order (pesanan untuk membeli atau menjual saham), tetapi setiap order hanya bisa dibuat oleh satu pengguna.

Implementasi:

Tabel users memiliki kolom id sebagai Primary Key.

Tabel orders memiliki kolom user_id sebagai Foreign Key yang mengacu ke kolom id di tabel users.

Relasi stocks-orders (1-to-many):

Penjelasan:

Satu saham (emiten) bisa diorder oleh banyak pengguna. Setiap order mereferensikan satu saham tertentu.

Implementasi:

Tabel stocks memiliki kolom id sebagai Primary Key.

Tabel orders memiliki kolom stock_id sebagai Foreign Key yang mengacu ke kolom id di tabel stocks.

2. Relasi Tabel transactions pada tabel orders

![image](https://github.com/user-attachments/assets/6c8057e1-4231-400c-a281-4e04008f3a9f)

Relasi orders → transactions (1-to-1):

Penjelasan:

Setiap order yang dieksekusi (berhasil diproses di pasar saham) akan menjadi satu transaksi. Hubungannya adalah satu order menghasilkan satu transaksi.

Implementasi:

Tabel orders memiliki kolom id sebagai Primary Key.

Tabel transactions memiliki kolom order_id sebagai Foreign Key yang mengacu ke kolom id di tabel orders.

3. Relasi Tabel portfolio pada tabel users dan stocks

![image](https://github.com/user-attachments/assets/85cd3136-e99e-4c99-8d36-48555ba19b7f)

Relasi users-portfolio (1-to-many):

Penjelasan:

Seorang pengguna bisa memiliki banyak saham di dalam portofolionya. Portofolio ini mencatat kepemilikan saham seorang pengguna.

Implementasi:

Tabel users memiliki kolom id sebagai Primary Key.

Tabel portfolio memiliki kolom user_id sebagai Foreign Key yang mengacu ke kolom id di tabel users.

Relasi stocks-portfolio (1-to-many):

Penjelasan:

Satu saham bisa dimiliki oleh banyak pengguna dalam portofolio mereka. Artinya, satu saham dapat tercatat di berbagai portofolio pengguna.

Implementasi:

Tabel stocks memiliki kolom id sebagai Primary Key.

Tabel portfolio memiliki kolom stock_id sebagai Foreign Key yang mengacu ke kolom id di tabel stocks.

4 Relasi Tabel watchlist pada tabel users dan stocks

![image](https://github.com/user-attachments/assets/95fecddd-b5e9-44a5-b3ab-585beddb38c3)

Relasi users-watchlist (1-to-many):

Penjelasan:

Seorang pengguna bisa menambahkan banyak saham ke dalam watchlist-nya. Watchlist adalah daftar saham yang sedang dipantau oleh pengguna.

Implementasi:

Tabel users memiliki kolom id sebagai Primary Key.

Tabel watchlist memiliki kolom user_id sebagai Foreign Key yang mengacu ke kolom id di tabel users.

Relasi stocks-watchlist (1-to-many):

Penjelasan:

 Seorang pengguna bisa menambahkan banyak saham ke dalam watchlist-nya. Watchlist adalah daftar saham yang sedang dipantau oleh pengguna.
 
Implementasi:

Tabel users memiliki kolom id sebagai Primary Key.

Tabel watchlist memiliki kolom user_id sebagai Foreign Key yang mengacu ke kolom id di tabel users.

# Alur Usecase Aplikasi Saham

1. Membuat Data Stock: (mutation create insert tabel stocks)
  
2. User melakukan pendaftaran dengan mengisi data
 
3. User melihat emiten saham dari data stocks yang ditampilkan melalui query.

4. User melakukan order untuk membeli atau menjual saham 

5. Order dieksekusi menjadi transaksi

6. Saham yang dibeli masuk ke dalam portofolio pengguna/user

7. User dapat menambah saham ke watchlist untuk dipantau tanpa melakukan pembelian 


