# XXI. Row Grouping 📁

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/grouping](https://filamentphp.com/docs/5.x/tables/grouping)

---

## 🤔 Apa itu Row Grouping?

**Row Grouping** mengelompokkan baris berdasarkan nilai tertentu, seperti mengelompokkan order berdasarkan status.

---

## 🚀 Grouping Dasar

```php
use Filament\Tables\Grouping\Group;

$table->groups([
    Group::make('status'),
    Group::make('category.name'),
])
```

---

## 📌 Default Grouping

```php
$table->defaultGroup('status')
```

---

## 🔗 Relationship Grouping

```php
Group::make('category.name')
    ->label('Kategori')
```

---

## 🏷️ Custom Label

```php
Group::make('status')
    ->label('Status Pesanan')
```

---

## 📝 Custom Title

```php
Group::make('status')
    ->getTitleFromRecordUsing(fn ($record) =>
        ucfirst($record->status) . ' Orders'
    )
```

---

## 📅 Date Grouping

```php
Group::make('created_at')
    ->date()  // Group by date

Group::make('created_at')
    ->dateTime()  // Include time
```

---

## 📂 Collapsible Groups

```php
$table->groupsCollapsible()
```

### Default Collapsed

```php
$table->groupsCollapsible(collapsed: true)
```

---

## 📊 Group Summaries

```php
TextColumn::make('amount')
    ->summarize(Sum::make())

// Summary akan muncul per group
```

---

## 👁️ Hide Group Rows

Tampilkan summary saja:

```php
$table->groupRecordsTriggerAction(
    fn (Action $action) => $action->hidden()
)
```

---

## 🎯 Latihan Mandiri

Buat grouping untuk tabel Order berdasarkan:

- Status (dengan collapsible)
- Tanggal order (date grouping)
