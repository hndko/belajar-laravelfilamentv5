# V. Melihat Detail Data (Viewing Records) 👁️

> **Sumber:** [https://filamentphp.com/docs/5.x/resources/viewing-records](https://filamentphp.com/docs/5.x/resources/viewing-records)

---

## 🤔 Apa itu View Page?

**View Page** adalah halaman untuk menampilkan detail data secara **read-only** (hanya baca, tidak bisa diedit).

### Kapan Pakai View Page?

- Menampilkan detail lengkap record
- Halaman yang tidak boleh diedit oleh user tertentu
- Preview sebelum mengedit

---

## 🚀 Membuat Resource dengan View Page

Saat membuat resource baru:

```bash
php artisan make:filament-resource User --view
```

---

## ➕ Menambah View Page ke Resource yang Sudah Ada

### Langkah 1: Buat Page

```bash
php artisan make:filament-page ViewUser --resource=UserResource --type=ViewRecord
```

### Langkah 2: Daftarkan di Resource

```php
// UserResource.php
public static function getPages(): array
{
    return [
        'index' => Pages\ListUsers::route('/'),
        'create' => Pages\CreateUser::route('/create'),
        'view' => Pages\ViewUser::route('/{record}'),
        'edit' => Pages\EditUser::route('/{record}/edit'),
    ];
}
```

---

## 📋 Menggunakan Infolist

Secara default, View page menampilkan form yang di-disable. Tapi kamu bisa pakai **Infolist** yang lebih bagus:

```php
// Di UserResource.php
use Filament\Infolists;
use Filament\Schemas\Schema;

public static function infolist(Schema $schema): Schema
{
    return $schema
        ->components([
            Infolists\Components\TextEntry::make('name'),
            Infolists\Components\TextEntry::make('email'),
            Infolists\Components\TextEntry::make('notes')
                ->columnSpanFull(),
        ]);
}
```

### Komponen Infolist yang Tersedia:

| Komponen        | Fungsi                 |
| --------------- | ---------------------- |
| `TextEntry`     | Teks biasa             |
| `IconEntry`     | Ikon (misal: ✓ atau ✗) |
| `ImageEntry`    | Gambar                 |
| `ColorEntry`    | Warna                  |
| `KeyValueEntry` | Pasangan kunci-nilai   |

---

## 💬 View dalam Modal

Untuk resource sederhana, kamu bisa tampilkan detail dalam modal (popup) tanpa halaman terpisah:

```php
use Filament\Actions\ViewAction;

public static function table(Table $table): Table
{
    return $table
        ->columns([
            // ...
        ])
        ->recordActions([
            ViewAction::make(),
        ]);
}
```

---

## 🔒 Authorization

View page menggunakan method `view()` dari Policy:

```php
public function view(User $user, Customer $customer): bool
{
    return $user->id === $customer->user_id;
}
```

---

## 💡 Perbedaan Form vs Infolist

| Fitur         | Form (disabled)            | Infolist           |
| ------------- | -------------------------- | ------------------ |
| Tampilan      | Field form yang di-disable | Tampilan teks rapi |
| Customization | Terbatas                   | Sangat fleksibel   |
| Performance   | Lebih berat                | Lebih ringan       |
| Rekomendasi   | Cepat dipakai              | Lebih profesional  |

---

## 🎯 Latihan Mandiri

1. Buat View page untuk resource Product
2. Gunakan Infolist dengan TextEntry untuk name, price, dan description

<details>
<summary>Jawaban</summary>

```php
// ProductResource.php
public static function infolist(Schema $schema): Schema
{
    return $schema
        ->components([
            Infolists\Components\TextEntry::make('name')
                ->label('Nama Produk'),
            Infolists\Components\TextEntry::make('price')
                ->label('Harga')
                ->money('IDR'),
            Infolists\Components\TextEntry::make('description')
                ->label('Deskripsi')
                ->columnSpanFull(),
        ]);
}
```

</details>
