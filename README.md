# Aplikasi rawat jalan JKN Rumah Sakit Kensato

Repositori ini berisi aplikasi Android untuk pelayanan rawat jalan pasien JKN (BPJS Kesehatan) di Rumah Sakit Kensato. Aplikasinya dibuat dengan Kotlin dan Jetpack Compose. Datanya disimpan di database lokal di HP memakai Room, jadi aplikasi bisa dijalankan tanpa server.

Semua pengguna masuk lewat halaman login yang sama. Aplikasi mengenali peran pengguna dari akun yang dipakai, lalu langsung membuka halaman sesuai perannya. Tombol Keluar ada di kanan atas setiap halaman.

## Level user yang kami gunakan

Kami memakai empat level user. Urutannya mengikuti perjalanan pasien di rumah sakit: resepsionis mendaftarkan pasien, dokter memeriksa dan menulis resep, farmasi menyiapkan dan menyerahkan obat, lalu pasien memantau resepnya sampai obat diambil.

### Resepsionis

Resepsionis adalah petugas pendaftaran rawat jalan. Petugas mencari data pasien dengan No. RM, NIK, nomor kartu JKN, atau nama. Setelah pasien dipilih, ada enam langkah verifikasi yang harus diselesaikan. Petugas mencocokkan nama dan tanggal lahir pasien, mengecek kepesertaan JKN, memilih surat rujukan yang masih berlaku (maksimal 90 hari sejak terbit), dan memilih dokter sesuai poli tujuan rujukan beserta sisa kuotanya. Setelah itu petugas melakukan verifikasi wajah dan mencentang persetujuan umum (general consent) dari pasien.

Kalau semua langkah sudah selesai, aplikasi menerbitkan nomor SEP dan tiket antrean. Tiketnya berisi nomor antrean seperti INT-001, nama poli, dokter, lokasi ruangan, dan perkiraan jam dipanggil. Resepsionis juga bisa melihat daftar kunjungan hari ini dan papan antrean. Papan antrean bisa dibuka dalam tampilan layar penuh untuk dipasang di TV atau tablet.

### Dokter

Setiap dokter punya akun sendiri dan terhubung ke satu poli. Di halaman antrean, dokter melihat pasien yang menunggu hari itu, memanggil pasien berikutnya, dan bisa memanggil ulang kalau pasien belum datang. Pasien yang tidak butuh obat bisa langsung ditandai selesai.

Untuk pasien yang butuh obat, dokter menulis resep elektronik. Obat dipilih dari daftar obat rumah sakit (formularium) yang menampilkan stok tersedia. Untuk setiap obat, dokter mengisi dosis, jumlah, aturan pakai, dan cara pakai. Aturan pakai yang sering dipakai, misalnya 3 × 1 sehari, sudah tersedia sebagai pilihan cepat. Dokter juga bisa mencatat alergi dan berat badan pasien, dan aplikasi memberi peringatan kalau obat yang dipilih cocok dengan alergi pasien. Begitu resep dikirim ke farmasi, pemeriksaan otomatis ditandai selesai. Status resep yang sudah dikirim bisa dipantau di tab Resep hari ini.

### Farmasi

Halaman farmasi punya empat tab, yaitu Resep, Serah, Stok, dan Terima.

Di tab Resep, apoteker melihat resep yang masuk dan mengeceknya dari sisi administratif, farmasetik, dan klinis sebelum memprosesnya. Saat resep diproses, aplikasi memilih batch obat yang tanggal kedaluwarsanya paling dekat (FEFO). Apoteker kemudian melihat etiket, mengecek ulang obatnya, dan menandai resep siap diambil. Saat itu juga pasien mendapat notifikasi.

Di tab Serah, petugas memindai QR dari aplikasi pasien atau mengetik kode ambilnya. Obat diserahkan setelah nama dan tanggal lahir pasien dicocokkan dan cara minum obatnya dijelaskan. Pada tahap inilah stok obat berkurang dan tercatat sebagai pengeluaran di kartu stok.

Tab Stok berisi daftar obat beserta peringatan untuk stok yang menipis, obat yang mendekati kedaluwarsa, dan obat yang tidak keluar selama tiga bulan. Kalau satu obat dibuka, terlihat daftar batch dan kartu stoknya, dan dari situ petugas bisa melakukan stok opname. Tab Terima dipakai untuk mencatat obat yang datang dari pemasok, lengkap dengan nomor faktur, nomor batch, dan tanggal kedaluwarsa.

### Pasien

Pasien memakai aplikasi untuk menebus obat. Pasien login dengan No. RM sebagai username dan tanggal lahir (ddmmyyyy) sebagai kata sandi.

Beranda pasien punya dua tab. Tab Resep saya menampilkan resep yang masih aktif dan riwayat resep. Kartu resepnya berubah hijau kalau obat sudah siap diambil. Tab Notifikasi berisi pemberitahuan dari farmasi, dengan angka yang menunjukkan jumlah notifikasi yang belum dibaca.

Kalau resep dibuka, pasien melihat statusnya dalam empat tahap: resep diterima farmasi, obat sedang disiapkan, obat siap diambil, dan obat sudah diambil. Di bawahnya ada kode QR dan kode ambil untuk ditunjukkan ke loket farmasi, lokasi dan jam layanan loket, lalu daftar obat dengan aturan pakainya. Setelah obat diambil, muncul ringkasan informasi obat. Layar pasien ikut berubah sendiri setiap kali farmasi mengubah status resep.

Level pasien masih setengah jadi. Datanya masih tersimpan di satu HP sehingga belum bisa sinkron antarperangkat. Notifikasinya juga masih lokal dan belum dikirim dari server, dan halaman profil serta fitur ganti kata sandi belum dibuat.

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
