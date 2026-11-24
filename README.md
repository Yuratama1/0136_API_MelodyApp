# Melody API & Backend

Dokumentasi backend dan aset basis data untuk **Melody**, aplikasi katalog dan pemutar musik berbasis mobile.

> Repository ini berisi dokumentasi backend, definisi basis data, spesifikasi API, kebijakan keamanan, dan dokumentasi penyimpanan file. Platform backend yang telah dipilih untuk Melody adalah **Supabase**. Repository ini bukan server Express.js yang berdiri sendiri.

## Gambaran Umum Proyek

Melody adalah aplikasi Android yang dibangun menggunakan Kotlin dan Jetpack Compose. Aplikasi ini menyediakan fitur autentikasi pengguna, penelusuran dan pengelolaan katalog musik, playlist, favorit, pencarian, serta pemutaran audio.

Aplikasi mobile berkomunikasi dengan backend melalui layanan Supabase:

- **Supabase Auth** — autentikasi pengguna dan pengelolaan sesi.
- **Supabase REST API (PostgREST)** — akses data dan pertukaran respons JSON.
- **PostgreSQL** — basis data relasional utama.
- **Row Level Security (RLS)** — kebijakan pengaturan hak akses data di sisi backend.
- **Supabase Storage** — penyimpanan file audio katalog dan gambar.

Aplikasi Android menggunakan arsitektur MVVM dan Repository Pattern yang telah disetujui. Pencarian metadata musik publik ditangani secara terpisah melalui MusicBrainz API. MusicBrainz bukan sumber basis data utama Melody dan tidak digunakan untuk streaming audio.

## Ruang Lingkup Repository

Repository ini direncanakan untuk menyimpan:

| Direktori | Fungsi |
|---|---|
| `docs/` | Dokumentasi arsitektur backend dan spesifikasi API |
| `database/` | Skema PostgreSQL, migrasi, dan kebijakan RLS |
| `storage/` | Dokumentasi bucket penyimpanan dan struktur file |

Kode sumber aplikasi Android disimpan pada [Mobile Repository](https://github.com/Yuratama1/0136_MelodyApp) yang terpisah.

## Rencana Struktur Repository

```text
0136_API_MelodyApp/
├── README.md
├── docs/
│   ├── architecture.md
│   └── api-specification.md
├── database/
│   ├── schema.sql
│   ├── migrations/
│   └── policies/
│       └── rls.sql
├── storage/
│   └── storage-structure.md
└── .gitignore
```

File dan direktori akan ditambahkan secara bertahap sesuai persiapan dan hasil peninjauan task terkait. Struktur yang direncanakan ini tidak berarti bahwa basis data, kebijakan keamanan, atau proyek Supabase sudah dibuat maupun diterapkan.

## Model Data Utama

Rancangan awal basis data yang telah disetujui terdiri dari sembilan tabel:

1. `users`
2. `songs`
3. `artists`
4. `albums`
5. `genres`
6. `playlists`
7. `playlist_songs`
8. `favorites`
9. `play_history`

Detail kolom, batasan data, relasi antartabel, aturan penghapusan, dan hak akses akan didokumentasikan lebih lanjut pada file skema basis data dan kebijakan keamanan.

## Prinsip Keamanan

- Hak akses wajib ditegakkan oleh backend menggunakan RLS, bukan hanya dengan menyembunyikan elemen antarmuka.
- Pendaftaran publik tidak boleh memberikan kemampuan kepada pengguna untuk menetapkan peran Admin bagi dirinya sendiri.
- Pengguna hanya boleh mengakses dan mengelola playlist, favorit, serta riwayat pemutarannya sendiri.
- Hak Admin untuk mengelola katalog musik tidak otomatis memberikan akses ke data musik pribadi pengguna.
- Supabase Service Role Key dan kredensial istimewa lainnya tidak boleh disimpan di dalam aplikasi Android.
- Secret dan file konfigurasi lingkungan lokal tidak boleh diunggah ke repository ini.

## Status Pengembangan

**Status saat ini: Repository telah dibuat dan README telah disiapkan. Implementasi backend serta penerapan Supabase belum diverifikasi.**

Aset backend akan ditambahkan secara bertahap mengikuti daftar task Melody yang telah disetujui. Suatu task hanya dinyatakan selesai setelah kriteria penerimaan dan bukti implementasinya ditinjau.

## Repository Terkait

- [Melody Android Mobile Repository](https://github.com/Yuratama1/0136_MelodyApp)

## Teknologi yang Digunakan

- Supabase Auth
- Supabase REST API (PostgREST)
- PostgreSQL
- Row Level Security (RLS)
- Supabase Storage
- MusicBrainz Public API (pencarian metadata musik)

---

README ini menjelaskan arah pengembangan proyek yang telah disetujui. Status pengembangan harus diperbarui berdasarkan perubahan repository dan bukti implementasi yang benar-benar tersedia.
