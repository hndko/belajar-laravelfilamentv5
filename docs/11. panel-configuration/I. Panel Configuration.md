# Panel Configuration ⚙️

> **Sumber:** [https://filamentphp.com/docs/5.x/panel-configuration](https://filamentphp.com/docs/5.x/panel-configuration)

---

## 🤔 Apa itu Panel?

**Panel** adalah admin interface terpisah. Bisa punya banyak panel (admin, customer, vendor, dll).

---

## 🚀 Membuat Panel Baru

```bash
php artisan make:filament-panel customer
```

---

## 📍 Changing Path

```php
// app/Providers/Filament/AdminPanelProvider.php

$panel->path('admin')  // URL: /admin

$panel->path('dashboard')  // URL: /dashboard
```

---

## 🌐 Custom Domain

```php
$panel->domain('admin.myapp.com')
```

---

## 📏 Content Width

```php
$panel->maxContentWidth(MaxWidth::Full)
// MaxWidth::ExtraSmall, Small, Medium, Large, ExtraLarge, TwoExtraLarge, ...
```

---

## 🔗 Render Hooks

```php
$panel->renderHook(
    'panels::body.start',
    fn () => view('custom-banner'),
)
```

---

## ⏳ Lifecycle Hooks

```php
$panel->bootUsing(function () {
    // Setiap panel boot
})

$panel->servingUsing(function () {
    // Setiap request
})
```

---

## 🚀 SPA Mode

```php
$panel->spa()  // Enable SPA navigation
```

### Disable untuk URL tertentu

```php
$panel->spa()
    ->unspaUrls([
        '*/logout',
        '/external/*',
    ])
```

---

## ⚠️ Unsaved Changes Alert

```php
$panel->unsavedChangesAlerts()
```

---

## 💾 Database Transactions

```php
$panel->databaseTransactions()
```

---

## 📦 Assets

```php
use Filament\Support\Assets\Css;
use Filament\Support\Assets\Js;

$panel->assets([
    Css::make('custom-styles', resource_path('css/custom.css')),
    Js::make('custom-scripts', resource_path('js/custom.js')),
])
```

---

## 🔒 Middleware

```php
$panel->middleware([
    VerifyCsrfToken::class,
    SubstituteBindings::class,
])

$panel->authMiddleware([
    Authenticate::class,
    CheckSubscription::class,
])
```

---

## 🔒 Strict Authorization

```php
$panel->strictAuthorization()  // Require policy untuk semua action
```

---

## 🎯 Latihan Mandiri

Konfigurasi panel dengan:

- Custom path `/dashboard`
- SPA mode enabled
- Unsaved changes alert
- Custom CSS asset
