# III. Chart Widgets 📊

> **Sumber:** [https://filamentphp.com/docs/5.x/widgets/charts](https://filamentphp.com/docs/5.x/widgets/charts)

---

## 🤔 Apa itu Chart Widget?

**Chart Widget** menampilkan data dalam bentuk grafik menggunakan Chart.js.

```bash
php artisan make:filament-widget RevenueChart --chart
```

---

## 📊 Jenis Chart

| Type        | Fungsi         |
| ----------- | -------------- |
| `line`      | Line chart     |
| `bar`       | Bar chart      |
| `pie`       | Pie chart      |
| `doughnut`  | Doughnut chart |
| `polarArea` | Polar area     |
| `radar`     | Radar chart    |
| `bubble`    | Bubble chart   |
| `scatter`   | Scatter plot   |

```php
protected static ?string $chartType = 'line';
```

---

## 📈 Chart Data

```php
use Filament\Widgets\ChartWidget;

class RevenueChart extends ChartWidget
{
    protected static ?string $heading = 'Revenue';

    protected function getData(): array
    {
        return [
            'datasets' => [
                [
                    'label' => 'Revenue',
                    'data' => [100, 200, 300, 400, 500, 600],
                    'backgroundColor' => '#36A2EB',
                    'borderColor' => '#9BD0F5',
                ],
            ],
            'labels' => ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'],
        ];
    }

    protected function getType(): string
    {
        return 'line';
    }
}
```

---

## 🎨 Colors

```php
protected static ?string $chartColor = 'info';  // danger, gray, info, primary, success, warning
```

---

## 📊 Data dari Eloquent

```php
protected function getData(): array
{
    $orders = Order::selectRaw('MONTH(created_at) as month, SUM(total) as revenue')
        ->whereYear('created_at', now()->year)
        ->groupBy('month')
        ->pluck('revenue', 'month');

    return [
        'datasets' => [
            [
                'label' => 'Revenue',
                'data' => $orders->values(),
            ],
        ],
        'labels' => $orders->keys()->map(fn ($m) => date('M', mktime(0, 0, 0, $m, 1))),
    ];
}
```

---

## 🔍 Filter

```php
use Filament\Widgets\Concerns\InteractsWithWidgetFilters;

class RevenueChart extends ChartWidget
{
    public ?string $filter = 'week';

    protected function getFilters(): ?array
    {
        return [
            'today' => 'Hari Ini',
            'week' => 'Minggu Ini',
            'month' => 'Bulan Ini',
            'year' => 'Tahun Ini',
        ];
    }

    protected function getData(): array
    {
        $filter = $this->filter;
        // Use filter to query data...
    }
}
```

---

## 🔄 Polling

```php
protected static ?string $pollingInterval = '15s';
```

---

## 📏 Max Height

```php
protected static ?string $maxHeight = '300px';
```

---

## 📂 Collapsible

```php
protected static bool $isCollapsible = true;
protected static bool $isCollapsed = false;
```

---

## 🎯 Latihan Mandiri

Buat Chart Widget untuk:

- Revenue line chart per bulan
- Orders bar chart dengan filter
- Category pie chart
