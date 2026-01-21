# I. Actions - Pengenalan ⚡

> **Sumber:** [https://filamentphp.com/docs/5.x/actions/overview](https://filamentphp.com/docs/5.x/actions/overview)

---

## 🤔 Apa itu Actions?

**Actions** adalah tombol interaktif untuk melakukan operasi seperti create, edit, delete, dan operasi kustom lainnya.

---

## 📋 Jenis Actions

| Action              | Fungsi                |
| ------------------- | --------------------- |
| `CreateAction`      | Membuat record baru   |
| `EditAction`        | Mengedit record       |
| `ViewAction`        | Melihat detail record |
| `DeleteAction`      | Menghapus record      |
| `ReplicateAction`   | Menduplikasi record   |
| `RestoreAction`     | Restore soft deleted  |
| `ForceDeleteAction` | Hapus permanen        |
| `ImportAction`      | Import dari CSV       |
| `ExportAction`      | Export ke CSV/XLSX    |

---

## 🎨 Trigger Style

```php
use Filament\Actions\Action;

// Button (default)
Action::make('save')->button()

// Link
Action::make('cancel')->link()

// Icon button
Action::make('refresh')->iconButton()
```

---

## 🏷️ Label & Icon

```php
Action::make('approve')
    ->label('Setujui')
    ->icon('heroicon-o-check')
```

---

## 🎨 Color & Size

```php
Action::make('delete')
    ->color('danger')
    ->size('lg')  // sm, md, lg
```

---

## 🔒 Authorization

```php
Action::make('publish')
    ->visible(fn () => auth()->user()->can('publish'))

Action::make('delete')
    ->authorize('delete')  // Gunakan policy
```

### Disable

```php
Action::make('submit')
    ->disabled(fn () => $this->record->is_locked)
```

---

## ⌨️ Keybinding

```php
Action::make('save')
    ->keyBindings(['mod+s'])
```

---

## 🔢 Badge

```php
Action::make('notifications')
    ->badge(fn () => Notification::unread()->count())
    ->badgeColor('danger')
```

---

## 🎨 Outlined

```php
Action::make('cancel')
    ->outlined()
```

---

## ⏱️ Rate Limiting

```php
Action::make('sendEmail')
    ->rateLimited(5)  // Max 5x per menit
```

---

## 💉 Utility Injection

```php
Action::make('approve')
    ->action(function (array $data, Model $record) {
        $record->update(['status' => 'approved']);
    })
```

---

## 🎯 Latihan Mandiri

Buat Actions untuk:

- `approve` dengan icon check dan warna success
- `reject` dengan color danger
- `export` dengan badge jumlah records
