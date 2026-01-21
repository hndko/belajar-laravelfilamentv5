# I. Schemas - Pengenalan 📐

> **Sumber:** [https://filamentphp.com/docs/5.x/schemas/overview](https://filamentphp.com/docs/5.x/schemas/overview)

---

## 🤔 Apa itu Schema?

**Schema** adalah sistem layout di Filament yang digunakan untuk mengatur tampilan komponen di Forms, Infolists, dan area lainnya. Schema memungkinkan Anda mengatur layout, grid, sections, tabs, dan wizards.

---

## 📋 Komponen yang Tersedia

| Komponen         | Fungsi               |
| ---------------- | -------------------- |
| **Layouts**      | Grid, Flex, Fieldset |
| **Sections**     | Kotak dengan heading |
| **Tabs**         | Navigasi tab         |
| **Wizards**      | Form multi-step      |
| **Empty States** | Tampilan saat kosong |
| **Primes**       | Text, Icon, Image    |
| **Custom**       | Blade view, Livewire |

---

## 📝 Contoh Schema

```php
use Filament\Schemas\Schema;
use Filament\Schemas\Components\Section;
use Filament\Forms\Components\TextInput;

Schema::make([
    Section::make('Informasi Pribadi')
        ->schema([
            TextInput::make('name'),
            TextInput::make('email'),
        ]),
    Section::make('Alamat')
        ->schema([
            TextInput::make('city'),
            TextInput::make('country'),
        ]),
])
```

---

## 💉 Utility Injection

Anda bisa inject berbagai utility ke dalam closure schema:

### State Komponen Lain

```php
TextInput::make('email')
    ->disabled(fn (Get $get) => $get('is_locked'))
```

### Record Eloquent

```php
TextInput::make('name')
    ->default(fn (?Model $record) => $record?->name)
```

### Operation Saat Ini

```php
TextInput::make('password')
    ->required(fn (string $operation) => $operation === 'create')
```

### Livewire Component

```php
TextInput::make('title')
    ->afterStateUpdated(fn (Livewire $livewire) => $livewire->dispatch('titleUpdated'))
```

---

## ⚙️ Global Settings

Konfigurasi default untuk semua schema:

```php
// AppServiceProvider.php
use Filament\Schemas\Components\Section;

Section::configureUsing(function (Section $section) {
    $section->compact();
});
```

---

## 🎯 Latihan Mandiri

Buat schema dengan 2 section: "Data Produk" dan "Harga & Stok".
