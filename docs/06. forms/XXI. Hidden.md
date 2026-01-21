# XXI. Hidden 👻

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/hidden](https://filamentphp.com/docs/5.x/forms/hidden)

---

## 🤔 Apa itu Hidden?

**Hidden** adalah field tersembunyi untuk menyimpan data tanpa tampilan.

```php
use Filament\Forms\Components\Hidden;

Hidden::make('user_id')
```

---

## 💡 Contoh Penggunaan

### Set Default Value

```php
Hidden::make('user_id')
    ->default(auth()->id())
```

### Set via Closure

```php
Hidden::make('ip_address')
    ->default(fn () => request()->ip())
```

### Dari Parent Record

```php
Hidden::make('parent_id')
    ->default(fn () => $this->ownerRecord->id)
```

---

## 🎯 Kapan Pakai Hidden?

- Menyimpan `user_id` pembuat record
- Menyimpan `parent_id` untuk relasi
- Data yang dihitung otomatis
- Data dari context (IP, timestamp, dll)

---

## 🎯 Latihan Mandiri

Buat form dengan Hidden untuk:

- `created_by` = user ID yang login
- `ip_address` = IP address request
