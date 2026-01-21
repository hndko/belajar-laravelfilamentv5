# XXIII. Custom Data Source 🌐

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/custom-data](https://filamentphp.com/docs/5.x/tables/custom-data)

---

## 🤔 Kapan Pakai Custom Data?

Gunakan ketika sumber data bukan dari Eloquent:

- External API
- Array statis
- CSV file
- Redis cache

---

## 📋 Columns dari Array

```php
$table
    ->query(fn () => collect([
        ['id' => 1, 'name' => 'John', 'email' => 'john@example.com'],
        ['id' => 2, 'name' => 'Jane', 'email' => 'jane@example.com'],
    ]))
    ->columns([
        TextColumn::make('name'),
        TextColumn::make('email'),
    ])
```

---

## 🔀 Custom Sorting

```php
TextColumn::make('name')
    ->sortable()
    ->sortUsing(function ($query, string $direction) {
        return $query->sortBy(
            fn ($item) => $item['name'],
            descending: $direction === 'desc'
        );
    })
```

---

## 🔍 Custom Searching

```php
TextColumn::make('name')
    ->searchable()
    ->searchUsing(function ($query, string $search) {
        return $query->filter(fn ($item) =>
            str_contains(strtolower($item['name']), strtolower($search))
        );
    })
```

---

## 🔍 Custom Filtering

```php
Filter::make('active')
    ->query(function ($query) {
        return $query->filter(fn ($item) => $item['is_active']);
    })
```

---

## 📑 Custom Pagination

```php
$table
    ->query(fn () => $this->getExternalData())
    ->paginated([10, 25, 50])
```

---

## 🌐 External API Example

```php
class ListProducts extends ListRecords
{
    protected function getTableQuery(): Collection
    {
        $response = Http::get('https://api.example.com/products');
        return collect($response->json('data'));
    }
}
```

### Dengan Sorting

```php
protected function getTableQuery(): Collection
{
    $sortColumn = $this->getTableSortColumn();
    $sortDirection = $this->getTableSortDirection();

    $response = Http::get('https://api.example.com/products', [
        'sort' => $sortColumn,
        'order' => $sortDirection,
    ]);

    return collect($response->json('data'));
}
```

### Dengan Searching

```php
protected function getTableQuery(): Collection
{
    $search = $this->getTableSearch();

    $response = Http::get('https://api.example.com/products', [
        'search' => $search,
    ]);

    return collect($response->json('data'));
}
```

---

## ⚡ Actions untuk Custom Data

```php
Action::make('view')
    ->action(function (array $record) {
        // $record adalah item dari array
        $this->dispatch('open-modal', id: $record['id']);
    })
```

---

## 🎯 Latihan Mandiri

Buat tabel yang menampilkan data dari:

- Array sederhana dengan 5 items
- Custom sorting dan searching
