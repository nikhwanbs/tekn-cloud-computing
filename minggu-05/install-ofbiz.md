<h1> Install Apache Ofbiz</h1>
OFBiz adalah Sistem Enterprise Resource Planning (ERP) yang ditulis di Java dan menampung sejumlah besar perpustakaan, entitas, layanan, dan fitur untuk menjalankan semua aspek bisnis Anda.

<h2>Persyaratan Sistem</h2>

Satu-satunya persyaratan untuk menjalankan OFBiz adalah memiliki Java Development Kit (JDK)
versi 8 diinstal pada sistem Anda (bukan hanya JRE, tetapi JDK lengkap) yang dapat mengunduh dari tautan di bawah ini. 

https://adoptopenjdk.net/[JDK download]


<h2>Mulai cepat</h2>

Untuk menginstal dan menjalankan OFBiz dengan cepat, ikuti petunjuk di bawah ini dari command line di direktori root OFBiz (folder). 
Dan juga pastikan sudah menginstall gradle
<br>
<img src=img/gradle.png>
<h2>Unduh Gradle wrapper:</h2>
MS Windows: init-gradle-wrapper
<br>
<img src=img/gradlewrapper.png>
<h2>Bersihkan sistem dan muat data OFBiz lengkap</h2>

MS Windows: gradlew cleanAll loadAll
<br>
<img src=img/Screenshot_1.png>
<br>
Menunggu proses instalasi dan download hingga selesai
<br>
<img src=img/buildsuccess.png>
<h2>Memulai OFBiz:</h2>
MS Windows: gradlew ofbiz
<br>
<img src=img/start.png>
<br>
<img src=img/start2.png>
_______________________________________________________________________________<br>
Catatan: Abaikan indikator %  karena tugas ini tidak berakhir selama OFBiz sedang berjalan.<br>
_______________________________________________________________________________

<h2>Kunjungi OFBiz melalui browser Anda:</h2>

https://localhost:8443/webtools
Akan muncul tampilan informasi user login dan password
<br>
<img src=img/web.png>
<br>
Tampilan login
<br>
<img src=img/web2.png>
<br>
Tampilan awal Apache Ofbiz
<br>
<img src=img/web3.png>