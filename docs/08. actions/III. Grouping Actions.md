# III. Grouping Actions 📂

> **Sumber:** [https://filamentphp.com/docs/5.x/actions/grouping-actions](https://filamentphp.com/docs/5.x/actions/grouping-actions)

---

## 🤔 Apa itu Action Group?

**Action Group** mengelompokkan beberapa actions ke dalam dropdown menu.

```php
use Filament\Actions\ActionGroup;

ActionGroup::make([
    Action::make('view'),
    Action::make('edit'),
    Action::make('delete'),
])
```

---

## 🎨 Trigger Style

```php
ActionGroup::make([...])
    ->button()  // atau ->link(), ->iconButton()
    ->label('Opsi')
    ->icon('heroicon-o-ellipsis-vertical')
```

### Grouped Button

```php
ActionGroup::make([...])
    ->grouped()
```

---

## 📍 Dropdown Placement

```php
ActionGroup::make([...])
    ->dropdownPlacement('bottom-end')
    // top, top-start, top-end
    // bottom, bottom-start, bottom-end
```

---

## ➖ Dividers

```php
ActionGroup::make([
    Action::make('view'),
    Action::make('edit'),
    Action::make('divider')->divider(),
    Action::make('delete')->color('danger'),
])
```

---

## 📏 Dropdown Width

```php
ActionGroup::make([...])
    ->dropdownWidth('sm')  // xs, sm, md, lg, xl
```

---

## 📏 Max Height

```php
ActionGroup::make([...])
    ->maxHeight('300px')
```

---

## 💡 Contoh Penggunaan

```php
// Di Table
protected function getTableActions(): array
{
    return [
        ActionGroup::make([
            ViewAction::make(),
            EditAction::make(),
            Action::make('duplicate')
                ->icon('heroicon-o-document-duplicate'),
            DeleteAction::make(),
        ])
            ->icon('heroicon-o-ellipsis-horizontal')
            ->size('sm'),
    ];
}
```

---

## 🎯 Latihan Mandiri

Buat ActionGroup dengan:

- View, Edit dengan divider, lalu Delete
- Dropdown placement bottom-end
- Icon ellipsis
