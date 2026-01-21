# XVII. Filter Layout 📐

> **Sumber:** [https://filamentphp.com/docs/5.x/tables/filters/layout](https://filamentphp.com/docs/5.x/tables/filters/layout)

---

## 📊 Grid Columns

Atur filter dalam grid:

```php
$table->filtersFormColumns(2)  // 2 kolom
```

---

## 📏 Dropdown Width

```php
$table->filtersFormWidth(MaxWidth::ExtraLarge)
```

---

## 📏 Dropdown Max Height

```php
$table->filtersFormMaxHeight('400px')
```

---

## 💬 Filters in Modal

```php
$table->filtersInModal()
```

---

## ⬆️ Filters Above Table

```php
$table->filtersLayout(
    FiltersLayout::AboveContent
)
```

### Collapsible

```php
$table->filtersLayout(FiltersLayout::AboveContentCollapsible)
```

---

## ⬇️ Filters Below Table

```php
$table->filtersLayout(
    FiltersLayout::BelowContent
)
```

---

## ◀️ ▶️ Filters di Samping

### Kiri

```php
$table->filtersLayout(FiltersLayout::Left)
```

### Kanan

```php
$table->filtersLayout(FiltersLayout::Right)
```

---

## 🏷️ Hide Indicators

```php
$table->hiddenFilterIndicators()
```

---

## 🎯 Ringkasan Layout

| Layout             | Posisi          |
| ------------------ | --------------- |
| Default            | Dropdown button |
| `AboveContent`     | Di atas tabel   |
| `BelowContent`     | Di bawah tabel  |
| `Left`             | Di kiri tabel   |
| `Right`            | Di kanan tabel  |
| `filtersInModal()` | Dalam modal     |

---

## 🎯 Latihan Mandiri

Coba berbagai layout filter dan pilih yang paling cocok untuk use case-mu.
