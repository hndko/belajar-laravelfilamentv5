# VIII. Replicate Action 📋

> **Sumber:** [https://filamentphp.com/docs/5.x/actions/replicate](https://filamentphp.com/docs/5.x/actions/replicate)

---

## 🤔 Apa itu ReplicateAction?

**ReplicateAction** menduplikasi record yang ada dengan opsi untuk mengubah beberapa field.

```php
use Filament\Actions\ReplicateAction;

ReplicateAction::make()
```

---

## 🚫 Excluding Attributes

```php
ReplicateAction::make()
    ->excludeAttributes(['id', 'created_at', 'updated_at', 'slug'])
```

---

## 🔧 Customize Data Before Fill

```php
ReplicateAction::make()
    ->mutateRecordDataUsing(function (array $data) {
        $data['name'] = $data['name'] . ' (Copy)';
        return $data;
    })
```

---

## 🔀 Redirect After Replicate

```php
ReplicateAction::make()
    ->successRedirectUrl(fn (Model $replica) => route('products.edit', $replica))
```

---

## 🔔 Custom Notification

```php
ReplicateAction::make()
    ->successNotificationTitle('Record berhasil diduplikasi')
```

---

## ⏳ Lifecycle Hooks

```php
ReplicateAction::make()
    ->beforeReplicaSaved(function (Model $replica, Model $original) {
        // Sebelum replica disimpan
        $replica->slug = Str::slug($replica->name);
    })
    ->afterReplicaSaved(function (Model $replica, Model $original) {
        // Setelah replica disimpan
        // Copy relasi
        foreach ($original->images as $image) {
            $replica->images()->create($image->toArray());
        }
    })
```

---

## ⛔ Halt Process

```php
ReplicateAction::make()
    ->before(function (Action $action, Model $record) {
        if (! $record->can_be_duplicated) {
            $action->halt();
        }
    })
```

---

## 💡 Contoh Penggunaan

```php
ReplicateAction::make()
    ->excludeAttributes(['id', 'slug', 'published_at'])
    ->mutateRecordDataUsing(fn (array $data) => [
        ...$data,
        'name' => $data['name'] . ' (Copy)',
        'status' => 'draft',
    ])
    ->afterReplicaSaved(function (Model $replica, Model $original) {
        // Copy tags
        $replica->tags()->sync($original->tags->pluck('id'));
    })
    ->successNotificationTitle('Produk berhasil diduplikasi')
```

---

## 🎯 Latihan Mandiri

Buat ReplicateAction yang:

- Exclude id, slug, created_at
- Tambahkan " (Copy)" ke nama
- Copy relasi tags setelah save
