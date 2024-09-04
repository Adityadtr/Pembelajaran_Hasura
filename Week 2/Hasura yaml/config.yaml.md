# Config yaml

config.yaml:

adalah file konfigurasi yang digunakan untuk menyimpan pengaturan atau parameter yang akan digunakan oleh aplikasi atau sistem, dalam hal ini Hasura. File ini biasanya dalam format YAML, yang merupakan format penulisan data yang sederhana dan mudah dibaca oleh manusia.

# Analisa config.yaml pada Hasura k8s

```
endpoint: http://localhost:8080
```
Penjelasan:

Ini adalah baris yang mendefinisikan endpoint atau URL yang digunakan oleh Hasura untuk berkomunikasi dengan server GraphQL.

`endpoint:`: Kata kunci ini mendefinisikan alamat URL yang akan digunakan oleh aplikasi atau alat yang berinteraksi dengan Hasura.

`http://localhost:8080`: Ini adalah nilai yang menunjukkan bahwa server Hasura dijalankan di localhost pada port 8080.

http://: Ini menunjukkan bahwa koneksi menggunakan protokol HTTP (Hypertext Transfer Protocol).

localhost: Ini adalah alamat yang mengacu pada mesin lokal di mana aplikasi atau server Hasura berjalan.

:8080: Ini menunjukkan port di mana server Hasura mendengarkan koneksi. Port 8080 sering digunakan untuk aplikasi web.

# Mengapa localhost:8080

`localhost:8080` sering digunakan sebagai endpoint default untuk aplikasi yang dijalankan secara lokal di komputer selama pengembangan. 

Ini berarti bahwa ketika menguji Hasura di lingkungan lokal, dapat mengaksesnya melalui browser atau alat lain dengan mengunjungi `http://localhost:8080`.

Dalam lingkungan Kubernetes, localhost mungkin perlu diganti dengan alamat IP atau nama DNS yang lebih spesifik, tergantung di mana Hasura dideploy. 

# Bisakah nilainya diubah

nilai endpoint ini dapat diubah sesuai dengan tempat di mana server Hasura di-host. Misalnya:

Jika Hasura diakses melalui alamat IP dalam jaringan lokal, endpoint mungkin menjadi `http://192.168.1.100:8080`. Alamat IP 192.168.1.100 adalah contoh alamat IP dalam jaringan lokal (private IP).

Jika mengakses Hasura melalui nama DNS di dalam cluster Kubernetes, mungkin dapat menggunakan `http://hasura-service:8080`. jika Service untuk Hasura dikonfigurasi dengan nama hasura-service.

Jika Hasura di-host di server jarak jauh, endpoint mungkin menjadi `http://example.com:8080`.

# Catatan Kesimpulan

File config.yaml ini mendefinisikan endpoint di mana aplikasi atau alat akan mengakses server Hasura.

`http://localhost:8080` menunjukkan bahwa Hasura berjalan di mesin lokal pada port 8080.

Dapat mengubah nilai endpoint ini sesuai dengan lingkungan di mana Hasura dijalankan, baik itu secara lokal, dalam Kubernetes, atau di server jarak jauh.
