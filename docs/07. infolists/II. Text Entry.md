# II. Text Entry 📝

> **Sumber:** [https://filamentphp.com/docs/5.x/infolists/text-entry](https://filamentphp.com/docs/5.x/infolists/text-entry)

---

## 🤔 Apa itu TextEntry?

**TextEntry** adalah entry untuk menampilkan teks, angka, tanggal, dan data berbasis teks lainnya.

```php
use Filament\Infolists\Components\TextEntry;

TextEntry::make('name')
```

---

## 🎨 Warna

```php
TextEntry::make('status')
    ->color('success')  // danger, warning, success, info, primary
```

### Warna Dinamis

```php
TextEntry::make('status')
    ->color(fn ($state) => match ($state) {
        'active' => 'success',
        'pending' => 'warning',
        'rejected' => 'danger',
    })
```

---

## 🎯 Icon

```php
TextEntry::make('email')
    ->icon('heroicon-o-envelope')
    ->iconPosition(IconPosition::After)
```

---

## 🏷️ Badge

```php
TextEntry::make('status')
    ->badge()
    ->color(fn ($state) => match ($state) {
        'published' => 'success',
        'draft' => 'gray',
    })
```

---

## 📅 Format Tanggal

```php
TextEntry::make('created_at')
    ->dateTime()

TextEntry::make('created_at')
    ->dateTime('d M Y H:i')

TextEntry::make('birthday')
    ->date()

TextEntry::make('created_at')
    ->since()  // "3 days ago"
```

---

## 🔢 Format Angka

```php
TextEntry::make('quantity')
    ->numeric()

TextEntry::make('price')
    ->numeric(decimalPlaces: 2)
```

---

## 💰 Format Uang

```php
TextEntry::make('price')
    ->money('IDR')

TextEntry::make('total')
    ->money('USD', locale: 'en_US')
```

---

## 📋 Multiple Values (List)

```php
TextEntry::make('tags.name')
    ->listWithLineBreaks()

TextEntry::make('categories.name')
    ->bulleted()

TextEntry::make('items.name')
    ->limitList(3)
    ->expandableLimitedList()
```

---

## 📏 Text Size

```php
TextEntry::make('title')
    ->size(TextEntry\TextEntrySize::Large)

TextEntry::make('name')
    ->weight(FontWeight::Bold)

TextEntry::make('code')
    ->fontFamily(FontFamily::Mono)
```

---

## ✂️ Text Panjang

```php
TextEntry::make('description')
    ->limit(50)
    ->tooltip(fn ($record) => $record->description)

TextEntry::make('content')
    ->words(10)

TextEntry::make('bio')
    ->lineClamp(3)
```

---

## 📋 Copyable

```php
TextEntry::make('api_key')
    ->copyable()
    ->copyMessage('Berhasil disalin!')
```

---

## 🎯 Latihan Mandiri

Buat infolist dengan:

- `name` bold
- `status` badge berwarna
- `price` format money IDR
- `created_at` format since
