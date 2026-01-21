# III. Broadcast Notifications 📡

> **Sumber:** [https://filamentphp.com/docs/5.x/notifications/broadcast-notifications](https://filamentphp.com/docs/5.x/notifications/broadcast-notifications)

---

## 🤔 Apa itu Broadcast Notifications?

**Broadcast Notifications** mengirim notifikasi realtime via WebSockets (Pusher, Ably, Soketi, dll).

---

## 📤 Sending

```php
use Filament\Notifications\Notification;

Notification::make()
    ->title('Order baru!')
    ->body('Ada order masuk dari John Doe')
    ->broadcast($recipient);
```

### Send Database + Broadcast

```php
Notification::make()
    ->title('Order baru')
    ->sendToDatabase($recipient)
    ->broadcast($recipient);
```

---

## 🚀 Setup WebSockets di Panel

```php
// app/Providers/Filament/AdminPanelProvider.php

use Filament\Support\Facades\FilamentAsset;
use Illuminate\Support\Facades\Vite;

public function panel(Panel $panel): Panel
{
    return $panel
        ->databaseNotifications()
        ->broadcastChannel(fn ($user) => "users.{$user->id}");
}
```

---

## ⚙️ Laravel Echo Setup

1. Install Laravel Echo:

```bash
npm install laravel-echo pusher-js
```

2. Configure di `resources/js/echo.js`:

```js
import Echo from "laravel-echo";
import Pusher from "pusher-js";

window.Pusher = Pusher;

window.Echo = new Echo({
  broadcaster: "pusher",
  key: import.meta.env.VITE_PUSHER_APP_KEY,
  cluster: import.meta.env.VITE_PUSHER_APP_CLUSTER,
});
```

---

## 🎯 Latihan Mandiri

Setup broadcast notifications dengan:

- Pusher atau Soketi
- Kirim notifikasi realtime saat order baru
- Kombinasi database + broadcast
