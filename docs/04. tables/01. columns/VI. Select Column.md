# VII. Select Column 📋

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/columns/select](https://filamentphp.com/docs/5.x/tables/columns/select)

---

## 🤔 Apa itu SelectColumn?

**SelectColumn** adalah dropdown yang bisa diedit langsung di tabel. User bisa mengubah nilai tanpa membuka halaman edit.

```php
use Filament\Tables\Columns\SelectColumn;

SelectColumn::make('status')
    ->options([
        'draft' => 'Draft',
        'published' => 'Published',
        'archived' => 'Archived',
    ])
```

---

## 🔍 Searchable

```php
SelectColumn::make('category_id')
    ->options(Category::pluck('name', 'id'))
    ->searchable()
```

---

## 🔗 Relationship

```php
SelectColumn::make('author_id')
    ->relationship('author', 'name')
```

### Custom Query

```php
SelectColumn::make('author_id')
    ->relationship('author', 'name')
    ->modifyQueryUsing(fn ($query) => $query->where('active', true))
```

---

## ⏳ Lifecycle Hooks

```php
SelectColumn::make('status')
    ->options([...])
    ->afterStateUpdated(function ($record, $state) {
        // Log perubahan
        ActivityLog::create([
            'record_id' => $record->id,
            'new_status' => $state,
        ]);
    })
```

---

## 🎯 Latihan Mandiri

Buat SelectColumn untuk mengubah `priority` (low/medium/high) langsung dari tabel.
