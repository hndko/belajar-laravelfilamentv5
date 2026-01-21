# II. Multi-Factor Authentication 🔐

> **Sumber:** [https://filamentphp.com/docs/5.x/users/multi-factor-authentication](https://filamentphp.com/docs/5.x/users/multi-factor-authentication)

---

## 🤔 Apa itu MFA?

**Multi-Factor Authentication (MFA)** menambah lapisan keamanan dengan membutuhkan kode verifikasi selain password.

---

## 📱 App Authentication (TOTP)

Menggunakan aplikasi seperti Google Authenticator, Authy, dll.

```php
// Di PanelProvider
$panel->multifactorAuthentication()
    ->appAuthentication()
```

---

## 🔑 Recovery Codes

```php
$panel->multifactorAuthentication()
    ->appAuthentication()
    ->appRecoveryCodesGeneration()
```

---

## ⏱️ Code Expiration

```php
$panel->multifactorAuthentication()
    ->appAuthentication()
    ->appCodeWindow(1)  // 30 detik (default)
```

---

## 🏷️ Brand Name di App

```php
$panel->multifactorAuthentication()
    ->appAuthentication()
    ->appIssuer('My App')
```

---

## 📧 Email Authentication

Kirim kode via email.

```php
$panel->multifactorAuthentication()
    ->emailAuthentication()
```

### Email Code Expiration

```php
$panel->multifactorAuthentication()
    ->emailAuthentication()
    ->emailCodeExpiry(now()->addMinutes(10))
```

---

## ⚡ Requiring MFA

```php
$panel->multifactorAuthentication()
    ->appAuthentication()
    ->required()  // Wajib setup MFA
```

### Required untuk User Tertentu

```php
$panel->multifactorAuthentication()
    ->appAuthentication()
    ->required(fn (User $user) => $user->isAdmin())
```

---

## ⚠️ Security Notes

- Simpan recovery codes dengan aman
- Gunakan HTTPS
- Set session timeout yang reasonable

---

## 🎯 Latihan Mandiri

Setup MFA dengan:

- App authentication (TOTP)
- Recovery codes enabled
- Required untuk admin users
