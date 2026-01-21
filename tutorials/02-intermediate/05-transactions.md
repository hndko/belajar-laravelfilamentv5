# 05. Transactions Resource

## 🎛️ Buat Resource

```bash
php artisan make:filament-resource Transaction --generate
```

## ✏️ Transaction Resource

Edit `app/Filament/Resources/TransactionResource.php`:

```php
<?php

namespace App\Filament\Resources;

use App\Filament\Resources\TransactionResource\Pages;
use App\Models\Transaction;
use App\Models\Product;
use Filament\Forms;
use Filament\Forms\Form;
use Filament\Resources\Resource;
use Filament\Tables;
use Filament\Tables\Table;

class TransactionResource extends Resource
{
    protected static ?string $model = Transaction::class;
    protected static ?string $navigationIcon = 'heroicon-o-arrows-right-left';
    protected static ?string $navigationGroup = 'Inventory';
    protected static ?string $modelLabel = 'Transaksi';

    public static function form(Form $form): Form
    {
        return $form
            ->schema([
                Forms\Components\Section::make()
                    ->schema([
                        Forms\Components\Select::make('product_id')
                            ->label('Produk')
                            ->relationship('product', 'name')
                            ->searchable()
                            ->preload()
                            ->required()
                            ->live()
                            ->afterStateUpdated(fn ($state, $set) =>
                                $set('current_stock', Product::find($state)?->stock ?? 0)
                            ),

                        Forms\Components\Placeholder::make('current_stock')
                            ->label('Stok Saat Ini')
                            ->content(fn ($get) =>
                                Product::find($get('product_id'))?->stock ?? '-'
                            ),

                        Forms\Components\Select::make('type')
                            ->label('Tipe')
                            ->options([
                                'in' => '📥 Stock In (Masuk)',
                                'out' => '📤 Stock Out (Keluar)',
                            ])
                            ->required(),

                        Forms\Components\TextInput::make('quantity')
                            ->label('Jumlah')
                            ->numeric()
                            ->required()
                            ->minValue(1),

                        Forms\Components\Textarea::make('notes')
                            ->label('Catatan')
                            ->rows(2)
                            ->columnSpanFull(),

                        Forms\Components\Hidden::make('user_id')
                            ->default(auth()->id()),
                    ])
                    ->columns(2),
            ]);
    }

    public static function table(Table $table): Table
    {
        return $table
            ->columns([
                Tables\Columns\TextColumn::make('created_at')
                    ->label('Tanggal')
                    ->dateTime('d M Y H:i')
                    ->sortable(),

                Tables\Columns\TextColumn::make('product.name')
                    ->label('Produk')
                    ->searchable()
                    ->sortable(),

                Tables\Columns\BadgeColumn::make('type')
                    ->label('Tipe')
                    ->colors([
                        'success' => 'in',
                        'danger' => 'out',
                    ])
                    ->formatStateUsing(fn ($state) =>
                        $state === 'in' ? 'Stock In' : 'Stock Out'
                    ),

                Tables\Columns\TextColumn::make('quantity')
                    ->label('Jumlah')
                    ->sortable(),

                Tables\Columns\TextColumn::make('user.name')
                    ->label('Oleh')
                    ->sortable(),

                Tables\Columns\TextColumn::make('notes')
                    ->label('Catatan')
                    ->limit(30),
            ])
            ->defaultSort('created_at', 'desc')
            ->filters([
                Tables\Filters\SelectFilter::make('type')
                    ->options([
                        'in' => 'Stock In',
                        'out' => 'Stock Out',
                    ]),

                Tables\Filters\SelectFilter::make('product')
                    ->relationship('product', 'name'),
            ])
            ->actions([
                Tables\Actions\ViewAction::make(),
            ]);
    }

    public static function getPages(): array
    {
        return [
            'index' => Pages\ListTransactions::route('/'),
            'create' => Pages\CreateTransaction::route('/create'),
        ];
    }
}
```

## 🔄 Auto Update Stock

Edit `app/Filament/Resources/TransactionResource/Pages/CreateTransaction.php`:

```php
<?php

namespace App\Filament\Resources\TransactionResource\Pages;

use App\Filament\Resources\TransactionResource;
use App\Models\Product;
use Filament\Resources\Pages\CreateRecord;
use Filament\Notifications\Notification;

class CreateTransaction extends CreateRecord
{
    protected static string $resource = TransactionResource::class;

    protected function afterCreate(): void
    {
        $transaction = $this->record;
        $product = Product::find($transaction->product_id);

        if ($transaction->type === 'in') {
            $product->increment('stock', $transaction->quantity);
        } else {
            if ($product->stock < $transaction->quantity) {
                Notification::make()
                    ->danger()
                    ->title('Stok tidak mencukupi!')
                    ->send();
                return;
            }
            $product->decrement('stock', $transaction->quantity);
        }

        Notification::make()
            ->success()
            ->title('Transaksi berhasil!')
            ->body("Stok {$product->name} sekarang: {$product->fresh()->stock}")
            ->send();
    }
}
```

## ➡️ Selanjutnya

Lanjut ke: [06-widgets.md](06-widgets.md)
