# I. Resources - Pengenalan 📚

> **Sumber:** [https://filamentphp.com/docs/5.x/resources/overview](https://filamentphp.com/docs/5.x/resources/overview)

---

## 🤔 Apa itu Resource?

**Resource** adalah kelas PHP yang digunakan untuk membuat halaman **CRUD** (Create, Read, Update, Delete) untuk model Eloquent-mu. Dengan Resource, kamu bisa mengelola data database melalui tabel dan form.

### Analoginya:

Bayangkan Resource seperti **meja kerja lengkap** untuk mengelola satu jenis data. Meja ini punya:

- **Daftar** semua data (tabel)
- **Form** untuk tambah data baru
- **Form** untuk edit data
- **Tombol** untuk hapus data

---

## 🚀 Membuat Resource Baru

### Perintah Dasar

Untuk membuat Resource untuk model `Customer`:

```bash
php artisan make:filament-resource Customer
```

### Hasil yang Dibuat

Perintah ini akan membuat beberapa file:

```
app/Filament/Resources/Customers/
├── CustomerResource.php        ← File utama resource
├── Pages/
│   ├── CreateCustomer.php      ← Halaman tambah data
│   ├── EditCustomer.php        ← Halaman edit data
│   └── ListCustomers.php       ← Halaman daftar data
├── Schemas/
│   └── CustomerForm.php        ← Definisi form
└── Tables/
    └── CustomersTable.php      ← Definisi tabel
```

---

## 🎛️ Opsi Tambahan Saat Membuat Resource

### 1. Simple Resource (Pakai Modal)

Untuk model yang sederhana, semua operasi bisa dilakukan di satu halaman dengan modal (popup):

```bash
php artisan make:filament-resource Customer --simple
```

**Hasil:** Hanya ada halaman "Manage" dengan modal untuk create/edit/delete.

### 2. Generate Otomatis Form dan Tabel

Filament bisa membaca struktur database dan generate form/tabel otomatis:

```bash
php artisan make:filament-resource Customer --generate
```

**Cocok untuk:** Membuat prototype cepat!

### 3. Dengan Soft Delete

Untuk model yang menggunakan soft delete (data tidak benar-benar dihapus):

```bash
php artisan make:filament-resource Customer --soft-deletes
```

### 4. Dengan Halaman View

Tambah halaman khusus untuk melihat detail (read-only):

```bash
php artisan make:filament-resource Customer --view
```

### 5. Generate Semua Sekaligus

Generate model, migration, factory, dan resource dalam satu perintah:

```bash
php artisan make:filament-resource Customer --model --migration --factory
```

---

## 📝 Record Title (Judul Record)

Atur kolom mana yang dipakai untuk mengidentifikasi record:

```php
// Di file CustomerResource.php
protected static ?string $recordTitleAttribute = 'name';
```

**Kenapa penting?** Dipakai untuk:

- Global search
- Notifikasi
- Breadcrumb

---

## 📋 Form di Resource

Form didefinisikan di file `Schemas/CustomerForm.php`:

```php
use Filament\Forms\Components\TextInput;
use Filament\Schemas\Schema;

public static function configure(Schema $schema): Schema
{
    return $schema
        ->components([
            TextInput::make('name')
                ->required(),
            TextInput::make('email')
                ->email()
                ->required(),
        ]);
}
```

### Contoh Field yang Tersedia:

| Field        | Fungsi             |
| ------------ | ------------------ |
| `TextInput`  | Input teks biasa   |
| `Textarea`   | Input teks panjang |
| `Select`     | Dropdown pilihan   |
| `Checkbox`   | Kotak centang      |
| `Toggle`     | Saklar on/off      |
| `DatePicker` | Pemilih tanggal    |
| `FileUpload` | Upload file        |

---

## 📊 Tabel di Resource

Tabel didefinisikan di file `Tables/CustomersTable.php`:

```php
use Filament\Tables\Columns\TextColumn;
use Filament\Tables\Table;

public static function configure(Table $table): Table
{
    return $table
        ->columns([
            TextColumn::make('name'),
            TextColumn::make('email'),
            TextColumn::make('created_at')
                ->dateTime(),
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

## 🧭 Navigasi Resource

Resource otomatis muncul di sidebar. Kamu bisa mengkustomisasi:

### Ubah Label Navigasi

```php
protected static ?string $navigationLabel = 'Pelanggan Saya';
```

### Ubah Ikon

```php
protected static ?string $navigationIcon = 'heroicon-o-users';
```

### Urutan di Menu

```php
protected static ?int $navigationSort = 2;
```

### Grup Menu

```php
protected static ?string $navigationGroup = 'Manajemen Pelanggan';
```

---

## 🔗 Generate URL ke Resource

Untuk membuat link ke halaman resource:

```php
use App\Filament\Resources\Customers\CustomerResource;

// URL ke halaman list
CustomerResource::getUrl(); // /admin/customers

// URL ke halaman create
CustomerResource::getUrl('create'); // /admin/customers/create

// URL ke halaman edit
CustomerResource::getUrl('edit', ['record' => $customer]); // /admin/customers/edit/1
```

---

## 🔒 Authorization (Hak Akses)

Filament menggunakan **Laravel Policy** untuk mengatur hak akses:

| Method Policy   | Fungsi                     |
| --------------- | -------------------------- |
| `viewAny()`     | Boleh lihat daftar?        |
| `create()`      | Boleh tambah data?         |
| `update()`      | Boleh edit data?           |
| `view()`        | Boleh lihat detail?        |
| `delete()`      | Boleh hapus data?          |
| `restore()`     | Boleh restore soft-delete? |
| `forceDelete()` | Boleh hapus permanen?      |

### Contoh Policy:

```php
// app/Policies/CustomerPolicy.php
public function viewAny(User $user): bool
{
    return $user->hasRole('admin');
}

public function create(User $user): bool
{
    return $user->hasPermission('create-customers');
}
```

---

## ❓ Troubleshooting

### Resource tidak muncul di menu?

1. Cek apakah ada policy dengan method `viewAny()` yang return `false`
2. Pastikan resource terdaftar di panel provider

---

## 💡 Ringkasan

| Perintah                        | Fungsi                       |
| ------------------------------- | ---------------------------- |
| `make:filament-resource Model`  | Buat resource standar        |
| `--simple`                      | Resource dengan modal        |
| `--generate`                    | Generate form/tabel otomatis |
| `--soft-deletes`                | Dengan soft delete           |
| `--view`                        | Dengan halaman view          |
| `--model --migration --factory` | Generate semua sekaligus     |

---

## 🎯 Latihan Mandiri

1. Buat model `Product` dengan migration
2. Buat resource dengan `--generate`:
   ```bash
   php artisan make:filament-resource Product --generate
   ```
3. Buka `/admin/products` dan lihat hasilnya
4. Coba tambah beberapa data produk

<details>
<summary>Langkah Detail</summary>

```bash
# 1. Buat model dengan migration
php artisan make:model Product -m

# 2. Edit migration (tambah kolom name, price, description)

# 3. Jalankan migration
php artisan migrate

# 4. Buat resource
php artisan make:filament-resource Product --generate

# 5. Buka browser: /admin/products
```

</details>
