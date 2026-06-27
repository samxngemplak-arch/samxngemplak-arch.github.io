# SIMBAH — Audit & Next Step

> Diperbarui: 27 Juni 2026 — sesi sore, trust strip + UI fixes selesai.
> Cara pakai: kerjakan dari atas ke bawah. Coret kalau sudah deploy & dicek live.

---

## ✅ SUDAH SELESAI

- [x] Domain canonical → `simbahngemplak.vercel.app`
- [x] Sitemap — 19 URL UMKM individual `?umkm=slug`, lastmod 2026-06-26
- [x] **[OPT-04]** `sitemap.xml` — tambah `<image:image>` per 19 UMKM (cover.webp + title), lastmod 2026-06-27
- [x] Heading semantik, preconnect, aria-label, loading lazy/eager
- [x] SEO per-UMKM — title, desc, OG, Twitter, canonical, Schema `LocalBusiness` + `FAQPage` dinamis
- [x] Schema `GovernmentOrganization` + `WebSite` statis di `<head>`
- [x] Schema `LocalBusiness` field `image` → `img/branding/logo.png`
- [x] Shuffle berbobot Beranda — semua kategori terwakili
- [x] Jam operasional — display "Fleksibel, hubungi WA" untuk UMKM bibit (buka subuh/malam), bukan jam kaku
- [x] Deskripsi 19 UMKM ditulis ulang per karakter usaha
- [x] Filter chip `data-filter` + active state
- [x] Data produk spesifik, koreksi karakter & kategori
- [x] Rahman Grosir Bibit masuk `id=3`
- [x] FAQ per UMKM — accordion, Schema `FAQPage`, semua ditulis ulang (tidak ada "Ya." generik)
- [x] seoTitle & seoDesc per UMKM — dalam batas karakter Google (title ≤70, desc ≤160)
- [x] Area layanan per UMKM — field `area`, tampil di info operasional, Schema `areaServed`
- [x] Disclaimer Agenda & Kas
- [x] Foto UMKM — 19/19 sudah `cover.webp` + gallery (3–4 foto, 62 total)
- [x] Internal linking Usaha Terkait — field `terkait` (53 referensi, semua ID valid)
- [x] Hapus section Testimoni Warga
- [x] Card Produk & Jasa — grid 2 kolom, field `keterangan`, label WA per produk dihapus
- [x] Nomor kontak belum ada → "Nomor belum tersedia" (tidak fallback ke Zen)
- [x] **[BUG-01]** Filter chip reset ke "Semua" saat `goBack()` & `nav('umkm')`
- [x] **[BUG-02]** Variable `history` → `navHistory`
- [x] **[BUG-03]** Twitter Card `summary` → `summary_large_image`
- [x] **[BUG-04]** Hapus `setTimeout` 50ms di `goToUMKM()`
- [x] **[RISIKO-01]** Preload `hero-bg.webp`
- [x] **[RISIKO-02]** `manifest.json` + theme-color
- [x] **[RISIKO-03]** Cache-Control img/css/js di `vercel.json`
- [x] **[KONTEN-01]** Tagline 19 UMKM — field `tagline`, render `#ud-tagline`
- [x] **[KONTEN-02]** Teks tombol Maps → "📍 Lihat Maps & Ulasan"
- [x] **[OPT-01]** Stat hardcode `18` → `19`
- [x] **[OPT-02]** `.uimg` & `.ug-img` sudah punya `position: relative`
- [x] **[OPT-03]** Kategori "Pertanian" → tidak perlu ditambah (semua UMKM bibit masuk "Perkebunan", keputusan final)

### Sesi 27 Juni 2026 (pagi)
- [x] SEO `index.html` — `<title>`, meta description, OG/Twitter desc, Schema description disinkronkan; ada angka & keyword spesifik
- [x] Footer watermark — ganti PNG+filter → SVG vektor bersih (`watermark-logo.svg`), opacity 13%, rotate -15°, pojok kanan bawah; tambah `::before` kiri atas lebih kecil diagonal balance
- [x] Footer border-top emas tipis, ukuran logo & teks dinaikkan sedikit
- [x] Banner CTA UMKM — "Usahamu belum ada di sini?" + tombol "Daftar via WA →" dengan pesan template pre-filled
- [x] Inventaris disclaimer — catatan "data ilustrasi awal, belum real" di atas daftar

### Sesi 27 Juni 2026 (sore)
- [x] Trust strip beranda — kalkulasi otomatis rata-rata rating & total ulasan dari `umkm.json` (weighted average); statis "1825 Dusun Bersejarah"
- [x] Trust strip warna — angka hijau (`--gr`), bintang & plus emas (`--br`) via `<span class="ts-star">` / `<span class="ts-sup">`; JS inject `innerHTML` bukan `textContent`
- [x] Desktop trust strip — pindah masuk ke dalam hero (`div.hero-trust`), trust strip standalone disembunyikan (`display:none` di `@media 1024px`); angka putih di atas foto hero
- [x] Hero desktop padding dikompres (`28px/24px`) supaya ticker toa masih in-fold setelah hero-trust ditambah
- [x] Mini card border — dari `rgba(0,0,0,.06)` (nyaris invisible) → `1px solid #DDD7C8` + `box-shadow: 0 1px 3px rgba(0,0,0,.06)`; hierarki tetap terjaga vs hero card yang hijau tebal

---

## 🟡 MENUNGGU DATA LAPANGAN (tugas Zen)

- [ ] **Nomor kontak** Nyuwun Tulung (Kades, RW, RT 01, RT 02, Bidan, Babinsa)
      → cara aktifkan: isi `href` di `index.html`, hapus atribut `data-kontak-publik`
- [ ] **Nama pengurus** organisasi (BPD, Takmir, PKK, Posyandu, Karang Taruna)
      → Ctrl+F nama jabatan di `index.html`, ganti `—` dengan nama asli
- [ ] **Foto hero beranda** → keputusan: tetap ilustrasi; ganti hanya kalau ada foto asli Ngemplak yang jauh lebih bagus

---

## 🔵 GOOGLE SEARCH CONSOLE — pantau terus

- [x] Sitemap sudah disubmit ke GSC
- [ ] Indexing masih proses (normal 4 hari–4 minggu)
      → kalau setelah 4 minggu nol: buka URL Inspection Tool → Request Indexing

---

## 🔵 WISHLIST — Nanti (tidak ada urgensi sekarang)

| Item | Catatan |
|---|---|
| Schema `BreadcrumbList` | Revisit kalau ada domain `.id` + SSR/prerender |
| Domain `.id` | Keputusan Zen & perangkat dusun |
| Backlink lokal | Koordinasi dengan web Desa Samping / Kec. Kemiri / Kab. Purworejo |
| Halaman Sentra Bibit | Butuh diskusi arsitektur, keluar dari SPA |

---

## 📌 STATUS SEKARANG

```
Tidak ada item coding yang outstanding.

Yang perlu dilakukan Zen:
  → Upload index.html, style.css, script.js dari sesi sore ke GitHub
  → Kumpulkan nomor kontak Nyuwun Tulung
  → Kumpulkan nama pengurus organisasi

Yang perlu dipantau:
  → GSC indexing report (~4 minggu dari submit sitemap, deadline ~25 Juli 2026)
```
