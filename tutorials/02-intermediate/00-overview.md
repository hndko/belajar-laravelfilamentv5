# 00. Project Overview

## 🎯 Tentang Project

Kita akan membuat **Inventory Management System** dengan fitur:

- Kelola data supplier
- Kelola data product dengan kategori
- Transaksi stock masuk/keluar
- Dashboard dengan grafik
- Multi-role access control

## 👥 User Roles

| Role      | Akses                                             |
| --------- | ------------------------------------------------- |
| **Admin** | Full access semua fitur                           |
| **Staff** | CRUD products & transactions, view-only suppliers |

## 📦 Fitur Utama

### 1. Suppliers

- CRUD suppliers (Admin only)
- View list (Staff)

### 2. Products

- CRUD products
- Relasi ke category & supplier
- Track stock quantity
- Low stock alerts

### 3. Transactions

- Stock in (pembelian)
- Stock out (penjualan)
- History log
- Auto update stock

### 4. Dashboard

- Total products
- Low stock alerts
- Recent transactions
- Stock movement chart

## 🔧 Tech Stack

- Laravel 11
- Filament v5
- MySQL
- Nginx (production)

## ➡️ Selanjutnya

Lanjut ke: [01-setup.md](01-setup.md)
