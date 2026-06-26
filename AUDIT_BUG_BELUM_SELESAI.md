# SIMBAH — Audit & Next Step

> Diperbarui: 26 Juni 2026 — grid produk 2 kolom diselesaikan (sebelumnya tercatat selesai tapi kode masih scroll horizontal, sudah diperbaiki & dicek ulang ke CSS aktual)
> Cara pakai: kerjakan dari atas ke bawah. Coret kalau sudah deploy & dicek live.

---

## ✅ SUDAH SELESAI

- [x] Domain canonical → `simbahngemplak.vercel.app` (OG, Twitter, Schema, sitemap, robots)
- [x] Sitemap — 19 URL UMKM individual `?umkm=slug`, lastmod 2026-06-26, semua slug match `slugify()`
- [x] Heading semantik, preconnect, aria-label, loading lazy/eager
- [x] SEO per-UMKM — title, desc, OG, Twitter, canonical, Schema `LocalBusiness` + `FAQPage` dinamis
- [x] Schema `GovernmentOrganization` + `WebSite` statis di `<head>`
- [x] Schema `LocalBusiness` field `image` — path diperbaiki ke `img/branding/logo.png`
- [x] Shuffle berbobot Beranda — semua kategori terwakili
- [x] Jam operasional — "Buka 24 jam" → "Hubungi untuk jam buka" / Plandemic → "Setiap hari, hubungi WA"
- [x] Deskripsi 19 UMKM — ditulis ulang per karakter usaha
- [x] Filter chip `data-filter`
- [x] Data dari katalog v2, v3, Excel — produk spesifik, koreksi karakter & kategori
- [x] Rahman Grosir Bibit masuk `id=3`
- [x] Samuji & PRIMATANI — produk dilengkapi
- [x] FAQ per UMKM — field `faq`, render accordion, Schema `FAQPage`. Semua 19 UMKM sudah ditulis ulang, tidak ada lagi jawaban "Ya." generik
- [x] seoTitle & seoDesc per UMKM — `updateMetaUMKM()`, semua dalam batas karakter Google (title ≤70, desc ≤160)
- [x] Area layanan per UMKM — field `area`, tampil di info operasional, Schema `areaServed`
- [x] Isron Furniture — deskripsi diperbaiki
- [x] Disclaimer Agenda & Kas — tampil di Beranda & halaman masing-masing
- [x] Foto UMKM — 19/19 sudah `cover.webp` + gallery (3–4 foto), path `img/umkm/...`
- [x] Internal linking Usaha Terkait — field `terkait` semua 19 UMKM, render list vertikal compact (`terkait-list`, `terkait-item`)
- [x] Hapus section Testimoni Warga — dari `index.html`, `script.js`, CSS `.rv*`
- [x] Card Produk & Jasa — field `k` (keterangan) ditambah semua produk, label "Hubungi WA" per produk dihapus
- [x] Produk grid 2 kolom — render `script.js` (sudah benar dari awal) + styling `.prow`/`.pcard` di `style.css` diganti dari scroll horizontal jadi grid 2 kolom (badge emoji 32px + nama + keterangan, tanpa kotak besar/box-shadow)
- [x] Nomor kontak Pemerintahan Desa — format `08xx-xxxx-xxxx` diganti "Nomor belum tersedia"
- [x] Komentar galeri foto di `script.js` diperbarui — bukan lagi "emoji placeholder"
- [x] Orphan code Testimoni dihapus dari `script.js`
- [x] `README.md` — struktur folder, status foto, jumlah UMKM diperbarui akurat

---

## 🔴 KERJAKAN BERIKUTNYA

### 1. Tagline per UMKM
**Masalah:** above the fold langsung ke deskripsi panjang — tidak ada hook singkat yang menjawab "ini usaha apa" dalam 1 kalimat.
**Data:** sudah ada di `Katalog_UMKM_Dusun_Ngemplak_FINAL.docx` field "Tagline" per UMKM.
**Yang perlu dikerjakan:**
- Tambah field `tagline` ke semua 19 UMKM di `umkm.json`
- Render 1 baris di bawah nama usaha di halaman detail (`script.js` + sedikit CSS)
- File: `umkm.json`, `script.js`, `style.css`

### 2. Teks tombol Maps
**Masalah:** pengunjung tidak tahu bisa cari review di Google Maps — Google tidak izinkan deep link langsung ke tab Review.
**Fix sederhana:** ubah teks tombol dari "Buka Maps" → "Lihat Maps & Ulasan"
- File: `index.html` (1 kata)

---

## 🟡 MENUNGGU DATA LAPANGAN (tugas Zen)

- [ ] **Nomor kontak** Nyuwun Tulung (Kades, RW, RT, Bidan, Babinsa) — cara aktifkan: isi `href` di `index.html`, hapus atribut `data-kontak-publik`
- [ ] **Nama pengurus** organisasi (BPD, Takmir, PKK, Posyandu, Karang Taruna) — Ctrl+F nama jabatan di `index.html`, ganti `—` dengan nama asli
- [ ] **Jam buka asli** tiap UMKM — update field `jam` per UMKM di `umkm.json` (14 UMKM masih "Hubungi untuk jam buka")
- [ ] **Luas wilayah** & KK/penduduk terverifikasi — update di `index.html` section Data Wilayah
- [ ] **Foto hero beranda** — ganti `img/backgrounds/hero-bg.webp` dengan foto asli Ngemplak

---

## 🔵 GOOGLE SEARCH CONSOLE — sudah disubmit, masih nunggu

- [x] Sitemap sudah disubmit ke GSC
- [ ] **Belum terindeks** — normal untuk domain baru (4 hari–4 minggu). Tidak ada tindakan coding diperlukan.
  - Kalau belum ada setelah ~4 minggu: buka URL Inspection Tool → Request Indexing (sekali saja)
  - Kalau setelah 4 minggu masih nol: cek robots.txt dan noindex

---

## 🔵 WISHLIST — Nanti

- **Halaman Sentra Bibit** — butuh halaman terpisah, keluar dari SPA, butuh diskusi arsitektur dulu
- **Schema `BreadcrumbList`** di homepage
- **Domain `.id`** — keputusan Zen & perangkat dusun
- **Backlink lokal** — dari website Desa Samping, Kec. Kemiri, Kab. Purworejo

---

## 📌 URUTAN KERJA BERIKUTNYA

```
1 → Tagline 19 UMKM   (umkm.json + script.js + style.css)
2 → Teks tombol Maps  (index.html — 1 kata, 5 menit)

--- menunggu data dari Zen ---
3 → Nomor kontak → aktifkan tombol Nyuwun Tulung
4 → Nama pengurus → isi tanda — di tab Pengurus
5 → Foto hero beranda → replace hero-bg.webp

--- pasif, tidak ada coding ---
6 → Pantau GSC Page Indexing report
```
