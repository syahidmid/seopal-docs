# Settings Reference — SEOPal Article Generator

Halaman ini menjelaskan semua pengaturan yang tersedia di plugin.

---

## Halaman Settings (AI Generator > Settings)

### Provider Configuration

| Setting | Tipe | Default | Deskripsi |
|---------|------|---------|-----------|
| Primary Provider | Dropdown | Claude | Provider AI utama yang digunakan |
| Fallback Provider 1 | Dropdown | Disabled | Provider cadangan pertama |
| Fallback Provider 2 | Dropdown | Disabled | Provider cadangan kedua |

**Available Providers:** Claude, OpenAI, Gemini, Disabled

### Claude Settings

Hanya muncul jika Claude dipilih di salah satu provider.

| Setting | Tipe | Default | Deskripsi |
|---------|------|---------|-----------|
| API Key | Password | - | API key Anthropic |
| Model | Text | claude-sonnet-4-20250514 | Model yang digunakan |

### OpenAI Settings

Hanya muncul jika OpenAI dipilih di salah satu provider.

| Setting | Tipe | Default | Deskripsi |
|---------|------|---------|-----------|
| API Key | Password | - | API key OpenAI |
| Model | Text | gpt-4o-mini | Model yang digunakan |

### Gemini Settings

Hanya muncul jika Gemini dipilih di salah satu provider.

| Setting | Tipe | Default | Deskripsi |
|---------|------|---------|-----------|
| API Key | Password | - | API key Google Gemini |
| Model | Text | gemini-1.5-flash | Model yang digunakan |

### SERP & General

| Setting | Tipe | Default | Deskripsi |
|---------|------|---------|-----------|
| Serper.dev API Key | Password | - | API key untuk SERP analysis |
| Articles Per Day | Number | 3 | Jumlah artikel yang di-generate per hari (1-24) |
| Default Post Status | Radio | Draft | Status artikel saat publish |

### Taxonomy

| Setting | Tipe | Default | Deskripsi |
|---------|------|---------|-----------|
| Scan & Refresh Categories/Tags | Button | - | Scan ulang semua kategori dan tags dari WP |
| Categories Cache | Display | - | Jumlah kategori yang sudah di-cache |
| Tags Cache | Display | - | Jumlah tags yang sudah di-cache |

### SaaS Configuration (Mode Backend)

| Setting | Tipe | Default | Deskripsi |
|---------|------|---------|-----------|
| License Key | Text | - | License key untuk aktivasi SaaS mode |
| User API Key (BYOK) | Password | - | API key sendiri (opsional) |
| Featured Image | Toggle | Off | Aktifkan DALL-E 3 untuk featured image |

### Content Preferences

| Setting | Tipe | Default | Deskripsi |
|---------|------|---------|-----------|
| Language | Dropdown | Indonesia | Bahasa artikel |
| Style | Dropdown | semi-formal | Gaya penulisan |
| Address | Text | kamu | Pen称呼 (kamu/anda/dll) |
| Article Min Words | Number | 1000 | Minimal jumlah kata |
| Article Max Words | Number | 1500 | Maksimal jumlah kata |
| Include FAQ | Toggle | false | Sertakan FAQ section |
| Slug Method | Dropdown | primary_key | Cara membuat slug |

---

## Halaman Keywords (AI Generator > Keywords)

### Tabel Keyword

| Kolom | Deskripsi |
|-------|-----------|
| Primary Keyword | Keyword utama |
| Secondary | Secondary keywords (jika ada) |
| Status | Status pemrosesan (queued/generating/done/failed) |
| Post | Link ke artikel yang di-generate |
| Created | Tanggal ditambahkan |
| Actions | Tombol Run Now dan Delete |

### Filter Status

Filter keyword berdasarkan status:
- All
- Queued
- Generating
- Done
- Failed

---

## Halaman Logs (AI Generator > Logs)

### Tabel Log

| Kolom | Deskripsi |
|-------|-----------|
| Keyword | Primary keyword |
| Stage | Tahap pipeline (serp/brief/article/taxonomy/publish) |
| Status | Success atau Error |
| Provider | Provider yang digunakan |
| Model | Model AI yang digunakan |
| Tokens | Jumlah token yang digunakan |
| Message | Pesan log |
| Time | Timestamp |

---

## Halaman Reporting (AI Generator > Reporting)

### Section 1: Overview Metrics

| Metric | Deskripsi |
|--------|-----------|
| Total Keywords | Total keyword yang ditambahkan |
| Artikel Generated | Jumlah artikel berhasil dibuat + persentase |
| Dalam Antrian | Jumlah menunggu + estimasi hari |
| Gagal | Jumlah gagal |

### Section 2: Progress Generation

- Progress bar percentage
- Breakdown per stage (SERP, Brief, Article, Taxonomy, Publish)
- Fallback usage count
- Token usage per provider dengan estimasi biaya

### Section 3: Token Usage per Stage

Tabel agregat token usage per stage dan provider.

---

## Options Database (wp_options)

Plugin menyimpan setting di WordPress options:

```
aigc_primary_provider        → 'claude' | 'openai' | 'gemini'
aigc_fallback_provider_1     → provider atau ''
aigc_fallback_provider_2     → provider atau ''
aigc_claude_api_key         → (encrypted)
aigc_claude_model            → string
aigc_openai_api_key         → (encrypted)
aigc_openai_model           → string
aigc_gemini_api_key         → (encrypted)
aigc_gemini_model           → string
aigc_serper_api_key         → (encrypted)
aigc_articles_per_day       → int
aigc_default_post_status    → 'draft' | 'publish'
aigc_categories_cache       → JSON
aigc_tags_cache              → JSON
aigc_plugin_version         → string
```

---

## Database Tables

### aigc_keywords

```sql
CREATE TABLE {prefix}aigc_keywords (
    id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    primary_keyword VARCHAR(255) NOT NULL,
    secondary_keywords JSON DEFAULT NULL,
    status ENUM('queued','generating','done','failed') DEFAULT 'queued',
    post_id BIGINT UNSIGNED DEFAULT NULL,
    scheduled_at DATETIME DEFAULT NULL,
    generated_at DATETIME DEFAULT NULL,
    error_message TEXT DEFAULT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    UNIQUE KEY unique_primary (primary_keyword)
);
```

### aigc_logs

```sql
CREATE TABLE {prefix}aigc_logs (
    id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    keyword_id BIGINT UNSIGNED NOT NULL,
    stage VARCHAR(50) NOT NULL,
    status ENUM('success','error') NOT NULL,
    provider_used VARCHAR(20) DEFAULT NULL,
    model_used VARCHAR(100) DEFAULT NULL,
    message TEXT DEFAULT NULL,
    tokens_used INT DEFAULT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```