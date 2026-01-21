# 02. Multi-Panel Setup

## 🎛️ 1. Admin Panel (Default)

```bash
php artisan filament:install --panels
# Name: admin
```

Edit `app/Providers/Filament/AdminPanelProvider.php`:

```php
public function panel(Panel $panel): Panel
{
    return $panel
        ->default()
        ->id('admin')
        ->path('admin')
        ->login()
        ->colors(['primary' => Color::Indigo])
        ->brandName('Booking Admin')
        ->discoverResources(in: app_path('Filament/Admin/Resources'), for: 'App\\Filament\\Admin\\Resources')
        ->discoverPages(in: app_path('Filament/Admin/Pages'), for: 'App\\Filament\\Admin\\Pages')
        ->discoverWidgets(in: app_path('Filament/Admin/Widgets'), for: 'App\\Filament\\Admin\\Widgets')
        ->pages([Pages\Dashboard::class])
        ->middleware([...])
        ->authMiddleware([Authenticate::class]);
}
```

## 🏪 2. Vendor Panel

```bash
php artisan make:filament-panel vendor
```

Edit `app/Providers/Filament/VendorPanelProvider.php`:

```php
use App\Models\Team;

public function panel(Panel $panel): Panel
{
    return $panel
        ->id('vendor')
        ->path('vendor')
        ->login()
        ->registration()  // Allow vendor registration
        ->colors(['primary' => Color::Emerald])
        ->brandName('Vendor Dashboard')
        // Multi-tenant setup
        ->tenant(Team::class, slugAttribute: 'slug')
        ->tenantRegistration(RegisterTeam::class)
        ->tenantProfile(EditTeamProfile::class)
        ->discoverResources(in: app_path('Filament/Vendor/Resources'), for: 'App\\Filament\\Vendor\\Resources')
        ->discoverPages(in: app_path('Filament/Vendor/Pages'), for: 'App\\Filament\\Vendor\\Pages')
        ->discoverWidgets(in: app_path('Filament/Vendor/Widgets'), for: 'App\\Filament\\Vendor\\Widgets')
        ->middleware([...])
        ->authMiddleware([Authenticate::class]);
}
```

## 👤 3. Customer Panel

```bash
php artisan make:filament-panel app
```

Edit `app/Providers/Filament/AppPanelProvider.php`:

```php
public function panel(Panel $panel): Panel
{
    return $panel
        ->id('app')
        ->path('app')
        ->login()
        ->registration()
        ->colors(['primary' => Color::Blue])
        ->brandName('Book Now')
        ->discoverResources(in: app_path('Filament/App/Resources'), for: 'App\\Filament\\App\\Resources')
        ->discoverPages(in: app_path('Filament/App/Pages'), for: 'App\\Filament\\App\\Pages')
        ->discoverWidgets(in: app_path('Filament/App/Widgets'), for: 'App\\Filament\\App\\Widgets')
        ->middleware([...])
        ->authMiddleware([Authenticate::class]);
}
```

## 📁 Folder Structure

```
app/Filament/
├── Admin/
│   ├── Resources/
│   │   ├── TeamResource.php
│   │   └── UserResource.php
│   ├── Pages/
│   └── Widgets/
├── Vendor/
│   ├── Resources/
│   │   ├── ServiceResource.php
│   │   └── BookingResource.php
│   ├── Pages/
│   └── Widgets/
└── App/
    ├── Resources/
    │   └── BookingResource.php
    ├── Pages/
    └── Widgets/
```

## 👤 Create Users for Testing

```bash
php artisan make:seeder RoleSeeder
```

```php
class RoleSeeder extends Seeder
{
    public function run(): void
    {
        // Super Admin
        User::create([
            'name' => 'Super Admin',
            'email' => 'superadmin@app.com',
            'password' => Hash::make('password'),
            'role' => 'superadmin',
        ]);

        // Vendor
        $vendor = User::create([
            'name' => 'Salon Owner',
            'email' => 'vendor@app.com',
            'password' => Hash::make('password'),
            'role' => 'vendor',
        ]);

        $team = Team::create([
            'name' => 'Beauty Salon',
            'slug' => 'beauty-salon',
            'owner_id' => $vendor->id,
        ]);

        $vendor->update(['current_team_id' => $team->id]);
        $team->members()->attach($vendor, ['role' => 'owner']);

        // Customer
        User::create([
            'name' => 'Customer',
            'email' => 'customer@app.com',
            'password' => Hash::make('password'),
            'role' => 'customer',
        ]);
    }
}
```

```bash
php artisan db:seed --class=RoleSeeder
```

## ✅ Test Access

- Admin: `http://localhost:8000/admin` (superadmin@app.com)
- Vendor: `http://localhost:8000/vendor` (vendor@app.com)
- Customer: `http://localhost:8000/app` (customer@app.com)

## ➡️ Selanjutnya

Lanjut ke: [03-multi-tenant.md](03-multi-tenant.md)
