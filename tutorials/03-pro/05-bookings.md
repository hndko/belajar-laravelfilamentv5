# 05. Booking System

## 🎛️ Booking Resource (Vendor Panel)

```bash
php artisan make:filament-resource Booking --panel=vendor
```

Edit `app/Filament/Vendor/Resources/BookingResource.php`:

```php
<?php

namespace App\Filament\Vendor\Resources;

use App\Filament\Vendor\Resources\BookingResource\Pages;
use App\Models\Booking;
use Filament\Forms;
use Filament\Forms\Form;
use Filament\Resources\Resource;
use Filament\Tables;
use Filament\Tables\Table;

class BookingResource extends Resource
{
    protected static ?string $model = Booking::class;
    protected static ?string $navigationIcon = 'heroicon-o-calendar-days';

    public static function form(Form $form): Form
    {
        return $form
            ->schema([
                Forms\Components\Section::make('Booking Details')
                    ->schema([
                        Forms\Components\Select::make('service_id')
                            ->relationship('service', 'name')
                            ->required()
                            ->live()
                            ->afterStateUpdated(function ($state, $set) {
                                $service = \App\Models\Service::find($state);
                                if ($service) {
                                    $set('total_price', $service->price);
                                }
                            }),

                        Forms\Components\Select::make('customer_id')
                            ->relationship('customer', 'name')
                            ->searchable()
                            ->preload()
                            ->required(),

                        Forms\Components\DatePicker::make('date')
                            ->required()
                            ->minDate(now()),

                        Forms\Components\TimePicker::make('start_time')
                            ->required()
                            ->seconds(false),

                        Forms\Components\TimePicker::make('end_time')
                            ->required()
                            ->seconds(false)
                            ->after('start_time'),

                        Forms\Components\Select::make('status')
                            ->options([
                                'pending' => 'Pending',
                                'confirmed' => 'Confirmed',
                                'completed' => 'Completed',
                                'cancelled' => 'Cancelled',
                            ])
                            ->default('pending')
                            ->required(),

                        Forms\Components\TextInput::make('total_price')
                            ->numeric()
                            ->prefix('Rp')
                            ->required(),

                        Forms\Components\Textarea::make('notes')
                            ->rows(2),
                    ])
                    ->columns(2),
            ]);
    }

    public static function table(Table $table): Table
    {
        return $table
            ->columns([
                Tables\Columns\TextColumn::make('date')
                    ->date('d M Y')
                    ->sortable(),

                Tables\Columns\TextColumn::make('start_time')
                    ->time('H:i'),

                Tables\Columns\TextColumn::make('service.name')
                    ->label('Layanan'),

                Tables\Columns\TextColumn::make('customer.name')
                    ->label('Customer')
                    ->searchable(),

                Tables\Columns\BadgeColumn::make('status')
                    ->colors([
                        'warning' => 'pending',
                        'primary' => 'confirmed',
                        'success' => 'completed',
                        'danger' => 'cancelled',
                    ]),

                Tables\Columns\TextColumn::make('total_price')
                    ->money('IDR'),
            ])
            ->defaultSort('date', 'desc')
            ->filters([
                Tables\Filters\SelectFilter::make('status')
                    ->options([
                        'pending' => 'Pending',
                        'confirmed' => 'Confirmed',
                        'completed' => 'Completed',
                        'cancelled' => 'Cancelled',
                    ]),

                Tables\Filters\Filter::make('today')
                    ->query(fn ($query) => $query->whereDate('date', today())),
            ])
            ->actions([
                Tables\Actions\Action::make('confirm')
                    ->icon('heroicon-o-check')
                    ->color('success')
                    ->visible(fn ($record) => $record->status === 'pending')
                    ->action(fn ($record) => $record->update(['status' => 'confirmed'])),

                Tables\Actions\Action::make('complete')
                    ->icon('heroicon-o-check-circle')
                    ->color('primary')
                    ->visible(fn ($record) => $record->status === 'confirmed')
                    ->action(fn ($record) => $record->update(['status' => 'completed'])),

                Tables\Actions\EditAction::make(),
            ]);
    }

    public static function getPages(): array
    {
        return [
            'index' => Pages\ListBookings::route('/'),
            'create' => Pages\CreateBooking::route('/create'),
            'edit' => Pages\EditBooking::route('/{record}/edit'),
        ];
    }
}
```

## 👤 Customer Booking Page

Buat di Customer panel `app/Filament/App/Pages/CreateBooking.php`:

```php
<?php

namespace App\Filament\App\Pages;

use App\Models\Booking;
use App\Models\Service;
use App\Models\Team;
use Filament\Forms;
use Filament\Forms\Concerns\InteractsWithForms;
use Filament\Forms\Form;
use Filament\Notifications\Notification;
use Filament\Pages\Page;

class CreateBooking extends Page
{
    use InteractsWithForms;

    protected static ?string $navigationIcon = 'heroicon-o-plus-circle';
    protected static ?string $title = 'Book Service';
    protected static string $view = 'filament.app.pages.create-booking';

    public ?array $data = [];

    public function mount(): void
    {
        $this->form->fill();
    }

    public function form(Form $form): Form
    {
        return $form
            ->schema([
                Forms\Components\Select::make('team_id')
                    ->label('Pilih Vendor')
                    ->options(Team::where('is_active', true)->pluck('name', 'id'))
                    ->required()
                    ->live(),

                Forms\Components\Select::make('service_id')
                    ->label('Pilih Layanan')
                    ->options(fn ($get) =>
                        Service::where('team_id', $get('team_id'))
                            ->where('is_active', true)
                            ->pluck('name', 'id')
                    )
                    ->required()
                    ->live(),

                Forms\Components\DatePicker::make('date')
                    ->required()
                    ->minDate(now()),

                Forms\Components\TimePicker::make('start_time')
                    ->required(),

                Forms\Components\Textarea::make('notes'),
            ])
            ->statePath('data');
    }

    public function submit(): void
    {
        $data = $this->form->getState();
        $service = Service::find($data['service_id']);

        Booking::create([
            'team_id' => $data['team_id'],
            'service_id' => $data['service_id'],
            'customer_id' => auth()->id(),
            'date' => $data['date'],
            'start_time' => $data['start_time'],
            'end_time' => now()->parse($data['start_time'])
                ->addMinutes($service->duration_minutes)->format('H:i'),
            'total_price' => $service->price,
            'notes' => $data['notes'],
            'status' => 'pending',
        ]);

        Notification::make()
            ->success()
            ->title('Booking berhasil!')
            ->send();

        $this->redirect(MyBookings::getUrl());
    }
}
```

## ➡️ Selanjutnya

Lanjut ke: [06-policies.md](06-policies.md)
