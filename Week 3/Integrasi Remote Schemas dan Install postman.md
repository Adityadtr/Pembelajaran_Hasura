# Integrasi Remote Schemas todos di HASURA

Pada Hasura console, klik tab remote schemas terlebih dahulu:

![image](https://github.com/user-attachments/assets/d2e72068-423b-43f2-8b53-2d57066731c7)

Setelah itu, klik add untuk menambahkan remote schemas:

![image](https://github.com/user-attachments/assets/4634f296-e393-499d-9e0b-28d8ccf35331)

Terlihat beberapa isian detail untuk kita remote, masukkan endpoint pertama terlebih dahulu yaitu : http://10.100.14.10:8989/query

![image](https://github.com/user-attachments/assets/1aea3ca2-d6d6-4144-9712-ab0e3e0552de)

isilah :

Remote Schema Name : todosGraphQL 

GraphQL Service URL : http://10.100.14.10:8989/query

Tetapi ada eror, dikarenakan field di hasura schemas saya memiliki field users yang sama dengan hasura schemas todographql, maka dapat memberikan penambahan root fields namespace nya:

dengan mengklik graphql customizations dan isi root fields namespacesnya: 

![image](https://github.com/user-attachments/assets/72e785d5-f006-4ae7-a965-f02b2fea4641)

isilah : 

root fields namespaces: todosRemote

Kemudian save dengan mengeklik add remote schema:

![image](https://github.com/user-attachments/assets/8a4bb55d-a9b2-421f-ba74-38c811e040de)

schemas todosGraphQL berhasil di remote 

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

# Menghubungkan Hasura dengan Postman untuk Graphql

1. Download dan Install terlebih dahulu aplikasi postman di browser

Buka browser dan kunjungi situs resmi Postman di https://www.postman.com/downloads/. dan download postman tersebut. setelah terdownload buka file installer postman dan jalankan penginstallan.

2. Login pada aplikasi postman

Setelah proses instalasi selesai, aplikasi postman terbuka dan lakukan login dengan membuat akun postman terlebih dahulu.

![image](https://github.com/user-attachments/assets/e49241b1-6d72-4b65-9736-f86cf1edd875)

3. Membuat request
   
Setelah login, halaman home postman dapat terlihat, kemudian dapat mulai membuat dan mengirimkan request API seperti GraphQL, REST, atau SOAP.

disini saya membuat request terlebih dahulu, dengan mengeklik tombol **New Request** lalu pilih tipe permintaan seperti HTTP yang saya lakukan
  
![image](https://github.com/user-attachments/assets/7d955b2a-6f28-4a1f-99bb-6e899d28ca92)

4. Melakukan pengubahan metode request get menjadi post

Setelah diarahkan ke halaman selanjutnya, kemudian ubah metode request get menjadi post

![image](https://github.com/user-attachments/assets/73f0bd06-0481-4345-b2cb-bdf86dbcb3bf)

5. Masukkan endpoint GraphQL di kolom Request URL.

Setelah mengubah request menjadi post, kemudian masukkan url graphql di kolom request url. jika hasura menggunakan admin secret, dapat menambahkan admin secret pada menu header dibawah kolom url

![image](https://github.com/user-attachments/assets/7cdeb6da-c378-491c-a0be-e6dcbdbe6547)

6. Melakukan query

setelah header sudah diatur, kemudian pilih menu body dibawah kolom url lalu pilih graphql, untuk dapat menjalankan query di graphql tersebut.

![image](https://github.com/user-attachments/assets/031c19c3-b1d9-44bd-bd3e-94e61a9429e9)
