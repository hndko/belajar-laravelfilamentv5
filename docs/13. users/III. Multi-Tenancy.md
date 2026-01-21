# III. Multi-Tenancy 🏢

> **Sumber:** [https://filamentphp.com/docs/5.x/users/tenancy](https://filamentphp.com/docs/5.x/users/tenancy)

---

## 🤔 Apa itu Multi-Tenancy?

**Multi-Tenancy** memungkinkan satu aplikasi digunakan oleh banyak organisasi/tenant dengan data terpisah.

---

## 🚀 Setup Tenancy

```php
// Di PanelProvider
$panel->tenant(Team::class)
```

---

## 🔗 User ke Tenant

```php
// User model
public function teams(): BelongsToMany
{
    return $this->belongsToMany(Team::class);
}

// Team model
public function members(): BelongsToMany
{
    return $this->belongsToMany(User::class);
}
```

---

## 📋 Tenant Registration

```php
$panel->tenant(Team::class)
    ->tenantRegistration(RegisterTeam::class)
```

---

## 📋 Tenant Profile

```php
$panel->tenant(Team::class)
    ->tenantProfile(EditTeamProfile::class)
```

---

## 📦 Access Current Tenant

```php
use Filament\Facades\Filament;

$tenant = Filament::getTenant();
```

---

## 💳 Billing

```php
use Laravel\Spark\Spark;

$panel->tenant(Team::class)
    ->tenantBillingProvider(new SparkBillingProvider())
    ->requiresTenantSubscription()
```

---

## 🎨 Tenant Menu

```php
$panel->tenant(Team::class)
    ->tenantMenuItems([
        'profile' => MenuItem::make()
            ->label('Team Settings'),
        'billing' => MenuItem::make()
            ->label('Billing'),
    ])
```

---

## 👤 Tenant Avatar

```php
// Team model
use Filament\Models\Contracts\HasAvatar;

class Team implements HasAvatar
{
    public function getFilamentAvatarUrl(): ?string
    {
        return $this->logo_url;
    }
}
```

---

## 🔗 Resource Scoping

Otomatis! Resources hanya menampilkan data tenant yang sedang aktif.

### Disable untuk Resource

```php
protected static bool $isScopedToTenant = false;
```

---

## 🔒 Security

```php
// Pastikan query selalu di-scope ke tenant
public function scopeTenant(Builder $query): Builder
{
    return $query->where('team_id', Filament::getTenant()->id);
}
```

---

## 🎯 Latihan Mandiri

Setup multi-tenancy dengan:

- Team sebagai tenant
- Registration dan profile pages
- Resource scoping otomatis
