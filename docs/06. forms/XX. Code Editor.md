# XX. Code Editor 💻

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/code-editor](https://filamentphp.com/docs/5.x/forms/code-editor)

---

## 🤔 Apa itu CodeEditor?

**CodeEditor** adalah field untuk menulis kode dengan syntax highlighting.

```php
use Filament\Forms\Components\CodeEditor;

CodeEditor::make('code')
```

---

## 🎨 Language

```php
CodeEditor::make('html_content')
    ->language('html')

CodeEditor::make('css_styles')
    ->language('css')

CodeEditor::make('js_code')
    ->language('javascript')

CodeEditor::make('php_code')
    ->language('php')

CodeEditor::make('config')
    ->language('json')
```

---

## 📏 Line Wrap

```php
CodeEditor::make('long_code')
    ->lineWrapping()
```

---

## 💡 Contoh Penggunaan

```php
CodeEditor::make('custom_css')
    ->label('Custom CSS')
    ->language('css')
    ->lineWrapping()
    ->helperText('Tambahkan CSS kustom untuk halaman ini')

CodeEditor::make('json_config')
    ->label('Konfigurasi JSON')
    ->language('json')
```

---

## 🎯 Latihan Mandiri

Buat CodeEditor untuk:

- `custom_css` bahasa CSS
- `embed_code` bahasa HTML
- `api_config` bahasa JSON
