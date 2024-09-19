# Integrasi Remote Schemas springboot di HASURA

Pada Hasura console, klik tab remote schemas terlebih dahulu:

![image](https://github.com/user-attachments/assets/d2e72068-423b-43f2-8b53-2d57066731c7)

Setelah itu, klik add untuk menambahkan remote schemas:

![image](https://github.com/user-attachments/assets/4634f296-e393-499d-9e0b-28d8ccf35331)

Terlihat beberapa isian detail untuk kita remote, masukkan endpoint kedua terlebih dahulu yaitu : http://10.100.13.24:8088/apis/graphql

![image](https://github.com/user-attachments/assets/ec3bb4d8-757e-4260-a51c-6b10c79c2f85)

isilah :

Remote Schema Name : springbootGraphQL 

GraphQL Service URL : http://10.100.13.24:8088/apis/graphql

Kemudian save dengan mengeklik add remote schema:

![image](https://github.com/user-attachments/assets/2fff7ed7-5fd4-444d-97df-dab2acb0d972)

schemas springbootGraphQL berhasil di remote 

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
query {
  findAllAuthors {
    id
    name
    age
  }
}

```
Hasil Output:

![image](https://github.com/user-attachments/assets/416acc3b-dc9d-419c-a67c-0c07c16ad4aa)

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
query {
  findAllTutorials {
    id
    title
    description
  }
}
```
Hasil Output:

![image](https://github.com/user-attachments/assets/1fa15fed-3dba-4f1a-a0b0-76b3899faa73)

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
query {
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

![image](https://github.com/user-attachments/assets/cf429e2b-da43-4878-91e4-721766acf91b)

Penjelasan Output:

Query ini mengembalikan semua tutorial yang tersimpan dalam tabel Tutorials, dengan informasi terkait masing-masing tutorial dan data penulisnya.

