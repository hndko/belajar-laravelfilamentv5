# IV. Icons 🎯

> **Sumber:** [https://filamentphp.com/docs/5.x/styling/icons](https://filamentphp.com/docs/5.x/styling/icons)

---

## 🤔 Tentang Icons

Filament menggunakan **Heroicons** sebagai icon set default.

---

## 🎯 Using Heroicons

```php
// Outline style
->icon('heroicon-o-user')

// Solid style
->icon('heroicon-s-user')

// Mini style
->icon('heroicon-m-user')

// Micro style
->icon('heroicon-c-user')
```

---

## 📦 Using Other Icon Sets

Install Blade Icons package:

```bash
composer require blade-ui-kit/blade-icons
```

### Contoh: Font Awesome

```bash
composer require owenvoke/blade-fontawesome
```

```php
->icon('fa-solid-user')
```

### Contoh: Tabler Icons

```bash
composer require ryangjchandler/blade-tabler-icons
```

```php
->icon('tabler-user')
```

---

## 📁 Custom SVG Icons

1. Buat folder untuk icons:

```
resources/svg/
└── custom-icon.svg
```

2. Register di `config/blade-icons.php`:

```php
'sets' => [
    'default' => [
        'path' => 'resources/svg',
        'prefix' => 'icon',
    ],
],
```

3. Gunakan:

```php
->icon('icon-custom-icon')
```

---

## 🔄 Replacing Default Icons

```php
use Filament\Support\Facades\FilamentIcon;

// Di AppServiceProvider
FilamentIcon::register([
    'panels::sidebar.collapse-button' => 'heroicon-o-chevron-left',
    'panels::sidebar.expand-button' => 'heroicon-o-chevron-right',
    'panels::topbar.open-database-notifications-button' => 'heroicon-o-bell-alert',
]);
```

---

## 📋 Icon Aliases

### Actions

- `actions::create-action` - Create button
- `actions::delete-action` - Delete button
- `actions::edit-action` - Edit button
- `actions::view-action` - View button

### Forms

- `forms::components.file-upload.remove-file-button`
- `forms::components.markdown-editor.bold`

### Tables

- `tables::columns.icon-column.false`
- `tables::columns.icon-column.true`
- `tables::filters.remove-button`

### Panels

- `panels::sidebar.collapse-button`
- `panels::topbar.open-database-notifications-button`

---

## 🎯 Latihan Mandiri

Konfigurasi icons:

- Install Font Awesome
- Custom SVG icon
- Replace sidebar collapse icon
