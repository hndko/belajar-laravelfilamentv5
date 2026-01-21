# I. Tables - Pengenalan 📊

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/overview](https://filamentphp.com/docs/5.x/tables/overview)

---

## 🤔 Apa itu Table?

**Table** di Filament adalah komponen untuk menampilkan data dalam format tabel yang interaktif. Table mendukung sorting, searching, filtering, pagination, dan actions.

### Fitur Utama:

- ✅ **Columns** - Menampilkan data
- ✅ **Filters** - Menyaring data
- ✅ **Actions** - Aksi untuk setiap row atau bulk
- ✅ **Pagination** - Navigasi halaman
- ✅ **Sorting** - Mengurutkan data
- ✅ **Searching** - Mencari data

---

## 📋 Struktur Dasar Table

```php
use Filament\Tables\Table;
use Filament\Tables\Columns\TextColumn;
use Filament\Actions\EditAction;
use Filament\Actions\DeleteBulkAction;

public static function table(Table $table): Table
{
    return $table
        ->columns([
            TextColumn::make('name'),
            TextColumn::make('email'),
            TextColumn::make('created_at')->dateTime(),
        ])
        ->filters([
            // Filter di sini
        ])
        ->recordActions([
            EditAction::make(),
        ])
        ->toolbarActions([
            BulkActionGroup::make([
                DeleteBulkAction::make(),
            ]),
        ]);
}
```

---

## 📑 Pagination (Halaman)

### Opsi Jumlah Per Halaman

```php
$table->paginated([10, 25, 50, 100])
```

### Default Jumlah Per Halaman

```php
$table->defaultPaginationPageOption(25)
```

### Matikan Pagination

```php
$table->paginated(false)
```

### Simple Pagination (Lebih Cepat)

```php
$table->simplePagination()
```

---

## 🔗 Baris yang Bisa Diklik

Arahkan ke halaman edit saat baris diklik:

```php
$table->recordUrl(
    fn (Model $record) => route('users.edit', $record)
)
```

### Membuka di Tab Baru:

```php
$table->openRecordUrlInNewTab()
```

---

## 🔄 Reordering (Urutkan Manual)

Memungkinkan user menggeser baris untuk mengubah urutan:

```php
$table->reorderable('sort_order')
```

### Hook Setelah Reorder:

```php
$table->afterReorder(function () {
    // Clear cache, refresh data, dll.
})
```

---

## 🎨 Styling Baris

### Baris Bergaris (Striped)

```php
$table->striped()
```

### CSS Class Kustom

```php
$table->recordClasses(function (Model $record) {
    return match ($record->status) {
        'draft' => 'opacity-50',
        'deleted' => 'bg-red-100',
        default => null,
    };
})
```

---

## ⏱️ Polling (Refresh Otomatis)

Refresh tabel setiap interval tertentu:

```php
$table->poll('10s') // Refresh setiap 10 detik
```

---

## 🔍 Searching dengan Laravel Scout

Untuk pencarian yang lebih canggih:

```php
$table->searchable('scout')
```

---

## 💡 Ringkasan Komponen Table

| Komponen              | Fungsi                      |
| --------------------- | --------------------------- |
| `columns()`           | Kolom yang ditampilkan      |
| `filters()`           | Filter untuk menyaring data |
| `recordActions()`     | Aksi per baris              |
| `toolbarActions()`    | Aksi toolbar (bulk, dll)    |
| `headerActions()`     | Aksi di header              |
| `emptyStateActions()` | Aksi saat tabel kosong      |

---

## 🎯 Latihan Mandiri

1. Buat tabel Product dengan kolom: name, price, stock
2. Tambahkan pagination 10, 25, 50
3. Buat baris bisa diklik ke halaman edit
