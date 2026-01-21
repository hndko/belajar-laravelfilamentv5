# II. Layouts 📐

> **Sumber:** [https://filamentphp.com/docs/5.x/schemas/layouts](https://filamentphp.com/docs/5.x/schemas/layouts)

---

## 🤔 Apa itu Layout?

**Layout** mengatur posisi dan ukuran komponen dalam schema menggunakan sistem grid.

---

## 📊 Grid System

### Mengatur Jumlah Kolom

```php
use Filament\Schemas\Components\Grid;

Grid::make(2)  // 2 kolom
    ->schema([
        TextInput::make('first_name'),
        TextInput::make('last_name'),
    ])
```

### Responsive Columns

```php
Grid::make([
    'default' => 1,
    'sm' => 2,
    'md' => 3,
    'lg' => 4,
])
```

---

## 📏 Column Span

### Span Kolom

```php
TextInput::make('description')
    ->columnSpan(2)  // Ambil 2 kolom

TextInput::make('notes')
    ->columnSpanFull()  // Full width
```

### Responsive Span

```php
TextInput::make('address')
    ->columnSpan([
        'default' => 1,
        'md' => 2,
    ])
```

---

## 📍 Column Start

Mulai dari kolom tertentu:

```php
TextInput::make('phone')
    ->columnStart(2)  // Mulai dari kolom 2
```

---

## 🔀 Column Ordering

```php
TextInput::make('mobile')
    ->columnOrder([
        'default' => 1,
        'md' => 2,
    ])
```

---

## 📦 Layout Components

### Grid Component

```php
use Filament\Schemas\Components\Grid;

Grid::make(3)
    ->schema([
        TextInput::make('a'),
        TextInput::make('b'),
        TextInput::make('c'),
    ])
```

### Flex Component

```php
use Filament\Schemas\Components\Flex;

Flex::make([
    TextInput::make('name'),
    TextInput::make('email'),
])->gap(4)
```

### Fieldset Component

```php
use Filament\Schemas\Components\Fieldset;

Fieldset::make('Alamat')
    ->schema([
        TextInput::make('city'),
        TextInput::make('country'),
    ])
```

---

## 📐 Container Queries

Responsive berdasarkan container, bukan viewport:

```php
TextInput::make('name')
    ->columnSpan([
        '@md' => 2,  // @ prefix untuk container query
    ])
```

---

## 📏 Mengatur Spacing

### Kurangi Space

```php
Grid::make()
    ->compactSpacing()
```

### Hilangkan Space

```php
Grid::make()
    ->withoutSpacing()
```

---

## 🎯 Latihan Mandiri

Buat layout responsive:

- 1 kolom di mobile
- 2 kolom di tablet
- 3 kolom di desktop
