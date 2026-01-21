# II. Database Notifications 💾

> **Sumber:** [https://filamentphp.com/docs/5.x/notifications/database-notifications](https://filamentphp.com/docs/5.x/notifications/database-notifications)

---

## 🤔 Apa itu Database Notifications?

**Database Notifications** menyimpan notifikasi ke database sehingga user bisa melihatnya kapan saja.

---

## 🚀 Setup Database Table

```bash
php artisan make:notifications-table
php artisan migrate
```

---

## ✅ Enable di Panel

```php
// app/Providers/Filament/AdminPanelProvider.php

public function panel(Panel $panel): Panel
{
    return $panel
        ->databaseNotifications();
}
```

### Polling

```php
$panel->databaseNotifications()
    ->databaseNotificationsPolling('30s')  // Cek tiap 30 detik
```

---

## 📤 Sending Notifications

```php
use Filament\Notifications\Notification;

$recipient = auth()->user();

Notification::make()
    ->title('Order baru')
    ->body('Ada order #12345 dari John Doe')
    ->icon('heroicon-o-shopping-bag')
    ->sendToDatabase($recipient);
```

### Send ke Multiple Users

```php
$admins = User::where('role', 'admin')->get();

Notification::make()
    ->title('System alert')
    ->sendToDatabase($admins);
```

---

## 📍 Move ke Sidebar

```php
$panel->databaseNotifications()
    ->databaseNotificationsInSidebar()
```

---

## 📥 Receiving Notifications

User akan melihat bell icon dengan badge jumlah notifikasi belum dibaca.

---

## ✅ Mark as Read

Notifikasi otomatis ditandai dibaca saat diklik.

```php
// Manual mark as read
Notification::make()
    ->title('Info')
    ->actions([
        Action::make('markAsRead')
            ->markAsRead(),
    ])
    ->sendToDatabase($recipient);
```

---

## 🔔 Open Modal Programmatically

```php
$this->dispatch('open-notifications');
```

---

## 🎯 Latihan Mandiri

Setup database notifications dan:

- Kirim notifikasi saat order baru
- Kirim ke semua admin
- Enable polling 15 detik
