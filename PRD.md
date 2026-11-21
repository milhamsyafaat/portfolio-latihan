# PRD — Portofolio Fahdin

**Status:** Draf
**Sumber acuan:** isi repo ini (`index.html`, `css/style.css`, `js/script.js`, `README.md`, `github-guide-global.md`, `semantic-versioning-guide.md`)
**Bahasa produk:** Indonesia (`lang="id"`)

---

## 1. Ringkasan Produk

Portofolio satu halaman statis untuk Fahdin, seorang desainer dan frontend developer asal Bandung. Halaman memperkenalkan profil, menampilkan tiga karya pilihan, dan menyediakan jalur kontak lewat email. Seluruh tampilan dibangun tanpa proses build, tanpa dependency lokal, dan tanpa backend.

## 2. Latar Belakang & Masalah

Portofolio ini masih berupa contoh latihan yang isinya dapat dikembangkan. Beberapa informasi masih berupa placeholder dan sejumlah tugas perbaikan belum dikerjakan (lihat `README.md`). Tujuan PRD ini adalah menetapkan ruang lingkup, kebutuhan, dan kriteria penerimaan agar kontributor dapat mengerjakan satu tugas tanpa menebak arah produk.

Masalah yang ingin diselesaikan:

- Pengunjung perlu memahami siapa Fahdin, apa yang ia kerjakan, dan bagaimana menghubunginya dalam satu kali kunjungan.
- Kontributor perlu batas kerja yang jelas agar perubahan tidak bertabrakan dan tidak mengarang konten.
- Halaman perlu tetap nyaman dipakai di ponsel dan saat pengaturan gerakan dikurangi aktif.

## 3. Tujuan & Non-Tujuan

### Tujuan

1. Menyajikan profil, fokus kerja, dan karya pilihan dalam satu halaman yang dapat dipindai cepat.
2. Menyediakan jalur kontak yang berfungsi (email dan tautan sosial).
3. Menjaga pengalaman baca yang konsisten di desktop dan ponsel, termasuk pada lebar 320 piksel.
4. Menjaga animasi tetap nyaman saat `prefers-reduced-motion` aktif.
5. Menjadi media latihan kontribusi: satu tugas, satu pull request.

### Non-Tujuan

- Bukan aplikasi dengan backend, autentikasi, database, atau CMS.
- Bukan toko, blog, atau sistem manajemen konten.
- Tidak menambahkan dependency, framework, atau proses build tanpa persetujuan fasilitator (aturan README).
- Tidak membuat halaman detail proyek pada iterasi ini; itu tercatat sebagai backlog (tugas 3).

## 4. Target Pengguna

| Pengguna | Kebutuhan utama |
|---|---|
| Perekrut / calon kolaborator | Melihat profil, fokus, karya, dan cara menghubungi dengan cepat. |
| Sesama desainer/developer | Menilai kualitas visual, detail interaksi, dan kerapian implementasi. |
| Kontributor latihan | Menemukan satu tugas yang jelas, mengerjakannya, lalu mengajukan PR. |
| Fasilitator | Menjaga konsistensi konten, desain, dan aturan kontribusi. |

## 5. Ruang Lingkup

### Termasuk (kondisi saat ini)

- Satu halaman dengan bagian: loader, header/navigasi, hero, tentang, karya, dan footer.
- Tiga kartu karya: Pasar Pagi, Ruang Dengar, Lintas Jalan.
- Animasi pemuatan dan reveal saat scroll menggunakan GSAP + ScrollTrigger dari CDN.
- Layout responsif dengan breakpoint 800px dan 540px.
- Dukungan `prefers-reduced-motion` di JS dan CSS.

### Di luar lingkup

- Halaman detail proyek, formulir kontak, analytics, dan SEO lanjutan (sebagian tercatat di backlog).
- Perubahan arah desain atau penambahan dependency tanpa diskusi dengan fasilitator.

## 6. Arsitektur & Teknologi

| Aspek | Kondisi saat ini |
|---|---|
| Entrypoint | `index.html` |
| Styling | CSS vanilla di `css/style.css` dengan custom properties; nama kelas bergaya BEM |
| Tailwind | Hanya Play CDN + `tailwind.config` inline untuk warna `paper`, `ink`, `moss`, `clay` |
| Animasi | GSAP 3.12.5 dan ScrollTrigger dari CDN |
| JavaScript | `js/script.js`, dimuat setelah GSAP/ScrollTrigger |
| Build / test / lint | Tidak ada |
| Aset gambar | Tidak ada; visual karya dibuat dari HTML + CSS |
| Prasyarat | Koneksi internet untuk CDN; dapat dibuka langsung atau lewat Laragon |

Catatan teknis:

- Warna palet terdefinisi ganda: di `tailwind.config` (`index.html`) dan `:root` (`style.css`). Perubahan warna harus menyentuh keduanya.
- Lebar halaman memakai `min(100% - 96px, 1248px)` lewat `.page-wrap` / `.section-wrap`, dengan penyesuaian di breakpoint.
- `body.is-loading` mengunci scroll (`overflow: hidden`) selama overlay loader tampil.

## 7. Kebutuhan Fungsional

### FR-1 Loader

- Menampilkan teks "sedang disiapkan", angka progres `00`, dan track progres.
- Angka bergerak ke `100` dan track terisi, lalu overlay bergeser ke atas dan dihapus.
- Setelah loader selesai, elemen hero tampil dengan animasi bertahap.
- Jika elemen loader tidak ada, GSAP tidak tersedia, atau reduced motion aktif, halaman langsung ditampilkan dan scroll dibuka.

### FR-2 Header & Navigasi

- Wordmark "fahdin." mengarah ke `#home`.
- Navigasi berisi "Tentang" (`#about`), "Karya" (`#projects`), dan "Ngobrol" (email).
- Smooth scroll aktif, kecuali saat reduced motion.
- Fokus keyboard terlihat dengan outline berwarna `clay`.

### FR-3 Hero

- Menampilkan label "Desainer & frontend developer" beserta lokasi "Bandung, Indonesia".
- Judul utama "Bikin hal digital terasa dekat."
- Paragraf pengantar dan tautan "Lihat pilihan karya" menuju bagian karya.
- Menampilkan keterangan "Portofolio pilihan" dan rentang "2022 sampai 2026".

### FR-4 Tentang

- Judul "Teknologi itu penting. Rasa juga."
- Dua paragraf deskripsi pendekatan kerja.
- Detail "Sekarang: Terbuka untuk kolaborasi" dan "Fokus: Product design dan frontend".

### FR-5 Karya

- Menampilkan tiga karya dalam grid: Pasar Pagi, Ruang Dengar, Lintas Jalan.
- Setiap karya memiliki visual dekoratif, keterangan kategori/tahun, judul, deskripsi, dan tautan.
- Tautan karya membuka email ke `halo@fahdin.dev` dengan subjek sesuai nama proyek.
- Setiap tautan visual memiliki `aria-label` yang menjelaskan tujuannya.
- Grid dua kolom di desktop; satu kolom pada lebar <=540px.

### FR-6 Footer

- Ajakan "Ada ide yang ingin dirapikan? Kita mulai dari obrolan."
- Tautan email `halo@fahdin.dev`.
- Tautan Instagram dan LinkedIn yang dibuka di tab baru dengan `rel="noreferrer"`.
- Keterangan "Dirancang dan dirakit dengan tenang di Bandung." dan tahun hak cipta.

### FR-7 Animasi & Interaksi

- Reveal saat scroll untuk `.about__content`, `.projects__heading`, dan setiap `.project`, dijalankan sekali.
- Hover pada kartu visual mengangkat dan memiringkan kartu sedikit.
- Hover pada tautan navigasi mengubah warna menjadi `clay`.
- Semua animasi di atas tidak dijalankan saat reduced motion aktif.

## 8. Kebutuhan Non-Fungsional

### Responsif

- Layout harus tetap utuh pada sekitar 1280px, <=800px, <=540px, dan 320px.
- Tidak boleh ada konten terpotong atau scroll horizontal pada lebar 320px (README tugas 11).

### Aksesibilitas

- Struktur judul berurutan: `h1` di hero, `h2` per bagian, `h3` per judul karya.
- Semua tautan dapat dijangkau keyboard dan memiliki fokus yang terlihat.
- Elemen dekoratif ditandai `aria-hidden="true"`.
- Kontras teks perlu diperiksa terhadap latar (README tugas 10).

### Performa

- Halaman hanya memuat satu CSS, satu JS, dan tiga skrip CDN.
- Tidak ada aset gambar; visual karya dirender dengan CSS.
- Ketergantungan CDN menjadi risiko performa dan ketersediaan (README tugas 13).

### Gerakan

- `prefers-reduced-motion: reduce` mematikan animasi di JS dan menekan transisi/animasi di CSS.
- Loader tidak boleh mengunci halaman ketika animasi dinonaktifkan.

### Kompatibilitas

- Browser modern yang mendukung custom properties, unit `svh`, `:focus-visible`, dan `prefers-reduced-motion`.

## 9. Konten & Data

- Seluruh teks antarmuka berbahasa Indonesia.
- Konten berasal dari fasilitator. Jangan mengarang fakta, angka, tautan, atau detail proyek.
- Placeholder yang diketahui:
  - Email: `halo@fahdin.dev` (tugas 1 dan 9).
  - Instagram dan LinkedIn masih mengarah ke halaman utama platform (tugas 2).
  - Tahun footer `© 2025` (tugas 1).
- Data karya yang ada: Pasar Pagi (platform komunitas, 2024), Ruang Dengar (identitas & website, 2023), Lintas Jalan (eksplorasi digital, 2022).

## 10. Batasan & Asumsi

- Tidak ada proses build, package manager, test, atau CI.
- Verifikasi dilakukan manual di browser.
- Pengembangan bergantung pada koneksi internet karena CDN.
- Repo belum diinisialisasi sebagai repositori Git (belum ada `.git`).
- Satu sesi kontribusi mengerjakan satu tugas dan satu pull request.
- Perubahan dependency, konfigurasi, atau arah desain harus dibicarakan lebih dulu.

## 11. Backlog (dari README)

| # | Tugas | Fokus | Status |
|---|---|---|---|
| 1 | Lengkapi profil Fahdin (lokasi, deskripsi, email, tahun) | Konten | Belum |
| 2 | Perbarui tautan Instagram dan LinkedIn | Konten | Belum |
| 3 | Buat halaman detail proyek dan hubungkan dari halaman utama | Fitur | Belum |
| 4 | Ceritakan proses proyek tanpa mengarang angka | Konten | Belum |
| 5 | Buat visual proyek baru dengan keterangan jelas | Visual | Belum |
| 6 | Rapikan navigasi ponsel untuk sentuhan dan keyboard | UX | Belum |
| 7 | Tunjukkan bagian yang sedang dibaca | UX | Belum |
| 8 | Tambahkan pengalaman kerja/kolaborasi | Konten | Belum |
| 9 | Lengkapi informasi kontak dan pastikan email berfungsi | Konten | Belum |
| 10 | Periksa aksesibilitas (kontras, urutan judul, fokus, label) | Kualitas | Belum |
| 11 | Uji dan perbaiki tampilan pada 320px dan posisi mendatar | Kualitas | Belum |
| 12 | Tambahkan ikon situs dan metadata pratinjau tautan | Visual/SEO | Belum |
| 13 | Kurangi ketergantungan CDN untuk mempercepat muat | Performa | Belum |

## 12. Kriteria Penerimaan

### Umum

- [ ] Halaman terbuka tanpa error JavaScript di konsol.
- [ ] Loader hilang dan halaman dapat di-scroll.
- [ ] Navigasi anchor dan tautan email berfungsi.
- [ ] Layout diperiksa pada ~1280px, <=800px, <=540px, dan 320px.
- [ ] Reduced motion aktif: tidak ada animasi yang mengganggu dan halaman tetap dapat di-scroll.
- [ ] Tidak ada teks, tautan, atau angka yang dikarang.
- [ ] Salinan antarmuka tetap berbahasa Indonesia.

### Perubahan konten

- [ ] Data yang diubah sesuai bahan dari fasilitator.
- [ ] Email dan tautan sosial mengarah ke tujuan yang benar.
- [ ] Tidak ada placeholder yang tertinggal tanpa catatan.

### Perubahan visual/UX

- [ ] Komponen baru mengikuti penamaan BEM-like dan memakai custom properties.
- [ ] Warna yang diubah diperbarui di `index.html` dan `style.css`.
- [ ] Ikon panah yang diubah diperbarui di semua kemunculannya.
- [ ] Fokus keyboard tetap terlihat dan urutan judul tetap logis.

### Perubahan animasi

- [ ] Animasi tetap berjalan normal pada perangkat biasa.
- [ ] Animasi tidak dijalankan saat reduced motion aktif.
- [ ] Fallback `finishLoading()` tetap ada dan diuji.

## 13. Risiko & Mitigasi

| Risiko | Dampak | Mitigasi |
|---|---|---|
| CDN tidak tersedia atau diblokir | Halaman tanpa gaya/animasi, loader berisiko mengunci | Pertahankan fallback loader; pertimbangkan tugas 13 |
| Kesalahan JS sebelum loader selesai | Halaman tidak dapat di-scroll | Jaga urutan skrip dan fallback; uji konsol |
| Konten placeholder dianggap final | Informasi kontak salah | Tandai placeholder, selesaikan tugas 1, 2, 9 |
| Palet berubah hanya di satu tempat | Warna tidak konsisten | Perbarui `tailwind.config` dan `:root` bersamaan |
| SVG panah disalin di banyak tempat | Perubahan tidak merata | Cari semua kemunculan sebelum mengedit |
| Belum ada Git | Tidak ada riwayat/rollback | Ikuti `github-guide-global.md` saat memulai alur Git |
| Angka atau klaim karangan | Kredibilitas rusak | Minta bahan ke fasilitator; jangan mengisi sendiri |

## 14. Definisi Selesai

Sebuah tugas dianggap selesai jika:

- Satu tujuan tugas terpenuhi dan tidak mencampur tugas lain.
- Verifikasi manual lolos pada desktop dan ponsel, termasuk reduced motion bila relevan.
- Tidak ada dependency atau perubahan desain yang belum disepakati.
- Pull request mengikuti `github-guide-global.md`: Session Setup, satu PR per sesi, lalu berhenti.
- Deskripsi PR menjelaskan perilaku yang berubah dan cara mengujinya.

## 15. Referensi

- `README.md` — cara menjalankan, aturan kontribusi, daftar tugas.
- `AGENTS.md` — catatan teknis dan jebakan implementasi.
- `github-guide-global.md` — SOP Git dan standar pull request.
- `semantic-versioning-guide.md` — ringkasan SemVer.
- `index.html`, `css/style.css`, `js/script.js` — sumber kebenaran implementasi.
