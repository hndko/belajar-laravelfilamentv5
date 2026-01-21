# VI. Menghapus Data (Deleting Records) 🗑️

> **Sumber:** [https://filamentphp.com/docs/5.x/resources/deleting-records](https://filamentphp.com/docs/5.x/resources/deleting-records)

---

## 🤔 Jenis-Jenis Hapus

| Jenis            | Penjelasan                                     |
| ---------------- | ---------------------------------------------- |
| **Delete**       | Hapus biasa (atau soft-delete jika diaktifkan) |
| **Force Delete** | Hapus permanen dari database                   |
| **Restore**      | Kembalikan data yang soft-deleted              |

---

## 🛡️ Soft Delete

**Soft Delete** = Data tidak benar-benar dihapus, hanya ditandai sebagai "dihapus" dengan kolom `deleted_at`.

### Membuat Resource dengan Soft Delete

```bash
php artisan make:filament-resource Customer --soft-deletes
```

---

## ➕ Menambah Soft Delete ke Resource yang Sudah Ada

### Langkah 1: Update Model

Pastikan model-mu menggunakan trait `SoftDeletes`:

```php
use Illuminate\Database\Eloquent\SoftDeletes;

class Customer extends Model
{
    use SoftDeletes;
}
```

### Langkah 2: Update Resource Table

```php
use Filament\Actions\DeleteAction;
use Filament\Actions\DeleteBulkAction;
use Filament\Actions\ForceDeleteAction;
use Filament\Actions\ForceDeleteBulkAction;
use Filament\Actions\RestoreAction;
use Filament\Actions\RestoreBulkAction;
use Filament\Tables\Filters\TrashedFilter;

public static function table(Table $table): Table
{
    return $table
        ->columns([
            // ...
        ])
        ->filters([
            TrashedFilter::make(), // Filter untuk lihat data terhapus
        ])
        ->recordActions([
            DeleteAction::make(),
            ForceDeleteAction::make(),
            RestoreAction::make(),
        ])
        ->toolbarActions([
            BulkActionGroup::make([
                DeleteBulkAction::make(),
                ForceDeleteBulkAction::make(),
                RestoreBulkAction::make(),
            ]),
        ]);
}
```

### Langkah 3: Update Query

```php
use Illuminate\Database\Eloquent\SoftDeletingScope;

public static function getRecordRouteBindingEloquentQuery(): Builder
{
    return parent::getRecordRouteBindingEloquentQuery()
        ->withoutGlobalScopes([
            SoftDeletingScope::class,
        ]);
}
```

### Langkah 4: Update Edit Page

```php
// EditCustomer.php
use Filament\Actions;

protected function getHeaderActions(): array
{
    return [
        Actions\DeleteAction::make(),
        Actions\ForceDeleteAction::make(),
        Actions\RestoreAction::make(),
    ];
}
```

---

## 🗑️ Delete dari List Page

Untuk menghapus dari halaman list:

```php
use Filament\Actions\DeleteAction;

public static function table(Table $table): Table
{
    return $table
        ->recordActions([
            DeleteAction::make(),
        ]);
}
```

---

## 🔒 Authorization

| Method Policy      | Fungsi                     |
| ------------------ | -------------------------- |
| `delete()`         | Boleh hapus satu record?   |
| `deleteAny()`      | Boleh bulk delete?         |
| `forceDelete()`    | Boleh hapus permanen?      |
| `forceDeleteAny()` | Boleh bulk force delete?   |
| `restore()`        | Boleh restore satu record? |
| `restoreAny()`     | Boleh bulk restore?        |

### Contoh Policy:

```php
public function delete(User $user, Customer $customer): bool
{
    return $user->can('delete-customers');
}

public function forceDelete(User $user, Customer $customer): bool
{
    return $user->isAdmin();
}

public function restore(User $user, Customer $customer): bool
{
    return $user->can('restore-customers');
}
```

---

## 💡 Ringkasan

| Action              | Fungsi               | Bulk Version            |
| ------------------- | -------------------- | ----------------------- |
| `DeleteAction`      | Hapus (soft/hard)    | `DeleteBulkAction`      |
| `ForceDeleteAction` | Hapus permanen       | `ForceDeleteBulkAction` |
| `RestoreAction`     | Kembalikan           | `RestoreBulkAction`     |
| `TrashedFilter`     | Filter data terhapus | -                       |

---

## 🎯 Latihan Mandiri

1. Tambahkan soft delete ke model Product
2. Tambahkan TrashedFilter ke tabel
3. Tambahkan tombol Restore di action tabel

<details>
<summary>Langkah-langkah</summary>

1. Edit model:

```php
use Illuminate\Database\Eloquent\SoftDeletes;

class Product extends Model
{
    use SoftDeletes;
}
```

2. Buat migration:

```bash
php artisan make:migration add_deleted_at_to_products_table
```

3. Isi migration:

```php
$table->softDeletes();
```

4. Update resource table dengan TrashedFilter dan RestoreAction

</details>
