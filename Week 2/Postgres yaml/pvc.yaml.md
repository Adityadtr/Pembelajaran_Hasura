# pvc.yaml

File ini digunakan untuk membuat `PersistentVolumeClaim` (PVC) di Kubernetes.

`PersistentVolumeClaim` (PVC): 

Sebuah permintaan penyimpanan dari aplikasi yang berjalan di Kubernetes. PVC memungkinkan aplikasi untuk mendapatkan akses ke penyimpanan yang stabil dan persisten (data tidak hilang meskipun pod dimatikan atau di-restart).

PVC mendefinisikan ukuran penyimpanan, mode akses (misalnya, hanya bisa dibaca atau ditulis), dan jenis penyimpanan yang dibutuhkan aplikasi.

Lebih singkatnya : `pvc.yaml` digunakan untuk memastikan aplikasi memiliki akses ke penyimpanan yang dibutuhkan.

# Analisa pvc.yaml pada postgres

File Yaml:

```
apiVersion: v1
```
Penjelasan: 

apiVersion menunjukkan versi API Kubernetes yang digunakan untuk membuat objek. Dalam hal ini, v1 adalah versi pertama dari API Kubernetes untuk objek seperti PersistentVolumeClaim.

```
kind: PersistentVolumeClaim
```
Penjelasan:

`kind` menunjukkan jenis objek yang akan dibuat. Di sini, jenis objeknya adalah `PersistentVolumeClaim`.

`PersistentVolumeClaim` (PVC) adalah permintaan untuk mengalokasikan atau meminta akses ke `PersistentVolume` (PV) di Kubernetes. 

`PVC` digunakan oleh Pod untuk menyimpan data yang membutuhkan penyimpanan tetap, bahkan ketika Pod dihentikan atau dihapus

```
metadata:
  name: postgres
```
Penjelasan:

`metadata`: Bagian ini berisi informasi metadata untuk PVC, seperti nama yang akan diberikan kepada PVC ini.

`Metadata` membantu mengidentifikasi objek di Kubernetes.

`name: postgres`: Nama PVC ini adalah postgres. Nama tersebut digunakan oleh Pod untuk merujuk pada PVC saat membutuhkan penyimpanan.

```
spec:
```
Penjelasan :

Bagian spec (spesifikasi) mendefinisikan konfigurasi dan persyaratan PVC.

```
  accessModes:
  - ReadWriteOnce
```
Penjelasan :

`accessModes` : menentukan mode akses yang dibutuhkan oleh PVC. Dalam yaml ini mode akses nya itu `readwriteonce`

`ReadWriteOnce`: Penyimpanan dapat di-mount untuk dibaca dan ditulis oleh satu Pod pada satu waktu.

Mode akses mengatur bagaimana penyimpanan dapat diakses oleh Pod. Mode ini memastikan bahwa hanya satu Pod yang dapat menulis ke penyimpanan pada saat yang bersamaan, yang dapat mencegah konflik data.

```
  storageClassName: default
```
Penjelasan :

`storageClassName` mengacu pada kelas penyimpanan yang digunakan oleh PVC. default berarti PVC ini akan menggunakan `StorageClass` default yang telah dikonfigurasi di cluster Kubernetes.

`StorageClass` menentukan jenis penyimpanan (seperti SSD atau HDD) dan penyediaan untuk PVC. 

Dengan `storageClassName: default`, Kubernetes akan menggunakan pengaturan default untuk jenis penyimpanan yang sesuai dengan kebutuhan.

```
  resources:
```
Penjelasan:

Bagian ini menunjukkan jumlah sumber daya penyimpanan yang diminta oleh PVC.

Menentukan berapa banyak penyimpanan yang diperlukan oleh aplikasi. Jika nilai yang diminta tidak tersedia, PVC tidak akan dibuat hingga kapasitas tersedia.

```
    requests:
```
Penjelasan:

Bagian ini mendefinisikan jumlah penyimpanan yang diminta oleh PVC.

Permintaan ini akan diperiksa oleh Kubernetes untuk melihat apakah PersistentVolume (PV) yang ada dapat memenuhi permintaan ini. Jika ya, PVC akan terikat ke PV yang tersedia. Jika tidak, PVC akan tetap dalam status Pending hingga PV yang sesuai tersedia.

```
      storage: 5Gi
```
Penjelasan: 

storage: 5Gi: Ini adalah jumlah penyimpanan yang diminta oleh PVC, dalam hal ini sebesar 5GiB (gibibyte).

# Catatan Kesimpulan

File pvc.yaml ini membuat PersistentVolumeClaim yang meminta 5GiB penyimpanan dengan mode akses ReadWriteOnce, menggunakan StorageClass default di cluster Kubernetes. 

PVC ini akan digunakan oleh Pod yang membutuhkan penyimpanan tetap, seperti untuk basis data PostgreSQL, yang memerlukan penyimpanan agar data tetap ada meskipun Pod dihentikan atau direstart.

Visualisasi Alur:

PVC Dibuat: File pvc.yaml dijalankan di Kubernetes untuk membuat PVC.

PVC Mencari PV: PVC akan mencari PersistentVolume (PV) yang sesuai dengan permintaan (misalnya, penyimpanan 5GiB).

PVC Terikat ke PV: Jika PV yang sesuai ditemukan, PVC akan terikat ke PV tersebut dan dapat digunakan oleh Pod.

Pod Menggunakan PVC: Pod yang membutuhkan penyimpanan akan merujuk ke PVC ini untuk menyimpan dan mengakses data.

# Tentang storage: 5Gi

storage: 5Gi: 

Ini menunjukkan bahwa PersistentVolumeClaim (PVC) meminta alokasi penyimpanan sebesar 5 GiB (gibibyte). 

Gi (Gibibyte) adalah ukuran penyimpanan berbasis biner (1 GiB = 1024 MiB = 1,073,741,824 bytes).

Apakah Nilainya Bisa Diubah?

nilai storage di PVC bisa diubah sesuai kebutuhan. dapat menyesuaikannya ke jumlah penyimpanan yang lebih besar atau lebih kecil, tergantung pada kebutuhan aplikasi.

Ada dampak dalam mengubah nilai storage:

Peningkatan penyimpanan:

Jika menambah kapasitas penyimpanan dengan mengubah nilai storage menjadi lebih besar, Kubernetes akan mencari PersistentVolume (PV) yang memiliki cukup ruang untuk memenuhi permintaan baru ini.

Namun, jikamenggunakan PVC yang ada dan ingin meningkatkan ukurannya, harus memeriksa apakah PV dan StorageClass yang digunakan mendukung fitur resize.

Pengurangan Penyimpanan :

Secara umum, Kubernetes tidak mendukung pengurangan ukuran PVC yang sudah digunakan. Jika perlu mengurangi kapasitas, memungkinkan harus membuat PVC baru dengan ukuran yang lebih kecil, memindahkan data dari PVC yang lama ke yang baru, dan kemudian menghapus PVC yang lama.

kesimpulannya : Menambah penyimpanan pada PVC relatif lebih mudah daripada menguranginya
