# III. Text Column 📝

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/columns/text](https://filamentphp.com/docs/5.x/tables/columns/text)

---

## 🤔 Apa itu TextColumn?

**TextColumn** adalah column paling umum untuk menampilkan teks, angka, tanggal, dan data berbasis teks lainnya.

```php
use Filament\Tables\Columns\TextColumn;

TextColumn::make('name')
```

---

## 🎨 Warna

```php
TextColumn::make('status')
    ->color('danger')  // danger, warning, success, info, primary
```

### Warna Dinamis

```php
TextColumn::make('status')
    ->color(fn ($state) => match ($state) {
        'draft' => 'gray',
        'published' => 'success',
        'rejected' => 'danger',
    })
```

---

## 🎯 Ikon

```php
TextColumn::make('email')
    ->icon('heroicon-o-envelope')
```

### Posisi Ikon

```php
TextColumn::make('email')
    ->icon('heroicon-o-envelope')
    ->iconPosition(IconPosition::After)  // Setelah teks
```

---

## 🏷️ Badge

Tampilkan sebagai badge berwarna:

```php
TextColumn::make('status')
    ->badge()
    ->color(fn ($state) => match ($state) {
        'pending' => 'warning',
        'approved' => 'success',
        'rejected' => 'danger',
    })
```

---

## 📅 Format Tanggal

```php
TextColumn::make('created_at')
    ->dateTime()  // Default format

TextColumn::make('created_at')
    ->dateTime('d M Y H:i')  // Custom format

TextColumn::make('birthday')
    ->date()  // Tanggal saja

TextColumn::make('login_at')
    ->time()  // Waktu saja

TextColumn::make('created_at')
    ->since()  // "3 days ago"
```

### Timezone

```php
TextColumn::make('created_at')
    ->dateTime()
    ->timezone('Asia/Jakarta')
```

---

## 🔢 Format Angka

```php
TextColumn::make('quantity')
    ->numeric()

TextColumn::make('price')
    ->numeric(decimalPlaces: 2)
```

---

## 💰 Format Uang (Currency)

```php
TextColumn::make('price')
    ->money('IDR')  // Rp 100.000

TextColumn::make('total')
    ->money('USD', locale: 'en_US')  // $100.00
```

---

## 📝 Deskripsi

Tampilkan teks kecil di bawah nilai utama:

```php
TextColumn::make('name')
    ->description(fn ($record) => $record->job_title)
```

### Posisi Deskripsi

```php
TextColumn::make('name')
    ->description(fn ($record) => $record->email, position: 'above')
```

---

## 📋 Multiple Values (List)

Untuk data array atau hasMany:

```php
TextColumn::make('tags.name')
    ->listWithLineBreaks()  // Satu per baris

TextColumn::make('categories.name')
    ->bulleted()  // Dengan bullet points

TextColumn::make('items.name')
    ->limitList(3)  // Maksimal 3 item
    ->expandableLimitedList()  // Bisa expand
```

---

## 📏 Ukuran Teks

```php
TextColumn::make('title')
    ->size(TextColumn\TextColumnSize::Large)
```

### Weight

```php
TextColumn::make('name')
    ->weight(FontWeight::Bold)
```

### Font Family

```php
TextColumn::make('code')
    ->fontFamily(FontFamily::Mono)
```

---

## ✂️ Handling Teks Panjang

### Limit Karakter

```php
TextColumn::make('description')
    ->limit(50)  // Potong setelah 50 karakter
    ->tooltip(fn ($record) => $record->description)  // Lihat full di tooltip
```

### Limit Kata

```php
TextColumn::make('content')
    ->words(10)
```

### Wrap (Bungkus Teks)

```php
TextColumn::make('description')
    ->wrap()
```

---

## 📋 Copy to Clipboard

```php
TextColumn::make('api_key')
    ->copyable()
    ->copyMessage('API Key copied!')
```

---

## 💡 Ringkasan

| Method          | Fungsi               |
| --------------- | -------------------- |
| `color()`       | Warna teks           |
| `icon()`        | Tambah ikon          |
| `badge()`       | Tampil sebagai badge |
| `dateTime()`    | Format tanggal       |
| `money()`       | Format uang          |
| `numeric()`     | Format angka         |
| `limit()`       | Batasi karakter      |
| `description()` | Teks tambahan        |
| `copyable()`    | Bisa copy            |

---

## 🎯 Latihan Mandiri

Buat tabel Order dengan:

- `order_number` dengan copyable
- `status` sebagai badge berwarna
- `total` dengan format money IDR
- `created_at` dengan format since ("2 days ago")
