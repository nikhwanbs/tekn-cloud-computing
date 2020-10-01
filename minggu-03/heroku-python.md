<h1>Memulai Heroku dengan Python</h1>
Tutorial ini akan membuat Anda menerapkan aplikasi Python (aplikasi Django sederhana) dalam beberapa menit.

<h3>Set up</h3>
Download aplikasi heroku, agar dapat digunakan lokal (menggunakan CMD). You use the CLI to manage and scale your applications, provision add-ons, view your application logs, and run your application locally.
<br>
<img src=lat/cliheroku.png>
<br>
Gunakan perintah heroku login untuk login ke Heroku CLI:
<br>
<img src=lat/login.png>
<h3>Siapkan aplikasinya</h3>
Pada langkah ini, Anda akan menyiapkan aplikasi sederhana yang dapat di-deploy.

Untuk meng-clone aplikasi sampel sehingga Anda memiliki versi lokal dari kode yang kemudian dapat Anda terapkan ke Heroku, jalankan perintah berikut di shell atau terminal perintah lokal Anda:
<br>
<img src=lat/clone.png>
<h3>Deploy aplikasinya</h3>
Membuat sebuah aplikasi di Heroku, yang mempersiapkan Heroku untuk menerima source code:
<br>
<img src=lat/Screenshot_1.png>
<br>
Sekarang terapkan kode Anda:
<br>
<img src=lat/Screenshot_2.png>
<img src=lat/Screenshot_3.png>
<br>
Aplikasi sekarang diterapkan. Pastikan setidaknya satu contoh aplikasi sedang berjalan:
<br>
<img src=lat/Screenshot_4.png>
<br>
Sekarang kunjungi aplikasi di URL yang dihasilkan oleh nama aplikasinya. Sebagai pintasan praktis, Anda dapat membuka situs web sebagai berikut:
<br>
<img src=lat/Screenshot_5.png>
<img src=lat/Screenshot_6.png>
<h3>View logs</h3>
Lihat informasi tentang aplikasi Anda yang sedang berjalan menggunakan salah satu perintah logging, heroku logs --tail:
<br>
<img src=lat/Screenshot_7.png>
<br>
Press Control+C untuk menghentikan streaming log.
<h3>Tentukan Procfile</h3>
Gunakan Procfile, file teks di direktori root aplikasi Anda, untuk secara eksplisit menyatakan perintah apa yang harus dijalankan untuk memulai aplikasi Anda.

Procfile di aplikasi contoh yang Anda terapkan terlihat seperti ini:
<br>
<img src=lat/procfile.png>
<h3>Skala aplikasi</h3>
Anda dapat memeriksa berapa banyak dynos yang berjalan menggunakan perintah ps:
<br>
<img src=lat/Screenshot_8.png>
<h3>Deklarasikan dependensi aplikasi</h3>
Heroku mengenali aplikasi sebagai aplikasi Python dengan mencari file kunci. Memasukkan requirements.txt di direktori root adalah salah satu cara Heroku mengenali aplikasi Python Anda.

Aplikasi demo yang Anda terapkan sudah memiliki requirements.txt, dan tampilannya seperti ini:
<br>
<img src=lat/req.png>
<br>
Untuk melakukan ini secara lokal, Anda dapat menjalankan perintah berikut:
<br>
<img src=lat/Screenshot_11.png>
<br>
Menginstal dependensi juga menyebabkan beberapa dependensi lainnya diinstal. Anda dapat melihatnya dengan menggunakan daftar fitur pip:
<br>
<img src=lat/Screenshot_12.png>
<br>
Setelah dependensi diinstal, Anda akan siap untuk menjalankan aplikasi Anda secara lokal.
<h3>Jalankan aplikasi secara lokal</h3>
Aplikasinya hampir siap untuk dimulai secara lokal. Django menggunakan aset lokal, jadi pertama-tama, Anda perlu menjalankan collectstatic:
<br>
<img src=lat/local.png>
<br>
Sama seperti Heroku, heroku lokal memeriksa Procfile untuk menentukan apa yang akan dijalankan.

Buka http: // localhost: 5000 dengan browser web Anda. Anda akan melihat aplikasi Anda berjalan secara lokal.

Untuk menghentikan aplikasi agar tidak berjalan secara lokal, kembali ke jendela terminal Anda dan tekan Ctrl + C untuk keluar.
<br>
<img src=lat/Screenshot_13.png>

<h3>Push perubahan lokal</h3>
Instal requests secara lokal:
<br>
<img src=lat/requests.png>
<br>
Dan kemudian tambahkan ke file requirements.txt:
<br>
<img src=lat/reqs.png>
<br>
Ubah hello / views.py sehingga itu mengimpor modul permintaan di awal:
<br>
<img src=lat/views.png>
<br>
Sekarang ubah metode indeks untuk menggunakan modul. Coba ganti metode indeks saat ini dengan kode berikut:
<br>
<img src=lat/index.png>
<br>
Sekarang uji secara lokal:
<br>
<img src=lat/locals.png>
<br>
Kunjungi lamaran Anda di http://localhost:5000. 
<br>
<img src=lat/Screenshot_15.png>
<br>
Sekarang terapkan. Hampir setiap penerapan ke Heroku mengikuti pola yang sama ini. Pertama, tambahkan file yang dimodifikasi ke repositori git lokal:

$ git add .
Sekarang komit perubahan ke repositori:

$ git commit -m "Demo"
Sekarang terapkan, seperti yang Anda lakukan sebelumnya:
<br>
<img src=lat/Screenshot_17.png>
<br>Terakhir, periksa apakah semuanya berfungsi:

$ heroku open 
<br>
<img src=lat/Screenshot_16.png>