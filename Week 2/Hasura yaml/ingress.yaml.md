# ingress.yaml

File ingress.yaml ini digunakan untuk mengatur Ingress di Kubernetes, yang merupakan cara untuk mengelola akses dari luar ke layanan yang berjalan dalam cluster Kubernetes, termasuk pengaturan HTTPS.

# Analisa ingress.yaml pada Hasura Kubernetes

```
apiVersion: extensions/v1beta1
```
Penjelasan:

Ini menunjukkan bahwa versi API yang digunakan untuk objek Ingress adalah extensions/v1beta1. 

API ini digunakan untuk mendefinisikan Ingress sebelum versi yang lebih baru. Dalam versi yang lebih baru, digunakan networking.k8s.io/v1.

```
kind: Ingress
```
Penjelasan:

Menunjukkan bahwa objek yang didefinisikan adalah Ingress, yang bertugas mengarahkan trafik dari luar ke layanan yang sesuai dalam cluster.

```
metadata:
  name: hasura
```
Penjelasan:

`metadata`: Bagian ini berisi metadata yang relevan, seperti nama dan anotasi untuk Ingress.

`name: hasura`:  Nama dari Ingress ini adalah hasura, yang digunakan untuk mengidentifikasinya di dalam cluster.

```
  annotations:
    kubernetes.io/ingress.class: "nginx"    
    certmanager.k8s.io/issuer: "letsencrypt-staging"
    #certmanager.k8s.io/issuer: "letsencrypt-prod"
    certmanager.k8s.io/acme-challenge-type: http01
```
Penjelasan:

`annotations`: adalah informasi tambahan yang dapat digunakan untuk konfigurasi khusus dari Ingress, seperti pengelolaan sertifikat TLS dan kelas Ingress yang digunakan.

`kubernetes.io/ingress.class: "nginx"`: Menunjukkan bahwa Ingress ini akan menggunakan Nginx sebagai pengendali Ingress (Ingress Controller). 

Nginx akan mengatur dan meneruskan trafik HTTP ke layanan yang diatur di dalam cluster.

`certmanager.k8s.io/issuer: "letsencrypt-staging"`: Menentukan bahwa sertifikat TLS akan dikelola oleh Cert-Manager menggunakan Let's Encrypt dengan lingkungan staging. Ini berguna untuk pengujian. 

Untuk produksi, dapat menggunakan `letsencrypt-prod` dengan menghapus komentar di baris tersebut.

`certmanager.k8s.io/acme-challenge-type: http01`: Menunjukkan bahwa tipe ACME challenge untuk verifikasi sertifikat adalah HTTP-01, yang berarti verifikasi akan dilakukan melalui HTTP di server.

```
spec:
```
Penjelasan: Bagian ini berisi spesifikasi tentang bagaimana Ingress akan bekerja, seperti aturan routing dan pengaturan TLS.

```
  tls:
  - hosts:
    - k8s-stack.hasura.app
    secretName: k8s-stack-hasura-app-tls
```
Penjelasan:

`tls`: Bagian ini mendefinisikan pengaturan TLS (Transport Layer Security) untuk akses HTTPS ke layanan.

`- hosts`: Ini adalah daftar nama host (domain) yang akan digunakan untuk akses TLS.

`- k8s-stack.hasura.app`: Host atau domain yang digunakan adalah k8s-stack.hasura.app. Ingress ini akan menangani semua trafik yang masuk ke domain ini melalui HTTPS.

`secretName: k8s-stack-hasura-app-tls`: Sertifikat TLS untuk domain k8s-stack.hasura.app akan disimpan dalam secret dengan nama k8s-stack-hasura-app-tls. Secret ini biasanya dihasilkan oleh Cert-Manager setelah sertifikat berhasil diterbitkan.

```
  rules:
  - host: k8s-stack.hasura.app
```
Penjelasan:

`rules`: Bagian ini mendefinisikan aturan bagaimana trafik yang masuk akan diarahkan ke layanan yang ada dalam cluster.

`host: k8s-stack.hasura.app`: Aturan ini berlaku untuk host k8s-stack.hasura.app. Semua permintaan HTTP/HTTPS yang datang ke domain ini akan mengikuti aturan di bawahnya.

```
    http:
```
Penjelasan: Bagian ini mendefinisikan aturan routing untuk permintaan HTTP.

```
      paths:
      - path: /
```
Penjelasan:

`paths`: Daftar rute (path) yang digunakan untuk mengarahkan permintaan ke layanan yang sesuai.

`path: /`: Semua trafik yang masuk ke root (/) dari domain k8s-stack.hasura.app akan diarahkan ke backend yang ditentukan di sini.

```
        backend:
          serviceName: hasura
          servicePort: 80
```
Penjelasan:

`backend`: Bagian ini mendefinisikan layanan Kubernetes mana yang harus menerima trafik dari Ingress.

`serviceName: hasura`: Trafik akan diarahkan ke layanan bernama hasura di dalam cluster.

`servicePort: 80`: Trafik akan diteruskan ke port 80 pada layanan hasura.

# Catatan Kesimpulan

File ingress.yaml ini digunakan untuk mengelola akses dari luar (internet) ke aplikasi Hasura yang berjalan di Kubernetes. 

Dengan Ingress ini, pengguna bisa mengakses Hasura melalui domain k8s-stack.hasura.app menggunakan HTTPS, dan trafik tersebut akan diarahkan ke layanan Hasura di port 80.

Ingress bertindak sebagai jembatan antara jaringan eskternal dan layanan internal di Kubernetes.

TLS memastikan komunikasi yang aman melalui HTTPS.

Cert-Manager dengan Let's Encrypt bertugas menangani pembuatan dan pembaruan sertifikat TLS secara otomatis.
