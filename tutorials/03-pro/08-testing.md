# 08. Automated Testing

## 🧪 Setup Testing

```bash
# Install Pest (optional, tapi recommended)
composer require pestphp/pest --dev
composer require pestphp/pest-plugin-laravel --dev
php artisan pest:install
```

## 📝 Feature Tests

### Test Service Resource

Buat `tests/Feature/ServiceResourceTest.php`:

```php
<?php

use App\Models\Service;
use App\Models\Team;
use App\Models\User;
use function Pest\Livewire\livewire;

beforeEach(function () {
    $this->vendor = User::factory()->create(['role' => 'vendor']);
    $this->team = Team::factory()->create(['owner_id' => $this->vendor->id]);
    $this->vendor->update(['current_team_id' => $this->team->id]);
    $this->team->members()->attach($this->vendor);
});

it('can render service list page', function () {
    $this->actingAs($this->vendor);

    livewire(\App\Filament\Vendor\Resources\ServiceResource\Pages\ListServices::class)
        ->assertSuccessful();
});

it('can create service', function () {
    $this->actingAs($this->vendor);

    livewire(\App\Filament\Vendor\Resources\ServiceResource\Pages\CreateService::class)
        ->fillForm([
            'name' => 'Haircut',
            'duration_minutes' => 30,
            'price' => 50000,
        ])
        ->call('create')
        ->assertHasNoFormErrors();

    $this->assertDatabaseHas('services', [
        'name' => 'Haircut',
        'team_id' => $this->team->id,
    ]);
});

it('can edit service', function () {
    $service = Service::factory()->create(['team_id' => $this->team->id]);

    $this->actingAs($this->vendor);

    livewire(\App\Filament\Vendor\Resources\ServiceResource\Pages\EditService::class, [
        'record' => $service->getRouteKey(),
    ])
        ->fillForm(['name' => 'Updated Service'])
        ->call('save')
        ->assertHasNoFormErrors();

    expect($service->fresh()->name)->toBe('Updated Service');
});

it('cannot access other team services', function () {
    $otherTeam = Team::factory()->create();
    $otherService = Service::factory()->create(['team_id' => $otherTeam->id]);

    $this->actingAs($this->vendor);

    livewire(\App\Filament\Vendor\Resources\ServiceResource\Pages\ListServices::class)
        ->assertCanNotSeeTableRecords([$otherService]);
});
```

### Test Booking Flow

```php
<?php

use App\Models\Booking;
use App\Models\Service;
use App\Models\Team;
use App\Models\User;

it('customer can create booking', function () {
    $customer = User::factory()->create(['role' => 'customer']);
    $team = Team::factory()->create();
    $service = Service::factory()->create(['team_id' => $team->id]);

    $this->actingAs($customer);

    $response = $this->post('/api/bookings', [
        'team_id' => $team->id,
        'service_id' => $service->id,
        'date' => now()->addDay()->format('Y-m-d'),
        'start_time' => '10:00',
    ]);

    $this->assertDatabaseHas('bookings', [
        'customer_id' => $customer->id,
        'service_id' => $service->id,
    ]);
});

it('vendor can confirm booking', function () {
    $vendor = User::factory()->create(['role' => 'vendor']);
    $team = Team::factory()->create(['owner_id' => $vendor->id]);
    $booking = Booking::factory()->create([
        'team_id' => $team->id,
        'status' => 'pending',
    ]);

    $this->actingAs($vendor);

    $booking->update(['status' => 'confirmed']);

    expect($booking->fresh()->status)->toBe('confirmed');
});
```

## 🔄 Policy Tests

```php
<?php

use App\Models\Booking;
use App\Models\Team;
use App\Models\User;

it('vendor can only view own team bookings', function () {
    $vendor = User::factory()->create(['role' => 'vendor']);
    $team = Team::factory()->create(['owner_id' => $vendor->id]);
    $ownBooking = Booking::factory()->create(['team_id' => $team->id]);
    $otherBooking = Booking::factory()->create();

    expect($vendor->can('view', $ownBooking))->toBeTrue();
    expect($vendor->can('view', $otherBooking))->toBeFalse();
});

it('customer can only view own bookings', function () {
    $customer = User::factory()->create(['role' => 'customer']);
    $ownBooking = Booking::factory()->create(['customer_id' => $customer->id]);
    $otherBooking = Booking::factory()->create();

    expect($customer->can('view', $ownBooking))->toBeTrue();
    expect($customer->can('view', $otherBooking))->toBeFalse();
});
```

## ▶️ Run Tests

```bash
# Run all tests
php artisan test

# Run dengan coverage
php artisan test --coverage

# Run specific file
php artisan test tests/Feature/ServiceResourceTest.php
```

## ➡️ Selanjutnya

Lanjut ke: [09-production.md](09-production.md)
