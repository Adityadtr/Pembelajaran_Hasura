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

Kemudian save dengan mengeklik add remote schema:

# Integrasi Remote Schemas springboot di HASURA

Pada Hasura console, klik tab remote schemas terlebih dahulu:

![image](https://github.com/user-attachments/assets/d2e72068-423b-43f2-8b53-2d57066731c7)

Setelah itu, klik add untuk menambahkan remote schemas:

![image](https://github.com/user-attachments/assets/4634f296-e393-499d-9e0b-28d8ccf35331)

Terlihat beberapa isian detail untuk kita remote, masukkan endpoint pertama terlebih dahulu yaitu : http://10.100.14.10:8989/query

![image](https://github.com/user-attachments/assets/ec3bb4d8-757e-4260-a51c-6b10c79c2f85)

isilah :

Remote Schema Name : springbootGraphQL 

GraphQL Service URL : http://10.100.13.24:8088/apis/graphql

Kemudian save dengan mengeklik add remote schema:

![image](https://github.com/user-attachments/assets/2fff7ed7-5fd4-444d-97df-dab2acb0d972)

schemas springbootGraphQL berhasil di remote 

