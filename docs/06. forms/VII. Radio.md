# VII. Radio 🔘

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/radio](https://filamentphp.com/docs/5.x/forms/radio)

---

## 🤔 Apa itu Radio?

**Radio** adalah pilihan tunggal dari beberapa opsi yang terlihat sekaligus.

```php
use Filament\Forms\Components\Radio;

Radio::make('status')
    ->options([
        'draft' => 'Draft',
        'published' => 'Published',
        'archived' => 'Archived',
    ])
```

---

## 📝 Option Descriptions

```php
Radio::make('plan')
    ->options([
        'basic' => 'Basic',
        'pro' => 'Pro',
        'enterprise' => 'Enterprise',
    ])
    ->descriptions([
        'basic' => 'Untuk personal use',
        'pro' => 'Untuk small business',
        'enterprise' => 'Untuk enterprise',
    ])
```

---

## ↔️ Inline

```php
Radio::make('gender')
    ->options([
        'male' => 'Laki-laki',
        'female' => 'Perempuan',
    ])
    ->inline()
```

---

## 🚫 Disable Options

```php
Radio::make('shipping')
    ->options([
        'standard' => 'Standard',
        'express' => 'Express',
        'same_day' => 'Same Day',
    ])
    ->disableOptionWhen(fn ($value) => $value === 'same_day')
```

---

## 🎨 Boolean Options

```php
Radio::make('is_active')
    ->boolean()
```

---

## 💡 Contoh Penggunaan

```php
Radio::make('payment_method')
    ->label('Metode Pembayaran')
    ->options([
        'bank_transfer' => 'Transfer Bank',
        'credit_card' => 'Kartu Kredit',
        'e_wallet' => 'E-Wallet',
    ])
    ->descriptions([
        'bank_transfer' => 'BCA, Mandiri, BNI, BRI',
        'credit_card' => 'Visa, Mastercard',
        'e_wallet' => 'GoPay, OVO, Dana',
    ])
    ->required()
```

---

## 🎯 Latihan Mandiri

Buat Radio untuk:

- `payment_method` dengan descriptions
- `priority` inline (low/medium/high)
- `gender` boolean
