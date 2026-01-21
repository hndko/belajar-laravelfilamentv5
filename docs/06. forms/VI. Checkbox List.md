# VI. Checkbox List ☑️

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/checkbox-list](https://filamentphp.com/docs/5.x/forms/checkbox-list)

---

## 🤔 Apa itu CheckboxList?

**CheckboxList** adalah daftar checkbox untuk memilih multiple options.

```php
use Filament\Forms\Components\CheckboxList;

CheckboxList::make('technologies')
    ->options([
        'php' => 'PHP',
        'javascript' => 'JavaScript',
        'python' => 'Python',
    ])
```

---

## 📝 Option Descriptions

```php
CheckboxList::make('features')
    ->options([
        'seo' => 'SEO',
        'api' => 'API',
    ])
    ->descriptions([
        'seo' => 'Optimisasi mesin pencari',
        'api' => 'Integrasi dengan aplikasi lain',
    ])
```

---

## 📊 Grid Columns

```php
CheckboxList::make('permissions')
    ->options([...])
    ->columns(2)  // 2 kolom
```

### Grid Direction

```php
CheckboxList::make('roles')
    ->options([...])
    ->columns(2)
    ->gridDirection('row')  // atau 'column'
```

---

## 🔍 Searchable

```php
CheckboxList::make('categories')
    ->options(Category::pluck('name', 'id'))
    ->searchable()
```

---

## ✅ Bulk Toggle

```php
CheckboxList::make('permissions')
    ->options([...])
    ->bulkToggleable()  // Select All / Deselect All
```

---

## 🔗 Relationship

```php
CheckboxList::make('roles')
    ->relationship('roles', 'name')
```

### Custom Query

```php
CheckboxList::make('categories')
    ->relationship('categories', 'name')
    ->modifyQueryUsing(fn ($query) => $query->where('active', true))
```

---

## 🚫 Disable Options

```php
CheckboxList::make('plans')
    ->options([
        'basic' => 'Basic',
        'pro' => 'Pro',
        'enterprise' => 'Enterprise',
    ])
    ->disableOptionWhen(fn ($value) => $value === 'enterprise')
```

---

## 🎯 Latihan Mandiri

Buat CheckboxList untuk:

- `permissions` dengan bulk toggle
- `categories` dengan relationship
- `features` dengan descriptions
