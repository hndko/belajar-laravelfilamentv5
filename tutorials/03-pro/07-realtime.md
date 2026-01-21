# 07. Real-time Features

## 📡 Setup Broadcasting

### 1. Install Pusher

```bash
composer require pusher/pusher-php-server
npm install --save laravel-echo pusher-js
```

### 2. Configure .env

```env
BROADCAST_DRIVER=pusher
PUSHER_APP_ID=your_app_id
PUSHER_APP_KEY=your_app_key
PUSHER_APP_SECRET=your_app_secret
PUSHER_APP_CLUSTER=ap1
```

### 3. Uncomment BroadcastServiceProvider

Di `bootstrap/providers.php`:

```php
App\Providers\BroadcastServiceProvider::class,
```

## 🔔 Real-time Booking Notifications

### Create Event

```bash
php artisan make:event NewBookingCreated
```

Edit `app/Events/NewBookingCreated.php`:

```php
<?php

namespace App\Events;

use App\Models\Booking;
use Illuminate\Broadcasting\Channel;
use Illuminate\Broadcasting\InteractsWithSockets;
use Illuminate\Broadcasting\PrivateChannel;
use Illuminate\Contracts\Broadcasting\ShouldBroadcast;
use Illuminate\Queue\SerializesModels;

class NewBookingCreated implements ShouldBroadcast
{
    use InteractsWithSockets, SerializesModels;

    public function __construct(public Booking $booking)
    {
    }

    public function broadcastOn(): Channel
    {
        return new PrivateChannel('team.' . $this->booking->team_id);
    }

    public function broadcastWith(): array
    {
        return [
            'booking_id' => $this->booking->id,
            'customer' => $this->booking->customer->name,
            'service' => $this->booking->service->name,
            'date' => $this->booking->date->format('d M Y'),
        ];
    }
}
```

### Dispatch Event

Di Booking model atau observer:

```php
protected static function booted(): void
{
    static::created(function (Booking $booking) {
        event(new NewBookingCreated($booking));
    });
}
```

## 🔔 Filament Database Notifications

### Enable di Panel

```php
->databaseNotifications()
->databaseNotificationsPolling('30s')
```

### Create Notification

```bash
php artisan make:notification BookingNotification
```

```php
<?php

namespace App\Notifications;

use App\Models\Booking;
use Filament\Notifications\Notification as FilamentNotification;
use Illuminate\Notifications\Notification;

class BookingNotification extends Notification
{
    public function __construct(
        public Booking $booking,
        public string $message
    ) {}

    public function via($notifiable): array
    {
        return ['database'];
    }

    public function toDatabase($notifiable): array
    {
        return FilamentNotification::make()
            ->title('Booking Update')
            ->body($this->message)
            ->icon('heroicon-o-calendar')
            ->getDatabaseMessage();
    }
}
```

### Send Notification

```php
// Notify vendor when new booking
$booking->team->owner->notify(
    new BookingNotification($booking, "New booking from {$booking->customer->name}")
);

// Notify customer when status changes
$booking->customer->notify(
    new BookingNotification($booking, "Your booking status: {$booking->status}")
);
```

## 🔄 Auto-refresh Widgets

```php
class TodayBookingsWidget extends Widget
{
    protected static string $view = 'filament.widgets.today-bookings';

    // Auto polling setiap 30 detik
    protected static ?string $pollingInterval = '30s';
}
```

## ➡️ Selanjutnya

Lanjut ke: [08-testing.md](08-testing.md)
