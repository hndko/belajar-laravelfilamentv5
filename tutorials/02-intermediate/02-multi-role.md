# 02. Multi-Role Implementation

## 🔐 Step 1: Update User Model

Edit `app/Models/User.php`:

```php
<?php

namespace App\Models;

use Filament\Models\Contracts\FilamentUser;
use Filament\Panel;
use Illuminate\Foundation\Auth\User as Authenticatable;

class User extends Authenticatable implements FilamentUser
{
    protected $fillable = ['name', 'email', 'password', 'role'];

    protected $hidden = ['password', 'remember_token'];

    public function canAccessPanel(Panel $panel): bool
    {
        return in_array($this->role, ['admin', 'staff']);
    }

    public function isAdmin(): bool
    {
        return $this->role === 'admin';
    }

    public function isStaff(): bool
    {
        return $this->role === 'staff';
    }
}
```

## 🛡️ Step 2: Buat Policy untuk Supplier

```bash
php artisan make:policy SupplierPolicy --model=Supplier
```

Edit `app/Policies/SupplierPolicy.php`:

```php
<?php

namespace App\Policies;

use App\Models\Supplier;
use App\Models\User;

class SupplierPolicy
{
    // Admin bisa view all
    public function viewAny(User $user): bool
    {
        return true; // Semua bisa lihat list
    }

    public function view(User $user, Supplier $supplier): bool
    {
        return true;
    }

    // Hanya admin yang bisa create
    public function create(User $user): bool
    {
        return $user->isAdmin();
    }

    public function update(User $user, Supplier $supplier): bool
    {
        return $user->isAdmin();
    }

    public function delete(User $user, Supplier $supplier): bool
    {
        return $user->isAdmin();
    }
}
```

## 📝 Step 3: Register Policy

Edit `app/Providers/AppServiceProvider.php`:

```php
use App\Models\Supplier;
use App\Policies\SupplierPolicy;
use Illuminate\Support\Facades\Gate;

public function boot(): void
{
    Gate::policy(Supplier::class, SupplierPolicy::class);
}
```

## 🎛️ Step 4: Buat User Seeder

```bash
php artisan make:seeder UserSeeder
```

Edit `database/seeders/UserSeeder.php`:

```php
<?php

namespace Database\Seeders;

use App\Models\User;
use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\Hash;

class UserSeeder extends Seeder
{
    public function run(): void
    {
        User::create([
            'name' => 'Admin',
            'email' => 'admin@admin.com',
            'password' => Hash::make('password'),
            'role' => 'admin',
        ]);

        User::create([
            'name' => 'Staff',
            'email' => 'staff@staff.com',
            'password' => Hash::make('password'),
            'role' => 'staff',
        ]);
    }
}
```

```bash
php artisan db:seed --class=UserSeeder
```

## 🎨 Step 5: Tampilkan Role di Dashboard

Buat widget info user. Edit `AdminPanelProvider.php`:

```php
->userMenuItems([
    'profile' => MenuItem::make()
        ->label(fn () => auth()->user()->name . ' (' . auth()->user()->role . ')'),
])
```

## ✅ Test Multi-Role

1. Login sebagai **admin@admin.com** → Full access
2. Login sebagai **staff@staff.com** → Limited access

## ➡️ Selanjutnya

Lanjut ke: [03-suppliers.md](03-suppliers.md)
