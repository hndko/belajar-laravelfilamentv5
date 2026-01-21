# XI. Markdown Editor 📝

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/markdown-editor](https://filamentphp.com/docs/5.x/forms/markdown-editor)

---

## 🤔 Apa itu MarkdownEditor?

**MarkdownEditor** adalah editor untuk menulis konten dalam format Markdown.

```php
use Filament\Forms\Components\MarkdownEditor;

MarkdownEditor::make('content')
```

---

## 🛠️ Toolbar Buttons

```php
MarkdownEditor::make('content')
    ->toolbarButtons([
        'bold',
        'italic',
        'strike',
        'link',
        'heading',
        'bulletList',
        'orderedList',
        'codeBlock',
        'table',
    ])
```

---

## 🖼️ Upload Images

```php
MarkdownEditor::make('content')
    ->fileAttachmentsDisk('public')
    ->fileAttachmentsDirectory('markdown-uploads')
```

### Validasi Image

```php
MarkdownEditor::make('content')
    ->fileAttachmentRules(['image', 'max:1024'])
```

---

## 💡 Contoh Penggunaan

```php
MarkdownEditor::make('readme')
    ->label('README')
    ->toolbarButtons([
        'heading',
        'bold',
        'italic',
        'link',
        'bulletList',
        'orderedList',
        'codeBlock',
    ])
    ->helperText('Tulis dalam format Markdown')
```

---

## 🎯 Latihan Mandiri

Buat MarkdownEditor untuk:

- `documentation` dengan toolbar lengkap
- `notes` dengan image upload
