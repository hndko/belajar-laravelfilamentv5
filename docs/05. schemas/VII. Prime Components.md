# VII. Prime Components 🎨

> **Sumber:** [https://filamentphp.com/docs/5.x/schemas/primes](https://filamentphp.com/docs/5.x/schemas/primes)

---

## 🤔 Apa itu Prime Components?

**Prime Components** adalah komponen dasar untuk menampilkan konten statis seperti teks, ikon, dan gambar di dalam schema.

---

## 📝 Text Component

```php
use Filament\Schemas\Components\Text;

Text::make('Selamat datang di dashboard!')
```

### Warna

```php
Text::make('Perhatian!')
    ->color('danger')  // danger, warning, success, info, primary
```

### Neutral Color

```php
Text::make('Catatan')
    ->color('gray')
```

### Badge

```php
Text::make('Aktif')
    ->badge()
    ->color('success')
```

### Size

```php
Text::make('Judul Besar')
    ->size('lg')  // xs, sm, md, lg, xl
```

### Weight

```php
Text::make('Teks Tebal')
    ->weight('bold')  // thin, light, normal, medium, semibold, bold
```

### Font Family

```php
Text::make('Kode: ABC123')
    ->fontFamily('mono')
```

### Tooltip

```php
Text::make('Hover untuk info')
    ->tooltip('Ini adalah tooltip')
```

---

## 🎯 Icon Component

```php
use Filament\Schemas\Components\Icon;

Icon::make('heroicon-o-check-circle')
```

### Warna

```php
Icon::make('heroicon-o-check')
    ->color('success')
```

### Size

```php
Icon::make('heroicon-o-star')
    ->size('lg')
```

### Tooltip

```php
Icon::make('heroicon-o-information-circle')
    ->tooltip('Klik untuk info lebih lanjut')
```

---

## 🖼️ Image Component

```php
use Filament\Schemas\Components\Image;

Image::make('/images/banner.jpg')
```

### Size

```php
Image::make('/images/avatar.jpg')
    ->width(100)
    ->height(100)
```

### Alignment

```php
Image::make('/images/logo.png')
    ->alignCenter()
```

### Tooltip

```php
Image::make('/images/product.jpg')
    ->tooltip('Gambar produk')
```

---

## 📋 Unordered List

```php
use Filament\Schemas\Components\UnorderedList;

UnorderedList::make([
    'Item pertama',
    'Item kedua',
    'Item ketiga',
])
```

### Bullet Size

```php
UnorderedList::make([...])
    ->bulletSize('lg')
```

---

## 🎯 Latihan Mandiri

Buat tampilan informasi dengan:

- Text "Status: Aktif" sebagai badge hijau
- Icon check-circle
- Gambar avatar
