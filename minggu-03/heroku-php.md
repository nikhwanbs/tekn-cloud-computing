<h1>Memulai Heroku dengan PHP</h1>

<h3>Set up</h3>
Sebelum Anda melanjutkan, periksa apakah Anda memiliki prasyarat yang diinstal dengan benar. Ketik setiap perintah di bawah ini dan pastikan itu menampilkan versi yang telah Anda instal. (Versi Anda mungkin berbeda dari contoh.) Jika tidak ada versi yang dikembalikan, kembali ke pengenalan tutorial ini dan instal prasyarat.

Semua penyiapan lokal berikut akan diperlukan untuk menyelesaikan "Deklarasikan dependensi aplikasi" dan langkah-langkah selanjutnya.
<br>
<img src=tgs/Screenshot_2.png>

<h3>Siapkan aplikasinya</h3>
Untuk menggandakan aplikasi sampel sehingga Anda memiliki versi lokal dari kode yang kemudian dapat Anda terapkan ke Heroku, jalankan perintah berikut di shell atau terminal perintah lokal Anda:
<br>
<img src=tgs/Screenshot_3.png>
<br>
Anda sekarang memiliki repositori git yang berfungsi yang berisi aplikasi sederhana serta file composer.json. Pastikan Anda telah menginstal Komposer. Heroku menggunakan Composer untuk manajemen ketergantungan dalam proyek PHP, dan file composer.json menunjukkan kepada Heroku bahwa aplikasi Anda dibuat dalam PHP.

<h3>Terapkan aplikasi</h3>
Pada langkah ini Anda akan menerapkan aplikasi ke Heroku.

Buat aplikasi di Heroku, yang mempersiapkan Heroku untuk menerima source code:
<br>
<img src=tgs/Screenshot_5.png>
<br>
Saat Anda membuat aplikasi, git remote (disebut heroku) juga dibuat dan dikaitkan dengan repositori git lokal Anda.

Sekarang terapkan code:
<br>
<img src=tgs/Screenshot_6.png>
<br>
Aplikasi sekarang diterapkan. Pastikan setidaknya satu contoh aplikasi sedang berjalan:
<br>
<img src=tgs/Screenshot_7.png>
<br>
Sekarang kunjungi aplikasi di URL yang dihasilkan oleh nama aplikasinya.
<br>
<img src=tgs/Screenshot_8.png>

<h3>View logs</h3>
Lihat informasi tentang aplikasi Anda yang sedang berjalan menggunakan salah satu perintah logging, heroku logs --tail:
<br>
<img src=tgs/Screenshot_7b.png>

<h3>Tentukan Procfile</h3>
Procfile di aplikasi contoh yang Anda terapkan terlihat seperti ini:
<br>
<img src=tgs/Screenshot_9.png>

<h3>Skala aplikasi</h3>
Anda dapat memeriksa berapa banyak dynos yang berjalan menggunakan perintah ps:
<br>
<img src=tgs/Screenshot_10.png>
<br>
Penskalaan aplikasi di Heroku sama dengan mengubah jumlah dino yang sedang berjalan. Skala jumlah web dynos ke nol:
<br>
<img src=tgs/Screenshot_11.png>
<br>
<img src=tgs/Screenshot_12.png>
<br>
Akses aplikasi lagi dengan menekan segarkan pada tab web, atau heroku terbuka untuk membukanya di tab web. Anda akan mendapatkan pesan kesalahan karena Anda tidak lagi memiliki web dynos yang tersedia untuk melayani permintaan.

Naikkan skalanya lagi:
<br>
<img src=tgs/Screenshot_13.png>
<br>
<img src=tgs/Screenshot_14.png>
<br>

<h3>Deklarasikan dependensi aplikasi</h3>
Heroku mengenali aplikasi sebagai PHP dengan adanya file composer.json di direktori root.

Aplikasi demo yang Anda terapkan sudah memiliki composer.json, dan tampilannya seperti ini:
<br>
<img src=tgs/Screenshot_15.png>
<br>
Jalankan perintah berikut untuk menginstal dependensi, mempersiapkan sistem Anda untuk menjalankan aplikasi secara lokal:
<br>
<img src=tgs/Screenshot_16.png>
<br>
<img src=tgs/Screenshot_17.png>
<br>

<h3>Push perubahan local</h3>
Pada langkah ini, Anda akan mempelajari cara menyebarkan perubahan lokal ke aplikasi melalui Heroku. Sebagai contoh, Anda akan memodifikasi aplikasi untuk menambahkan ketergantungan tambahan (pustaka Cowsay) dan kode untuk menggunakannya.

Pertama, gunakan composer untuk meminta dependensi baru:
<br>
<img src=tgs/Screenshot_18.png>
<br>
Ini juga akan mengubah composer.json. Jika Anda memperkenalkan dependensi dengan memodifikasi file composer.json sendiri, pastikan untuk memperbarui dependensi dengan menjalankan:
<br>
<img src=tgs/Screenshot_19.png>
<br>
Sekarang ubah web / index.php untuk menggunakan pustaka ini. Tambahkan rute baru setelah yang sudah ada, untuk / cowsay:
<br>
<img src=tgs/Screenshot_20.png>
<br>
Jika rute tersebut dikunjungi, maka akan menjadi sapi yang cantik.

Sekarang terapkan. Hampir setiap penerapan ke Heroku mengikuti pola yang sama ini.

Pertama, tambahkan file yang dimodifikasi ke repositori git lokal:
<br>
<img src=tgs/Screenshot_21a.png>
<br>
Sekarang komit perubahan ke repositori:
<br>
<img src=tgs/Screenshot_21b.png>
<br>
Sekarang terapkan, seperti yang Anda lakukan sebelumnya:
<br>
<img src=tgs/Screenshot_21c.png>
<br>
Terakhir, periksa apakah semuanya berfungsi:
<br>
<img src=tgs/Screenshot_23.png>
<br>
<img src=tgs/Screenshot_22.png>

<h3>Mulai shell interaktif</h3>
Anda dapat menjalankan perintah, biasanya skrip dan aplikasi yang merupakan bagian dari aplikasi Anda, dalam dyno satu kali menggunakan perintah run heroku. Ini juga dapat digunakan untuk meluncurkan shell PHP interaktif yang dilampirkan ke terminal lokal Anda untuk bereksperimen di lingkungan aplikasi Anda:
<br>
<img src=tgs/Screenshot_23b.png>
<br>
Untuk mendapatkan gambaran nyata tentang cara kerja dynos, Anda dapat membuat dyno sekali pakai dan menjalankan perintah bash, yang membuka shell di dyno tersebut. Anda kemudian dapat menjalankan perintah di sana. Setiap dyno memiliki ruang file efemeral sendiri, yang diisi dengan aplikasi Anda dan dependensinya - setelah perintah selesai (dalam hal ini, bash), dyno akan dihapus.
<br>
<img src=tgs/Screenshot_24.png>

<h3>Tentukan config vars</h3>
Heroku memungkinkan Anda mengeksternalisasi konfigurasi - menyimpan data seperti kunci enkripsi atau alamat sumber daya eksternal di config vars.

Saat runtime, config vars diekspos sebagai variabel lingkungan untuk aplikasi.

Ubah web / index.php sehingga rute root mengembalikan kata Hello yang diulangi dengan nilai variabel lingkungan TIMES:
<br>
<img src=tgs/Screenshot_24b.png>
<br>
Untuk menyetel config var di Heroku, jalankan yang berikut ini:
<br>
<img src=tgs/Screenshot_25b.png>
<br>
Lihat config vars yang disetel menggunakan konfigurasi heroku:
<br>
<img src=tgs/Screenshot_25.png>

<h3>Menyediakan database</h3>
Pasar add-on memiliki sejumlah besar penyimpanan data, dari penyedia Redis dan MongoDB, hingga Postgres dan MySQL. Pada langkah ini Anda akan menambahkan database dev Heroku Postgres Starter Tier gratis ke aplikasi Anda.

Tambahkan database:
<br>
<img src=tgs/Screenshot_26.png>
<br>
Ini membuat database, dan menyetel konfigurasi var DATABASE_URL (Anda dapat memeriksanya dengan menjalankan konfigurasi heroku).

Ubah composer.json agar menyertakan dependensi untuk penyedia layanan PDO sederhana, csanquer / pdo-service-provider:
<br>
<img src=tgs/Screenshot_27.png>
<br>
Instal dependensi baru:
<br>
<img src=tgs/Screenshot_28.png>
<br>
Sekarang ubah index.php untuk memperluas aplikasi untuk menambahkan koneksi PDO:
<br>
<img src=tgs/Screenshot_29b.png>
<br>
Perhatikan bagaimana kode ini mengambil config var DATABASE_URL dari lingkungan menggunakan getenv (), dan mengekstrak informasi tentang nama host, database dan kredensial dari config var tersebut menggunakan parse_url ().

Di file yang sama, tambahkan handler baru untuk membuat kueri database:
<br>
<img src=tgs/Screenshot_29v.png>
<br>
Ini memastikan bahwa ketika Anda mengakses aplikasi Anda menggunakan rute /db, itu akan mengembalikan semua baris dalam tabel test_table, dan menampilkan hasilnya menggunakan template database.twig. Buat template di direktori web/views:
<br>
<img src=tgs/Screenshot_29.png>
<br>
Jika Anda tersesat saat melakukan perubahan ini, lihat cabang db dari aplikasi sampel.

Terapkan modifikasi aplikasi ke Heroku:
<br>
<img src=tgs/Screenshot_30.png>
<br>
Jika sekarang Anda mengakses /db, Anda akan melihat Nameless di output karena tidak ada tabel di database. Dengan asumsi bahwa Anda telah menginstal Postgres secara lokal, gunakan perintah heroku pg: psql untuk terhubung ke database yang Anda sediakan sebelumnya, buat tabel dan masukkan baris:
<br>
<img src=tgs/Screenshot_31.png>
<br>
Sekarang saat Anda mengakses rute aplikasi /db, Anda akan melihat sesuatu seperti ini:
<br>
<img src=tgs/Screenshot_32.png>