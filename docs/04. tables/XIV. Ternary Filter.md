# XIV. Ternary Filter 🔀

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/filters/ternary](https://filamentphp.com/docs/5.x/tables/filters/ternary)

---

## 🤔 Apa itu TernaryFilter?

**TernaryFilter** adalah filter dengan 3 opsi: Yes, No, dan All. Cocok untuk boolean fields.

```php
use Filament\Tables\Filters\TernaryFilter;

TernaryFilter::make('is_active')
```

---

## 📝 Nullable Column

Untuk column yang bisa null:

```php
TernaryFilter::make('verified_at')
    ->nullable()
```

---

## 🔄 Custom Column

```php
TernaryFilter::make('verification')
    ->column('email_verified_at')
    ->nullable()
```

---

## 🏷️ Custom Labels

```php
TernaryFilter::make('is_active')
    ->trueLabel('Aktif')
    ->falseLabel('Tidak Aktif')
    ->placeholder('Semua Status')
```

---

## 🔧 Custom Query

```php
TernaryFilter::make('has_reviews')
    ->queries(
        true: fn ($query) => $query->has('reviews'),
        false: fn ($query) => $query->doesntHave('reviews'),
    )
```

---

## 🗑️ Soft Delete Filter

Filter bawaan untuk soft delete:

```php
use Filament\Tables\Filters\TrashedFilter;

TrashedFilter::make()
```

---

## 🎯 Latihan Mandiri

Buat TernaryFilter untuk `has_avatar` yang cek apakah user punya avatar.
