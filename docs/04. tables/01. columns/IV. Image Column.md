# V. Image Column 🖼️

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/columns/image](https://filamentphp.com/docs/5.x/tables/columns/image)

---

## 🤔 Apa itu ImageColumn?

**ImageColumn** menampilkan gambar dari path yang disimpan di database.

```php
use Filament\Tables\Columns\ImageColumn;

ImageColumn::make('avatar')
```

---

## 💾 Storage Disk

Default menggunakan disk `public`. Untuk disk lain:

```php
ImageColumn::make('document')
    ->disk('s3')
```

---

## 📏 Ukuran

```php
ImageColumn::make('avatar')
    ->width(100)
    ->height(100)
```

### Square (Kotak)

```php
ImageColumn::make('avatar')
    ->square()
    ->size(50)
```

---

## ⭕ Circular (Bulat)

Cocok untuk avatar:

```php
ImageColumn::make('avatar')
    ->circular()
```

---

## 🔗 Default Image

Jika gambar tidak ada:

```php
ImageColumn::make('avatar')
    ->defaultImageUrl('/images/default-avatar.png')
```

---

## 📋 Stacking (Multiple Images)

Untuk array gambar:

```php
ImageColumn::make('gallery')
    ->stacked()
    ->limit(3)
```

### Ring Width

```php
ImageColumn::make('team.members.avatar')
    ->stacked()
    ->ring(4)  // Border width
```

### Overlap

```php
ImageColumn::make('gallery')
    ->stacked()
    ->overlap(4)  // Overlap size
```

---

## 🔢 Limit dengan Counter

```php
ImageColumn::make('photos')
    ->stacked()
    ->limit(3)
    ->limitedRemainingText()  // "+5 more"
```

---

## 🎨 Extra Attributes

```php
ImageColumn::make('banner')
    ->extraImgAttributes(['loading' => 'lazy'])
```

---

## 💡 Contoh Penggunaan

### Avatar User

```php
ImageColumn::make('avatar')
    ->circular()
    ->size(40)
    ->defaultImageUrl(fn ($record) =>
        'https://ui-avatars.com/api/?name=' . urlencode($record->name)
    )
```

### Product Gallery

```php
ImageColumn::make('images')
    ->stacked()
    ->limit(4)
    ->limitedRemainingText()
    ->square()
    ->size(60)
```

---

## 🎯 Latihan Mandiri

1. Buat ImageColumn untuk `profile_photo` yang circular
2. Buat ImageColumn untuk `product_images` yang stacked
