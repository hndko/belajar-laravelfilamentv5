# 06. Advanced Policies & Authorization

## 🛡️ Booking Policy

```bash
php artisan make:policy BookingPolicy --model=Booking
```

Edit `app/Policies/BookingPolicy.php`:

```php
<?php

namespace App\Policies;

use App\Models\Booking;
use App\Models\User;
use Filament\Facades\Filament;

class BookingPolicy
{
    public function viewAny(User $user): bool
    {
        return true;
    }

    public function view(User $user, Booking $booking): bool
    {
        // Vendor: hanya booking di team mereka
        if ($user->isVendor()) {
            return $booking->team_id === Filament::getTenant()?->id;
        }

        // Customer: hanya booking mereka sendiri
        if ($user->role === 'customer') {
            return $booking->customer_id === $user->id;
        }

        // Admin: semua
        return $user->isSuperAdmin();
    }

    public function create(User $user): bool
    {
        return true;
    }

    public function update(User $user, Booking $booking): bool
    {
        // Vendor bisa update booking di team mereka
        if ($user->isVendor()) {
            return $booking->team_id === Filament::getTenant()?->id;
        }

        // Customer hanya bisa cancel jika pending
        if ($user->role === 'customer') {
            return $booking->customer_id === $user->id
                && $booking->status === 'pending';
        }

        return $user->isSuperAdmin();
    }

    public function delete(User $user, Booking $booking): bool
    {
        // Hanya admin yang bisa delete
        return $user->isSuperAdmin();
    }
}
```

## 🔒 Service Policy

```php
<?php

namespace App\Policies;

use App\Models\Service;
use App\Models\User;
use Filament\Facades\Filament;

class ServicePolicy
{
    public function viewAny(User $user): bool
    {
        return true;
    }

    public function view(User $user, Service $service): bool
    {
        if ($user->isVendor()) {
            return $service->team_id === Filament::getTenant()?->id;
        }
        return true;
    }

    public function create(User $user): bool
    {
        return $user->isVendor() || $user->isSuperAdmin();
    }

    public function update(User $user, Service $service): bool
    {
        if ($user->isVendor()) {
            return $service->team_id === Filament::getTenant()?->id;
        }
        return $user->isSuperAdmin();
    }

    public function delete(User $user, Service $service): bool
    {
        if ($user->isVendor()) {
            return $service->team_id === Filament::getTenant()?->id;
        }
        return $user->isSuperAdmin();
    }
}
```

## 📝 Register Policies

Edit `app/Providers/AppServiceProvider.php`:

```php
use Illuminate\Support\Facades\Gate;

public function boot(): void
{
    Gate::policy(Booking::class, BookingPolicy::class);
    Gate::policy(Service::class, ServicePolicy::class);
    Gate::policy(Team::class, TeamPolicy::class);

    // Super admin bypass
    Gate::before(function (User $user, $ability) {
        if ($user->isSuperAdmin()) {
            return true;
        }
    });
}
```

## 🎭 Custom Gates

```php
// Di AppServiceProvider
Gate::define('manage-team', function (User $user, Team $team) {
    return $user->id === $team->owner_id
        || $user->teams()->where('team_id', $team->id)
            ->wherePivot('role', 'admin')->exists();
});

Gate::define('view-reports', function (User $user) {
    return in_array($user->role, ['superadmin', 'admin', 'vendor']);
});
```

## 🔐 Use in Resource

```php
// Di resource
public static function canCreate(): bool
{
    return Gate::allows('create', Service::class);
}

public static function canEdit(Model $record): bool
{
    return Gate::allows('update', $record);
}

public static function canDelete(Model $record): bool
{
    return Gate::allows('delete', $record);
}
```

## ➡️ Selanjutnya

Lanjut ke: [07-realtime.md](07-realtime.md)
