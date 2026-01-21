# XI. Widget di Resource 📊

> **Sumber:** [https://filamentphp.com/docs/5.x/resources/widgets](https://filamentphp.com/docs/5.x/resources/widgets)

---

## 🤔 Apa itu Widget di Resource?

**Widget** adalah komponen visual yang bisa ditampilkan di halaman resource, biasanya untuk menampilkan statistik atau informasi ringkasan.

### Posisi Widget:

- **Header** → Di atas konten halaman
- **Footer** → Di bawah konten halaman

---

## 🚀 Membuat Widget untuk Resource

```bash
php artisan make:filament-widget CustomerOverview --resource=CustomerResource
```

### Hasilnya:

```
app/Filament/Resources/Customers/Widgets/CustomerOverview.php
resources/views/filament/resources/customers/widgets/customer-overview.blade.php
```

---

## 📝 Daftarkan Widget di Resource

```php
// CustomerResource.php

use App\Filament\Resources\Customers\Widgets\CustomerOverview;

public static function getWidgets(): array
{
    return [
        CustomerOverview::class,
    ];
}
```

---

## 📍 Tampilkan Widget di Halaman

```php
// ListCustomers.php

protected function getHeaderWidgets(): array
{
    return [
        CustomerResource\Widgets\CustomerOverview::class,
    ];
}

// Atau di footer
protected function getFooterWidgets(): array
{
    return [
        CustomerResource\Widgets\CustomerStats::class,
    ];
}
```

---

## 🎯 Akses Record di Widget

Untuk widget di halaman Edit atau View, kamu bisa akses record:

```php
use Illuminate\Database\Eloquent\Model;

class CustomerOverview extends Widget
{
    public ?Model $record = null;

    protected function getStats(): array
    {
        return [
            Stat::make('Total Orders', $this->record->orders()->count()),
            Stat::make('Total Spent', 'Rp ' . number_format($this->record->orders()->sum('total'))),
        ];
    }
}
```

---

## 📊 Akses Data Tabel di Widget

Untuk widget di halaman List:

```php
use Filament\Widgets\Concerns\InteractsWithPageTable;

class CustomerStats extends StatsOverviewWidget
{
    use InteractsWithPageTable;

    protected function getStats(): array
    {
        return [
            Stat::make('Total Records', $this->getPageTableRecordsCount()),
        ];
    }
}
```

---

## 💡 Ringkasan

| Method               | Lokasi         | Fungsi                   |
| -------------------- | -------------- | ------------------------ |
| `getHeaderWidgets()` | Page class     | Widget di atas           |
| `getFooterWidgets()` | Page class     | Widget di bawah          |
| `getWidgets()`       | Resource class | Daftarkan widget         |
| `$record` property   | Widget class   | Akses record (Edit/View) |

---

## 🎯 Latihan Mandiri

1. Buat widget `ProductStats` untuk ProductResource
2. Tampilkan: Total Products, Average Price, Products in Stock

<details>
<summary>Jawaban</summary>

```php
// ProductStats.php
class ProductStats extends StatsOverviewWidget
{
    protected function getStats(): array
    {
        return [
            Stat::make('Total Produk', Product::count()),
            Stat::make('Rata-rata Harga', 'Rp ' . number_format(Product::avg('price'))),
            Stat::make('Stok Tersedia', Product::where('stock', '>', 0)->count()),
        ];
    }
}
```

</details>
