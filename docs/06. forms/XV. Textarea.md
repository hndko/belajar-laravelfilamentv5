# XV. Textarea 📝

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/textarea](https://filamentphp.com/docs/5.x/forms/textarea)

---

## 🤔 Apa itu Textarea?

**Textarea** adalah field untuk input teks panjang multi-line.

```php
use Filament\Forms\Components\Textarea;

Textarea::make('description')
```

---

## 📏 Resize

```php
Textarea::make('notes')
    ->rows(5)
    ->cols(50)
```

### Disable Resize

```php
Textarea::make('content')
    ->resize(false)
```

---

## 🔄 Autosize

Tinggi otomatis menyesuaikan konten:

```php
Textarea::make('bio')
    ->autosize()
```

---

## 📖 Read-only

```php
Textarea::make('terms')
    ->readOnly()
```

---

## ✂️ Trim Whitespace

```php
Textarea::make('content')
    ->trim()
```

---

## ✅ Validasi

```php
Textarea::make('description')
    ->minLength(10)
    ->maxLength(1000)
```

---

## 💡 Contoh Penggunaan

```php
Textarea::make('address')
    ->label('Alamat Lengkap')
    ->rows(3)
    ->required()

Textarea::make('bio')
    ->label('Tentang Saya')
    ->autosize()
    ->maxLength(500)
    ->helperText('Maksimal 500 karakter')
```

---

## 🎯 Latihan Mandiri

Buat Textarea untuk:

- `address` 3 rows
- `bio` autosize max 500 karakter
- `notes` opsional
