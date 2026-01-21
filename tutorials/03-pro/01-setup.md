# 01. Project Setup

## 🚀 Create Project

```bash
composer create-project laravel/laravel booking-saas
cd booking-saas
composer require filament/filament:"^3.2"
```

## 🗄️ Database Migrations

### Teams Table

```bash
php artisan make:model Team -m
```

```php
Schema::create('teams', function (Blueprint $table) {
    $table->id();
    $table->string('name');
    $table->string('slug')->unique();
    $table->text('description')->nullable();
    $table->string('logo')->nullable();
    $table->foreignId('owner_id')->constrained('users')->cascadeOnDelete();
    $table->boolean('is_active')->default(true);
    $table->timestamps();
});
```

### Modify Users Table

```bash
php artisan make:migration add_role_and_team_to_users_table
```

```php
Schema::table('users', function (Blueprint $table) {
    $table->enum('role', ['superadmin', 'admin', 'vendor', 'customer'])->default('customer');
    $table->foreignId('current_team_id')->nullable()->constrained('teams')->nullOnDelete();
});
```

### Team User Pivot

```bash
php artisan make:migration create_team_user_table
```

```php
Schema::create('team_user', function (Blueprint $table) {
    $table->id();
    $table->foreignId('team_id')->constrained()->cascadeOnDelete();
    $table->foreignId('user_id')->constrained()->cascadeOnDelete();
    $table->string('role')->default('member');
    $table->timestamps();

    $table->unique(['team_id', 'user_id']);
});
```

### Services Table

```bash
php artisan make:model Service -m
```

```php
Schema::create('services', function (Blueprint $table) {
    $table->id();
    $table->foreignId('team_id')->constrained()->cascadeOnDelete();
    $table->string('name');
    $table->text('description')->nullable();
    $table->integer('duration_minutes');
    $table->decimal('price', 12, 2);
    $table->boolean('is_active')->default(true);
    $table->timestamps();
});
```

### Bookings Table

```bash
php artisan make:model Booking -m
```

```php
Schema::create('bookings', function (Blueprint $table) {
    $table->id();
    $table->foreignId('team_id')->constrained()->cascadeOnDelete();
    $table->foreignId('service_id')->constrained()->cascadeOnDelete();
    $table->foreignId('customer_id')->constrained('users')->cascadeOnDelete();
    $table->date('date');
    $table->time('start_time');
    $table->time('end_time');
    $table->enum('status', ['pending', 'confirmed', 'completed', 'cancelled'])->default('pending');
    $table->decimal('total_price', 12, 2);
    $table->text('notes')->nullable();
    $table->timestamps();
});
```

## 📦 Models with Relations

### Team.php

```php
class Team extends Model
{
    protected $fillable = ['name', 'slug', 'description', 'logo', 'owner_id', 'is_active'];

    public function owner(): BelongsTo
    {
        return $this->belongsTo(User::class, 'owner_id');
    }

    public function members(): BelongsToMany
    {
        return $this->belongsToMany(User::class)->withPivot('role')->withTimestamps();
    }

    public function services(): HasMany
    {
        return $this->hasMany(Service::class);
    }

    public function bookings(): HasMany
    {
        return $this->hasMany(Booking::class);
    }
}
```

### User.php

```php
class User extends Authenticatable implements FilamentUser
{
    use Notifiable;

    protected $fillable = ['name', 'email', 'password', 'role', 'current_team_id'];

    public function teams(): BelongsToMany
    {
        return $this->belongsToMany(Team::class)->withPivot('role');
    }

    public function currentTeam(): BelongsTo
    {
        return $this->belongsTo(Team::class, 'current_team_id');
    }

    public function ownedTeams(): HasMany
    {
        return $this->hasMany(Team::class, 'owner_id');
    }

    public function isSuperAdmin(): bool
    {
        return $this->role === 'superadmin';
    }

    public function isVendor(): bool
    {
        return $this->role === 'vendor';
    }

    public function canAccessPanel(Panel $panel): bool
    {
        return match ($panel->getId()) {
            'admin' => in_array($this->role, ['superadmin', 'admin']),
            'vendor' => $this->role === 'vendor',
            'app' => $this->role === 'customer',
            default => false,
        };
    }
}
```

```bash
php artisan migrate
```

## ➡️ Selanjutnya

Lanjut ke: [02-multi-panel.md](02-multi-panel.md)
