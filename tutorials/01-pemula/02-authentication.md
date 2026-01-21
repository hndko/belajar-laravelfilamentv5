# 02. Authentication

## 🔐 Fitur Auth Bawaan Filament

Filament sudah menyediakan:

- ✅ Login page
- ✅ Logout
- ✅ Session management

## 🛡️ Membatasi Akses Panel

Edit `app/Models/User.php`:

```php
<?php

namespace App\Models;

use Filament\Models\Contracts\FilamentUser;
use Filament\Panel;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;

class User extends Authenticatable implements FilamentUser
{
    use Notifiable;

    protected $fillable = [
        'name',
        'email',
        'password',
    ];

    protected $hidden = [
        'password',
        'remember_token',
    ];

    protected function casts(): array
    {
        return [
            'email_verified_at' => 'datetime',
            'password' => 'hashed',
        ];
    }

    // Method untuk mengontrol akses panel
    public function canAccessPanel(Panel $panel): bool
    {
        // Semua user yang login bisa akses
        return true;

        // Atau batasi dengan kondisi:
        // return $this->email === 'admin@admin.com';
        // return $this->is_admin === true;
    }
}
```

## 🔄 Test Authentication

1. **Logout**
   - Klik avatar di kanan atas
   - Pilih "Sign out"

2. **Login kembali**
   - Masukkan email: `admin@admin.com`
   - Password: `password`

3. **Coba URL langsung**
   - Buka `http://localhost:8000/admin` tanpa login
   - Seharusnya redirect ke halaman login

## ✅ Checklist

- [ ] User model implements FilamentUser
- [ ] canAccessPanel() method ada
- [ ] Login/logout berfungsi

## ➡️ Selanjutnya

Lanjut ke: [03-category-resource.md](03-category-resource.md)
