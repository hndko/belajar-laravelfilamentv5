# II. Menampilkan Data (Listing Records) 📋

> **Sumber:** [https://filamentphp.com/docs/5.x/resources/listing-records](https://filamentphp.com/docs/5.x/resources/listing-records)

---

## 🤔 Apa itu List Page?

**List Page** adalah halaman yang menampilkan semua data dalam bentuk tabel. Ini adalah halaman utama setiap resource.

### Yang Bisa Dilakukan di List Page:

- ✅ Melihat semua data
- ✅ Mencari data (search)
- ✅ Memfilter data
- ✅ Mengurutkan data (sort)
- ✅ Memilih beberapa data (bulk action)
- ✅ Navigasi ke halaman lain (pagination)

---

## 🏷️ Menggunakan Tab untuk Filter

Tab adalah cara cepat untuk memfilter data berdasarkan kondisi tertentu.

### Contoh: Tab Status Pelanggan

```php
// Di file ListCustomers.php

use Filament\Schemas\Components\Tabs\Tab;
use Illuminate\Database\Eloquent\Builder;

public function getTabs(): array
{
    return [
        'all' => Tab::make('Semua'),

        'active' => Tab::make('Aktif')
            ->modifyQueryUsing(fn (Builder $query) =>
                $query->where('active', true)
            ),

        'inactive' => Tab::make('Tidak Aktif')
            ->modifyQueryUsing(fn (Builder $query) =>
                $query->where('active', false)
            ),
    ];
}
```

### Analoginya:

Bayangkan tab seperti **folder** di lemari arsip. Folder "Semua" berisi semua dokumen, folder "Aktif" hanya berisi yang aktif, dst.

---

## 🎨 Mengkustomisasi Tab

### Menambah Ikon

```php
use Filament\Schemas\Components\Tabs\Tab;

Tab::make('Aktif')
    ->icon('heroicon-m-check-circle')
```

### Menambah Badge (Jumlah)

```php
Tab::make('Aktif')
    ->badge(Customer::where('active', true)->count())
```

### Mengubah Warna Badge

```php
Tab::make('Aktif')
    ->badge(Customer::where('active', true)->count())
    ->badgeColor('success')
```

### Posisi Ikon

```php
use Filament\Support\Enums\IconPosition;

Tab::make('Aktif')
    ->icon('heroicon-m-check-circle')
    ->iconPosition(IconPosition::After) // Ikon di belakang text
```

---

## 🔍 Mengkustomisasi Query Tabel

Kamu bisa memodifikasi query Eloquent untuk tabel:

```php
use Filament\Tables\Table;
use Illuminate\Database\Eloquent\Builder;

public static function table(Table $table): Table
{
    return $table
        ->modifyQueryUsing(fn (Builder $query) =>
            $query->where('company_id', auth()->user()->company_id)
        );
}
```

### Contoh Penggunaan:

- Filter berdasarkan user yang login
- Hanya tampilkan data tertentu
- Hapus global scope

---

## 🔒 Authorization

Halaman List menggunakan method `viewAny()` dari Policy:

```php
// CustomerPolicy.php
public function viewAny(User $user): bool
{
    return $user->hasRole(['admin', 'staff']);
}
```

**Jika return `false`:** Resource tidak muncul di menu dan tidak bisa diakses.

---

## 📝 Custom Page Content

Kamu bisa menambah konten custom di halaman List:

```php
use Filament\Schemas\Components\EmbeddedTable;
use Filament\Schemas\Components\RenderHook;
use Filament\Schemas\Schema;

public function content(Schema $schema): Schema
{
    return $schema
        ->components([
            // Konten sebelum tabel
            $this->getTabsContentComponent(),

            RenderHook::make(PanelsRenderHook::RESOURCE_PAGES_LIST_RECORDS_TABLE_BEFORE),

            // Tabel utama
            EmbeddedTable::make(),

            // Konten setelah tabel
            RenderHook::make(PanelsRenderHook::RESOURCE_PAGES_LIST_RECORDS_TABLE_AFTER),
        ]);
}
```

---

## 💡 Ringkasan

| Fitur             | Method/Property      |
| ----------------- | -------------------- |
| Tambah tab filter | `getTabs()`          |
| Modifikasi query  | `modifyQueryUsing()` |
| Custom content    | `content()`          |
| Authorization     | Policy `viewAny()`   |

---

## 🎯 Latihan Mandiri

1. Tambahkan tab filter ke resource Product:
   - Tab "Semua"
   - Tab "Harga Mahal" (price > 100000)
   - Tab "Harga Murah" (price <= 100000)

2. Tambahkan badge yang menunjukkan jumlah di setiap tab

<details>
<summary>Contoh Jawaban</summary>

```php
// Di file ListProducts.php

public function getTabs(): array
{
    return [
        'all' => Tab::make('Semua')
            ->badge(Product::count()),

        'expensive' => Tab::make('Harga Mahal')
            ->modifyQueryUsing(fn (Builder $query) =>
                $query->where('price', '>', 100000)
            )
            ->badge(Product::where('price', '>', 100000)->count())
            ->badgeColor('danger'),

        'cheap' => Tab::make('Harga Murah')
            ->modifyQueryUsing(fn (Builder $query) =>
                $query->where('price', '<=', 100000)
            )
            ->badge(Product::where('price', '<=', 100000)->count())
            ->badgeColor('success'),
    ];
}
```

</details>
