# XIX. Table Layout 📐

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/layout](https://filamentphp.com/docs/5.x/tables/layout)

---

## 🤔 Masalah Layout Tradisional

Tabel dengan banyak kolom sulit dibaca di mobile. Filament menyediakan solusi responsive.

---

## 📱 Stack (Responsive)

Kolom ditumpuk di mobile:

```php
use Filament\Tables\Columns\Layout\Stack;

$table->columns([
    Stack::make([
        TextColumn::make('name'),
        TextColumn::make('email'),
    ])->space(2),
])
```

---

## ↔️ Split

Bagi kolom menjadi kiri-kanan:

```php
use Filament\Tables\Columns\Layout\Split;

$table->columns([
    Split::make([
        ImageColumn::make('avatar')->circular(),
        Stack::make([
            TextColumn::make('name')->weight(FontWeight::Bold),
            TextColumn::make('email')->color('gray'),
        ]),
    ]),
])
```

---

## 🔲 Grid

Atur lebar kolom dengan grid:

```php
use Filament\Tables\Columns\Layout\Grid;

$table->columns([
    Grid::make([
        TextColumn::make('name'),
        TextColumn::make('email'),
        TextColumn::make('phone'),
    ])->columns(2),
])
```

---

## 📂 Collapsible Content

Sembunyikan detail yang bisa di-expand:

```php
use Filament\Tables\Columns\Layout\Panel;

$table->columns([
    TextColumn::make('name'),
    Panel::make([
        TextColumn::make('description'),
        TextColumn::make('notes'),
    ])->collapsible(),
])
```

---

## 🎴 Grid Layout (Card Style)

Tampilkan sebagai card grid:

```php
$table
    ->contentGrid([
        'md' => 2,
        'xl' => 3,
    ])
```

---

## 📝 Custom HTML

```php
use Filament\Tables\Columns\Layout\View;

View::make('components.product-card')
```

---

## 🎯 Latihan Mandiri

Buat layout responsive untuk tabel User dengan:

- Avatar (circular)
- Name dan Email stacked
- Role sebagai badge
