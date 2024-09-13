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















