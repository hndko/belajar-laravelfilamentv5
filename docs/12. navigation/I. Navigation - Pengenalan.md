# I. Navigation - Pengenalan 🧭

> **Sumber:** [https://filamentphp.com/docs/5.x/navigation/overview](https://filamentphp.com/docs/5.x/navigation/overview)

---

## 🤔 Apa itu Navigation?

**Navigation** adalah menu sidebar untuk berpindah antar halaman di panel.

---

## 🏷️ Label

```php
// Di Resource
protected static ?string $navigationLabel = 'Produk';
```

---

## 🎯 Icon

```php
protected static ?string $navigationIcon = 'heroicon-o-shopping-bag';
```

### Active Icon

```php
protected static ?string $activeNavigationIcon = 'heroicon-s-shopping-bag';
```

---

## 🔢 Sorting

```php
protected static ?int $navigationSort = 1;  // Urutan menu
```

---

## 🔢 Badge

```php
public static function getNavigationBadge(): ?string
{
    return static::getModel()::count();
}

public static function getNavigationBadgeColor(): ?string
{
    return static::getModel()::count() > 10 ? 'warning' : 'primary';
}
```

---

## 📂 Grouping

```php
protected static ?string $navigationGroup = 'Master Data';
```

### Nested Groups

```php
protected static ?string $navigationParentItem = 'Settings';
```

---

## 📂 Collapsible Sidebar

```php
// Di PanelProvider
$panel->collapsibleNavigationGroups()

$panel->sidebarCollapsedOnDesktop()
```

---

## 🔗 Custom Navigation Item

```php
// Di PanelProvider
$panel->navigation(function (NavigationBuilder $builder) {
    return $builder
        ->items([
            NavigationItem::make('Dashboard')
                ->icon('heroicon-o-home')
                ->url('/admin'),
            NavigationItem::make('Analytics')
                ->icon('heroicon-o-chart-bar')
                ->url('https://analytics.google.com')
                ->openUrlInNewTab(),
        ]);
})
```

---

## 👁️ Hide Navigation Item

```php
public static function shouldRegisterNavigation(): bool
{
    return auth()->user()->can('view-users');
}
```

---

## 📍 Top Navigation

```php
$panel->topNavigation()
```

---

## 📏 Sidebar Width

```php
$panel->sidebarWidth('20rem')
```

---

## 🍞 Disable Breadcrumbs

```php
$panel->breadcrumbs(false)
```

---

## 🎯 Latihan Mandiri

Konfigurasi navigation:

- Group Products dan Orders ke "Shop"
- Badge untuk pending orders
- Hide menu berdasarkan permission
