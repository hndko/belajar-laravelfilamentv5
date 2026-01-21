# XIII. Select Filter 📋

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/filters/select](https://filamentphp.com/docs/5.x/tables/filters/select)

---

## 🤔 Apa itu SelectFilter?

**SelectFilter** adalah filter dengan dropdown pilihan.

```php
use Filament\Tables\Filters\SelectFilter;

SelectFilter::make('status')
    ->options([
        'draft' => 'Draft',
        'published' => 'Published',
        'archived' => 'Archived',
    ])
```

---

## 🔄 Custom Column

```php
SelectFilter::make('author')
    ->column('author_id')
    ->options(User::pluck('name', 'id'))
```

---

## ✅ Multi-Select

Pilih beberapa opsi sekaligus:

```php
SelectFilter::make('status')
    ->multiple()
    ->options([...])
```

---

## 🔗 Relationship Filter

```php
SelectFilter::make('category')
    ->relationship('category', 'name')
```

### Preload Options

```php
SelectFilter::make('author')
    ->relationship('author', 'name')
    ->preload()
```

### Custom Query

```php
SelectFilter::make('category')
    ->relationship('category', 'name')
    ->modifyQueryUsing(fn ($query) => $query->where('is_active', true))
```

---

## 🔍 Searchable

```php
SelectFilter::make('user')
    ->relationship('user', 'name')
    ->searchable()
```

---

## 📌 Default Value

```php
SelectFilter::make('status')
    ->options([...])
    ->default('published')
```

---

## 🎯 Latihan Mandiri

Buat SelectFilter untuk:

- `category_id` dengan relationship
- `priority` dengan opsi low/medium/high dan multi-select
