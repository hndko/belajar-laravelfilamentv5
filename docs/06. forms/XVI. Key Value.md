# XVI. Key Value 🔑

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/key-value](https://filamentphp.com/docs/5.x/forms/key-value)

---

## 🤔 Apa itu KeyValue?

**KeyValue** adalah field untuk memasukkan pasangan key-value dinamis.

```php
use Filament\Forms\Components\KeyValue;

KeyValue::make('meta')
```

---

## ➕ Add Rows

```php
KeyValue::make('settings')
    ->addActionLabel('Tambah Setting')
```

### Disable Add

```php
KeyValue::make('config')
    ->addable(false)
```

---

## ❌ Delete Rows

```php
KeyValue::make('data')
    ->deletable(false)
```

---

## 🏷️ Key Label & Placeholder

```php
KeyValue::make('headers')
    ->keyLabel('Header')
    ->keyPlaceholder('Content-Type')
```

### Disable Key Editing

```php
KeyValue::make('predefined')
    ->editableKeys(false)
```

---

## 📝 Value Label & Placeholder

```php
KeyValue::make('headers')
    ->valueLabel('Nilai')
    ->valuePlaceholder('application/json')
```

### Disable Value Editing

```php
KeyValue::make('readonly')
    ->editableValues(false)
```

---

## 🔀 Reorderable

```php
KeyValue::make('priorities')
    ->reorderable()
```

---

## 💡 Contoh Penggunaan

```php
KeyValue::make('social_links')
    ->keyLabel('Platform')
    ->valueLabel('URL')
    ->keyPlaceholder('Instagram')
    ->valuePlaceholder('https://instagram.com/username')
    ->reorderable()
```

---

## 🎯 Latihan Mandiri

Buat KeyValue untuk:

- `meta_tags` untuk SEO
- `api_headers` untuk HTTP headers
- `social_links` reorderable
