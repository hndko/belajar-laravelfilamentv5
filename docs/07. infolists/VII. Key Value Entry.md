# VII. Key Value Entry 🔑

> **Sumber:** [https://filamentphp.com/docs/5.x/infolists/key-value-entry](https://filamentphp.com/docs/5.x/infolists/key-value-entry)

---

## 🤔 Apa itu KeyValueEntry?

**KeyValueEntry** menampilkan data key-value dalam format tabel.

```php
use Filament\Infolists\Components\KeyValueEntry;

KeyValueEntry::make('meta')
```

---

## 🏷️ Custom Column Labels

```php
KeyValueEntry::make('settings')
    ->keyLabel('Pengaturan')
    ->valueLabel('Nilai')
```

---

## 💡 Contoh Penggunaan

```php
// Meta data
KeyValueEntry::make('meta_data')
    ->label('Meta Data')
    ->keyLabel('Key')
    ->valueLabel('Value')

// Social links
KeyValueEntry::make('social_links')
    ->label('Media Sosial')
    ->keyLabel('Platform')
    ->valueLabel('URL')

// HTTP headers
KeyValueEntry::make('request_headers')
    ->label('Headers')
    ->keyLabel('Header')
    ->valueLabel('Nilai')
```

---

## 🎯 Latihan Mandiri

Buat KeyValueEntry untuk:

- `meta_tags` dengan label custom
- `social_links` untuk media sosial
- `api_headers` untuk HTTP headers
