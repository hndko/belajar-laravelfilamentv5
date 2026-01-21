# V. Color Entry 🎨

> **Sumber:** [https://filamentphp.com/docs/5.x/infolists/color-entry](https://filamentphp.com/docs/5.x/infolists/color-entry)

---

## 🤔 Apa itu ColorEntry?

**ColorEntry** menampilkan kotak warna berdasarkan nilai HEX atau RGB di database.

```php
use Filament\Infolists\Components\ColorEntry;

ColorEntry::make('color')
```

---

## 📋 Copyable

```php
ColorEntry::make('brand_color')
    ->copyable()
    ->copyMessage('Warna berhasil disalin!')
```

---

## 💡 Contoh Penggunaan

```php
// Brand color
ColorEntry::make('primary_color')
    ->label('Warna Utama')
    ->copyable()

// Category color
ColorEntry::make('category.color')
    ->label('Warna Kategori')

// Multiple colors
ColorEntry::make('palette')
    ->label('Palet Warna')
```

---

## 🎯 Latihan Mandiri

Buat infolist dengan:

- `primary_color` copyable
- `secondary_color` copyable
- `category.color` dari relasi
