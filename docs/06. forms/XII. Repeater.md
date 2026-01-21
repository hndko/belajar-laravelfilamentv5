# XII. Repeater 🔄

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/repeater](https://filamentphp.com/docs/5.x/forms/repeater)

---

## 🤔 Apa itu Repeater?

**Repeater** adalah field untuk menambah item berulang dinamis.

```php
use Filament\Forms\Components\Repeater;

Repeater::make('items')
    ->schema([
        TextInput::make('name'),
        TextInput::make('quantity')
            ->numeric(),
    ])
```

---

## 📋 Default Items

```php
Repeater::make('contacts')
    ->schema([...])
    ->defaultItems(1)
```

### Empty Default

```php
Repeater::make('items')
    ->defaultItems(0)
```

---

## ➕ Add Button

```php
Repeater::make('items')
    ->addActionLabel('Tambah Item')
    ->addActionAlignment(Alignment::Start)
```

### Disable Add

```php
Repeater::make('items')
    ->addable(false)
```

---

## ❌ Delete Items

```php
Repeater::make('items')
    ->deletable(false)  // Tidak bisa hapus
```

---

## 🔀 Reorder

```php
Repeater::make('steps')
    ->reorderable()
    ->reorderableWithButtons()
```

---

## 📂 Collapsible

```php
Repeater::make('sections')
    ->collapsible()
    ->collapsed()  // Default collapsed
```

---

## 📋 Clone Items

```php
Repeater::make('items')
    ->cloneable()
```

---

## 🔗 Relationship

```php
Repeater::make('addresses')
    ->relationship()
    ->schema([
        TextInput::make('street'),
        TextInput::make('city'),
    ])
```

### Reorder Relationship

```php
Repeater::make('items')
    ->relationship()
    ->orderColumn('sort')
```

---

## 📊 Grid Layout

```php
Repeater::make('features')
    ->grid(2)  // 2 kolom
    ->schema([...])
```

---

## 🏷️ Item Label

```php
Repeater::make('contacts')
    ->itemLabel(fn (array $state) => $state['name'] ?? 'Kontak Baru')
```

---

## 🔢 Numbering

```php
Repeater::make('steps')
    ->itemLabel(fn ($component) => 'Langkah ' . ($component->getItemIndex() + 1))
```

---

## 📋 Table Mode

```php
Repeater::make('line_items')
    ->table()
    ->schema([
        TextInput::make('product'),
        TextInput::make('qty')->numeric(),
        TextInput::make('price')->numeric(),
    ])
```

---

## ✅ Validasi

```php
Repeater::make('items')
    ->minItems(1)
    ->maxItems(10)
```

---

## 🎯 Latihan Mandiri

Buat Repeater untuk:

- `addresses` dengan relationship
- `order_items` table mode
- `steps` dengan numbering dan reorder
