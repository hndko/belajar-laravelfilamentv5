# II. CSS Hooks 🪝

> **Sumber:** [https://filamentphp.com/docs/5.x/styling/css-hooks](https://filamentphp.com/docs/5.x/styling/css-hooks)

---

## 🤔 Apa itu CSS Hooks?

**CSS Hooks** adalah class CSS khusus di Filament yang bisa digunakan untuk styling kustom tanpa publish views.

---

## 🔍 Discovering Hook Classes

Buka browser DevTools dan inspect element. Class yang diawali `fi-` adalah hook classes.

Contoh:

- `fi-sidebar`
- `fi-topbar`
- `fi-header`
- `fi-body`
- `fi-ta-` (table)
- `fi-fo-` (form)

---

## 🎨 Applying Styles

```css
/* resources/css/filament/admin/theme.css */

.fi-sidebar {
  background: linear-gradient(to bottom, #1e3a8a, #1e40af);
}

.fi-topbar {
  border-bottom: 2px solid #3b82f6;
}

.fi-header-heading {
  font-size: 1.5rem;
  font-weight: 700;
}
```

---

## 📋 Common Abbreviations

| Prefix   | Component     |
| -------- | ------------- |
| `fi-ac-` | Actions       |
| `fi-fo-` | Forms         |
| `fi-in-` | Infolists     |
| `fi-no-` | Notifications |
| `fi-ta-` | Tables        |
| `fi-wi-` | Widgets       |
| `fi-pa-` | Panels        |
| `fi-btn` | Buttons       |

---

## 📝 Contoh Hook Classes

```css
/* Warna sidebar */
.fi-sidebar {
  --c-50: theme("colors.blue.50");
  --c-100: theme("colors.blue.100");
}

/* Button primary */
.fi-btn-primary {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

/* Table row hover */
.fi-ta-row:hover {
  background-color: theme("colors.blue.50");
}

/* Form field focus */
.fi-fo-field-wrp:focus-within {
  border-color: theme("colors.primary.500");
}
```

---

## 📦 Publishing Blade Views

Jika perlu lebih banyak kontrol:

```bash
php artisan vendor:publish --tag=filament-panels-views
```

---

## 🎯 Latihan Mandiri

Kustomisasi dengan CSS hooks:

- Warna gradient sidebar
- Custom button style
- Table row hover effect
