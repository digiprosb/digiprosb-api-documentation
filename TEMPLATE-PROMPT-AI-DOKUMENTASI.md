# Template prompt AI — dokumentasi proyek (MkDocs + README)

Salin **blok di bawah** (antara garis `---`) ke chat AI (Cursor, ChatGPT, dll.) lalu isi placeholder `[...]` sesuai proyek Anda.

---

## PROMPT (salin dari sini)

Saya ingin kamu membuat **dokumentasi teknis** untuk proyek berikut, pola dan kualitas mirip dokumentasi API yang rapi (multi-halaman, navigasi sidebar, bisa di-build ke situs statis lokal).

### Konteks proyek

- **Nama / jenis proyek:** [contoh: SDK Node, API backend, library Python, monorepo, dll.]
- **Path / root kode:** [folder workspace atau repo]
- **Bahasa dokumentasi:** [Bahasa Indonesia / Inggris / dwibahsa]
- **Audiens:** [developer integrator / tim internal / kontributor open source]

### Tujuan output

1. **README.md** di root proyek: pengantar singkat, cara instal, prasyarat, tautan ke dokumentasi detail, cara menjalankan dokumentasi lokal (jika ada MkDocs).
2. **Dokumentasi multi-halaman** dengan **MkDocs** + tema **Material**:
   - File konfigurasi `mkdocs.yml` (atau letakkan di subfolder `[FOLDER_DOCS]` jika saya minta semua di dalam `docs/` saja).
   - Folder sumber Markdown (mis. `doc/` atau `guide/`) berisi bab-bab logis.
   - `requirements-docs.txt` berisi `mkdocs`, `mkdocs-material`, `pymdown-extensions`.
   - `.gitignore` memasukkan folder output `site/` (dan `docs/site/` jika relevan).
3. **README.md di dalam folder dokumentasi** (`docs/README.md` atau setara) yang menjelaskan isi folder, cara `mkdocs serve` / `mkdocs build`, dan beda antara “panduan” vs “referensi otomatis” jika ada.
4. Isi bab **selaras dengan kode nyata**: baca `src/`, `package.json`, env yang dipakai, error yang dilempar, endpoint/path yang ada di kode — jangan mengarang perilaku yang tidak ada di implementasi.
5. Jika ini **API / SDK**: sertakan **tabel environment variables** yang benar-benar dipakai konstruktor/config, dan **daftar endpoint atau method** sesuai file sumber.
6. **Tanpa** menyebut merek / dokumentasi pihak ketiga sebagai acuan (kecuali saya minta).
7. **Jangan** menulis dokumentasi tentang deploy ke GitHub Pages / `gh-pages` / CI/CD publikasi — hanya pratinjau lokal (`mkdocs serve`, `mkdocs build`).

### Struktur nav MkDocs (sesuaikan dengan proyek)

Usulkan nav seperti: Beranda → Memulai / Instalasi → Konfigurasi → [modul fitur per domain] → Referensi → [Lampiran]. Sesuaikan nama file `.md` dengan istilah domain proyek saya.

### Setelah selesai

Ringkas di chat: daftar file yang dibuat/diubah, dan perintah untuk pratinjau lokal (`mkdocs serve`).

Lakukan pekerjaan ini di workspace saya sekarang.

---

## PROMPT (sampai sini)

---

## Cara pakai cepat

1. Ganti semua `[...]` di atas dengan data proyek Anda.
2. Tambahkan kalimat khusus jika perlu, mis.: *"Dokumentasi hanya dalam folder `docs/`, jangan di root"* atau *"Sertakan contoh curl untuk setiap endpoint"*.
3. Lampirkan / buka folder proyek di Cursor agar AI bisa baca kode.

## Opsional: variasi singkat (one-liner)

```
Buat dokumentasi MkDocs Material (Bahasa Indonesia) untuk proyek ini: baca kode di src/, tulis README root + docs/README + folder panduan + mkdocs.yml + requirements-docs.txt + .gitignore site/, isi selaras implementasi nyata, tanpa referensi kompetitor. Tanpa bab deploy/hosting GitHub; hanya mkdocs serve/build lokal.
```
