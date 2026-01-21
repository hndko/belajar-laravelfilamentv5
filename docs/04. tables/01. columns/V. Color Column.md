# VI. Color Column 🎨

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/columns/color](https://filamentphp.com/docs/5.x/tables/columns/color)

---

## 🤔 Apa itu ColorColumn?

**ColorColumn** menampilkan kotak warna berdasarkan nilai HEX atau RGB di database.

```php
use Filament\Tables\Columns\ColorColumn;

ColorColumn::make('color')
```

---

## 📋 Copy to Clipboard

```php
ColorColumn::make('brand_color')
    ->copyable()
    ->copyMessage('Warna berhasil disalin!')
```

---

## 📋 Multiple Colors

Untuk array warna:

```php
ColorColumn::make('palette')
    ->wrap()  // Wrap ke baris berikutnya jika banyak
```

---

## 💡 Contoh Penggunaan

### Brand Colors

```php
ColorColumn::make('primary_color')
    ->copyable()
    ->label('Warna Utama')
```

### Category Colors

```php
ColorColumn::make('category.color')
    ->label('Warna Kategori')
```

---

## 🎯 Latihan Mandiri

Buat tabel Category dengan ColorColumn untuk field `color`.
