# 08. Notifications System

## 🔔 Database Notifications Setup

### 1. Buat Migration

```bash
php artisan make:notifications-table
php artisan migrate
```

### 2. Update User Model

```php
use Illuminate\Notifications\Notifiable;
use Filament\Models\Contracts\HasAvatar;

class User extends Authenticatable implements FilamentUser, HasAvatar
{
    use Notifiable;

    public function getFilamentAvatarUrl(): ?string
    {
        return null; // Atau URL avatar
    }
}
```

### 3. Enable di Panel

Edit `AdminPanelProvider.php`:

```php
->databaseNotifications()
->databaseNotificationsPolling('30s')
```

## 📤 Kirim Notifikasi Low Stock

Buat Notification class:

```bash
php artisan make:notification LowStockNotification
```

Edit `app/Notifications/LowStockNotification.php`:

```php
<?php

namespace App\Notifications;

use App\Models\Product;
use Illuminate\Notifications\Notification;
use Filament\Notifications\Notification as FilamentNotification;

class LowStockNotification extends Notification
{
    public function __construct(public Product $product)
    {
    }

    public function via($notifiable): array
    {
        return ['database'];
    }

    public function toDatabase($notifiable): array
    {
        return FilamentNotification::make()
            ->warning()
            ->title('Stok Menipis!')
            ->body("Produk {$this->product->name} stok: {$this->product->stock}")
            ->getDatabaseMessage();
    }
}
```

## 🔄 Auto Notify on Low Stock

Tambahkan observer atau event:

```bash
php artisan make:observer ProductObserver --model=Product
```

Edit `app/Observers/ProductObserver.php`:

```php
<?php

namespace App\Observers;

use App\Models\Product;
use App\Models\User;
use App\Notifications\LowStockNotification;

class ProductObserver
{
    public function updated(Product $product): void
    {
        if ($product->isLowStock() && $product->wasChanged('stock')) {
            // Notify all admins
            User::where('role', 'admin')->each(function ($admin) use ($product) {
                $admin->notify(new LowStockNotification($product));
            });
        }
    }
}
```

Register di `AppServiceProvider.php`:

```php
use App\Models\Product;
use App\Observers\ProductObserver;

public function boot(): void
{
    Product::observe(ProductObserver::class);
}
```

## 🔔 Toast Notifications

Sudah kita pakai di actions:

```php
use Filament\Notifications\Notification;

Notification::make()
    ->success()
    ->title('Berhasil!')
    ->body('Data tersimpan.')
    ->send();

Notification::make()
    ->danger()
    ->title('Gagal!')
    ->body('Terjadi kesalahan.')
    ->send();
```

## ➡️ Selanjutnya

Lanjut ke: [09-deploy-vps.md](09-deploy-vps.md)
