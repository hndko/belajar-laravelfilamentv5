# VII. Berkontribusi ke Filament 🤝

> **Sumber:** [https://filamentphp.com/docs/5.x/introduction/contributing](https://filamentphp.com/docs/5.x/introduction/contributing)

---

## 🤔 Apa itu Berkontribusi?

Filament adalah proyek **open source** - artinya siapa saja bisa membantu mengembangkannya! Berkontribusi bisa bermacam-macam:

- Melaporkan bug
- Memperbaiki bug
- Menambah fitur baru
- Membuat plugin
- Membantu terjemahan

### Analoginya:

Bayangkan Filament seperti **taman komunitas**. Semua orang boleh datang dan membantu menanam bunga, mencabut rumput liar, atau menambah bangku baru!

---

## 1️⃣ Melaporkan Bug 🐛

Langkah paling sederhana untuk berkontribusi!

### Cara Mudah:

Jalankan perintah ini di proyek Laravel-mu:

```bash
php artisan make:filament-issue
```

Ini akan membuka browser dengan form issue yang sudah terisi versi PHP, Laravel, dan Filament-mu!

### Cara Manual:

1. Buka [GitHub Issues](https://github.com/filamentphp/filament/issues/new/choose)
2. Pilih template yang sesuai
3. Isi informasi yang diminta

### ⚠️ Wajib: Repository Reproduksi

Setiap laporan bug **harus** menyertakan repository reproduksi.

**Apa itu?**
Proyek Laravel baru yang sederhana, hanya berisi kode yang menunjukkan bug tersebut.

**Template untuk mulai:**
🔗 [https://unitedbycode.com/filament-issue](https://unitedbycode.com/filament-issue)

**Kenapa diperlukan?**

- Memudahkan developer melihat masalahnya
- Mempercepat proses perbaikan
- Issue tanpa reproduksi akan **ditutup otomatis**!

---

## 2️⃣ Mengusulkan Fitur Baru 💡

Punya ide untuk fitur baru?

### Langkah-langkah:

1. Buka [GitHub Discussions](https://github.com/filamentphp/filament/discussions)
2. Pilih kategori **Ideas**
3. Jelaskan fitur yang kamu inginkan
4. Tag **@danharrin** (maintainer Filament) jika kamu mau mengerjakan sendiri

### Tips:

- Jelaskan **masalah** yang ingin dipecahkan
- Jelaskan **solusi** yang kamu usulkan
- Beri **contoh kode** jika memungkinkan

---

## 3️⃣ Membuat Plugin 🔌

Plugin adalah cara bagus untuk berkontribusi tanpa mengubah kode Filament langsung!

### Apa itu Plugin?

Package terpisah yang menambah fitur ke Filament.

### Dokumentasi Plugin:

[https://filamentphp.com/docs/5.x/plugins](https://filamentphp.com/docs/5.x/plugins)

### Butuh Bantuan?

Tanya di channel **#plugin-developers-chat** di Discord

### Submit Plugin:

Jika plugin-mu sudah jadi, submit untuk ditampilkan di website Filament:
[https://github.com/filamentphp/filamentphp.com/blob/main/README.md#contributing](https://github.com/filamentphp/filamentphp.com/blob/main/README.md#contributing)

---

## 4️⃣ Memperbaiki Kode Filament 💻

Untuk developer yang ingin langsung memperbaiki kode Filament:

### Langkah-langkah:

1. **Fork** repository Filament:
   [https://github.com/filamentphp/filament](https://github.com/filamentphp/filament)

2. **Clone** fork-mu ke folder proyek Laravel:

   ```bash
   cd /path/to/laravel-project
   git clone https://github.com/USERNAME-MU/filament.git
   ```

3. **Buat branch** untuk pekerjaanmu:

   ```bash
   cd filament
   git checkout -b fix/nama-perbaikan
   ```

4. **Edit composer.json** proyek Laravel-mu:

   ```json
   {
     "require": {
       "filament/filament": "*"
     },
     "minimum-stability": "dev",
     "repositories": [
       {
         "type": "path",
         "url": "filament/packages/*"
       }
     ]
   }
   ```

5. **Update composer:**

   ```bash
   composer update
   ```

6. **Buat perubahan** dan test

7. **Commit** dan **push** ke GitHub-mu

8. **Buat Pull Request** ke repository Filament

---

## 5️⃣ Membantu Terjemahan 🌍

Filament tersedia dalam banyak bahasa. Kamu bisa membantu menerjemahkan atau memperbaiki terjemahan!

### Cara Cek Terjemahan yang Ketinggalan:

```bash
# Clone repository
git clone [email protected]:filamentphp/filament.git

# Masuk ke folder
cd filament

# Install dependencies
composer install

# Jalankan tool terjemahan
./bin/translation-tool.php
```

Pilih "List outdated translations" dan pilih bahasa yang ingin dicek.

---

## 6️⃣ Melaporkan Celah Keamanan 🔒

Jika kamu menemukan celah keamanan:

### ⛔ JANGAN:

- Post di Discord
- Buat issue publik di GitHub
- Tweet tentang itu

### ✅ LAKUKAN:

Laporkan secara **private** melalui:
[GitHub Security Advisory](https://github.com/filamentphp/filament/security/advisories)

---

## 📜 Code of Conduct

Semua kontributor harus mengikuti aturan perilaku:
[Code of Conduct](https://github.com/filamentphp/filament/blob/5.x/CODE_OF_CONDUCT.md)

### Intinya:

- Hormati semua orang
- Berkomunikasi dengan sopan
- Bantu, jangan menyerang
- Terima kritik dengan baik

---

## 💡 Cara Berkontribusi untuk Pemula

Tidak perlu langsung menulis kode! Mulai dari yang sederhana:

| Level       | Jenis Kontribusi                                 |
| ----------- | ------------------------------------------------ |
| 🌱 Pemula   | Laporkan bug, bantu jawab pertanyaan di Discord  |
| 🌿 Menengah | Buat plugin sederhana, bantu terjemahan          |
| 🌳 Lanjut   | Perbaiki bug, tambah fitur, review PR orang lain |

---

## 📊 Ringkasan Cara Berkontribusi

| Cara             | Link                                                                             |
| ---------------- | -------------------------------------------------------------------------------- |
| Laporkan Bug     | `php artisan make:filament-issue`                                                |
| Usulkan Fitur    | [GitHub Discussions](https://github.com/filamentphp/filament/discussions)        |
| Buat Plugin      | [Plugin Docs](https://filamentphp.com/docs/5.x/plugins)                          |
| Perbaiki Kode    | [Fork & PR](https://github.com/filamentphp/filament)                             |
| Bantu Terjemahan | `./bin/translation-tool.php`                                                     |
| Lapor Keamanan   | [Security Advisory](https://github.com/filamentphp/filament/security/advisories) |

---

## 💡 Manfaat Berkontribusi

1. **Belajar** - Pelajari kode berkualitas dari developer hebat
2. **Networking** - Kenalan dengan developer dari seluruh dunia
3. **Portfolio** - Kontribusimu terlihat di GitHub
4. **Kepuasan** - Membantu ribuan developer lain!

---

## 🎯 Latihan Mandiri

1. **Level 1:** Gabung Discord dan bantu jawab 1 pertanyaan
2. **Level 2:** Coba cari fitur yang kurang → buat discussion di GitHub
3. **Level 3:** Coba fork Filament dan explore kodenya

<details>
<summary>Tidak Berani Berkontribusi Kode?</summary>

Tidak apa-apa! Berkontribusi tidak harus menulis kode:

- Laporkan bug yang kamu temukan
- Bantu jawab pertanyaan di Discord
- Buat tutorial atau video tentang Filament
- Bantu terjemahan ke bahasa Indonesia

Semua kontribusi berharga! 🎉

</details>
