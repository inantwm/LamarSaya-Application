# LamarSaya — Android (Jetpack Compose)

Starter project aplikasi LamarSaya untuk dibuka di **Android Studio**. Isinya meniru
persis aplikasi web LamarSaya: 3 tab (Buat Surat, Kirim Email, Pengaturan), Preview
2 tab, Generate PDF beneran, dan Kirim Email via intent.

## Cara membuka
1. Ekstrak zip ini.
2. Android Studio → **Open** → pilih folder `lamarsaya-android`.
3. Tunggu Gradle Sync selesai (butuh internet untuk unduh dependency pertama kali).
   Jika diminta membuat Gradle Wrapper, klik setuju / jalankan `gradle wrapper` sekali.
4. Run ▶ ke emulator / HP (min. Android 7.0 / API 24).

## Yang sudah jadi
- **Ikon aplikasi**: logo resmi LamarSaya (glif LS putih di atas biru #1668DC, varian
  reversed dari logo final) — adaptive icon (mipmap-anydpi-v26, background warna brand +
  foreground glif) + PNG legacy & round semua densitas (mdpi–xxxhdpi). File
  `icon-512.png` di root project untuk Play Store.
- **Navbar** biru #1668DC: logo resmi LamarSaya (file `res/drawable-nodpi/logo_lamarsaya.png`,
  simbol LS dari logo final) + nama aplikasi, tombol bulat Preview (ikon mata).
- **Navigasi bawah wave** persis desain final: awal dibuka = Datar; ketuk Buat Surat =
  Wave Kiri (puncak di kiri, FAB Buat Surat); Kirim Email = Lembah (FAB email di cekungan);
  Pengaturan = Miring (puncak kanan, FAB gear). Animasi morfosis ±350ms.
- **Buat Surat**: form lengkap (Data Pelamar, Surat, Lampiran, Opsi PDF), 4 template surat,
  unggah tanda tangan (PNG), tombol **Generate PDF** full width → PDF A4 tersimpan di
  folder Download aplikasi + bisa dibagikan (FileProvider).
- **Kirim Email**: 5 template, subjek otomatis, body formal; **Salin Email** ke clipboard,
  **Kirim Email** membuka aplikasi email (Intent ACTION_SENDTO mailto).
- **Berkas Pendukung** (di bagian Lampiran, tab Buat Surat): pilih sekali file PDF
  gabungan berkas (CV, KTP, ijazah, dll.) — tersimpan permanen (DataStore + izin URI
  persisten); bila belum dipilih hanya tampil teks "Berkas pendukung belum dipilih."
  Bila berkas terpilih, **Generate PDF** menghasilkan **satu PDF gabungan** (halaman
  surat vektor + seluruh halaman berkas yang DISALIN LOSSLESS via PDFBox — sama seperti pdf-lib di website, ukuran file tetap normal; fallback render PdfRenderer), dan tombol
  **Kirim Email** melampirkan file gabungan yang sama (ACTION_SEND + FileProvider).
  Tanpa berkas terpilih, kirim tetap mailto polos tanpa lampiran.
- **Preview**: dialog layar penuh 2 tab (Surat Lamaran gaya A4 serif + Body Email),
  live mengikuti form.
- **Pengaturan**: pilihan **Tema 3 mode** (Ikuti Sistem / Terang / Gelap, tersimpan),
  toggle dialog simpan (CreateDocument vs simpan langsung),
  Reset Data, Hapus Semua Data (modal konfirmasi), versi 1.0.0.
- Data form tersimpan otomatis (DataStore) di perangkat pengguna. Nilai awal form
  SENGAJA kosong (versi publik) — tidak ada data pribadi siapa pun di dalam aplikasi;
  tanggal surat otomatis terisi hari ini.

## Catatan
- Project ini disusun sebagai starter yang lengkap dan mengikuti struktur standar
  Android Studio, tetapi **belum dikompilasi di mesin pembuatnya** (tidak ada Android SDK
  di sana). Jika Android Studio menandai error kecil, biasanya seputar versi dependency —
  sesuaikan versi di `app/build.gradle.kts` bila perlu.
- Template surat selain "Formal & Umum" adalah variasi redaksi; sesuaikan teks persisnya
  di `util/Templates.kt` bila perlu sama persis dengan website.
