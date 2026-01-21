# XX. Table Summaries 📊

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/summaries](https://filamentphp.com/docs/5.x/tables/summaries)

---

## 🤔 Apa itu Summary?

**Summary** menampilkan ringkasan data di footer tabel, seperti total, rata-rata, dll.

---

## 📋 Jenis Summarizers

| Summarizer | Fungsi            |
| ---------- | ----------------- |
| `Average`  | Rata-rata         |
| `Count`    | Jumlah            |
| `Range`    | Rentang (min-max) |
| `Sum`      | Total             |

---

## 📈 Average (Rata-rata)

```php
TextColumn::make('price')
    ->summarize(Average::make())
```

---

## 🔢 Count (Jumlah)

```php
TextColumn::make('id')
    ->summarize(Count::make())
```

### Count Icons

```php
IconColumn::make('status')
    ->summarize(
        Count::make()->icons()  // Hitung per icon
    )
```

---

## 📏 Range (Rentang)

```php
TextColumn::make('price')
    ->summarize(Range::make())  // Tampilkan min - max
```

### Date Range

```php
TextColumn::make('created_at')
    ->summarize(Range::make()->dateTime())
```

---

## ➕ Sum (Total)

```php
TextColumn::make('quantity')
    ->summarize(Sum::make())
```

---

## 🏷️ Label

```php
TextColumn::make('price')
    ->summarize(
        Sum::make()->label('Total Harga')
    )
```

---

## 💰 Formatting

```php
TextColumn::make('price')
    ->summarize(
        Sum::make()
            ->money('IDR')
    )

TextColumn::make('percentage')
    ->summarize(
        Average::make()
            ->suffix('%')
    )
```

---

## 🔍 Scoping

Ringkasan berdasarkan subset data:

```php
TextColumn::make('price')
    ->summarize([
        Sum::make()->label('Total Keseluruhan'),
        Sum::make()
            ->label('Total Premium')
            ->scope(fn ($query) => $query->where('is_premium', true)),
    ])
```

---

## 🎯 Latihan Mandiri

Tambahkan summary untuk tabel Order:

- Total jumlah order (Count)
- Total revenue (Sum)
- Average order value (Average)
