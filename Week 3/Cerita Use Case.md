# Pendaftaran Pengguna Baru (Create User)

Intan  ingin berinvestasi di pasar saham. Dia membuka aplikasi saham, mengisi nama dan email di formulir pendaftaran, lalu klik "Daftar". Data intan berhasil disimpan dan dia sekarang dapat mengakses semua fitur aplikasi.

```
mutation {
  insert_users(objects: {name: "Budi", email: "budi@example.com"}) {
    returning {
      id
      name
      email
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/17a3d198-0474-4041-8035-460e11691ad3)

# User Melihat Daftar Saham Tersedia (Read Stocks)

Intan ingin melihat saham-saham yang tersedia di pasar. Dia membuka halaman Daftar Saham di aplikasi. Aplikasi menampilkan berbagai emiten s, lengkap dengan harga per lembar, total harga saham yang tersedia, serta jumlah lembar saham yang masih bisa dibeli.

```
query {
  stocks {
    id
    emiten_name
    stock_symbol
    stock_price
    quantity
    total_price
    create_at
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/b969d73c-d1ea-4627-a597-e6522136709b)

# Membeli Saham (Create Order, Update Stocks)

Budi memutuskan untuk membeli saham PT Unilever Indonesia (UNVR) sebanyak 50 lembar dengan harga 7.500 Rupiah per lembar. Dia memilih untuk melakukan Order Beli, kemudian mengonfirmasi transaksi. Setelah itu, jumlah saham UNVR di pasar berkurang dari 500 lembar menjadi 450 lembar.

```
mutation {
  insert_orders(objects: {
    user_id: 5, 
    stock_id: 11, 
    order_type: "buy", 
    quantity: 100, 
    order_price: 2200
  }) {
    returning {
      id
      user_id
      stock_id
      order_type
      quantity
      order_price
      created_at
    }
  }
}
```





