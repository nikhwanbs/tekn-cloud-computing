<h1>DevStack</h1>
<h2>Install Linux</h2>
Start with a clean and minimal install of a Linux system. 
Pada praktik kali ini menggunakan Ubuntu 18.04 (Bionic Beaver).
<h2>Menambah Stack User (optional)</h2>
DevStack harus dijalankan sebagai pengguna non-root dengan sudo diaktifkan 

Jika Anda tidak menggunakan cloud image, Anda dapat membuat pengguna stack terpisah untuk menjalankan DevStack
<br>
<img src=img/Screenshot1.png>
<br>
Karena pengguna ini akan membuat banyak perubahan pada sistem Anda, ia harus memiliki hak sudo:
<br>
<img src=img/Screenshot2.png>
<br>
<h2>Download DevStack</h2>
<br>
<img src=img/Screenshot3.png>
<br>
Repo devstack berisi skrip yang menginstal OpenStack dan template untuk file konfigurasi.
<h2>Membuat file local.conf</h2>
Buat file local.conf dengan empat kata sandi yang telah ditetapkan di root repo git devstack.
<br>
<img src=img/Screenshot4.png>
<br>
Ini adalah konfigurasi minimum yang diperlukan untuk memulai dengan DevStack.
<h2> Mulai penginstalan</h2>
<br>
<img src=img/Screenshot5.png>
<img src=img/Screenshot6.png>
<br>
Ini akan memakan waktu 15 - 20 menit, sebagian besar tergantung pada kecepatan koneksi internet.