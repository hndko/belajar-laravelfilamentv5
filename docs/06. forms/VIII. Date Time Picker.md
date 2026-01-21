# VIII. Date Time Picker 📅

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/date-time-picker](https://filamentphp.com/docs/5.x/forms/date-time-picker)

---

## 🤔 Apa itu DateTimePicker?

**DateTimePicker** adalah field untuk memilih tanggal dan/atau waktu.

```php
use Filament\Forms\Components\DateTimePicker;

DateTimePicker::make('published_at')
```

---

## 📅 Jenis Picker

```php
// Tanggal saja
DatePicker::make('birthday')

// Waktu saja
TimePicker::make('start_time')

// Tanggal + Waktu
DateTimePicker::make('event_at')
```

---

## 📝 Format Penyimpanan

```php
DateTimePicker::make('created_at')
    ->format('Y-m-d H:i:s')
```

---

## ⏱️ Disable Detik

```php
DateTimePicker::make('meeting_at')
    ->seconds(false)
```

---

## 🌍 Timezone

```php
DateTimePicker::make('scheduled_at')
    ->timezone('Asia/Jakarta')
```

---

## 🎨 JavaScript Picker

```php
DateTimePicker::make('date')
    ->native(false)  // Gunakan JS picker
```

### Display Format

```php
DateTimePicker::make('date')
    ->native(false)
    ->displayFormat('d/m/Y')
```

### Time Intervals

```php
DateTimePicker::make('appointment')
    ->native(false)
    ->minutesStep(15)  // Interval 15 menit
```

---

## 🚫 Disable Dates

```php
DateTimePicker::make('booking_date')
    ->native(false)
    ->disabledDates(['2024-12-25', '2024-01-01'])
```

---

## ✅ Validasi

```php
DateTimePicker::make('start_date')
    ->minDate(now())
    ->maxDate(now()->addYear())

DateTimePicker::make('end_date')
    ->afterOrEqual('start_date')
```

---

## 🎯 Latihan Mandiri

Buat form dengan:

- `birthday` DatePicker
- `start_time` TimePicker tanpa detik
- `event_at` DateTimePicker dengan min date hari ini
