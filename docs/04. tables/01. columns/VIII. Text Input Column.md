# IX. Text Input Column ⌨️

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/columns/text-input](https://filamentphp.com/docs/5.x/tables/columns/text-input)

---

## 🤔 Apa itu TextInputColumn?

**TextInputColumn** adalah input field yang bisa diedit langsung di tabel.

```php
use Filament\Tables\Columns\TextInputColumn;

TextInputColumn::make('quantity')
```

---

## ✅ Validasi

```php
TextInputColumn::make('price')
    ->rules(['required', 'numeric', 'min:0'])
```

---

## 🔢 Input Type

```php
TextInputColumn::make('quantity')
    ->type('number')

TextInputColumn::make('date')
    ->type('date')
```

---

## 🏷️ Affix (Prefix/Suffix)

```php
TextInputColumn::make('price')
    ->prefix('Rp')

TextInputColumn::make('percentage')
    ->suffix('%')
```

### Dengan Icon

```php
TextInputColumn::make('website')
    ->prefixIcon('heroicon-o-globe-alt')
```

---

## ⏳ Lifecycle Hooks

```php
TextInputColumn::make('stock')
    ->afterStateUpdated(function ($record, $state) {
        if ($state <= 10) {
            Notification::make()
                ->warning()
                ->title('Stock rendah!')
                ->send();
        }
    })
```

---

## 🎯 Latihan Mandiri

Buat TextInputColumn untuk `stock` dengan type number dan validasi min:0.
