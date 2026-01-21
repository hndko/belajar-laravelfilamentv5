# VII. Delete Action 🗑️

> **Sumber:** [https://filamentphp.com/docs/5.x/actions/delete](https://filamentphp.com/docs/5.x/actions/delete)

---

## 🤔 Apa itu DeleteAction?

**DeleteAction** adalah action bawaan untuk menghapus record dengan konfirmasi.

```php
use Filament\Actions\DeleteAction;

DeleteAction::make()
```

---

## 🔀 Redirect After Delete

```php
DeleteAction::make()
    ->successRedirectUrl(route('users.index'))
```

---

## 🔔 Custom Notification

```php
DeleteAction::make()
    ->successNotificationTitle('Record berhasil dihapus')
```

---

## ⏳ Lifecycle Hooks

```php
DeleteAction::make()
    ->before(function (Model $record) {
        // Sebelum delete
        // Contoh: hapus file terkait
        Storage::delete($record->avatar);
    })
    ->after(function () {
        // Setelah delete
    })
```

---

## 🚀 Bulk Delete Performance

Untuk bulk delete yang lebih cepat:

```php
DeleteBulkAction::make()
    ->deselectRecordsAfterCompletion()
```

---

## 💡 Contoh Penggunaan

```php
// Single delete dengan konfirmasi
DeleteAction::make()
    ->requiresConfirmation()
    ->modalHeading('Hapus User')
    ->modalDescription('Apakah Anda yakin ingin menghapus user ini?')
    ->modalSubmitActionLabel('Ya, Hapus')
    ->before(function (Model $record) {
        // Hapus data terkait
        $record->orders()->delete();
    })
    ->successNotificationTitle('User berhasil dihapus')
```

---

## 🎯 Latihan Mandiri

Buat DeleteAction dengan:

- Custom modal heading dan description
- Before hook untuk hapus file avatar
- Custom notification
