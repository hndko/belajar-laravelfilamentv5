# 05. Customization & Branding

## 🎨 Mengubah Warna & Branding

Edit `app/Providers/Filament/AdminPanelProvider.php`:

```php
use Filament\Support\Colors\Color;

public function panel(Panel $panel): Panel
{
    return $panel
        ->default()
        ->id('admin')
        ->path('admin')
        ->login()
        ->brandName('Blog Admin')
        ->brandLogo(asset('images/logo.png'))  // Optional
        ->favicon(asset('images/favicon.ico')) // Optional
        ->colors([
            'primary' => Color::Blue,
            'danger' => Color::Rose,
            'success' => Color::Emerald,
            'warning' => Color::Orange,
        ])
        ->font('Poppins')
        // ... sisanya
}
```

## 📊 Menambah Widget Dashboard

Buat widget stats:

```bash
php artisan make:filament-widget StatsOverview --stats-overview
```

Edit `app/Filament/Widgets/StatsOverview.php`:

```php
<?php

namespace App\Filament\Widgets;

use App\Models\Category;
use App\Models\Post;
use Filament\Widgets\StatsOverviewWidget as BaseWidget;
use Filament\Widgets\StatsOverviewWidget\Stat;

class StatsOverview extends BaseWidget
{
    protected function getStats(): array
    {
        return [
            Stat::make('Total Kategori', Category::count())
                ->description('Kategori tersedia')
                ->icon('heroicon-o-folder')
                ->color('success'),

            Stat::make('Total Artikel', Post::count())
                ->description('Artikel dibuat')
                ->icon('heroicon-o-document-text')
                ->color('primary'),

            Stat::make('Artikel Published', Post::where('status', 'published')->count())
                ->description('Sudah dipublish')
                ->icon('heroicon-o-check-circle')
                ->color('success'),

            Stat::make('Artikel Draft', Post::where('status', 'draft')->count())
                ->description('Masih draft')
                ->icon('heroicon-o-pencil')
                ->color('warning'),
        ];
    }
}
```

## 📋 Widget Latest Posts

```bash
php artisan make:filament-widget LatestPosts --table
```

Edit `app/Filament/Widgets/LatestPosts.php`:

```php
<?php

namespace App\Filament\Widgets;

use App\Models\Post;
use Filament\Tables;
use Filament\Tables\Table;
use Filament\Widgets\TableWidget as BaseWidget;

class LatestPosts extends BaseWidget
{
    protected static ?int $sort = 2;
    protected int | string | array $columnSpan = 'full';

    public function table(Table $table): Table
    {
        return $table
            ->query(Post::query()->latest()->limit(5))
            ->columns([
                Tables\Columns\TextColumn::make('title')
                    ->label('Judul')
                    ->limit(50),
                Tables\Columns\TextColumn::make('category.name')
                    ->label('Kategori')
                    ->badge(),
                Tables\Columns\BadgeColumn::make('status')
                    ->colors([
                        'warning' => 'draft',
                        'success' => 'published',
                    ]),
                Tables\Columns\TextColumn::make('created_at')
                    ->label('Dibuat')
                    ->dateTime('d M Y H:i'),
            ])
            ->paginated(false);
    }
}
```

## 🔧 Navigation Grouping

Edit resource untuk grouping:

```php
// Di CategoryResource.php dan PostResource.php
protected static ?string $navigationGroup = 'Blog';
protected static ?int $navigationSort = 1; // Urutan dalam group
```

## ✅ Hasil

- Dashboard dengan statistik
- Warna tema custom
- Widget latest posts
- Menu terorganisir

## ➡️ Selanjutnya

Lanjut ke: [06-deploy.md](06-deploy.md)
