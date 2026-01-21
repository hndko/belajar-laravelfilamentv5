# II. Stats Overview 📈

> **Sumber:** [https://filamentphp.com/docs/5.x/widgets/stats-overview](https://filamentphp.com/docs/5.x/widgets/stats-overview)

---

## 🤔 Apa itu Stats Overview?

**Stats Overview** menampilkan angka/statistik dalam bentuk kartu.

```bash
php artisan make:filament-widget StatsOverview --stats-overview
```

---

## 📊 Basic Stats

```php
use Filament\Widgets\StatsOverviewWidget;
use Filament\Widgets\StatsOverviewWidget\Stat;

class StatsOverview extends StatsOverviewWidget
{
    protected function getStats(): array
    {
        return [
            Stat::make('Total Users', User::count()),
            Stat::make('Total Orders', Order::count()),
            Stat::make('Revenue', 'Rp ' . number_format(Order::sum('total'))),
        ];
    }
}
```

---

## 📝 Description & Icon

```php
Stat::make('Total Users', User::count())
    ->description('User terdaftar')
    ->descriptionIcon('heroicon-o-user-group')
```

### Trend Description

```php
Stat::make('Revenue', 'Rp 50.000.000')
    ->description('Naik 10% dari bulan lalu')
    ->descriptionIcon('heroicon-o-arrow-trending-up')
    ->descriptionColor('success')
```

---

## 🎨 Color

```php
Stat::make('Pending Orders', Order::where('status', 'pending')->count())
    ->color('warning')
```

---

## 📈 Mini Chart

```php
Stat::make('Revenue', 'Rp 50.000.000')
    ->chart([7, 3, 4, 5, 6, 3, 5, 8])  // Data points
    ->chartColor('success')
```

---

## 🔄 Polling

```php
protected static ?string $pollingInterval = '10s';  // Update tiap 10 detik

// Disable
protected static ?string $pollingInterval = null;
```

---

## 🔗 URL

```php
Stat::make('Orders', Order::count())
    ->url(route('filament.admin.resources.orders.index'))
```

---

## 🎨 Extra Attributes

```php
Stat::make('Revenue', 'Rp 50.000.000')
    ->extraAttributes([
        'class' => 'cursor-pointer',
        'wire:click' => 'showDetails',
    ])
```

---

## 📍 Heading

```php
protected ?string $heading = 'Statistik Hari Ini';
protected ?string $description = 'Data terakhir 24 jam';
```

---

## 🎯 Latihan Mandiri

Buat StatsOverview dengan:

- Total Users dengan icon
- Revenue dengan mini chart
- Pending Orders dengan warning color
