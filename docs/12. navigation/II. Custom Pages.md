# II. Custom Pages 📄

> **Sumber:** [https://filamentphp.com/docs/5.x/navigation/custom-pages](https://filamentphp.com/docs/5.x/navigation/custom-pages)

---

## 🤔 Apa itu Custom Pages?

**Custom Pages** adalah halaman panel yang dibuat manual, bukan dari Resource.

---

## 🚀 Membuat Page

```bash
php artisan make:filament-page Settings
```

---

## 📍 Navigation

```php
protected static ?string $navigationIcon = 'heroicon-o-cog';
protected static ?string $navigationLabel = 'Pengaturan';
protected static ?string $navigationGroup = 'System';
protected static ?int $navigationSort = 100;
```

---

## 🔒 Authorization

```php
public static function canAccess(): bool
{
    return auth()->user()->isAdmin();
}
```

---

## ⚡ Header Actions

```php
protected function getHeaderActions(): array
{
    return [
        Action::make('save')
            ->label('Simpan')
            ->action('save'),
    ];
}

public function save(): void
{
    // Save logic
}
```

---

## 📊 Widgets

```php
protected function getHeaderWidgets(): array
{
    return [
        StatsOverviewWidget::class,
    ];
}

protected function getFooterWidgets(): array
{
    return [
        ChartWidget::class,
    ];
}
```

### Widget Grid

```php
public function getHeaderWidgetsColumns(): int | array
{
    return 3;
}
```

---

## 🏷️ Page Title

```php
protected static ?string $title = 'Pengaturan Sistem';
protected ?string $heading = 'Pengaturan';
protected ?string $subheading = 'Kelola pengaturan aplikasi';
```

---

## 📍 Custom URL

```php
protected static ?string $slug = 'system-settings';

// URL: /admin/system-settings
```

---

## 📏 Content Width

```php
public function getMaxContentWidth(): MaxWidth
{
    return MaxWidth::Full;
}
```

---

## 🔗 Generate URL

```php
// Di Blade atau PHP lain
$url = Settings::getUrl();

// Dengan parameter
$url = Settings::getUrl(['tab' => 'general']);
```

---

## 🎯 Latihan Mandiri

Buat custom page untuk:

- Settings dengan form dan save action
- Reports dengan widgets
- Help page dengan konten statis
