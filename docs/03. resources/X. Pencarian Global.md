# X. Pencarian Global (Global Search) 🔍

> **Sumber:** [https://filamentphp.com/docs/5.x/resources/global-search](https://filamentphp.com/docs/5.x/resources/global-search)

---

## 🤔 Apa itu Global Search?

**Global Search** adalah fitur pencarian yang bisa mencari data dari **semua resource** sekaligus dari satu kotak pencarian di header panel.

---

## 🚀 Mengaktifkan Global Search

### Langkah 1: Set Record Title Attribute

Di resource, tentukan kolom yang jadi "judul" record:

```php
// CustomerResource.php
protected static ?string $recordTitleAttribute = 'name';
```

> **Catatan:** Resource harus punya halaman Edit atau View agar hasil pencarian bisa diklik.

---

## 🔍 Mencari di Beberapa Kolom

Untuk mencari di lebih dari satu kolom:

```php
public static function getGloballySearchableAttributes(): array
{
    return ['name', 'email', 'phone', 'address'];
}
```

### Mencari di Relasi (Dot Notation):

```php
public static function getGloballySearchableAttributes(): array
{
    return [
        'title',
        'slug',
        'author.name',    // Kolom dari relasi author
        'category.name',  // Kolom dari relasi category
    ];
}
```

---

## 📝 Menambah Detail di Hasil Pencarian

Tampilkan info tambahan di bawah judul:

```php
public static function getGlobalSearchResultDetails(Model $record): array
{
    return [
        'Email' => $record->email,
        'Kategori' => $record->category->name,
    ];
}
```

### Optimasi dengan Eager Loading:

```php
public static function getGlobalSearchEloquentQuery(): Builder
{
    return parent::getGlobalSearchEloquentQuery()
        ->with(['author', 'category']); // Eager load relasi
}
```

---

## 🎨 Kustomisasi Judul Hasil

```php
use Illuminate\Contracts\Support\Htmlable;

public static function getGlobalSearchResultTitle(Model $record): string|Htmlable
{
    return $record->name . ' - ' . $record->email;
}
```

---

## 📌 Pengaturan Lainnya

### Batasi Jumlah Hasil

```php
protected static int $globalSearchResultsLimit = 5;
```

### Pindahkan Search ke Sidebar

```php
// Di Panel Provider
$panel->globalSearchSidebar()
```

### Matikan Global Search untuk Resource Tertentu

```php
protected static bool $isGloballySearchable = false;
```

### Keyboard Shortcut

```php
// Di Panel Provider
$panel->globalSearchKeyBindings(['command+k', 'ctrl+k'])
```

---

## 💡 Ringkasan

| Method                              | Fungsi                     |
| ----------------------------------- | -------------------------- |
| `$recordTitleAttribute`             | Kolom untuk judul hasil    |
| `getGloballySearchableAttributes()` | Kolom yang bisa dicari     |
| `getGlobalSearchResultDetails()`    | Detail tambahan            |
| `getGlobalSearchResultTitle()`      | Custom judul               |
| `$isGloballySearchable = false`     | Matikan untuk resource ini |

---

## 🎯 Latihan Mandiri

1. Aktifkan global search untuk ProductResource
2. Cari berdasarkan: name, description, category.name
3. Tampilkan harga di detail hasil pencarian

<details>
<summary>Jawaban</summary>

```php
// ProductResource.php

protected static ?string $recordTitleAttribute = 'name';

public static function getGloballySearchableAttributes(): array
{
    return ['name', 'description', 'category.name'];
}

public static function getGlobalSearchResultDetails(Model $record): array
{
    return [
        'Harga' => 'Rp ' . number_format($record->price),
        'Kategori' => $record->category?->name ?? '-',
    ];
}

public static function getGlobalSearchEloquentQuery(): Builder
{
    return parent::getGlobalSearchEloquentQuery()->with('category');
}
```

</details>
