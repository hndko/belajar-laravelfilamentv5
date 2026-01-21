# XVIII. Toggle Buttons 🔘

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/toggle-buttons](https://filamentphp.com/docs/5.x/forms/toggle-buttons)

---

## 🤔 Apa itu ToggleButtons?

**ToggleButtons** adalah pilihan dalam bentuk tombol yang bisa di-toggle.

```php
use Filament\Forms\Components\ToggleButtons;

ToggleButtons::make('status')
    ->options([
        'draft' => 'Draft',
        'published' => 'Published',
        'archived' => 'Archived',
    ])
```

---

## 🎨 Warna

```php
ToggleButtons::make('priority')
    ->options([
        'low' => 'Low',
        'medium' => 'Medium',
        'high' => 'High',
    ])
    ->colors([
        'low' => 'success',
        'medium' => 'warning',
        'high' => 'danger',
    ])
```

---

## 🎯 Icon

```php
ToggleButtons::make('status')
    ->options([...])
    ->icons([
        'draft' => 'heroicon-o-pencil',
        'published' => 'heroicon-o-check',
        'archived' => 'heroicon-o-archive-box',
    ])
```

---

## 🎨 Boolean

```php
ToggleButtons::make('is_active')
    ->boolean()
```

---

## ↔️ Inline

```php
ToggleButtons::make('size')
    ->inline()
    ->options([
        's' => 'S',
        'm' => 'M',
        'l' => 'L',
        'xl' => 'XL',
    ])
```

---

## 📊 Grouped

```php
ToggleButtons::make('view')
    ->grouped()
    ->options([
        'list' => 'List',
        'grid' => 'Grid',
    ])
```

---

## ✅ Multiple

```php
ToggleButtons::make('features')
    ->multiple()
    ->options([
        'wifi' => 'WiFi',
        'ac' => 'AC',
        'pool' => 'Pool',
    ])
```

---

## 📊 Grid

```php
ToggleButtons::make('amenities')
    ->columns(3)
    ->options([...])
```

---

## 🎯 Latihan Mandiri

Buat ToggleButtons untuk:

- `status` dengan warna dan icon
- `size` inline grouped
- `amenities` multiple grid
