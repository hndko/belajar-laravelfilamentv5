# XVI. Custom Filters 🛠️

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/filters/custom](https://filamentphp.com/docs/5.x/tables/filters/custom)

---

## 🤔 Kapan Pakai Custom Filter?

Gunakan custom filter ketika:

- Butuh form field khusus
- Logic filtering kompleks
- Kombinasi beberapa field

---

## 📋 Custom Schema

```php
use Filament\Forms\Components\DatePicker;
use Filament\Tables\Filters\Filter;

Filter::make('date_range')
    ->schema([
        DatePicker::make('from')
            ->label('Dari'),
        DatePicker::make('until')
            ->label('Sampai'),
    ])
    ->query(function ($query, array $data) {
        return $query
            ->when($data['from'], fn ($q, $date) => $q->whereDate('created_at', '>=', $date))
            ->when($data['until'], fn ($q, $date) => $q->whereDate('created_at', '<=', $date));
    })
```

---

## 📌 Default Values

```php
Filter::make('date_range')
    ->schema([
        DatePicker::make('from')->default(now()->subMonth()),
        DatePicker::make('until')->default(now()),
    ])
```

---

## 🏷️ Active Indicators

Tampilkan badge saat filter aktif:

```php
Filter::make('date_range')
    ->schema([...])
    ->indicateUsing(function (array $data): ?string {
        if (! $data['from'] && ! $data['until']) {
            return null;
        }

        return 'Tanggal: ' . $data['from'] . ' - ' . $data['until'];
    })
```

### Multiple Indicators

```php
Filter::make('date_range')
    ->indicateUsing(function (array $data): array {
        $indicators = [];

        if ($data['from']) {
            $indicators[] = Indicator::make('Dari: ' . $data['from'])
                ->removeField('from');
        }

        if ($data['until']) {
            $indicators[] = Indicator::make('Sampai: ' . $data['until'])
                ->removeField('until');
        }

        return $indicators;
    })
```

---

## 🎯 Latihan Mandiri

Buat custom filter untuk rentang harga (min/max price).
