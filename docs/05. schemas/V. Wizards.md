# V. Wizards 🧙

> **Sumber:** [https://filamentphp.com/docs/5.x/schemas/wizards](https://filamentphp.com/docs/5.x/schemas/wizards)

---

## 🤔 Apa itu Wizard?

**Wizard** adalah form multi-step yang membimbing user melalui proses bertahap.

```php
use Filament\Schemas\Components\Wizard;

Wizard::make([
    Wizard\Step::make('Data Diri')
        ->schema([
            TextInput::make('name'),
            TextInput::make('email'),
        ]),
    Wizard\Step::make('Alamat')
        ->schema([
            TextInput::make('city'),
            TextInput::make('country'),
        ]),
    Wizard\Step::make('Konfirmasi')
        ->schema([
            Checkbox::make('agree'),
        ]),
])
```

---

## 📤 Submit Button di Step Terakhir

```php
Wizard::make([...])
    ->submitAction(
        Action::make('submit')
            ->label('Kirim')
            ->submit('create')
    )
```

---

## 🎯 Step Icon

```php
Wizard\Step::make('Account')
    ->icon('heroicon-o-user')
    ->schema([...])
```

### Icon Step Selesai

```php
Wizard\Step::make('Profile')
    ->completedIcon('heroicon-o-check-circle')
```

---

## 📝 Step Description

```php
Wizard\Step::make('Pembayaran')
    ->description('Pilih metode pembayaran Anda')
    ->schema([...])
```

---

## 📌 Default Active Step

```php
Wizard::make([...])
    ->startOnStep(2)
```

---

## ⏭️ Skip Steps

```php
Wizard::make([...])
    ->skippable()
```

---

## 🔗 Persist di URL

```php
Wizard::make([...])
    ->persistStepInQueryString('step')
```

---

## ⏳ Lifecycle Hooks

### Before & After Step

```php
Wizard\Step::make('Data')
    ->beforeValidation(function () {
        // Sebelum validasi
    })
    ->afterValidation(function () {
        // Setelah validasi sukses
    })
```

### Prevent Next Step

```php
Wizard\Step::make('Verification')
    ->afterValidation(function (Component $component) {
        if (! $this->isVerified()) {
            $component->halt();

            Notification::make()
                ->danger()
                ->title('Verifikasi gagal')
                ->send();
        }
    })
```

---

## 📊 Grid dalam Step

```php
Wizard\Step::make('Details')
    ->columns(2)
    ->schema([...])
```

---

## 🎨 Custom Actions

```php
Wizard::make([...])
    ->nextAction(fn (Action $action) => $action->label('Lanjut'))
    ->previousAction(fn (Action $action) => $action->label('Kembali'))
```

---

## 🎯 Latihan Mandiri

Buat wizard pendaftaran dengan 3 step:

1. "Akun" - email dan password
2. "Profil" - nama dan foto
3. "Konfirmasi" - checkbox terima syarat
