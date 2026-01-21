# 00. Architecture Overview

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    BOOKING SAAS                          │
├──────────────┬──────────────┬──────────────────────────┤
│ Admin Panel  │ Vendor Panel │ Customer Panel           │
│ /admin       │ /vendor      │ /app                     │
├──────────────┴──────────────┴──────────────────────────┤
│                  Shared Services                        │
│  - Authentication  - Authorization  - Notifications     │
├─────────────────────────────────────────────────────────┤
│                     Database                            │
│        MySQL with Multi-tenant Data Isolation           │
└─────────────────────────────────────────────────────────┘
```

## 👥 User Roles

| Role            | Panel    | Capabilities                        |
| --------------- | -------- | ----------------------------------- |
| **Super Admin** | Admin    | Manage all tenants, global settings |
| **Team Admin**  | Admin    | Manage own team settings            |
| **Vendor**      | Vendor   | Manage services, bookings, schedule |
| **Customer**    | Customer | Book services, view history         |

## 🔐 Multi-Tenancy Model

Menggunakan **Team-based Tenancy**:

- Setiap vendor punya Team
- Data di-isolate berdasarkan `team_id`
- Customer bisa book dari berbagai teams

## 📦 Core Features

### Admin Panel

- Dashboard global statistics
- Manage all teams/vendors
- User management
- System settings
- Reports & analytics

### Vendor Panel

- Dashboard team statistics
- Manage services
- Manage schedule
- Handle bookings
- View earnings

### Customer Panel

- Browse vendors
- Search services
- Make bookings
- View booking history
- Profile settings

## 🛠️ Tech Stack

- Laravel 11 + Filament v5
- MySQL
- Laravel Broadcasting (Pusher/Soketi)
- PHPUnit + Pest
- GitHub Actions CI/CD
- Docker (optional)

## ➡️ Selanjutnya

Lanjut ke: [01-setup.md](01-setup.md)
