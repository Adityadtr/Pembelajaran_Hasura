# deployment-service.yaml pada Hasura k8s

File `deployment-service.yaml` digunakan untuk mendefinisikan bagaimana aplikasi Hasura GraphQL Engine akan dijalankan dalam lingkungan Kubernetes.

File ini terdiri dari dua bagian utama: Deployment dan Service. 

`Deployment`: dalam Kubernetes adalah objek yang digunakan untuk mengelola pengaturan dan pengelolaan pod. Pod adalah unit paling dasar di Kubernetes yang menjalankan satu atau lebih kontainer.

`Service`: dalam Kubernetes adalah objek yang digunakan untuk mendefinisikan cara mengakses pod dalam cluster. Ini bertindak sebagai abstraksi jaringan yang mengarahkan trafik ke pod yang relevan.

# Analisa deployment-service.yaml pada Hasura

```
apiVersion: apps/v1
```
Penjelasan:

Menentukan versi API yang digunakan untuk membuat Deployment. apps/v1 adalah versi stabil yang digunakan untuk mendefinisikan objek Deployment.

```
kind: Deployment
```
Penjelasan

Menunjukkan bahwa objek yang didefinisikan adalah sebuah Deployment.

```
metadata:
  name: hasura
```
Penjelasan:

Nama dari Deployment ini adalah hasura, yang digunakan untuk mengidentifikasi deployment ini di dalam cluster Kubernetes.

```
spec:
```
Penjelasan: `spec` mendefinisikan spesifikasi untuk Deployment.

```
  selector:
    matchLabels:
      app: hasura
```
Penjelasan: 

matchLabels: Bagian ini menentukan label yang harus sesuai antara Deployment dan pod yang dikelolanya. 

Dalam hal ini, app: hasura digunakan sebagai label.

```
  template:
```
Penjelasan: Mendefinisikan `template` pod yang akan dibuat oleh Deployment.

```
    metadata:
      labels:
        app: hasura
```
Penjelasan:

`labels`: Label yang diberikan pada pod yang dibuat oleh template ini

yang dalam hal ini juga `app: hasura`: digunakan sebagai label

```
    spec:
```
Penjelasan: Mendefinisikan spesifikasi untuk pod, termasuk kontainer apa yang harus dijalankan.

```
      containers:
      - name: hasura
        image: hasura/graphql-engine:v1.0.0-alpha39
```
Penjelasan:

`containers`: Daftar kontainer yang akan dijalankan di dalam pod.

`name: hasura`: Nama dari kontainer ini adalah hasura.

`image: hasura/graphql-engine:v1.0.0-alpha39`: Menentukan image yang akan digunakan untuk menjalankan kontainer. Dalam hal ini, Hasura GraphQL Engine dengan versi v1.0.0-alpha39 akan digunakan.

```
        env:
        - name: HASURA_GRAPHQL_DATABASE_URL
          valueFrom:
            secretKeyRef:
              key: dburl
              name: hasura
        - name: HASURA_GRAPHQL_ACCESS_KEY
          valueFrom:
           secretKeyRef:
             key: accessKey
             name: hasura
        - name: HASURA_GRAPHQL_ENABLE_CONSOLE
          value: "true"
```
Penjelasan:

`env`: Daftar variabel lingkungan (environment variables) yang akan diatur untuk kontainer ini.

`HASURA_GRAPHQL_DATABASE_URL`: Mengatur URL database yang digunakan oleh Hasura.

`valueFrom: secretKeyRef`: berarti nilai variabel ini diambil dari sebuah Secret Kubernetes, yang dalam hal ini adalah secret dengan nama hasura dan kunci dburl.

`HASURA_GRAPHQL_ACCESS_KEY`: Mengatur kunci akses untuk Hasura.

`valueFrom: secretKeyRef`: Nilainya juga diambil dari Secret Kubernetes, kunci accessKey dari secret bernama hasura.

`HASURA_GRAPHQL_ENABLE_CONSOLE`: Mengaktifkan console Hasura.

`value: "true"`: Nilai ini diatur secara langsung sebagai string "true".

```
        resources:
          limits:
            memory: "256Mi"
            cpu: "500m"
          requests:
            memory: "128Mi"
            cpu: "50m"
```
Penjelasan:

`resources`: Bagian ini menentukan batasan sumber daya yang akan digunakan oleh kontainer.

`limits`: Batas maksimum sumber daya (resource) yang dapat digunakan kontainer.

`memory: "256Mi"`: Kontainer ini dibatasi menggunakan maksimal 256 MiB memori.

`cpu: "500m"`: Kontainer ini dibatasi menggunakan maksimal 500 millicores CPU (setengah dari satu CPU).

requests: Sumber daya minimum yang diminta oleh kontainer.

memory: "128Mi": Kontainer ini meminta setidaknya 128 MiB memori.

cpu: "50m": Kontainer ini meminta setidaknya 50 millicores CPU (0.05 vCPU).

```
        ports:
        - containerPort: 8080
```
Penjelasan:

ports: Daftar port yang akan diekspos oleh kontainer.

containerPort: 8080: Menentukan bahwa kontainer ini akan mendengarkan pada port 8080.

```
---
apiVersion: v1
```
Penjelasan:

`apiVersion: v1`: Menentukan versi API yang digunakan untuk membuat Service. v1 adalah versi stabil yang digunakan untuk objek Service.

```
kind: Service
```
Penjelasan: Menunjukkan bahwa objek yang didefinisikan adalah sebuah `Service`.

```
metadata:
  name: hasura
```
Penjelasan: Nama dari Service ini adalah `hasura`.

```
spec:
```
Penjelasan: Mendefinisikan spesifikasi untuk Service.

```
  selector:
    app: hasura
```
Penjelasan: 

`selector`: Menentukan pod mana yang harus dilayani oleh Service ini berdasarkan label.

`app: hasura`: Ini berarti Service akan mengarahkan trafik ke pod yang memiliki label app: hasura.

```
  ports:
  - port: 80
    targetPort: 8080
```
Penjelasan:

`ports`: Daftar port yang akan diekspos oleh Service.

`port: 80`: Menentukan bahwa Service akan mendengarkan pada port 80.

`targetPort: 8080`: Menunjukkan bahwa trafik yang diterima di port 80 akan diteruskan ke port 8080 pada pod target.

# Catatan Kesimpulan

Deployment: Mengelola bagaimana pod Hasura dijalankan, dengan konfigurasi seperti image yang digunakan, variabel lingkungan, dan batasan sumber daya (Resource).

Service: Memungkinkan pod Hasura untuk diakses melalui jaringan, dengan mengarahkan trafik dari port 80 ke port 8080 pada pod.
