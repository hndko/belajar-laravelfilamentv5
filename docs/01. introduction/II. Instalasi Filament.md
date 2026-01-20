# II. Instalasi Filament 📥

> **Sumber:** [https://filamentphp.com/docs/5.x/introduction/installation](https://filamentphp.com/docs/5.x/introduction/installation)

---

## 📋 Syarat yang Dibutuhkan

Sebelum install Filament, pastikan kamu sudah punya:

| Syarat       | Versi Minimum         |
| ------------ | --------------------- |
| PHP          | 8.2 atau lebih baru   |
| Laravel      | 11.28 atau lebih baru |
| Tailwind CSS | 4.1 atau lebih baru   |

---

## 🚀 Dua Cara Install Filament

Ada dua cara untuk menggunakan Filament:

### Cara 1: Panel Builder (Paling Populer) ⭐

Ini untuk membuat **panel admin lengkap** dengan sidebar, menu, dashboard, dll.

**Kapan pilih ini:** Kamu ingin membuat halaman admin yang lengkap.

### Cara 2: Komponen Individual

Ini untuk menggunakan **komponen Filament tertentu** di dalam Blade views yang sudah ada.

**Kapan pilih ini:** Kamu sudah punya website dan hanya ingin menambahkan fitur tertentu (misalnya tabel interaktif).

---

## 📦 Cara 1: Install Panel Builder

### Langkah 1: Install via Composer

Buka terminal di folder proyekmu, lalu jalankan:

```bash
composer require filament/filament:"^5.0"
php artisan filament:install --panels
```

> **Catatan untuk Windows PowerShell:**
> Gunakan tanda `~` bukan `^`:
>
> ```bash
> composer require filament/filament:"~5.0"
> php artisan filament:install --panels
> ```

### Apa yang Terjadi?

Perintah ini akan membuat file baru:

```
app/Providers/Filament/AdminPanelProvider.php
```

File ini adalah "pusat kontrol" untuk panel admin kamu.

### Langkah 2: Buat User Admin

```bash
php artisan make:filament-user
```

Ikuti instruksi di terminal untuk memasukkan:

- Nama
- Email
- Password

### Langkah 3: Buka Panel Admin

Buka browser dan kunjungi:

```
http://localhost/admin
```

Login dengan akun yang baru kamu buat tadi!

---

## 🧩 Cara 2: Install Komponen Individual

Jika kamu hanya butuh komponen tertentu:

```bash
composer require filament/tables:"^5.0" filament/forms:"^5.0"
```

Kamu bisa pilih komponen yang dibutuhkan saja:

- `filament/tables` - untuk tabel
- `filament/forms` - untuk form
- `filament/schemas` - untuk skema UI
- `filament/infolists` - untuk daftar informasi
- `filament/actions` - untuk tombol aksi
- `filament/notifications` - untuk notifikasi
- `filament/widgets` - untuk widget

---

## 🎨 Setup Tailwind CSS (untuk Komponen Individual)

### Langkah 1: Install Tailwind

```bash
npm install tailwindcss @tailwindcss/vite --save-dev
```

### Langkah 2: Edit `resources/css/app.css`

Tambahkan import yang diperlukan:

```css
@import "tailwindcss";

/* Wajib untuk semua komponen */
@import "../../vendor/filament/support/resources/css/index.css";

/* Pilih sesuai komponen yang kamu install */
@import "../../vendor/filament/forms/resources/css/index.css";
@import "../../vendor/filament/tables/resources/css/index.css";
/* ... tambahkan sesuai kebutuhan */

@variant dark (&:where(.dark, .dark *));
```

### Langkah 3: Edit `vite.config.js`

```javascript
import { defineConfig } from "vite";
import laravel from "laravel-vite-plugin";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [
    laravel({
      input: ["resources/css/app.css", "resources/js/app.js"],
      refresh: true,
    }),
    tailwindcss(),
  ],
});
```

### Langkah 4: Compile Assets

```bash
npm install
npm run dev
```

---

## 📄 Setup Layout (untuk Komponen Individual)

### Langkah 1: Buat File Layout

```bash
php artisan livewire:layout
```

Ini akan membuat file di:

```
resources/views/components/layouts/app.blade.php
```

### Langkah 2: Edit Layout

```html
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="csrf-token" content="{{ csrf_token() }}" />
    <title>{{ config('app.name') }}</title>

    <style>
      [x-cloak] {
        display: none !important;
      }
    </style>

    @filamentStyles @vite('resources/css/app.css')
  </head>
  <body class="antialiased">
    {{ $slot }} @livewire('notifications') {{-- Hanya jika pakai notifikasi --}}
    @filamentScripts @vite('resources/js/app.js')
  </body>
</html>
```

**Yang Penting:**

- `@filamentStyles` - di dalam `<head>` untuk CSS Filament
- `@filamentScripts` - di akhir `<body>` untuk JavaScript Filament

---

## ⚙️ Publish Konfigurasi

Untuk melihat dan mengubah pengaturan Filament:

```bash
php artisan vendor:publish --tag=filament-config
```

Ini akan membuat file:

```
config/filament.php
```

Di sini kamu bisa mengatur berbagai opsi seperti disk penyimpanan, pengaturan UI, dll.

---

## 🔍 Troubleshooting

### Error saat akses /admin?

Cek apakah service provider sudah terdaftar di:

```
bootstrap/providers.php
```

Jika belum ada, tambahkan:

```php
App\Providers\Filament\AdminPanelProvider::class,
```

---

## 💡 Ringkasan

| Langkah                  | Perintah                                    |
| ------------------------ | ------------------------------------------- |
| Install Filament (Panel) | `composer require filament/filament:"^5.0"` |
| Setup Panel              | `php artisan filament:install --panels`     |
| Buat User Admin          | `php artisan make:filament-user`            |
| Akses Admin              | Buka `/admin` di browser                    |

---

## 🎯 Latihan Mandiri

1. Install Filament Panel Builder di proyekmu
2. Buat user admin dengan nama dan emailmu
3. Login ke halaman admin
4. Eksplorasi tampilan dashboard kosong

<details>
<summary>Tips Jika Stuck</summary>

- Pastikan versi PHP sudah 8.2+: `php -v`
- Pastikan Laravel sudah v11+: `php artisan --version`
- Jika ada error, baca pesan errornya dengan teliti

</details>
