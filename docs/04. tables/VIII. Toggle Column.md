# VIII. Toggle Column 🔘

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/columns/toggle](https://filamentphp.com/docs/5.x/tables/columns/toggle)

---

## 🤔 Apa itu ToggleColumn?

**ToggleColumn** adalah switch on/off yang bisa diedit langsung di tabel. Cocok untuk boolean fields.

```php
use Filament\Tables\Columns\ToggleColumn;

ToggleColumn::make('is_active')
```

---

## ⏳ Lifecycle Hooks

```php
ToggleColumn::make('is_featured')
    ->beforeStateUpdated(function ($record, $state) {
        // Validasi sebelum ubah
        if ($state && ! $record->canBeFeatured()) {
            throw new \Exception('Cannot feature this item');
        }
    })
    ->afterStateUpdated(function ($record, $state) {
        // Setelah diubah
        if ($state) {
            Cache::forget('featured_items');
        }
    })
```

---

## 💡 Contoh Penggunaan

### Publish/Unpublish

```php
ToggleColumn::make('is_published')
    ->label('Published')
```

### User Active Status

```php
ToggleColumn::make('is_active')
    ->label('Active')
    ->afterStateUpdated(fn ($record, $state) =>
        $state ? $record->activate() : $record->deactivate()
    )
```

---

## 🎯 Latihan Mandiri

Buat ToggleColumn untuk `is_visible` dengan hook yang clear cache setelah perubahan.
