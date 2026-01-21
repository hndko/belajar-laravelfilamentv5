# I. Notifications - Pengenalan 🔔

> **Sumber:** [https://filamentphp.com/docs/5.x/notifications/overview](https://filamentphp.com/docs/5.x/notifications/overview)

---

## 🤔 Apa itu Notifications?

**Notifications** adalah sistem untuk menampilkan pesan toast/alert ke user.

```php
use Filament\Notifications\Notification;

Notification::make()
    ->title('Data berhasil disimpan')
    ->success()
    ->send();
```

---

## 🏷️ Title

```php
Notification::make()
    ->title('Selamat datang!')
    ->send();
```

---

## 🎯 Icon

```php
Notification::make()
    ->title('File diupload')
    ->icon('heroicon-o-document-arrow-up')
    ->send();
```

---

## 🎨 Background Color

```php
Notification::make()
    ->title('Sukses')
    ->success()  // success, warning, danger, info

Notification::make()
    ->title('Peringatan')
    ->warning()

Notification::make()
    ->title('Error')
    ->danger()

Notification::make()
    ->title('Info')
    ->info()
```

---

## ⏱️ Duration

```php
Notification::make()
    ->title('Sebentar')
    ->duration(3000)  // 3 detik
    ->send();

Notification::make()
    ->title('Tetap muncul')
    ->persistent()  // Tidak hilang otomatis
    ->send();
```

---

## 📝 Body Text

```php
Notification::make()
    ->title('Order diterima')
    ->body('Order #12345 berhasil diproses.')
    ->send();
```

---

## ⚡ Actions

```php
Notification::make()
    ->title('Order baru')
    ->body('Ada order baru masuk.')
    ->actions([
        Action::make('view')
            ->label('Lihat')
            ->url('/orders/123'),
        Action::make('dismiss')
            ->label('Tutup')
            ->close(),
    ])
    ->send();
```

### URL Action

```php
Action::make('view')
    ->url('/orders/123')
    ->openUrlInNewTab()
```

### Livewire Event

```php
Action::make('refresh')
    ->dispatch('refreshTable')
```

---

## 📍 Position

```php
Notification::make()
    ->title('Notifikasi')
    ->send();

// Di AppServiceProvider
Notification::position('top-center');
// top-right, top-center, top-left
// bottom-right, bottom-center, bottom-left
```

---

## 🎯 Latihan Mandiri

Buat notification untuk:

- Success saat data tersimpan
- Warning dengan action undo
- Error dengan body detail
