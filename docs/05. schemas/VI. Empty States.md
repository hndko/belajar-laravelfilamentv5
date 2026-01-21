# VI. Empty States 📭

> **Sumber:** [https://filamentphp.com/docs/5.x/schemas/empty-states](https://filamentphp.com/docs/5.x/schemas/empty-states)

---

## 🤔 Apa itu Empty State?

**Empty State** adalah komponen untuk menampilkan pesan ketika tidak ada konten.

```php
use Filament\Schemas\Components\EmptyState;

EmptyState::make()
    ->heading('Tidak ada data')
    ->description('Belum ada item yang ditambahkan.')
```

---

## 🎯 Icon

```php
EmptyState::make()
    ->icon('heroicon-o-document-text')
    ->heading('Tidak ada dokumen')
    ->description('Upload dokumen pertama Anda.')
```

---

## ⚡ Footer Actions

```php
EmptyState::make()
    ->icon('heroicon-o-shopping-bag')
    ->heading('Keranjang kosong')
    ->description('Mulai belanja untuk menambah item.')
    ->footerActions([
        Action::make('browse')
            ->label('Lihat Produk')
            ->url('/products'),
    ])
```

---

## 🎨 Remove Container

```php
EmptyState::make()
    ->contained(false)
    ->heading('Tidak ada notifikasi')
```

---

## 💡 Contoh Penggunaan

### Di Repeater

```php
Repeater::make('items')
    ->schema([...])
    ->emptyState(
        EmptyState::make()
            ->heading('Tidak ada item')
            ->description('Klik tombol di bawah untuk menambah item.')
    )
```

### Di Infolist

```php
RepeatableEntry::make('orders')
    ->schema([...])
    ->emptyState(
        EmptyState::make()
            ->icon('heroicon-o-shopping-cart')
            ->heading('Belum ada pesanan')
    )
```

---

## 🎯 Latihan Mandiri

Buat empty state untuk repeater "Alamat" dengan icon, heading, description, dan action "Tambah Alamat".
