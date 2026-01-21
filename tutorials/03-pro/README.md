# 🎓 Tutorial Pro: Multi-Tenant Booking SaaS

> **Level:** Pro | **Durasi:** 8-10 Jam | **Project:** Multi-Tenant Booking System

---

## 📋 Apa yang Akan Dipelajari

| Topik                | Keterangan                           |
| -------------------- | ------------------------------------ |
| ✅ Multi-Panel       | Admin, Vendor, Customer panels       |
| ✅ Multi-Tenant      | Tenant isolation dengan Team/Company |
| ✅ Complex Relations | Polymorphic, Many-to-Many            |
| ✅ Policies & Gates  | Advanced authorization               |
| ✅ Real-time         | Broadcasting & notifications         |
| ✅ Testing           | Feature & unit tests                 |
| ✅ Production        | Full deployment dengan CI/CD         |

---

## 📁 Struktur Tutorial

1. [00-overview.md](00-overview.md) - Architecture & ERD
2. [01-setup.md](01-setup.md) - Project setup
3. [02-multi-panel.md](02-multi-panel.md) - Setup 3 panels
4. [03-multi-tenant.md](03-multi-tenant.md) - Team-based tenancy
5. [04-services.md](04-services.md) - Services management
6. [05-bookings.md](05-bookings.md) - Booking system
7. [06-policies.md](06-policies.md) - Advanced authorization
8. [07-realtime.md](07-realtime.md) - Real-time features
9. [08-testing.md](08-testing.md) - Automated testing
10. [09-production.md](09-production.md) - Production deployment

---

## 🎯 Hasil Akhir

Aplikasi booking SaaS dengan:

- **Admin Panel**: Manage all tenants, users, reports
- **Vendor Panel**: Manage services, bookings, schedule
- **Customer Panel**: Browse, book, payment

---

## 📊 Database Design

```
teams (tenants)
├── id
├── name
├── slug
└── owner_id

users
├── id
├── name
├── email
├── role (superadmin/admin/vendor/customer)
└── current_team_id

team_user (pivot)
├── team_id
├── user_id
└── role

services
├── id
├── team_id
├── name
├── description
├── duration_minutes
├── price
└── is_active

schedules
├── id
├── team_id
├── day_of_week
├── start_time
├── end_time

bookings
├── id
├── team_id
├── service_id
├── customer_id
├── date
├── start_time
├── end_time
├── status (pending/confirmed/completed/cancelled)
├── total_price
└── notes
```

---

## 🚀 Mulai Belajar

Lanjut ke: [00-overview.md](00-overview.md)
