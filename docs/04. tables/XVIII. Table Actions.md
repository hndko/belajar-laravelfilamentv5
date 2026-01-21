# XVIII. Table Actions ⚡

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/actions](https://filamentphp.com/docs/5.x/tables/actions)

---

## 🤔 Jenis-Jenis Actions

| Jenis              | Lokasi       | Untuk                   |
| ------------------ | ------------ | ----------------------- |
| **Record Actions** | Per baris    | Edit, Delete, View      |
| **Bulk Actions**   | Toolbar      | Delete Selected, Export |
| **Header Actions** | Header tabel | Create, Import          |
| **Column Actions** | Dalam column | Custom per cell         |

---

## 📋 Record Actions

```php
$table->recordActions([
    EditAction::make(),
    DeleteAction::make(),
    ViewAction::make(),
])
```

### Posisi di Depan

```php
$table->recordActions([...])->position(ActionPosition::BeforeColumns)
```

---

## 📦 Bulk Actions

```php
use Filament\Actions\BulkActionGroup;
use Filament\Actions\DeleteBulkAction;

$table->toolbarActions([
    BulkActionGroup::make([
        DeleteBulkAction::make(),
        ExportBulkAction::make(),
    ]),
])
```

### Custom Bulk Action

```php
BulkAction::make('updateStatus')
    ->label('Update Status')
    ->icon('heroicon-o-check')
    ->action(function (Collection $records, array $data) {
        $records->each->update(['status' => $data['status']]);
    })
    ->schema([
        Select::make('status')
            ->options([
                'published' => 'Published',
                'draft' => 'Draft',
            ])
            ->required(),
    ])
    ->requiresConfirmation()
    ->deselectRecordsAfterCompletion()
```

---

## 🔝 Header Actions

```php
$table->headerActions([
    CreateAction::make(),
    ImportAction::make(),
])
```

---

## 📊 Column Actions

```php
TextColumn::make('email')
    ->action(
        Action::make('send_email')
            ->action(fn ($record) => Mail::to($record)->send(...))
    )
```

---

## 📁 Grouping Actions

```php
ActionGroup::make([
    EditAction::make(),
    DeleteAction::make(),
])->dropdown()
```

---

## 🔒 Authorization Bulk Action

```php
DeleteBulkAction::make()
    ->authorizeIndividualRecords()
```

---

## 🔔 Bulk Action Notifications

```php
DeleteBulkAction::make()
    ->successNotificationTitle('Records deleted')
    ->failureNotificationTitle('Some records failed to delete')
```

---

## 🎯 Latihan Mandiri

Buat:

- Record action untuk "Duplicate"
- Bulk action untuk "Update Category"
