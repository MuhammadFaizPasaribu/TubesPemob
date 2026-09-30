# 🏥 Mobile Hospital Queue & Pharmacy System

Aplikasi mobile rumah sakit yang membantu pasien melakukan **pengambilan nomor antrean dokter** melalui aplikasi. Setelah pasien mendapatkan pelayanan dari dokter, dokter dapat mengirimkan **resep obat secara digital ke bagian farmasi** melalui sistem.

Pasien kemudian dapat melihat status resep dan mengambil obat setelah obat selesai diproses oleh farmasi.

---

## 📌 Latar Belakang

Proses pelayanan pasien di rumah sakit biasanya melibatkan beberapa tahapan, mulai dari mengambil nomor antrean, menunggu pemeriksaan dokter, menerima resep, hingga mengambil obat di farmasi.

Sistem ini dirancang untuk mengintegrasikan proses tersebut dalam satu aplikasi sehingga pasien tidak perlu melakukan proses antrean secara manual dari awal hingga akhir.

Dengan sistem ini, pasien dapat mengambil nomor antrean melalui aplikasi, dokter dapat melihat antrean pasien, dan resep dapat langsung dikirimkan ke farmasi melalui sistem.

---

#  Tujuan

Aplikasi ini bertujuan untuk:

* Mempermudah pasien mengambil nomor antrean dokter.
* Mengurangi antrean manual di rumah sakit.
* Membantu dokter melihat daftar pasien yang menunggu.
* Mempermudah dokter mengirim resep ke farmasi.
* Membantu farmasi menerima dan memproses resep secara digital.
* Memberikan informasi status obat kepada pasien.
* Membuat proses pelayanan pasien menjadi lebih terintegrasi.

---

# Aktor Sistem

Sistem memiliki 3 aktor utama:

###  Pasien

Pasien dapat:

* Login ke aplikasi.
* Melihat daftar poli/dokter.
* Mengambil nomor antrean.
* Melihat nomor antrean saat ini.
* Melihat status antrean.
* Mendapatkan notifikasi ketika mendekati giliran.
* Melihat resep dari dokter.
* Melihat status obat.
* Mengambil obat di farmasi.

### 👨‍⚕️ Dokter

Dokter dapat:

* Login ke aplikasi.
* Melihat daftar pasien yang sedang menunggu.
* Memanggil pasien berdasarkan nomor antrean.
* Melihat informasi pasien yang diperlukan.
* Melakukan pemeriksaan.
* Membuat resep obat.
* Mengirim resep secara digital ke farmasi.
* Melihat status resep.

### Farmasi

Petugas farmasi dapat:

* Melihat resep yang dikirim dokter.
* Melihat data obat yang diresepkan.
* Memproses resep.
* Mengubah status resep.
* Memberikan informasi bahwa obat sudah siap diambil.
* Mengubah status menjadi obat telah diambil.

---

# Alur Utama Sistem

Alur utama aplikasi:

```text
┌──────────────┐
│    PASIEN    │
└──────┬───────┘
       │
       ▼
Ambil Nomor Antrean
       │
       ▼
Menunggu Antrean
       │
       ▼
┌──────────────┐
│    DOKTER    │
└──────┬───────┘
       │
       ▼
Dokter Memanggil Pasien
       │
       ▼
Pemeriksaan Pasien
       │
       ▼
Dokter Membuat Resep
       │
       ▼
Kirim Resep ke Sistem
       │
       ▼
┌──────────────┐
│   FARMASI    │
└──────┬───────┘
       │
       ▼
Farmasi Menerima Resep
       │
       ▼
Menyiapkan Obat
       │
       ▼
Obat Siap Diambil
       │
       ▼
Pasien Mendapat Notifikasi
       │
       ▼
Pasien Mengambil Obat
```

---

# 1. Pengambilan Nomor Antrean

Pasien membuka aplikasi dan memilih dokter atau poli yang ingin dikunjungi.

### Alur:

```text
Login
  ↓
Pilih Poli
  ↓
Pilih Dokter
  ↓
Ambil Nomor Antrean
  ↓
Nomor Antrean Diperoleh
  ↓
Menunggu
```

Contoh:

```text
================================
        NOMOR ANTREAN
================================

            A-025

Poli Penyakit Dalam
Dr. Ahmad

Sedang Dilayani : A-020
Nomor Anda      : A-025

Sisa Antrean    : 5 Pasien

Status: MENUNGGU
================================
```

---

# 2. Dokter Melihat Antrean

Dokter memiliki halaman yang menampilkan pasien yang sedang menunggu.

Contoh:

```text
================================
          ANTREAN PASIEN
================================

A-023   Budi       [Panggil]
A-024   Andi       [Panggil]
A-025   Siti       [Panggil]
A-026   Rina       [Panggil]

================================
```

Dokter memanggil pasien sesuai urutan antrean.

Setelah pasien dipanggil:

```text
A-023
Status: SEDANG DIPERIKSA
```

---

# 3. Pemeriksaan Dokter

Setelah pasien masuk ke ruang pemeriksaan, dokter melakukan pemeriksaan.

Setelah pemeriksaan selesai, dokter dapat membuat resep melalui aplikasi.

Contoh:

```text
Pasien:
Siti

Keluhan:
Demam dan sakit kepala

Resep:
- Paracetamol 500 mg
- Obat X 10 tablet

[ KIRIM RESEP ]
```

---

# 4. Dokter Mengirim Resep ke Farmasi

Setelah dokter menekan tombol **Kirim Resep**, resep langsung masuk ke sistem farmasi.

```text
Dokter
   │
   │ Kirim Resep
   ▼
┌───────────────┐
│    SERVER     │
└───────┬───────┘
        │
        │ Resep Baru
        ▼
┌───────────────┐
│    FARMASI    │
└───────────────┘
```

Status resep:

```text
RESEP TERKIRIM
       ↓
SEDANG DIPROSES
       ↓
OBAT SIAP DIAMBIL
       ↓
SUDAH DIAMBIL
```

---

# 5. Farmasi Memproses Resep

Petugas farmasi melihat resep yang masuk.

Contoh:

```text
================================
          RESEP MASUK
================================

No. Resep     : RX-00125
Pasien        : Siti
Dokter        : Dr. Ahmad

Obat:
1. Paracetamol 500 mg
   Jumlah: 10

2. Obat X
   Jumlah: 10

Status:
[ PROSES RESEP ]
================================
```

Setelah obat selesai disiapkan, petugas mengubah status menjadi:

**OBAT SIAP DIAMBIL**

---

# 6. Pasien Mendapat Notifikasi

Pasien mendapatkan notifikasi melalui aplikasi.

Contoh:

```text
 Obat Anda sudah siap

Resep: RX-00125

Obat sudah selesai diproses
dan dapat diambil di Farmasi.

Silakan menuju loket farmasi.
```

---

# 7. Pengambilan Obat

Pasien datang ke bagian farmasi dan menunjukkan informasi resep atau kode pengambilan pada aplikasi.

Contoh:

```text
================================
       PENGAMBILAN OBAT
================================

Kode Resep:

          RX-00125

Pasien:
Siti

Status:
✅ SIAP DIAMBIL

[ TUNJUKKAN KODE ]
================================
```

Setelah obat diberikan kepada pasien, petugas mengubah status menjadi:

```text
SUDAH DIAMBIL
```

---

# Status Sistem

### Antrean Pasien

```text
MENUNGGU
   ↓
DIPANGGIL
   ↓
SEDANG DIPERIKSA
   ↓
SELESAI
```

### Resep

```text
RESEP DIBUAT
     ↓
TERKIRIM KE FARMASI
     ↓
DIPROSES
     ↓
SIAP DIAMBIL
     ↓
SUDAH DIAMBIL
```

---

# Rencana Database

Tabel utama yang digunakan:

```text
users
  │
  ├── patients
  │
  ├── doctors
  │
  └── pharmacists

patients
   │
   └── queues
          │
          └── consultations
                  │
                  └── prescriptions
                         │
                         └── prescription_items
```

### Tabel `users`

| Field    | Keterangan                    |
| -------- | ----------------------------- |
| id       | ID user                       |
| name     | Nama                          |
| email    | Email                         |
| password | Password                      |
| role     | patient / doctor / pharmacist |

### Tabel `queues`

| Field        | Keterangan     |
| ------------ | -------------- |
| id           | ID antrean     |
| patient_id   | ID pasien      |
| doctor_id    | ID dokter      |
| queue_number | Nomor antrean  |
| date         | Tanggal        |
| status       | Status antrean |

### Tabel `consultations`

| Field      | Keterangan        |
| ---------- | ----------------- |
| id         | ID pemeriksaan    |
| queue_id   | ID antrean        |
| patient_id | ID pasien         |
| doctor_id  | ID dokter         |
| diagnosis  | Diagnosis         |
| notes      | Catatan dokter    |
| created_at | Waktu pemeriksaan |

### Tabel `prescriptions`

| Field           | Keterangan     |
| --------------- | -------------- |
| id              | ID resep       |
| consultation_id | ID pemeriksaan |
| patient_id      | ID pasien      |
| doctor_id       | ID dokter      |
| status          | Status resep   |
| created_at      | Waktu dibuat   |

### Tabel `prescription_items`

| Field           | Keterangan |
| --------------- | ---------- |
| id              | ID         |
| prescription_id | ID resep   |
| medicine_id     | ID obat    |
| quantity        | Jumlah     |
| dosage          | Dosis      |

### Tabel `medicines`

| Field | Keterangan |
| ----- | ---------- |
| id    | ID obat    |
| name  | Nama obat  |
| stock | Stok       |
| unit  | Satuan     |

---

# 🛠️ Teknologi yang Direncanakan

### Mobile Application

* Kotlin
* Jetpack Compose
* Android Studio

### Backend

* Laravel
* REST API

### Database

* MySQL

### Authentication

* Laravel Sanctum

### Version Control

* Git & GitHub

---

# Struktur Repository

```text
hospital-app/
│
├── mobile/
│   ├── app/
│   ├── screens/
│   ├── components/
│   ├── models/
│   ├── navigation/
│   └── services/
│
├── backend/
│   ├── app/
│   ├── routes/
│   ├── database/
│   └── tests/
│
├── docs/
│   ├── use-case/
│   ├── flowchart/
│   ├── erd/
│   └── ui-ux/
│
└── README.md
```

---

#  Roadmap Pengembangan

## Phase 1 — Analisis

* [ ] Analisis kebutuhan sistem
* [ ] Identifikasi aktor
* [ ] Use Case Diagram
* [ ] Activity Diagram
* [ ] Flowchart
* [ ] ERD

## Phase 2 — UI/UX

* [ ] Wireframe
* [ ] Login
* [ ] Dashboard pasien
* [ ] Halaman antrean
* [ ] Dashboard dokter
* [ ] Halaman resep
* [ ] Dashboard farmasi
* [ ] Halaman status obat

## Phase 3 — Backend

* [ ] Database
* [ ] Authentication
* [ ] API pasien
* [ ] API dokter
* [ ] API antrean
* [ ] API konsultasi
* [ ] API resep
* [ ] API farmasi

## Phase 4 — Mobile

* [ ] Login & registrasi
* [ ] Pengambilan nomor antrean
* [ ] Monitoring antrean
* [ ] Notifikasi antrean
* [ ] Integrasi resep
* [ ] Status obat
* [ ] Kode pengambilan obat

## Phase 5 — Testing

* [ ] Unit testing
* [ ] API testing
* [ ] Integration testing
* [ ] UI testing
* [ ] User acceptance testing

---

#  Keamanan

Karena aplikasi menangani data pasien dan informasi medis, keamanan menjadi bagian penting dalam pengembangan.

Sistem direncanakan menggunakan:

* Authentication.
* Authorization berdasarkan role.
* Password hashing.
* HTTPS.
* Validasi input.
* Proteksi API.
* Pembatasan akses data pasien.
* Pengelolaan session/token secara aman.

---

#  Ringkasan Sistem

Secara sederhana, aplikasi ini memiliki konsep:

> **Pasien mengambil nomor → Dokter memanggil pasien → Pasien diperiksa → Dokter mengirim resep → Farmasi memproses resep → Pasien mendapat informasi → Pasien mengambil obat.**

Dengan konsep tersebut, proses pelayanan pasien, dokter, dan farmasi dapat terhubung dalam satu sistem.
