# I. Forms - Pengenalan 📝

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/overview](https://filamentphp.com/docs/5.x/forms/overview)

---

## 🤔 Apa itu Forms?

**Forms** adalah komponen untuk membuat form input di Filament. Digunakan untuk create, edit, dan input data lainnya.

---

## 📋 Jenis-Jenis Field

| Field            | Fungsi              |
| ---------------- | ------------------- |
| `TextInput`      | Input teks biasa    |
| `Select`         | Dropdown pilihan    |
| `Checkbox`       | Kotak centang       |
| `Toggle`         | Switch on/off       |
| `DateTimePicker` | Pilih tanggal/waktu |
| `FileUpload`     | Upload file         |
| `RichEditor`     | Editor HTML         |
| `Repeater`       | Item berulang       |

---

## ✅ Validasi

```php
TextInput::make('email')
    ->required()
    ->email()
    ->unique()
```

---

## 🏷️ Label

```php
TextInput::make('name')
    ->label('Nama Lengkap')
```

### Sembunyikan Label

```php
TextInput::make('search')
    ->hiddenLabel()
```

---

## 📌 Default Value

```php
TextInput::make('country')
    ->default('Indonesia')
```

---

## 🔒 Disabled & Hidden

```php
TextInput::make('id')
    ->disabled()

TextInput::make('secret')
    ->hidden()
```

### Berdasarkan Operation

```php
TextInput::make('email')
    ->disabled(fn (string $operation) => $operation === 'edit')

TextInput::make('password')
    ->hidden(fn (string $operation) => $operation === 'edit')
```

---

## 💡 Placeholder

```php
TextInput::make('email')
    ->placeholder('contoh@email.com')
```

---

## 🎯 Autofocus

```php
TextInput::make('name')
    ->autofocus()
```

---

## 💉 Utility Injection

### State Field Lain

```php
TextInput::make('city')
    ->disabled(fn (Get $get) => $get('country') === null)
```

### Current Record

```php
TextInput::make('name')
    ->default(fn (?Model $record) => $record?->name)
```

### Current Operation

```php
TextInput::make('password')
    ->required(fn (string $operation) => $operation === 'create')
```

---

## 🔄 Reactivity

```php
Select::make('country')
    ->live()  // Trigger update saat berubah
    ->afterStateUpdated(fn (Set $set) => $set('city', null))

Select::make('city')
    ->options(fn (Get $get) => City::where('country_id', $get('country'))->pluck('name', 'id'))
```

### On Blur

```php
TextInput::make('username')
    ->live(onBlur: true)
```

---

## 🎯 Latihan Mandiri

Buat form dengan:

- `name` required
- `email` required, email, unique
- `country` select yang live
- `city` select tergantung country
