# III. Menambah Data (Creating Records) ➕

> **Sumber:** [https://filamentphp.com/docs/5.x/resources/creating-records](https://filamentphp.com/docs/5.x/resources/creating-records)

---

## 🤔 Apa itu Create Page?

**Create Page** adalah halaman dengan form untuk menambah data baru ke database.

### Alur Kerja:

1. User klik tombol "Create" atau "Buat Baru"
2. Form tampil dengan field-field yang sudah didefinisikan
3. User isi data
4. Klik "Create" / "Simpan"
5. Data tersimpan ke database
6. User redirect ke halaman lain

---

## ✏️ Memodifikasi Data Sebelum Disimpan

Kadang kamu perlu menambah atau mengubah data sebelum disimpan:

```php
// Di file CreateCustomer.php

protected function mutateFormDataBeforeCreate(array $data): array
{
    // Tambah user_id dari user yang login
    $data['user_id'] = auth()->id();

    // Atau modifikasi data lain
    $data['slug'] = Str::slug($data['name']);

    return $data;
}
```

### Contoh Penggunaan:

- Menambah `user_id` atau `created_by`
- Generate slug otomatis
- Set default value
- Enkripsi data sensitif

---

## 🔧 Mengkustomisasi Proses Create

Untuk kontrol penuh atas bagaimana data dibuat:

```php
use Illuminate\Database\Eloquent\Model;

protected function handleRecordCreation(array $data): Model
{
    // Custom logic di sini
    $customer = Customer::create($data);

    // Bisa tambah logic lain
    $customer->assignDefaultRole();

    return $customer;
}
```

---

## 🔄 Mengatur Redirect Setelah Create

Secara default, setelah create akan redirect ke halaman Edit. Untuk mengubahnya:

```php
protected function getRedirectUrl(): string
{
    // Kembali ke halaman list
    return $this->getResource()::getUrl('index');
}
```

### Opsi Redirect:

```php
// Ke halaman list
return $this->getResource()::getUrl('index');

// Ke halaman view
return $this->getResource()::getUrl('view', ['record' => $this->record]);

// Ke halaman sebelumnya
return $this->previousUrl ?? $this->getResource()::getUrl('index');
```

### Set Default di Panel (Semua Resource):

```php
// Di AdminPanelProvider.php
use Filament\Panel;

public function panel(Panel $panel): Panel
{
    return $panel
        ->resourceCreatePageRedirect('index'); // atau 'view', 'edit'
}
```

---

## 📢 Mengkustomisasi Notifikasi

Ubah pesan yang muncul setelah data berhasil disimpan:

```php
use Filament\Notifications\Notification;

protected function getCreatedNotification(): ?Notification
{
    return Notification::make()
        ->success()
        ->title('Pelanggan berhasil ditambahkan')
        ->body('Data pelanggan baru telah tersimpan.');
}
```

---

## 🔁 Lifecycle Hooks

Hooks adalah method yang berjalan di waktu tertentu selama proses create:

```php
use Filament\Resources\Pages\CreateRecord;

class CreateCustomer extends CreateRecord
{
    // Sebelum form diisi default value
    protected function beforeFill(): void
    {
        // ...
    }

    // Setelah form diisi default value
    protected function afterFill(): void
    {
        // ...
    }

    // Sebelum validasi
    protected function beforeValidate(): void
    {
        // ...
    }

    // Setelah validasi
    protected function afterValidate(): void
    {
        // ...
    }

    // Sebelum data disimpan
    protected function beforeCreate(): void
    {
        // ...
    }

    // Setelah data disimpan
    protected function afterCreate(): void
    {
        // Kirim email notifikasi
        Mail::to($this->record->email)->send(new WelcomeEmail());
    }
}
```

### Diagram Lifecycle:

```
beforeFill() → afterFill() → [User isi form] →
beforeValidate() → afterValidate() →
beforeCreate() → [Data disimpan] → afterCreate()
```

---

## 🛑 Menghentikan Proses Create

Kamu bisa menghentikan proses create jika kondisi tertentu tidak terpenuhi:

```php
use Filament\Notifications\Notification;

protected function beforeCreate(): void
{
    // Cek apakah user punya subscription aktif
    if (! auth()->user()->hasActiveSubscription()) {
        Notification::make()
            ->warning()
            ->title('Subscription Tidak Aktif!')
            ->body('Silakan perpanjang subscription Anda.')
            ->persistent()
            ->send();

        $this->halt(); // ← Hentikan proses
    }
}
```

---

## 🧙 Menggunakan Wizard (Multi-Step Form)

Untuk form yang panjang, kamu bisa pecah jadi beberapa langkah:

```php
use Filament\Resources\Pages\CreateRecord;

class CreateCategory extends CreateRecord
{
    use CreateRecord\Concerns\HasWizard;

    protected function getSteps(): array
    {
        return [
            Step::make('Nama')
                ->description('Berikan nama yang jelas')
                ->schema([
                    TextInput::make('name')
                        ->required(),
                    TextInput::make('slug'),
                ]),

            Step::make('Deskripsi')
                ->description('Tambah detail')
                ->schema([
                    MarkdownEditor::make('description'),
                ]),

            Step::make('Pengaturan')
                ->description('Atur visibilitas')
                ->schema([
                    Toggle::make('is_visible')
                        ->label('Tampilkan ke publik')
                        ->default(true),
                ]),
        ];
    }
}
```

### Hasil:

Form akan tampil dalam 3 langkah dengan tombol "Next" dan "Previous".

---

## ➕ Tombol "Create & Create Another"

Secara default, ada tombol untuk membuat data lain setelah create. Untuk mematikan:

```php
protected function canCreateAnother(): bool
{
    return false;
}
```

---

## 🔒 Authorization

Create page menggunakan method `create()` dari Policy:

```php
// CustomerPolicy.php
public function create(User $user): bool
{
    return $user->can('create-customers');
}
```

---

## 💡 Ringkasan

| Fitur                          | Method                             |
| ------------------------------ | ---------------------------------- |
| Modifikasi data sebelum simpan | `mutateFormDataBeforeCreate()`     |
| Custom proses create           | `handleRecordCreation()`           |
| Ubah redirect                  | `getRedirectUrl()`                 |
| Custom notifikasi              | `getCreatedNotification()`         |
| Sebelum/sesudah create         | `beforeCreate()` / `afterCreate()` |
| Hentikan proses                | `$this->halt()`                    |
| Multi-step form                | `HasWizard` trait                  |

---

## 🎯 Latihan Mandiri

1. Buat resource `Order` dengan field: `customer_name`, `total`, `status`
2. Tambahkan `user_id` otomatis saat create
3. Setelah create, redirect ke halaman list
4. Tampilkan notifikasi custom "Pesanan berhasil dibuat!"

<details>
<summary>Contoh Jawaban</summary>

```php
// CreateOrder.php

protected function mutateFormDataBeforeCreate(array $data): array
{
    $data['user_id'] = auth()->id();
    return $data;
}

protected function getRedirectUrl(): string
{
    return $this->getResource()::getUrl('index');
}

protected function getCreatedNotification(): ?Notification
{
    return Notification::make()
        ->success()
        ->title('Pesanan berhasil dibuat!')
        ->body('Pesanan baru telah ditambahkan ke sistem.');
}
```

</details>
