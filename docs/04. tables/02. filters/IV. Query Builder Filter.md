# XV. Query Builder Filter 🏗️

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/filters/query-builder](https://filamentphp.com/docs/5.x/tables/filters/query-builder)

---

## 🤔 Apa itu Query Builder?

**Query Builder** memungkinkan user membuat filter kompleks dengan operator AND/OR, seperti di aplikasi spreadsheet.

```php
use Filament\Tables\Filters\QueryBuilder;
use Filament\Tables\Filters\QueryBuilder\Constraints;

QueryBuilder::make()
    ->constraints([
        Constraints\TextConstraint::make('name'),
        Constraints\NumberConstraint::make('price'),
        Constraints\DateConstraint::make('created_at'),
    ])
```

---

## 📋 Jenis Constraint

| Constraint               | Untuk   |
| ------------------------ | ------- |
| `TextConstraint`         | Teks    |
| `NumberConstraint`       | Angka   |
| `DateConstraint`         | Tanggal |
| `BooleanConstraint`      | Boolean |
| `SelectConstraint`       | Pilihan |
| `RelationshipConstraint` | Relasi  |

---

## 📝 Text Constraint

```php
Constraints\TextConstraint::make('name')
    ->label('Nama')
```

Operator: contains, starts with, ends with, equals, etc.

---

## 🔢 Number Constraint

```php
Constraints\NumberConstraint::make('price')
    ->label('Harga')
```

Operator: equals, greater than, less than, between, etc.

---

## 📅 Date Constraint

```php
Constraints\DateConstraint::make('created_at')
    ->label('Tanggal Dibuat')
```

---

## ✅ Boolean Constraint

```php
Constraints\BooleanConstraint::make('is_active')
    ->label('Status Aktif')
```

---

## 📋 Select Constraint

```php
Constraints\SelectConstraint::make('status')
    ->options([
        'draft' => 'Draft',
        'published' => 'Published',
    ])
```

---

## 🔗 Relationship Constraint

```php
Constraints\RelationshipConstraint::make('categories')
    ->label('Kategori')
    ->selectable(
        IsRelatedToOperator::make()
            ->titleAttribute('name')
            ->preload()
    )
```

---

## 🎯 Latihan Mandiri

Buat QueryBuilder dengan constraints:

- name (text)
- price (number)
- category (relationship)
- created_at (date)
