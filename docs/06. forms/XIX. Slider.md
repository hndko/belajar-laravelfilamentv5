# XIX. Slider 📊

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/slider](https://filamentphp.com/docs/5.x/forms/slider)

---

## 🤔 Apa itu Slider?

**Slider** adalah field untuk memilih nilai dengan menggeser handle.

```php
use Filament\Forms\Components\Slider;

Slider::make('volume')
```

---

## 📏 Range

```php
Slider::make('price')
    ->min(0)
    ->max(1000)
```

---

## 🔢 Step

```php
Slider::make('quantity')
    ->min(0)
    ->max(100)
    ->step(5)  // Increment 5
```

---

## 📊 Multiple Handles (Range)

```php
Slider::make('price_range')
    ->range()  // Min dan Max handle
```

---

## ↕️ Vertical

```php
Slider::make('level')
    ->vertical()
    ->height('200px')
```

---

## 💬 Tooltip

```php
Slider::make('brightness')
    ->tooltip()
```

### Custom Tooltip Format

```php
Slider::make('price')
    ->tooltip()
    ->tooltipFormat(fn ($value) => 'Rp ' . number_format($value))
```

---

## 🎨 Fill Track

```php
Slider::make('progress')
    ->fill()
```

---

## 📍 Pips (Marks)

```php
Slider::make('rating')
    ->min(1)
    ->max(5)
    ->pips()
```

---

## 💡 Contoh Penggunaan

```php
Slider::make('budget')
    ->label('Budget')
    ->min(100000)
    ->max(10000000)
    ->step(100000)
    ->tooltip()
    ->tooltipFormat(fn ($value) => 'Rp ' . number_format($value))
    ->fill()
```

---

## 🎯 Latihan Mandiri

Buat Slider untuk:

- `volume` 0-100 dengan tooltip
- `price_range` range dengan pips
- `rating` 1-5 dengan step 1
