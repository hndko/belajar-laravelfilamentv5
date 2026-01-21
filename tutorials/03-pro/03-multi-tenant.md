# 03. Multi-Tenant Implementation

## 🏢 Tenant Model Setup

Edit `app/Models/Team.php`:

```php
<?php

namespace App\Models;

use Filament\Models\Contracts\HasAvatar;
use Filament\Models\Contracts\HasCurrentTenantLabel;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\BelongsTo;
use Illuminate\Database\Eloquent\Relations\BelongsToMany;
use Illuminate\Database\Eloquent\Relations\HasMany;

class Team extends Model implements HasCurrentTenantLabel, HasAvatar
{
    protected $fillable = ['name', 'slug', 'description', 'logo', 'owner_id', 'is_active'];

    public function getFilamentAvatarUrl(): ?string
    {
        return $this->logo ? Storage::url($this->logo) : null;
    }

    public function getCurrentTenantLabel(): string
    {
        return 'Current Team';
    }

    // Relations...
}
```

## 👤 User Tenant Relationship

Edit `app/Models/User.php`:

```php
use Filament\Models\Contracts\HasTenants;
use Illuminate\Support\Collection;

class User extends Authenticatable implements FilamentUser, HasTenants
{
    // Implement HasTenants
    public function getTenants(Panel $panel): Collection
    {
        return $this->teams;
    }

    public function canAccessTenant(Model $tenant): bool
    {
        return $this->teams()->whereKey($tenant)->exists();
    }
}
```

## 🔒 Tenant Scope untuk Resources

Buat Trait `app/Traits/HasTeamScope.php`:

```php
<?php

namespace App\Traits;

use Illuminate\Database\Eloquent\Builder;
use Filament\Facades\Filament;

trait HasTeamScope
{
    protected static function bootHasTeamScope(): void
    {
        static::creating(function ($model) {
            if (Filament::getTenant()) {
                $model->team_id = Filament::getTenant()->id;
            }
        });

        static::addGlobalScope('team', function (Builder $query) {
            if (Filament::getTenant()) {
                $query->where('team_id', Filament::getTenant()->id);
            }
        });
    }
}
```

Gunakan di models:

```php
class Service extends Model
{
    use HasTeamScope;
    // ...
}

class Booking extends Model
{
    use HasTeamScope;
    // ...
}
```

## 📝 Team Registration Page

Buat `app/Filament/Vendor/Pages/RegisterTeam.php`:

```php
<?php

namespace App\Filament\Vendor\Pages;

use App\Models\Team;
use Filament\Forms\Components\TextInput;
use Filament\Forms\Components\Textarea;
use Filament\Forms\Components\FileUpload;
use Filament\Forms\Form;
use Filament\Pages\Tenancy\RegisterTenant;
use Illuminate\Support\Str;

class RegisterTeam extends RegisterTenant
{
    public static function getLabel(): string
    {
        return 'Register Business';
    }

    public function form(Form $form): Form
    {
        return $form
            ->schema([
                TextInput::make('name')
                    ->label('Nama Bisnis')
                    ->required()
                    ->live(onBlur: true)
                    ->afterStateUpdated(fn ($state, $set) =>
                        $set('slug', Str::slug($state))
                    ),

                TextInput::make('slug')
                    ->required()
                    ->unique(Team::class),

                Textarea::make('description')
                    ->label('Deskripsi')
                    ->rows(3),

                FileUpload::make('logo')
                    ->image()
                    ->directory('team-logos'),
            ]);
    }

    protected function handleRegistration(array $data): Team
    {
        $team = Team::create([
            ...$data,
            'owner_id' => auth()->id(),
        ]);

        $team->members()->attach(auth()->user(), ['role' => 'owner']);

        auth()->user()->update(['current_team_id' => $team->id]);

        return $team;
    }
}
```

## ⚙️ Team Profile Edit

Buat `app/Filament/Vendor/Pages/EditTeamProfile.php`:

```php
<?php

namespace App\Filament\Vendor\Pages;

use Filament\Forms\Components\TextInput;
use Filament\Forms\Components\Textarea;
use Filament\Forms\Components\FileUpload;
use Filament\Forms\Form;
use Filament\Pages\Tenancy\EditTenantProfile;

class EditTeamProfile extends EditTenantProfile
{
    public static function getLabel(): string
    {
        return 'Business Profile';
    }

    public function form(Form $form): Form
    {
        return $form
            ->schema([
                TextInput::make('name')
                    ->required(),

                Textarea::make('description')
                    ->rows(3),

                FileUpload::make('logo')
                    ->image()
                    ->directory('team-logos'),
            ]);
    }
}
```

## ✅ Test Multi-Tenant

1. Login sebagai vendor
2. Register team baru
3. Data akan terisolasi per team
4. Switch antar team (jika punya lebih dari 1)

## ➡️ Selanjutnya

Lanjut ke: [04-services.md](04-services.md)
