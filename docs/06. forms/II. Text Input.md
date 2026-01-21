# II. Text Input ⌨️

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/text-input](https://filamentphp.com/docs/5.x/forms/text-input)

---

## 🤔 Apa itu TextInput?

**TextInput** adalah field untuk input teks, angka, email, password, dan lainnya.

```php
use Filament\Forms\Components\TextInput;

TextInput::make('name')
```

---

## 🔢 Input Type

```php
TextInput::make('email')
    ->type('email')

TextInput::make('age')
    ->type('number')

TextInput::make('password')
    ->type('password')
```

### Numeric dengan Step

```php
TextInput::make('price')
    ->numeric()
    ->step(0.01)
```

---

## 🏷️ Prefix & Suffix

```php
TextInput::make('price')
    ->prefix('Rp')

TextInput::make('domain')
    ->suffix('.com')
```

### Dengan Icon

```php
TextInput::make('email')
    ->prefixIcon('heroicon-o-envelope')

TextInput::make('website')
    ->suffixIcon('heroicon-o-globe-alt')
```

---

## 👁️ Password Revealable

```php
TextInput::make('password')
    ->password()
    ->revealable()
```

---

## 📋 Copyable

```php
TextInput::make('api_key')
    ->copyable()
    ->copyMessage('Berhasil disalin!')
```

---

## 🎭 Input Mask

```php
TextInput::make('phone')
    ->mask('(99) 9999-9999')

TextInput::make('credit_card')
    ->mask('9999 9999 9999 9999')
```

---

## ✂️ Trim Whitespace

```php
TextInput::make('username')
    ->trim()
```

---

## 📖 Read-only

```php
TextInput::make('code')
    ->readOnly()
```

---

## ✅ Validasi

### Panjang

```php
TextInput::make('username')
    ->minLength(3)
    ->maxLength(20)
```

### Angka

```php
TextInput::make('age')
    ->numeric()
    ->minValue(1)
    ->maxValue(150)
```

### Phone

```php
TextInput::make('phone')
    ->tel()
```

---

## 💡 Autocomplete

```php
TextInput::make('email')
    ->autocomplete('email')

TextInput::make('country')
    ->datalist([
        'Indonesia',
        'Malaysia',
        'Singapore',
    ])
```

---

## 🎯 Latihan Mandiri

Buat form dengan:

- `username` min 3 karakter, max 20
- `email` dengan prefix icon envelope
- `price` numeric dengan prefix Rp
- `phone` dengan mask telepon
