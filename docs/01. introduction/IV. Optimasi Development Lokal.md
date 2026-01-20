# IV. Optimasi Development Lokal 🚀

> **Sumber:** [https://filamentphp.com/docs/5.x/introduction/optimizing-local-development](https://filamentphp.com/docs/5.x/introduction/optimizing-local-development)

---

## 🤔 Apa Maksudnya?

Saat kamu membuka halaman web, ada banyak proses yang terjadi di komputer. Jika proses-proses ini lambat, halaman web juga jadi lambat dibuka.

Bagian ini berisi **tips untuk mempercepat** aplikasi Filament saat berjalan di komputermu (development lokal).

### Analoginya:

Bayangkan komputermu seperti **dapur**. Jika peralatan dapur berantakan atau tidak efisien, masak jadi lama. Tips-tips ini seperti **merapikan dapur** agar masak lebih cepat!

---

## 1️⃣ Aktifkan OPcache

### Apa itu OPcache?

OPcache adalah fitur PHP yang **menyimpan hasil kompilasi kode**. Bayangkan seperti ini:

- **Tanpa OPcache:** Setiap kali halaman dibuka, PHP harus "membaca ulang" semua file
- **Dengan OPcache:** PHP "mengingat" file yang sudah dibaca, jadi lebih cepat

### Cara Cek OPcache Aktif

Buka terminal dan jalankan:

```bash
php -r "echo 'opcache.enable => ' . ini_get('opcache.enable') . PHP_EOL;"
```

Jika muncul `opcache.enable => 1`, artinya sudah aktif! ✅

Jika muncul `0` atau kosong, perlu diaktifkan.

### Cara Mengaktifkan OPcache

1. **Cari file php.ini:**

   ```bash
   php --ini
   ```

2. **Buka file php.ini dan tambahkan:**

   ```ini
   opcache.enable=1
   ```

3. **Restart web server**

### Pengaturan Tambahan (Opsional)

Jika aplikasimu besar, tambahkan juga:

```ini
opcache.memory_consumption=128      ; Memori untuk cache (MB)
opcache.max_accelerated_files=10000 ; Maksimum file yang di-cache
```

---

## 2️⃣ Kecualikan Folder Proyek dari Antivirus

### Kenapa Ini Penting?

Antivirus seperti **Microsoft Defender** memeriksa setiap file yang diakses. Karena PHP membaca banyak file setiap request, ini bisa memperlambat!

### Cara Melakukannya (Windows)

1. Buka **Windows Security**
2. Pilih **Virus & threat protection**
3. Klik **Manage settings**
4. Scroll ke **Exclusions**, klik **Add or remove exclusions**
5. Tambahkan folder proyekmu (contoh: `C:\xampp\htdocs\my-project`)

> ⚠️ **Peringatan:** Hanya lakukan ini jika kamu yakin proyekmu aman!

---

## 3️⃣ Matikan Tools Debugging yang Tidak Terpakai

Tools debugging berguna untuk mencari bug, tapi bisa memperlambat jika tidak terpakai.

### A. Matikan View Debugging di Laravel Herd

Jika kamu pakai Laravel Herd:

1. Buka **Herd > Dumps**
2. Klik **Settings**
3. Hapus centang pada **"Views"**

### B. Matikan Laravel Debugbar

Jika kamu install [Laravel Debugbar](https://github.com/barryvdh/laravel-debugbar):

Edit file `.env`:

```env
DEBUGBAR_ENABLED=false
```

### C. Matikan Xdebug

Xdebug sangat memperlambat PHP jika aktif tapi tidak dipakai.

**Cara cek Xdebug aktif:**

```bash
php -v
```

Jika ada tulisan "with Xdebug", berarti aktif.

**Cara matikan:**

1. Cari file php.ini: `php --ini`
2. Tambahkan atau ubah:
   ```ini
   xdebug.mode=off
   ```
3. Restart web server

---

## 4️⃣ Cache Blade Icons

Filament menggunakan banyak ikon. Caching ikon bisa mempercepat rendering.

**Jalankan perintah ini:**

```bash
php artisan icons:cache
```

> **Catatan:** Jalankan lagi perintah ini setelah install paket ikon baru!

---

## 📊 Ringkasan Tips Optimasi

| Tips                             | Dampak     | Kesulitan       |
| -------------------------------- | ---------- | --------------- |
| Aktifkan OPcache                 | ⭐⭐⭐⭐⭐ | 🔧 Mudah        |
| Kecualikan folder dari antivirus | ⭐⭐⭐⭐   | 🔧 Mudah        |
| Matikan Debugbar                 | ⭐⭐⭐     | 🔧 Sangat Mudah |
| Matikan Xdebug                   | ⭐⭐⭐⭐⭐ | 🔧 Mudah        |
| Cache Blade Icons                | ⭐⭐       | 🔧 Sangat Mudah |

---

## 🔍 Cara Cek Apakah Sudah Lebih Cepat

1. **Sebelum optimasi:** Perhatikan berapa lama halaman admin terbuka
2. **Setelah optimasi:** Bandingkan waktunya

Kamu juga bisa pakai **Developer Tools** di browser:

1. Tekan `F12`
2. Buka tab **Network**
3. Refresh halaman
4. Lihat waktu di bawah (contoh: "Finish: 2.5s")

---

## ⚠️ Catatan Penting

Tips-tips ini untuk **development lokal** saja. Untuk optimasi **production** (server online), ada tips berbeda yang bisa dilihat di [deployment documentation](https://filamentphp.com/docs/5.x/deployment).

---

## 💡 Checklist Optimasi

- [ ] OPcache aktif
- [ ] Folder proyek dikecualikan dari antivirus (Windows)
- [ ] Debugbar dimatikan (jika tidak terpakai)
- [ ] Xdebug dimatikan (jika tidak sedang debugging)
- [ ] Blade icons di-cache

---

## 🎯 Latihan Mandiri

1. Cek apakah OPcache sudah aktif di komputermu
2. Jika pakai Windows, cek pengaturan Windows Defender
3. Cek apakah ada Xdebug yang aktif
4. Jalankan `php artisan icons:cache`

<details>
<summary>Tidak Tahu Cara Restart Web Server?</summary>

**Untuk XAMPP:**

- Buka XAMPP Control Panel
- Klik Stop pada Apache
- Klik Start lagi

**Untuk Laravel Herd:**

- Klik ikon Herd di menubar
- Pilih Stop PHP lalu Start lagi

**Untuk ServBay:**

- Buka ServBay.app
- Restart PHP service

</details>
