# SIMBAH — Audit & Next Step

> Diperbarui: 26 Juni 2026 — setelah brief produk, FAQ, testimoni, dan rencana redesign visual
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
- [x] Foto UMKM — 19/19 UMKM sudah punya `cover.webp` + gallery (3–4 foto), field `cover` & `galeri` di `umkm.json` sudah pakai path `img/umkm/...`
- [x] Internal linking "Usaha Terkait" — field `terkait` (array of id) ditambah ke semua 19 UMKM, render card horizontal scroll di halaman detail (`script.js` + `index.html`)
- [x] Hapus section Testimoni Warga — `ud-testimoni-sec` dihapus dari `index.html`, render testimoni dihapus dari `showUMKM()` di `script.js`. Field `testimoni` di `umkm.json` dibiarkan ada (tidak mengganggu, tidak dirender)
- [x] Card Produk & Jasa — redesign total. Field `k` (keterangan) ditambahkan ke semua 75 produk di 19 UMKM (highlight keunggulan, bukan harga). Layout diganti dari scroll horizontal card jadi **grid 2 kolom** (badge emoji bulat kecil + nama + keterangan), label "Hubungi WA" per produk **dihapus** (sudah ada CTA WhatsApp besar di atas & bawah section, jadi tidak perlu diulang). Emoji yang sebelumnya duplikat dalam 1 UMKM yang sama (Plandemic Space: Print&Scan vs Servis Printer; Bibit Cabai Alip Sihmanto: Cabai Rawit vs Cabai Keriting) sudah dibedakan supaya tidak membingungkan pelanggan.

---

## 🔴 KERJAKAN BERIKUTNYA

### 1. Tulis ulang FAQ semua 19 UMKM
**Masalah:** 14 dari 19 UMKM punya FAQ dengan jawaban "Ya." saja — tidak berguna untuk pengunjung maupun Google.
**Prinsip:** FAQ yang baik menjawab pertanyaan yang bikin orang *ragu sebelum hubungi* — bukan pertanyaan yang jawabannya sudah obvious dari nama usahanya.
**Contoh yang salah vs benar:**

| ❌ Sekarang | ✅ Seharusnya |
|---|---|
| "Apakah tersedia bibit buah?" → Ya. | "Berapa minimum pembelian bibit?" |
| "Apakah menerima pesanan custom?" → Ya. | "Berapa lama waktu pengerjaan furniture?" |
| "Apakah tersedia kambing dan domba?" → Ya. | "Apakah ternak sudah divaksin?" |

**Yang perlu dikerjakan:**
- Tulis ulang field `faq` di `umkm.json` untuk semua 19 UMKM
- Masing-masing 2–3 pertanyaan yang benar-benar relevan per usaha
- Tidak perlu sentuh `script.js` atau `index.html` — render FAQ sudah benar

---

## 🟡 MENUNGGU DATA LAPANGAN (tugas Zen)

- [ ] **Nomor kontak** Nyuwun Tulung (Kades, RW, RT, Bidan, Babinsa) — cara aktifkan: isi `href` di `index.html` dengan nomor asli, hapus atribut `data-kontak-publik`
- [ ] **Nama pengurus** organisasi (BPD, Takmir, PKK, Posyandu, Karang Taruna) — cara isi: Ctrl+F nama jabatan di `index.html`, ganti `—` dengan nama asli
- [ ] **Jam buka asli** tiap UMKM — update field `jam` per UMKM di `umkm.json` (14 UMKM masih "Hubungi untuk jam buka")
- [ ] **Luas wilayah** & KK/penduduk terverifikasi — update di `index.html` section Data Wilayah

---

## 🔵 REDESIGN VISUAL UMKM — Perlu Brief Tersendiri

Sudah disepakati untuk dikerjakan, tapi butuh keputusan visual dulu sebelum eksekusi. Cakupan yang akan dibahas:

- **Grid halaman UMKM** — kartu lebih besar, foto lebih dominan, info lebih readable
- **Halaman detail UMKM** — layout cover foto, strip info, section produk
- **Card produk** — dari kotak emoji kecil ke tampilan yang lebih informatif

> Diskusikan di sesi tersendiri sebelum mulai coding.

---

## 🔵 WISHLIST — Nanti setelah yang di atas beres

- **Schema `WebSite`** di homepage — effort kecil, SEO boost (tambah 1 blok JSON-LD di `<head>`)
- **Halaman Sentra Bibit** — identitas terkuat Ngemplak, butuh halaman terpisah (keluar dari SPA), butuh diskusi arsitektur
- **Halaman kategori** (`/kategori/bibit-buah`, dst) — butuh arsitektur multi-halaman
- **Schema `BreadcrumbList`** di homepage
- **Google Search Console** — submit sitemap, pantau keyword (tugas Zen, bukan coding)
- **Domain `.id`** — keputusan Zen & perangkat dusun
- **Backlink lokal** — dari website Desa Samping, Kec. Kemiri, Kab. Purworejo

---

## 📌 URUTAN KERJA BERIKUTNYA

```
1 → Tulis ulang FAQ 19 UMKM (umkm.json) — sesi tersendiri
2 → Brief & eksekusi redesign visual UMKM (index.html + script.js + style.css)

--- menunggu data dari Zen ---
3 → Nomor kontak → aktifkan tombol Nyuwun Tulung di index.html
4 → Nama pengurus → isi tanda — di index.html tab Pengurus
```
