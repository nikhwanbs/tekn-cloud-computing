<h1>Git Version</h1>

Git sudah terinstall, jadi langsung saya tes menggunakan cmd :
<br>
<img src=gambar/git-version.png>

<h1>Konfigurasi Git</h1>

Secara minimal, user harus memberitahu Git tentang username serta email yang digunakan setiap kali terjadi perubahan pada repo Git. Username serta email ini yang akan dimasukkan oleh Git ke catatan perubahan di repo. Di sistem operasi Linux atau sejanis (UNIX), konfigurasi ini nantinya akan disimpan di $HOME/.gitconfig. Untuk sistem operasi Windows, konfigurasi ini akan disimpan di C:\Document and Settings\NamaUser dengan nama file .gitconfig. Secara minimal, ada 2 hal yang perlu dikonfigurasi yaitu username dan email. Gunakan perintah berikut:

<img src=gambar/git-config.png>

Isian di atas harus disesuaikan dengan nama serta email yang digunakan untuk mendaftar di GitHub. Untuk melihat konfigurasi yang sudah ada:

<h1>Konfigurasi Git</h1>

Langkah ini cukup dilakukan sekali saja, kecuali jika ingin melakukan perubahan nama dan email.

<h1>Mengelola Repo Sendiri di Account Sendiri</h1>

<h2>Langkah-langkah</h2>

Setiap orang yang telah mempunyai account di GitHub bisa membuat repo dengan. Secara umum, langkah-langkahnya adalah sebagai berikut:

<ol>
<li>Buat repo kosong di GitHub, bisa public maupun private.</li>
<li>Cloe repo kosong tersebut di komputer lokal</li>
<li>Perintah berikutnya terkait dengan perubahan repo serta sinkronisasi antara GitHub dengan lokal.</li>

<h2>Membuat Repo</h2>

Untuk membuat repo, gunakan langkah-langkan berikut:

<ol>
<li>Klik tanda + pada bagian atas setelah login, pilih New repository</li>

<img src=gambar/new-repo.png>

<li>Isikan nama, keterangan, serta lisensi. Jika dikehendaki, bisa membuat repo Private</li>

<li>Klik Create Repository</li>
</ol>
Setelah langkah-langkah tersebut, repo akan dibuat dan bisa diakses menggunakan pola https://github.com/username/reponame. Pada repo tersebut, hanya akan muncul 1 file, yaitu LICENSE. Jika memilih membuat README pada saat langkah ke 2, juga akan muncul README.md. Ada atau tidak ada README.md tidak mempunyai efek apapun pada langkah ini.

<img src=gambar/repository.png>

<h2>Clone Repo</h2>

Proses clone adalah proses untuk menduplikasikan remote repo di GitHub ke komputer lokal. Untuk melakukan proses clone, gunakan perintah berikut:

<img src=gambar/clone-repo.png>

Setelah perintah ini, di direktori awesome-project akan disimpan isi repo yang sama dengan di GitHub. Perbedaannya, di komputer lokal terdapat direktori .git yang digunakan secara internal oleh Git.

<h2>Mengelola Repo</h2>

Setelah clone ke komputer lokal, semua manipulasi konten dilakukan di komputer lokal dan hasilnya akan di-push ke remote repo di GitHub. Dengan demikian, jangan berganti-ganti remote lokal, sekali dibuat disitu, tetap berada disitu. Jika kehilangan repo lokal, clone ulang ke direktori yang bersih (kosong) setelah itu baru lakukan pengelolaan repo. Beberapa hal yang biasanya dilakukan akan diuraikan berikut ini.

<h3>Mengubah Isi - Push Tanpa Branching dan Merging</h3>

Perubahan isi bisa terjadi karena satu atau kombinasi beberapa hal berikut:
<ol>
<li>File dihapus</li>
<li>File diedit</li>
<li>Membuat file / direktori baru</li>
<li>Menghapus direktori</li>
Untuk kasus-kasus tersebut, lakukan perubahan di komputer lokal, setelah itu push ke repo.

<img src=gambar/Screenshot_8.png>
<img src=gambar/Screenshot_9.png>
<img src=gambar/Screenshot_10.png>
<img src=gambar/Screenshot_11.png>
<img src=gambar/Screenshot_12.png>

Cara ini lebih mudah tetapi mempunyai resiko jika terjadi kesalahan dalam edit. Cara yang lebih aman tetapi memerlukan langkah yang lebih panjang adalah branching and merging

<h3>Mengubah Isi dengan Branching and Merging</h3>

Dengan menggunakan cara ini, setiap kali akan melakukan perubaham, perubahan itu dilakukan di komputer lokal dengan membuat suatu cabang yang nantinya digunakan untuk menampung perubahan-perubahan tersebut. Setelah itu, cabang itu yang akan dikirim ke repo GitHub untuk dimintai review kemudian digabungkan (merge) ke master. Secara umum, repo yang dibuat biasanya sudah mempunyai satu branch yang disebut dengan master. Cara ini lebih aman, terstruktur, terkendali, dan mempunyai history yang lebih baik. Jika perubahan yang kita buat sudah terlalu kacau dan kita menyesal, maka ada cara untuk "membersihkan" repo lokal kita. Secara umum, langkahnya adalah sebagai berikut:
<ol>
<li>Buat branch untuk menampung perubahan-perubahan</li>
<li>Lakukan perubahan-perubahan</li>
<li>Add dan commit perubahan-perubahan tersebut ke branch</li>
<li>Kembali ke repo master</li>
<li>Buat pull request di GitHub</li>
<li>Merge pull request di GitHub</li>
<li>Merge branch untuk menampung perubahan-perubahan tersebut ke master.</li>
<li>Selesai.</li>
</ol>

<img src=gambar/Screenshot_13.png>
<img src=gambar/Screenshot_14.png>
<img src=gambar/Screenshot_15.png>
<img src=gambar/Screenshot_16.png>

Setelah itu, kirim pull request (PR):<br>

<img src=gambar/Screenshot_17.png>

Setelah membuat PR, PR tersebut bisa di-merge:<br>

<img src=gambar/Screenshot_19.png>

Setelah itu, Confirm Merge, branch yang kita kirimkan tadi sudah dimasukkan ke branch master. Setelah itu, merge di komputer lokal:

<img src=gambar/Screenshot_21.png>

<h3>Sinkronisasi</h3>

Suatu saat, bisa saja terjadi kita menggunakan komputer lain dan mengedit repo melalui repo lokal di komputer lain, setelah itu pindah ke kamputer lain lagi. Saat itu, kita perlu melakukan sinkronisasi ke kemputer lokal. Perintah untuk sinkronisasi adalah:

<img src=gambar/Screenshot_21.png>

Perintah ini dikerjakan di direktori tempat repo lokal kita berada.

<h3>Membatalkan Perubahan</h3>

Praktik yang baik adalah membuat branch pada saat kita akan melakukan perubahan-perubahan. Jika perubahan-perubahan yang kita lakukan sudah sedemikian kacaunya, maka kita bisa membuat supaya perubahan-perubahan yang kacau tersebut hilang dan kembali ke kondisi bersih seperti semula.

<img src=gambar/Screenshot_22.png>

<h3>Undo Commit Terakhir</h3>

Suatu saat, mungkin kita sudah terlanjur mem-push perubahan ke repo GitHub, setelah itu kita baru menyadari bahwa perubahan tersebut salah. Untuk itu, kita bisa melakukan git revert.

<img src=gambar/Screenshot_23.png>
<img src=gambar/Screenshot_24.png>

Contoh di atas adalah contoh untuk mengubah README.md dengan beberapa commit. Setelh itu, kita akan mengembalikan ke posisi terakhir sebelum commit terakhir.

<img src=gambar/Screenshot_25.png>

Perintah di atas akan membuka editor. Pada editor tersebut kita bisa mengetikkan pesan revert ( = pesan commit untuk pembatalan). Setelah selesai, simpan:

<img src=gambar/Screenshot_26.png>

Selanjutnya, tinggal di-push ke repo GitHub.

<img src=gambar/Screenshot_27.png>

Jika commit sudah dilakukan, tetapi belum di-push ke repo GitHub (masih berada di lokal), cara membatalkannya:

<img src=gambar/Screenshot_28.png>

Untuk kembali ke perubahan pada saat yang sudah lama, yang perlu dilakukan adalah melakukan git revert <posisi> kemudian mengedit secara manual kemudian push ke repo.

<img src=gambar/Screenshot1.png>

Setelah itu, jika dilihat pada file, akan muncul tambahan untuk memudahkan meng-edit. File ini harus di-resolve terlebih dahulu, setelah itu baru di add dan commit:

<img src=gambar/Screenshot2.png>

Edit file tersebut, setelah itu simpan.

<img src=gambar/Screenshot_29.png>

<img src=gambar/Screenshot3.png>

Setelah itu, lanjutkan proses revert. Saat git revert --continue isikan pesan revert.

<img src=gambar/Screenshot_30.png>