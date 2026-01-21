# VI. View Action 👁️

> **Sumber:** [https://filamentphp.com/docs/5.x/actions/view](https://filamentphp.com/docs/5.x/actions/view)

---

## 🤔 Apa itu ViewAction?

**ViewAction** adalah action bawaan untuk melihat detail record dalam modal read-only.

```php
use Filament\Actions\ViewAction;

ViewAction::make()
```

---

## 🔧 Customize Data Before Fill

```php
ViewAction::make()
    ->mutateRecordDataUsing(function (array $data) {
        // Modify data sebelum ditampilkan
        $data['formatted_price'] = 'Rp ' . number_format($data['price']);
        return $data;
    })
```

---

## 📋 Custom Infolist

```php
ViewAction::make()
    ->infolist([
        TextEntry::make('name'),
        TextEntry::make('email'),
        TextEntry::make('created_at')
            ->dateTime(),
    ])
```

---

## 💡 Contoh Penggunaan

```php
// Di Table
ViewAction::make()
    ->infolist([
        Section::make('Informasi User')
            ->schema([
                TextEntry::make('name')
                    ->label('Nama'),
                TextEntry::make('email')
                    ->label('Email'),
                TextEntry::make('phone')
                    ->label('Telepon'),
            ])
            ->columns(2),
        Section::make('Status')
            ->schema([
                IconEntry::make('is_active')
                    ->boolean(),
                TextEntry::make('created_at')
                    ->dateTime(),
            ]),
    ])
```

---

## 🎯 Latihan Mandiri

Buat ViewAction dengan infolist yang menampilkan:

- Informasi user dalam section
- Status dengan IconEntry boolean
- Tanggal dengan format datetime
