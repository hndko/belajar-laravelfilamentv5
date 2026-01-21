# XII. Filters - Pengenalan 🔍

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/filters/overview](https://filamentphp.com/docs/5.x/tables/filters/overview)

---

## 🤔 Apa itu Filter?

**Filter** digunakan untuk menyaring data di tabel berdasarkan kondisi tertentu. User bisa memilih filter dan tabel akan menampilkan data yang sesuai.

---

## 📋 Jenis-Jenis Filter

| Filter          | Fungsi                         |
| --------------- | ------------------------------ |
| `Filter`        | Filter dasar dengan checkbox   |
| `SelectFilter`  | Filter dengan dropdown         |
| `TernaryFilter` | Filter 3 opsi (Yes/No/All)     |
| `QueryBuilder`  | Filter kompleks dengan kondisi |

---

## 🚀 Filter Dasar

```php
use Filament\Tables\Filters\Filter;

Filter::make('is_featured')
    ->query(fn ($query) => $query->where('is_featured', true))
```

---

## 🏷️ Label

```php
Filter::make('is_featured')
    ->label('Hanya Produk Unggulan')
```

---

## 🔘 Toggle Button

Ganti checkbox dengan toggle:

```php
Filter::make('is_active')
    ->toggle()
```

---

## 📌 Default Value

Filter aktif secara default:

```php
Filter::make('is_published')
    ->default()
```

---

## 💾 Persist Filter

Simpan pilihan filter di session:

```php
$table->persistFiltersInSession()
```

---

## ⚡ Live Filter

Filter langsung tanpa tombol Apply:

```php
$table->filtersApplyAction(null)
```

Atau dengan custom action:

```php
$table->filtersApplyAction(
    fn (Action $action) => $action->label('Terapkan')
)
```

---

## 🎯 Latihan Mandiri

Buat filter untuk:

- `is_featured` (checkbox)
- `status` (selectfilter dengan opsi draft/published)
