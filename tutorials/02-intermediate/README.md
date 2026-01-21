# 🎓 Tutorial Intermediate: Inventory Management System

> **Level:** Intermediate | **Durasi:** 4-6 Jam | **Project:** Inventory Management

---

## 📋 Apa yang Akan Dipelajari

| Topik             | Keterangan                         |
| ----------------- | ---------------------------------- |
| ✅ Multi-Role     | Admin & Staff dengan akses berbeda |
| ✅ Relasi Complex | HasMany, BelongsTo, BelongsToMany  |
| ✅ Widgets        | Stats & Chart dashboards           |
| ✅ Actions        | Custom actions & bulk actions      |
| ✅ Notifications  | Toast & database notifications     |
| ✅ Deploy         | VPS dengan Nginx                   |

---

## 📁 Struktur Tutorial

1. [00-overview.md](00-overview.md) - Project overview & ERD
2. [01-setup.md](01-setup.md) - Setup project & migrations
3. [02-multi-role.md](02-multi-role.md) - Implementasi multi-role
4. [03-suppliers.md](03-suppliers.md) - CRUD suppliers
5. [04-products.md](04-products.md) - CRUD products dengan relasi
6. [05-transactions.md](05-transactions.md) - Stock in/out
7. [06-widgets.md](06-widgets.md) - Dashboard widgets & charts
8. [07-actions.md](07-actions.md) - Custom actions
9. [08-notifications.md](08-notifications.md) - Notifications system
10. [09-deploy-vps.md](09-deploy-vps.md) - Deploy ke VPS

---

## 🎯 Hasil Akhir

Aplikasi inventory management dengan:

- Multi-role (Admin full access, Staff limited)
- Kelola suppliers, products, categories
- Stock in/out transactions
- Dashboard dengan statistik realtime
- Export data

---

## 📊 Database Design (ERD)

```
users
├── id
├── name
├── email
├── role (admin/staff)
└── password

categories
├── id
└── name

suppliers
├── id
├── name
├── phone
├── email
└── address

products
├── id
├── category_id (FK)
├── supplier_id (FK)
├── name
├── sku
├── price
├── stock
└── min_stock

transactions
├── id
├── product_id (FK)
├── user_id (FK)
├── type (in/out)
├── quantity
├── notes
└── created_at
```

---

## 🚀 Mulai Belajar

Lanjut ke: [00-overview.md](00-overview.md)
