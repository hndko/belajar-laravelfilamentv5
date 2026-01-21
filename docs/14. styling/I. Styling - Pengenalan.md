# I. Styling - Pengenalan 🎨

> **Sumber:** [https://filamentphp.com/docs/5.x/styling/overview](https://filamentphp.com/docs/5.x/styling/overview)

---

## 🤔 Tentang Styling

Filament menyediakan berbagai cara untuk mengkustomisasi tampilan panel.

---

## 🎨 Mengubah Warna

```php
use Filament\Support\Colors\Color;

$panel->colors([
    'primary' => Color::Amber,
    'danger' => Color::Rose,
    'gray' => Color::Zinc,
    'info' => Color::Blue,
    'success' => Color::Emerald,
    'warning' => Color::Orange,
])
```

### Custom Color dari HEX

```php
$panel->colors([
    'primary' => Color::hex('#FF5722'),
])
```

---

## 🔤 Mengubah Font

```php
$panel->font('Poppins')
```

### Font Provider

```php
use Filament\FontProviders\LocalFontProvider;

$panel->font('Inter', provider: LocalFontProvider::class)
```

---

## 🎨 Custom Theme

```bash
php artisan make:filament-theme
```

### Files yang Dibuat:

```
resources/css/filament/admin/theme.css
resources/css/filament/admin/tailwind.config.js
```

### Register Theme

```php
$panel->viteTheme('resources/css/filament/admin/theme.css')
```

---

## 🌙 Dark Mode

### Disable Dark Mode

```php
$panel->darkMode(false)
```

### Default Theme Mode

```php
$panel->defaultThemeMode(ThemeMode::Dark)

// ThemeMode::Light
// ThemeMode::Dark
// ThemeMode::System
```

---

## 🖼️ Logo

```php
$panel->brandLogo(asset('images/logo.svg'))
    ->brandLogoHeight('2rem')
```

### Dark Mode Logo

```php
$panel->darkModeBrandLogo(asset('images/logo-dark.svg'))
```

---

## 🔖 Favicon

```php
$panel->favicon(asset('images/favicon.ico'))
```

---

## 🎯 Latihan Mandiri

Kustomisasi styling dengan:

- Warna primary custom
- Font Poppins
- Logo brand
- Default dark mode
