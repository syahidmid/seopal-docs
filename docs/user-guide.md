# User Guide — SEOPal Article Generator

## Apa itu SEOPal?

SEOPal adalah plugin WordPress yang secara otomatis menghasilkan artikel SEO berdasarkan keyword yang Anda tentukan. Plugin ini menggunakan AI (Claude, OpenAI, atau Gemini) dengan pipeline multi-stage:

1. **SERP Analysis** — Mengambil data dari Google (PAA, headings, competitors)
2. **Brief Generation** — AI membuat struktur artikel
3. **Article Writing** — AI menulis artikel 1000-1500 kata
4. **Taxonomy Decision** — AI memilih kategori dan tags
5. **Publish** — Artikel dipublish sebagai Draft atau Published

---

## Mode Penggunaan

### Mode 1: SaaS Backend (Direkomendasikan)

Menghubungkan ke server pusat dengan license key. System prompt dan API dikelola oleh developer.

**Cara setup:**
1. Install dan aktifkan plugin
2. Buka **AI Generator > Settings**
3. Masukkan License Key dan klik "Validate"
4. (Opsional) Masukkan API key sendiri untuk BYOK (Bring Your Own Key)
5. Klik "Scan Taxonomy" untuk cache kategori dan tags
6. Tambahkan keyword di **AI Generator > Keywords**

### Mode 2: Local API

Menggunakan API key AI Anda sendiri secara langsung (tanpa server pusat).

**Cara setup:**
1. Install dan aktifkan plugin
2. Buka **AI Generator > Settings**
3. Konfigurasi API key (Claude, OpenAI, atau Gemini)
4. Konfigurasi Serper.dev API key untuk SERP analysis
5. Klik "Scan Taxonomy"
6. Tambahkan keyword dan mulai generate

---

##Cara Menggunakan

### Menambah Keyword

1. Buka **AI Generator > Keywords**
2. Pilih salah satu metode:

   **Metode 1 — Input Manual:**
   - Masukkan primary keyword
   - Masukkan secondary keywords (pisahkan dengan koma)
   - Klik "Add Keyword"

   **Metode 2 — Import CSV:**
   - Siapkan file CSV dengan format: `primary_keyword,secondary_keywords`
   - Klik "Import CSV"
   - Upload file

### Menjalankan Generation

**Opsi 1 — Otomatis via WP Cron:**
Plugin akan secara otomatis memproses keyword berdasarkan jadwal (default: 3 artikel/hari). Atur jadwal di **Settings > Articles Per Day**.

**Opsi 2 — Manual (Run Now):**
1. Di halaman Keywords, klik tombol "Run Now" pada baris keyword yang ingin diproses
2. Plugin akan menjalankan pipeline lengkap

### Monitoring Progress

- **Keywords Page:** Lihat status setiap keyword (queued/generating/done/failed)
- **Logs Page:** Lihat detail log setiap stage generation
- **Reporting Page:** Lihat statistik total, token usage, dan estimasi biaya

---

## Fitur Tambahan

### Featured Image Generation

Plugin dapat secara otomatis menghasilkan featured image menggunakan DALL-E 3 setelah artikel dipublish. Aktifkan di **Settings > Featured Image**.

### Fallback Provider

Jika provider utama (misal: Claude) gagal, plugin akan otomatis mencoba provider cadangan (OpenAI/Gemini).

### BYOK (Bring Your Own Key)

Anda dapat menggunakan API key sendiri dengan backend SaaS. API key disimpan terenkripsi menggunakan WP salt.

---

## FAQ

### API key mana yang diperlukan?

**Mode SaaS:** Hanya License Key (opsional BYOK)

**Mode Local:** Satu AI provider (Claude, OpenAI, atau Gemini) + Serper.dev key

### Bagaimana cara import keyword dalam jumlah banyak?

Gunakan tombol "Import CSV" di halaman Keywords. Format: `primary_keyword,secondary_keywords`

### Apa yang terjadi jika provider gagal?

Plugin akan otomatis mencoba provider berikutnya jika dikonfigurasi. Jika semua provider gagal, keyword akan ditandai sebagai "failed" dengan pesan error.

### Bagaimana jika saya ingin menggenerate ulang artikel yang gagal?

Ubah status keyword ke "queued" lalu jalankan ulang.