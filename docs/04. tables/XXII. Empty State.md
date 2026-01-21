# XXII. Empty State 📭

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/empty-state](https://filamentphp.com/docs/5.x/tables/empty-state)

---

## 🤔 Apa itu Empty State?

**Empty State** adalah tampilan yang muncul ketika tabel tidak memiliki data.

---

## 📝 Heading

```php
$table->emptyStateHeading('Belum ada produk')
```

---

## 📋 Description

```php
$table->emptyStateDescription('Mulai dengan menambahkan produk pertama Anda.')
```

---

## 🎯 Icon

```php
$table->emptyStateIcon('heroicon-o-shopping-bag')
```

---

## ⚡ Actions

Tambahkan tombol saat kosong:

```php
$table->emptyStateActions([
    CreateAction::make()
        ->label('Buat Produk Pertama')
        ->icon('heroicon-o-plus'),
])
```

---

## 🎨 Custom View

```php
$table->emptyState(view('filament.tables.empty-state'))
```

```blade
{{-- resources/views/filament/tables/empty-state.blade.php --}}
<div class="text-center py-12">
    <img src="/images/empty-box.svg" class="w-32 mx-auto mb-4">
    <h2 class="text-xl font-bold">Belum ada data</h2>
    <p class="text-gray-500">Klik tombol di bawah untuk memulai</p>
</div>
```

---

## 💡 Contoh Lengkap

```php
$table
    ->emptyStateIcon('heroicon-o-document-text')
    ->emptyStateHeading('Belum ada artikel')
    ->emptyStateDescription('Mulai menulis artikel pertama Anda untuk berbagi dengan dunia.')
    ->emptyStateActions([
        CreateAction::make()
            ->label('Tulis Artikel')
            ->icon('heroicon-o-pencil'),
    ])
```

---

## 🎯 Latihan Mandiri

Buat empty state yang menarik untuk tabel Product dengan icon, heading, description, dan action.
