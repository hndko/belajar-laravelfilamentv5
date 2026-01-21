# V. Edit Action ✏️

> **Sumber:** [https://filamentphp.com/docs/5.x/actions/edit](https://filamentphp.com/docs/5.x/actions/edit)

---

## 🤔 Apa itu EditAction?

**EditAction** adalah action bawaan untuk mengedit record yang ada.

```php
use Filament\Actions\EditAction;

EditAction::make()
```

---

## 🔧 Customize Data Before Fill

```php
EditAction::make()
    ->mutateRecordDataUsing(function (array $data) {
        // Modify data sebelum mengisi form
        return $data;
    })
```

---

## 🔧 Customize Data Before Save

```php
EditAction::make()
    ->mutateFormDataUsing(function (array $data) {
        $data['updated_by'] = auth()->id();
        return $data;
    })
```

---

## 🔧 Custom Saving Process

```php
EditAction::make()
    ->using(function (Model $record, array $data) {
        $record->update($data);
        return $record;
    })
```

---

## 🔀 Redirect After Save

```php
EditAction::make()
    ->successRedirectUrl(fn (Model $record) => route('users.show', $record))
```

---

## 🔔 Custom Notification

```php
EditAction::make()
    ->successNotificationTitle('Data berhasil diperbarui')
```

---

## ⏳ Lifecycle Hooks

```php
EditAction::make()
    ->beforeFormFilled(function () {
        // Sebelum form diisi
    })
    ->afterFormFilled(function () {
        // Setelah form diisi
    })
    ->beforeFormValidated(function () {
        // Sebelum validasi
    })
    ->afterFormValidated(function () {
        // Setelah validasi
    })
    ->before(function () {
        // Sebelum save
    })
    ->after(function (Model $record) {
        // Setelah save
    })
```

---

## ⛔ Halt Process

```php
EditAction::make()
    ->before(function (Action $action, Model $record) {
        if ($record->is_locked) {
            $action->halt();

            Notification::make()
                ->warning()
                ->title('Record terkunci')
                ->send();
        }
    })
```

---

## 🎯 Latihan Mandiri

Buat EditAction dengan:

- mutateFormDataUsing untuk set updated_by
- Custom notification
- Halt jika record locked
