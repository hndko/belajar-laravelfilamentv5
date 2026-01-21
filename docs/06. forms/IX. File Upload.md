# IX. File Upload 📁

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/file-upload](https://filamentphp.com/docs/5.x/forms/file-upload)

---

## 🤔 Apa itu FileUpload?

**FileUpload** adalah field untuk upload file dan gambar.

```php
use Filament\Forms\Components\FileUpload;

FileUpload::make('attachment')
```

---

## 💾 Storage

```php
FileUpload::make('document')
    ->disk('public')
    ->directory('documents')
```

---

## 📷 Multiple Files

```php
FileUpload::make('gallery')
    ->multiple()
    ->maxFiles(5)
```

---

## 🖼️ Avatar Mode

```php
FileUpload::make('avatar')
    ->avatar()
```

---

## ✂️ Image Editor

```php
FileUpload::make('photo')
    ->image()
    ->imageEditor()
```

### Aspect Ratios

```php
FileUpload::make('banner')
    ->image()
    ->imageEditor()
    ->imageEditorAspectRatios([
        '16:9',
        '4:3',
        '1:1',
    ])
```

### Circle Crop

```php
FileUpload::make('profile')
    ->image()
    ->imageEditor()
    ->circleCropper()
```

---

## 📊 Grid Display

```php
FileUpload::make('photos')
    ->multiple()
    ->panelLayout('grid')
```

---

## 🔀 Reorderable

```php
FileUpload::make('gallery')
    ->multiple()
    ->reorderable()
```

---

## 📥 Downloadable & Previewable

```php
FileUpload::make('document')
    ->downloadable()
    ->previewable()
    ->openable()
```

---

## ✅ Validasi

### File Type

```php
FileUpload::make('document')
    ->acceptedFileTypes(['application/pdf', 'image/*'])
```

### Size

```php
FileUpload::make('image')
    ->maxSize(2048)  // 2MB in KB
```

### Image Dimensions

```php
FileUpload::make('banner')
    ->image()
    ->minWidth(800)
    ->maxWidth(1920)
    ->minHeight(400)
    ->maxHeight(1080)
```

---

## 🎯 Latihan Mandiri

Buat FileUpload untuk:

- `avatar` dengan circle crop
- `gallery` multiple max 5 files
- `document` PDF only, max 5MB
