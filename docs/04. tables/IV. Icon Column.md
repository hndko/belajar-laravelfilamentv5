# IV. Icon Column 🎯

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/columns/icon](https://filamentphp.com/docs/5.x/tables/columns/icon)

---

## 🤔 Apa itu IconColumn?

**IconColumn** menampilkan ikon berdasarkan nilai data. Cocok untuk boolean, status, atau kategori.

```php
use Filament\Tables\Columns\IconColumn;

IconColumn::make('is_featured')
    ->boolean()
```

---

## 🎨 Warna

```php
IconColumn::make('status')
    ->icon('heroicon-o-check-circle')
    ->color('success')
```

### Warna Dinamis

```php
IconColumn::make('priority')
    ->icon(fn ($state) => match ($state) {
        'low' => 'heroicon-o-arrow-down',
        'medium' => 'heroicon-o-minus',
        'high' => 'heroicon-o-arrow-up',
    })
    ->color(fn ($state) => match ($state) {
        'low' => 'gray',
        'medium' => 'warning',
        'high' => 'danger',
    })
```

---

## 📏 Ukuran

```php
IconColumn::make('is_active')
    ->boolean()
    ->size(IconColumn\IconColumnSize::Large)
```

---

## ✅ Boolean Mode

Otomatis tampilkan ✓ atau ✗:

```php
IconColumn::make('is_active')
    ->boolean()
```

### Custom Icon Boolean

```php
IconColumn::make('is_visible')
    ->boolean()
    ->trueIcon('heroicon-o-eye')
    ->falseIcon('heroicon-o-eye-slash')
```

### Custom Color Boolean

```php
IconColumn::make('is_enabled')
    ->boolean()
    ->trueColor('success')
    ->falseColor('danger')
```

---

## 📋 Multiple Icons

Untuk array values:

```php
IconColumn::make('technologies')
    ->icons([
        'heroicon-o-cpu-chip' => 'ai',
        'heroicon-o-cloud' => 'cloud',
        'heroicon-o-device-phone-mobile' => 'mobile',
    ])
    ->wrap()  // Wrap ke baris berikutnya
```

---

## 💡 Contoh Penggunaan

### Status Pesanan

```php
IconColumn::make('status')
    ->icon(fn ($state) => match ($state) {
        'pending' => 'heroicon-o-clock',
        'processing' => 'heroicon-o-arrow-path',
        'shipped' => 'heroicon-o-truck',
        'delivered' => 'heroicon-o-check-badge',
        'cancelled' => 'heroicon-o-x-circle',
    })
    ->color(fn ($state) => match ($state) {
        'pending' => 'warning',
        'processing' => 'info',
        'shipped' => 'primary',
        'delivered' => 'success',
        'cancelled' => 'danger',
    })
```

### Rating Bintang

```php
IconColumn::make('rating')
    ->icon('heroicon-s-star')
    ->color('warning')
```

---

## 🎯 Latihan Mandiri

Buat IconColumn untuk:

- `is_verified` (boolean dengan ikon shield)
- `priority` (low/medium/high dengan ikon panah)
