# III. Colors 🌈

> **Sumber:** [https://filamentphp.com/docs/5.x/styling/colors](https://filamentphp.com/docs/5.x/styling/colors)

---

## 🤔 Tentang Colors

Filament menggunakan sistem warna berbasis Tailwind CSS dengan beberapa warna default.

---

## 🎨 Default Colors

| Color     | Penggunaan         |
| --------- | ------------------ |
| `primary` | Tombol utama, link |
| `danger`  | Error, delete      |
| `gray`    | Background, border |
| `info`    | Informasi          |
| `success` | Sukses, aktif      |
| `warning` | Peringatan         |

---

## 📝 Passing Color

```php
// String color name
TextColumn::make('status')
    ->color('success')

// Closure untuk dynamic color
TextColumn::make('status')
    ->color(fn ($state) => match ($state) {
        'active' => 'success',
        'pending' => 'warning',
        'rejected' => 'danger',
    })
```

---

## 🎨 Customizing Default Colors

```php
use Filament\Support\Colors\Color;

$panel->colors([
    'primary' => Color::Indigo,
    'danger' => Color::Red,
    'success' => Color::Green,
    'warning' => Color::Amber,
    'info' => Color::Sky,
])
```

---

## ➕ Registering Extra Colors

```php
$panel->colors([
    'primary' => Color::Indigo,
    'secondary' => Color::Slate,
    'accent' => Color::Fuchsia,
])
```

### Menggunakan Extra Color

```php
TextColumn::make('category')
    ->color('accent')
```

---

## 🎨 Non-Tailwind Colors

### Dari HEX

```php
$panel->colors([
    'primary' => Color::hex('#6366f1'),
])
```

### Dari RGB

```php
$panel->colors([
    'primary' => Color::rgb('rgb(99, 102, 241)'),
])
```

### Generating Full Palette

```php
use Filament\Support\Colors\Color;

$panel->colors([
    'primary' => [
        50 => '#f0f9ff',
        100 => '#e0f2fe',
        200 => '#bae6fd',
        // ... sampai 950
    ],
])
```

---

## 🎯 Latihan Mandiri

Konfigurasi warna:

- Primary dari brand color HEX
- Tambah warna 'secondary'
- Custom danger color
