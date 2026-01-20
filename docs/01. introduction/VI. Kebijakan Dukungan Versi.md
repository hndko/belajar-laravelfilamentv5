# VI. Kebijakan Dukungan Versi 📅

> **Sumber:** [https://filamentphp.com/docs/5.x/introduction/version-support-policy](https://filamentphp.com/docs/5.x/introduction/version-support-policy)

---

## 🤔 Apa Maksudnya?

Seperti software lainnya, Filament terus berkembang. Ada versi baru yang rilis secara berkala (Filament 3, 4, 5, dst).

Kebijakan ini menjelaskan **berapa lama** setiap versi akan didukung (dapat update, perbaikan bug, dll).

### Analoginya:

Bayangkan smartphone. Setelah beberapa tahun, pabriknya berhenti memberikan update. Sama dengan Filament - versi lama pada akhirnya tidak akan didukung lagi.

---

## 📦 Jenis-jenis Update

### 1. Fitur Baru (New Features) ✨

**Apa itu?**
Penambahan kemampuan baru ke Filament.

**Contoh:** Komponen form baru, integrasi dengan tools baru, dll.

**Didukung untuk:**
Hanya versi mayor **terbaru** saja.

**Artinya:**
Jika Filament 5 adalah yang terbaru, fitur baru hanya akan ditambahkan ke Filament 5 - tidak ke Filament 4, 3, dst.

---

### 2. Perbaikan Bug (Bug Fixes) 🐛

**Apa itu?**
Memperbaiki kesalahan/error yang ditemukan di Filament.

**Didukung untuk:**

- Versi mayor **terbaru** (utama)
- Versi mayor **sebelumnya** (selama 1 tahun)

**Contoh:**
| Versi | Status |
|-------|--------|
| Filament 5 (terbaru) | ✅ Dapat bug fix |
| Filament 4 (sebelumnya) | ✅ Dapat bug fix (1 tahun) |
| Filament 3 | ❌ Tidak dapat bug fix lagi |

---

### 3. Perbaikan Keamanan (Security Fixes) 🔒

**Apa itu?**
Memperbaiki celah keamanan yang bisa dieksploitasi hacker.

**Didukung untuk:**
Minimal **2 tahun** sejak rilis.

**Artinya:**
Ini yang paling lama didukung karena keamanan itu penting!

---

## 📊 Tabel Ringkasan

| Jenis Update | Versi yang Didukung        | Durasi Dukungan                |
| ------------ | -------------------------- | ------------------------------ |
| Fitur Baru   | Versi terbaru saja         | Selama jadi versi terbaru      |
| Bug Fix      | Versi terbaru + sebelumnya | 1 tahun untuk versi sebelumnya |
| Security Fix | Beberapa versi             | Minimal 2 tahun                |

---

## ⚠️ Peringatan Penting

### Dependencies Juga Penting!

Filament bergantung pada:

- **PHP** (versi minimal tertentu)
- **Laravel** (versi minimal tertentu)
- **Livewire** (versi minimal tertentu)

Walaupun versi Filament-mu masih dapat security fix, kalau **Laravel** atau **PHP** yang kamu pakai sudah tidak didukung, aplikasimu tetap rentan!

**Contoh:**

```
Filament 4 masih dapat security fix
TAPI
PHP 8.0 yang kamu pakai sudah tidak didukung

= Aplikasimu tetap rentan!
```

**Solusi:** Selalu update PHP dan Laravel juga, tidak hanya Filament.

---

## 🚨 Melaporkan Celah Keamanan

Jika kamu menemukan celah keamanan di Filament:

1. **JANGAN** posting di Discord atau GitHub Issues (publik)
2. **Laporkan secara private** melalui: [GitHub Security Advisory](https://github.com/filamentphp/filament/security/advisories)

Tim Filament akan merespons dengan cepat!

---

## 💡 Apa yang Harus Dilakukan?

### Untuk Proyek Baru:

Selalu gunakan **versi terbaru** Filament!

### Untuk Proyek Lama:

1. Cek versi Filament yang kamu pakai:

   ```bash
   composer show filament/filament
   ```

2. Lihat apakah masih didukung

3. Jika sudah tidak didukung, **upgrade** ke versi lebih baru

---

## 📅 Kenapa Harus Upgrade?

| Risiko Tidak Upgrade          | Dampak                        |
| ----------------------------- | ----------------------------- |
| Bug tidak diperbaiki          | Aplikasi error terus          |
| Celah keamanan tidak ditambal | Bisa di-hack                  |
| Tidak dapat fitur baru        | Ketinggalan                   |
| Sulit cari bantuan            | Komunitas fokus di versi baru |

---

## 🔄 Cara Upgrade Filament

Tutorial upgrade ada di dokumentasi resmi. Biasanya langkahnya:

1. **Backup** proyekmu dulu!
2. **Baca** upgrade guide untuk versi yang dituju
3. **Update** composer.json
4. **Jalankan** perintah upgrade
5. **Test** semua fitur aplikasimu

---

## 💡 Ringkasan

1. **Fitur baru** = Hanya untuk versi terbaru
2. **Bug fix** = Versi terbaru + 1 tahun untuk versi sebelumnya
3. **Security fix** = Minimal 2 tahun
4. Selalu **update** PHP & Laravel juga, bukan hanya Filament
5. Lapor celah keamanan **secara private**

---

## 🎯 Latihan Mandiri

1. Cek versi Filament di proyekmu:

   ```bash
   composer show filament/filament
   ```

2. Cek versi PHP:

   ```bash
   php -v
   ```

3. Cek versi Laravel:

   ```bash
   php artisan --version
   ```

4. Pastikan semuanya masih didukung!

<details>
<summary>Cara Cek Apakah Versi Masih Didukung?</summary>

**PHP:** Cek di [https://www.php.net/supported-versions.php](https://www.php.net/supported-versions.php)

**Laravel:** Cek di [https://laravel.com/docs/releases](https://laravel.com/docs/releases)

**Filament:** Lihat dokumentasi versi yang kamu pakai - jika masih ada di website resmi, berarti masih didukung.

</details>
