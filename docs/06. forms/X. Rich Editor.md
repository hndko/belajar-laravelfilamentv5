# X. Rich Editor 📝

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/rich-editor](https://filamentphp.com/docs/5.x/forms/rich-editor)

---

## 🤔 Apa itu RichEditor?

**RichEditor** adalah editor WYSIWYG untuk konten HTML.

```php
use Filament\Forms\Components\RichEditor;

RichEditor::make('content')
```

---

## 🛠️ Toolbar Buttons

```php
RichEditor::make('content')
    ->toolbarButtons([
        'bold',
        'italic',
        'underline',
        'strike',
        'link',
        'orderedList',
        'bulletList',
        'h2',
        'h3',
        'blockquote',
        'codeBlock',
    ])
```

---

## 🎨 Text Colors

```php
RichEditor::make('content')
    ->colors([
        '#ff0000' => 'Red',
        '#00ff00' => 'Green',
        '#0000ff' => 'Blue',
    ])
```

---

## 🖼️ Upload Images

```php
RichEditor::make('content')
    ->fileAttachmentsDisk('public')
    ->fileAttachmentsDirectory('uploads')
```

### Validasi Image

```php
RichEditor::make('content')
    ->fileAttachmentsDirectory('uploads')
    ->fileAttachmentRules(['max:1024'])  // Max 1MB
```

---

## 📦 Custom Blocks

```php
RichEditor::make('content')
    ->blocks([
        Block::make('callout')
            ->schema([
                Select::make('type')
                    ->options(['info', 'warning', 'danger']),
                Textarea::make('content'),
            ]),
    ])
```

---

## 🏷️ Merge Tags

```php
RichEditor::make('email_template')
    ->mergeTags([
        'name',
        'email',
        'company',
    ])
```

---

## 👥 Mentions

```php
RichEditor::make('comment')
    ->mentions(
        fn () => User::pluck('name', 'id')
    )
```

---

## 🎯 Latihan Mandiri

Buat RichEditor untuk:

- `content` dengan toolbar dasar
- `email_template` dengan merge tags
- `article` dengan image upload
