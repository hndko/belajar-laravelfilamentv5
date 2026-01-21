# XIII. Builder 🧱

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/builder](https://filamentphp.com/docs/5.x/forms/builder)

---

## 🤔 Apa itu Builder?

**Builder** adalah field untuk membuat konten dinamis dengan berbagai jenis block. Cocok untuk page builder, content blocks, dll.

```php
use Filament\Forms\Components\Builder;
use Filament\Forms\Components\Builder\Block;

Builder::make('content')
    ->blocks([
        Block::make('heading')
            ->schema([
                TextInput::make('content'),
                Select::make('level')
                    ->options([
                        'h2' => 'H2',
                        'h3' => 'H3',
                        'h4' => 'H4',
                    ]),
            ]),
        Block::make('paragraph')
            ->schema([
                RichEditor::make('content'),
            ]),
        Block::make('image')
            ->schema([
                FileUpload::make('image'),
                TextInput::make('alt'),
            ]),
    ])
```

---

## 🏷️ Block Label

```php
Block::make('hero')
    ->label('Hero Section')
```

### Dynamic Label

```php
Block::make('heading')
    ->label(fn (array $state) => $state['content'] ?? 'Heading')
```

---

## 🎯 Block Icon

```php
Block::make('image')
    ->icon('heroicon-o-photo')
```

### Icon di Header

```php
Builder::make('content')
    ->blockIcons()
```

---

## 👁️ Block Preview

```php
Block::make('callout')
    ->preview('filament.blocks.callout-preview')
```

---

## ➕ Add Items

```php
Builder::make('content')
    ->addActionLabel('Tambah Block')
```

---

## 📂 Collapsible

```php
Builder::make('content')
    ->collapsible()
    ->collapsed()
```

---

## 📋 Clone

```php
Builder::make('content')
    ->cloneable()
```

---

## 🎨 Block Picker

```php
Builder::make('content')
    ->blockPickerColumns(2)
    ->blockPickerWidth(MaxWidth::Medium)
```

---

## 🔢 Limit Block Usage

```php
Block::make('hero')
    ->maxItems(1)  // Hanya 1 hero block
```

---

## ✅ Validasi

```php
Builder::make('content')
    ->minItems(1)
    ->maxItems(20)
```

---

## 🎯 Latihan Mandiri

Buat Builder dengan blocks:

- `hero` (heading, subheading, image) max 1
- `text` (rich editor)
- `gallery` (multiple images)
