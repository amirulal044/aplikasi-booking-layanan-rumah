
# Dokumen Spesifikasi Kebutuhan Perangkat Lunak (SRS)
## Aplikasi Mobile SaaS: Servisku (MVP)


* Nama  : Amirul Af Arif
* NIM   : 221240001249
* Kelas : C

## Daftar Isi

1.  [Pendahuluan](#1-pendahuluan)
    1.1. [Tujuan Dokumen](#11-tujuan-dokumen)
    1.2. [Ruang Lingkup Produk](#12-ruang-lingkup-produk)
    1.3. [Audiens Sasaran Dokumen](#13-audiens-sasaran-dokumen)
    1.4. [Definisi, Akronim, dan Singkatan](#14-definisi-akronim-dan-singkatan)
    1.5. [Referensi](#15-referensi)
2.  [Deskripsi Umum](#2-deskripsi-umum)
    2.1. [Perspektif Produk](#21-perspektif-produk)
    2.2. [Fungsi Produk](#22-fungsi-produk)
    2.3. [Karakteristik Pengguna](#23-karakteristik-pengguna)
    2.4. [Batasan Umum](#24-batasan-umum)
    2.5. [Asumsi dan Dependensi](#25-asumsi-dan-dependensi)
3.  [Persyaratan Fungsional (What the system will do)](#3-persyaratan-fungsional-what-the-system-will-do)
    3.1. [Modul Autentikasi](#31-modul-autentikasi)
    3.2. [Modul Pelanggan](#32-modul-pelanggan)
    3.3. [Modul Penyedia Layanan](#33-modul-penyedia-layanan)
    3.4. [Modul Admin (Backend Sederhana/Appwrite Console)](#34-modul-admin-backend-sederhanappwrite-console)
    3.5. [Modul Notifikasi](#35-modul-notifikasi)
4.  [Persyaratan Non-Fungsional (How well the system performs)](#4-persyaratan-non-fungsional-how-well-the-system-performs)
    4.1. [Performa](#41-performa)
    4.2. [Keamanan](#42-keamanan)
    4.3. [Usability (Kegunaan)](#43-usability-kegunaan)
    4.4. [Reliabilitas (Keandalan)](#44-reliabilitas-keandalan)
    4.5. [Maintainability (Kemudahan Pemeliharaan)](#45-maintainability-kemudahan-pemeliharaan)
    4.6. [Portabilitas](#46-portabilitas)
    4.7. [Persyaratan Lingkungan](#47-persyaratan-lingkungan)
5.  [Persyaratan Antarmuka Eksternal](#5-persyaratan-antarmuka-eksternal)
    5.1. [Antarmuka Pengguna (UI)](#51-antarmuka-pengguna-ui)
    5.2. [Antarmuka Perangkat Lunak](#52-antarmuka-perangkat-lunak)
6.  [Model Data (Skema Appwrite Database)](#6-model-data-skema-appwrite-database)
    6.1. [Koleksi `users`](#61-koleksi-users)
    6.2. [Koleksi `bookings`](#62-koleksi-bookings)
    6.3. [Koleksi `services_categories` (Opsional untuk MVP, bisa disederhanakan)](#63-koleksi-services_categories-opsional-untuk-mvp-bisa-disederhanakan)
7.  [Diagram Alur (Flowcharts)](#7-diagram-alur-flowcharts)
    7.1. [Alur Pelanggan](#71-alur-pelanggan)
    7.2. [Alur Penyedia Layanan](#72-alur-penyedia-layanan)
    7.3. [Alur Verifikasi Admin (Konseptual)](#73-alur-verifikasi-admin-konseptual)
8.  [Metrik Kesuksesan MVP](#8-metrik-kesuksesan-mvp)
9.  [Rencana Iterasi Setelah MVP](#9-rencana-iterasi-setelah-mvp)
10. [Glossarium/Indeks](#10-glossariumindeks)

---

## 1. Pendahuluan

### 1.1 Tujuan Dokumen
Dokumen ini bertujuan untuk menjelaskan persyaratan perangkat lunak untuk pengembangan aplikasi mobile **"Servisku" (MVP)** menggunakan Flutter sebagai frontend dan Appwrite (versi gratis) sebagai backend. Ini akan menjadi panduan utama bagi tim pengembangan, desainer, penguji, dan pemangku kepentingan lainnya.

### 1.2 Ruang Lingkup Produk
Aplikasi "Servisku" (MVP) adalah platform mobile yang menghubungkan pemilik rumah tangga (Pelanggan) dengan penyedia layanan rumah tangga (Penyedia Layanan/Teknisi). Fokus MVP adalah fungsionalitas inti pencarian, pemesanan, dan manajemen status pemesanan dasar.

**Fitur Utama MVP:**
*   Pendaftaran dan login untuk Pelanggan dan Penyedia Layanan.
*   Pelanggan dapat mencari Penyedia Layanan berdasarkan jenis layanan.
*   Pelanggan dapat melihat profil dasar Penyedia Layanan.
*   Pelanggan dapat membuat permintaan pemesanan dengan detail masalah, alamat, serta preferensi tanggal dan waktu sederhana.
*   Penyedia Layanan dapat mengelola status ketersediaan sederhana.
*   Penyedia Layanan dapat menerima atau menolak permintaan pemesanan.
*   Penyedia Layanan dapat memperbarui status pekerjaan menjadi selesai.
*   Pelanggan dan Penyedia Layanan dapat melihat riwayat dan status pemesanan.
*   Notifikasi dasar in-app untuk pembaruan status pemesanan.
*   Admin dapat memverifikasi Penyedia Layanan dan memantau pemesanan melalui Appwrite Console atau antarmuka admin sederhana.

**Fitur yang TIDAK termasuk dalam MVP:**
*   Integrasi pembayaran dalam aplikasi.
*   Fitur chat real-time antara Pelanggan dan Penyedia Layanan.
*   Sistem rating dan ulasan detail.
*   Pelacakan lokasi Penyedia Layanan secara real-time.
*   Filter pencarian lanjutan (harga, jarak, rating).
*   Manajemen jadwal Penyedia Layanan yang kompleks dengan kalender.

### 1.3 Audiens Sasaran Dokumen
*   Pengembang Flutter
*   Desainer UI/UX
*   Penguji Kualitas (QA)
*   Manajer Proyek
*   Pemangku Kepentingan Bisnis

### 1.4 Definisi, Akronim, dan Singkatan
*   **MVP**: Minimum Viable Product
*   **SRS**: Software Requirements Specification
*   **UI**: User Interface
*   **UX**: User Experience
*   **API**: Application Programming Interface
*   **SaaS**: Software as a Service
*   **Appwrite**: Backend-as-a-Service platform yang digunakan.
*   **Flutter**: Framework Pengembangan UI cross-platform.
*   **ID**: Identifikasi unik.
*   **Pelanggan**: Pengguna yang mencari dan memesan layanan rumah tangga.
*   **Penyedia Layanan**: Teknisi atau penyedia jasa yang menawarkan layanan rumah tangga.
*   **Admin**: Pengelola platform aplikasi.
*   **FR**: Functional Requirement (Persyaratan Fungsional).
*   **NFR**: Non-Functional Requirement (Persyaratan Non-Fungsional).

### 1.5 Referensi
*   Dokumen Konsep Awal Aplikasi "Servisku".
*   Dokumentasi Appwrite ([https://appwrite.io/docs](https://appwrite.io/docs))
*   Dokumentasi Flutter ([https://flutter.dev/docs](https://flutter.dev/docs))

---

## 2. Deskripsi Umum

### 2.1 Perspektif Produk
Servisku adalah aplikasi mobile standalone yang dibangun menggunakan Flutter untuk frontend. Aplikasi ini akan sangat bergantung pada Appwrite (versi gratis, baik self-hosted atau Cloud) sebagai backend untuk autentikasi, database, dan fungsi notifikasi dasar. Semua interaksi data antara aplikasi mobile dan backend akan melalui Appwrite API.

### 2.2 Fungsi Produk
Aplikasi "Servisku" dirancang untuk menyelesaikan masalah kesulitan menemukan penyedia layanan rumah tangga yang terpercaya, tersedia, dan berkualitas dengan cepat.

**Fungsi Utama:**
*   **Pelanggan:** Dapat mendaftar, login, mencari layanan berdasarkan kategori, melihat profil penyedia, membuat pemesanan, melacak status pemesanan, dan menerima notifikasi.
*   **Penyedia Layanan:** Dapat mendaftar (dengan proses verifikasi oleh Admin), login, mengatur ketersediaan dasar, menerima/menolak pemesanan, memperbarui status pekerjaan, dan menerima notifikasi.
*   **Admin:** Dapat memverifikasi pendaftaran Penyedia Layanan baru dan memantau aktivitas pemesanan melalui Appwrite Console atau antarmuka admin yang sangat sederhana.

### 2.3 Karakteristik Pengguna

*   **Pelanggan:**
    *   Pemilik rumah tangga muda (25-45 tahun) di perkotaan.
    *   Sibuk dan melek teknologi.
    *   Mencari kemudahan dan efisiensi dalam mengatasi masalah rumah tangga.
    *   Familiar dengan penggunaan aplikasi mobile untuk berbagai kebutuhan.
*   **Penyedia Layanan (Teknisi/Jasa Kebersihan):**
    *   Individu atau usaha kecil yang sudah memiliki basis pelanggan atau baru memulai.
    *   Ingin memperluas jangkauan pasar dan mendapatkan lebih banyak pekerjaan.
    *   Membutuhkan cara yang lebih modern dan terorganisir untuk mengelola pesanan.
    *   Tingkat keakraban dengan teknologi bervariasi, sehingga antarmuka harus intuitif.
*   **Admin:**
    *   Staf operasional atau teknis dari tim "Servisku".
    *   Bertanggung jawab untuk menjaga kualitas platform dengan memverifikasi Penyedia Layanan.
    *   Membutuhkan akses untuk memantau transaksi dan pengguna.

### 2.4 Batasan Umum
*   Pengembangan aplikasi mobile harus menggunakan Flutter SDK versi stabil terbaru.
*   Backend harus menggunakan Appwrite versi gratis (self-hosted atau Cloud dengan batasan yang berlaku).
*   Tidak ada integrasi payment gateway di fase MVP ini. Pembayaran diasumsikan dilakukan secara langsung antara Pelanggan dan Penyedia Layanan di luar aplikasi.
*   Tidak ada fitur chat real-time di fase MVP. Komunikasi lanjutan (jika diperlukan) dilakukan di luar aplikasi.
*   Fitur ulasan/rating tidak tersedia di fase MVP.
*   Pencarian layanan tidak menyertakan filter lokasi geografis yang kompleks (misalnya, berdasarkan GPS atau radius). Pelanggan dapat melihat area layanan yang dicantumkan oleh Penyedia.
*   Manajemen ketersediaan Penyedia Layanan bersifat sederhana (tersedia/tidak tersedia), bukan kalender detail.

### 2.5 Asumsi dan Dependensi
*   Pengguna memiliki koneksi internet yang stabil untuk menggunakan aplikasi.
*   Layanan Appwrite (server) berjalan stabil dan dapat diakses oleh aplikasi klien.
*   Pengguna dapat mengunduh dan menginstal aplikasi dari toko aplikasi (Google Play Store/Apple App Store) setelah dirilis.
*   Pembatasan Appwrite versi gratis (jumlah dokumen, eksekusi fungsi, dll.) akan dipatuhi.

---

## 3. Persyaratan Fungsional (What the system will do)

### 3.1 Modul Autentikasi

**FR-AUTH-001: Pendaftaran Akun Pelanggan**
*   **Deskripsi:** Pengguna baru dapat mendaftar sebagai Pelanggan menggunakan alamat email dan password.
*   **Aktor:** Pengguna Tidak Terdaftar.
*   **Pemicu:** Pengguna memilih opsi "Daftar sebagai Pelanggan".
*   **Alur Utama:**
    1.  Pengguna membuka aplikasi dan memilih opsi "Daftar".
    2.  Pengguna memilih peran "Pelanggan".
    3.  Pengguna mengisi form pendaftaran (Nama Lengkap, Email, Password, Konfirmasi Password).
    4.  Pengguna menyetujui Syarat & Ketentuan.
    5.  Pengguna menekan tombol "Daftar".
    6.  Sistem memvalidasi input (format email valid, password memenuhi kriteria minimal, password cocok).
    7.  Jika valid, sistem membuat akun baru di Appwrite Authentication.
    8.  Sistem membuat dokumen profil pengguna di koleksi `users` Appwrite Database dengan `role: "customer"`.
    9.  Sistem mengarahkan pengguna ke halaman utama Pelanggan (sudah login).
*   **Alur Alternatif:**
    *   Email sudah terdaftar: Sistem menampilkan pesan kesalahan.
    *   Password tidak memenuhi kriteria: Sistem menampilkan pesan kesalahan.
*   **Integrasi Appwrite:** `Appwrite.account.create()`, `Appwrite.database.createDocument()`.

**FR-AUTH-002: Pendaftaran Akun Penyedia Layanan**
*   **Deskripsi:** Calon Penyedia Layanan dapat mendaftar akun menggunakan email dan password, serta mengisi detail profil awal untuk verifikasi.
*   **Aktor:** Pengguna Tidak Terdaftar.
*   **Pemicu:** Pengguna memilih opsi "Daftar sebagai Penyedia Layanan".
*   **Alur Utama:**
    1.  Pengguna membuka aplikasi dan memilih opsi "Daftar".
    2.  Pengguna memilih peran "Penyedia Layanan".
    3.  Pengguna mengisi form pendaftaran (Nama Lengkap/Nama Usaha, Email, Password, Konfirmasi Password, Nomor Telepon, Jenis Layanan Utama yang ditawarkan (pilihan dari daftar atau input teks), Deskripsi Keahlian Singkat, Area Jangkauan Layanan (input teks, misal "Jakarta Selatan, Depok")).
    4.  Pengguna menyetujui Syarat & Ketentuan.
    5.  Pengguna menekan tombol "Daftar".
    6.  Sistem memvalidasi input.
    7.  Jika valid, sistem membuat akun baru di Appwrite Authentication.
    8.  Sistem membuat dokumen profil pengguna di koleksi `users` Appwrite Database dengan `role: "provider"`, `is_verified: false`, dan detail lainnya.
    9.  Sistem menampilkan pesan bahwa pendaftaran berhasil dan akun akan diverifikasi oleh Admin. Pengguna diarahkan ke halaman tunggu atau halaman utama Penyedia dengan fungsionalitas terbatas hingga diverifikasi.
*   **Integrasi Appwrite:** `Appwrite.account.create()`, `Appwrite.database.createDocument()`.

**FR-AUTH-003: Login Pengguna (Pelanggan & Penyedia Layanan)**
*   **Deskripsi:** Pengguna terdaftar (Pelanggan atau Penyedia Layanan) dapat login ke akun mereka menggunakan email dan password.
*   **Aktor:** Pengguna Tidak Terdaftar/Terdaftar.
*   **Pemicu:** Pengguna memilih opsi "Login".
*   **Alur Utama:**
    1.  Pengguna mengisi form login (Email, Password).
    2.  Pengguna menekan tombol "Login".
    3.  Sistem memvalidasi kredensial dengan Appwrite Authentication.
    4.  Jika kredensial valid, sistem membuat sesi login.
    5.  Sistem mengarahkan pengguna ke halaman utama sesuai dengan peran mereka (`role` dari data pengguna).
*   **Alur Alternatif:**
    *   Kredensial tidak valid: Sistem menampilkan pesan kesalahan "Email atau password salah".
*   **Integrasi Appwrite:** `Appwrite.account.createEmailSession()`.

**FR-AUTH-004: Logout Pengguna**
*   **Deskripsi:** Pengguna yang sudah login dapat keluar dari sesi akun mereka.
*   **Aktor:** Pengguna Terdaftar (Pelanggan/Penyedia Layanan).
*   **Pemicu:** Pengguna memilih opsi "Logout" dari menu profil atau pengaturan.
*   **Alur Utama:**
    1.  Pengguna menekan tombol "Logout".
    2.  Sistem menghapus sesi login saat ini di Appwrite.
    3.  Sistem mengarahkan pengguna kembali ke halaman login atau halaman awal aplikasi.
*   **Integrasi Appwrite:** `Appwrite.account.deleteSession('current')` atau `Appwrite.account.deleteSessions()`.

**FR-AUTH-005: Lupa Password (Opsional untuk MVP Awal, tapi sangat direkomendasikan)**
*   **Deskripsi:** Pengguna dapat meminta reset password jika lupa.
*   **Aktor:** Pengguna Tidak Terdaftar/Terdaftar.
*   **Pemicu:** Pengguna memilih opsi "Lupa Password" di halaman login.
*   **Alur Utama:**
    1.  Pengguna memasukkan alamat email terdaftar.
    2.  Sistem mengirimkan email berisi link atau kode untuk reset password (via Appwrite).
    3.  Pengguna mengikuti instruksi di email untuk membuat password baru.
*   **Integrasi Appwrite:** `Appwrite.account.createRecovery()`.

### 3.2 Modul Pelanggan

**FR-CUST-001: Pencarian Layanan Berdasarkan Kategori**
*   **Deskripsi:** Pelanggan dapat mencari Penyedia Layanan berdasarkan kategori layanan yang telah ditentukan.
*   **Aktor:** Pelanggan Terdaftar.
*   **Pemicu:** Pelanggan berada di halaman utama dan memilih kategori layanan.
*   **Alur Utama:**
    1.  Pelanggan melihat daftar kategori layanan yang tersedia (misal: "Teknisi AC", "Tukang Ledeng", "Jasa Kebersihan").
    2.  Pelanggan memilih salah satu kategori layanan.
    3.  Sistem mengambil dan menampilkan daftar Penyedia Layanan yang menawarkan layanan tersebut, `is_verified: true`, dan `is_available: true`. Informasi yang ditampilkan per penyedia: Nama, Jenis Layanan Utama, Area Jangkauan (teks).
*   **Integrasi Appwrite:** `Appwrite.database.listDocuments()` pada koleksi `users` dengan filter `role: "provider"`, `service_type: [kategori_dipilih]`, `is_verified: true`, `is_available: true`.

**FR-CUST-002: Melihat Detail Profil Penyedia Layanan**
*   **Deskripsi:** Pelanggan dapat melihat halaman detail profil Penyedia Layanan yang dipilih.
*   **Aktor:** Pelanggan Terdaftar.
*   **Pemicu:** Pelanggan memilih salah satu Penyedia Layanan dari hasil pencarian.
*   **Alur Utama:**
    1.  Sistem menampilkan halaman detail Penyedia Layanan yang berisi: Nama Lengkap/Nama Usaha, Foto Profil (jika ada), Jenis Layanan Utama, Deskripsi Keahlian Singkat, Area Jangkauan Layanan.
    2.  Terdapat tombol "Pesan Sekarang".
*   **Integrasi Appwrite:** `Appwrite.database.getDocument()` dari koleksi `users` berdasarkan `userId` Penyedia.

**FR-CUST-003: Membuat Pemesanan Layanan**
*   **Deskripsi:** Pelanggan dapat membuat permintaan pemesanan layanan kepada Penyedia Layanan yang dipilih.
*   **Aktor:** Pelanggan Terdaftar.
*   **Pemicu:** Pelanggan menekan tombol "Pesan Sekarang" di halaman detail Penyedia Layanan.
*   **Alur Utama:**
    1.  Sistem menampilkan form pemesanan.
    2.  Pelanggan memilih/mengkonfirmasi jenis layanan (jika Penyedia menawarkan >1 dan belum dipilih).
    3.  Pelanggan memilih tanggal yang diinginkan dari kalender sederhana.
    4.  Pelanggan memilih slot waktu yang diinginkan (misalnya, "Pagi (08:00-12:00)", "Siang (13:00-17:00)", "Sore (18:00-21:00)").
    5.  Pelanggan mengisi deskripsi masalah/kebutuhan layanan (input teks).
    6.  Pelanggan mengisi atau mengkonfirmasi alamat lengkap layanan (input teks, bisa pre-fill dari profil Pelanggan).
    7.  Pelanggan menekan tombol "Konfirmasi Pemesanan".
    8.  Sistem memvalidasi input.
    9.  Jika valid, sistem membuat dokumen baru di koleksi `bookings` dengan `status: "pending_confirmation"`, `customerId`, `providerId`, dan detail pesanan lainnya.
    10. Sistem mengirimkan notifikasi (in-app) kepada Penyedia Layanan terkait.
    11. Sistem menampilkan pesan konfirmasi kepada Pelanggan dan mengarahkan ke halaman riwayat pemesanan.
*   **Integrasi Appwrite:** `Appwrite.database.createDocument()` ke koleksi `bookings`.

**FR-CUST-004: Melihat Riwayat dan Status Pemesanan**
*   **Deskripsi:** Pelanggan dapat melihat daftar semua pemesanan yang telah mereka buat beserta statusnya.
*   **Aktor:** Pelanggan Terdaftar.
*   **Pemicu:** Pelanggan mengakses menu "Riwayat Pemesanan" atau sejenisnya.
*   **Alur Utama:**
    1.  Sistem mengambil dan menampilkan daftar pemesanan milik Pelanggan tersebut, diurutkan berdasarkan tanggal terbaru.
    2.  Informasi yang ditampilkan per pemesanan: Nama Penyedia Layanan, Jenis Layanan, Tanggal Pemesanan, Status Pemesanan ("Menunggu Konfirmasi", "Dikonfirmasi", "Ditolak", "Selesai", "Dibatalkan").
*   **Integrasi Appwrite:** `Appwrite.database.listDocuments()` dari koleksi `bookings` dengan filter `customerId: [ID_Pelanggan_Saat_Ini]`.

**FR-CUST-005: Membatalkan Pemesanan (Opsional untuk MVP, tapi berguna)**
*   **Deskripsi:** Pelanggan dapat membatalkan pemesanan yang belum dikonfirmasi oleh Penyedia Layanan.
*   **Aktor:** Pelanggan Terdaftar.
*   **Pemicu:** Pelanggan memilih opsi "Batalkan" pada pemesanan dengan status "Menunggu Konfirmasi".
*   **Alur Utama:**
    1.  Sistem meminta konfirmasi pembatalan.
    2.  Jika dikonfirmasi, sistem memperbarui status pemesanan di koleksi `bookings` menjadi `"cancelled_by_customer"`.
    3.  Sistem mengirim notifikasi (in-app) kepada Penyedia Layanan terkait.
*   **Integrasi Appwrite:** `Appwrite.database.updateDocument()`.

### 3.3 Modul Penyedia Layanan

**FR-PROV-001: Mengelola Profil Penyedia Layanan**
*   **Deskripsi:** Penyedia Layanan dapat mengedit informasi profil mereka.
*   **Aktor:** Penyedia Layanan Terdaftar dan Terverifikasi.
*   **Pemicu:** Penyedia mengakses menu "Profil Saya".
*   **Alur Utama:**
    1.  Sistem menampilkan form edit profil yang berisi: Nama Lengkap/Nama Usaha, Nomor Telepon, Foto Profil (opsional), Deskripsi Keahlian, Area Jangkauan Layanan.
    2.  Penyedia mengubah data yang diinginkan dan menyimpan.
    3.  Sistem memperbarui dokumen profil di koleksi `users` Appwrite Database.
*   **Integrasi Appwrite:** `Appwrite.database.updateDocument()`.

**FR-PROV-002: Mengelola Status Ketersediaan Sederhana**
*   **Deskripsi:** Penyedia Layanan dapat mengatur status ketersediaan mereka untuk menerima pesanan baru.
*   **Aktor:** Penyedia Layanan Terdaftar dan Terverifikasi.
*   **Pemicu:** Penyedia mengakses halaman utama atau pengaturan ketersediaan.
*   **Alur Utama:**
    1.  Sistem menampilkan toggle atau tombol untuk status "Tersedia Menerima Pesanan" (Aktif/Nonaktif).
    2.  Penyedia mengubah status.
    3.  Sistem memperbarui atribut `is_available` (boolean) pada dokumen profil Penyedia di koleksi `users`. Penyedia yang `is_available: false` tidak akan muncul di hasil pencarian pelanggan.
*   **Integrasi Appwrite:** `Appwrite.database.updateDocument()`.

**FR-PROV-003: Melihat Daftar Permintaan Pemesanan Masuk**
*   **Deskripsi:** Penyedia Layanan dapat melihat daftar permintaan pemesanan baru yang ditujukan kepada mereka.
*   **Aktor:** Penyedia Layanan Terdaftar dan Terverifikasi.
*   **Pemicu:** Penyedia mengakses menu "Pemesanan Masuk" atau notifikasi pemesanan baru.
*   **Alur Utama:**
    1.  Sistem mengambil dan menampilkan daftar pemesanan dengan `status: "pending_confirmation"` yang `providerId`-nya sesuai dengan ID Penyedia saat ini.
    2.  Informasi yang ditampilkan per pemesanan: Nama Pelanggan, Jenis Layanan, Tanggal & Waktu yang Diajukan, Alamat Layanan, Deskripsi Masalah.
*   **Integrasi Appwrite:** `Appwrite.database.listDocuments()` dari koleksi `bookings` dengan filter `providerId: [ID_Penyedia_Saat_Ini]` dan `status: "pending_confirmation"`.

**FR-PROV-004: Mengelola Permintaan Pemesanan (Terima/Tolak)**
*   **Deskripsi:** Penyedia Layanan dapat menerima atau menolak permintaan pemesanan yang masuk.
*   **Aktor:** Penyedia Layanan Terdaftar dan Terverifikasi.
*   **Pemicu:** Penyedia memilih salah satu permintaan pemesanan dari daftar.
*   **Alur Utama (Terima):**
    1.  Penyedia memilih opsi "Terima Pemesanan".
    2.  Sistem meminta konfirmasi.
    3.  Jika dikonfirmasi, sistem memperbarui status pemesanan di koleksi `bookings` menjadi `"confirmed_by_provider"`.
    4.  Sistem mengirimkan notifikasi (in-app) kepada Pelanggan terkait.
*   **Alur Utama (Tolak):**
    1.  Penyedia memilih opsi "Tolak Pemesanan".
    2.  Sistem meminta konfirmasi dan (opsional) alasan penolakan singkat.
    3.  Jika dikonfirmasi, sistem memperbarui status pemesanan di koleksi `bookings` menjadi `"rejected_by_provider"` (dan menyimpan alasan jika ada).
    4.  Sistem mengirimkan notifikasi (in-app) kepada Pelanggan terkait.
*   **Integrasi Appwrite:** `Appwrite.database.updateDocument()`.

**FR-PROV-005: Memperbarui Status Pekerjaan menjadi Selesai**
*   **Deskripsi:** Penyedia Layanan dapat menandai pemesanan sebagai selesai setelah pekerjaan diselesaikan.
*   **Aktor:** Penyedia Layanan Terdaftar dan Terverifikasi.
*   **Pemicu:** Penyedia memilih pemesanan yang sedang berjalan atau sudah dikonfirmasi.
*   **Alur Utama:**
    1.  Penyedia memilih opsi "Tandai Selesai" pada pemesanan yang relevan.
    2.  Sistem meminta konfirmasi.
    3.  Jika dikonfirmasi, sistem memperbarui status pemesanan di koleksi `bookings` menjadi `"completed"`.
    4.  Sistem mengirimkan notifikasi (in-app) kepada Pelanggan terkait.
*   **Integrasi Appwrite:** `Appwrite.database.updateDocument()`.

**FR-PROV-006: Melihat Riwayat Pekerjaan**
*   **Deskripsi:** Penyedia Layanan dapat melihat daftar semua pekerjaan yang telah mereka terima/selesaikan/tolak.
*   **Aktor:** Penyedia Layanan Terdaftar dan Terverifikasi.
*   **Pemicu:** Penyedia mengakses menu "Riwayat Pekerjaan".
*   **Alur Utama:**
    1.  Sistem mengambil dan menampilkan daftar pemesanan yang `providerId`-nya sesuai, diurutkan berdasarkan tanggal terbaru.
    2.  Informasi yang ditampilkan per pemesanan: Nama Pelanggan, Jenis Layanan, Tanggal Pemesanan, Status Pemesanan.
*   **Integrasi Appwrite:** `Appwrite.database.listDocuments()` dari koleksi `bookings` dengan filter `providerId: [ID_Penyedia_Saat_Ini]`.

### 3.4 Modul Admin (Backend Sederhana/Appwrite Console)

**FR-ADMIN-001: Verifikasi Akun Penyedia Layanan Baru**
*   **Deskripsi:** Admin dapat meninjau dan memverifikasi pendaftaran Penyedia Layanan baru.
*   **Aktor:** Admin.
*   **Pemicu:** Admin mengakses daftar Penyedia Layanan yang belum diverifikasi.
*   **Alur Utama (via Appwrite Console atau UI Admin Sederhana):**
    1.  Admin melihat daftar pengguna dengan `role: "provider"` dan `is_verified: false`.
    2.  Admin meninjau detail profil Penyedia Layanan (kontak, jenis layanan, area).
    3.  Admin dapat menghubungi Penyedia Layanan di luar sistem jika diperlukan klarifikasi.
    4.  Admin memperbarui atribut `is_verified` menjadi `true` untuk Penyedia Layanan yang disetujui. Jika ditolak, Admin bisa menghapus akun atau menandainya sebagai `rejected` (membutuhkan atribut status tambahan).
    5.  (Opsional) Sistem mengirim notifikasi (email atau in-app jika ada UI Admin) kepada Penyedia Layanan tentang status verifikasi.
*   **Integrasi Appwrite:** `Appwrite.database.updateDocument()` atau modifikasi langsung via Appwrite Console.

**FR-ADMIN-002: Melihat Daftar Pengguna (Pelanggan & Penyedia Layanan)**
*   **Deskripsi:** Admin dapat melihat daftar semua pengguna yang terdaftar di platform.
*   **Aktor:** Admin.
*   **Pemicu:** Admin mengakses fitur manajemen pengguna.
*   **Alur Utama (via Appwrite Console atau UI Admin Sederhana):**
    1.  Sistem menampilkan daftar pengguna dari koleksi `users` beserta detail dasarnya.
    2.  Admin dapat melakukan filter berdasarkan peran.
*   **Integrasi Appwrite:** Akses langsung ke koleksi `users` via Appwrite Console atau `Appwrite.database.listDocuments()`.

**FR-ADMIN-003: Melihat Semua Pemesanan**
*   **Deskripsi:** Admin dapat melihat semua transaksi pemesanan yang terjadi di platform.
*   **Aktor:** Admin.
*   **Pemicu:** Admin mengakses fitur manajemen pemesanan.
*   **Alur Utama (via Appwrite Console atau UI Admin Sederhana):**
    1.  Sistem menampilkan daftar semua pemesanan dari koleksi `bookings` beserta detailnya.
    2.  Admin dapat melakukan filter berdasarkan status, tanggal, dll.
*   **Integrasi Appwrite:** Akses langsung ke koleksi `bookings` via Appwrite Console atau `Appwrite.database.listDocuments()`.

**FR-ADMIN-004: Mengelola Kategori Layanan (Opsional untuk MVP, bisa hardcode dulu)**
*   **Deskripsi:** Admin dapat menambah, mengedit, atau menonaktifkan kategori layanan yang tersedia di platform.
*   **Aktor:** Admin.
*   **Pemicu:** Admin mengakses fitur manajemen kategori layanan.
*   **Alur Utama (via Appwrite Console atau UI Admin Sederhana):**
    1.  Jika menggunakan koleksi `services_categories`, Admin dapat melakukan operasi CRUD pada koleksi tersebut.
    2.  Jika kategori di-hardcode di aplikasi, perubahan memerlukan update aplikasi.
*   **Integrasi Appwrite:** CRUD pada koleksi `services_categories`.

### 3.5 Modul Notifikasi (Fokus In-App untuk MVP)

**FR-NOTIF-001: Notifikasi Pemesanan Baru untuk Penyedia Layanan**
*   **Deskripsi:** Penyedia Layanan menerima notifikasi (in-app) ketika ada permintaan pemesanan baru.
*   **Aktor:** Penyedia Layanan.
*   **Pemicu:** Dokumen baru dibuat di koleksi `bookings` dengan `providerId` yang sesuai.
*   **Alur Utama:**
    1.  Saat Penyedia Layanan membuka aplikasi atau melakukan refresh pada daftar pemesanan, sistem menampilkan indikator notifikasi (misalnya, badge) atau item baru dalam daftar pemesanan masuk.
*   **Integrasi Appwrite:** Query periodik atau real-time (jika didukung dan sesuai batasan gratis) ke koleksi `bookings`. *Appwrite Functions untuk push notification bisa dipertimbangkan pasca-MVP karena potensi kompleksitas dan batasan free tier.*

**FR-NOTIF-002: Notifikasi Pembaruan Status Pemesanan untuk Pelanggan**
*   **Deskripsi:** Pelanggan menerima notifikasi (in-app) ketika status pemesanan mereka diperbarui oleh Penyedia Layanan (Dikonfirmasi, Ditolak, Selesai).
*   **Aktor:** Pelanggan.
*   **Pemicu:** Atribut `status` pada dokumen `bookings` diperbarui.
*   **Alur Utama:**
    1.  Saat Pelanggan membuka aplikasi atau melakukan refresh pada riwayat pemesanan, sistem menampilkan indikator notifikasi atau status terbaru pada pemesanan terkait.
*   **Integrasi Appwrite:** Query periodik atau real-time.

---

## 4. Persyaratan Non-Fungsional (How well the system performs)

### 4.1 Performa
*   **NFR-PERF-001 (Waktu Respons):** Waktu loading data utama (daftar layanan, daftar penyedia, riwayat pemesanan) dan navigasi antar halaman tidak boleh lebih dari 3-5 detik pada kondisi jaringan seluler 4G normal.
*   **NFR-PERF-002 (Skalabilitas):** Meskipun menggunakan Appwrite versi gratis untuk MVP, arsitektur kode Flutter dan struktur database harus dirancang sedemikian rupa sehingga memungkinkan peningkatan jumlah pengguna dan transaksi di masa mendatang dengan migrasi ke Appwrite versi berbayar atau self-hosted yang lebih besar tanpa memerlukan refactoring besar pada logika inti aplikasi.

### 4.2 Keamanan
*   **NFR-SEC-001 (Autentikasi):** Semua akses ke fitur yang memerlukan identifikasi pengguna harus dilindungi oleh mekanisme autentikasi Appwrite yang aman. Sesi pengguna harus dikelola dengan aman.
*   **NFR-SEC-002 (Otorisasi):** Pengguna hanya dapat mengakses dan memanipulasi data yang menjadi hak mereka. Ini akan diimplementasikan menggunakan Appwrite Permissions pada level koleksi dan dokumen.
    *   Pelanggan hanya dapat melihat dan mengelola pemesanan mereka sendiri.
    *   Penyedia Layanan hanya dapat melihat dan mengelola pemesanan yang ditujukan kepada mereka dan profil mereka sendiri.
    *   Data Penyedia Layanan yang `is_verified: false` tidak boleh terlihat oleh Pelanggan.
*   **NFR-SEC-003 (Perlindungan Data):** Password pengguna harus di-hash oleh Appwrite dan tidak disimpan dalam format plain text. Komunikasi antara aplikasi klien dan server Appwrite harus menggunakan HTTPS.
*   **NFR-SEC-004 (Input Validation):** Semua input dari pengguna harus divalidasi di sisi klien dan (jika memungkinkan dengan Appwrite) di sisi server untuk mencegah data korup atau serangan dasar.

### 4.3 Usability (Kegunaan)
*   **NFR-USAB-001 (Intuitif):** Antarmuka pengguna harus dirancang secara intuitif, jelas, dan mudah dipahami serta dinavigasi oleh target pengguna (Pelanggan dan Penyedia Layanan) tanpa memerlukan pelatihan khusus.
*   **NFR-USAB-002 (Konsistensi):** Desain UI dan pola interaksi (UX) harus konsisten di seluruh bagian aplikasi untuk memberikan pengalaman pengguna yang koheren.
*   **NFR-USAB-003 (Pesan Kesalahan):** Aplikasi harus menampilkan pesan kesalahan yang jelas, informatif, dan ramah pengguna ketika terjadi masalah (misalnya, "Koneksi internet terputus", "Email sudah terdaftar", "Terjadi kesalahan, coba lagi nanti").
*   **NFR-USAB-004 (Feedback Pengguna):** Aplikasi harus memberikan feedback visual kepada pengguna atas tindakan mereka (misalnya, loading indicator saat mengambil data, pesan sukses setelah operasi berhasil).

### 4.4 Reliabilitas (Keandalan)
*   **NFR-REL-001 (Ketersediaan):** Fungsi inti aplikasi harus tersedia dan berfungsi selama server Appwrite aktif dan dapat diakses.
*   **NFR-REL-002 (Penanganan Error):** Aplikasi harus dapat menangani kesalahan API dari Appwrite atau masalah jaringan secara gracefully tanpa crash. Pengguna harus diberi tahu jika ada masalah koneksi.
*   **NFR-REL-003 (Konsistensi Data):** Sistem harus memastikan konsistensi data pemesanan dan status pengguna sejauh mungkin, terutama saat ada operasi update.

### 4.5 Maintainability (Kemudahan Pemeliharaan)
*   **NFR-MAINT-001 (Kode Bersih):** Kode sumber Flutter harus ditulis dengan mengikuti praktik terbaik (misalnya, SOLID principles jika relevan, penamaan variabel yang jelas, komentar pada logika kompleks).
*   **NFR-MAINT-002 (Modularitas):** Arsitektur kode harus modular (misalnya, memisahkan UI, logika bisnis, dan layanan data) untuk memudahkan pemahaman, pengujian, dan penambahan fitur di masa depan. Penggunaan state management yang terstruktur (Provider, BLoC, Riverpod, GetX) sangat dianjurkan.
*   **NFR-MAINT-003 (Dokumentasi Kode):** Komentar pada kode harus ada untuk bagian-bagian yang kompleks atau tidak jelas secara langsung.

### 4.6 Portabilitas
*   **NFR-PORT-001 (Cross-Platform):** Aplikasi yang dikembangkan dengan Flutter harus berfungsi dengan baik dan memberikan pengalaman pengguna yang konsisten di platform Android (minimal versi 8.0 Oreo ke atas) dan iOS (minimal versi 12.0 ke atas).

### 4.7 Persyaratan Lingkungan
*   **Flutter SDK:** Versi stabil terbaru yang direkomendasikan.
*   **Appwrite Server:** Versi stabil terbaru yang kompatibel.
*   **Perangkat Target (Minimum):** Smartphone dengan RAM minimal 2GB.

---

## 5. Persyaratan Antarmuka Eksternal

### 5.1 Antarmuka Pengguna (UI)
*   Aplikasi akan mengadopsi prinsip desain Material Design (untuk Android) dan Cupertino (aspek tertentu untuk iOS) atau gaya desain kustom yang konsisten dan modern.
*   Antarmuka harus responsif terhadap berbagai ukuran layar smartphone.
*   **Wireframe/Mock-up Dasar (Perlu dibuat terpisah, contoh halaman kunci):**
    *   Splash Screen
    *   Halaman Pilihan Peran (Pelanggan/Penyedia) saat pertama kali atau jika belum login.
    *   Halaman Pendaftaran (form umum, lalu spesifik peran).
    *   Halaman Login.
    *   **Pelanggan:**
        *   Halaman Utama (Dashboard dengan daftar Kategori Layanan).
        *   Halaman Daftar Penyedia (hasil pencarian).
        *   Halaman Detail Profil Penyedia Layanan.
        *   Halaman Form Pemesanan.
        *   Halaman Riwayat Pemesanan (dengan filter status).
        *   Halaman Profil Pelanggan.
    *   **Penyedia Layanan:**
        *   Halaman Utama (Dashboard dengan ringkasan pemesanan masuk, toggle ketersediaan).
        *   Halaman Daftar Pemesanan Masuk.
        *   Halaman Detail Pemesanan.
        *   Halaman Riwayat Pekerjaan.
        *   Halaman Profil Penyedia Layanan (untuk edit).
*   Font, palet warna, dan ikonografi akan ditentukan dalam panduan gaya desain terpisah.

### 5.2 Antarmuka Perangkat Lunak
*   **Appwrite SDK (Flutter):** Aplikasi akan menggunakan Appwrite SDK resmi untuk Flutter untuk semua interaksi dengan backend Appwrite, termasuk:
    *   `Appwrite.account`: Untuk autentikasi pengguna (pendaftaran, login, logout, sesi, lupa password).
    *   `Appwrite.database`: Untuk operasi CRUD (Create, Read, Update, Delete) pada koleksi `users` dan `bookings`.
    *   `Appwrite.realtime` (jika digunakan untuk notifikasi in-app dasar dan sesuai batasan free tier).
*   **Package Flutter Pihak Ketiga (Contoh):**
    *   State Management: `provider`, `flutter_bloc`, `riverpod`, atau `get`.
    *   Navigasi: `go_router` atau navigator bawaan Flutter.
    *   HTTP Client (jika diperlukan di luar SDK Appwrite, biasanya tidak untuk MVP ini): `http` atau `dio`.
    *   Format Tanggal/Waktu: `intl`.
    *   UI Components Tambahan: Sesuai kebutuhan (misalnya, `flutter_slidable` untuk aksi pada list item).

---

## 6. Model Data (Skema Appwrite Database)

### 6.1 Koleksi `users`
*   **Tujuan:** Menyimpan informasi profil untuk semua pengguna (Pelanggan, Penyedia Layanan, dan Admin). Peran dibedakan oleh atribut `role`.
*   **ID Dokumen:** Menggunakan ID unik yang dihasilkan oleh Appwrite (`$id`) atau `userId` dari Appwrite Authentication.
*   **Atribut:**
    *   `userId` (String, Wajib, Unik): ID dari Appwrite Authentication. Digunakan sebagai foreign key di koleksi lain.
    *   `name` (String, Wajib): Nama lengkap pengguna atau nama usaha untuk Penyedia.
    *   `email` (String, Wajib, Unik): Alamat email (digunakan untuk login).
    *   `phoneNumber` (String, Opsional tapi Wajib untuk Penyedia): Nomor telepon aktif.
    *   `role` (String, Wajib, Enum: `"customer"`, `"provider"`, `"admin"`): Peran pengguna dalam sistem.
    *   `profilePictureUrl` (String, Opsional): URL ke gambar profil (jika diunggah ke Appwrite Storage).
    *   `address` (String, Opsional, khusus `role: "customer"`): Alamat utama pelanggan.
    *   `serviceType` (String, Opsional, khusus `role: "provider"`): Jenis layanan utama yang ditawarkan (misalnya, "Teknisi AC", "Tukang Ledeng"). Bisa juga list of strings jika penyedia menawarkan beberapa layanan utama.
    *   `expertiseDescription` (String, Opsional, khusus `role: "provider"`): Deskripsi singkat keahlian.
    *   `areaCoverage` (String, Opsional, khusus `role: "provider"`): Teks deskriptif area jangkauan layanan (misalnya, "Jakarta Selatan, Tangerang Kota").
    *   `isVerified` (Boolean, Wajib, Default: `false`, khusus `role: "provider"`): Status verifikasi oleh Admin. Hanya Penyedia yang `isVerified: true` yang aktif.
    *   `isAvailable` (Boolean, Wajib, Default: `true`, khusus `role: "provider"`): Status ketersediaan Penyedia untuk menerima pesanan baru.
    *   `createdAt` (Datetime, Otomatis oleh Appwrite): Waktu pembuatan akun.
    *   `updatedAt` (Datetime, Otomatis oleh Appwrite): Waktu pembaruan akun.
*   **Indeks (Contoh):** `email`, `role`, `serviceType` (jika sering difilter), `isVerified`, `isAvailable`.
*   **Izin (Permissions) - Contoh Konfigurasi Dasar:**
    *   **Dokumen Level:**
        *   Read: `role:all` (untuk data publik seperti nama, serviceType, areaCoverage pada profil provider yang sudah terverifikasi), `user:[userId]` (pengguna bisa baca data sendiri).
        *   Update: `user:[userId]` (pengguna hanya bisa update data sendiri).
        *   Delete: `user:[userId]` (pengguna bisa hapus akun sendiri, atau hanya Admin).
    *   **Koleksi Level:**
        *   Create: `role:all` (untuk pendaftaran).

### 6.2 Koleksi `bookings`
*   **Tujuan:** Menyimpan semua detail transaksi pemesanan layanan.
*   **ID Dokumen:** Menggunakan ID unik yang dihasilkan oleh Appwrite (`$id`).
*   **Atribut:**
    *   `customerId` (String, Wajib, Relasi ke `users.userId`): ID Pelanggan yang membuat pemesanan.
    *   `providerId` (String, Wajib, Relasi ke `users.userId`): ID Penyedia Layanan yang dituju.
    *   `serviceTypeBooked` (String, Wajib): Jenis layanan spesifik yang dipesan (misalnya, "Cuci AC", "Perbaikan Pipa Bocor").
    *   `problemDescription` (String, Wajib): Deskripsi masalah atau kebutuhan dari Pelanggan.
    *   `serviceAddress` (String, Wajib): Alamat lengkap tempat layanan akan dilakukan.
    *   `bookingDate` (Datetime, Wajib): Tanggal yang diinginkan untuk layanan.
    *   `timeSlot` (String, Wajib, Enum: `"Pagi"`, `"Siang"`, `"Sore"` atau format waktu spesifik): Slot waktu yang dipilih.
    *   `status` (String, Wajib, Enum: `"pending_confirmation"`, `"confirmed_by_provider"`, `"rejected_by_provider"`, `"cancelled_by_customer"`, `"completed"`): Status terkini pemesanan.
    *   `rejectionReason` (String, Opsional): Alasan penolakan oleh Penyedia.
    *   `cancellationReason` (String, Opsional): Alasan pembatalan oleh Pelanggan.
    *   `createdAt` (Datetime, Otomatis oleh Appwrite): Waktu pemesanan dibuat.
    *   `updatedAt` (Datetime, Otomatis oleh Appwrite): Waktu pemesanan terakhir diperbarui.
*   **Indeks (Contoh):** `customerId`, `providerId`, `status`, `bookingDate`.
*   **Izin (Permissions) - Contoh Konfigurasi Dasar:**
    *   **Dokumen Level:**
        *   Read: `user:[customerId]`, `user:[providerId]`, `role:admin`.
        *   Update: `user:[customerId]` (untuk pembatalan), `user:[providerId]` (untuk update status terima/tolak/selesai), `role:admin`.
    *   **Koleksi Level:**
        *   Create: `user:[loggedInUserId]` (hanya pengguna terdaftar yang bisa membuat booking).

### 6.3 Koleksi `services_categories` (Opsional untuk MVP, bisa disederhanakan dengan list statis di Flutter)
*   **Tujuan:** Menyimpan daftar kategori layanan utama yang ditawarkan platform (jika tidak di-hardcode).
*   **ID Dokumen:** ID unik (`$id`).
*   **Atribut:**
    *   `name` (String, Wajib, Unik): Nama kategori layanan (misalnya, "Teknisi AC").
    *   `description` (String, Opsional): Deskripsi singkat.
    *   `iconUrl` (String, Opsional): URL ikon.
    *   `isActive` (Boolean, Wajib, Default: `true`).
*   **Izin (Permissions):**
    *   Read: `role:all`.
    *   Create, Update, Delete: `role:admin`.

---

## 7. Diagram Alur (Flowcharts)

### 7.1 Alur Pelanggan

```mermaid
flowchart TD
    A[Mulai Aplikasi Servisku] --> B{Sudah Punya Akun?};
    B -- Ya --> C[Login dengan Email & Password];
    B -- Tidak --> D[Pilih "Daftar"];
    D --> D1[Pilih Peran "Pelanggan"];
    D1 --> D2[Isi Form Pendaftaran Pelanggan];
    D2 -- Validasi --> E[Akun Pelanggan Dibuat];
    C --> F[Halaman Utama Pelanggan];
    E --> F;
    F --> G[Pilih/Cari Kategori Layanan];
    G --> H[Tampilkan Daftar Penyedia Layanan (Terverifikasi & Tersedia)];
    H --> I{Pilih Penyedia?};
    I -- Ya --> J[Lihat Detail Profil Penyedia];
    J --> K[Klik "Pesan Sekarang"];
    K --> L[Isi Form Pemesanan (Tanggal, Waktu, Masalah, Alamat)];
    L -- Validasi --> M[Konfirmasi Pemesanan];
    M --> N[Pemesanan Dibuat (Status: Menunggu Konfirmasi)];
    N --> O[Terima Notifikasi Pembaruan Status];
    O --> P[Lihat Riwayat & Status Pemesanan];
    P --> Q[Selesai];
    I -- Tidak / Kembali --> H;
```

### 7.2 Alur Penyedia Layanan

```mermaid
flowchart TD
    A[Mulai Aplikasi Servisku] --> B{Sudah Punya Akun?};
    B -- Ya --> C[Login dengan Email & Password];
    B -- Tidak --> D[Pilih "Daftar"];
    D --> D1[Pilih Peran "Penyedia Layanan"];
    D1 --> D2[Isi Form Pendaftaran Penyedia];
    D2 -- Validasi --> E[Akun Penyedia Dibuat (Status: Belum Diverifikasi)];
    E --> E1[Menunggu Verifikasi Admin];
    C --> F[Halaman Utama Penyedia Layanan];
    E1 -- Diverifikasi Admin --> F;
    F --> G[Atur Status Ketersediaan (Tersedia/Tidak Tersedia)];
    F --> H[Lihat Daftar Pemesanan Masuk (Status: Menunggu Konfirmasi)];
    H --> I{Pilih Pemesanan?};
    I -- Ya --> J[Lihat Detail Pemesanan];
    J --> K{Terima atau Tolak Pemesanan?};
    K -- Terima --> L[Update Status: Dikonfirmasi];
    K -- Tolak --> M[Update Status: Ditolak];
    L --> N[Kirim Notifikasi ke Pelanggan];
    M --> N;
    L --> O{Pekerjaan Selesai?};
    O -- Ya --> P[Update Status: Selesai];
    P --> N;
    F --> Q[Edit Profil Penyedia];
    F --> R[Lihat Riwayat Pekerjaan];
    R --> S[Selesai];
    I -- Tidak / Kembali --> H;
```

### 7.3 Alur Verifikasi Admin (Konseptual)

```mermaid
flowchart TD
    A[Admin Login ke Appwrite Console / Dashboard Admin] --> B[Akses Daftar Penyedia (is_verified: false)];
    B --> C{Ada Pendaftar Baru?};
    C -- Ya --> D[Review Detail Profil Pendaftar];
    D --> E{Data Valid & Memenuhi Syarat?};
    E -- Ya --> F[Update Status Penyedia: is_verified = true];
    E -- Tidak --> G[Hubungi Pendaftar (jika perlu) atau Tandai Ditolak/Hapus];
    F --> H[Penyedia Terverifikasi & Aktif di Platform];
    C -- Tidak --> I[Selesai/Monitor Aktivitas Lain];
```

---

## 8. Metrik Kesuksesan MVP
*   **Jumlah Pendaftaran Pengguna Aktif (Pelanggan):** Target [X] pengguna dalam 1 bulan pertama.
*   **Jumlah Pendaftaran Penyedia Layanan Terverifikasi:** Target [Y] penyedia dalam 1 bulan pertama.
*   **Jumlah Pemesanan yang Berhasil Dibuat:** Target [Z] pemesanan dalam 1 bulan pertama.
*   **Tingkat Konversi Pemesanan (Dari Lihat Profil Penyedia ke Buat Pesanan):** Persentase.
*   **Tingkat Penerimaan Pesanan oleh Penyedia:** Persentase pesanan yang diterima dari total pesanan masuk ke penyedia.
*   **Waktu Rata-rata dari Pemesanan Dibuat hingga Dikonfirmasi Penyedia.**
*   **Umpan Balik Kualitatif:** Kumpulkan feedback dari pengguna awal (Pelanggan dan Penyedia) melalui survei singkat atau wawancara untuk memahami pengalaman mereka, kesulitan yang dihadapi, dan fitur yang paling diinginkan selanjutnya.

---

## 9. Rencana Iterasi Setelah MVP
Berdasarkan analisis metrik kesuksesan MVP dan umpan balik pengguna, prioritas pengembangan selanjutnya dapat mencakup:
1.  **Sistem Ulasan dan Rating:** Membangun kepercayaan dan transparansi.
2.  **Integrasi Pembayaran Sederhana:** (misalnya, transfer manual dengan konfirmasi unggah bukti, sebelum ke payment gateway penuh).
3.  **Fitur Chat In-App:** Memudahkan komunikasi antara Pelanggan dan Penyedia Layanan.
4.  **Notifikasi Push Real-time:** Menggunakan Appwrite Functions atau layanan pihak ketiga.
5.  **Pencarian Berbasis Lokasi Lebih Akurat:** Menggunakan GPS atau filter jarak.
6.  **Manajemen Jadwal Lebih Detail untuk Penyedia Layanan:** Kalender ketersediaan.
7.  **Portofolio Pekerjaan untuk Penyedia Layanan.**
8.  **Layanan Darurat/Cepat.**
9.  **Paket Layanan atau Langganan.**

---

## 10. Glossarium/Indeks
(Semua akronim dan istilah teknis utama telah didefinisikan di bagian [1.4 Definisi, Akronim, dan Singkatan](#14-definisi-akronim-dan-singkatan)).

---

Ini adalah draf SRS yang komprehensif berdasarkan input Anda. Anda mungkin perlu menyesuaikan beberapa detail kecil, terutama pada bagian Izin (Permissions) di Appwrite agar sesuai dengan kebutuhan keamanan spesifik Anda dan batasan Appwrite free tier. Semoga ini membantu!