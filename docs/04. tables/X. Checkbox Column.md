# X. Checkbox Column ☑️

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/columns/checkbox](https://filamentphp.com/docs/5.x/tables/columns/checkbox)

---

## 🤔 Apa itu CheckboxColumn?

**CheckboxColumn** adalah checkbox yang bisa diklik langsung di tabel.

```php
use Filament\Tables\Columns\CheckboxColumn;

CheckboxColumn::make('is_completed')
```

---

## ⏳ Lifecycle Hooks

```php
CheckboxColumn::make('is_completed')
    ->afterStateUpdated(function ($record, $state) {
        if ($state) {
            $record->update(['completed_at' => now()]);
        } else {
            $record->update(['completed_at' => null]);
        }
    })
```

---

## 💡 Perbedaan dengan ToggleColumn

| CheckboxColumn       | ToggleColumn    |
| -------------------- | --------------- |
| Kotak checkbox       | Switch toggle   |
| Tampilan tradisional | Tampilan modern |
| Lebih compact        | Lebih visual    |

---

## 🎯 Latihan Mandiri

Buat CheckboxColumn untuk task `is_done` dengan hook yang set `completed_at`.
