# VI. Code Entry 💻

> **Sumber:** [https://filamentphp.com/docs/5.x/infolists/code-entry](https://filamentphp.com/docs/5.x/infolists/code-entry)

---

## 🤔 Apa itu CodeEntry?

**CodeEntry** menampilkan kode dengan syntax highlighting.

```php
use Filament\Infolists\Components\CodeEntry;

CodeEntry::make('source_code')
```

---

## 🎨 Language (Grammar)

```php
CodeEntry::make('html_content')
    ->language('html')

CodeEntry::make('css_styles')
    ->language('css')

CodeEntry::make('js_code')
    ->language('javascript')

CodeEntry::make('php_code')
    ->language('php')

CodeEntry::make('config')
    ->language('json')
```

---

## 🎨 Theme

```php
CodeEntry::make('code')
    ->language('php')
    ->theme('github-dark')
```

---

## 📋 Copyable

```php
CodeEntry::make('embed_code')
    ->language('html')
    ->copyable()
    ->copyMessage('Kode berhasil disalin!')
```

---

## 💡 Contoh Penggunaan

```php
// Embed code
CodeEntry::make('embed_code')
    ->label('Kode Embed')
    ->language('html')
    ->copyable()

// API response
CodeEntry::make('api_response')
    ->label('Response API')
    ->language('json')

// Custom CSS
CodeEntry::make('custom_css')
    ->label('CSS Kustom')
    ->language('css')
```

---

## 🎯 Latihan Mandiri

Buat CodeEntry untuk:

- `embed_code` HTML dengan copyable
- `api_config` JSON
- `custom_styles` CSS
