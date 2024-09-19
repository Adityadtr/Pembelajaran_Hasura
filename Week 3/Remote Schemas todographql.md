# Tabel pada schemas todographql

1. Tabel todos: adalah tabel yang berisi daftar tugas (to-do items) dalam sebuah aplikasi

Kolom tabel: 

. id: ID unik untuk setiap tugas. (Tipe data: integer, primary key)

. text: Deskripsi dari tugas tersebut. (Tipde data: string)

. done: Status apakah tugas tersebut sudah diselesaikan atau belum. (Tipde data: boolean, true atau false)

. user_id: Menyimpan ID dari pengguna yang membuat tugas tersebut. (Tipde data: int)

2. Tabel users:  adalh tabel yang berisi informasi mengenai pengguna (user) yang membuat atau berinteraksi dengan tugas-tugas dalam aplikasi

Kolom tabel: 

. id: ID unik untuk setiap pengguna. (Tipe data: integer, primary key)

. name: Nama dari pengguna. (Tipde data: string)

# Hubungan Antara Tabel todos dengan Tabel users

Relasi: Tabel todos memiliki relasi many-to-one dengan tabel users. 

Ini berarti satu pengguna (dari tabel users) dapat membuat banyak tugas (dari tabel todos), tetapi setiap tugas hanya bisa dimiliki oleh satu pengguna.

Foreign Key: Kolom user_id dalam tabel todos merujuk pada kolom id di tabel users. Hal ini memastikan bahwa setiap tugas dihubungkan dengan seorang pengguna tertentu.

# Perbedaan todos, todo, users, user

. todos: 

Kegunaan: Mengembalikan atau mengirim balik (return) semua daftar todo yang ada di database.

Cakupan: Tidak memerlukan argumen dan mengembalikan daftar semua todo.

. todo (query by_pk):

Kegunaan: Mengembalikan atau mengirim balik (return) satu daftar todo berdasarkan ID tertentu yang diberikan sebagai argumen.

Cakupan: Memerlukan argumen (biasanya id) untuk mengidentifikasi todo spesifik.

. users:

Kegunaan: Mengembalikan atau mengirim balik (return) semua pengguna yang ada di database.

Cakupan: Ini adalah query yang tidak memerlukan argumen dan mengembalikan daftar semua pengguna.

. user (query by_pk):

Kegunaan: Mengembalikan atau mengirim balik (return) satu pengguna berdasarkan ID tertentu yang diberikan sebagai argumen.

Cakupan: Ini adalah query yang memerlukan argumen (biasanya id) untuk mengidentifikasi pengguna spesifik.

# Analisa Query pada todographql

1. Queries todos

Query: `todos` mengambil daftar semua tugas (todo items) yang ada di database.

Subfields:

. `id`: ID unik untuk setiap todo.

. `text`: Deskripsi teks untuk setiap todo.

. `done`: Status apakah tugas sudah selesai (true/false).

`user`: Berisi informasi tentang pengguna yang membuat todo, dengan subfield:

. `id`: ID pengguna.

. `name`: Nama pengguna.

Query dalam graphql di postman:

```
query MyQuery {
  todosRemote {
    todos {
      id
      text
      done
      user {
        id
        name
      }
    }
  }
}

```
Hasil Output:

![image](https://github.com/user-attachments/assets/a504e886-32e1-4f77-99a6-f478361790de)

Penjelasan Output:

Query ini mengembalikan daftar (array) semua tugas yang ada dalam database, lengkap dengan informasi pembuatnya (user).

2. Queries todo

Query: `todo` mengambil satu tugas (todo item) berdasarkan ID yang diberikan sebagai argumen.

`Arguments`:

. id: ID dari todo yang ingin diambil (misalnya, id: 1).

Subfields:

. `id`: ID unik untuk setiap todo.

. `text`: Deskripsi teks untuk setiap todo.

. `done`: Status apakah tugas sudah selesai (true/false).

`user`: Berisi informasi tentang pengguna yang membuat todo, dengan subfield:

. `id`: ID pengguna.

. `name`: Nama pengguna.

Query dalam graphql di postman:

```
query MyQuery {
  todosRemote {
    todo(id: "1") {
      id
      text
      done
      user {
        id
        name
      }
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/cf5ffe4b-7854-4fb9-b09f-716b931f681b)

Penjelasan Output:

query tersebut mengambil hanya satu tugas tertentu berdasarkan id, menghasilkan satu objek tugas (bukan array).

3. Queries users

Query: `users` akan mengambil semua pengguna yang ada di database.

Subfields:

. `id`: ID pengguna.

. `name`: Nama pengguna.

Query dalam graphql di postman:

```
query MyQuery {
  todosRemote {
    users {
      id
      name
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/3fcaf3c1-6a1a-483a-9547-0c0e510f5c51)

Penjelasan Output:

Query ini mengembalikan semua pengguna yang tersimpan dalam database, dengan informasi dasar berupa id dan name.

4. Queries user

Query: `user` mengambil satu pengguna (user) berdasarkan ID yang diberikan sebagai argumen.

`Arguments`:

. id: ID dari todo yang ingin diambil (misalnya, id: 1).

Subfields:

. `id`: ID unik dari pengguna.

. `name`: Nama pengguna.

Query dalam graphql di postman:

```
query MyQuery {
  todosRemote {
    user(id: "1") {
      id
      name
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/116e6ac5-3516-4c60-bf42-632ec0a68bf4)

Penjelasan Output:

Query ini hanya mengembalikan satu pengguna berdasarkan ID-nya.

