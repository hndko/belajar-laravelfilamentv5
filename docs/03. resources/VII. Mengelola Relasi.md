# VII. Mengelola Relasi (Managing Relationships) 🔗

> **Sumber:** [https://filamentphp.com/docs/5.x/resources/managing-relationships](https://filamentphp.com/docs/5.x/resources/managing-relationships)

---

## 🤔 Apa itu Relation?

**Relation** adalah hubungan antara tabel di database. Contoh:

- Satu `Category` punya banyak `Product` (hasMany)
- Satu `Product` dimiliki satu `Category` (belongsTo)
- Satu `User` punya banyak `Role`, dan sebaliknya (belongsToMany)

---

## 🛠️ Pilihan Tool untuk Mengelola Relasi

| Tool                    | Cocok Untuk              | UI                          |
| ----------------------- | ------------------------ | --------------------------- |
| **Relation Manager**    | HasMany, BelongsToMany   | Tabel di bawah form         |
| **Select/CheckboxList** | BelongsTo, BelongsToMany | Dropdown/checkbox di form   |
| **Repeater**            | HasMany (sederhana)      | Form berulang di dalam form |

---

## 📋 Relation Manager

Relation Manager menampilkan tabel data relasi di bawah form Edit/View.

### Membuat Relation Manager

```bash
php artisan make:filament-relation-manager CategoryResource posts title
```

**Penjelasan:**

- `CategoryResource` = Resource parent
- `posts` = Nama relasi di model
- `title` = Kolom untuk identifikasi record

### Hasil File

```
CategoryResource/RelationManagers/PostsRelationManager.php
```

### Isi File

```php
use Filament\Forms;
use Filament\Tables;

public function form(Schema $schema): Schema
{
    return $schema
        ->components([
            Forms\Components\TextInput::make('title')
                ->required(),
        ]);
}

public function table(Table $table): Table
{
    return $table
        ->columns([
            Tables\Columns\TextColumn::make('title'),
        ]);
}
```

### Daftarkan di Resource

```php
public static function getRelations(): array
{
    return [
        RelationManagers\PostsRelationManager::class,
    ];
}
```

---

## 🔗 Attach & Detach (BelongsToMany)

Untuk relasi many-to-many, kamu bisa "attach" (hubungkan) dan "detach" (lepaskan) record:

```php
use Filament\Actions\AttachAction;
use Filament\Actions\DetachAction;
use Filament\Actions\DetachBulkAction;

public function table(Table $table): Table
{
    return $table
        ->columns([...])
        ->headerActions([
            AttachAction::make()
                ->preloadRecordSelect(), // Load semua opsi
        ])
        ->recordActions([
            DetachAction::make(),
        ])
        ->toolbarActions([
            BulkActionGroup::make([
                DetachBulkAction::make(),
            ]),
        ]);
}
```

---

## 🔄 Associate & Dissociate (HasMany)

Untuk relasi hasMany dimana child record sudah ada:

```php
use Filament\Actions\AssociateAction;
use Filament\Actions\DissociateAction;

public function table(Table $table): Table
{
    return $table
        ->headerActions([
            AssociateAction::make(),
        ])
        ->recordActions([
            DissociateAction::make(),
        ]);
}
```

---

## 🆕 Create Related Records

Buat record baru langsung dari Relation Manager:

```php
use Filament\Actions\CreateAction;

public function table(Table $table): Table
{
    return $table
        ->headerActions([
            CreateAction::make(),
        ]);
}
```

---

## 📂 Pivot Attributes

Untuk relasi many-to-many dengan data pivot (contoh: quantity di tabel pivot):

### Di Model

```php
public function products()
{
    return $this->belongsToMany(Product::class)
        ->withPivot('quantity');
}
```

### Di Relation Manager

```php
AttachAction::make()
    ->form([
        TextInput::make('quantity')
            ->required()
            ->numeric(),
    ])
```

---

## 🎨 Menampilkan Relation Manager di Tab

Gabungkan form dan relation manager dalam satu tab:

```php
// Di resource
protected static function getContentTabLabel(): ?string
{
    return 'Detail';
}
```

---

## 💡 Ringkasan

| Action             | Fungsi                    | Untuk Relasi  |
| ------------------ | ------------------------- | ------------- |
| `CreateAction`     | Buat record baru          | Semua         |
| `EditAction`       | Edit record               | Semua         |
| `DeleteAction`     | Hapus record              | Semua         |
| `AttachAction`     | Hubungkan record yang ada | BelongsToMany |
| `DetachAction`     | Lepaskan hubungan         | BelongsToMany |
| `AssociateAction`  | Hubungkan child           | HasMany       |
| `DissociateAction` | Lepaskan child            | HasMany       |

---

## 🎯 Latihan Mandiri

1. Buat relasi `Category hasMany Product`
2. Buat Relation Manager untuk mengelola Product dari Category
3. Coba tambah Product baru dari halaman Edit Category

<details>
<summary>Langkah</summary>

```bash
# Buat relation manager
php artisan make:filament-relation-manager CategoryResource products name
```

```php
// Daftarkan di CategoryResource.php
public static function getRelations(): array
{
    return [
        RelationManagers\ProductsRelationManager::class,
    ];
}
```

</details>
