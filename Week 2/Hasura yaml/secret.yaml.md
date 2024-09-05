# Secret.yaml

secret.yaml adalah file konfigurasi di Kubernetes yang digunakan untuk mendefinisikan resource Secret. 

Secret adalah cara Kubernetes untuk menyimpan data sensitif seperti password, API keys, database credentials, dan informasi lainnya secara aman.

# Analisa secret.yaml pada Hasura Kubernetes

```
apiVersion: v1
```
Penjelasan:

Bagian ini mendefinisikan versi API Kubernetes yang digunakan untuk membuat resource. Dalam hal ini, API version yang digunakan adalah v1, yang merupakan versi dasar untuk berbagai resource seperti Secret, ConfigMap, dan lainnya.

```
kind: Secret
```
Penjelasan:

`kind`: menunjukkan jenis resource yang sedang dibuat. 

`Secret`: berarti file ini digunakan untuk menyimpan data sensitif, seperti password, access key, atau URL koneksi database, secara terenkripsi. 

```
metadata:
  name: hasura
```
Penjelasan:

`Metadata`: bagian yang memberikan informasi dasar tentang resource Kubernetes, seperti nama, label, dan informasi lainnya yang membantu mengidentifikasi resource.

`name`: Menentukan nama secret yang dibuat, yaitu hasura. Nama tersebut digunakan untuk mengakses secret ini.

```
stringData:
```
Penjelasan: Bagian ini berisi data dalam bentuk string yang akan dienkripsi oleh Kubernetes sebagai bagian dari secret.

```
  accessKey: accessKey
```
Penjelasan:

`accessKey`: adalah kunci akses yang digunakan oleh Hasura untuk memastikan hanya klien yang memiliki kunci ini yang dapat mengakses konsol atau API GraphQL. nilai kuncinya adalah accessKey

  # only change postgres username, password and dbname as set
  # in postgres secret

```  
  dburl: postgres://username:password@postgres:5432/dbname
```
Penjelasan:

`dburl`: Ini adalah URL koneksi ke database PostgreSQL. URL ini berisi detail login seperti username, password, host (postgres), port (5432), dan nama database (dbname).

`postgres://`: Protokol yang digunakan untuk koneksi database PostgreSQL.

`username`: Nama pengguna yang digunakan untuk login ke database PostgreSQL.

`password`: Kata sandi yang digunakan untuk otentikasi ke database.

`@postgres`: Host di mana database berjalan, di sini postgres adalah nama service database yang akan di-resolve oleh Kubernetes.

`:5432`: Port default untuk PostgreSQL, yaitu 5432.

`/dbname`: Nama database yang digunakan oleh aplikasi Hasura.

  # Catatan Kesimpulan

`Secret` digunakan untuk menyimpan informasi sensitif seperti password dan akses URL tanpa menuliskannya secara terbuka dalam file deployment. Kubernetes menyimpan secret ini dalam format terenkripsi.

`Secret` digunakan oleh deployment Hasura untuk membaca variabel dburl dan accessKey, sehingga Hasura dapat terhubung ke database PostgreSQL dan menjaga akses API GraphQL tetap aman.
