# Changelog — SEOPal Article Generator

## [1.0.3] - 2026

### Added
- Integrasi SaaS backend dengan struktur `prompt_type` + `config`
- System prompts sekarang terpusat di backend (bisa diupdate tanpa update plugin)
- Prompt building berbasis config (language, style, address)

### Changed
- Refactor `class-ai-router` untuk mengirim payload yang benar ke backend

---

## [1.0.2] - 2026

### Added
- Integrasi SaaS backend dengan validasi license
- Dukungan BYOK (simpan API key terenkripsi)
- Kompatibilitas PHP 7.4
- Featured Image generation dengan DALL-E 3
- Secondary keywords separator fix
- Writer per Category feature

### Fixed
- API key visibility toggle
- Writer mapping category matching

---

## [1.0.1] - 2026

### Added
- Secondary keywords separator fix
- Writer per Category feature
- API key visibility toggle
- Modal CSS untuk writer management

---

## [1.0.0] - 2026-04-29

### Added
- Initial release
- Multi-stage pipeline: SERP → Brief → Article → Taxonomy → Publish
- Dukungan AI providers: Claude, OpenAI, Gemini
- SERP analysis via Serper.dev
- Reporting dashboard dengan token usage dan cost estimates
- WP Cron scheduling (1-24 artikel/hari)

---

## Older Releases

### Project Initialization (2026-04-29)

- Setup plugin WordPress untuk generate artikel SEO otomatis via AI
- Setup GitHub private repo
- Setup symlink ke Local site untuk development
- Convert readme.txt ke format Markdown
- Fix API key visibility (password field + toggle)
- Fix column width uniformity di settings page
- Add configurable Prompt Configuration (language, address, style, dll)
- Add separate Prompt page di admin menu
- Add slug method options: primary_key, title, ai
- Add Featured Image Generation dengan DALL-E 3
- Implement Feedback Loop / Auto-Fix post-processing