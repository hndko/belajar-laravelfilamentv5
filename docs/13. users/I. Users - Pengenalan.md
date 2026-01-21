# I. Users - Pengenalan 👥

> **Sumber:** [https://filamentphp.com/docs/5.x/users/overview](https://filamentphp.com/docs/5.x/users/overview)

---

## 🤔 Tentang Users

Section ini membahas autentikasi, otorisasi, dan fitur user di panel Filament.

---

## 🔒 Authorize Panel Access

```php
// Di User model
use Filament\Panel;

public function canAccessPanel(Panel $panel): bool
{
    if ($panel->getId() === 'admin') {
        return $this->is_admin;
    }

    return true;
}
```

---

## 🔒 Authorize Resources

```php
// Gunakan Laravel Policy
// app/Policies/PostPolicy.php

class PostPolicy
{
    public function viewAny(User $user): bool
    {
        return $user->can('view_posts');
    }

    public function create(User $user): bool
    {
        return $user->can('create_posts');
    }

    public function update(User $user, Post $post): bool
    {
        return $user->can('edit_posts');
    }

    public function delete(User $user, Post $post): bool
    {
        return $user->can('delete_posts');
    }
}
```

---

## 👤 Avatar

```php
// Di User model
use Filament\Models\Contracts\HasAvatar;

class User implements HasAvatar
{
    public function getFilamentAvatarUrl(): ?string
    {
        return $this->avatar_url;
    }
}
```

### Default Avatar Provider

```php
// Di PanelProvider
use Filament\Support\Facades\FilamentColor;

$panel->defaultAvatarProvider(BoringAvatarsProvider::class)
```

---

## 🏷️ Name Attribute

```php
// Di User model
use Filament\Models\Contracts\HasName;

class User implements HasName
{
    public function getFilamentName(): string
    {
        return $this->full_name;
    }
}
```

---

## 🔐 Authentication Features

### Login

```php
$panel->login()  // Default enabled
```

### Registration

```php
$panel->registration()
```

### Password Reset

```php
$panel->passwordReset()
```

### Email Verification

```php
$panel->emailVerification()
```

### Profile

```php
$panel->profile()
```

---

## 🔒 Auth Guard

```php
$panel->authGuard('admin')
```

---

## 🎯 Latihan Mandiri

Setup authentication dengan:

- Custom canAccessPanel
- Avatar dari database
- Enable registration dan password reset
