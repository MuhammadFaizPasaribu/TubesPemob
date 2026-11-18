# Stok Obat Kensato

Aplikasi Android untuk mencatat obat masuk dan obat keluar di gudang Instalasi Farmasi RS Kensato. Aplikasinya dibuat dengan Kotlin dan Jetpack Compose. Datanya disimpan di HP memakai Room, jadi bisa dijalankan tanpa server. Semua data di dalamnya adalah data contoh yang fiktif.

## Cara kerjanya

Stok tidak pernah diubah langsung. Setiap perubahan selalu lewat dokumen, dan ada lima jenis dokumen: terima obat dari PBF, distribusi ke ruangan, retur ke PBF, pemusnahan, dan stok opname. Petugas membuat dokumen, lalu apoteker memeriksa dan menyetujuinya. Stok baru berubah setelah dokumen disetujui, dan perubahannya ditulis sebagai baris baru di kartu stok. Baris kartu stok tidak bisa diubah atau dihapus (dijaga sampai ke database dengan trigger), jadi kalau ada yang salah, koreksinya dibuat lewat dokumen baru dan jejaknya tetap terlihat.

Obat disimpan dalam satuan terkecilnya, misalnya tablet, kapsul, botol, atau vial. Di master obat dicatat isi kemasannya, contohnya 1 dus = 10 strip = 100 tablet. Waktu mengisi jumlah, petugas boleh memilih dus, strip, atau tablet, dan aplikasi langsung menampilkan hasilnya, misalnya "2 dus = 200 tablet". Jadi barang boleh dihitung per dus, tetapi yang tersimpan tetap jumlah tablet, sehingga tidak ada salah hitung antar satuan. Stok juga ditampilkan dengan cara yang mudah dibaca, misalnya "12 dus + 3 strip + 4 tablet".

Setiap obat dicatat per batch beserta tanggal kedaluwarsanya (ED). Saat distribusi ke ruangan, aplikasi memilih sendiri batch dengan ED paling dekat (FEFO), dan batch yang sudah kedaluwarsa tidak ikut dikeluarkan. Di beranda muncul peringatan untuk obat yang habis, stok di bawah minimum, ED kurang dari 3 atau 6 bulan, batch yang sudah kedaluwarsa, dan obat yang tidak keluar selama 3 bulan.

## Cara aplikasi mencegah kesalahan

Saat menerima obat, ED wajib diisi. Obat yang sudah kedaluwarsa ditolak, sedangkan obat dengan sisa ED kurang dari 2 tahun boleh diterima asal ada alasannya (mengacu Permenkes 72/2016). Batch yang sama harus punya ED yang sama, faktur yang sama dari PBF yang sama tidak bisa dicatat dua kali, dan barang yang kemasannya rusak tidak boleh dicatat masuk. Kalau petugas memindai barcode, kodenya harus cocok dengan obat di master.

Saat mengeluarkan obat, stok tidak bisa minus. Pengecekan dilakukan dua kali, waktu dokumen dibuat dan waktu disetujui. Stok yang sedang dipakai dokumen lain yang belum disetujui juga ikut dihitung, jadi dua petugas tidak bisa memakai stok yang sama.

Stok opname memakai cara hitung buta. Petugas menghitung barang di rak tanpa melihat angka sistem, dan angka sistem baru dibuka setelah hitungan selesai. Kalau hasilnya berbeda, petugas wajib menulis alasan. Kalau stok berubah antara waktu dihitung dan waktu disetujui, aplikasi menolak persetujuan supaya barang dihitung ulang.

Persetujuan selalu melibatkan dua orang. Hanya apoteker yang boleh menyetujui, dan pembuat dokumen tidak bisa menyetujui dokumennya sendiri. Obat high alert, obat LASA (nama atau rupa mirip, ditulis dengan huruf tall man seperti cefTRIAXone dan cefoTAXime), serta psikotropika diberi label khusus, dan dokumennya ditandai supaya diperiksa lebih teliti.

Barcode 2D GS1 pada kemasan obat (sesuai Peraturan BPOM 22/2022) bisa dipindai dengan kamera. Satu kali pindai mengisi nama obat, nomor batch, dan ED sekaligus, jadi petugas tidak perlu mengetik. PIN disimpan dalam bentuk hash, dan kalau salah 5 kali, akun dikunci 30 detik. Semua tindakan, dari masuk aplikasi sampai menyetujui dokumen, tercatat di jejak audit.

## Supaya mudah dipakai semua umur

Huruf dasarnya 18sp dan ikut membesar kalau ukuran huruf HP diperbesar. Ada juga tombol "Huruf" di beranda untuk memperbesar semua tulisan di dalam aplikasi. Tombol dibuat besar (minimal 48dp, tombol utama 56dp), warnanya berkontras tinggi, dan status selalu ditulis dengan kata, ikon, dan warna sekaligus, jadi tidak hanya mengandalkan warna. Menu di beranda tersusun satu kolom dengan keterangan singkat. Pekerjaan yang panjang dibagi menjadi tiga langkah, dan sebelum mengirim, petugas melihat kalimat konfirmasi yang jelas. Untuk masuk, pengguna cukup mengetuk namanya lalu menekan PIN 6 angka di tombol angka yang besar.

## Cara mencoba

Buka folder proyek di Android Studio lewat File > Open, tunggu Gradle Sync selesai, lalu jalankan ke emulator atau HP dengan Android 8.0 ke atas. Data contoh dibuat otomatis waktu aplikasi pertama kali dibuka.

Akun apoteker adalah apt. Maya Sari (PIN 111111) dan apt. Rudi Hartono (PIN 222222). Akun petugas adalah Dewi Lestari (PIN 333333) dan Bambang Prasetyo (PIN 444444).

Gambar contoh barcode untuk uji pindai ada di folder `contoh`. Buka gambarnya di layar laptop, lalu pindai dengan HP. Kalau memakai emulator, ketik saja kode yang tertulis di bawah tiap barcode ke kolom "Atau ketik kode barcode".

## Alur demo yang disarankan

Masuk sebagai Dewi. Di beranda terlihat Cetirizine habis, Glimepiride di bawah minimum, Captopril punya batch kedaluwarsa, Omeprazole ED-nya kurang dari 3 bulan, dan ada 2 dokumen yang menunggu verifikasi.

Buka Terima obat, pilih PBF, isi nomor faktur, lalu tambahkan obat dengan memindai contoh barcode. Paracetamol batch PCT2911 akan diterima biasa, Amoxicillin batch AMX2805 akan meminta alasan karena ED-nya kurang dari 2 tahun, dan cefTRIAXone batch CTX2604 akan ditolak karena sudah kedaluwarsa. Setelah itu kirim dokumennya.

Keluar, lalu masuk sebagai Maya. Buka Verifikasi, periksa dokumen dari Dewi, lalu setujui. Di Cek stok, buka obat yang tadi diterima, lalu lihat tab Kartu stok untuk melihat baris barunya.

Buka Keluarkan obat, pilih Distribusi ke ruangan, pilih IGD, lalu minta Paracetamol 15 strip. Aplikasi akan mengambil 100 tablet dari batch PCT2604 dulu karena ED-nya paling dekat, lalu sisanya dari batch PCT2610. Untuk pemusnahan, tombol "Tambahkan semua batch kedaluwarsa" langsung memasukkan Captopril batch CAP2301. Terakhir, coba Stok opname untuk satu obat, lalu buka Laporan untuk melihat mutasi bulan ini dan jejak audit.

## Isi kode

Kode ada di `app/src/main/java/com/kensato/stokobat`. Folder `domain` berisi aturan stok yang murni Kotlin, yaitu konversi kemasan, FEFO, cek ED, pembaca barcode GS1, dan keamanan PIN. Folder `data` berisi tabel Room, query, `Repository` (tempat semua pengecekan kesalahan), dan `DataAwal` untuk data contoh. Folder `ui` berisi layar per menu, dan `util` berisi sesi pengguna serta format tanggal dan angka.

Unit test untuk aturan stok ada di `app/src/test`. Cara menjalankannya: klik kanan folder tersebut di Android Studio, lalu pilih Run 'Tests in ...'.

## Batasan

Aplikasi ini hanya mencatat satu gudang dan datanya tersimpan di satu HP. Aplikasi belum terhubung ke SIMRS, e-katalog, atau sistem BPOM, dan surat pesanan maupun berita acara pemusnahan hanya dicatat nomornya. Dokumen fisiknya tetap dibuat di luar aplikasi.
