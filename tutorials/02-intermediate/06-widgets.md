# 06. Dashboard Widgets & Charts

## 📊 Stats Overview Widget

```bash
php artisan make:filament-widget StatsOverview --stats-overview
```

Edit `app/Filament/Widgets/StatsOverview.php`:

```php
<?php

namespace App\Filament\Widgets;

use App\Models\Product;
use App\Models\Supplier;
use App\Models\Transaction;
use Filament\Widgets\StatsOverviewWidget as BaseWidget;
use Filament\Widgets\StatsOverviewWidget\Stat;

class StatsOverview extends BaseWidget
{
    protected function getStats(): array
    {
        $lowStockCount = Product::whereColumn('stock', '<=', 'min_stock')->count();

        return [
            Stat::make('Total Produk', Product::count())
                ->description('Produk terdaftar')
                ->icon('heroicon-o-cube')
                ->color('primary'),

            Stat::make('Total Supplier', Supplier::count())
                ->description('Supplier aktif')
                ->icon('heroicon-o-truck')
                ->color('success'),

            Stat::make('Stok Menipis', $lowStockCount)
                ->description('Perlu restock')
                ->icon('heroicon-o-exclamation-triangle')
                ->color($lowStockCount > 0 ? 'danger' : 'success'),

            Stat::make('Transaksi Hari Ini',
                Transaction::whereDate('created_at', today())->count()
            )
                ->description('Stock in/out')
                ->icon('heroicon-o-arrows-right-left')
                ->color('warning'),
        ];
    }
}
```

## 📈 Chart Widget

```bash
php artisan make:filament-widget TransactionChart --chart
```

Edit `app/Filament/Widgets/TransactionChart.php`:

```php
<?php

namespace App\Filament\Widgets;

use App\Models\Transaction;
use Filament\Widgets\ChartWidget;
use Illuminate\Support\Carbon;

class TransactionChart extends ChartWidget
{
    protected static ?string $heading = 'Transaksi 7 Hari Terakhir';
    protected static ?int $sort = 2;

    protected function getData(): array
    {
        $days = collect(range(6, 0))->map(fn ($day) =>
            Carbon::now()->subDays($day)->format('Y-m-d')
        );

        $stockIn = [];
        $stockOut = [];

        foreach ($days as $date) {
            $stockIn[] = Transaction::where('type', 'in')
                ->whereDate('created_at', $date)
                ->sum('quantity');

            $stockOut[] = Transaction::where('type', 'out')
                ->whereDate('created_at', $date)
                ->sum('quantity');
        }

        return [
            'datasets' => [
                [
                    'label' => 'Stock In',
                    'data' => $stockIn,
                    'backgroundColor' => '#10b981',
                    'borderColor' => '#10b981',
                ],
                [
                    'label' => 'Stock Out',
                    'data' => $stockOut,
                    'backgroundColor' => '#ef4444',
                    'borderColor' => '#ef4444',
                ],
            ],
            'labels' => $days->map(fn ($date) =>
                Carbon::parse($date)->format('d M')
            )->toArray(),
        ];
    }

    protected function getType(): string
    {
        return 'bar';
    }
}
```

## 📋 Low Stock Alert Widget

```bash
php artisan make:filament-widget LowStockAlert --table
```

Edit `app/Filament/Widgets/LowStockAlert.php`:

```php
<?php

namespace App\Filament\Widgets;

use App\Models\Product;
use Filament\Tables;
use Filament\Tables\Table;
use Filament\Widgets\TableWidget as BaseWidget;

class LowStockAlert extends BaseWidget
{
    protected static ?string $heading = '⚠️ Produk Stok Menipis';
    protected static ?int $sort = 3;
    protected int | string | array $columnSpan = 'full';

    public function table(Table $table): Table
    {
        return $table
            ->query(
                Product::whereColumn('stock', '<=', 'min_stock')
            )
            ->columns([
                Tables\Columns\TextColumn::make('sku'),
                Tables\Columns\TextColumn::make('name')
                    ->label('Nama'),
                Tables\Columns\TextColumn::make('supplier.name')
                    ->label('Supplier'),
                Tables\Columns\TextColumn::make('stock')
                    ->label('Stok')
                    ->color('danger'),
                Tables\Columns\TextColumn::make('min_stock')
                    ->label('Min'),
            ])
            ->paginated(false);
    }
}
```

## ➡️ Selanjutnya

Lanjut ke: [07-actions.md](07-actions.md)
