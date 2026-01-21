# IX. Force Delete Action ⚠️

> **Sumber:** [https://filamentphp.com/docs/5.x/actions/force-delete](https://filamentphp.com/docs/5.x/actions/force-delete)

---

## 🤔 Apa itu ForceDeleteAction?

**ForceDeleteAction** menghapus record secara permanen (untuk model dengan soft deletes).

```php
use Filament\Actions\ForceDeleteAction;

ForceDeleteAction::make()
```

---

## 🔀 Redirect After Force Delete

```php
ForceDeleteAction::make()
    ->successRedirectUrl(route('users.index'))
```

---

## 🔔 Custom Notification

```php
ForceDeleteAction::make()
    ->successNotificationTitle('Record dihapus permanen')
```

---

## ⏳ Lifecycle Hooks

```php
ForceDeleteAction::make()
    ->before(function (Model $record) {
        // Sebelum force delete
        // Hapus file terkait
        Storage::deleteDirectory("users/{$record->id}");
    })
    ->after(function () {
        // Setelah force delete
    })
```

---

## 🚀 Bulk Force Delete Performance

```php
ForceDeleteBulkAction::make()
    ->deselectRecordsAfterCompletion()
```

---

## 💡 Contoh Penggunaan

```php
ForceDeleteAction::make()
    ->requiresConfirmation()
    ->modalHeading('Hapus Permanen')
    ->modalDescription('PERINGATAN: Data akan dihapus permanen dan tidak dapat dikembalikan!')
    ->modalSubmitActionLabel('Ya, Hapus Permanen')
    ->before(function (Model $record) {
        // Hapus semua data terkait
        $record->orders()->forceDelete();
        $record->comments()->forceDelete();
        Storage::deleteDirectory("users/{$record->id}");
    })
    ->successNotificationTitle('Data dihapus permanen')
```

---

## 🎯 Latihan Mandiri

Buat ForceDeleteAction dengan:

- Modal konfirmasi dengan warning
- Before hook untuk hapus file dan relasi
- Custom notification
