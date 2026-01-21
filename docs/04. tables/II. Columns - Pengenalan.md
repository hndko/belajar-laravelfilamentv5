# II. Columns - Pengenalan 📊

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/columns/overview](https://filamentphp.com/docs/5.x/tables/columns/overview)

---

## 🤔 Apa itu Column?

**Column** adalah komponen untuk menampilkan data di setiap kolom tabel. Setiap kolom menampilkan value dari attribute model atau hasil kalkulasi.

---

## 📋 Jenis-Jenis Column

| Column            | Fungsi                     |
| ----------------- | -------------------------- |
| `TextColumn`      | Teks biasa, tanggal, angka |
| `IconColumn`      | Ikon (boolean, status)     |
| `ImageColumn`     | Gambar                     |
| `ColorColumn`     | Warna                      |
| `SelectColumn`    | Dropdown edit              |
| `ToggleColumn`    | Switch on/off              |
| `TextInputColumn` | Input teks inline          |
| `CheckboxColumn`  | Checkbox inline            |

---

## 🔧 Mengatur State Column

### Dari Attribute Langsung

```php
TextColumn::make('name')
```

### Custom State

```php
TextColumn::make('full_name')
    ->state(fn ($record) => $record->first_name . ' ' . $record->last_name)
```

### Default Value

```php
TextColumn::make('nickname')
    ->default('Tidak ada')
```

---

## 🔗 Data dari Relasi

Gunakan "dot notation":

```php
TextColumn::make('author.name')  // belongsTo
TextColumn::make('tags.name')    // hasMany / belongsToMany
```

---

## 🏷️ Label Column

```php
TextColumn::make('name')
    ->label('Nama Lengkap')
```

---

## 🔀 Sorting

```php
TextColumn::make('name')
    ->sortable()
```

### Sort by Default

```php
$table->defaultSort('created_at', 'desc')
```

---

## 🔍 Searching

```php
TextColumn::make('name')
    ->searchable()
```

### Search di Beberapa Kolom

```php
TextColumn::make('title')
    ->searchable(['title', 'description'])
```

### Individual Search per Column

```php
TextColumn::make('name')
    ->searchable(isIndividual: true)
```

---

## 🖱️ Clickable Cell

### Buka URL

```php
TextColumn::make('website')
    ->url(fn ($record) => $record->website)
    ->openUrlInNewTab()
```

### Trigger Action

```php
TextColumn::make('email')
    ->action(
        Action::make('sendEmail')
            ->action(fn ($record) => Mail::to($record->email)->send(...))
    )
```

---

## 💬 Tooltip

```php
TextColumn::make('description')
    ->tooltip(fn ($record) => $record->full_description)
```

---

## 📏 Alignment

```php
TextColumn::make('price')
    ->alignEnd()  // atau alignCenter(), alignStart()
```

---

## 📊 Lebar Kolom

```php
TextColumn::make('description')
    ->grow()  // Ambil sisa lebar

TextColumn::make('id')
    ->width('100px')
```

---

## 👁️ Hide/Show Column

```php
TextColumn::make('internal_notes')
    ->hidden()

TextColumn::make('secret')
    ->visible(fn () => auth()->user()->isAdmin())
```

### User Toggle Visibility

```php
$table->columns([...])->toggleable()
```

---

## 🗂️ Grouping Columns

```php
use Filament\Tables\Columns\ColumnGroup;

ColumnGroup::make('Address', [
    TextColumn::make('city'),
    TextColumn::make('state'),
    TextColumn::make('country'),
])
```

---

## 💡 Ringkasan

| Method                   | Fungsi                |
| ------------------------ | --------------------- |
| `state()`                | Custom value          |
| `default()`              | Default jika null     |
| `label()`                | Ubah label            |
| `sortable()`             | Bisa disort           |
| `searchable()`           | Bisa dicari           |
| `hidden()` / `visible()` | Sembunyikan/tampilkan |
| `tooltip()`              | Tooltip saat hover    |
| `url()`                  | Buat link             |
| `alignEnd()`             | Rata kanan            |

---

## 🎯 Latihan Mandiri

Buat tabel dengan:

- Kolom `name` yang searchable dan sortable
- Kolom `email` yang clickable (buka mailto:)
- Kolom `price` yang rata kanan
