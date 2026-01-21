# 06. Deploy ke Shared Hosting

## 📋 Persiapan Sebelum Deploy

### 1. Update .env untuk Production

```env
APP_NAME="Blog Admin"
APP_ENV=production
APP_DEBUG=false
APP_URL=https://yourdomain.com

DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=your_database
DB_USERNAME=your_username
DB_PASSWORD=your_password
```

### 2. Optimize untuk Production

```bash
# Di local sebelum upload
composer install --optimize-autoloader --no-dev
php artisan config:cache
php artisan route:cache
php artisan view:cache
php artisan icons:cache
```

## 📦 Step 1: Persiapkan Files

1. Zip semua folder KECUALI:
   - `node_modules/`
   - `.git/`
   - `storage/app/public/` (buat kosong)

2. Export database:

```bash
mysqldump -u root -p blog_filament > backup.sql
```

## 🚀 Step 2: Upload ke Hosting

### Struktur Folder di Hosting

```
public_html/
├── index.php (modified)
├── .htaccess
├── storage/ -> ../storage/app/public (symlink)
└── assets, css, js...

laravel-app/  (di luar public_html)
├── app/
├── bootstrap/
├── config/
├── database/
├── resources/
├── routes/
├── storage/
├── vendor/
└── ...
```

### Upload Files

1. **Upload** folder Laravel ke luar `public_html`
2. **Pindahkan** isi folder `public/` ke `public_html/`
3. **Edit** `public_html/index.php`:

```php
// Ubah path ini
require __DIR__.'/../laravel-app/vendor/autoload.php';
$app = require_once __DIR__.'/../laravel-app/bootstrap/app.php';
```

## 🗄️ Step 3: Setup Database

1. Buat database baru di cPanel
2. Import file `backup.sql`
3. Update `.env` dengan credentials baru

## 🔗 Step 4: Setup Storage Link

Via SSH:

```bash
cd laravel-app
php artisan storage:link
```

Atau buat file `create-symlink.php`:

```php
<?php
symlink(
    '/home/username/laravel-app/storage/app/public',
    '/home/username/public_html/storage'
);
echo 'Symlink created!';
```

## ✅ Step 5: Final Setup

```bash
# Via SSH atau terminal hosting
php artisan migrate --force
php artisan filament:assets
php artisan optimize
```

## 🔒 Step 6: Security

1. Pastikan `.env` tidak bisa diakses publik
2. Set folder permissions:
   - `storage/` → 775
   - `bootstrap/cache/` → 775

## 📋 Checklist Deploy

- [ ] .env sudah dikonfigurasi
- [ ] Database sudah diimport
- [ ] Storage link sudah dibuat
- [ ] Migrations sudah dijalankan
- [ ] APP_DEBUG=false
- [ ] Cache sudah di-generate

## 🎉 Selesai!

Buka `https://yourdomain.com/admin` dan login!

---

## 🎓 Recap Tutorial Pemula

Anda telah belajar:

- ✅ Install Laravel + Filament
- ✅ Authentication dasar
- ✅ CRUD Categories & Posts
- ✅ Relasi antar table
- ✅ Customization dashboard
- ✅ Deploy ke production

## ➡️ Lanjut ke Level Berikutnya

Siap naik level? Lanjut ke: [Tutorial Intermediate](../02-intermediate/README.md)
