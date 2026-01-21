# II. Modals 🪟

> **Sumber:** [https://filamentphp.com/docs/5.x/actions/modals](https://filamentphp.com/docs/5.x/actions/modals)

---

## 🤔 Apa itu Modal?

**Modal** adalah dialog popup yang muncul saat action diklik. Bisa berisi form, konfirmasi, atau konten kustom.

---

## ✅ Confirmation Modal

```php
Action::make('delete')
    ->requiresConfirmation()
```

### Custom Confirmation

```php
Action::make('delete')
    ->requiresConfirmation()
    ->modalHeading('Hapus Record')
    ->modalDescription('Apakah Anda yakin ingin menghapus? Tindakan ini tidak bisa dibatalkan.')
    ->modalSubmitActionLabel('Ya, Hapus')
```

---

## 📝 Form Modal

```php
Action::make('updateStatus')
    ->form([
        Select::make('status')
            ->options([
                'pending' => 'Pending',
                'approved' => 'Approved',
                'rejected' => 'Rejected',
            ])
            ->required(),
        Textarea::make('notes'),
    ])
    ->action(function (array $data, Model $record) {
        $record->update($data);
    })
```

---

## 🎯 Modal Icon

```php
Action::make('warning')
    ->modalIcon('heroicon-o-exclamation-triangle')
    ->modalIconColor('warning')
```

---

## 📏 Modal Width

```php
Action::make('settings')
    ->modalWidth('lg')  // xs, sm, md, lg, xl, 2xl, 3xl, 4xl, 5xl, 6xl, 7xl
```

---

## ↔️ Slide Over

```php
Action::make('details')
    ->slideOver()
```

---

## 📌 Sticky Header/Footer

```php
Action::make('longForm')
    ->stickyModalHeader()
    ->stickyModalFooter()
```

---

## 🎨 Custom Content

```php
Action::make('info')
    ->modalContent(view('modals.info'))

Action::make('preview')
    ->modalContentFooter(view('modals.preview-footer'))
```

---

## ⚡ Footer Actions

```php
Action::make('wizard')
    ->modalFooterActions([
        Action::make('previous')
            ->action(fn () => $this->previousStep()),
        Action::make('next')
            ->action(fn () => $this->nextStep()),
    ])
```

---

## ❌ Closing Modal

### Close by Click Away

```php
Action::make('form')
    ->closeModalByClickingAway(false)
```

### Close by Escape

```php
Action::make('critical')
    ->closeModalByEscaping(false)
```

---

## 🎯 Latihan Mandiri

Buat Action dengan modal:

- `updateStatus` dengan form select
- `delete` dengan confirmation
- `preview` dengan slide over
