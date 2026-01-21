# XXIII. Validation ✅

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/validation](https://filamentphp.com/docs/5.x/forms/validation)

---

## 🤔 Apa itu Validation?

**Validation** adalah aturan untuk memastikan input user sesuai format yang diharapkan.

---

## 📋 Rule Umum

```php
TextInput::make('name')
    ->required()

TextInput::make('email')
    ->email()

TextInput::make('website')
    ->url()

TextInput::make('slug')
    ->unique()

TextInput::make('password')
    ->confirmed()
```

---

## 📏 String Length

```php
TextInput::make('username')
    ->minLength(3)
    ->maxLength(20)
```

---

## 🔢 Numeric

```php
TextInput::make('age')
    ->numeric()
    ->minValue(1)
    ->maxValue(150)

TextInput::make('price')
    ->gt(0)  // Greater than
    ->lte(1000000)  // Less than or equal
```

---

## 📅 Date

```php
DatePicker::make('start_date')
    ->after('today')
    ->before('end_date')

DatePicker::make('end_date')
    ->afterOrEqual('start_date')
```

---

## 🔗 Exists & Unique

```php
Select::make('category_id')
    ->exists('categories', 'id')

TextInput::make('email')
    ->unique(table: 'users', column: 'email', ignoreRecord: true)
```

---

## 📝 Regex

```php
TextInput::make('phone')
    ->regex('/^[0-9]{10,12}$/')

TextInput::make('slug')
    ->alphaNum()
    ->alphaDash()
```

---

## 🔄 Conditional

```php
TextInput::make('company')
    ->requiredIf('type', 'business')

TextInput::make('personal_id')
    ->requiredUnless('type', 'business')

TextInput::make('spouse_name')
    ->requiredWith('is_married')
```

---

## 🛠️ Custom Rules

```php
TextInput::make('username')
    ->rules(['required', 'string', new CustomRule()])
```

### Inline Rule

```php
TextInput::make('code')
    ->rules([
        fn () => function ($attribute, $value, $fail) {
            if ($value !== strtoupper($value)) {
                $fail('Kode harus huruf kapital.');
            }
        },
    ])
```

---

## 📝 Custom Messages

```php
TextInput::make('email')
    ->required()
    ->email()
    ->validationMessages([
        'required' => 'Email wajib diisi.',
        'email' => 'Format email tidak valid.',
    ])
```

---

## 🏷️ Validation Attribute

```php
TextInput::make('email')
    ->validationAttribute('alamat email')
```

---

## 💡 Ringkasan Rule

| Rule           | Fungsi                           |
| -------------- | -------------------------------- |
| `required()`   | Wajib diisi                      |
| `email()`      | Format email                     |
| `url()`        | Format URL                       |
| `numeric()`    | Angka                            |
| `minLength(n)` | Min karakter                     |
| `maxLength(n)` | Max karakter                     |
| `minValue(n)`  | Min nilai                        |
| `maxValue(n)`  | Max nilai                        |
| `unique()`     | Harus unik                       |
| `exists()`     | Harus ada                        |
| `regex()`      | Pattern regex                    |
| `confirmed()`  | Harus sama dengan \_confirmation |

---

## 🎯 Latihan Mandiri

Buat validasi untuk:

- `username` min 3, max 20, alphanumeric, unique
- `email` required, email, unique
- `password` required, min 8, confirmed
- `age` numeric, min 17, max 100
