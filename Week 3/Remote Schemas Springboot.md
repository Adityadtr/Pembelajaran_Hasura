# Tabel pada schemas springbootgraphql

1. Tabel authors: adalah tabel yang berisi informasi tentang penulis

Kolom tabel: 

. id: ID unik untuk setiap penulis. (Tipe data: integer, primary key)

. name: Nama dari penulis. (Tipde data: string)

. age: umur dari penulis. (Tipde data: int)

2. Tabel tutorials:  adalah tabel yang berisi informasi tentang tutorial

Kolom tabel: 

. id: ID unik untuk setiap tutorial. (Tipe data: integer, primary key)

. title: judul tutorial. (Tipde data: string)

. description: deskripsi tentang tutorial. (Tipde data: string)

# Hubungan Antara Tabel authors dengan Tabel tutorials

Relasi One-to-Many

Authors ke Tutorials: Setiap penulis (Authors) dapat menulis banyak tutorial (Tutorials).

Foreign Key di Tabel Tutorials: 

Tabel Tutorials memiliki kolom author yang bertindak sebagai foreign key yang mengacu pada id di tabel Authors. Ini menunjukkan bahwa setiap tutorial dikaitkan dengan satu penulis tertentu.

# Analisa Query pada springbootgraphql

1. Queries findAllAuthors

Query: `findAllAuthors ` adalah query yang mengembalikan atau mengirim balik (return) daftar semua penulis (authors) yang ada dalam database.

Subfields:

`id`: ID unik setiap penulis.

`name`: Nama penulis.

`age`: Usia penulis.

Query dalam graphql di postman:

```
query MyQuery {
  findAllAuthors {
    id
    name
    age
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/539b2e8e-e9a3-4a50-80e7-837685a91a92)

Penjelasan Output:

Query ini mengambil seluruh data penulis tanpa filter atau batasan. Semua penulis yang ada di dalam tabel Authors akan ditampilkan beserta kolom id, name, dan age.

2. Queries findAllTutorials (tanpa relasi dari data author)

Query `findAllTutorials `: Query ini tetap mengembalikan daftar semua tutorial dari database, tetapi hanya mengambil informasi id, title, dan description dari setiap tutorial tanpa informasi author.

Subfields:

.`id`: ID unik setiap tutorial.

.`title`: Judul tutorial.

.`description`: Deskripsi dari tutorial.

Query dalam graphql di postman:

```
query MyQuery {
  findAllTutorials {
    id
    title
    description
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/89113c8f-e0fe-4232-8819-ab69e3d71184)

Penjelasan Output:

query ini Mengembalikan array yang berisi daftar tutorial, masing-masing dengan id, title, dan description.

3. Queries findAllTutorials (dengan relasi dari data author)

Query: `findAllTutorials ` adalah query yang mengembalikan daftar semua tutorial yang ada dalam database.

Subfields:

.`id`: ID unik setiap tutorial.

.`title`: Judul tutorial.

.`description`: Deskripsi dari tutorial.

`author`: Objek penulis yang memiliki sub-fields berikut:

.`id`: ID unik penulis.

.`name`: Nama penulis.

.`age`: Usia penulis.

Query dalam graphql di postman:

```
query MyQuery {
  findAllTutorials {
    id
    title
    description
    author {
      id
      name
      age
    }
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/20d6e772-64e8-4c13-96f3-cf79f601dea1)

Penjelasan Output:

Query ini mengembalikan semua tutorial yang tersimpan dalam tabel Tutorials, dengan informasi terkait masing-masing tutorial dan data penulisnya.

4. Query countAuthors 

Query `countAuthors `: Query ini digunakan untuk menghitung jumlah total authors yang ada di dalam database.

Query dalam graphql di postman:

```
query MyQuery {
  countAuthors
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/a9a6928a-f095-4565-9e73-2bdc4dfffe45)

Penjelasan Output:

Output menunjukkan bahwa jumlah total author di dalam database adalah 1. Ini artinya ada 1 author yang terdaftar dalam sistem.

5. Query countTutorials

Query `countTutorials `: Query ini digunakan untuk menghitung jumlah total tutorials yang ada di dalam database.

Query dalam graphql di postman:

```
{
  countTutorials
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/97f8c979-67aa-41f3-9ce8-f4d08dc9db98)

Penjelasan Output:

Output menunjukkan bahwa jumlah total tutorial di dalam database adalah 2. Jadi, terdapat 2 tutorial yang disimpan dalam sistem.
