# I. Widgets - Pengenalan 📊

> **Sumber:** [https://filamentphp.com/docs/5.x/widgets/overview](https://filamentphp.com/docs/5.x/widgets/overview)

---

## 🤔 Apa itu Widgets?

**Widgets** adalah komponen untuk menampilkan informasi di dashboard. Bisa berupa stats, charts, tables, dll.

---

## 🚀 Membuat Widget

```bash
php artisan make:filament-widget StatsOverview
```

---

## 📋 Sorting Widgets

```php
protected static ?int $sort = 1;  // Urutan widget
```

---

## 🎨 Grid Columns

```php
// Di Dashboard.php
public function getColumns(): int|string|array
{
    return 2;  // 2 kolom
}

// Responsive
public function getColumns(): int|string|array
{
    return [
        'default' => 1,
        'md' => 2,
        'xl' => 3,
    ];
}
```

### Widget Column Span

```php
protected int | string | array $columnSpan = 'full';

// atau
protected int | string | array $columnSpan = [
    'default' => 'full',
    'md' => 1,
];
```

---

## 👁️ Hide Widget

```php
public static function canView(): bool
{
    return auth()->user()->isAdmin();
}
```

---

## 📋 Table Widget

```php
use Filament\Widgets\TableWidget;

class LatestOrders extends TableWidget
{
    protected function getTableQuery(): Builder
    {
        return Order::latest()->limit(5);
    }

    protected function getTableColumns(): array
    {
        return [
            TextColumn::make('number'),
            TextColumn::make('customer.name'),
            TextColumn::make('total'),
        ];
    }
}
```

---

## 🎨 Custom Widget

```php
use Filament\Widgets\Widget;

class WelcomeWidget extends Widget
{
    protected static string $view = 'widgets.welcome';
}
```

---

## 🔍 Filter Widget Data

```php
use Filament\Widgets\Concerns\InteractsWithWidgetFilters;

class StatsWidget extends StatsOverviewWidget
{
    use InteractsWithWidgetFilters;

    public function filterForm(Form $form): Form
    {
        return $form->schema([
            DatePicker::make('start_date'),
            DatePicker::make('end_date'),
        ]);
    }

    protected function getStats(): array
    {
        $start = $this->filters['start_date'] ?? null;
        $end = $this->filters['end_date'] ?? null;

        // Use filters...
    }
}
```

---

## 🎯 Latihan Mandiri

Buat widgets:

- StatsOverview dengan 3 stats
- TableWidget untuk latest orders
- Custom widget dengan view
