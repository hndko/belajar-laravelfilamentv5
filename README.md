<p align="center">
  <img src="https://raw.githubusercontent.com/filamentphp/filament/3.x/art/logo.svg" alt="Filament Logo" width="200">
</p>

<h1 align="center">📚 Dokumentasi Filament v5 - Bahasa Indonesia</h1>

<p align="center">
  <strong>Dokumentasi lengkap Laravel Filament v5 dalam Bahasa Indonesia yang mudah dipahami</strong>
</p>

<p align="center">
  <a href="#-tentang-project">Tentang</a> •
  <a href="#-fitur">Fitur</a> •
  <a href="#-daftar-isi">Daftar Isi</a> •
  <a href="#-cara-penggunaan">Penggunaan</a> •
  <a href="#-kontribusi">Kontribusi</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Filament-v5.x-orange?style=for-the-badge&logo=laravel" alt="Filament v5">
  <img src="https://img.shields.io/badge/Laravel-11.x-red?style=for-the-badge&logo=laravel" alt="Laravel 11">
  <img src="https://img.shields.io/badge/Bahasa-Indonesia-blue?style=for-the-badge" alt="Bahasa Indonesia">
  <img src="https://img.shields.io/badge/Docs-153%2B%20Files-green?style=for-the-badge" alt="153+ Files">
</p>

---

## 🎯 Tentang Project

Project ini adalah **dokumentasi lengkap Laravel Filament v5** yang ditulis dalam **Bahasa Indonesia** dengan penjelasan sederhana dan contoh kode yang mudah dipahami. Cocok untuk developer Indonesia yang ingin belajar Filament dari dasar hingga mahir.

### Mengapa Project Ini?

- 📖 **Bahasa Indonesia** - Dokumentasi resmi dalam Bahasa Inggris, ini memudahkan developer Indonesia
- 🎯 **Simpel & To The Point** - Penjelasan ringkas dengan contoh langsung
- 💻 **Praktis** - Setiap topik dilengkapi contoh kode yang bisa langsung dipakai
- 📝 **Latihan Mandiri** - Setiap bagian ada latihan untuk mengasah pemahaman

---

## ✨ Fitur

| Fitur                        | Keterangan                       |
| ---------------------------- | -------------------------------- |
| 📚 **153+ File Dokumentasi** | Mencakup semua fitur Filament v5 |
| 🇮🇩 **Full Bahasa Indonesia** | Mudah dipahami developer lokal   |
| 💡 **Contoh Kode Lengkap**   | Copy-paste ready                 |
| 🎯 **Terstruktur Rapi**      | 20 section terorganisir          |
| 🔄 **Up-to-date**            | Mengikuti Filament v5 terbaru    |

---

## 📖 Daftar Isi

<table>
<tr>
<td width="50%" valign="top">

### 🚀 Getting Started

- [01. Introduction](docs/01.%20introduction/) (7 file)
- [02. Getting Started](docs/02.%20getting-started/) (1 file)

### 📦 Core Features

- [03. Resources](docs/03.%20resources/) (13 file)
- [04. Tables](docs/04.%20tables/) (23+ file)
- [05. Schemas](docs/05.%20schemas/) (8 file)
- [06. Forms](docs/06.%20forms/) (23 file)
- [07. Infolists](docs/07.%20infolists/) (9 file)
- [08. Actions](docs/08.%20actions/) (12 file)

### 🔔 UI Components

- [09. Notifications](docs/09.%20notifications/) (3 file)
- [10. Widgets](docs/10.%20widgets/) (3 file)

</td>
<td width="50%" valign="top">

### ⚙️ Configuration

- [11. Panel Configuration](docs/11.%20panel-configuration/) (1 file)
- [12. Navigation](docs/12.%20navigation/) (4 file)
- [13. Users](docs/13.%20users/) (3 file)
- [14. Styling](docs/14.%20styling/) (4 file)

### 🔧 Advanced

- [15. Advanced](docs/15.%20advanced/) (5 file)
- [16. Testing](docs/16.%20testing/) (6 file)
- [17. Plugins](docs/17.%20plugins/) (4 file)
- [18. Components](docs/18.%20components/) (26 file)

### 🚀 Production

- [19. Deployment](docs/19.%20deployment/) (1 file)
- [20. Upgrade Guide](docs/20.%20upgrade-guide/) (1 file)

</td>
</tr>
</table>

---

## 🚀 Cara Penggunaan

### Browse Online

Buka folder `docs/` dan pilih topik yang ingin dipelajari.

### Clone Repository

```bash
git clone https://github.com/hndko/belajar-laravelfilamentv5.git
cd belajar-laravelfilamentv5
```

### Struktur Folder

```
docs/
├── 01. introduction/      # Pengenalan Filament
├── 02. getting-started/   # Instalasi & Setup
├── 03. resources/         # CRUD Resources
├── 04. tables/            # Data Tables
├── 05. schemas/           # Layout Components
├── 06. forms/             # Form Fields
├── 07. infolists/         # Read-only Data
├── 08. actions/           # Buttons & Modals
├── 09. notifications/     # Toast Alerts
├── 10. widgets/           # Dashboard Widgets
├── ...
└── 20. upgrade-guide/     # Upgrade v4 ke v5
```

---

## 📝 Contoh Dokumentasi

### Membuat Resource

```php
php artisan make:filament-resource Product
```

### Table dengan Filter

```php
public static function table(Table $table): Table
{
    return $table
        ->columns([
            TextColumn::make('name')->searchable(),
            TextColumn::make('price')->money('IDR'),
            BadgeColumn::make('status')->colors([
                'success' => 'active',
                'danger' => 'inactive',
            ]),
        ])
        ->filters([
            SelectFilter::make('status')
                ->options([
                    'active' => 'Aktif',
                    'inactive' => 'Nonaktif',
                ]),
        ]);
}
```

---

## 👨‍💻 Author

<p align="center">
  <img src="https://github.com/hndko.png" width="100" style="border-radius: 50%">
</p>

<p align="center">
  <strong>Handoko</strong><br>
  Full Stack Developer
</p>

<p align="center">
  <a href="https://github.com/hndko">
    <img src="https://img.shields.io/badge/GitHub-hndko-black?style=flat-square&logo=github" alt="GitHub">
  </a>
</p>

---

## 🤝 Kontribusi

Kontribusi sangat diterima! Silakan:

1. Fork repository ini
2. Buat branch baru (`git checkout -b feature/tambah-docs`)
3. Commit perubahan (`git commit -m 'Tambah dokumentasi XYZ'`)
4. Push ke branch (`git push origin feature/tambah-docs`)
5. Buat Pull Request

---

## 📄 Lisensi

Project ini menggunakan lisensi [MIT](LICENSE). Silakan gunakan untuk belajar dan project Anda.

---

## ⭐ Support

Jika dokumentasi ini membantu, berikan ⭐ star di repository ini!

<p align="center">
  <strong>Happy Coding! 🚀</strong>
</p>
