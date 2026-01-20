# I. Apa itu Filament? 🎯

> **Sumber:** [https://filamentphp.com/docs/5.x/introduction/overview](https://filamentphp.com/docs/5.x/introduction/overview)

---

## 🤔 Penjelasan Sederhana

Bayangkan kamu ingin membuat **halaman admin** untuk website-mu (tempat untuk mengelola data seperti daftar produk, pengguna, pesanan, dll). Biasanya, ini membutuhkan banyak waktu karena kamu harus membuat form, tabel, tombol, dan banyak lagi.

**Filament** adalah alat yang membantu kamu membuat halaman admin dengan **sangat cepat** menggunakan PHP saja! Tidak perlu menulis banyak kode JavaScript atau CSS yang rumit.

### Analoginya:

Bayangkan Filament seperti **LEGO**. Kamu tinggal pilih blok-blok yang sudah jadi (form, tabel, tombol), lalu susun sesuai kebutuhanmu. Tidak perlu membuat setiap blok dari nol!

---

## 📦 Apa Saja yang Ada di Filament?

Filament terdiri dari beberapa **paket** (seperti kotak peralatan berbeda):

### 1. `filament/filament` - Paket Utama Panel Builder

Ini adalah paket utama untuk membuat panel admin. Kalau kamu install ini, semua paket lainnya akan ikut ter-install.

**Contoh penggunaan:** Membuat halaman admin lengkap dengan sidebar, menu, dan dashboard.

### 2. `filament/tables` - Pembuat Tabel

Untuk menampilkan data dalam bentuk tabel yang interaktif (bisa di-filter, diurutkan, dan ada paginasi).

**Contoh penggunaan:** Menampilkan daftar semua pengguna dengan kolom nama, email, tanggal daftar.

### 3. `filament/forms` - Pembuat Form

Untuk membuat berbagai macam input form (text, dropdown, checkbox, file upload, dll).

**Contoh penggunaan:** Form untuk menambah produk baru dengan nama, harga, dan gambar.

### 4. `filament/infolists` - Penampil Informasi

Untuk menampilkan detail data dalam format yang rapi (seperti halaman profil).

**Contoh penggunaan:** Halaman detail pesanan yang menampilkan informasi pembeli, alamat, dan produk yang dibeli.

### 5. `filament/actions` - Tombol & Modal

Untuk membuat tombol dengan aksi tertentu, termasuk popup konfirmasi.

**Contoh penggunaan:** Tombol "Hapus" dengan popup konfirmasi "Yakin ingin menghapus?"

### 6. `filament/notifications` - Notifikasi

Untuk menampilkan pesan notifikasi ke pengguna.

**Contoh penggunaan:** Muncul pesan "Data berhasil disimpan!" setelah submit form.

### 7. `filament/widgets` - Widget Dashboard

Untuk membuat widget statistik di dashboard.

**Contoh penggunaan:** Kotak yang menampilkan "Total Penjualan Hari Ini: Rp 5.000.000"

---

## 🔌 Plugins (Tambahan)

Selain paket bawaan, ada juga **plugins** buatan komunitas yang bisa kamu install untuk menambah fitur. Beberapa gratis, beberapa berbayar.

Kamu bisa lihat daftar plugins di: [https://filamentphp.com/plugins](https://filamentphp.com/plugins)

---

## 🎨 Mengubah Tampilan

Filament menggunakan **Tailwind CSS** untuk styling. Kamu bisa mengubah tampilan (warna, ukuran, dll) dengan mudah.

**Contoh sederhana:** Mengubah sudut tombol dari bulat menjadi lebih kotak:

```css
/* Sebelumnya (sudut bulat) */
.fi-btn {
  @apply rounded-lg;
}

/* Diubah menjadi (sudut sedikit bulat) */
.fi-btn {
  @apply rounded-sm;
}
```

---

## 🧪 Testing

Filament punya tools untuk membantu kamu membuat **test** (pengujian) untuk aplikasimu. Ini penting untuk memastikan semuanya berjalan dengan benar.

---

## ❓ Kalau Filament Bukan yang Tepat Untukmu?

Tidak apa-apa! Ada alternatif lain:

| Situasi                       | Alternatif yang Disarankan                              |
| ----------------------------- | ------------------------------------------------------- |
| Filament terasa terlalu rumit | [Laravel Nova](https://nova.laravel.com)                |
| Tidak mau pakai Livewire      | [Laravel Nova](https://nova.laravel.com) (pakai Vue.js) |
| Butuh CMS yang langsung jadi  | [Statamic](https://statamic.com)                        |
| Mau tulis Blade views sendiri | [Flux](https://fluxui.dev)                              |

---

## 💡 Poin Penting untuk Diingat

1. **Filament = Alat untuk membuat panel admin dengan cepat**
2. **Dibangun di atas:** Laravel + Livewire + Alpine.js + Tailwind CSS
3. **Keuntungan:** Tidak perlu menulis JavaScript, cukup PHP saja
4. **Bisa dipakai untuk:** Admin panel, dashboard, CRM, portal pengguna, dll

---

## 🎯 Latihan Mandiri

Coba jawab pertanyaan ini:

1. Paket apa yang dipakai untuk membuat tabel data?
2. Paket apa yang dipakai untuk menampilkan notifikasi?
3. Apa keuntungan menggunakan Filament dibanding membuat admin panel dari nol?

<details>
<summary>Lihat Jawaban</summary>

1. `filament/tables`
2. `filament/notifications`
3. Lebih cepat, tidak perlu menulis JavaScript, komponen sudah siap pakai

</details>
