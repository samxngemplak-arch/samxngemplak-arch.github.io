# SIMBAH — Audit & Next Step

> Diperbarui: 25 Juni 2026 — audit total setelah baca semua dokumen (katalog v2, v3, profil sentra, panduan SEO, Excel data UMKM)
> Cara pakai: kerjakan dari atas ke bawah. Coret kalau sudah deploy & dicek live.

---

## ✅ SUDAH SELESAI

- [x] Domain canonical → `simbahngemplak.vercel.app` (OG, Twitter, Schema, sitemap, robots)
- [x] Sitemap — URL `?page=...` dihapus, 19 URL UMKM individual `?umkm=slug` ditambahkan
- [x] Heading semantik — `<div>` judul → `<h1>`/`<h2>`/`<h3>`
- [x] `preconnect` Google Fonts, `aria-label` tombol ikon, `loading="lazy/eager"` logo
- [x] SEO per-UMKM — title, desc, OG, Twitter, canonical, Schema `LocalBusiness` dinamis per UMKM
- [x] Schema `GovernmentOrganization` statis di `<head>` untuk profil dusun
- [x] Shuffle berbobot Beranda — semua kategori terwakili, tidak lagi 8 bibit pertama terus
- [x] Jam operasional — ganti "Buka 24 jam" → "Hubungi untuk jam buka" (kecuali yang memang ada jam asli)
- [x] Deskripsi 19 UMKM — ditulis ulang per karakter usaha, tidak lagi template generik
- [x] Filter chip `data-filter` — tidak lagi bergantung pada teks tombol
- [x] Data dari katalog PDF, v2, v3, Excel — produk spesifik, koreksi karakter & kategori per UMKM
- [x] Rahman Grosir Bibit masuk `id=3`, sitemap diupdate, slug bersih
- [x] Samuji & PRIMATANI — produk dilengkapi dari 1 → 4 item

---

## 🔴 KERJAKAN SEKARANG (kode, tidak butuh data lapangan)

### 1. FAQ per UMKM — belum ada sama sekali
**Kenapa penting:** Panduan SEO v3 menyebut ini wajib. FAQ sering muncul di Google sebagai rich snippet. Schema `FAQPage` juga baru bisa dipasang kalau FAQ-nya ada.
**Data:** Sudah tersedia di katalog v3 — 3-5 FAQ per UMKM, tinggal dipindahkan ke `umkm.json` (tambah field `faq`) dan dirender di halaman detail UMKM.
**File:** `umkm.json` + `script.js` (render FAQ) + `style.css` (styling FAQ)

### 2. Schema FAQPage per UMKM
**Kenapa penting:** Nyambung langsung dengan #1. Begitu FAQ ada di data, schema `FAQPage` ditambahkan ke `updateMetaUMKM()` di `script.js` — Google bisa tampilkan FAQ langsung di hasil pencarian.
**File:** `script.js`, fungsi `updateMetaUMKM()`

### 3. Field `tagline` & `seoDesc` per UMKM
**Kenapa penting:** Sekarang `updateMetaUMKM()` pakai `u.desc` yang dipotong 155 karakter untuk meta description. Masalahnya `desc` ditulis untuk dibaca pengunjung (panjang, naratif), bukan untuk meta description Google (ringkas, keyword-rich). Katalog v3 sudah menyediakan meta description khusus per UMKM yang berbeda dari `desc`.
**Solusi:** Tambah field `seoDesc` di `umkm.json`, dipakai khusus untuk meta description. Kalau kosong, fallback ke `desc` yang dipotong seperti sekarang.
**File:** `umkm.json` + `script.js`

### 4. Field `area` (area layanan) per UMKM
**Kenapa penting:** Katalog v3 mencatat area layanan per UMKM (Purworejo, Kebumen, Magelang, dst). Ini bisa masuk Schema `areaServed` yang sekarang masih generik `"Desa Samping, Kemiri, Purworejo"` untuk semua UMKM.
**File:** `umkm.json` + `script.js` (Schema `areaServed`)

### 5. Internal linking "UMKM Terkait"
**Kenapa penting:** Katalog v3 sudah menyusun rekomendasi "UMKM Terkait" per usaha (3 UMKM per halaman). Ini memperkuat SEO internal dan UX — pengunjung yang lihat Heri Bibit langsung bisa lompat ke Khanza Bibit atau Trijaya Bibit.
**Data:** Sudah ada di katalog v3 per UMKM.
**File:** `umkm.json` (tambah field `terkait`) + `script.js` (render section) + `style.css`

### 6. Meta title per UMKM lebih spesifik
**Sekarang:** `u.name + ' — ' + u.cat + ' di Dusun Ngemplak | SIMBAH'`
**Contoh hasil:** `Heri Bibit — Perkebunan di Dusun Ngemplak | SIMBAH`
**Masalah:** Kata "Perkebunan" terlalu generik — tidak ada keyword spesifik. Katalog v3 sudah menyiapkan SEO Title yang jauh lebih kuat per UMKM, contoh: `Heri Bibit | Bibit Variegata dan Tanaman Koleksi Purworejo`
**Solusi:** Tambah field `seoTitle` di `umkm.json`. Kalau ada, dipakai. Kalau kosong, fallback ke format lama.
**File:** `umkm.json` + `script.js`

### 7. Isron Furniture — deskripsi terlalu pendek
**Sekarang:** `desc` Isron hanya 119 karakter — satu-satunya yang tidak lolos cek >200 karakter.
**File:** `umkm.json`

---

## 🟡 MENUNGGU DATA LAPANGAN (tugas Zen)

- [ ] **Foto asli** UMKM & dusun — sedang disiapkan *(paling berdampak ke SEO menurut panduan v3)*
- [ ] **Nomor kontak** Nyuwun Tulung (Kades, RW, RT, Bidan, Babinsa)
- [ ] **Nama pengurus** organisasi (BPD, Takmir, PKK, Posyandu, Karang Taruna)
- [ ] **Jam buka asli** tiap UMKM — sementara "Hubungi untuk jam buka"
- [ ] **Luas wilayah** & KK/penduduk terverifikasi

---

## 🔵 WISHLIST — Bisa dikerjakan nanti, bukan sekarang

Item-item ini valid secara SEO (dari panduan v3) tapi keluar dari prinsip SIMBAH (vanilla JS, 1 halaman, tanpa backend) atau butuh keputusan lebih dulu:

- **Halaman kategori** (`/kategori/bibit-buah`, `/kategori/penghijauan`, dst) — panduan v3 bilang ini bisa naikan traffic 3-5x, tapi butuh arsitektur multi-halaman atau perombakan navigasi besar
- **Halaman Sentra Bibit** — identitas terkuat Ngemplak menurut panduan v2, butuh halaman terpisah
- **Schema `WebSite` + `BreadcrumbList`** di homepage — minor tapi dicatat
- **Google Search Console** — daftarkan sitemap, pantau keyword. Ini tugas Zen, bukan coding
- **Domain `.id`** — panduan v2 bilang ini pembeda antara 9.5/10 dan 10/10. Keputusan Zen & perangkat dusun
- **Backlink lokal** — dari website Desa Samping, Kec. Kemiri, Kab. Purworejo. Bukan tugas coding

---

## 📌 URUTAN KERJAKAN SEKARANG

```
1 → FAQ per UMKM (data sudah siap di katalog v3)
2 → Schema FAQPage (nyambung langsung dengan #1)
3 → seoTitle & seoDesc per UMKM (data sudah siap di katalog v3)
4 → Area layanan per UMKM (data sudah siap di katalog v3)
5 → Internal linking UMKM Terkait (data sudah siap di katalog v3)
6 → Fix deskripsi Isron Furniture
--- setelah foto dari Zen tiba ---
7 → Ganti emoji galeri → <img> asli + loading="lazy"
--- setelah nomor kontak dari Zen ---
8 → Aktifkan tombol Nyuwun Tulung
```
