# IV. Image Entry 🖼️

> **Sumber:** [https://filamentphp.com/docs/5.x/infolists/image-entry](https://filamentphp.com/docs/5.x/infolists/image-entry)

---

## 🤔 Apa itu ImageEntry?

**ImageEntry** menampilkan gambar dari path yang disimpan di database.

```php
use Filament\Infolists\Components\ImageEntry;

ImageEntry::make('avatar')
```

---

## 💾 Storage Disk

```php
ImageEntry::make('document')
    ->disk('s3')
```

---

## 📏 Size

```php
ImageEntry::make('photo')
    ->width(100)
    ->height(100)
```

### Square

```php
ImageEntry::make('thumbnail')
    ->square()
    ->size(80)
```

---

## ⭕ Circular

```php
ImageEntry::make('avatar')
    ->circular()
```

---

## 🔗 Default Image

```php
ImageEntry::make('avatar')
    ->defaultImageUrl('/images/default-avatar.png')
```

---

## 📋 Stacking (Multiple Images)

```php
ImageEntry::make('gallery')
    ->stacked()
    ->limit(3)
```

### Ring Width & Overlap

```php
ImageEntry::make('team_members.avatar')
    ->stacked()
    ->ring(4)
    ->overlap(4)
```

---

## 🔢 Limit dengan Counter

```php
ImageEntry::make('photos')
    ->stacked()
    ->limit(3)
    ->limitedRemainingText()  // "+5 more"
```

---

## 💡 Contoh Penggunaan

```php
// Avatar dengan fallback
ImageEntry::make('avatar')
    ->circular()
    ->size(60)
    ->defaultImageUrl(fn ($record) =>
        'https://ui-avatars.com/api/?name=' . urlencode($record->name)
    )

// Gallery produk
ImageEntry::make('images')
    ->stacked()
    ->limit(4)
    ->limitedRemainingText()
    ->square()
    ->size(80)
```

---

## 🎯 Latihan Mandiri

Buat ImageEntry untuk:

- `avatar` circular dengan default
- `gallery` stacked limit 3
- `logo` square 100px
