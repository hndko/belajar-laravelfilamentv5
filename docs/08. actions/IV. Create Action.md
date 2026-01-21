# IV. Create Action ➕

> **Sumber:** [https://filamentphp.com/docs/5.x/actions/create](https://filamentphp.com/docs/5.x/actions/create)

---

## 🤔 Apa itu CreateAction?

**CreateAction** adalah action bawaan untuk membuat record baru dengan modal form.

```php
use Filament\Actions\CreateAction;

CreateAction::make()
    ->model(User::class)
```

---

## 🔧 Customize Data Before Save

```php
CreateAction::make()
    ->mutateFormDataUsing(function (array $data) {
        $data['user_id'] = auth()->id();
        return $data;
    })
```

---

## 🔧 Custom Creation Process

```php
CreateAction::make()
    ->using(function (array $data, string $model) {
        return $model::create($data);
    })
```

---

## 🔀 Redirect After Create

```php
CreateAction::make()
    ->successRedirectUrl(fn (Model $record) => route('users.show', $record))
```

---

## 🔔 Custom Notification

```php
CreateAction::make()
    ->successNotificationTitle('User berhasil dibuat')
```

---

## ⏳ Lifecycle Hooks

```php
CreateAction::make()
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
        // Sebelum create
    })
    ->after(function (Model $record) {
        // Setelah create
    })
```

---

## ⛔ Halt Process

```php
CreateAction::make()
    ->before(function (Action $action) {
        if (! $this->canCreate()) {
            $action->halt();

            Notification::make()
                ->danger()
                ->title('Tidak bisa membuat record')
                ->send();
        }
    })
```

---

## 🧙 Wizard

```php
CreateAction::make()
    ->steps([
        Step::make('Informasi Dasar')
            ->schema([
                TextInput::make('name'),
            ]),
        Step::make('Detail')
            ->schema([
                Textarea::make('description'),
            ]),
    ])
```

---

## 🔁 Create Another

```php
CreateAction::make()
    ->createAnother()
```

---

## 🎯 Latihan Mandiri

Buat CreateAction dengan:

- mutateFormDataUsing untuk set created_by
- Custom notification
- Wizard 2 steps
