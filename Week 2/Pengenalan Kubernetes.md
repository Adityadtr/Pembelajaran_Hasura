# Apa Itu Kubernetes

Kubernetes (k8s) adalah sebuah platform open-source yang digunakan untuk mengotomatisasi deployment, scaling, dan manajemen aplikasi containerized.

Kubernetes memungkinkan untuk menjalankan container secara efisien di berbagai lingkungan, baik on-premise, di cloud, maupun hybrid.

Kubernetes awalnya dikembangkan oleh Google dan sekarang dikelola oleh Cloud Native Computing Foundation (CNCF). Inti dari Kubernetes adalah memastikan bahwa aplikasi berjalan dengan cara yang diinginkan, baik itu dalam hal ketersediaan, skalabilitas, maupun kinerja.

Kontainer sendiri adalah environment dengan resource, CPU, dan sistem file untuk satu aplikasi. Jadi, aplikasi tersebut akan memiliki resource sendiri.

Kubernetes memiliki kemampuan untuk melakukan penjadwalan aplikasi, load balancing server dan peningkatan kapasitas kontainer secara otomatis. 

Kubernetes kini banyak digunakan untuk membangun microservices, yaitu aplikasi kecil yang menjadi pengembangan dari aplikasi besar dan saling terhubung satu sama lain. 

Dengan menggunakan Kubernetes, proses pengembangan aplikasi jadi lebih cepat karena proses scale up aplikasi tidak dibuat sekaligus seperti pada pendekatan monolith.

# Kelebihan Kubernetes

1. Otomatisasi dan Skalabilitas:

Kubernetes secara otomatis menangani penjadwalan dan deployment container, sehingga memudahkan proses scaling aplikasi berdasarkan kebutuhan. Kubernetes juga dapat secara otomatis memulihkan container yang gagal dan menyeimbangkan beban kerja.

2. Portabilitas:

Kubernetes dapat berjalan di berbagai platform, baik di cloud (seperti AWS, GCP, Azure) maupun on-premise, sehingga aplikasi dapat dengan mudah dipindahkan dari satu lingkungan ke lingkungan lain.

3. Pengelolaan Resource:

Kubernetes memungkinkan pengelolaan resource secara efisien, seperti CPU dan memori, melalui fitur seperti limit dan request yang dapat dikonfigurasi untuk setiap container.

4. Ekosistem yang Kuat:

Kubernetes memiliki ekosistem yang sangat kuat dengan banyak alat pendukung, seperti Helm untuk manajemen package, Prometheus untuk monitoring, dan Istio untuk service mesh.

5. High Availability:

Kubernetes dirancang untuk mendukung aplikasi yang membutuhkan high availability dengan cara menyediakan replikasi dan distribusi container secara otomatis.

# Kekurangan Kubernetes

1. Kompleksitas:

Kubernetes memiliki kurva pembelajaran yang cukup kompleks. Pengelolaan cluster Kubernetes dapat menjadi kompleks, terutama saat skalanya besar.
Proses instalasi dan konfigurasi yang kompleks.

2. Overhead:

Penggunaan Kubernetes bisa memerlukan resource yang signifikan, baik dari sisi infrastruktur maupun dari sisi administrasi. Ini bisa menjadi tantangan bagi organisasi kecil atau startup dengan resource terbatas.

3. Keamanan:

Meskipun Kubernetes memiliki berbagai fitur keamanan, pengelolaan keamanannya bisa menjadi tantangan, terutama jika tidak dikelola dengan benar. harus memastikan konfigurasi yang aman untuk mencegah potensi ancaman keamanan.

# Network Kubernetes

Network di Kubernetes adalah bagian penting yang menghubungkan container-container di dalam cluster agar bisa saling berkomunikasi, baik antar container, dengan service di luar cluster, atau dengan pengguna akhir. Berikut adalah konsep dasar jaringan di Kubernetes:

Pod Network:

Setiap Pod di Kubernetes memiliki alamat IP sendiri yang unik dalam sebuah cluster. Pod dapat berkomunikasi satu sama lain menggunakan IP ini tanpa perlu NAT (Network Address Translation).

Service:

Service di Kubernetes bertindak sebagai abstraksi yang menghubungkan satu atau lebih Pod ke alamat IP virtual yang stabil. Service ini memungkinkan akses ke aplikasi meskipun Pod yang mendukungnya berubah atau di-scaling.

Network Policies:

Kubernetes memungkinkan untuk mengontrol alur jaringan di dalam cluster menggunakan Network Policies. Ini memungkinkan menentukan aturan tentang bagaimana Pod dapat berkomunikasi satu sama lain, memberikan keamanan tambahan.

Ingress:

Ingress adalah objek Kubernetes yang mengatur akses ke service dalam cluster dari luar. Ingress memungkinkan untuk mengatur routing HTTP dan HTTPS, menyediakan fitur seperti load balancing, SSL termination, dan host/path-based routing.


# Volume Kubernetes

Volume di Kubernetes adalah mekanisme penyimpanan data yang memungkinkan container di dalam Pod untuk menyimpan dan berbagi data. Ada berbagai jenis volume di Kubernetes, masing-masing dengan karakteristik dan kegunaan yang berbeda:

emptyDir:

Volume ini dibuat ketika Pod dimulai dan dihapus ketika Pod dihapus. Ini cocok untuk menyimpan data sementara yang tidak perlu dipertahankan.

hostPath:

Volume ini mengacu pada path di host node tempat Pod berjalan. Ini berguna untuk aplikasi yang membutuhkan akses langsung ke file system node.

persistentVolume (PV) dan persistentVolumeClaim (PVC):

PV adalah representasi dari resource penyimpanan di luar Kubernetes, seperti disk pada cloud provider, NFS, atau storage lain yang dapat diakses. 

PVC adalah permintaan oleh user untuk PV dengan spesifikasi tertentu. PV dan PVC memungkinkan data untuk bertahan meskipun Pod dihapus atau dipindahkan.

configMap dan secret:

Ini adalah volume khusus untuk menyimpan data konfigurasi atau data sensitif seperti password atau API keys. configMap digunakan untuk menyimpan data konfigurasi, sementara secret digunakan untuk menyimpan data sensitif.

Network File System (NFS):

Kubernetes juga mendukung NFS sebagai jenis volume, memungkinkan beberapa Pod untuk berbagi akses ke sistem file yang sama.

Cloud Storage Volumes:

Kubernetes mendukung berbagai penyimpanan cloud, seperti Google Persistent Disk, Amazon EBS, atau Azure Disk, yang memungkinkan integrasi dengan penyimpanan cloud untuk kebutuhan penyimpanan data.
