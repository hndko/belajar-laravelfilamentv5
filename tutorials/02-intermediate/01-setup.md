# 01. Setup Project & Migrations

## 🚀 Step 1: Buat Project

```bash
composer create-project laravel/laravel inventory-filament
cd inventory-filament
composer require filament/filament:"^3.2"
php artisan filament:install --panels
```

## 🗄️ Step 2: Buat Semua Migrations

### Users (modify existing)

```bash
php artisan make:migration add_role_to_users_table
```

```php
public function up(): void
{
    Schema::table('users', function (Blueprint $table) {
        $table->enum('role', ['admin', 'staff'])->default('staff')->after('email');
    });
}
```

### Categories

```bash
php artisan make:model Category -m
```

```php
Schema::create('categories', function (Blueprint $table) {
    $table->id();
    $table->string('name');
    $table->timestamps();
});
```

### Suppliers

```bash
php artisan make:model Supplier -m
```

```php
Schema::create('suppliers', function (Blueprint $table) {
    $table->id();
    $table->string('name');
    $table->string('phone')->nullable();
    $table->string('email')->nullable();
    $table->text('address')->nullable();
    $table->timestamps();
});
```

### Products

```bash
php artisan make:model Product -m
```

```php
Schema::create('products', function (Blueprint $table) {
    $table->id();
    $table->foreignId('category_id')->constrained()->cascadeOnDelete();
    $table->foreignId('supplier_id')->constrained()->cascadeOnDelete();
    $table->string('name');
    $table->string('sku')->unique();
    $table->decimal('price', 12, 2);
    $table->integer('stock')->default(0);
    $table->integer('min_stock')->default(5);
    $table->timestamps();
});
```

### Transactions

```bash
php artisan make:model Transaction -m
```

```php
Schema::create('transactions', function (Blueprint $table) {
    $table->id();
    $table->foreignId('product_id')->constrained()->cascadeOnDelete();
    $table->foreignId('user_id')->constrained()->cascadeOnDelete();
    $table->enum('type', ['in', 'out']);
    $table->integer('quantity');
    $table->text('notes')->nullable();
    $table->timestamps();
});
```

## 📦 Step 3: Setup Models

### User.php

```php
protected $fillable = ['name', 'email', 'password', 'role'];

public function isAdmin(): bool
{
    return $this->role === 'admin';
}

public function isStaff(): bool
{
    return $this->role === 'staff';
}
```

### Category.php

```php
protected $fillable = ['name'];

public function products(): HasMany
{
    return $this->hasMany(Product::class);
}
```

### Supplier.php

```php
protected $fillable = ['name', 'phone', 'email', 'address'];

public function products(): HasMany
{
    return $this->hasMany(Product::class);
}
```

### Product.php

```php
protected $fillable = [
    'category_id', 'supplier_id', 'name',
    'sku', 'price', 'stock', 'min_stock'
];

public function category(): BelongsTo
{
    return $this->belongsTo(Category::class);
}

public function supplier(): BelongsTo
{
    return $this->belongsTo(Supplier::class);
}

public function transactions(): HasMany
{
    return $this->hasMany(Transaction::class);
}

public function isLowStock(): bool
{
    return $this->stock <= $this->min_stock;
}
```

### Transaction.php

```php
protected $fillable = ['product_id', 'user_id', 'type', 'quantity', 'notes'];

public function product(): BelongsTo
{
    return $this->belongsTo(Product::class);
}

public function user(): BelongsTo
{
    return $this->belongsTo(User::class);
}
```

## 🔄 Step 4: Migrate & Seed

```bash
php artisan migrate
php artisan make:filament-user
# Buat admin: admin@admin.com, password: password
```

## ➡️ Selanjutnya

Lanjut ke: [02-multi-role.md](02-multi-role.md)
