# E-TATIB — Sistem Informasi Pelanggaran Tata Tertib Siswa

## 1. Judul & Deskripsi

**Nama produk digital:** E-TATIB 

**Latar belakang masalah:**
Pencatatan pelanggaran tata tertib siswa di sekolah umumnya dilakukan secara manual (buku catatan atau kertas). Cara ini menimbulkan beberapa masalah:
- Sulit menghitung jumlah pelanggaran siswa per semester.
- Siswa yang sudah mencapai batas pelanggaran (5 kali per semester) terlambat diketahui sehingga pemanggilan orang tua tidak berjalan tepat waktu.
- Informasi tidak sampai secara cepat kepada Guru BK, wali kelas, siswa, dan orang tua.

**Solusi:**
E-TATIB adalah aplikasi web yang mencatat pelanggaran siswa dan otomatis memasukkan siswa ke **antrian pemanggilan Guru BK** ketika mencapai **5 kali pelanggaran dalam 1 semester**. Sistem lalu mengirim notifikasi kepada pihak terkait dan menyiapkan pesan WhatsApp untuk orang tua.

**Target pengguna:**

| Pengguna | Kegunaan |
|---|---|
| Admin | Mengelola seluruh data master dan akun |
| Tim Tatib | Menginput dan memantau pelanggaran |
| Guru BK | Memproses pemanggilan orang tua & siswa |
| Wali Kelas | Memantau siswa bimbingan |
| Siswa | Melihat riwayat pelanggaran sendiri |
| Orang Tua | Memantau pelanggaran anak |

### Fitur Utama
- Login multi-role dengan menu berbeda untuk tiap peran.
- Input pelanggaran dengan pilihan siswa dari data master (jurusan, kelas, dan No. HP orang tua terisi otomatis).
- Semester dan tahun pelajaran otomatis mengikuti tanggal (Jul–Des = Ganjil, Jan–Jun = Genap), dapat diubah manual.
- Aturan 5x pelanggaran per semester → antrian pemanggilan BK.
- Alur status pemanggilan: `Menunggu BK` → `Dipanggil` → `Selesai`.
- Kirim pesan WhatsApp ke orang tua lewat tautan `wa.me`.
- Notifikasi terpisah untuk BK, siswa, orang tua, dan wali kelas.
- CRUD jurusan, kelas, bentuk pelanggaran, siswa, serta akun Tatib/Wali Kelas/BK/Orang Tua.
- Import data siswa dari Excel dan ekspor/impor/reset data (JSON).
- Pencarian data pelanggaran dan tampilan responsif.

---

## 2. Teknologi yang Digunakan

| Kategori | Keterangan |
|---|---|
| Bahasa pemrograman | HTML5, CSS3, JavaScript (ES6+, tanpa framework) |
| Modul/pustaka | Via CDN untuk import/unduh template Excel |
| Penyimpanan data | Web Storage API (`localStorage`) |
| API browser | Notification API |
| Integrasi eksternal | WhatsApp Click-to-Chat |
| Platform publikasi | `GitHub untuk repositori untuk deploy nya menggunakan vercel]` |

---

## 3. Pemanfaatan AI (AI Usage Disclosure)

### Alat AI yang digunakan
- `ChatGPT`

### Contoh perintah (prompt) utama
`| 1 | "buatkan saya web yg didalam nya itu ada tatibnya atau bentuk pelanggaran siswa yg dimana role nya ada 4" | Diskusi awal |`
`| 2 | "buatkan saya web… role nya ada 4: 1. admin sbg pengelola 2. tim tatib memasukkan data pelanggaran 3. siswa yg dapat melihat bentuk dan seberapa dia melanggar 4. orang tua yg bisa melihat data siswa yg melanggar. Nah untuk bahasa pemrograman itu html, css, javascript, tambahkan firestore sbg penyimpan data. Ketentuannya: 1. terlambat 2. seragam tidak sesuai ketentuan 3. memakai make up tebal 4. membawa make up 5. memakai aksesoris saat sekolah 6. membawa rokok dan miras 7. pulang tidak sesuai dgn jadwal. Lalu jika siswa sudah melakukan pelanggaran sebanyak 5 kali maka akan dilakukan pemanggilan orang tua dari tim tatib dan siswa juga" |`

Daftar lengkap interaksi ada di [`AI_LOGBOOK.md`](AI_LOGBOOK.md).

### Penyesuaian/perbaikan mandiri terhadap saran AI

**| 1 |** Menyesuaikan daftar bentuk pelanggaran dengan tata tertib SMKN 2 TRENGGALEK.
**| 2 |** Menyesuaikan jurusan dan kelas dengan data sekolah.
**| 3 |** Menguji alur 5x pelanggaran dan memperbaiki kesalahan yang ditemukan.
**| 4 |** Mengganti logo dan tampilan sesuai identitas sekolah.
**| 5 |** Mengganti text yang akan dikirim ke nomor orang tua
**| 6 |** Mengganti poin pelanggaran dan menambahkan menu baru yang bisa di input oleh admin dan tatib
**| 7 |** Mengubah desain UX UI


## 4. Panduan Penggunaan

### Opsi A — Situs web aktif
Buka: `https://e-tatib-smkn2tglek.vercel.app/`

### Opsi B — Menjalankan di komputer sendiri
1. Unduh atau *clone* repositori ini.
   git clone [`https://github.com/mirzawhyuu-stack/e-tatib-smkn2tglek.git`]
   cd SMKN2TGLK_LATIKA
2. Login memakai username dan password di bawah

| Role | Username | Password |
|---|---|---|
| Admin | `admin` | `admin123` |

**admin harus mengisi data dulu, admin juga bisa menambahkan login username dan password dan bisa di atur role nya sebagai apa (guru bk/siswa/orang tua/wali kelas)**

### Alur pemakaian singkat
1. Login sebagai **Admin**: lengkapi data jurusan, kelas, wali kelas, dan siswa (bisa lewat import Excel).
2. Login sebagai **Tatib** (atau Admin): buka **Input Pelanggaran**, pilih siswa, jenis pelanggaran, dan tanggal, lalu simpan.
3. Saat siswa mencapai 5x pelanggaran dalam satu semester, ia muncul di menu **Pemanggilan BK**.
4. Login sebagai **Guru BK**: klik **💬 WA Ortu** (status menjadi *Dipanggil*), lalu klik **✅ Selesai** setelah orang tua dan siswa ditangani.
5. Siswa, orang tua, dan wali kelas melihat riwayat serta notifikasi lewat akun masing-masing.

> Fitur import Excel membutuhkan koneksi internet karena library SheetJS dimuat dari CDN.

### Format import Excel
Unduh template dari **Kelola Siswa → Unduh Format Excel**. Kolom: `Username`, `Password`, `NIS`, `Nama`, `Jurusan`, `Kelas`, `Alamat`, `Wali Kelas`, `Nama Orang Tua`, `No. HP Orang Tua`, `Username Orang Tua`, `Password Orang Tua`. Kolom wajib: Username, Password, NIS, Nama, Kelas. Kelas harus sudah ada di menu Kelola Kelas.

---

## 5. Identitas Pengembang

| Item | Keterangan |
|---|---|
| Nama lengkap | `Mirza Wahyu Sihanturi` |
| Kelas | `XI RPL B` |
| Jurusan | `Rekayasa Perangkat Lunak` |
| Asal sekolah | `Smkn 2 Trenggalek`|
| Nama lengkap | `Andhika Satria Juliano` |
| Kelas | `X RPL B` |
| Jurusan | `Rekayasa Perangkat Lunak` |
| Asal sekolah | `Smkn 2 Trenggalek`|

---

## Struktur Proyek

```
SMKN2_LATIKA/
├── index.html      # Halaman login dan seluruh halaman aplikasi
├── css/style.css   # Tampilan responsif
├── js/app.js       # Logika aplikasi (database lokal, role, fitur)
└── img/smk.jpg     # Gambar sekolah
```

## Keterbatasan
- Data tersimpan di `localStorage` browser, tidak tersinkron antar perangkat. Gunakan Ekspor JSON untuk cadangan.
- Password disimpan sebagai teks biasa dan autentikasi dilakukan di sisi klien, sehingga ini prototipe/demo, bukan sistem produksi.
- Pesan WhatsApp dikirim manual oleh pengguna (membuka `wa.me`).
- Pengembangan lanjutan: backend dan database sungguhan dengan hash password, rekap/laporan PDF, serta poin pelanggaran.
