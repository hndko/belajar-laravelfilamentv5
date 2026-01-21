# IV. Checkbox ☑️

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/checkbox](https://filamentphp.com/docs/5.x/forms/checkbox)

---

## 🤔 Apa itu Checkbox?

**Checkbox** adalah kotak centang untuk nilai boolean (true/false).

```php
use Filament\Forms\Components\Checkbox;

Checkbox::make('is_active')
```

---

## 🏷️ Label Position

```php
Checkbox::make('agree')
    ->label('Saya setuju dengan syarat dan ketentuan')
```

### Label di Atas

```php
Checkbox::make('newsletter')
    ->label('Langganan newsletter')
    ->labelAbove()
```

---

## ✅ Validasi

### Accepted

```php
Checkbox::make('terms')
    ->accepted()  // Harus dicentang
```

### Declined

```php
Checkbox::make('opt_out')
    ->declined()  // Harus tidak dicentang
```

---

## 💡 Contoh Penggunaan

```php
Checkbox::make('is_featured')
    ->label('Tampilkan di halaman utama')

Checkbox::make('send_notification')
    ->label('Kirim notifikasi email')
    ->default(true)

Checkbox::make('terms_accepted')
    ->label('Saya setuju dengan syarat dan ketentuan')
    ->accepted()
    ->validationMessages([
        'accepted' => 'Anda harus menyetujui syarat dan ketentuan.',
    ])
```

---

## 🎯 Latihan Mandiri

Buat form dengan:

- `is_active` default true
- `is_featured` untuk produk
- `terms` yang wajib dicentang
