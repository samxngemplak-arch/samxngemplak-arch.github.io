# SIMBAH — Audit & Next Step

> Diperbarui: 26 Juni 2026 — setelah sesi internal linking + sitemap audit
> Cara pakai: kerjakan dari atas ke bawah. Coret kalau sudah deploy & dicek live.

---

## ✅ SUDAH SELESAI

- [x] Domain canonical → `simbahngemplak.vercel.app` (OG, Twitter, Schema, sitemap, robots)
- [x] Sitemap — URL `?page=...` dihapus, 19 URL UMKM individual `?umkm=slug` ditambahkan
- [x] Sitemap slug — dicek ulang, semua 19 slug 100% match dengan output `slugify()` di `script.js`
- [x] Heading semantik — `<div>` judul → `<h1>`/`<h2>`/`<h3>`
- [x] `preconnect` Google Fonts, `aria-label` tombol ikon, `loading="lazy/eager"` logo
- [x] SEO per-UMKM — title, desc, OG, Twitter, canonical, Schema `LocalBusiness` dinamis per UMKM
- [x] Schema `GovernmentOrganization` statis di `<head>` untuk profil dusun
- [x] Shuffle berbobot Beranda — semua kategori terwakili, tidak lagi 8 bibit pertama terus
- [x] Jam operasional — ganti "Buka 24 jam" → "Hubungi untuk jam buka" (kecuali yang ada jam asli)
- [x] Plandemic Space jam — diperbarui ke "Setiap hari, hubungi WA untuk ketersediaan"
- [x] Deskripsi 19 UMKM — ditulis ulang per karakter usaha, tidak lagi template generik
- [x] Filter chip `data-filter` — tidak lagi bergantung pada teks tombol
- [x] Data dari katalog PDF, v2, v3, Excel — produk spesifik, koreksi karakter & kategori per UMKM
- [x] Rahman Grosir Bibit masuk `id=3`, sitemap diupdate, slug bersih
- [x] Samuji & PRIMATANI — produk dilengkapi dari 1 → 4 item
- [x] FAQ per UMKM — field `faq` di `umkm.json`, render accordion di halaman detail, Schema `FAQPage`
- [x] `seoTitle` & `seoDesc` per UMKM — `updateMetaUMKM()` pakai field khusus, fallback ke format lama
- [x] Area layanan per UMKM — field `area` di `umkm.json`, tampil di info operasional, Schema `areaServed` spesifik per UMKM
- [x] Isron Furniture — deskripsi diperbaiki (sebelumnya < 200 karakter)
- [x] Meta `google-site-verification` dijaga — tidak boleh hilang saat update `index.html`
- [x] Disclaimer Agenda — label "contoh ilustrasi" tampil di Beranda & halaman Agenda penuh
- [x] Disclaimer Kas — label "ilustrasi sementara" tampil di Beranda & halaman Kas penuh
- [x] Internal linking "Usaha Terkait" — field `terkait` (array of id) ditambah ke semua 19 UMKM di `umkm.json`, render card horizontal scroll di halaman detail (`script.js` + `index.html`), section otomatis sembunyi kalau kosong

---

## 🔴 KERJAKAN BERIKUTNYA

Tidak ada bug aktif saat ini. Semua item sebelumnya sudah selesai.

---

## 🟡 MENUNGGU DATA LAPANGAN (tugas Zen)

- [ ] **Foto asli** UMKM & dusun — sedang disiapkan *(begitu siap, ganti path di field `galeri` & `cover` di `umkm.json`, render otomatis sebagai `<img>` — lihat catatan di `script.js` bagian render galeri)*
- [ ] **Nomor kontak** Nyuwun Tulung (Kades, RW, RT, Bidan, Babinsa) — cara aktifkan: isi `href` di `index.html` dengan nomor asli, hapus atribut `data-kontak-publik`
- [ ] **Nama pengurus** organisasi (BPD, Takmir, PKK, Posyandu, Karang Taruna) — cara isi: Ctrl+F nama jabatan di `index.html`, ganti `—` dengan nama asli
- [ ] **Jam buka asli** tiap UMKM — update field `jam` per UMKM di `umkm.json`
- [ ] **Luas wilayah** & KK/penduduk terverifikasi — update di `index.html` section Data Wilayah

---

## 🔵 WISHLIST — Nanti setelah yang di atas beres

- **Halaman Sentra Bibit** — identitas terkuat Ngemplak, butuh halaman terpisah (keluar dari SPA)
- **Halaman kategori** (`/kategori/bibit-buah`, dst) — butuh arsitektur multi-halaman
- **Schema `WebSite` + `BreadcrumbList`** di homepage
- **Google Search Console** — submit sitemap, pantau keyword (tugas Zen, bukan coding)
- **Domain `.id`** — keputusan Zen & perangkat dusun
- **Backlink lokal** — dari website Desa Samping, Kec. Kemiri, Kab. Purworejo

---

## 📌 URUTAN KERJA BERIKUTNYA

```
--- menunggu data dari Zen ---
1 → Foto UMKM tiba → update field galeri & cover di umkm.json
                   → ganti render emoji ke <img> di script.js
2 → Nomor kontak tiba → aktifkan tombol Nyuwun Tulung di index.html
3 → Nama pengurus tiba → isi tanda — di index.html tab Pengurus
```
