# III. Pengembangan dengan Bantuan AI 🤖

> **Sumber:** [https://filamentphp.com/docs/5.x/introduction/ai](https://filamentphp.com/docs/5.x/introduction/ai)

---

## 🤔 Apa Maksudnya?

Sekarang ada alat-alat AI (Kecerdasan Buatan) yang bisa membantu kamu menulis kode lebih cepat! Contohnya:

- **Claude Code** - AI yang bisa menulis kode
- **Cursor** - Editor kode dengan AI built-in
- **GitHub Copilot** - Asisten coding dari GitHub

Filament menyediakan panduan khusus agar AI-AI ini bisa **menulis kode Filament dengan benar**.

### Analoginya:

Bayangkan AI seperti **asisten baru** yang mau belajar. Dengan "panduan" dari Filament, asisten ini jadi tahu cara menulis kode Filament yang tepat.

---

## 📦 Laravel Boost

**Laravel Boost** adalah alat yang mengajarkan AI cara menulis kode Laravel dan Filament dengan benar.

### Cara Install Laravel Boost

```bash
# 1. Install Boost
composer require laravel/boost --dev

# 2. Jalankan installer
php artisan boost:install
```

Saat menjalankan installer, pilih **Filament** ketika diminta.

### Apa yang Terjadi?

Boost akan membuat file seperti:

- `AGENTS.md`
- `CLAUDE.md`

File-file ini berisi "instruksi" untuk AI agar tahu cara menulis kode Filament.

---

## 🔷 Filament Blueprint (Premium)

**Filament Blueprint** adalah alat berbayar yang membantu AI membuat **rencana implementasi** yang detail sebelum menulis kode.

### Kenapa Ini Penting?

Bayangkan kamu mau membangun rumah:

- **Tanpa blueprint:** Langsung bangun, hasilnya mungkin berantakan
- **Dengan blueprint:** Ada gambar rencana dulu, hasilnya lebih rapi

Sama dengan koding - AI yang punya rencana detail akan menghasilkan kode yang lebih baik!

### Apa yang Dihasilkan Blueprint?

Blueprint akan membuat dokumen detail yang berisi:

- **Models:** Atribut, relasi, dan enum
- **Resources:** Namespace dan konfigurasi
- **Forms:** Komponen field dan validasi
- **Tables:** Kolom, filter, dan aksi
- **Authorization:** Aturan hak akses
- **Testing:** Apa yang perlu diuji

### Cara Install Blueprint

```bash
# 1. Konfigurasi repository
composer config repositories.filament composer https://packages.filamentphp.com/composer

# 2. Masukkan kredensial
composer config --auth http-basic.packages.filamentphp.com "EMAIL_KAMU" "LICENSE_KEY_KAMU"

# 3. Install Blueprint
composer require filament/blueprint --dev

# 4. Jalankan installer
php artisan boost:install
```

Pilih **Filament Blueprint** saat diminta.

### Contoh Penggunaan

Kamu bisa meminta AI seperti ini:

```
Create a Filament Blueprint for an order management system.
Orders belong to customers and have many order items.
Each order has a status (pending, confirmed, shipped, delivered, cancelled),
shipping address, and optional notes.
```

Terjemahannya:

> "Buatkan Filament Blueprint untuk sistem manajemen pesanan.
> Pesanan milik pelanggan dan punya banyak item.
> Setiap pesanan punya status (pending, confirmed, shipped, delivered, cancelled),
> alamat pengiriman, dan catatan opsional."

AI akan membuat dokumen rencana yang sangat detail!

---

## 📊 Perbandingan: Tanpa vs Dengan Blueprint

| Aspek           | Tanpa Blueprint | Dengan Blueprint |
| --------------- | --------------- | ---------------- |
| Detail rencana  | Umum/kabur      | Sangat spesifik  |
| Namespace       | Mungkin salah   | Pasti benar      |
| Struktur kode   | Bisa berantakan | Terorganisir     |
| Waktu debugging | Lebih lama      | Lebih singkat    |

---

## 💡 Kapan Pakai AI untuk Filament?

### Bagus untuk:

✅ Membuat resource baru dengan cepat
✅ Generate form dan tabel standar
✅ Menambah fitur yang umum
✅ Belajar cara pakai Filament

### Hati-hati untuk:

⚠️ Fitur yang sangat custom
⚠️ Logika bisnis yang kompleks
⚠️ Kode yang butuh keamanan tinggi

---

## 🆓 Gratis vs Berbayar

| Fitur                        | Gratis | Berbayar     |
| ---------------------------- | ------ | ------------ |
| Laravel Boost                | ✅     | -            |
| AI Guidelines untuk Filament | ✅     | -            |
| Filament Blueprint           | -      | ✅ (Premium) |

**Tips:** Untuk pemula, Laravel Boost yang gratis sudah cukup!

---

## 🔧 Tools AI yang Bisa Dipakai

1. **Claude Code** - AI dari Anthropic
2. **Cursor** - Editor VS Code dengan AI
3. **GitHub Copilot** - Dari GitHub/Microsoft
4. **ChatGPT** - Dari OpenAI (bisa copy-paste kode)

Semuanya bisa bekerja lebih baik dengan bantuan Laravel Boost!

---

## 💡 Ringkasan

1. **Laravel Boost** = Alat gratis yang mengajarkan AI cara menulis kode Filament
2. **Filament Blueprint** = Alat berbayar untuk membuat rencana detail
3. AI bisa membantu, tapi tetap perlu **review** dari manusia
4. Untuk pemula, mulai dengan Laravel Boost yang gratis

---

## 🎯 Latihan Mandiri

1. Jika kamu punya akses ke AI coding assistant, coba install Laravel Boost
2. Minta AI untuk membuat resource sederhana tanpa dan dengan Boost
3. Bandingkan kualitas kodenya

<details>
<summary>Tidak Punya AI Assistant?</summary>

Tidak apa-apa! Kamu tetap bisa belajar Filament secara manual dengan membaca dokumentasi. AI hanya mempercepat proses, bukan keharusan.

</details>
