# XIII. Tips Kualitas Kode 💎

> **Sumber:** [https://filamentphp.com/docs/5.x/resources/code-quality-tips](https://filamentphp.com/docs/5.x/resources/code-quality-tips)

---

## 🤔 Masalah: File Resource yang Membesar

Seiring waktu, file resource bisa jadi **sangat besar** karena form dan tabel didefinisikan di satu tempat. Ini membuat kode sulit dibaca dan di-maintain.

---

## 📁 Solusi 1: Schema & Table Classes

Filament v5 sudah otomatis membuatkan file terpisah untuk form dan tabel:

```
CustomerResource/
├── CustomerResource.php         ← File utama (kecil)
├── Schemas/
│   └── CustomerForm.php         ← Definisi form
└── Tables/
    └── CustomersTable.php       ← Definisi tabel
```

### Contoh CustomerForm.php:

```php
namespace App\Filament\Resources\Customers\Schemas;

use Filament\Forms\Components\TextInput;
use Filament\Schemas\Schema;

class CustomerForm
{
    public static function configure(Schema $schema): Schema
    {
        return $schema
            ->components([
                TextInput::make('name')->required(),
                TextInput::make('email')->email()->required(),
            ]);
    }
}
```

### Cara Pakai di Resource:

```php
use App\Filament\Resources\Customers\Schemas\CustomerForm;

public static function form(Schema $schema): Schema
{
    return CustomerForm::configure($schema);
}
```

---

## 🧩 Solusi 2: Component Classes

Untuk komponen yang kompleks, buat class khusus:

### Contoh: CustomerNameInput.php

```php
namespace App\Filament\Resources\Customers\Schemas\Components;

use Filament\Forms\Components\TextInput;

class CustomerNameInput
{
    public static function make(): TextInput
    {
        return TextInput::make('name')
            ->label('Nama Lengkap')
            ->required()
            ->maxLength(255)
            ->placeholder('Masukkan nama lengkap')
            ->helperText('Nama yang akan ditampilkan di profil');
    }
}
```

### Cara Pakai:

```php
use App\Filament\Resources\Customers\Schemas\Components\CustomerNameInput;

public static function configure(Schema $schema): Schema
{
    return $schema
        ->components([
            CustomerNameInput::make(),
            // Component lainnya...
        ]);
}
```

---

## 📂 Struktur Folder yang Disarankan

```
CustomerResource/
├── CustomerResource.php
├── Schemas/
│   ├── CustomerForm.php
│   ├── CustomerInfolist.php
│   └── Components/
│       ├── CustomerNameInput.php
│       └── CustomerEmailInput.php
├── Tables/
│   ├── CustomersTable.php
│   ├── Columns/
│   │   └── CustomerNameColumn.php
│   └── Filters/
│       └── CustomerStatusFilter.php
├── Actions/
│   ├── EmailCustomerAction.php
│   └── ExportCustomersBulkAction.php
└── Pages/
    ├── ListCustomers.php
    ├── CreateCustomer.php
    └── EditCustomer.php
```

---

## 🎯 Contoh Action Class

```php
namespace App\Filament\Resources\Customers\Actions;

use App\Models\Customer;
use Filament\Actions\Action;
use Filament\Forms\Components\Textarea;
use Filament\Forms\Components\TextInput;

class EmailCustomerAction
{
    public static function make(): Action
    {
        return Action::make('email')
            ->label('Kirim Email')
            ->icon('heroicon-o-envelope')
            ->schema([
                TextInput::make('subject')->required(),
                Textarea::make('body')->required()->rows(5),
            ])
            ->action(function (Customer $customer, array $data) {
                // Logic kirim email
            });
    }
}
```

---

## 💡 Ringkasan Tips

| Masalah               | Solusi                   |
| --------------------- | ------------------------ |
| Form terlalu panjang  | Pisahkan ke Schema class |
| Tabel terlalu panjang | Pisahkan ke Table class  |
| Input berulang        | Buat Component class     |
| Action kompleks       | Buat Action class        |
| Filter berulang       | Buat Filter class        |

---

## ✅ Keuntungan Struktur Ini

1. **Mudah dibaca** → Setiap file fokus pada satu hal
2. **Reusable** → Component bisa dipakai di resource lain
3. **Mudah test** → Setiap class bisa di-test terpisah
4. **Mudah maintain** → Perubahan terisolasi

---

## 🎯 Latihan Mandiri

1. Pisahkan form ProductResource ke file `ProductForm.php`
2. Buat component `PriceInput` yang bisa dipakai di berbagai resource
3. Buat action `ExportProductsAction` untuk export ke CSV
