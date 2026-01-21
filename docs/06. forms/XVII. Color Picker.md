# XVII. Color Picker 🎨

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/color-picker](https://filamentphp.com/docs/5.x/forms/color-picker)

---

## 🤔 Apa itu ColorPicker?

**ColorPicker** adalah field untuk memilih warna.

```php
use Filament\Forms\Components\ColorPicker;

ColorPicker::make('color')
```

---

## 📝 Format

```php
ColorPicker::make('color')
    ->hex()  // #ffffff

ColorPicker::make('color')
    ->rgb()  // rgb(255, 255, 255)

ColorPicker::make('color')
    ->rgba()  // rgba(255, 255, 255, 1)

ColorPicker::make('color')
    ->hsl()  // hsl(0, 100%, 50%)
```

---

## ✅ Validasi

```php
ColorPicker::make('brand_color')
    ->required()
```

---

## 💡 Contoh Penggunaan

```php
ColorPicker::make('primary_color')
    ->label('Warna Utama')
    ->hex()

ColorPicker::make('background_color')
    ->label('Warna Background')
    ->rgba()
    ->default('rgba(255, 255, 255, 1)')
```

---

## 🎯 Latihan Mandiri

Buat form tema dengan:

- `primary_color` hex
- `secondary_color` hex
- `background_color` rgba
