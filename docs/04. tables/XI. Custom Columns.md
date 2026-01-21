# XI. Custom Columns 🛠️

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/columns/custom-columns](https://filamentphp.com/docs/5.x/tables/columns/custom-columns)

---

## 🤔 Kapan Pakai Custom Column?

Gunakan custom column ketika column bawaan tidak memenuhi kebutuhan.

---

## 🚀 Membuat Custom Column

```bash
php artisan make:filament-column StatusBadge
```

### File yang Dibuat:

```
app/Filament/Tables/Columns/StatusBadge.php
resources/views/filament/tables/columns/status-badge.blade.php
```

---

## 📄 Akses Data di Blade

### State (Nilai Column)

```blade
{{-- resources/views/filament/tables/columns/status-badge.blade.php --}}
<div>
    {{ $getState() }}
</div>
```

### Record (Model)

```blade
<div>
    {{ $getRecord()->name }}
    {{ $getRecord()->created_at->diffForHumans() }}
</div>
```

### Livewire Component

```blade
<div wire:click="$parent.someMethod">
    {{ $getState() }}
</div>
```

---

## ⚙️ Menambah Configuration Method

```php
// app/Filament/Tables/Columns/StatusBadge.php

class StatusBadge extends Column
{
    protected string $view = 'filament.tables.columns.status-badge';

    protected ?string $badgeSize = 'md';

    public function size(string $size): static
    {
        $this->badgeSize = $size;
        return $this;
    }

    public function getSize(): string
    {
        return $this->badgeSize ?? 'md';
    }
}
```

### Pakai di Blade:

```blade
<span class="badge badge-{{ $getSize() }}">
    {{ $getState() }}
</span>
```

### Pakai di Resource:

```php
StatusBadge::make('status')
    ->size('lg')
```

---

## 💡 Contoh: Progress Bar Column

```php
// app/Filament/Tables/Columns/ProgressBar.php
class ProgressBar extends Column
{
    protected string $view = 'filament.tables.columns.progress-bar';

    protected int $max = 100;

    public function max(int $max): static
    {
        $this->max = $max;
        return $this;
    }

    public function getMax(): int
    {
        return $this->max;
    }
}
```

```blade
{{-- resources/views/filament/tables/columns/progress-bar.blade.php --}}
@php
    $percentage = ($getState() / $getMax()) * 100;
@endphp

<div class="w-full bg-gray-200 rounded-full h-2.5">
    <div class="bg-blue-600 h-2.5 rounded-full" style="width: {{ $percentage }}%"></div>
</div>
<span class="text-xs text-gray-500">{{ $getState() }}/{{ $getMax() }}</span>
```

---

## 🎯 Latihan Mandiri

Buat custom column `StarRating` yang menampilkan bintang berdasarkan nilai 1-5.
