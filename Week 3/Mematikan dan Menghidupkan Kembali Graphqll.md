# Mematikan Sumber Graphql

Disini saya ingin mematikan sumber graphql pada todosgraphql dengan menggunakan rancher, dapat dilihat dibawah ini :

. Pertama Akses Rancher UI atau CLI untuk Kubernetes.

. Pilih Cluster yang sesuai dan cari deployment untuk todosgraphql

. Di bagian Workloads:

- Klik pada todosgraphql.

- Ubah jumlah replicas menjadi 0.

![image](https://github.com/user-attachments/assets/1af45995-08e3-4993-b3f3-c5105a8ff026)

# Analisis Error di Hasura setelah Mematikan Sumber GQL

. Setelah mematikan sumber gqlnya (todosgraphql), selanjutnya mengakses Hasura Console.

. Kemudian melakukan query dari schema todosgraphql di Postman:

```
query findAllAuthors {
  todosRemote {
    todos {
      id
      text
      done
    }
  }
}
```
. Hasil Outputnya akan terdapat error pada network, karena Hasura tidak dapat terhubung ke endpoint remote schema yang sudah tidak aktif. (karena sumber gql sudah di nonaktifkan)

![WhatsApp Image 2024-09-23 at 13 32 46](https://github.com/user-attachments/assets/20aeb11c-1171-467c-aadd-04c2f6a00b40)

# Menghidupkan Kembali Sumber GQL (Scale Up ke 1)

. Kembali ke Rancher UI.

. Ubah jumlah replicas dari 0 ke 1 untuk todosgraphql 

. Tunggu hingga pods aktif kembali.

![image](https://github.com/user-attachments/assets/f4151fa2-4206-4e37-a234-c9a0d44dcc52)

# Uji Query dari Postman setelah Sumber GQL Dihidupkan (Tanpa Reload Schema)

. Setelah GQL kembali dihidupkan, coba lakukan query kembali di Postman, tanpa melakukan reload schema di Hasura Console.

. Melakukan query yang sama seperti sebelumnya, contohnya query todos:

```
query findAllAuthors {
  todosRemote {
    todos {
      id
      text
      done
    }
  }
}
```
Hasil Output:

![WhatsApp Image 2024-09-23 at 13 36 02](https://github.com/user-attachments/assets/f89e01e2-9f9f-48f2-959a-4c43ae277cad)

Jika schema masih tidak terhubung dengan benar, bisa mendapatkan error seperti remote-schema-error.

Namun, jika koneksi telah kembali normal, query akan berhasil dijalankan tanpa error, dan hasil query akan mendapatkan data yang sesuai dari remote schema.

# Kesimpulan

. Setelah scale down, Hasura tidak bisa mengakses schema dan query melalui Postman akan gagal.

. Setelah scale up dan tanpa reload schema, query dapat kembali berhasil dijalankan melalui postman 

. Tapi jika query tetap gagal, karena Hasura masih menggunakan schema lama.

. Untuk memperbaikinya, harus melakukan reload schema dari Hasura Console agar schema di-refresh dan kembali berjalan normal.
