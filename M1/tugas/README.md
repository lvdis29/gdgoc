# Hands-On Module 1 — Exploratory Data Analysis Spotify Songs Dataset

**Nama** : Eka Suci Ramadhani
**NIM** : 18225063
**Program** : GDGoC ITB — Career Path Program
**Modul** : Module 1 — Intro to AI and Python Ecosystem

## Deskripsi

Repo ini berisi pengerjaan tugas hands-on Module 1: melakukan exploratory data analysis (EDA) lengkap pada [Spotify Songs Dataset (TidyTuesday 2020)](https://github.com/rfordatascience/tidytuesday/blob/main/data/2020/2020-01-21/readme.md) menggunakan Pandas dan NumPy.

## Isi Repo

| File | Deskripsi |
|---|---|
| `spotify_eda.ipynb` | Notebook utama — seluruh proses EDA, sudah dieksekusi (kode, output, dan narasi markdown) |
| `README.md` | Dokumen ini |

## Cara Menjalankan

```bash
pip install pandas numpy jupyter
jupyter notebook spotify_eda.ipynb
```

Notebook mengambil dataset langsung dari URL TidyTuesday, jadi tidak perlu download file terpisah — cukup jalankan semua cell dari atas ke bawah.

## Cerita Proses & Eksplorasi

Awalnya aku sempat bingung mau mulai dari mana karena datasetnya lumayan besar (32 ribuan baris, 23 kolom), jadi langkah pertama yang aku lakukan adalah `df.info()` dan `df.describe()` dulu buat "kenalan" sama datanya sebelum masuk ke pertanyaan-pertanyaan analitis di instruksi tugas. Dari situ aku baru sadar ada tiga kolom dengan sedikit missing value (`track_name`, `track_artist`, `track_album_name`), tapi untungnya jumlahnya kecil banget (cuma 5 baris) jadi nggak perlu drop kolom.

Bagian yang paling bikin aku mikir agak lama justru bukan di kode-nya, tapi di keputusan strategi deduplikasi. Awalnya aku sempat coba `df.drop_duplicates()` biasa (tanpa subset), tapi ternyata jumlah baris yang kehapus sedikit banget — setelah aku cek lebih teliti, ternyata itu karena satu lagu bisa muncul di banyak baris dengan `playlist_id` yang berbeda (satu lagu ada di beberapa playlist). Jadi aku ganti strateginya jadi dedup berdasarkan `track_id`, karena itu identifier resmi satu rekaman di Spotify — biar statistik audio-feature nggak "dobel hitung" untuk lagu yang kebetulan masuk banyak playlist.

Waktu masuk ke bagian NumPy (normalisasi min-max dan matriks korelasi), sempat ada momen "aha" buat aku: awalnya aku kira harus loop manual per kolom buat normalisasi, tapi ternyata broadcasting NumPy bisa langsung `(X - X.min(axis=0)) / (X.max(axis=0) - X.min(axis=0))` dalam satu baris tanpa loop sama sekali. Ini juga yang bikin aku akhirnya baca-baca lagi dokumentasi broadcasting NumPy biar paham kenapa itu bisa jalan padahal shape `X` dan `X.min(axis=0)` beda.

Untuk bagian dokumentasi, aku coba pakai AI coding tool buat generate docstring, dan ternyata hasilnya nggak langsung sempurna — ada parameter yang kelewat di salah satu fungsi (`feature_cols` di `artist_fingerprint`), jadi aku harus baca ulang manual dan benerin sendiri. Ini jadi pengingat buat aku pribadi bahwa AI itu mempercepat proses nulis draft, tapi tetap harus dicek lagi teliti-teliti, apalagi kalau menyangkut detail teknis kayak signature fungsi.

Secara keseluruhan, proses ini ngebantu aku lebih paham bedanya "sekadar manggil fungsi library" dengan "benar-benar ngerti apa yang terjadi di balik layar" — terutama pas harus implementasi IQR dari rumus matematikanya langsung tanpa scipy.

## Ringkasan Temuan Utama

1. Genre **pop** punya sebaran popularitas paling lebar (variansi tertinggi di antara 6 genre) — artinya label genre saja tidak cukup untuk menebak apakah pendengar akan menyukai sebuah lagu pop.
2. Jumlah lagu yang banyak tidak menjamin rata-rata popularitas tinggi — korelasi antara volume rilis dan rata-rata popularitas di antara 10 artis paling produktif sangat lemah (0.23).
3. Fitur `energy` berkorelasi kuat positif dengan `loudness` (0.68) dan kuat negatif dengan `acousticness` (-0.55), konsisten dengan intuisi musikal.

## Referensi

1. [TidyTuesday — Spotify Songs Dataset (data dictionary resmi)](https://github.com/rfordatascience/tidytuesday/blob/main/data/2020/2020-01-21/readme.md)
2. [NumPy User Guide — Broadcasting](https://numpy.org/doc/stable/user/basics.broadcasting.html)
3. [NumPy Documentation](https://numpy.org/doc/stable/user/)
4. [Pandas User Guide — Group by: split-apply-combine](https://pandas.pydata.org/docs/user_guide/groupby.html)
5. [Pandas User Guide — Working with missing data](https://pandas.pydata.org/docs/user_guide/missing_data.html)
6. [Google AI — Responsible AI Practices](https://ai.google/responsibility/responsible-ai-practices/)
7. [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
8. [Gemini Code Assist Overview](https://cloud.google.com/gemini/docs/codeassist/overview)
9. Handbook Module 1 & Hands-On Module 1 — GDGoC ITB Curriculum Team (materi kelas)
