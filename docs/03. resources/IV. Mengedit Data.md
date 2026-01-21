# IV. Mengedit Data (Editing Records) ✏️

> **Sumber:** [https://filamentphp.com/docs/5.x/resources/editing-records](https://filamentphp.com/docs/5.x/resources/editing-records)

---

## 🤔 Apa itu Edit Page?

**Edit Page** adalah halaman dengan form yang sudah terisi data dari database. User bisa mengubah data dan menyimpannya kembali.

---

## 📥 Modifikasi Data Sebelum Mengisi Form

Kadang data perlu dimodifikasi sebelum ditampilkan di form:

```php
// Di file EditCustomer.php

protected function mutateFormDataBeforeFill(array $data): array
{
    // Contoh: Format tanggal
    $data['formatted_date'] = Carbon::parse($data['date'])->format('d/m/Y');

    return $data;
}
```

---

## 📤 Modifikasi Data Sebelum Disimpan

Untuk mengubah data sebelum disimpan ke database:

```php
protected function mutateFormDataBeforeSave(array $data): array
{
    // Catat siapa yang terakhir mengedit
    $data['last_edited_by_id'] = auth()->id();

    return $data;
}
```

---

## 🔧 Kustomisasi Proses Update

Untuk kontrol penuh atas proses update:

```php
use Illuminate\Database\Eloquent\Model;

protected function handleRecordUpdate(Model $record, array $data): Model
{
    // Custom logic
    $record->update($data);

    // Log aktivitas
    activity()->performedOn($record)->log('Updated record');

    return $record;
}
```

---

## 🔁 Lifecycle Hooks

Hooks yang tersedia untuk Edit page:

```php
use Filament\Resources\Pages\EditRecord;

class EditCustomer extends EditRecord
{
    // Sebelum data diambil dari database
    protected function beforeFill(): void { }

    // Setelah data mengisi form
    protected function afterFill(): void { }

    // Sebelum validasi
    protected function beforeValidate(): void { }

    // Setelah validasi
    protected function afterValidate(): void { }

    // Sebelum data disimpan
    protected function beforeSave(): void { }

    // Setelah data disimpan
    protected function afterSave(): void
    {
        // Kirim notifikasi email
        Mail::to($this->record->email)->send(new DataUpdated());
    }
}
```

---

## 💾 Menyimpan Sebagian Form

Kamu bisa menyimpan bagian form secara terpisah:

```php
use Filament\Actions\Action;
use Filament\Schemas\Components\Section;

Section::make('Rate limiting')
    ->schema([
        // Field di sini...
    ])
    ->footerActions([
        Action::make('save')
            ->action(function (Section $component, EditRecord $livewire) {
                $livewire->saveFormComponentOnly($component);

                Notification::make()
                    ->title('Rate limiting saved')
                    ->success()
                    ->send();
            })
            ->visible($operation === 'edit'),
    ])
```

---

## 🔒 Authorization

Edit page menggunakan method `update()` dari Policy:

```php
public function update(User $user, Customer $customer): bool
{
    return $user->id === $customer->user_id || $user->isAdmin();
}
```

---

## 💡 Ringkasan

| Fitur                            | Method                         |
| -------------------------------- | ------------------------------ |
| Modifikasi data sebelum isi form | `mutateFormDataBeforeFill()`   |
| Modifikasi data sebelum simpan   | `mutateFormDataBeforeSave()`   |
| Custom proses update             | `handleRecordUpdate()`         |
| Hook sebelum/sesudah simpan      | `beforeSave()` / `afterSave()` |
| Simpan sebagian form             | `saveFormComponentOnly()`      |

---

## 🎯 Latihan Mandiri

Tambahkan field `updated_by` yang otomatis terisi ID user saat edit data.

<details>
<summary>Jawaban</summary>

```php
// EditProduct.php
protected function mutateFormDataBeforeSave(array $data): array
{
    $data['updated_by'] = auth()->id();
    return $data;
}
```

</details>
