# VIII. Custom Components 🛠️

> **Sumber:** [https://filamentphp.com/docs/5.x/schemas/custom-components](https://filamentphp.com/docs/5.x/schemas/custom-components)

---

## 🤔 Kapan Pakai Custom Component?

Gunakan custom component ketika komponen bawaan tidak memenuhi kebutuhan atau Anda perlu menampilkan UI khusus.

---

## 📄 Blade View

```php
use Filament\Schemas\Components\View;

View::make('filament.components.my-custom-component')
```

### Akses State

```blade
{{-- resources/views/filament/components/my-custom-component.blade.php --}}
<div>
    {{ $get('name') }}
</div>
```

### Render Child Schema

```blade
<div class="p-4 bg-gray-100 rounded">
    {{ $getChildComponentContainer() }}
</div>
```

### Akses Record

```blade
<div>
    <h3>{{ $getRecord()->name }}</h3>
    <p>{{ $getRecord()->email }}</p>
</div>
```

### Akses Operation

```blade
@if ($getOperation() === 'create')
    <p>Anda sedang membuat data baru</p>
@else
    <p>Anda sedang mengedit data</p>
@endif
```

### Akses Livewire

```blade
<button wire:click="$parent.refresh">
    Refresh
</button>
```

---

## ⚡ Livewire Component

```php
use Filament\Schemas\Components\Livewire;

Livewire::make(MyCustomComponent::class)
```

### Passing Parameters

```php
Livewire::make(ProductCard::class, ['productId' => 123])
```

### Lazy Loading

```php
Livewire::make(HeavyComponent::class)
    ->lazy()
```

---

## 🏗️ Custom Component Class

```bash
php artisan make:filament-schema-component MyComponent
```

### File yang Dibuat:

```
app/Filament/Schemas/Components/MyComponent.php
resources/views/filament/schemas/components/my-component.blade.php
```

### Contoh Class:

```php
// app/Filament/Schemas/Components/StatusCard.php

namespace App\Filament\Schemas\Components;

use Filament\Schemas\Components\Component;

class StatusCard extends Component
{
    protected string $view = 'filament.schemas.components.status-card';

    protected ?string $status = null;

    public function status(string $status): static
    {
        $this->status = $status;
        return $this;
    }

    public function getStatus(): ?string
    {
        return $this->status;
    }
}
```

### Blade View:

```blade
{{-- resources/views/filament/schemas/components/status-card.blade.php --}}
<div class="p-4 rounded-lg {{ $getStatus() === 'active' ? 'bg-green-100' : 'bg-red-100' }}">
    <span class="font-bold">Status: {{ $getStatus() }}</span>
</div>
```

### Penggunaan:

```php
StatusCard::make()
    ->status('active')
```

---

## ⚙️ Configuration Method dengan Utility Injection

```php
class UserInfo extends Component
{
    protected string $view = 'filament.schemas.components.user-info';

    protected ?Closure $formatUsing = null;

    public function formatUsing(?Closure $callback): static
    {
        $this->formatUsing = $callback;
        return $this;
    }

    public function getFormattedValue(): string
    {
        return $this->evaluate($this->formatUsing);
    }
}
```

---

## 🎯 Latihan Mandiri

Buat custom component "PriceDisplay" yang:

- Menerima parameter price
- Menampilkan dengan format Rupiah
- Beri warna hijau jika ada diskon
