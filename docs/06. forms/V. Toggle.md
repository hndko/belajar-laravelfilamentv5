# V. Toggle 🔘

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/toggle](https://filamentphp.com/docs/5.x/forms/toggle)

---

## 🤔 Apa itu Toggle?

**Toggle** adalah switch on/off untuk nilai boolean. Tampilan lebih modern dari checkbox.

```php
use Filament\Forms\Components\Toggle;

Toggle::make('is_active')
```

---

## 🎯 Icon

```php
Toggle::make('is_visible')
    ->onIcon('heroicon-o-eye')
    ->offIcon('heroicon-o-eye-slash')
```

---

## 🎨 Warna

```php
Toggle::make('is_admin')
    ->onColor('success')
    ->offColor('danger')
```

---

## 🏷️ Label Position

```php
Toggle::make('notifications')
    ->label('Aktifkan notifikasi')
    ->labelAbove()
```

---

## ✅ Validasi

### Accepted

```php
Toggle::make('agree')
    ->accepted()  // Harus on
```

### Declined

```php
Toggle::make('disable')
    ->declined()  // Harus off
```

---

## 💡 Contoh Penggunaan

```php
Toggle::make('is_published')
    ->label('Publish')
    ->onIcon('heroicon-o-check')
    ->offIcon('heroicon-o-x-mark')
    ->onColor('success')
    ->default(false)

Toggle::make('maintenance_mode')
    ->label('Mode Maintenance')
    ->onColor('warning')
    ->helperText('Aktifkan untuk menutup website sementara')
```

---

## 🎯 Latihan Mandiri

Buat Toggle untuk:

- `is_published` dengan icon check/x
- `is_featured` dengan warna success
- `maintenance_mode` dengan warning color
