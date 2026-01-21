# XII. Export Action 📤

> **Sumber:** [https://filamentphp.com/docs/5.x/actions/export](https://filamentphp.com/docs/5.x/actions/export)

---

## 🤔 Apa itu ExportAction?

**ExportAction** mengexport data ke file CSV atau XLSX.

```php
use Filament\Actions\ExportAction;

ExportAction::make()
    ->exporter(UserExporter::class)
```

---

## 🚀 Membuat Exporter

```bash
php artisan make:filament-exporter User
```

### File yang Dibuat:

```
app/Filament/Exports/UserExporter.php
```

---

## 📋 Defining Columns

```php
// app/Filament/Exports/UserExporter.php

use Filament\Actions\Exports\ExportColumn;
use Filament\Actions\Exports\Exporter;

class UserExporter extends Exporter
{
    protected static ?string $model = User::class;

    public static function getColumns(): array
    {
        return [
            ExportColumn::make('id'),
            ExportColumn::make('name'),
            ExportColumn::make('email'),
            ExportColumn::make('created_at'),
        ];
    }
}
```

---

## 🏷️ Column Label

```php
ExportColumn::make('name')
    ->label('Nama Lengkap')
```

---

## ☑️ Default Selection

```php
ExportColumn::make('phone')
    ->enabledByDefault(false)  // Tidak dicentang by default
```

---

## 🔧 Calculated State

```php
ExportColumn::make('full_address')
    ->state(fn ($record) => "{$record->street}, {$record->city}")
```

---

## 🎨 Formatting

```php
ExportColumn::make('price')
    ->formatStateUsing(fn ($state) => 'Rp ' . number_format($state))
```

---

## 🔗 Relationships

```php
ExportColumn::make('category.name')
    ->label('Kategori')

ExportColumn::make('tags.name')
    ->listAsJson()
```

---

## 📊 Export Formats

```php
ExportAction::make()
    ->exporter(UserExporter::class)
    ->formats([
        ExportFormat::Csv,
        ExportFormat::Xlsx,
    ])
```

---

## 🔍 Modify Query

```php
class UserExporter extends Exporter
{
    public static function modifyQuery(Builder $query): Builder
    {
        return $query->where('is_active', true);
    }
}
```

---

## 💾 Storage

```php
ExportAction::make()
    ->exporter(UserExporter::class)
    ->fileDisk('s3')
    ->fileName(fn () => 'users-' . now()->format('Y-m-d') . '.csv')
```

---

## ⚙️ Export Options

```php
ExportAction::make()
    ->exporter(UserExporter::class)
    ->options(fn () => [
        'include_headers' => true,
    ])
```

---

## 🎯 Latihan Mandiri

Buat Exporter untuk Product dengan columns:

- `id`, `name`, `price` (formatted)
- `category.name` relationship
- `created_at`
- Support CSV dan XLSX
