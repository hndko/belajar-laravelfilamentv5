# XI. Import Action 📥

> **Sumber:** [https://filamentphp.com/docs/5.x/actions/import](https://filamentphp.com/docs/5.x/actions/import)

---

## 🤔 Apa itu ImportAction?

**ImportAction** mengimport data dari file CSV ke database.

```php
use Filament\Actions\ImportAction;

ImportAction::make()
    ->importer(UserImporter::class)
```

---

## 🚀 Membuat Importer

```bash
php artisan make:filament-importer User
```

### File yang Dibuat:

```
app/Filament/Imports/UserImporter.php
```

---

## 📋 Defining Columns

```php
// app/Filament/Imports/UserImporter.php

use Filament\Actions\Imports\ImportColumn;
use Filament\Actions\Imports\Importer;

class UserImporter extends Importer
{
    protected static ?string $model = User::class;

    public static function getColumns(): array
    {
        return [
            ImportColumn::make('name')
                ->requiredMapping()
                ->rules(['required', 'string']),
            ImportColumn::make('email')
                ->requiredMapping()
                ->rules(['required', 'email', 'unique:users,email']),
            ImportColumn::make('phone')
                ->rules(['nullable', 'string']),
        ];
    }
}
```

---

## 🏷️ Column Label

```php
ImportColumn::make('name')
    ->label('Nama Lengkap')
```

---

## ✅ Validation

```php
ImportColumn::make('email')
    ->rules(['required', 'email', 'unique:users,email'])
```

---

## 🔄 Casting

```php
ImportColumn::make('is_active')
    ->castStateUsing(fn ($state) => $state === 'Yes')

ImportColumn::make('price')
    ->numeric()

ImportColumn::make('birthday')
    ->date()
```

---

## 🔗 Import Relationships

```php
ImportColumn::make('category')
    ->relationship(
        resolveUsing: fn ($state) => Category::where('name', $state)->first()
    )
```

---

## 📝 Update Existing

```php
class UserImporter extends Importer
{
    public function resolveRecord(): ?User
    {
        return User::firstOrNew([
            'email' => $this->data['email'],
        ]);
    }
}
```

---

## ⚙️ Import Options

```php
ImportAction::make()
    ->importer(UserImporter::class)
    ->options(fn () => [
        'default_role' => 'user',
    ])
```

---

## 📄 Example CSV

```php
public static function getCompletedNotificationBody(): string
{
    return 'Import selesai.';
}

public static function getExampleCsvData(): array
{
    return [
        ['name' => 'John Doe', 'email' => 'john@example.com'],
        ['name' => 'Jane Doe', 'email' => 'jane@example.com'],
    ];
}
```

---

## 🎯 Latihan Mandiri

Buat Importer untuk Product dengan columns:

- `name` required
- `price` numeric
- `category` relationship
- `is_active` boolean cast
