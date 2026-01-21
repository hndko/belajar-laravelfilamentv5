# X. Restore Action ♻️

> **Sumber:** [https://filamentphp.com/docs/5.x/actions/restore](https://filamentphp.com/docs/5.x/actions/restore)

---

## 🤔 Apa itu RestoreAction?

**RestoreAction** mengembalikan record yang soft deleted.

```php
use Filament\Actions\RestoreAction;

RestoreAction::make()
```

---

## 🔀 Redirect After Restore

```php
RestoreAction::make()
    ->successRedirectUrl(fn (Model $record) => route('users.show', $record))
```

---

## 🔔 Custom Notification

```php
RestoreAction::make()
    ->successNotificationTitle('Record berhasil dikembalikan')
```

---

## ⏳ Lifecycle Hooks

```php
RestoreAction::make()
    ->before(function (Model $record) {
        // Sebelum restore
    })
    ->after(function (Model $record) {
        // Setelah restore
        // Restore relasi juga
        $record->comments()->restore();
    })
```

---

## 🚀 Bulk Restore Performance

```php
RestoreBulkAction::make()
    ->deselectRecordsAfterCompletion()
```

---

## 💡 Contoh Penggunaan

```php
RestoreAction::make()
    ->after(function (Model $record) {
        // Restore semua relasi
        $record->comments()->restore();
        $record->orders()->restore();

        // Kirim notifikasi
        $record->notify(new AccountRestoredNotification());
    })
    ->successNotificationTitle('Akun berhasil dikembalikan')
```

---

## 🎯 Latihan Mandiri

Buat RestoreAction dengan:

- After hook untuk restore relasi comments
- Custom notification
- Redirect ke halaman show
