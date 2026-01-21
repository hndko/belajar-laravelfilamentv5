# IV. Tabs 📑

> **Sumber:** [https://filamentphp.com/docs/5.x/schemas/tabs](https://filamentphp.com/docs/5.x/schemas/tabs)

---

## 🤔 Apa itu Tabs?

**Tabs** memungkinkan Anda membagi form/infolist menjadi beberapa tab untuk organisasi yang lebih baik.

```php
use Filament\Schemas\Components\Tabs;

Tabs::make('Tabs')
    ->tabs([
        Tabs\Tab::make('Info Dasar')
            ->schema([
                TextInput::make('name'),
                TextInput::make('email'),
            ]),
        Tabs\Tab::make('Alamat')
            ->schema([
                TextInput::make('city'),
                TextInput::make('country'),
            ]),
    ])
```

---

## 📌 Default Active Tab

```php
Tabs::make('Tabs')
    ->tabs([
        Tabs\Tab::make('Tab 1'),
        Tabs\Tab::make('Tab 2'),
    ])
    ->activeTab(2)  // Tab kedua aktif
```

---

## 🎯 Tab Icon

```php
Tabs\Tab::make('Profile')
    ->icon('heroicon-o-user')
    ->schema([...])
```

### Icon Position

```php
Tabs\Tab::make('Settings')
    ->icon('heroicon-o-cog')
    ->iconPosition(IconPosition::After)
```

---

## 🏷️ Tab Badge

```php
Tabs\Tab::make('Orders')
    ->badge(fn () => Order::count())
    ->schema([...])
```

### Badge Color

```php
Tabs\Tab::make('Pending')
    ->badge(5)
    ->badgeColor('warning')
```

---

## 📊 Grid dalam Tab

```php
Tabs\Tab::make('Details')
    ->columns(2)
    ->schema([
        TextInput::make('first_name'),
        TextInput::make('last_name'),
    ])
```

---

## ↕️ Vertical Tabs

```php
Tabs::make('Tabs')
    ->tabs([...])
    ->vertical()
```

---

## 🎨 Remove Container

```php
Tabs::make('Tabs')
    ->tabs([...])
    ->contained(false)
```

---

## 💾 Persist Tab

### Di Session

```php
Tabs::make('Settings')
    ->tabs([...])
    ->persistTabInQueryString()
```

### Di URL Query String

```php
Tabs::make('Tabs')
    ->tabs([...])
    ->persistTabInQueryString('active-tab')
```

---

## 🎯 Latihan Mandiri

Buat form dengan 3 tabs:

- "Data Diri" dengan icon user
- "Alamat" dengan icon map
- "Dokumen" dengan badge jumlah file
