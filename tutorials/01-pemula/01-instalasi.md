# 01. Instalasi Laravel & Filament

## 🚀 Step 1: Buat Project Laravel

```bash
# Buat project baru
composer create-project laravel/laravel blog-filament

# Masuk ke folder
cd blog-filament
```

## 🗄️ Step 2: Setup Database

### Buat Database

Buat database baru di MySQL dengan nama `blog_filament`.

### Konfigurasi .env

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=blog_filament
DB_USERNAME=root
DB_PASSWORD=
```

## 📦 Step 3: Install Filament

```bash
# Install Filament
composer require filament/filament:"^3.2"

# Install panel
php artisan filament:install --panels
```

Saat ditanya nama panel, ketik: `admin`

## 👤 Step 4: Buat User Admin

```bash
php artisan make:filament-user
```

Isi data:

- Name: `Admin`
- Email: `admin@admin.com`
- Password: `password`

## ▶️ Step 5: Jalankan Server

```bash
php artisan serve
```

## ✅ Step 6: Test Akses

1. Buka: `http://localhost:8000/admin`
2. Login dengan email dan password yang dibuat
3. Jika berhasil, Anda akan melihat dashboard Filament! 🎉

## 📸 Hasil

Anda seharusnya melihat:

- Halaman login Filament
- Dashboard kosong setelah login

## ➡️ Selanjutnya

Lanjut ke: [02-authentication.md](02-authentication.md)
