# Membuat Data Stock (Emiten)

Pertama membuat data emiten (stocks) terlebih dahulu, dapat menggunakan perintah:

Single Data Insert (Membuat satu stock):

Ini menambahkan satu data emiten. Admin atau sistem dapat menambah stok baru.

```
mutation {
  insert_stocks(objects: {id: 12, emiten_name: "Adhi Commuter Properti Tbk", stock_symbol: "ADCP", stock_price: 51.00, quantity: 15400300, total_price:785415300.00, created_at: "2024-09-12 14:00:00"}) {
    returning {
      id
      emiten_name
      stock_symbol
      stock_price
      quantity
      total_price
      created_at
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/198d49bb-2977-484d-9fa5-8635cc55d4d4)

![image](https://github.com/user-attachments/assets/652d8884-9241-47a2-89fd-b696296cc049)

Atau dapat menggunakan Multiple Data Insert (Membuat Banyak Stock):

Ini menambahkan beberapa stok sekaligus dalam satu mutation, berguna untuk proses bulk insert.

```
mutation {
  insert_stocks(objects: [
    {id: 13, emiten_name: "FKS Food Sejahtera Tbk", stock_symbol: "AISA", stock_price: 128.00, quantity: 3048900, total_price:391467500.00, created_at: "2024-09-12 14:00:00"},
    {id: 14, emiten_name: "Samator Indo Gas Tbk", stock_symbol: "AGII", stock_price: 1750.00, quantity: 45300, total_price:79549000.00, created_at: "2024-09-12 14:00:00"},
    {id: 15, emiten_name: "Alkindo Naratama Tbk", stock_symbol: "ALDO", stock_price: 432.00, quantity: 486700, total_price:208565200.00, created_at: "2024-09-12 14:00:00"}
  ]) {
    returning {
      id
      emiten_name
      stock_symbol
      stock_price
      quantity
      total_price
      created_at
    }
  }
}
```

Hasil Output:

![image](https://github.com/user-attachments/assets/8a852f6b-6fff-4f30-b4a3-e84fbd2062dd)

![image](https://github.com/user-attachments/assets/8188bc88-f88f-452a-8c98-cde8c0bd275e)

# Menampilkan emiten saham dari data stocks melalui query

Mengambil Semua Emiten Saham (Get Multiple Data):

Query ini mengambil seluruh data saham yang ada.

```
query {
  stocks {
    id
    emiten_name
    stock_symbol
    stock_price
    quantity
    total_price
    created_at
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/b1f47924-6075-4484-8d1c-a68032674c67)

Dapat juga melakukan pengambilan satu Emiten Saham (Get Single Data):

Ini mengambil satu saham berdasarkan ID

```
query {
  stocks(where: {id: {_eq: 5}}) {
    id
    emiten_name
    stock_symbol
    stock_price
    quantity
    total_price
    created_at
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/66530ed7-b2ff-456b-93c0-37680efe7f4b)

![image](https://github.com/user-attachments/assets/ff5bf409-fca3-4c5c-8cd0-c8eac8b7eb78)

# Membuat Pendaftaran Pengguna Baru (user)

Single Data Insert (Pendaftaran Satu User) : 

Satu pengguna mendaftarkan akun dengan data seperti nama dan email.

```
mutation {
  insert_users(objects: {name: "Andi", email: "andi@gmail.com"}) {
    returning {
      id
      name
      email
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/0da84181-01bd-4342-ba8f-c997aafd865a)

![image](https://github.com/user-attachments/assets/fb3dd3e6-877a-4578-bae4-6d960eec9cc6)

Dapat juga melakukan Multiple Data Insert (Pendaftaran Banyak User):

Pendaftaran beberapa user sekaligus dalam satu proses.

```
mutation {
  insert_users(objects: [
    {name: "Budi", email: "budi@gmail.com"},
    {name: "Cici", email: "cici@gmail.com"},
    {name: "Doni", email: "doni@gmail.com"}
  ]) {
    returning {
      id
      name
      email
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/be5b9ae0-a35a-41c3-b748-d7535fd9f2b1)

![image](https://github.com/user-attachments/assets/f8c637a8-d04a-42e6-abe2-add26c7b2b3d)

dapat melihat output order dari kolom pengguna:

![image](https://github.com/user-attachments/assets/26ceeb82-3382-4bc7-9276-170e5ce0bdeb)

# Mengupdate Data Pengguna

Untuk melakukan update data pengguna dapat mengupdate menggunakan mutation:

1. Update nama pengguna melalui id dengan menggunakan where

```
mutation MyMutation {
  update_users(
    where: { id: { _eq: 6 } },  # Kondisi untuk memilih berdasarkan id
    _set: { name: "Sari Ayu" }  # Data yang di-update
  ) {
    affected_rows
    returning {
      id
      name
      email
    }
  }
}
```
2. Update nama pengguna melalui kolom name menggunakan where:

```
mutation MyMutation {
  update_users(where: {name: {_eq: "sari"}}, _set: {name: "Sari Ayu"}) {
    returning {
      id
      email
      name
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/bf7151d2-da54-42db-a431-92f6382bfa78)

![image](https://github.com/user-attachments/assets/18642619-36c6-4f1b-916f-e40a8baf04ce)

3. Update email melalui kolom email menggunakan where:

```
mutation updateUserByEmail {
  update_users(
    where: { email: { _eq: "joni@example.com" } },  # Kondisi untuk memilih berdasarkan email
    _set: { email: "updatedjoni@example.com" }  # Data yang di-update
  ) {
    affected_rows
    returning {
      id
      name
      email
    }
  }
}
```
4. Update Data dalam graphql

```
mutation updateUser {
  update_users_by_pk(pk_columns: {id: 6}, _set: {name: "Sari Ayu", email: "sariayu@gmail.com"}) {
    id
    name
    email
  }
}
```

# Menghapus data pengguna

Untuk melakukan delete data pengguna dapat mengdelete menggunakan mutation:

1. Delete berdasarkan id

```
mutation deleteUserByID {
  delete_users(where: {id: {_eq: 6}}) {
    affected_rows
    returning {
      id
      name
      email
    }
  }
}
```
2. Delete berdasarkan name

```
mutation insertUsers {
  delete_users(where: {name: {_eq: "Dewi"}}) {
    returning {
      email
      id
      name
    }
  }
}

```
Hasil Output:

![image](https://github.com/user-attachments/assets/69e6776b-504a-443b-b0c0-4c8613f023cf)

3. Delete berdasarkan email

```
mutation deleteUserByEmail {
  delete_users(where: {email: {_eq: "sari@gmail.com"}}) {
    affected_rows
    returning {
      id
      name
      email
    }
  }
}
```
# Menampilkan data pengguna menggunakan query where 

1. Memfilter berdasarkan id:

```
query getUserById {
  users(where: {id: {_eq: 1}}) {
    id
    name
    email
  }
}
```
2. Memfilter berdasarkan nama:

```
query MyQuery {
  users(where: {name: {_eq: "Sarah"}}) {
    id
    name
    email
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/e4c2835b-861a-4536-bc43-51be9a3e617e)

3. Memfilter berdasarkan email:

```
query getUserByEmail {
  users(where: {email: {_eq: "joni@example.com"}}) {
    id
    name
    email
  }
}
```

# Operator Like di Graphql

Di GraphQL, untuk melakukan pencarian yang mirip dengan SQL LIKE, dapat menggunakan operator pencocokan string seperti _ilike atau _like. Operator ini memungkinkan untuk melakukan pencarian berdasarkan pola tertentu dalam data string.

_like: Menggunakan pola pencocokan yang case-sensitive (sensitif terhadap huruf besar/kecil).

_ilike: Menggunakan pola pencocokan yang case-insensitive (tidak sensitif terhadap huruf besar/kecil).

1. Mencari Nama yang Mengandung Substring Tertentu

Misalkan ingin mencari pengguna yang nama depannya mengandung substring "Joni". bisa menggunakan operator _like atau _ilike untuk mencapainya.

Query GraphQL untuk Mencari Nama yang Mengandung "Joni" (Case-Insensitive):

```
query MyQuery {
  users(where: {name: {_ilike: "%Ayu%"}}) {
    email
    id
    name
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/e71e95b1-480f-4f22-b25e-759cca3965e9)

2. Memfilter nama menggunakan operator like dan relasi dalam tabel order

```
query MyQuery {
  users(where: {name: {_ilike: "%ayu%"}}) {
    id
    name
    email
    orders {
      id
      user_id
      stock_id
      order_type
      order_quantity
      order_price
      created_at
    }
  }
}
```
Hasi Output:

![image](https://github.com/user-attachments/assets/cd83a827-d51e-4537-8d6f-687b2fdf6d6f)

# Query untuk relasi

disini saya akan menggunakan query untuk relasi antar tabel. tabel order ini digunakan untuk menampilkan data yang terkait dengan tabel users.

tabel orders memiliki user_id yang merupakan foreign key yang terhubung ke kolom id di tabel users. Dengan relasi tersebut, kita dapat menampilkan data dari tabel orders dan data pengguna terkait dari tabel users.

1. Query untuk Relasi Tabel orders dan users

menampilkan data dari tabel orders serta data terkait dari tabel users:

```
query MyQuery {
  orders {
    id
    user_id
    stock_id
    order_type
    order_quantity
    order_price
    created_at
    user {
      id
      name
      email
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/d3bda06e-1c92-4925-a37d-132498d85c79)

Penjelasan:

orders: Query ini menargetkan tabel orders.

user {}: Bagian ini mendefinisikan relasi ke tabel users melalui foreign key user_id. Di sini mengambil kolom id, name, dan email dari tabel users.

2. Query dengan Kondisi WHERE

Jika ingin melakukan filter data berdasarkan kolom tertentu, misalnya  hanya ingin menampilkan order dari pengguna tertentu, bisa dapat menggunakan filter where. Misalnya, menampilkan semua order yang dimiliki pengguna dengan name yang mengandung "Ayu":

```
query MyQuery {
  orders(where: {user: {name: {_ilike: "%ayu%"}}}) {
    id
    user_id
    stock_id
    order_type
    order_quantity
    order_price
    created_at
    user {
      id
      name
      email
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/bcb7d572-8b1b-4b55-aa04-9be54672df09)

where: {user: {name: {_like: "%ayu%"}}}: Bagian ini memfilter order berdasarkan nama pengguna yang mengandung "Ayu". Di sini kita memanfaatkan relasi antara orders dan users untuk melakukan filter.

3. Query dengan Kondisi order_type

Jika ingin menampilkan semua order yang memiliki order_type tertentu, misalnya hanya order dengan tipe "buy", dapat melakukan hal ini:

```
query MyQuery {
  orders(where: {order_type: {_eq: "BUY"}}) {
    id
    user_id
    stock_id
    order_type
    order_quantity
    order_price
    created_at
    user {
      id
      name
      email
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/92008858-e2e3-41b7-9e7b-e78a713ababc)

query tersebut menampilkan data order beserta data pengguna dari kolom order_type

4. Query dengan Relasi ke Tabel users dan Tabel stocks
   
Jika memiliki relasi ke tabel stocks melalui stock_id di tabel orders, bisa memperluas query untuk menampilkan data saham yang diorder.

```
query MyQuery {
  orders {
    id
    user_id
    stock_id
    order_type
    order_quantity
    order_price
    created_at
    user {
      id
      name
      email
    }
    stock {
      id
      emiten_name
      stock_symbol
      stock_price
      quantity
      total_price
      created_at
    }
  }
}
```
Hasil Output: 

![image](https://github.com/user-attachments/assets/72d3c6fc-1683-489b-834d-d9e9c95548ec)

stock {}: Relasi ke tabel stocks menggunakan foreign key stock_id. Kita bisa menampilkan informasi terkait saham seperti emiten_name, stock_symbol, stock_price, quantity, total_price, dan created_at.

# User melakukan order untuk membeli atau menjual saham

Single Data Insert (Satu Order):

Pengguna melakukan satu order untuk membeli saham.

```
mutation {
  insert_orders(objects: {user_id: 2, stock_id: 7, order_type: "buy"}) {
    returning {
      id
      user_id
      stock_id
      order_type
    }
  }
}
```
Hasil Output dari graphql:

![image](https://github.com/user-attachments/assets/0c49366b-03fc-4094-9a79-bce00d204edb)

Multiple Data Insert (Beberapa Order Sekaligus):

Pengguna melakukan beberapa order sekaligus.

```
mutation {
  insert_orders(objects: [
    {user_id: 1, stock_id: 2, order_type: "buy"},
    {user_id: 3, stock_id: 3, order_type: "sell"}
  ]) {
    returning {
      id
      user_id
      stock_id
      order_type
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/fce353df-f84f-4e6f-b7a5-09724261f360)

Menambah order lagi dengan user_id yang sama dan stock_id yg sama:

```
mutation {
  insert_orders(objects: {user_id: 2, stock_id: 7, order_type: "buy"}) {
    returning {
      id
      user_id
      stock_id
      order_type
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/ad0dd701-d9bd-4548-9a2d-0b1d81041545)

output hasura dari tab data orders, dapat melihat stocks yang pengguna pesan:

![image](https://github.com/user-attachments/assets/3a3cbaf6-c4b2-4cf1-87a8-aad6566952b7)

![image](https://github.com/user-attachments/assets/3ddf011f-08e9-4361-a16e-37ff72dbcda6)

hasil output dari pengguna yang melakukan order:

![image](https://github.com/user-attachments/assets/0bd14c1f-d7ae-4afd-8a6e-b81e334e7a7f)

# Eksekusi Order menjadi Transaksi (Insert Transactions)

Single Transaction Insert (Satu Transaksi):

Order dieksekusi menjadi satu transaksi dengan harga saham yang dieksekusi.

```
mutation {
  insert_transactions(objects: {order_id: 1, executed_price: 985.00, executed_quantity: 500, total_amount: 492500.00}) {
    returning {
      id
      order_id
      executed_at
      executed_price
      executed_quantity
      total_amount
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/bfdc5c96-15c8-4cb0-a4be-6f1561dcc605)

Multiple Transactions Insert (Beberapa Transaksi):

Beberapa order dieksekusi menjadi beberapa transaksi.

```
mutation {
  insert_transactions(objects: [
    {order_id: 2, executed_price: 26375.00, executed_quantity: 500, total_amount: 13187500.00},
    {order_id: 3, executed_price: 11750.00, executed_quantity: 500, total_amount: 5875000.00}
  ]) {
    returning {
      id
      order_id
      executed_at
      executed_price
      executed_quantity
      total_amount
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/a74d9c3a-8ae7-4cfd-8084-f4604922d3fd)

melakukan transaction lagi dengan order_id yang sama:

```
mutation {
  insert_transactions(objects: {order_id: 4, executed_price: 1000.00, executed_quantity: 250, total_amount: 250000.00})
{
    returning {
      id
      order_id
      executed_at
      executed_price
      executed_quantity
      total_amount
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/6b32cc81-3411-433b-bb2b-4b7156bf4eca)

Hasil Output dari Tab transactions:

![image](https://github.com/user-attachments/assets/6ea4a425-e25b-4e32-89de-1c35c4a7610a)

# Saham yang dibeli masuk ke dalam portfolio pengguna/user

Single Data Insert (Satu Saham ke Portofolio):

Saham yang dibeli ditambahkan ke portofolio pengguna.

```
mutation {
  insert_portfolio(objects: {
    user_id: 2, 
    stock_id: 7, 
    total_shares: 750  , 
    average_price: 990.00
  }) {
    returning {
      id
      user_id
      stock_id
      total_shares
      average_price
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/f8203a98-60ec-4437-afad-f0cdc1ec529a)

# User dapat menambah saham ke watchlist untuk dipantau tanpa melakukan pembelian

Single Data Insert (Satu Saham ke Watchlist):

Pengguna menambahkan satu saham ke watchlist untuk dipantau.

```
mutation {
  insert_watchlist(objects: {user_id: 1, stock_id: 9}) {
    returning {
      id
      user_id
      stock_id
      added_at
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/d3150aca-1ba4-404d-b0c2-e8b23970c16f)

Multiple Data Insert (Beberapa Saham ke Watchlist):

Pengguna menambahkan beberapa saham sekaligus ke watchlist.

```
mutation {
  insert_watchlist(objects: [
    {user_id: 2, stock_id: 5},
    {user_id: 3, stock_id: 9}
  ]) {
    returning {
      id
      user_id
      stock_id
      added_at
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/fccdfdbe-6044-4d59-9079-ac05f4ceff7f)

# affected rows

Penggunaan affected_rows dalam GraphQL pada Hasura bertujuan untuk menunjukkan jumlah baris yang terpengaruh oleh operasi mutation seperti insert, update, atau delete. Ini sangat berguna untuk memverifikasi apakah operasi berhasil dan mengetahui berapa banyak baris yang diubah dalam proses tersebut.

Berikut adalah beberapa contoh penggunaan affected_rows di Hasura:

1. Penggunaan Affected rows dalam 1 baris , pada mutation insert

```
mutation insertUsers {
  insert_users(objects: 
    {id: 9, name: "Rama", email: "rama@gmail.com"}) {
    affected_rows
  }
}
```
Hasil output :

![image](https://github.com/user-attachments/assets/d6472afa-bf4d-43c9-8aaa-8ac088c7a759)

![image](https://github.com/user-attachments/assets/9f3a968f-666f-4d7a-8d8c-87f5f1f38e68)

2. Penggunaan Affected rows dalam 2 baris , pada mutation insert

```
mutation insertUsers {
  insert_users(objects: [
    {id:7, name: "Sarah", email: "sarah@gmail.com"},
    {id:8, name: "Dewi", email: "dewi@gmail.com"}
  ]) {
    affected_rows
  }
}
```
Hasil output :

![image](https://github.com/user-attachments/assets/4774b5c2-240e-4993-b563-ef136e37ca56)















