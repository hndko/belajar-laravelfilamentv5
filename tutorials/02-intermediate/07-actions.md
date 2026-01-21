# 07. Custom Actions

## ⚡ Quick Stock Actions

Tambahkan di `ProductResource.php` actions:

```php
->actions([
    Tables\Actions\Action::make('stock_in')
        ->label('Stock In')
        ->icon('heroicon-o-plus-circle')
        ->color('success')
        ->form([
            Forms\Components\TextInput::make('quantity')
                ->label('Jumlah')
                ->numeric()
                ->required()
                ->minValue(1),
            Forms\Components\Textarea::make('notes')
                ->label('Catatan'),
        ])
        ->action(function (Product $record, array $data) {
            Transaction::create([
                'product_id' => $record->id,
                'user_id' => auth()->id(),
                'type' => 'in',
                'quantity' => $data['quantity'],
                'notes' => $data['notes'] ?? null,
            ]);

            $record->increment('stock', $data['quantity']);

            Notification::make()
                ->success()
                ->title('Stock In berhasil!')
                ->body("Stok {$record->name}: {$record->fresh()->stock}")
                ->send();
        }),

    Tables\Actions\Action::make('stock_out')
        ->label('Stock Out')
        ->icon('heroicon-o-minus-circle')
        ->color('danger')
        ->form([
            Forms\Components\TextInput::make('quantity')
                ->label('Jumlah')
                ->numeric()
                ->required()
                ->minValue(1),
            Forms\Components\Textarea::make('notes')
                ->label('Catatan'),
        ])
        ->action(function (Product $record, array $data) {
            if ($record->stock < $data['quantity']) {
                Notification::make()
                    ->danger()
                    ->title('Stok tidak mencukupi!')
                    ->send();
                return;
            }

            Transaction::create([
                'product_id' => $record->id,
                'user_id' => auth()->id(),
                'type' => 'out',
                'quantity' => $data['quantity'],
                'notes' => $data['notes'] ?? null,
            ]);

            $record->decrement('stock', $data['quantity']);

            Notification::make()
                ->success()
                ->title('Stock Out berhasil!')
                ->send();
        }),

    Tables\Actions\EditAction::make(),
])
```

## 📦 Bulk Actions

```php
->bulkActions([
    Tables\Actions\BulkActionGroup::make([
        Tables\Actions\DeleteBulkAction::make(),

        Tables\Actions\BulkAction::make('bulk_stock_in')
            ->label('Bulk Stock In')
            ->icon('heroicon-o-plus-circle')
            ->color('success')
            ->form([
                Forms\Components\TextInput::make('quantity')
                    ->label('Jumlah per produk')
                    ->numeric()
                    ->required(),
            ])
            ->action(function ($records, array $data) {
                foreach ($records as $record) {
                    Transaction::create([
                        'product_id' => $record->id,
                        'user_id' => auth()->id(),
                        'type' => 'in',
                        'quantity' => $data['quantity'],
                        'notes' => 'Bulk stock in',
                    ]);
                    $record->increment('stock', $data['quantity']);
                }

                Notification::make()
                    ->success()
                    ->title(count($records) . ' produk di-update')
                    ->send();
            })
            ->deselectRecordsAfterCompletion(),
    ]),
])
```

## 📤 Export Action

```php
Tables\Actions\Action::make('export')
    ->label('Export CSV')
    ->icon('heroicon-o-arrow-down-tray')
    ->action(function () {
        return response()->streamDownload(function () {
            $products = Product::with(['category', 'supplier'])->get();

            echo "SKU,Nama,Kategori,Supplier,Stok,Harga\n";

            foreach ($products as $product) {
                echo "{$product->sku},{$product->name},{$product->category->name},{$product->supplier->name},{$product->stock},{$product->price}\n";
            }
        }, 'products-' . now()->format('Y-m-d') . '.csv');
    }),
```

## ➡️ Selanjutnya

Lanjut ke: [08-notifications.md](08-notifications.md)
