# AI LOGBOOK — E-TATIB

Dokumentasi interaksi dengan kecerdasan artifisial (AI) dalam pengembangan **E-TATIB — Sistem Informasi Pelanggaran Tata Tertib Siswa**.

| Item | Keterangan |
|---|---|
| Pengembang | `Mirza Wahyu Sihanturi` |
| Kelas / Jurusan | `XI RPL B` |
| Sekolah | `SMKN 2 Trenggalek` |
| Pengembang | `Andika Satria Juliano` |
| Kelas / Jurusan | `X RPL B` |
| Sekolah | `SMKN 2 Trenggalek` |
| Alat AI | `ChatGPT` |
| Periode pengerjaan | `11 NOv 2026 - 16 Nov 2026` |


## Tahap 1: Eksplorasi Ide & Perancangan Solusi
*Interaksi AI dalam menentukan konsep produk.*

| No | Prompt kepada AI | Ringkasan Respons AI | Validasi & Modifikasi Mandiri |
|---|---|---|---|---|
| 1.1 | `"Saya ingin membuat aplikasi untuk mencatat pelanggaran siswa di sekolah. Apa saja fitur yang dibutuhkan?"]` | AI mengusulkan fitur pencatatan pelanggaran, daftar siswa, dan laporan. | `fitur mana yang Anda pilih/buang sesuai kebutuhan sekolah, dan alasannya]` |
| 1.2 | `"Siapa saja pengguna sistem ini dan apa hak aksesnya?"]` | AI menyusun 6 peran: Admin, Tim Tatib, Guru BK, Wali Kelas, Siswa, Orang Tua, beserta menu tiap peran. | `peran yang Anda sesuaikan setelah bertanya ke guru/tim tatib]` |
| 1.3 | `"Bagaimana alur jika siswa melanggar berkali-kali?"]` | AI merancang aturan **5 pelanggaran per semester → antrian pemanggilan Guru BK**, dengan status Menunggu BK → Dipanggil → Selesai. | `memastikan batas 5x sesuai tata tertib sekolah, bukan angka asal dari AI]` |
| 1.4 | `"Data disimpan di mana jika tidak ada server?"]` | AI menyarankan `localStorage` sehingga aplikasi bisa berjalan tanpa backend. | `memahami konsekuensinya (data hanya di satu browser) dan menambahkan ekspor/impor JSON sebagai cadangan]` |

---

## Tahap 2: Penyusunan Kerangka Kode (*Scaffolding*)
*Interaksi AI dalam merancang struktur dasar HTML/CSS dan logika fungsi.*

| No | Prompt kepada AI | Ringkasan Respons AI | Validasi & Modifikasi Mandiri |
|---|---|---|---|---|
| 2.1 | `"Buatkan struktur HTML halaman login dan dashboard dengan sidebar."]` | AI membuat `index.html` berisi halaman login dan beberapa `<section class="page">` yang ditampilkan/disembunyikan sesuai menu. | `mengubah teks, urutan menu, dan judul halaman sesuai kebutuhan]` |
| 2.3 | `"Buatkan fungsi simpan dan baca data memakai localStorage."]` | AI membuat `dbRead`/`dbWrite` dengan awalan `simtatib_` dan data awal (seed) berupa akun demo, 4 jurusan, dan 7 jenis pelanggaran. | `mengganti daftar pelanggaran sesuai tata tertib SMKN 2 Trenggalek]` |
| 2.4 | `"Buat login dengan menu berbeda tiap peran."]` | AI membuat `doLogin()`, objek `MENU` per peran, dan `buildSidebar()`. | `mencoba login dengan tiap akun demo dan memeriksa menu yang tampil]` |
| 2.5 | `"Buat fitur CRUD untuk jurusan, kelas, dan siswa."]` | AI membuat form tambah/edit/hapus dengan validasi duplikat dan konfirmasi hapus. | `menambah/mengubah validasi atau label form]` |
| 2.6 | `"Buat aturan 5x pelanggaran per semester."]` | AI membuat `semesterDariTanggal()` dan `cekBatasPanggilan()` yang menambahkan siswa ke antrian BK. | ` menguji dengan menginput 5 pelanggaran satu siswa]` |
| 2.7 | `"Buat fitur import siswa dari Excel."]` | AI membuat `unduhTemplateSiswa()` dan `prosesImportSiswa()` memakai SheetJS dengan validasi tiap baris. | `mencoba file Excel yang sengaja diberi data salah untuk melihat laporan error]` |
| 2.8 | `"Pisahkan notifikasi untuk orang tua, siswa, BK, dan wali kelas."]` | AI menambahkan penanda `untukOrtu`, `untukSiswa`, `untukBk`, `untukWk` dan fungsi `notifUntukSaya()`. | `login tiap peran untuk memastikan notifikasi hanya muncul ke penerima yang tepat]` |

---

## Tahap 3: Pemecahan Masalah & Penanganan Galat (*Debugging*)
*Interaksi AI saat memperbaiki kesalahan program.*

| No | Tanggal | Masalah / Pesan Error | Prompt kepada AI | Respons AI (ringkas) | Validasi & Modifikasi Mandiri |
|---|---|---|---|---|---|
| 3.1 | Dropdown kelas pada form siswa tidak sesuai jurusan. Saat jurusan RPL dipilih, kelas jurusan lain ikut muncul sehingga data siswa bisa salah. | "Pilihan kelas di form siswa harus menyesuaikan jurusan yang dipilih." | AI membuat kelas difilter berdasarkan jurusan lewat `isiDropdownKelasSiswa()`. Dropdown kelas nonaktif sebelum jurusan dipilih, dan `submitSiswa()` menolak data jika kelas tidak sesuai jurusan. | Menguji dengan memilih jurusan RPL dan memastikan hanya kelas RPL yang muncul, lalu mengosongkan jurusan dan memastikan dropdown kelas nonaktif. Mencoba menyimpan dengan kelas yang tidak cocok dan memastikan muncul pesan error. |
| 3.2 | Status pemanggilan sulit dipahami karena memakai dropdown, sehingga mudah salah pilih. | "Status pemanggilan jangan pakai dropdown. Buat otomatis: kalau BK klik WA jadi Dipanggil, kalau klik Selesai jadi Selesai." | AI menghapus dropdown dan menggantinya dengan tombol 💬 WA Ortu (status jadi *Dipanggil* lewat `kirimWa()`) dan ✅ Selesai (status jadi *Selesai* lewat `tandaiSelesai()`). | Login sebagai `bk1`, mengklik WA Ortu lalu Selesai, dan memastikan status berubah berurutan: Menunggu BK → Dipanggil → Selesai. |
| 3.3 | Nomor HP orang tua harus diketik ulang saat input pelanggaran, sehingga sering salah atau tidak sama dengan data orang tua. | "No HP orang tua di input pelanggaran ambil otomatis dari data siswa dan jangan bisa diedit." | AI membuat kolom `mNoHp` *readonly* dan diisi otomatis oleh `isiDataSiswaPelanggaran()` dari data orang tua (dicari lewat NIS). Jika nomor kosong, muncul peringatan agar data dilengkapi. | Memilih siswa `budi` dan memastikan nomor terisi otomatis. Memilih siswa tanpa data orang tua dan memastikan peringatan muncul. |
| 3.4 | Notifikasi untuk orang tua dan siswa tercampur, sehingga satu pihak bisa melihat pesan yang bukan untuknya. | "Notifikasi orang tua dan siswa harus dipisah, masing-masing hanya lihat miliknya." | AI menambahkan penanda `untukOrtu`, `untukSiswa`, `untukBk`, `untukWk` dan fungsi `notifUntukSaya()` yang menyaring notifikasi berdasarkan peran, NIS, dan ID pengguna. | Login bergantian sebagai `budi` dan `ortu_budi` setelah satu panggilan dikirim, lalu memastikan isi notifikasi berbeda dan sesuai penerima. |

**Penanganan galat yang sudah ada di kode** (bahan untuk dipahami dan dijelaskan):
- `window.addEventListener("error", ...)` dan `"unhandledrejection"` menampilkan toast jika terjadi error tak terduga.
- Pembacaan `localStorage` dibungkus `try/catch` agar data rusak tidak membuat aplikasi mati.
- Fungsi `esc()` menghindarkan teks pengguna dibaca sebagai HTML (mencegah injeksi/XSS).
- Validasi form memberi pesan jelas, misalnya username/NIS ganda, kelas tidak sesuai jurusan, dan data siswa belum lengkap.

---

## Tahap 4: Refleksi & Penjelasan Kode
*Verifikasi pemahaman terhadap fungsi program yang dibuat.*


### Refleksi
**Yang terbantu oleh AI:** `AI mempercepat pembuatan bagian yang berulang seperti form CRUD, validasi, dan tabel. AI juga membantu menyusun alur aturan 5x pelanggaran dan struktur kode.`
**Saran AI yang kurang tepat:** `Penyimpanan di localStorage dan password teks biasa cukup untuk demo, tetapi tidak aman untuk data sekolah sungguhan, jadi saran itu perlu dinilai sendiri.`
**Yang saya pelajari:** `Cara kerja penyimpanan di browser, perhitungan semester dari tanggal, hubungan antar data lewat NIS dan ID, serta pentingnya validasi input dan pengujian tiap peran.`
**Rencana pengembangan:** `Backend dan database, hash password, laporan PDF/Excel, dan poin pelanggaran.`


### Penjelasan kode dengan kata sendiri

**1. dbRead() dan dbWrite()**
dbRead mengambil data dari localStorage (kunci berawalan simtatib_) dan mengubah teks JSON menjadi array. Jika datanya kosong atau rusak, hasilnya array kosong sehingga aplikasi tidak error. dbWrite kebalikannya: mengubah array menjadi teks JSON lalu menyimpannya.

**2. seedIfEmpty()**
Fungsi ini jalan saat halaman dibuka. Jika data masih kosong, ia membuat akun demo (admin, tatib, BK, wali kelas, siswa, orang tua), jenis pelanggaran, jurusan, dan kelas bawaan. Data yang sudah ada tidak ditimpa.

**3. semesterDariTanggal()**
Semester ditentukan dari bulan. Bulan 7–12 jadi Ganjil dan bulan 1–6 jadi Genap. Contoh: 15 Agustus 2026 → Ganjil 2026/2027, 10 Maret 2027 → Genap 2026/2027.

**4. submitPelanggaran()**
Dijalankan saat form disimpan. Fungsi ini memeriksa siswa, data siswa (NIS, jurusan, kelas), jenis pelanggaran, tanggal, dan semester. Jika lengkap, pelanggaran disimpan lalu cekBatasPanggilan() dipanggil.

**5. cekBatasPanggilan()**
Menghitung pelanggaran siswa pada semester yang sama. Jika sudah 5 kali atau lebih dan belum ada panggilan aktif, dibuat data panggilan berstatus Menunggu BK. Notifikasi dikirim ke Guru BK dan wali kelas.

**6. kirimWa()**
Mengambil nomor HP orang tua dan membersihkannya jadi angka saja. Jika status masih Menunggu BK, status berubah menjadi Dipanggil dan notifikasi dikirim ke orang tua, siswa, dan wali kelas. Setelah itu WhatsApp dibuka lewat wa.me dengan pesan yang sudah disiapkan.

**7. tandaiSelesai()**
Mengubah status panggilan menjadi Selesai dan mencatat siapa yang mengubah serta waktunya.

**8. notifUntukSaya()**
Menyaring notifikasi sesuai peran yang login. Siswa hanya melihat notifikasi untuk dirinya (cocok NIS), orang tua untuk anaknya, BK untuk BK, dan wali kelas untuk dirinya sendiri.

**9. prosesImportSiswa()**
Membaca tiap baris Excel. Setiap baris diperiksa kolom wajibnya, username dan NIS ganda, serta kecocokan kelas dan jurusan. Baris yang valid disimpan, baris yang gagal dicatat beserta nomor barisnya.




