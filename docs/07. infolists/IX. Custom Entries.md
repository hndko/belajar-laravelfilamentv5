# IX. Custom Entries 🛠️

> **Sumber:** [https://filamentphp.com/docs/5.x/infolists/custom-entries](https://filamentphp.com/docs/5.x/infolists/custom-entries)

---

## 🤔 Kapan Pakai Custom Entry?

Gunakan custom entry ketika entry bawaan tidak memenuhi kebutuhan tampilan.

---

## 🚀 Membuat Custom Entry

```bash
php artisan make:filament-infolist-entry StatusBadge
```

### File yang Dibuat:

```
app/Filament/Infolists/Components/StatusBadge.php
resources/views/filament/infolists/components/status-badge.blade.php
```

---

## 📄 Blade View

```blade
{{-- resources/views/filament/infolists/components/status-badge.blade.php --}}
<x-dynamic-component
    :component="$getEntryWrapperView()"
    :entry="$entry"
>
    <div class="flex items-center gap-2">
        <span class="px-2 py-1 rounded {{ $getState() === 'active' ? 'bg-green-100 text-green-800' : 'bg-red-100 text-red-800' }}">
            {{ $getState() }}
        </span>
    </div>
</x-dynamic-component>
```

---

## 💉 Akses State

```blade
<div>
    {{ $getState() }}
</div>
```

---

## 📦 Akses State Lain

```blade
<div>
    {{ $get('name') }}
</div>
```

---

## 📦 Akses Record

```blade
<div>
    {{ $getRecord()->name }}
    {{ $getRecord()->created_at->format('d M Y') }}
</div>
```

---

## ⚙️ Configuration Methods

```php
class RatingStars extends Entry
{
    protected string $view = 'filament.infolists.components.rating-stars';

    protected int $maxStars = 5;

    public function maxStars(int $max): static
    {
        $this->maxStars = $max;
        return $this;
    }

    public function getMaxStars(): int
    {
        return $this->maxStars;
    }
}
```

### Pakai di Blade:

```blade
@php
    $rating = $getState();
    $maxStars = $getMaxStars();
@endphp

<div class="flex">
    @for ($i = 1; $i <= $maxStars; $i++)
        <span class="{{ $i <= $rating ? 'text-yellow-400' : 'text-gray-300' }}">
            ★
        </span>
    @endfor
</div>
```

### Penggunaan:

```php
RatingStars::make('rating')
    ->maxStars(5)
```

---

## 🎯 Latihan Mandiri

Buat custom entry "ProgressBar" yang:

- Menampilkan progress bar
- Config untuk max value (default 100)
- Warna berbeda berdasarkan persentase
