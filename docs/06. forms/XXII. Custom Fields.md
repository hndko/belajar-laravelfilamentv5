# XXII. Custom Fields 🛠️

> **Sumber:** [https://filamentphp.com/docs/5.x/forms/custom-fields](https://filamentphp.com/docs/5.x/forms/custom-fields)

---

## 🤔 Kapan Pakai Custom Field?

Gunakan custom field ketika field bawaan tidak memenuhi kebutuhan.

---

## 🚀 Membuat Custom Field

```bash
php artisan make:filament-field RangeSlider
```

### File yang Dibuat:

```
app/Filament/Forms/Components/RangeSlider.php
resources/views/filament/forms/components/range-slider.blade.php
```

---

## 📄 Blade View

```blade
{{-- resources/views/filament/forms/components/range-slider.blade.php --}}
<x-dynamic-component
    :component="$getFieldWrapperView()"
    :field="$field"
>
    <div
        x-data="{ state: $wire.$entangle('{{ $getStatePath() }}') }"
    >
        <input
            type="range"
            x-model="state"
            min="0"
            max="100"
        />
        <span x-text="state"></span>
    </div>
</x-dynamic-component>
```

---

## 💉 Akses State Lain

```blade
<div>
    {{ $get('other_field') }}
</div>
```

---

## 📦 Akses Record

```blade
<div>
    {{ $getRecord()->name }}
</div>
```

---

## ⚙️ Configuration Methods

```php
class RangeSlider extends Field
{
    protected string $view = 'filament.forms.components.range-slider';

    protected int $min = 0;
    protected int $max = 100;

    public function min(int $min): static
    {
        $this->min = $min;
        return $this;
    }

    public function max(int $max): static
    {
        $this->max = $max;
        return $this;
    }

    public function getMin(): int
    {
        return $this->min;
    }

    public function getMax(): int
    {
        return $this->max;
    }
}
```

### Pakai di Blade:

```blade
<input
    type="range"
    min="{{ $getMin() }}"
    max="{{ $getMax() }}"
/>
```

### Penggunaan:

```php
RangeSlider::make('rating')
    ->min(1)
    ->max(10)
```

---

## 🎯 Latihan Mandiri

Buat custom field "StarRating" dengan:

- Config untuk max stars (default 5)
- Tampilan bintang yang bisa diklik
