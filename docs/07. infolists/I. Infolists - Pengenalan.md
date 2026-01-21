# I. Infolists - Pengenalan 📋

> **Sumber:** [https://filamentphp.com/docs/5.x/infolists/overview](https://filamentphp.com/docs/5.x/infolists/overview)

---

## 🤔 Apa itu Infolist?

**Infolist** adalah komponen untuk menampilkan data dalam format read-only. Berbeda dengan Forms yang untuk input, Infolists untuk display data.

---

## 📋 Contoh Penggunaan

Infolist biasanya digunakan di:

- Halaman View record
- Modal detail
- Sidebar informasi
- Dashboard cards

---

## 📝 Defining Entries

```php
use Filament\Infolists\Infolist;
use Filament\Infolists\Components\TextEntry;

Infolist::make()
    ->record($this->record)
    ->schema([
        TextEntry::make('name'),
        TextEntry::make('email'),
        TextEntry::make('created_at')
            ->dateTime(),
    ])
```

---

## 🔧 Entry State

### Custom State

```php
TextEntry::make('full_name')
    ->state(fn ($record) => $record->first_name . ' ' . $record->last_name)
```

### Default State

```php
TextEntry::make('nickname')
    ->default('Tidak ada')
```

---

## 🏷️ Label

```php
TextEntry::make('email')
    ->label('Alamat Email')
```

### Sembunyikan Label

```php
TextEntry::make('bio')
    ->hiddenLabel()
```

---

## 🔗 URL

```php
TextEntry::make('website')
    ->url(fn ($record) => $record->website)
    ->openUrlInNewTab()
```

---

## 👁️ Hidden

```php
TextEntry::make('secret')
    ->hidden()

TextEntry::make('admin_notes')
    ->visible(fn () => auth()->user()->isAdmin())
```

---

## ↔️ Inline Label

```php
TextEntry::make('status')
    ->inlineLabel()
```

---

## 💬 Tooltip

```php
TextEntry::make('description')
    ->tooltip('Deskripsi lengkap produk')
```

---

## 📏 Alignment

```php
TextEntry::make('price')
    ->alignEnd()
```

---

## 💉 Utility Injection

```php
TextEntry::make('status')
    ->color(fn ($state) => match ($state) {
        'active' => 'success',
        'inactive' => 'danger',
    })
```

---

## 🎯 Latihan Mandiri

Buat infolist untuk User dengan:

- `name` dengan label "Nama Lengkap"
- `email` dengan icon
- `created_at` format datetime
- `status` sebagai badge
