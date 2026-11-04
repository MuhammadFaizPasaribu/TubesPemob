# Aplikasi rawat jalan JKN Rumah Sakit Kensato

Repositori ini berisi aplikasi Android untuk pelayanan rawat jalan pasien JKN di Rumah Sakit Kensato. Aplikasinya dibuat dengan Kotlin dan Jetpack Compose. Datanya disimpan di database lokal (Room), jadi aplikasi bisa dijalankan tanpa server. README ini khusus membahas level user pasien, yang sekarang masih setengah jadi.

## Level user pasien

Di aplikasi ini pasien cuma punya satu urusan, yaitu menebus obat setelah diperiksa dokter. Pasien masuk dengan No. RM sebagai username dan tanggal lahir sebagai kata sandi, ditulis tanpa pemisah (ddmmyyyy). Untuk mencoba, pakai akun Budi Santoso dengan No. RM 00012345 dan sandi 15011980.

Setelah login, pasien masuk ke beranda dengan sapaan "Halo, Budi Santoso" dan tombol Keluar di kanan atas. Di bagian bawah ada dua tab. Tab Resep saya menampilkan resep yang masih aktif di atas, lalu riwayat resep yang sudah selesai di bawahnya. Setiap kartu resep berisi status, poli, nama dokter, tanggal, dan jumlah obat. Kalau obatnya sudah siap diambil, kartunya berubah hijau dan ada tulisan yang mengarahkan pasien ke loket farmasi.

Tab Notifikasi berisi pemberitahuan dari farmasi, misalnya saat obat sudah siap atau sudah diserahkan. Angka di ikon tab menunjukkan jumlah notifikasi yang belum dibaca, dan angka itu hilang begitu tabnya dibuka. Notifikasi bisa diketuk untuk langsung membuka resepnya. Saat obat siap, HP juga memunculkan notifikasi di status bar.

## Halaman detail resep

Halaman ini terbuka waktu pasien mengetuk salah satu resep. Paling atas ada timeline status dengan empat tahap: resep diterima farmasi, obat sedang disiapkan, obat siap diambil, dan obat sudah diambil. Tahap yang sudah lewat diberi centang hijau beserta jamnya, sedangkan tahap yang sedang berjalan ditulis tebal. Di database, statusnya tetap disimpan sebagai TERKIRIM, DIPROSES, SIAP_DIAMBIL, dan SUDAH_DIAMBIL. Layar pasien cuma mengganti kode itu dengan kalimat yang lebih gampang dipahami.

Di bawah timeline ada kode QR dan kode ambil yang bentuknya seperti AMB-7K3QPX. Pasien tinggal menunjukkan QR ini ke petugas farmasi, dan kalau kamera bermasalah, petugas bisa mengetik kode ambilnya. QR dibuat langsung di aplikasi memakai library ZXing. Setelah itu ada lokasi loket farmasi beserta jam layanannya, lalu daftar obat lengkap dengan jumlah, aturan pakai, dan cara pakainya.

Setelah obat diambil, bagian QR tidak ditampilkan lagi. Gantinya muncul ringkasan informasi obat yang menjelaskan cara minum tiap obat, cara menyimpannya, dan apa yang perlu dilakukan kalau lupa minum.

## Cara kerjanya di kode

Semua layar pasien ada di file `ui/pasien/PasienScreens.kt`. Di dalamnya ada beranda (`PasienHome`), daftar resep (`TabResepSaya`), daftar notifikasi (`TabNotifikasi`), halaman detail (`DetailResepPasien`), dan timeline status (`TimelineStatus`). Datanya diambil lewat `PasienViewModel`, yang hanya memuat resep dan notifikasi milik pasien yang sedang login.

Data dari database dikirim ke layar dalam bentuk Flow. Jadi begitu petugas farmasi mengubah status resep, layar pasien ikut berubah sendiri tanpa perlu ditutup dan dibuka lagi.

Tampilannya kami sesuaikan untuk pengguna usia 30 tahun ke atas. Ukuran huruf isi 18sp dan tombol utama tingginya 56dp. Status juga tidak cuma dibedakan lewat warna, karena selalu ada teks dan ikonnya.

## Yang sudah dan belum selesai

Yang sudah jalan sekarang adalah login pasien, daftar resep aktif dan riwayat, timeline status, QR untuk mengambil obat, notifikasi dengan jumlah yang belum dibaca, info loket, dan ringkasan informasi obat.

Yang belum, data masih tersimpan di satu HP, jadi belum bisa sinkron kalau pasien dan petugas memakai HP yang berbeda. Notifikasinya juga masih notifikasi lokal dan belum dikirim dari server. Halaman profil dan fitur ganti kata sandi untuk pasien juga belum dibuat.

## Cara mencoba

Buka folder RawatJalanJKN di Android Studio lewat File > Open, tunggu Gradle Sync selesai, lalu jalankan ke emulator atau HP dengan Android 8.0 ke atas. Data contoh dibuat otomatis waktu aplikasi pertama kali dibuka.

Resep baru muncul di akun pasien setelah dokter mengirim resep. Jadi sebelum mencoba level pasien, daftarkan dulu Budi Santoso dari akun resepsionis (resepsionis / 123456), lalu kirim resep dari akun dokter (dokter1 / 123456). Kalau mau melihat resep dalam status siap diambil, proses juga resepnya dari akun farmasi (farmasi / 123456).
