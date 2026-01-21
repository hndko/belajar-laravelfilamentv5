# III. Select 📋

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/select](https://filamentphp.com/docs/5.x/forms/select)

---

## 🤔 Apa itu Select?

**Select** adalah dropdown untuk memilih satu atau beberapa opsi.

```php
use Filament\Forms\Components\Select;

Select::make('status')
    ->options([
        'draft' => 'Draft',
        'published' => 'Published',
        'archived' => 'Archived',
    ])
```

---

## 🔍 Searchable

```php
Select::make('country')
    ->options(Country::pluck('name', 'id'))
    ->searchable()
```

---

## ✅ Multi-Select

```php
Select::make('categories')
    ->multiple()
    ->options(Category::pluck('name', 'id'))
```

### Reorder Selected

```php
Select::make('tags')
    ->multiple()
    ->reorderable()
```

---

## 📂 Grouping Options

```php
Select::make('product')
    ->options([
        'Electronics' => [
            'laptop' => 'Laptop',
            'phone' => 'Phone',
        ],
        'Clothing' => [
            'shirt' => 'Shirt',
            'pants' => 'Pants',
        ],
    ])
```

---

## 🔗 Relationship

```php
Select::make('author_id')
    ->relationship('author', 'name')
```

### Preload

```php
Select::make('category_id')
    ->relationship('category', 'name')
    ->preload()
```

### Custom Query

```php
Select::make('user_id')
    ->relationship('user', 'name')
    ->searchable()
    ->modifyQueryUsing(fn ($query) => $query->where('active', true))
```

---

## ➕ Create Option

```php
Select::make('category_id')
    ->relationship('category', 'name')
    ->createOptionForm([
        TextInput::make('name')
            ->required(),
    ])
```

---

## ✏️ Edit Option

```php
Select::make('category_id')
    ->relationship('category', 'name')
    ->editOptionForm([
        TextInput::make('name'),
    ])
```

---

## 🎨 Boolean Options

```php
Select::make('is_active')
    ->boolean()
```

---

## ✅ Validasi

```php
Select::make('categories')
    ->multiple()
    ->minItems(1)
    ->maxItems(5)
```

---

## 🎯 Latihan Mandiri

Buat Select untuk:

- `status` dengan 3 opsi
- `category_id` dengan relationship dan create option
- `tags` multiple dengan max 5 items
