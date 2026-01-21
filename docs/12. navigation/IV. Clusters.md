# IV. Clusters 📂

> **Sumber:** [https://filamentphp.com/docs/5.x/navigation/clusters](https://filamentphp.com/docs/5.x/navigation/clusters)

---

## 🤔 Apa itu Cluster?

**Cluster** mengelompokkan beberapa resources/pages menjadi satu menu dengan sub-navigation.

---

## 🚀 Membuat Cluster

```bash
php artisan make:filament-cluster Settings
```

### File yang Dibuat:

```
app/Filament/Clusters/Settings.php
```

---

## 📋 Cluster Class

```php
namespace App\Filament\Clusters;

use Filament\Clusters\Cluster;

class Settings extends Cluster
{
    protected static ?string $navigationIcon = 'heroicon-o-cog';
    protected static ?string $navigationLabel = 'Pengaturan';
}
```

---

## 🔗 Add Resources ke Cluster

```php
// Di Resource
protected static ?string $cluster = Settings::class;
```

### Add Pages ke Cluster

```php
// Di Page
protected static ?string $cluster = Settings::class;
```

---

## 📁 File Structure

```
app/Filament/
├── Clusters/
│   └── Settings.php
│   └── Settings/
│       ├── Resources/
│       │   ├── GeneralResource.php
│       │   └── EmailResource.php
│       └── Pages/
│           └── BackupPage.php
```

---

## 📍 Sub-Navigation Position

```php
// Di Cluster
protected static SubNavigationPosition $subNavigationPosition = SubNavigationPosition::Top;

// SubNavigationPosition::Start (sidebar kiri)
// SubNavigationPosition::Top (atas)
// SubNavigationPosition::End (sidebar kanan)
```

---

## 🍞 Custom Breadcrumb

```php
public static function getBreadcrumb(): string
{
    return 'Pengaturan Sistem';
}
```

---

## 🎯 Latihan Mandiri

Buat cluster Settings dengan:

- GeneralResource
- EmailResource
- BackupPage
- Sub-navigation di top
