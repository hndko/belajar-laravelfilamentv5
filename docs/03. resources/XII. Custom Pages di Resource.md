# XII. Custom Pages di Resource 📄

> **Sumber:** [https://filamentphp.com/docs/5.x/resources/custom-pages](https://filamentphp.com/docs/5.x/resources/custom-pages)

---

## 🤔 Apa itu Custom Page?

**Custom Page** adalah halaman bebas yang bisa kamu tambahkan ke resource. Berbeda dengan List/Create/Edit/View yang sudah ada fungsi bawaan.

### Contoh Penggunaan:

- Halaman statistik khusus
- Halaman import data
- Halaman bulk update
- Halaman sorting manual

---

## 🚀 Membuat Custom Page

```bash
php artisan make:filament-page SortUsers --resource=UserResource --type=custom
```

### Hasilnya:

```
app/Filament/Resources/Users/Pages/SortUsers.php
resources/views/filament/resources/users/pages/sort-users.blade.php
```

---

## 📝 Daftarkan Page di Resource

```php
// UserResource.php

public static function getPages(): array
{
    return [
        'index' => Pages\ListUsers::route('/'),
        'create' => Pages\CreateUsers::route('/create'),
        'edit' => Pages\EditUser::route('/{record}/edit'),
        'sort' => Pages\SortUsers::route('/sort'), // Custom page
    ];
}
```

---

## 🔗 Akses Record di Custom Page

Jika custom page perlu menampilkan/mengelola satu record:

```php
use Filament\Resources\Pages\Page;
use Filament\Resources\Pages\Concerns\InteractsWithRecord;

class ManageUserSettings extends Page
{
    use InteractsWithRecord;

    public function mount(int|string $record): void
    {
        $this->record = $this->resolveRecord($record);
    }

    // Akses record dengan $this->getRecord()
}
```

### Daftarkan dengan Parameter:

```php
public static function getPages(): array
{
    return [
        // ...
        'settings' => Pages\ManageUserSettings::route('/{record}/settings'),
    ];
}
```

---

## 📍 Generate URL ke Custom Page

```php
// Tanpa record
UserResource::getUrl('sort'); // /admin/users/sort

// Dengan record
UserResource::getUrl('settings', ['record' => $user]); // /admin/users/5/settings
```

---

## 💡 Ringkasan

| Fitur            | Cara                               |
| ---------------- | ---------------------------------- |
| Buat custom page | `make:filament-page --type=custom` |
| Akses record     | `InteractsWithRecord` trait        |
| Daftarkan page   | `getPages()` di resource           |
| Generate URL     | `Resource::getUrl('page-name')`    |

---

## 🎯 Latihan Mandiri

Buat custom page "Analytics" untuk ProductResource yang menampilkan:

- Produk terlaris
- Produk dengan stok habis

<details>
<summary>Langkah</summary>

```bash
php artisan make:filament-page ProductAnalytics --resource=ProductResource --type=custom
```

```php
// getPages()
'analytics' => Pages\ProductAnalytics::route('/analytics'),
```

</details>
