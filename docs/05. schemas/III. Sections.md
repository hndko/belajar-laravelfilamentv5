# III. Sections 📦

> **Sumber:** [https://filamentphp.com/docs/5.x/schemas/sections](https://filamentphp.com/docs/5.x/schemas/sections)

---

## 🤔 Apa itu Section?

**Section** adalah container dengan heading dan border untuk mengelompokkan komponen terkait.

```php
use Filament\Schemas\Components\Section;

Section::make('Informasi Pengguna')
    ->schema([
        TextInput::make('name'),
        TextInput::make('email'),
    ])
```

---

## 📝 Heading & Description

```php
Section::make('Detail Produk')
    ->description('Masukkan informasi produk Anda')
    ->schema([...])
```

---

## 🎯 Icon

```php
Section::make('Pengaturan')
    ->icon('heroicon-o-cog-6-tooth')
    ->schema([...])
```

---

## ↔️ Aside Layout

Heading di samping kiri:

```php
Section::make('Profil')
    ->aside()
    ->schema([...])
```

---

## 📂 Collapsible

### Bisa Collapse

```php
Section::make('Detail Lanjutan')
    ->collapsible()
    ->schema([...])
```

### Default Collapsed

```php
Section::make('Opsional')
    ->collapsed()
    ->schema([...])
```

### Persist di Session

```php
Section::make('Settings')
    ->collapsible()
    ->persistCollapsed()
    ->id('user-settings')
```

---

## 🎨 Styling

### Compact

```php
Section::make('Info')
    ->compact()
    ->schema([...])
```

### Secondary Style

```php
Section::make('Catatan')
    ->secondary()
    ->schema([...])
```

---

## ⚡ Header & Footer Actions

### Header Actions

```php
Section::make('Data')
    ->headerActions([
        Action::make('refresh')
            ->icon('heroicon-o-arrow-path')
            ->action(fn () => $this->refresh()),
    ])
    ->schema([...])
```

### Footer Actions

```php
Section::make('Formulir')
    ->footerActions([
        Action::make('submit')
            ->label('Simpan')
            ->submit('save'),
    ])
    ->schema([...])
```

---

## 📊 Grid dalam Section

```php
Section::make('Alamat')
    ->columns(2)
    ->schema([
        TextInput::make('city'),
        TextInput::make('state'),
        TextInput::make('country'),
        TextInput::make('postal_code'),
    ])
```

---

## 🎯 Latihan Mandiri

Buat section "Pengaturan Akun" yang:

- Collapsible
- Ada icon
- Ada description
- 2 kolom
