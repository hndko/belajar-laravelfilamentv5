# III. User Menu 👤

> **Sumber:** [https://filamentphp.com/docs/5.x/navigation/user-menu](https://filamentphp.com/docs/5.x/navigation/user-menu)

---

## 🤔 Apa itu User Menu?

**User Menu** adalah dropdown menu di kanan atas yang menampilkan profil user dan opsi lainnya.

---

## 📍 Move ke Sidebar

```php
// Di PanelProvider
$panel->userMenuInSidebar()
```

---

## 👤 Profile Link

```php
$panel->profile(EditProfile::class)
```

### isSimple Profile

```php
$panel->profile(EditProfile::class, isSimple: false)
```

---

## 🚪 Logout Link

```php
$panel->logoutUrl('/custom-logout')
```

---

## ➕ Custom Menu Items

```php
use Filament\Navigation\MenuItem;

$panel->userMenuItems([
    MenuItem::make()
        ->label('Pengaturan')
        ->url('/settings')
        ->icon('heroicon-o-cog'),
    MenuItem::make()
        ->label('Bantuan')
        ->url('/help')
        ->icon('heroicon-o-question-mark-circle'),
])
```

---

## 👁️ Conditional Items

```php
MenuItem::make()
    ->label('Admin Panel')
    ->url('/admin')
    ->visible(fn () => auth()->user()->isAdmin())
```

---

## 📤 POST Request

```php
MenuItem::make()
    ->label('Clear Cache')
    ->postAction(fn () => route('cache.clear'))
    ->icon('heroicon-o-trash')
```

---

## 🚫 Disable User Menu

```php
$panel->userMenu(false)
```

---

## 🎯 Latihan Mandiri

Konfigurasi user menu dengan:

- Custom profile page
- Link ke settings
- Admin-only link
