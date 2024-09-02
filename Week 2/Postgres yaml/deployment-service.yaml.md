# Analisa deployment-service.yaml pada postgres

File yaml :

```
apiVersion: apps/v1
```
Penjelasan:

Menentukan versi API yang digunakan untuk objek Deployment.
apps/v1 Ini digunakan untuk objek-objek yang berada dalam grup API apps, seperti Deployment, StatefulSet, dan DaemonSet.
Versi apps/v1 adalah yang paling umum digunakan dan stabil untuk objek-objek ini.

```
kind: Deployment
```
Penjelasan:

Menunjukkan bahwa ini adalah konfigurasi untuk sebuah Deployment, yang bertanggung jawab untuk mengelola dan menjalankan Pod-pod yang sesuai dengan template yang diberikan.

```
metadata:
  name: postgres
```
Penjelasan:

Nama dari Deployment, yang dalam hal ini adalah postgres. Nama ini digunakan untuk mengidentifikasi Deployment di dalam namespace.

```
spec:
  selector:
    matchLabels:
      app: postgres
```
Penjelasan:

Selector ini memastikan bahwa Deployment ini hanya akan mengelola Pod-pod yang memiliki label app: postgres.

```
  template:
    metadata:
      labels:
        app: postgres
```
Penjelasan:

Label ini akan ditambahkan ke setiap Pod yang dibuat oleh Deployment ini. Label ini penting untuk pemilihan Pod oleh Service.

```
    spec:
      containers:
```
Penjelasan:

Daftar container yang akan dijalankan di setiap Pod.

```
      - name: postgres
        image: postgres:11.1
```
Penjelasan:

Nama container, di sini postgres.

Image Docker yang digunakan untuk membuat kontainer. image ini adalah postgres versi 11.1.

```
        env:
        - name: PGDATA
          value: /var/lib/postgresql/data/pgdata
```
Penjelasan:

Lokasi direktori data Postgres di dalam kontainer.

```
        - name: POSTGRES_PASSWORD
          valueFrom:
            secretKeyRef:
              key: password
              name: postgres
```
Penjelasan:

Password untuk pengguna Postgres. Password ini diambil dari Secret Kubernetes dengan nama postgres dan kunci password.

```
        - name: POSTGRES_USER
          valueFrom:
            secretKeyRef:
              key: username
              name: postgres
```
Penjelasan:

Nama pengguna Postgres. Nama ini diambil dari Secret Kubernetes dengan nama postgres dan kunci username.

```
        - name: POSTGRES_DB
          valueFrom:
            secretKeyRef:
              key: dbname
              name: postgres
```
Penjelasan:

Nama basis data yang akan dibuat. Nama ini diambil dari Secret Kubernetes dengan nama postgres dan kunci dbname.

```
        resources:
```
Penjelasan:

Menentukan sumber daya yang dibatasi dan diminta oleh kontainer. sumber daya yang dimaksud merujuk pada kapasitas komputasi (seperti CPU dan memori) yang digunakan oleh kontainer di dalam Pod.

```
          limits:
            memory: "512Mi"
            cpu: "1"
```
Penjelasan:

limits: Batas maksimum sumber daya yang dapat digunakan oleh kontainer.

memory: "512Mi": Kontainer ini dibatasi menggunakan maksimal 512 MiB memori.

cpu: "1": Kontainer ini dibatasi menggunakan maksimal 1 vCPU.

```
          requests:
            memory: "256Mi"
            cpu: "100m"
```
Penjelasan:

request: Sumber daya (resource) minimum yang diminta oleh kontainer.

memory: "256Mi": Kontainer ini meminta setidaknya 256 MiB memori.

cpu: "100m": Kontainer ini meminta setidaknya 100 millicores (0.1 vCPU).

```
        ports:
        - containerPort: 5432
```
Penjelasan:

containerPort: 5432: Menunjukkan bahwa kontainer PostgreSQL di dalam Pod Kubernetes akan mendengarkan di port 5432. Ini berarti jika ada aplikasi lain dalam Pod yang sama, atau di Pod yang berbeda yang berkomunikasi dengan PostgreSQL, mereka harus mengarah ke port 5432 untuk mengakses database.

Port 5432 adalah port default yang digunakan oleh PostgreSQL untuk berkomunikasi dengan klien atau aplikasi yang ingin terhubung ke database PostgreSQL.

```
        volumeMounts:
        - mountPath: /var/lib/postgresql/data
          name: data
```
Penjelasan:

volumeMounts: Menentukan volume yang akan di-mount ke dalam kontainer.

mountPath: /var/lib/postgresql/data: Volume akan di-mount ke jalur ini di dalam kontainer.

name: data: Nama volume yang di-mount.

```
      volumes:
      - name: data
        persistentVolumeClaim:
          claimName: postgres
```
Penjelasan :

volumes: Menentukan volume yang digunakan oleh Pod.

name: data: Nama volume ini adalah data.

persistentVolumeClaim: Menunjukkan bahwa volume ini terkait dengan Persistent Volume Claim (PVC).

claimName: postgres: Nama PVC yang digunakan.

```
---
apiVersion: v1
```
Penjelasan:

Menentukan versi API yang digunakan untuk objek Service. v1 adalah versi yang umum digunakan untuk Service di Kubernetes.

```
kind: Service
```

Penjelasan:

Menunjukkan bahwa ini adalah konfigurasi untuk sebuah Service, yang bertugas untuk mengekspos aplikasi yang berjalan di Pod melalui jaringan.

```
metadata:
  name: postgres
```
Penjelasan:

name: postgres
Nama dari Service ini, yang dalam hal ini adalah postgres.

```
spec:
  selector:
    app: postgres
```
Penjelasan: 

Selector ini memastikan bahwa Service hanya akan mengarahkan trafik ke Pod-pod yang memiliki label app: postgres.

```
  ports:
  - port: 5432
    targetPort: 5432
```
Penjelasan: 

ports: Mendefinisikan port yang akan diekspos oleh Service.

port: 5432: Port 5432 akan diekspos oleh Service. artinya Service akan diekspos melalui port 5432. Ini berarti klien yang ingin mengakses Service ini akan menggunakan port 5432.

targetPort: 5432: Trafik yang diterima di port 5432 akan diteruskan ke port 5432 di dalam Pod yang terpilih. sehingga aplikasi di dalam Pod bisa menerima dan memproses permintaan tersebut.

# Catatan Kesimpulan

Deployment: 

Bagian ini mendefinisikan bagaimana Pod yang menjalankan PostgreSQL akan dibuat dan dikelola. Ini termasuk pengaturan container, environment variables, resources, dan volume yang diperlukan.

Service: 

Bagian ini mendefinisikan bagaimana Pod yang dibuat oleh Deployment akan diekspos ke jaringan, sehingga dapat diakses dari luar cluster atau oleh komponen lain dalam cluster.

# apiVersion: apps/v1 dan apiVersion: v1

apiVersion: apps/v1: Ini digunakan untuk objek-objek yang berada dalam grup API apps, seperti Deployment, StatefulSet, dan DaemonSet. 

Versi apps/v1 adalah yang paling umum digunakan dan stabil untuk objek-objek ini.

apiVersion: v1: Ini digunakan untuk objek-objek yang berada dalam grup API utama (core API group), seperti Pod, Service, ConfigMap, PersistentVolume, dan PersistentVolumeClaim. 

Versi ini tidak memerlukan prefiks grup karena merupakan bagian dari core API.

Jadi, Sebagai contoh:

Untuk Deployment, StatefulSet, atau DaemonSet, digunakan apiVersion: apps/v1.

Untuk Pod, Service, atau ConfigMap, digunakan apiVersion: v1.

# Limits: Memilih 512Mi Memori dan 1 CPU?

Memory (512Mi):

dalam 512MiB memungkinkan dianggap cukup untuk aplikasi yang dijalankan di dalam kontainer tersebut. Jika aplikasi memiliki kebutuhan memori yang lebih tinggi (misalnya, aplikasi yang memproses data besar), dapat memilih batas memori yang lebih besar.
Jika aplikasi terlalu banyak menggunakan memori (melebihi limits yang ditentukan), Kubernetes akan mencoba menghentikan kontainer tersebut untuk mencegah dampak pada kontainer lain yang berjalan di node yang sama (kondisi ini disebut OutOfMemory atau OOM).

CPU (1):

1 CPU berarti kontainer ini dapat menggunakan hingga satu vCPU (virtual CPU). Jika aplikasi yang berjalan membutuhkan banyak pemrosesan (seperti analisis data berat atau aplikasi yang memerlukan kalkulasi intensif), dapat memilih batas CPU yang lebih tinggi.
Jika aplikasi mencoba menggunakan lebih dari 1 CPU, Kubernetes akan menurunkan kinerjanya agar tetap dalam batas yang ditentukan, yang dapat memengaruhi kinerja aplikasi.

Apakah bisa mengganti nilai nya?

Nilai nilai tersebut bisa dapat diubah sesuai kebutuhan aplikasi. Penjelasan yaitu:

Dalam Mengubah Memori (memory):

Menurunkan Memori (misalnya, dari 512Mi ke 256Mi): Jika aplikasi menggunakan lebih dari 256MiB memori, ini bisa menyebabkan aplikasi tersebut berhenti atau menjadi tidak stabil karena kehabisan memori.

Meningkatkan Memori (misalnya, dari 512Mi ke 1Gi): Ini memberi aplikasi lebih banyak ruang memori untuk beroperasi. Tapi memungkinkan juga bisa dapat mengurangi jumlah Pod yang dapat dijalankan di node yang sama, tergantung pada total memori yang tersedia di node tersebut.

Dalam Mengubah CPU (cpu):

Menurunkan CPU (misalnya, dari 1 ke 500m): Aplikasi mungkin berjalan lebih lambat jika membutuhkan lebih banyak pemrosesan daripada yang tersedia. Ini dapat memperpanjang waktu respons aplikasi atau menyebabkan kegagalan

Meningkatkan CPU (misalnya, dari 1 ke 2 atau lebih): Aplikasi dapat memiliki lebih banyak kekuatan pemrosesan, yang dapat meningkatkan kinerjanya. tapi memungkinkan juga dapat mempengaruhi sumber daya yang tersedia untuk Pod lain di node yang sama.

# Request: Memilih 256Mib memori dan 100m cpu

requests adalah jumlah sumber daya (resource) minimum yang dijamin akan tersedia untuk kontainer saat dijalankan di Kubernetes. 

Kubernetes akan memastikan bahwa setidaknya jumlah ini tersedia pada node sebelum menjadwalkan Pod di sana.

Memory (memory: "256Mi"):

dalam 256MiB memori : 

Berarti kontainer ini meminta setidaknya 256 MiB (mebibyte) memori. Node yang akan menjalankan Pod ini harus memiliki setidaknya 256 MiB memori yang tidak terpakai untuk memastikan bahwa aplikasi dalam kontainer dapat berjalan dengan baik tanpa kehabisan memori.
Jika menetapkan requests memori terlalu rendah, dapat adanya risiko bahwa aplikasi mungkin kehabisan memori jika mencoba menggunakan lebih dari yang diminta, terutama jika ada kontainer lain yang bersaing untuk memori di node yang sama. tapi karena requests, ini adalah jumlah yang akan disediakan, bukan batas maksimal yang bisa digunakan.
CPU (cpu: "100m"):

dalam 100m cpu: 

Berarti container ini meminta setidaknya 100 millicores CPU, atau 0.1 vCPU (10% dari satu vCPU). Kubernetes akan menjadwalkan Pod ini hanya jika node memiliki setidaknya 100m CPU yang tidak terpakai.
Jika requests CPU terlalu rendah, container mungkin berjalan lebih lambat atau mengalami masalah kinerja, terutama di bawah beban kerja yang berat, karena Kubernetes hanya menjamin bahwa 100m CPU akan tersedia.

Apakah Bisa Mengganti Nilainya?

Nilai request tersebut bisa dapat diubah sesuai dengan kebutuhan aplikasi

Dalam Mengubah Memori (memory):

Menurunkan Memori (misalnya, dari 256Mi ke 128Mi): Jika aplikasi dapat berjalan dengan baik dengan memori yang lebih sedikit, berarti dapat menurunkan nilai requests. Ini akan memungkinkan Kubernetes untuk menempatkan Pod pada node dengan memori yang lebih sedikit, meningkatkan fleksibilitas penjadwalan.

Meningkatkan Memori (misalnya, dari 256Mi ke 512Mi): Jika aplikasi membutuhkan lebih banyak memori untuk berjalan dengan baik, berarti dapat meningkatkan nilai requests. Ini memastikan bahwa Kubernetes hanya menempatkan Pod pada node yang memiliki cukup memori, yang mengurangi risiko kehabisan memori.

Dalam Mengubah CPU (cpu):

Menurunkan CPU (misalnya, dari 100m ke 50m): Ini dapat dilakukan jika aplikasi membutuhkan lebih sedikit pemrosesan. tapi memungkinkan juga bisa meningkatkan risiko aplikasi dapat berjalan lambat jika CPU yang tersedia terbatas.

Meningkatkan CPU (misalnya, dari 100m ke 200m): Ini akan memastikan aplikasi memiliki lebih banyak CPU yang dijamin tersedia, yang berguna jika aplikasi membutuhkan lebih banyak kekuatan pemrosesan.
