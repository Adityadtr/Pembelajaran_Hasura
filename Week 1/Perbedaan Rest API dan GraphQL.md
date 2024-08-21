# Rest API

REST (Representational State Transfer) adalah arsitektur desain untuk membangun layanan web. REST API (Application Programming Interface) adalah antarmuka yang memungkinkan aplikasi untuk berkomunikasi satu sama lain menggunakan prinsip-prinsip REST. Berikut beberapa tentang REST API:

a) Metode HTTP (HTTP Method):

REST API menggunakan metode HTTP standar seperti GET, POST, PUT, DELETE untuk melakukan operasi pada data.

1. Get    : Mengambil data dari server
2. POST   : Mengirim data ke server untuk membuat entri baru.
3. PUT    : Memperbarui data yang ada di server.
4. DELETE : Menghapus data dari server.
   
b.  Stateless: 

Setiap permintaan dari klien ke server harus memuat semua informasi yang diperlukan untuk memproses permintaan tersebut. Server tidak menyimpan informasi tentang status permintaan sebelumnya.

Misalnya, jika aplikasi klien ingin mengakses data pengguna, klien harus mengirimkan semua informasi yang diperlukan (seperti identitas pengguna) dalam setiap permintaan. Server tidak akan mengingat klien tersebut dari permintaan sebelumnya; server hanya akan memproses permintaan saat itu berdasarkan informasi yang dikirim.

c. Berbasis Entitas: 

REST API berfokus pada entitas (entity) yang diidentifikasi oleh URL (Uniform Resource Locator). Dengan menggunakan URL untuk setiap entitas, REST API memungkinkan klien (seperti aplikasi web atau mobile) untuk dengan mudah melakukan operasi seperti mengambil, menambah, mengubah, atau menghapus data dari server. 
Misalnya, Menambah pengguna baru: POST https://api.example.com/users memungkinkan Anda mengirim data pengguna baru ke server.

d. Format Data: 

REST API umumnya menggunakan format data seperti JSON (JavaScript Object Notation) atau XML (Extensible Markup Language) untuk mengirim dan menerima data.

# GraphQL

GraphQL API dikembangkan oleh Facebook, dengan tujuan untuk mendapatkan sebuah API yang lebih fleksibel dan efisien. Pendekatan ini dapat menyelesaikan permasalahan yang ada sekarang dan juga permasalahan yang dihadapi pengembang pada saat mengembangkan API dengan menggunakan pendekatan REST API. Dirancang untuk memberikan lebih banyak kontrol kepada klien dalam hal data yang mereka terima dari server. 

Berikut beberapa tentang GraphQL:

1. Query:
Dengan GraphQL, klien dapat mengajukan query yang menentukan data spesifik yang mereka butuhkan, bukan hanya mendapatkan seluruh entitas atau koleksi. Misalnya, klien dapat meminta hanya nama dan email pengguna daripada seluruh objek pengguna.

3. Schema:
GraphQL menggunakan schema yang mendefinisikan tipe data dan relasi antara tipe data. Ini memudahkan pengembangan dan dokumentasi API karena schema menjelaskan secara jelas struktur data yang tersedia.

4. Single Endpoint:
Berbeda dengan REST API yang mungkin memiliki banyak endpoint untuk berbagai operasi, GraphQL biasanya menggunakan satu endpoint untuk semua permintaan.

5. Real-time Updates:
GraphQL memiliki fitur langganan (subscription) yang memungkinkan klien menerima pembaruan secara real-time ketika data di server berubah.

# Perbedaan Rest API dan GraphQL

1. Segi Definisi:
REST: seperangkat aturan yang mendefinisikan pertukaran data terstruktur antara klien dan server.
GraphQL: merupakan bahasa kueri, gaya arsitektur, dan seperangkat alat untuk membuat dan memanipulasi API.

2. Segi Kecocokan:
REST: bagus untuk sumber data sederhana di mana resource didefinisikan dengan baik.
GraphQL: bagus untuk sumber data besar, kompleks, dan saling terkait.

3. Segi Query:
REST API: Client harus melakukan beberapa permintaan ke berbagai endpoint untuk mendapatkan data yang berbeda. 
GraphQL: Client dapat melakukan satu query untuk mendapatkan semua data yang dibutuhkan, dan data tersebut dikembalikan dalam satu respons.

4. Dari Segi Fleksibilitas Data:
REST API: Respons seringkali berisi data lebih dari yang dibutuhkan karena format data diatur oleh server.
GraphQL: Klien memiliki kontrol penuh atas data yang diterima dengan menentukan secara eksplisit apa yang dibutuhkan.

5. Dari Segi Pengambilan Data:
REST API: sering kali mengharuskan client untuk mengakses beberapa titik akhir(Endpoint) untuk mengumpulkan data. Mereka menggunakan hierarchies route atau titik akhir (Endpoint), yang dapat mempersulit pengambilan data.
GraphQL: memungkinkan client untuk cukup mengirim kueri dengan persyaratan data mereka ke server, dan server merespons dengan objek JSON. JSON adalah format yang sangat umum digunakan untuk mengirimkan data antara server dan klien karena mudah dibaca dan diproses oleh aplikasi.
