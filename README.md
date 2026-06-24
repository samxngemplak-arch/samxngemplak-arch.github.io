# SIMBAH — Portal Digital Dusun Ngemplak

Website profil & layanan digital untuk Dusun Ngemplak, Desa Samping, Kecamatan
Kemiri, Kabupaten Purworejo, Jawa Tengah. Dibangun pakai HTML + CSS + JavaScript
murni (tanpa framework, tanpa build tool), hosting gratis via GitHub Pages.

**Live:** https://samxngemplak-arch.github.io/

> Status: tahap pengembangan bertahap. Belum pindah ke domain berbayar —
> rencana migrasi setelah dianggap matang oleh perangkat dusun
> (lihat bagian "Migrasi ke Domain Sendiri" di bawah).

---

## 📁 Struktur File

```
(root repo)
├── index.html          ← satu-satunya halaman HTML. Semua section
│                           (Beranda, UMKM, UMKM Detail, Agenda, Kas,
│                           Inventaris, Nyuwun Tulung, Tentang) ada di
│                           file ini, ditampilkan/disembunyikan lewat JS
│                           (lihat nav() di script.js)
├── 404.html            ← halaman error custom, auto-redirect ke Beranda
├── sitemap.xml         ← daftar URL untuk Google (SEO)
├── robots.txt          ← izin crawl untuk search engine
├── favicon.ico + img/favicon-*.png, icon-*.png, apple-touch-icon.png
│                           ← ikon tab browser & home screen HP
├── css/
│   └── style.css       ← SEMUA styling, 1 file. Pakai CSS variables
│                           di :root (warna, radius, dll) — jangan
│                           hardcode hex baru, tambah variable kalau perlu
├── js/
│   └── script.js       ← SEMUA logika & data dinamis (AGENDA, INVENTARIS,
│                           KAS, footer, navigasi, render UMKM, dll)
├── data/
│   └── umkm.json       ← data UMKM/usaha warga, dibaca oleh script.js
└── img/
    ├── logo.png         ← logo resmi Dusun Ngemplak (final, jangan ganti
    │                        kecuali memang mau rebranding)
    └── hero-bg.webp     ← foto/ilustrasi background hero di Beranda
                             (bisa diganti foto asli Ngemplak kapan saja)
```

> Belum ada folder `img/umkm/` — UMKM masih pakai emoji sebagai ikon
> sementara. Foto asli usaha warga bisa ditambahkan kapan saja begitu
> sudah ada foto yang layak.

---

## 🧩 Cara Kerja Website (Single Page, bukan multi-halaman)

Ini bukan website multi-halaman biasa. Semua section ada di **1 file
`index.html`**, masing-masing dibungkus `<div class="page" id="p-NAMA">`.
JavaScript (`nav('nama-section')`) yang mengatur section mana yang
tampil/sembunyi — URL tidak berubah-ubah per section (kecuali untuk
link share halaman detail UMKM).

Cara cari section tertentu di `index.html`: cari komentar seperti
`<!-- ======= UMKM ======= -->` atau cari `id="p-umkm"`, `id="p-agenda"`, dll.

---

## ✏️ Data yang Bisa Diedit (TANPA perlu paham JS)

Semua data yang sering berubah sudah dipisahkan ke variabel/file khusus.
Edit di sini saja — **tidak perlu** sentuh bagian lain dari kode.

### 1. UMKM — `data/umkm.json`

- Tambah usaha baru: copy salah satu blok `{ ... }`, paste sebelum `]`
  penutup, ganti isinya. Lihat field `_petunjuk` di baris paling atas
  file untuk detail tiap kolom.
- Jumlah UMKM di Hero & statistik dusun **otomatis bertambah** saat
  UMKM baru ditambahkan — tidak perlu update manual di `index.html`.
- Tombol WA otomatis tersembunyi kalau field `phone` kosong
  (diganti badge "📍 Lihat Maps").
- `fetch()` UMKM hanya berjalan kalau dibuka lewat server
  (Laragon/localhost atau GitHub Pages) — **tidak bisa** dibuka
  langsung klik dua kali dari File Explorer.

### 2. Agenda Dusun — `const AGENDA` di `js/script.js`

- Cari `const AGENDA = [` di `script.js`.
- Copy salah satu blok `{ ... }`, ganti tanggal (format wajib
  `YYYY-MM-DD`), judul, jam, lokasi, dan tag.
- Event yang tanggalnya sudah lewat otomatis hilang dari tampilan —
  tidak perlu dihapus manual.
- **Catatan kebijakan:** khusus event besar yang layak diketahui
  orang luar dusun (festival, sedekah bumi, HUT dusun, dll). Agenda
  rutin RT (kerja bakti, posyandu, pengajian) cukup di grup WA warga.

### 3. Inventaris Dusun — `const INVENTARIS` di `js/script.js`

- Cari `const INVENTARIS = [` di `script.js`.
- Tambah barang baru dengan copy salah satu blok `{ ... }`. Field
  `kelompok` menentukan barang masuk section mana (otomatis
  dikelompokkan, tidak perlu buat section HTML baru).

### 4. Transparansi Kas — `const KAS_UPDATE` & `KAS_TOTAL` di `js/script.js`

- `KAS_TOTAL` : total gabungan semua kas (string, misal `'Rp 905.000'`)
- `KAS_UPDATE` : tanggal update terakhir (misal `'23 Juni 2026'`)
- Saldo per komunitas (RT 01, RT 02, Karang Taruna, PKK) diisi langsung
  di `index.html` — cari `kaskom-saldo`.
- **PENTING:** angka di website TIDAK live-sync dengan Google Sheets.
  Update angka di kode setiap ada perubahan saldo yang signifikan.

### 5. Nomor WhatsApp Utama — `const WA_UTAMA` di `js/script.js`

- 1 variabel ini dipakai di SEMUA tombol WA di seluruh halaman.
- Ganti di sini saja — tidak perlu cari satu-satu di `index.html`.
- **Catatan penting:** kontak di Nyuwun Tulung yang belum ada nomor
  aslinya (Kepala Desa, Bidan Desa, dll) saat ini **jangan diklik** —
  masih dalam proses pengumpulan nomor asli. Tombolnya akan dinonaktifkan
  begitu perbaikan bug §2.1 selesai dikerjakan.

### 6. Footer — `templateFooter()` di `js/script.js`

- Footer dirender dari 1 fungsi `templateFooter()`, otomatis ditempel
  ke semua id yang terdaftar di array `FOOTER_SLOTS`.
- Edit alamat, kontak, sosmed di `templateFooter()` satu kali —
  semua halaman yang pakai footer ikut berubah.
- Kalau nanti ada halaman baru yang butuh footer: tambah
  `<div class="footer-slot" id="footer-NAMA-BARU"></div>` di
  `index.html`, lalu daftarkan id-nya ke `FOOTER_SLOTS` di `script.js`.

### 7. Ganti Logo / Foto Hero

- **Logo**: `img/logo.png` — sudah final, jangan diganti tanpa alasan
  kuat (ini identitas visual yang sudah disepakati).
- **Foto background hero**: `img/hero-bg.webp` — saat ini pakai foto
  ilustratif, bisa diganti foto asli Ngemplak kapan saja. Cukup replace
  file dengan nama yang sama (format boleh `.jpg`/`.png`, sesuaikan nama
  di CSS kalau diganti format).

### 8. Kontak Penting (Nyuwun Tulung) & Struktur Pengurus

- Masih banyak placeholder ("nama menyusul", "Segera diperbarui") —
  cari teks itu di `index.html` untuk menggantinya begitu data asli ada.
- Nomor yang belum diisi sebaiknya dikosongkan dulu, jangan dibiarkan
  jalan dengan fallback ke nomor WA Zen (lihat ⚠️ Status Bug di bawah).

---

## 🎨 Sistem Desain (jangan dilanggar tanpa diskusi)

- **Warna:** semua lewat CSS variable di `:root` (`css/style.css`, paling
  atas) — `--iv` (ivory/krem, dasar), `--gr` (hijau, aksen utama), `--br`
  (emas/bronze, detail halus). Proporsi target: Ivory 70% : Hijau 20% : Emas 10%.
  Jangan tulis hex color baru langsung di selector.
- **Mobile-first, full-responsive.** Breakpoint `@media (min-width: 1024px)`
  di akhir `style.css` untuk varian desktop (nav atas, grid 2-kolom di
  Beranda, dll).
- **Karakter visual:** hangat, agraris, tenang, sederhana, modern-tradisional.
  Hindari gaya startup/fintech/SaaS.

---

## 🚀 Cara Update Website (workflow: edit → drag-drop GitHub)

Repo ini tidak punya CI/CD otomatis. Setiap ada perubahan file:

1. Siapkan file yang sudah diubah
2. Buka repo `samxngemplak-arch.github.io` di GitHub
3. Drag & drop file ke folder yang sesuai (replace file lama)
4. Klik **Commit changes**
5. Tunggu 1–2 menit → GitHub Pages otomatis rebuild

---

## ⚠️ Status Bug & Pekerjaan Aktif

### 🔴 Bug §2.1 — Kontak Nyuwun Tulung fallback ke WA Zen (BELUM DIPERBAIKI)

Kontak di section Nyuwun Tulung yang **belum ada nomor aslinya** (Kepala Desa
Samping, Ketua RW, Bidan Desa, Babinsa, Polsek Kemiri, Damkar, Tokoh Agama)
saat ini di-fallback diam-diam ke `WA_UTAMA` (nomor Zen) oleh mekanisme
auto-inject di `index.html`.

**Risiko**: warga klik "💬 WA Bidan Desa" tapi yang menerima chat adalah Zen.

**Perbaikan yang perlu dikerjakan**: untuk kontak tanpa nomor asli, tombol WA
harus dinonaktifkan dan ditampilkan sebagai "Nomor belum tersedia" — jangan
fallback diam-diam. Ini bisa dikerjakan sekarang (Rp0, kode saja) tanpa harus
menunggu nomor asli terkumpul.

---

## 🔄 Roadmap Singkat

| Prioritas | Item | Status |
|-----------|------|--------|
| 🔴 Tinggi | Bug kontak Nyuwun Tulung (§2.1) | Belum dikerjakan |
| 🟡 Data | Nomor kontak asli perangkat dusun | Pengumpulan lapangan |
| 🟡 Data | Nama pengurus organisasi (BPD, PKK, dll) | Pengumpulan lapangan |
| 🟡 Data | Foto asli UMKM & dusun | Pengumpulan lapangan |
| 🟢 Enhancement | Sejarah Dusun → accordion collapsible | Belum dikerjakan |
| 🟢 Enhancement | Visualisasi bar saldo kas (CSS murni) | Belum dikerjakan |
| 🟢 Enhancement | CTA button "Lihat UMKM →" di Hero | Belum dikerjakan |
| ⚪ Wishlist | Histori transaksi kas | Tunda |
| ⚪ Wishlist | Pengaduan warga (terintegrasi Nyuwun Tulung) | Tunda |

Detail lengkap dengan reasoning ada di `ROADMAP___MASTER_SIMBAH.md`.

---

## 🔄 Migrasi ke Domain Sendiri (Nanti)

Kalau sudah matang dan mau pakai domain sendiri (misal `dusunngemplak.id`):

1. Beli domain (Cloudflare/Niagahoster, ±Rp 30–150rb/tahun)
2. GitHub repo → **Settings → Pages → Custom domain**, isi domain baru
3. Di pengelola DNS, tambah CNAME record ke `samxngemplak-arch.github.io`
4. Tunggu propagasi DNS (5–30 menit, kadang hingga 24 jam)
5. Selesai — konten & kode tidak perlu diubah sama sekali

---

## ⚠️ Batasan yang Disengaja (jangan ditambahkan tanpa diskusi)

SIMBAH sengaja **tidak** punya: login warga, dashboard admin, forum/chat
warga, sistem surat-menyurat, booking inventaris, WA Gateway/notifikasi
otomatis, atau backend/database apapun.

Semua data tersimpan sebagai file statis (JSON + JS array) dan diedit manual
oleh pengelola. Ini keputusan sadar demi kemudahan maintenance jangka panjang
oleh 1–2 orang tanpa tim IT — bukan keterbatasan yang perlu "diperbaiki".

Alasan detail dan daftar fitur yang ditolak permanen ada di
`ROADMAP___MASTER_SIMBAH.md`.
