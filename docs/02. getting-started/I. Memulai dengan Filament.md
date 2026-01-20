# I. Memulai dengan Filament 🚀

> **Sumber:** [https://filamentphp.com/docs/5.x/getting-started](https://filamentphp.com/docs/5.x/getting-started)

---

## 🤔 Apa yang Harus Dilakukan Setelah Install?

Setelah kamu [menginstall Filament](../01.%20introduction/II.%20Instalasi%20Filament.md), langkah selanjutnya adalah mulai membangun aplikasimu!

### Langkah Pertama:

1. Buka browser
2. Kunjungi `/admin` (contoh: `http://localhost/admin`)
3. Login dengan akun yang sudah dibuat
4. Kamu akan melihat **Dashboard** (halaman utama panel)

> **Catatan:** Panduan ini untuk **Panel Builder** Filament. Jika kamu ingin menggunakan komponen Filament di luar panel, lihat dokumentasi [Components](https://filamentphp.com/docs/5.x/components).

---

## 📚 Tiga Hal Utama di Filament

Di Filament, ada **3 hal utama** yang perlu kamu ketahui:

| Komponen         | Fungsi                             | Contoh                           |
| ---------------- | ---------------------------------- | -------------------------------- |
| **Resources**    | Mengelola data (CRUD)              | Halaman daftar produk, edit user |
| **Widgets**      | Menampilkan statistik di dashboard | Chart penjualan, jumlah user     |
| **Custom Pages** | Halaman bebas sesuai kebutuhan     | Halaman pengaturan, dokumentasi  |

Mari kita bahas satu per satu!

---

## 1️⃣ Resources (Sumber Daya)

### Apa itu Resource?

**Resource** adalah fitur untuk mengelola data dalam database. Ini yang paling sering dipakai!

### Analoginya:

Bayangkan kamu punya **buku catatan** untuk mencatat data. Resource adalah **halaman-halaman** di buku itu - ada halaman daftar, halaman tambah baru, halaman edit.

### Apa yang Dibuat Otomatis?

Ketika kamu membuat Resource, Filament otomatis membuat **3 halaman**:

| Halaman    | Fungsi                             | Contoh              |
| ---------- | ---------------------------------- | ------------------- |
| **List**   | Menampilkan semua data dalam tabel | Daftar semua produk |
| **Create** | Form untuk menambah data baru      | Tambah produk baru  |
| **Edit**   | Form untuk mengubah data           | Edit detail produk  |

Kamu juga bisa menambahkan halaman **View** (hanya lihat, tidak bisa edit).

### Contoh Nyata:

Jika kamu punya tabel `products` di database, Resource akan membuat:

- Halaman daftar semua produk
- Halaman form tambah produk
- Halaman form edit produk
- Menu "Products" di sidebar

### Cara Membuat Resource:

```bash
php artisan make:filament-resource Product
```

Ini akan membuat file-file di folder:

```
app/Filament/Resources/ProductResource.php
app/Filament/Resources/ProductResource/Pages/
```

📖 **Pelajari lebih lanjut:** [Resources Documentation](https://filamentphp.com/docs/5.x/resources)

---

## 2️⃣ Widgets (Widget)

### Apa itu Widget?

**Widget** adalah komponen kecil yang biasanya ditampilkan di **Dashboard** untuk menunjukkan informasi penting.

### Analoginya:

Bayangkan widget seperti **kotak informasi** di dashboard mobilmu - speedometer, indikator bensin, suhu mesin. Semuanya menampilkan info penting dalam bentuk yang mudah dibaca.

### Jenis-jenis Widget:

| Jenis      | Fungsi                 | Contoh                          |
| ---------- | ---------------------- | ------------------------------- |
| **Stats**  | Menampilkan angka      | "Total Penjualan: Rp 5.000.000" |
| **Chart**  | Menampilkan grafik     | Grafik penjualan per bulan      |
| **Table**  | Menampilkan tabel data | 5 pesanan terbaru               |
| **Custom** | Bebas sesuai kebutuhan | Apapun yang kamu mau!           |

### Widget Bawaan:

Saat pertama kali buka dashboard, ada 2 widget bawaan:

1. **Greeting Widget** - Menyapa user dan tombol logout
2. **Filament Info Widget** - Info tentang Filament

### Cara Membuat Widget:

```bash
php artisan make:filament-widget SalesChart
```

Ini akan membuat:

- File PHP: `app/Filament/Widgets/SalesChart.php`
- File Blade: `resources/views/filament/widgets/sales-chart.blade.php`

### Fakta Menarik:

Setiap widget adalah **Livewire component**, jadi bisa:

- Update data secara real-time
- Merespons interaksi user
- Refresh tanpa reload halaman

📖 **Pelajari lebih lanjut:** [Widgets Documentation](https://filamentphp.com/docs/5.x/widgets)

---

## 3️⃣ Custom Pages (Halaman Kustom)

### Apa itu Custom Page?

**Custom Page** adalah halaman kosong yang bisa kamu isi dengan apapun yang kamu mau. Tidak terikat dengan database tertentu.

### Analoginya:

Jika Resource adalah **halaman buku catatan** yang sudah ada kolomnya, Custom Page adalah **kertas kosong** - kamu bebas menggambar atau menulis apapun!

### Kapan Pakai Custom Page?

- Halaman **Pengaturan** (Settings)
- Halaman **Dokumentasi** internal
- Halaman **Dashboard custom**
- Halaman **Import/Export** data
- Halaman **Laporan** khusus

### Cara Membuat Custom Page:

```bash
php artisan make:filament-page Settings
```

Ini akan membuat:

- File PHP: `app/Filament/Pages/Settings.php`
- File Blade: `resources/views/filament/pages/settings.blade.php`

### Fakta Menarik:

Sama seperti widget, setiap custom page juga adalah **Livewire component**. Jadi kamu bisa:

- Membuat form interaktif
- Handle klik tombol
- Menampilkan data dinamis

📖 **Pelajari lebih lanjut:** [Custom Pages Documentation](https://filamentphp.com/docs/5.x/navigation/custom-pages)

---

## 🗺️ Peta Perjalanan Belajar

Setelah memahami 3 hal utama ini, kamu bisa mulai belajar lebih dalam:

```
┌────────────────────────────────────────────────────────┐
│                    MULAI DI SINI                       │
│                         ↓                              │
│        ┌─────────────────────────────────┐            │
│        │       Resources (CRUD)          │            │
│        │   Buat halaman kelola data      │            │
│        └─────────────────────────────────┘            │
│                         ↓                              │
│        ┌─────────────────────────────────┐            │
│        │         Widgets                  │            │
│        │   Tambah widget di dashboard    │            │
│        └─────────────────────────────────┘            │
│                         ↓                              │
│        ┌─────────────────────────────────┐            │
│        │       Custom Pages              │            │
│        │   Buat halaman sesuai kebutuhan │            │
│        └─────────────────────────────────┘            │
│                         ↓                              │
│                   APLIKASI JADI! 🎉                    │
└────────────────────────────────────────────────────────┘
```

---

## 💡 Ringkasan

| Komponen    | Perintah Buat            | Kapan Dipakai        |
| ----------- | ------------------------ | -------------------- |
| Resource    | `make:filament-resource` | Kelola data database |
| Widget      | `make:filament-widget`   | Tampilkan statistik  |
| Custom Page | `make:filament-page`     | Halaman bebas        |

---

## 🎯 Latihan Mandiri

1. **Buka dashboard** - Kunjungi `/admin` dan login
2. **Lihat widget bawaan** - Perhatikan 2 widget yang sudah ada
3. **Coba buat Resource** pertamamu:
   ```bash
   php artisan make:filament-resource Product
   ```
4. **Refresh halaman admin** - Lihat menu baru di sidebar!

<details>
<summary>Belum Punya Model Product?</summary>

Buat dulu model dan migration-nya:

```bash
php artisan make:model Product -m
```

Edit migration di `database/migrations/xxx_create_products_table.php`:

```php
Schema::create('products', function (Blueprint $table) {
    $table->id();
    $table->string('name');
    $table->text('description')->nullable();
    $table->decimal('price', 10, 2);
    $table->timestamps();
});
```

Jalankan migration:

```bash
php artisan migrate
```

Baru setelah itu buat resource-nya!

</details>

---

## ➡️ Langkah Selanjutnya

Setelah memahami dasar ini, lanjut ke dokumentasi:

- **Resources** - Untuk belajar cara membuat dan mengkustomisasi resource
- **Forms** - Untuk belajar membuat form input
- **Tables** - Untuk belajar membuat tabel data

Selamat belajar! 🎉
