# III. Icon Entry 🎯

> **Sumber:** [https://filamentphp.com/docs/5.x/infolists/icon-entry](https://filamentphp.com/docs/5.x/infolists/icon-entry)

---

## 🤔 Apa itu IconEntry?

**IconEntry** menampilkan ikon berdasarkan nilai data. Cocok untuk boolean, status, atau kategori.

```php
use Filament\Infolists\Components\IconEntry;

IconEntry::make('status')
    ->icon(fn ($state) => match ($state) {
        'pending' => 'heroicon-o-clock',
        'approved' => 'heroicon-o-check-circle',
        'rejected' => 'heroicon-o-x-circle',
    })
```

---

## 🎨 Warna

```php
IconEntry::make('priority')
    ->icon('heroicon-o-flag')
    ->color(fn ($state) => match ($state) {
        'low' => 'gray',
        'medium' => 'warning',
        'high' => 'danger',
    })
```

---

## 📏 Size

```php
IconEntry::make('status')
    ->icon('heroicon-o-star')
    ->size(IconEntry\IconEntrySize::Large)
```

---

## ✅ Boolean

```php
IconEntry::make('is_active')
    ->boolean()
```

### Custom Boolean Icons

```php
IconEntry::make('is_visible')
    ->boolean()
    ->trueIcon('heroicon-o-eye')
    ->falseIcon('heroicon-o-eye-slash')
```

### Custom Boolean Colors

```php
IconEntry::make('is_verified')
    ->boolean()
    ->trueColor('success')
    ->falseColor('danger')
```

---

## 💡 Contoh Penggunaan

```php
// Status Pesanan
IconEntry::make('order_status')
    ->icon(fn ($state) => match ($state) {
        'pending' => 'heroicon-o-clock',
        'processing' => 'heroicon-o-arrow-path',
        'shipped' => 'heroicon-o-truck',
        'delivered' => 'heroicon-o-check-badge',
    })
    ->color(fn ($state) => match ($state) {
        'pending' => 'warning',
        'processing' => 'info',
        'shipped' => 'primary',
        'delivered' => 'success',
    })
```

---

## 🎯 Latihan Mandiri

Buat IconEntry untuk:

- `is_active` boolean
- `priority` dengan 3 level (low/medium/high)
- `payment_status` dengan icon berbeda
