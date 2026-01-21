# XIV. Tags Input 🏷️

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/tags-input](https://filamentphp.com/docs/5.x/forms/tags-input)

---

## 🤔 Apa itu TagsInput?

**TagsInput** adalah field untuk memasukkan multiple tags.

```php
use Filament\Forms\Components\TagsInput;

TagsInput::make('tags')
```

---

## 📝 Separator

Default disimpan sebagai array. Untuk string comma-separated:

```php
TagsInput::make('tags')
    ->separator(',')
```

---

## 💡 Suggestions

```php
TagsInput::make('tags')
    ->suggestions([
        'PHP',
        'Laravel',
        'Filament',
        'JavaScript',
    ])
```

---

## 🔑 Split Keys

```php
TagsInput::make('tags')
    ->splitKeys(['Tab', ',', ' '])
```

---

## 🏷️ Prefix & Suffix

```php
TagsInput::make('hashtags')
    ->tagPrefix('#')

TagsInput::make('mentions')
    ->tagPrefix('@')
```

---

## 🔀 Reorderable

```php
TagsInput::make('priorities')
    ->reorderable()
```

---

## 🎨 Tag Color

```php
TagsInput::make('status')
    ->color('success')
```

---

## ✅ Validasi

```php
TagsInput::make('tags')
    ->minItems(1)
    ->maxItems(10)
```

---

## 🎯 Latihan Mandiri

Buat TagsInput untuk:

- `tags` dengan suggestions
- `hashtags` dengan prefix #
- `skills` reorderable max 5
