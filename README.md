<div align="center">

# Sistem Informasi Peminjaman Alat — UKK RPL Paket 1

Aplikasi manajemen peminjaman alat sekolah/laboratorium, dibangun menggunakan **Laravel** dan **Filament v3**.
Dikembangkan mengikuti serial tutorial YouTube *"Aplikasi Peminjaman Alat — UKK RPL Paket 1"* oleh **Iwan Setiawan**.

**Status: 🚧 Work in Progress — Part 15 dari 17**

</div>

---

## Fitur

> Progress saat ini mengikuti tutorial sampai **Part 15**. Fitur pengembalian, denda, dan laporan masih dalam pengembangan.

- **Autentikasi & Role-based Access Control** — login dengan pembagian hak akses Admin dan Petugas
- **Manajemen Master Data Alat** — CRUD data alat/barang laboratorium melalui panel admin
- **Manajemen Kategori Alat** — CRUD kategori alat
- **Manajemen User & Role** — pengelolaan akun pengguna beserta perannya
- **Alur Peminjaman Alat** — form pengajuan peminjaman alat (proses awal)
- **Admin CMS (Filament)** — dashboard, tabel data dengan pencarian & filter, form builder otomatis

**Belum tersedia (Upcoming):**
- Fitur pengembalian alat & perhitungan denda keterlambatan
- Cetak laporan / export data peminjaman

---

## Tech Stack

| Layer | Teknologi |
|---|---|
| Backend | Laravel |
| Admin Panel | Filament v3 |
| Frontend | Blade + Tailwind CSS |
| Database | MySQL / MariaDB |
| Environment | PHP >= 8.2, Composer, Node.js |

---

## Struktur Database (ERD)

```
users (id, name, email, password, role[admin/petugas])
  └── hasMany → loans

categories (id, name, slug)
  └── hasMany → tools

tools (id, category_id, name, code, stock, condition, image)
  ├── belongsTo → categories
  └── hasMany → loan_items

loans (id, user_id, borrower_name, loan_date, return_date, status)
  ├── belongsTo → users
  └── hasMany → loan_items

loan_items (id, loan_id, tool_id, quantity)
  ├── belongsTo → loans
  └── belongsTo → tools
```

> Skema di atas merupakan gambaran umum relasi antar tabel sampai dengan Part 15. Struktur dapat berubah/bertambah pada part-part selanjutnya (misalnya penambahan tabel untuk pengembalian & denda).

---

## Instalasi

### Prasyarat
- PHP >= 8.2 (dengan ekstensi `zip`, `fileinfo`, `gd`, `intl`, `pdo_mysql` aktif)
- Composer
- MySQL / MariaDB
- Node.js & NPM (jika ingin build ulang asset)

### Langkah-langkah

**1. Clone repository**
```bash
git clone https://github.com/Chizuyu/UKK-RPL-1.git
cd UKK-RPL-1
```

**2. Install dependency**
```bash
composer install
npm install
```

**3. Setup environment**
```bash
cp .env.example .env
php artisan key:generate
```

Edit `.env`, sesuaikan koneksi database dan `APP_URL` (harus sama persis dengan alamat yang diakses di browser):
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=peminjaman_alat
DB_USERNAME=root
DB_PASSWORD=

APP_URL=http://localhost:8000
```

**4. Migrasi *
```bash
php artisan migrate 
```

**5. Buat akun admin pertama**
```bash
php artisan tinker
```
```php
\App\Models\User::create([
    'name' => 'Admin',
    'email' => 'admin@gmail.com',
    'password' => bcrypt('123'),
]);
```

**6. Link storage** (wajib, agar gambar upload bisa diakses publik)
```bash
php artisan storage:link
```

**7. Build asset frontend** (opsional, jika ada perubahan CSS/JS)
```bash
npm run build
```

**8. Jalankan server**
```bash
php artisan serve
```

---

## Akses Aplikasi

| Halaman | URL |
|---|---|
| Admin CMS (Filament) | `http://localhost:8000/admin` |


## Struktur Project (Ringkas)

```
app/
├── Filament/
│   └── Resources/                   # User, Category, Tool, Loan
├── Models/
│   ├── User.php
│   ├── Category.php
│   ├── Tool.php
│   ├── Loan.php
│   └── LoanItem.php
└── Providers/Filament/AdminPanelProvider.php

database/
├── migrations/
└── seeders/

routes/web.php
```

---

## Referensi / Credit

Proyek ini dibangun dengan mengikuti serial tutorial YouTube **"Aplikasi Peminjaman Alat — UKK RPL Paket 1"** oleh **Iwan Setiawan**, yang membahas pembuatan Sistem Informasi Peminjaman Alat menggunakan Laravel dan Filament PHP secara bertahap.

▶️ **Playlist Tutorial:** [Aplikasi Peminjaman Alat - UKK RPL Paket 1 (YouTube Playlist)](https://youtube.com/playlist?list=PLsB_GEZYywrdmcLmIuxvvfoz0VnxiCVxA)

Seluruh kredit konsep, alur pembelajaran, dan struktur pengerjaan proyek merupakan hasil karya dari channel YouTube Iwan Setiawan. Repository ini dibuat untuk tujuan pembelajaran dan latihan pribadi (UKK RPL).

---

## Dokumentasi

<!-- Tempel screenshot aplikasi di sini, contoh format:
<img width="1920" height="1080" alt="Landing Page" src="URL_SCREENSHOT_ANDA" />
-->
