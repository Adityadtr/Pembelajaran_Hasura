# Pengertian CMD & CLI
CMD :

`cmd` adalah singkatan dari command yang berarti perintah. Dalam konteks sistem operasi, perintah adalah instruksi yang diberikan pengguna untuk dieksekusi oleh komputer. Perintah ini biasanya dimasukkan melalui antarmuka baris perintah seperti Command Prompt di Windows atau terminal di Linux.

Perintah-perintah tersebut dapat digunakan untuk melakukan berbagai tugas seperti mengelola file, menjalankan program, atau mengatur konfigurasi sistem.

CLI :

CLI adalah singkatan dari Command Line Interface, yaitu sebuah antarmuka pengguna berbasis teks di mana pengguna dapat memasukkan perintah langsung untuk berinteraksi dengan sistem operasi.

Tidak seperti antarmuka pengguna grafis (GUI), di CLI, pengguna harus mengetikkan perintah secara manual. CLI dianggap lebih efisien dan fleksibel bagi pengguna yang terbiasa, karena memungkinkan kontrol penuh atas sistem dengan perintah-perintah spesifik.

# Membuat Contoh Direktori 

Saya membuat contoh studi kasus proyek Sistem Kampus dengan direktori dibawah ini 

Direktori : Project_Sistem_Kampus

Direktori Folder  : Documents, Data, Scripts, Reports

Sub Direktori     : 

- Documents : academic, administration, students
  
- Data : raw_data, processed_data, backup

- Scripts : python, bash

File direktori : 

- academic : kurikulum.txt, jadwal_kuliah.txt

- administration : keuangan.txt, inventaris.txt

- students : biodata_mahasiswa.txt, nilai_mahasiswa.txt

- reports : semester1_report.txt, semester2_report.txt

# Membuat Contoh Direktori di Linux dengan Ubuntu Server 

Langkah 1 : Jalankan perintah berikut untuk membuat direktori dan sub-direktori

```
mkdir -p Project_Sistem_Kampus/documents/academic Project_Sistem_Kampus/documents/administration Project_Sistem_Kampus/documents/students

mkdir -p Project_Sistem_Kampus/data/raw_data Project_Sistem_Kampus/data/processed_data Project_Sistem_Kampus/data/backup

mkdir -p Project_Sistem_Kampus/scripts/python Project_Sistem_Kampus/scripts/bash

mkdir -p Project_Sistem_Kampus/reports

```
Perintah ini menggunakan mkdir -p untuk membuat direktori utama dan sub-direktorinya

Langkah 2 : Membuat File Kosong Menggunakan `touch`

```
touch Project_Sistem_Kampus/documents/academic/kurikulum.txt Project_Sistem_Kampus/documents/academic/jadwal_kuliah.txt
touch Project_Sistem_Kampus/documents/administration/keuangan.txt Project_Sistem_Kampus/documents/administration/inventaris.txt
touch Project_Sistem_Kampus/documents/students/biodata_mahasiswa.txt Project_Sistem_Kampus/documents/students/nilai_mahasiswa.txt
touch Project_Sistem_Kampus/data/raw_data/raw_students.csv Project_Sistem_Kampus/data/raw_data/raw_courses.csv
touch Project_Sistem_Kampus/data/processed_data/processed_students.csv Project_Sistem_Kampus/data/processed_data/processed_courses.csv
touch Project_Sistem_Kampus/reports/semester1_report.txt Project_Sistem_Kampus/reports/semester2_report.txt
```
Perintah ini akan membuat file kosong didalam direktori

Langkah 3 : Selanjutnya menambahkan isi di dalam file

```
echo "Daftar Kurikulum Semester Ganjil" > Project_Sistem_Kampus/documents/academic/kurikulum.txt
echo "Jadwal Kuliah Semester 1 Tahun 2023" > Project_Sistem_Kampus/documents/academic/jadwal_kuliah.txt
```
Perintah `echo` ini akan menambahkan atau menuliskan isi ke dalam file tersebut

# Menjalankan perintah ls, mv, rm dan tree

Langkah 1 : Menampilkan daftar direktori dan file menggunakan perintah `ls`

Untuk melihat isi direktori Project_Sistem_Kampus dapat menggunakan perintah `ls`:

```
ls Project_Sistem_Kampus
```
Jika ingin menampilkan file dan direktori beserta detail dapat menggunakan perintah `ls -l`:

```
ls -l Project_Sistem_Kampus
```
Langkah 2 : Memindahkan dan merename file dan direktori menggunakan perintah `mv`

Untuk Memindahkan file `processed_students.csv ` dari `data/processed_data` ke 'scripts` dapat menggunakan perintah `mv`:

```
mv Project_Sistem_Kampus/data/processed_data/processed_students.csv Project_Sistem_Kampus/scripts/
```
Untuk merename file `semester1_report.txt` menjadi `studi_semester_1.txt` didalam direktori `reports` dapat menggunakan `mv`:

```
mv Project_Sistem_Kampus/reports/semester1_report.txt Project_Sistem_Kampus/reports/studi_semester_1.txt
```
Langkah 3 : Menghapus Direktori dan File menggunakan perintah `rm`

Untuk menghapus File tertentu seperti menghapus file `processed_courses.csv` di dalam direktori `data` dapat menggunakan `rm`:

```
rm Project_Sistem_Kampus/data/processed_data/processed_courses.csv
```
Untuk menghapus Direktori 'scripts` beserta isinya dapat menggunakan `rm` :

```
rm -r Project_Sistem_Kampus/scripts/bash
```
Hati-hati saat menggunakan rm, karena file yang dihapus dengan perintah ini tidak dapat dipulihkan.

Langkah 4 : Mengecek Struktur Direktori dengan perintah `tree`

Install `tree` dahulu, untuk dapat digunakan perintah:

```
sudo apt-get install tree
```
Untuk melihat struktur direktori dan file yang telah dibuat, gunakan perintah tree:

```
tree Project_Sistem_Kampus
```
Untuk Hasil Output dapat lihat dibawah ini :

![image](https://github.com/user-attachments/assets/2018ccc0-3806-4dc4-b2e1-c2227bcba106)

# Mengecek Kapasitas RAM

Untuk mengecek kapasitas RAM di linux dapat menggunakan perintah `free`:

```
free -h
```
Perintah free menampilkan informasi mengenai penggunaan memori di sistem. 

Opsi -h (human-readable) membuat output lebih mudah dibaca dengan menampilkan ukuran dalam format yang lebih mudah dipahami (KB, MB, GB).

Hasil output :

![image](https://github.com/user-attachments/assets/9e30279b-b6ca-4a72-8e8e-f47ec0e79747)

Untuk menampilkan informasi lebih rinci dapat menggunakan perintah:

```
cat /proc/meminfo
```
Perintah ini menampilkan informasi rinci tentang memori sistem, termasuk total kapasitas RAM, penggunaan, buffer, cache, dan swap.

Hasil Output:

![image](https://github.com/user-attachments/assets/381f9f5e-b541-475a-bf74-b7eb711ff721)


# Mengecek Kapasitas CPU

Untuk mengecek kapasitas CPU dalam sistem dapat menggunakan perintah `lscpu`:

```
lscpu
```
Perintah lscpu menampilkan informasi detail mengenai arsitektur CPU, jumlah core, thread, kecepatan CPU, dan banyak lagi.

Hasil Output:

![image](https://github.com/user-attachments/assets/30bb4a43-b7e0-463c-bd40-6b4402ddb9ff)


Untuk menampilkan informasi lebih rinci dapat menggunakan perintah:

```
cat /proc/cpuinfo
```
Perintah ini menampilkan informasi rinci mengenai setiap core CPU, termasuk model, kecepatan, dan cache.

Hasil Output:

![image](https://github.com/user-attachments/assets/ee72cce8-8397-4ba4-8294-dfd06af85b4d)


# Mengecek Kecepatan Hard Disk 

Untuk mengecek kecepatan Baca/Tulis Hard Disk, dapat menggunakan perintah `hdparm`:

```
sudo hdparm -Tt /dev/sda
```
Perintah ini akan melakukan benchmark pada hard disk yang berada di /dev/sda.

Opsi -T mengukur kecepatan akses cache (buffered), sedangkan -t mengukur kecepatan baca langsung dari disk (disk read).

Hasil Output:

![image](https://github.com/user-attachments/assets/e72be022-5f50-45e9-9a5f-2beae8477e87)



