# Pengertian RESTified Endpoint

RESTified Endpoints di Hasura adalah fitur yang memungkinkan pengguna untuk membuat endpoint REST dari query atau mutation GraphQL yang ada, sehingga dapat diakses dengan cara REST API.

# RESTified Endpoints di Hasura Console pada todosgraphql

- Akses REST Endpoints:

   Di sisi kiri panel navigasi, pilih API lalu klik REST Endpoints.

   ![image](https://github.com/user-attachments/assets/5de021f6-5170-48f8-8722-1dd0a198d885)

- Menambahkan REST Endpoint

   Klik button create REST untuk mulai membuat endpoint baru

   ![image](https://github.com/user-attachments/assets/cd746c3b-fc84-483e-9683-f338614f2658)

- Isi Form REST Endpoint:

   setelah mengeklik create REST, akan terlihat form REST Endpoint yang harus diisi.

   Untuk Pengisian form REST endpoint tersebut dapat menggunakan 2 cara yaitu:

1. Dapat Test in graphql

   Pengisian form REST tersebut dapat diisi melalui test in graphql:

   - Klik button Test in graphql pada disebelah kanan atas, dibagian form Graphql Request
   - Selanjutnya pilih query atau mutation yang akan digunakan
   - Untuk query saya mengambil query GetTodos.

     Query ini digunakan untuk mengambil semua todos beserta detail user yang terkait.
     ```
     query todos {
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
   - Setelah memilih query yang ingin digunakan klik button REST pada kolom graphql. ditandai dengan warna kuning artinya button REST dipilih.

     ![image](https://github.com/user-attachments/assets/85b55023-ebbc-426f-99e7-df2349cc8ba5)

   - Setelah diklik, akan diarahkan kembali ke halaman form REST Endpoint, dan bagian GraphQL Request sudah terisi. 

     ![image](https://github.com/user-attachments/assets/3b1a7cd1-9b70-4d19-bd5e-ec65d49540d1)

   - Kemudian isi Name, Description (optional), URL Path dan Methods.

     Name: get-todos

     URL Path: http:/10.100.14.8:8083/api/rest/get-todos

     Methods: Pilih metode HTTP yang sesuai (GET, POST, PUT, atau DELETE). Disini saya menggunakan GET.

     ![image](https://github.com/user-attachments/assets/1b0ac3c6-b8fd-4b4a-ad9e-e7e8c21ed6e2)

   - Setelah form diisi, kemudian klik create. dan REST Endpoint telah dibuat
  
     ![image](https://github.com/user-attachments/assets/e67e324b-50ca-4b43-abe6-5d24257156ed)

2. Dapat diisi Manual

   Form REST Endpoint dapat juga diisi manual, yang dibedakan dari test in graphql yaitu pada bagian Graphql Requestnya.

   Bagian Graphql Request dalam pengisian manual dapat mengisi query atau mutation yang ingin digunakan dengan mengetik query atau mutation nya.

    ![image](https://github.com/user-attachments/assets/3b1a7cd1-9b70-4d19-bd5e-ec65d49540d1)

   Untuk pengisian lainnya seperti name, descriprtion, url path dan method pada form tersebut dapat diisi manual juga.
   
# Pengujian Query di Postman

Setelah endpoint REST dibuat, bisa mengaksesnya menggunakan tool seperti Postman.

1. Buat New Request di postman terlebih dahulu, kemudian pilih permintaannya seperti HTTP

   ![image](https://github.com/user-attachments/assets/3ce53611-f78b-49d6-aa85-8fca4eff914c)

2. Selanjutnya perhatikan method requestnya, gunakan sesuai kebutuhan request. Disini saya menggunakan GET

   ![image](https://github.com/user-attachments/assets/119d3ca6-ae8d-4de1-b063-d4715b583093)

3. Kemudian Masukan url REST Endpoint nya. Disini URL : http://10.100.14.8:8083/api/rest/get-todos

   ![image](https://github.com/user-attachments/assets/894c8fe6-fbae-4e1a-a67c-1df221d3f31e)

4. Jika menggunakan admin secret di Hasura, tambahkan `x-hasura-admin-secret` di kolom header:

   ![image](https://github.com/user-attachments/assets/1d30147a-1729-46d5-a304-4b1d1cc0d20d)

5. Jalankan REST Endpoint dengan mengeklik **SEND**. Hasil Output dapat terlihat dibawah ini:

   ![image](https://github.com/user-attachments/assets/4a12324e-35f4-45fc-8621-6b891c85aec4)

# Tambahkan REST Endpoint lainnya pada todosgraphql

Menambahkan REST Endpoint lainnya pada todosgraphql dengan membuat REST Endpoint nya terlebih dahulu.

![image](https://github.com/user-attachments/assets/f08bb2fb-9a98-4de1-bc95-3069c998779c)

Di gambar tersebut, saya sudah melakukan penambahan REST Endpoint lainnya. 

dengan query : get todo, get todos, get user, get users

# Menjalankan REST Endpoint lainnya di Postman

Kemudian, saya jalankan REST tersebut di postman dengan menggunakan metode request get. 

- query get todo : (where dan join)

  query ini mengambil satu tugas (todo item) berdasarkan ID yang diberikan sebagai argumen.

  ![image](https://github.com/user-attachments/assets/646d2065-2c2f-4178-81c3-8f7ca9e6c7af)

- query get users

query ini mengambil semua pengguna yang ada di database.

![image](https://github.com/user-attachments/assets/4fe66481-2aeb-43b8-9cca-434b957a86c9)

- query get user (where)

query ini mengambil satu pengguna (user) berdasarkan ID yang diberikan sebagai argumen.

![image](https://github.com/user-attachments/assets/f23f8445-5058-40cd-a480-accaaec92954)


   




     

     




     
