#  Aplikasi Mobile Rumah Sakit

Aplikasi mobile yang dirancang untuk membantu pasien dalam melakukan **pengambilan nomor kunjungan dokter** dan **pengambilan obat** tanpa harus mengantre terlalu lama secara langsung di rumah sakit.

Aplikasi ini bertujuan untuk meningkatkan kenyamanan pasien serta membantu rumah sakit dalam mengelola antrean secara lebih terstruktur dan efisien.

---

## Latar Belakang

Proses pelayanan di rumah sakit sering kali membuat pasien harus menunggu dalam antrean, baik saat ingin melakukan kunjungan dokter maupun ketika mengambil obat di bagian farmasi.

Dengan adanya aplikasi mobile ini, pasien dapat mengambil nomor antrean melalui smartphone sebelum datang atau ketika sudah berada di rumah sakit. Pasien juga dapat melihat informasi nomor antrean yang sedang berjalan sehingga dapat memperkirakan waktu pelayanan.

Aplikasi ini diharapkan dapat mengurangi penumpukan pasien di area pendaftaran, poli, dan farmasi serta membuat proses pelayanan menjadi lebih terorganisir.

---

##  Tujuan

Tujuan dari pengembangan aplikasi ini adalah:

* Mempermudah pasien dalam mengambil nomor antrean kunjungan dokter.
* Mempermudah pasien dalam melakukan antrean pengambilan obat.
* Mengurangi waktu tunggu pasien di rumah sakit.
* Memberikan informasi mengenai status dan nomor antrean secara real-time.
* Membantu rumah sakit mengelola antrean pasien dengan lebih terstruktur.
* Mengurangi penumpukan pasien pada area pelayanan.
* Meningkatkan efisiensi pelayanan rumah sakit.

---

##  Target Pengguna

Aplikasi ini memiliki beberapa jenis pengguna:

### 1. Pasien

Pasien dapat:

* Membuat akun dan login.
* Melengkapi data diri.
* Melihat daftar dokter dan poli.
* Memilih dokter atau poli yang ingin dikunjungi.
* Mengambil nomor antrean kunjungan dokter.
* Melihat nomor antrean yang sedang dilayani.
* Melihat estimasi antrean.
* Mendapatkan notifikasi ketika antrean mendekati giliran.
* Melihat riwayat kunjungan.
* Mengambil nomor antrean pengambilan obat.
* Melihat status obat yang sudah siap diambil.

### 2. Petugas Rumah Sakit

Petugas dapat:

* Melihat daftar antrean pasien.
* Memanggil nomor antrean.
* Mengubah status antrean.
* Mengelola data pasien.
* Mengelola jadwal dokter.
* Mengelola data poli.
* Mengelola antrean farmasi.
* Mengubah status obat menjadi siap diambil.

### 3. Dokter

Dokter dapat:

* Melihat daftar pasien yang sedang menunggu.
* Melihat nomor antrean pasien.
* Memanggil pasien berikutnya.
* Melihat informasi dasar pasien yang diperlukan untuk pelayanan.

---

#  Fitur Utama

## 1.  Login & Registrasi

Pasien dapat membuat akun menggunakan data yang diperlukan oleh rumah sakit.

Fitur:

* Registrasi akun.
* Login.
* Logout.
* Lupa password.
* Pengelolaan profil pasien.

---

## 2.  Pendaftaran Kunjungan Dokter

Pasien dapat memilih layanan yang ingin digunakan.

Alur:

```text
Login
  ↓
Pilih Poli
  ↓
Pilih Dokter
  ↓
Pilih Tanggal
  ↓
Ambil Nomor Antrean
  ↓
Nomor Antrean Berhasil
```

Informasi yang ditampilkan:

* Nama poli
* Nama dokter
* Tanggal kunjungan
* Jam praktik
* Nomor antrean
* Jumlah pasien yang menunggu
* Status antrean

---

## 3.  Nomor Antrean

Setelah melakukan pendaftaran, pasien mendapatkan nomor antrean.

Contoh:

```text
================================
       NOMOR ANTREAN
================================

          A-025

Poli Penyakit Dalam
Dr. Nama Dokter

Nomor Saat Ini : A-018
Antrean Anda   : A-025

Sisa Antrean   : 7 pasien

Status:
Menunggu
================================
```

Nomor antrean dapat diperbarui secara berkala berdasarkan antrean yang sedang berjalan.

---

## 4.  Notifikasi Antrean

Pasien mendapatkan notifikasi ketika nomor antreannya sudah mendekati giliran.

Contoh:

```text
🔔 Antrean Anda hampir tiba!

Nomor antrean Anda: A-025
Nomor yang sedang dilayani: A-022

Harap bersiap menuju ruang poli.
```

---

## 5.  Antrean Pengambilan Obat

Setelah dokter memberikan resep, pasien dapat melihat status resep melalui aplikasi.

Alur:

```text
Kunjungan Dokter
       ↓
    Resep Obat
       ↓
   Farmasi Menerima
       ↓
   Obat Diproses
       ↓
   Obat Siap Diambil
       ↓
Pasien Mendapat Notifikasi
       ↓
Ambil Obat
```

Status obat:

* `Resep Diterima`
* `Sedang Diproses`
* `Sedang Disiapkan`
* `Siap Diambil`
* `Sudah Diambil`

---

#  Nomor Antrean Farmasi

Pasien mendapatkan nomor antrean khusus untuk pengambilan obat.

Contoh:

```text
================================
       ANTREAN FARMASI
================================

          F-032

Status Obat:
✅ Resep diterima
✅ Obat sedang disiapkan

Nomor Saat Ini : F-028
Nomor Anda     : F-032

Sisa Antrean   : 4
================================
```

---

# Dashboard

Dashboard pasien menampilkan informasi penting seperti:

* Antrean dokter.
* Antrean farmasi.
* Jadwal kunjungan.
* Status resep.
* Notifikasi.
* Riwayat kunjungan.

Contoh tampilan:

```text
Halo, Nama Pasien 👋

┌─────────────────────────┐
│ Antrean Dokter          │
│ A-025                   │
│ Sedang dilayani: A-022  │
└─────────────────────────┘

┌─────────────────────────┐
│ Antrean Farmasi         │
│ F-032                   │
│ Status: Diproses        │
└─────────────────────────┘

[ Riwayat Kunjungan ]

[ Profil ]
```

---

#  Rencana Arsitektur Sistem

Secara umum sistem direncanakan menggunakan arsitektur:

```text
              ┌──────────────────┐
              │   Mobile App     │
              │     Pasien       │
              └────────┬─────────┘
                       │
                       ▼
              ┌──────────────────┐
              │    Backend /     │
              │       API        │
              └────────┬─────────┘
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
     ┌─────────┐  ┌─────────┐  ┌─────────┐
     │ Database│  │ Dokter  │  │ Petugas │
     └─────────┘  └─────────┘  └─────────┘
```

Mobile application berkomunikasi dengan backend melalui API. Backend bertanggung jawab untuk mengelola data pasien, dokter, jadwal, antrean, resep, dan farmasi.

---

# Rencana Database

Beberapa tabel yang direncanakan:

### Users

| Field    | Tipe    | Keterangan            |
| -------- | ------- | --------------------- |
| id       | INT     | Primary Key           |
| name     | VARCHAR | Nama pengguna         |
| email    | VARCHAR | Email                 |
| password | VARCHAR | Password              |
| role     | ENUM    | Pasien/Petugas/Dokter |

### Patients

| Field      | Tipe    | Keterangan    |
| ---------- | ------- | ------------- |
| id         | INT     | Primary Key   |
| user_id    | INT     | Relasi User   |
| nik        | VARCHAR | NIK pasien    |
| birth_date | DATE    | Tanggal lahir |
| phone      | VARCHAR | Nomor telepon |
| address    | TEXT    | Alamat        |

### Doctors

| Field          | Tipe    | Keterangan   |
| -------------- | ------- | ------------ |
| id             | INT     | Primary Key  |
| name           | VARCHAR | Nama dokter  |
| specialization | VARCHAR | Spesialisasi |
| poly_id        | INT     | Poli         |

### Queues

| Field        | Tipe    | Keterangan     |
| ------------ | ------- | -------------- |
| id           | INT     | Primary Key    |
| patient_id   | INT     | Pasien         |
| doctor_id    | INT     | Dokter         |
| queue_number | VARCHAR | Nomor antrean  |
| date         | DATE    | Tanggal        |
| status       | VARCHAR | Status antrean |

### Prescriptions

| Field      | Tipe     | Keterangan   |
| ---------- | -------- | ------------ |
| id         | INT      | Primary Key  |
| patient_id | INT      | Pasien       |
| doctor_id  | INT      | Dokter       |
| status     | VARCHAR  | Status resep |
| created_at | DATETIME | Waktu dibuat |

### Pharmacy Queues

| Field           | Tipe     | Keterangan     |
| --------------- | -------- | -------------- |
| id              | INT      | Primary Key    |
| prescription_id | INT      | Resep          |
| queue_number    | VARCHAR  | Nomor antrean  |
| status          | VARCHAR  | Status antrean |
| created_at      | DATETIME | Waktu dibuat   |

---

#  Alur Sistem

## Kunjungan Dokter

```text
Pasien Login
     ↓
Pilih Poli
     ↓
Pilih Dokter
     ↓
Pilih Jadwal
     ↓
Ambil Nomor Antrean
     ↓
Sistem Memberikan Nomor
     ↓
Pasien Menunggu
     ↓
Nomor Dipanggil
     ↓
Pasien Bertemu Dokter
```

## Pengambilan Obat

```text
Dokter Membuat Resep
        ↓
Resep Masuk ke Sistem
        ↓
Farmasi Menerima Resep
        ↓
Obat Diproses
        ↓
Obat Siap
        ↓
Pasien Mendapat Notifikasi
        ↓
Pasien Mengambil Obat
        ↓
Status Selesai
```

---

#  Teknologi yang Direncanakan

Teknologi dapat disesuaikan dengan kebutuhan proyek.

### Mobile

* Kotlin
* Jetpack Compose
* Android Studio

### Backend

* Laravel / Node.js
* REST API

### Database

* MySQL

### Authentication

* JWT / Laravel Sanctum

### Version Control

* Git
* GitHub

---

#  Struktur Repository

Contoh struktur repository:

```text
hospital-mobile-app/
│
├── mobile/
│   ├── app/
│   ├── components/
│   ├── screens/
│   ├── navigation/
│   ├── models/
│   └── services/
│
├── backend/
│   ├── app/
│   ├── routes/
│   ├── database/
│   └── tests/
│
├── docs/
│   ├── flowchart/
│   ├── erd/
│   ├── wireframe/
│   └── ui-design/
│
├── README.md
└── .gitignore
```

---

#  Tahapan Pengembangan

### Phase 1 — Analisis

* [ ] Mengidentifikasi kebutuhan pasien.
* [ ] Mengidentifikasi kebutuhan dokter.
* [ ] Mengidentifikasi kebutuhan petugas.
* [ ] Membuat use case.
* [ ] Membuat flowchart.
* [ ] Membuat ERD.

### Phase 2 — UI/UX

* [ ] Membuat wireframe.
* [ ] Membuat desain halaman login.
* [ ] Membuat desain dashboard.
* [ ] Membuat desain antrean dokter.
* [ ] Membuat desain antrean farmasi.
* [ ] Membuat desain profil.
* [ ] Membuat prototype aplikasi.

### Phase 3 — Backend

* [ ] Membuat database.
* [ ] Membuat authentication API.
* [ ] Membuat API pasien.
* [ ] Membuat API dokter.
* [ ] Membuat API antrean.
* [ ] Membuat API resep.
* [ ] Membuat API farmasi.

### Phase 4 — Mobile Development

* [ ] Membuat project Android.
* [ ] Membuat login & registrasi.
* [ ] Membuat dashboard.
* [ ] Membuat pemilihan poli.
* [ ] Membuat pemilihan dokter.
* [ ] Membuat sistem antrean.
* [ ] Membuat antrean farmasi.
* [ ] Membuat notifikasi.
* [ ] Menghubungkan aplikasi dengan API.

### Phase 5 — Testing

* [ ] Unit testing.
* [ ] API testing.
* [ ] UI testing.
* [ ] Integration testing.
* [ ] User acceptance testing.

### Phase 6 — Deployment

* [ ] Deploy backend.
* [ ] Setup database production.
* [ ] Build aplikasi Android.
* [ ] Pengujian pada perangkat nyata.
* [ ] Dokumentasi aplikasi.

---

#  Keamanan

Karena aplikasi menangani data pasien, keamanan menjadi salah satu aspek penting.

Beberapa hal yang direncanakan:

* Password disimpan menggunakan hashing.
* Authentication menggunakan token.
* Validasi input pengguna.
* Role-based access control.
* Pengamanan API.
* Pembatasan akses data berdasarkan role.
* Penggunaan HTTPS.
* Tidak menyimpan informasi sensitif secara sembarangan di perangkat.

---

#  Pengembangan Selanjutnya

Beberapa fitur yang dapat dikembangkan pada tahap berikutnya:

* Pembayaran rumah sakit melalui aplikasi.
* Konsultasi online.
* Rekam medis digital.
* Pengingat jadwal kontrol.
* Integrasi BPJS.
* Peta lokasi rumah sakit.
* Informasi ketersediaan kamar.
* Chat dengan petugas.
* Push notification.
* Integrasi dengan sistem informasi rumah sakit yang sudah ada.

---

# Status Project

**Status:** 🚧 Dalam Perencanaan / Development

Project ini masih dalam tahap perencanaan dan pengembangan awal.

---

## Catatan

Aplikasi ini merupakan rancangan sistem untuk membantu meningkatkan efisiensi proses antrean pasien di rumah sakit. Implementasi pada lingkungan rumah sakit sebenarnya memerlukan penyesuaian dengan prosedur operasional, sistem informasi rumah sakit, serta ketentuan keamanan dan privasi data yang berlaku.
