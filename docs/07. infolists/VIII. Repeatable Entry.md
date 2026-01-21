# VIII. Repeatable Entry 🔄

> **Sumber:** [https://filamentphp.com/docs/5.x/infolists/repeatable-entry](https://filamentphp.com/docs/5.x/infolists/repeatable-entry)

---

## 🤔 Apa itu RepeatableEntry?

**RepeatableEntry** menampilkan data berulang seperti relasi hasMany atau array.

```php
use Filament\Infolists\Components\RepeatableEntry;

RepeatableEntry::make('addresses')
    ->schema([
        TextEntry::make('street'),
        TextEntry::make('city'),
        TextEntry::make('country'),
    ])
```

---

## 📊 Grid Layout

```php
RepeatableEntry::make('features')
    ->schema([...])
    ->grid(2)  // 2 kolom
```

### Responsive Grid

```php
RepeatableEntry::make('items')
    ->schema([...])
    ->grid([
        'default' => 1,
        'md' => 2,
        'lg' => 3,
    ])
```

---

## 🎨 Remove Container

```php
RepeatableEntry::make('tags')
    ->schema([...])
    ->contained(false)
```

---

## 📋 Table Layout

```php
RepeatableEntry::make('order_items')
    ->table()
    ->schema([
        TextEntry::make('product'),
        TextEntry::make('quantity'),
        TextEntry::make('price')
            ->money('IDR'),
    ])
```

---

## 💡 Contoh Penggunaan

```php
// Alamat user
RepeatableEntry::make('addresses')
    ->label('Alamat')
    ->schema([
        TextEntry::make('label')
            ->badge(),
        TextEntry::make('street'),
        TextEntry::make('city'),
        TextEntry::make('postal_code'),
    ])
    ->grid(2)

// Order items
RepeatableEntry::make('items')
    ->label('Item Pesanan')
    ->table()
    ->schema([
        TextEntry::make('product.name'),
        TextEntry::make('quantity'),
        TextEntry::make('price')
            ->money('IDR'),
        TextEntry::make('subtotal')
            ->money('IDR'),
    ])
```

---

## 🎯 Latihan Mandiri

Buat RepeatableEntry untuk:

- `addresses` dengan grid 2
- `order_items` table layout
- `documents` contained false
