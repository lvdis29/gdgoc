# Hands-On Module 2 — MPG Fuel Efficiency Analysis

Analisis dataset **MPG (fuel efficiency mobil)** buat Hands-On Task Module 2 (Mathematical Foundation & Data Visualization for AI) — GDGoC ITB Career Path Program.

**Nama:** Eka Suci Ramadhani
**NIM:** 18225063

## Deskripsi

Notebook ini nerapin konsep linear algebra, statistik, EDA, dan visualisasi data ke dataset MPG dari seaborn, buat nyari tau faktor-faktor apa aja yang paling ngaruh ke efisiensi bahan bakar mobil (mpg). Semua perhitungan statistik dasar (mean, median, std, IQR, korelasi, standardisasi) dikerjakan manual pakai NumPy, tanpa pakai `pandas.describe()` atau `sklearn`.

## Dataset

MPG dataset bawaan seaborn — 398 baris data mobil dengan 9 kolom (mpg, cylinders, displacement, horsepower, weight, acceleration, model_year, origin, name).

```python
import seaborn as sns
df = sns.load_dataset('mpg')
```

## Isi Repo

```
├── mpg_eda_module2.ipynb   # notebook utama (Stage 1-4)
├── evidence.docx           # dokumen evidence (proses eksplorasi & temuan)
└── README.md
```

## Cara Menjalankan

1. Clone / download repo ini.
2. Install dependency yang dibutuhkan:
   ```bash
   pip install numpy pandas matplotlib seaborn jupyter
   ```
3. Buka notebook-nya:
   ```bash
   jupyter notebook mpg_eda_module2.ipynb
   ```
4. Run all cell dari atas ke bawah (`Kernel > Restart & Run All`). Notebook udah didesain buat jalan top-to-bottom tanpa error, dataset otomatis ke-load dari seaborn jadi gak perlu download file terpisah.

## Struktur Notebook

| Stage | Isi |
|---|---|
| **Stage 1** | Inspection & data cleaning — cek shape/dtype/missing value, drop baris kosong di horsepower, summary table manual (mean, median, std, IQR, outlier count) pakai NumPy |
| **Stage 2** | Statistical analysis — z-score standardisasi vectorized, correlation matrix, analisis multikolinearitas, boolean masking horsepower vs weight |
| **Stage 3** | Visualisasi — histogram+KDE distribusi mpg, boxplot mpg per origin, scatter weight vs mpg + trend line, correlation heatmap |
| **Stage 4** | Interpretasi kontekstual — faktor terkuat yang memprediksi mpg, tren rata-rata mpg per dekade |

## Ringkasan Temuan Utama

- Distribusi mpg **right-skewed** (mean > median), bukan simetris.
- Mobil **Japan** paling fuel-efficient, **USA** paling boros.
- **Weight** adalah prediktor terkuat terhadap mpg (r ≈ -0.83), diikuti displacement dan horsepower.
- Ada **multikolinearitas** kuat antara displacement, horsepower, dan weight (semua saling berkorelasi > 0.8).
- Rata-rata mpg naik terus dari dekade 1970 ke 1980-an, kemungkinan besar karena krisis minyak dan regulasi efisiensi bahan bakar.

## Referensi

- [Essence of Linear Algebra — 3Blue1Brown](https://www.3blue1brown.com/topics/linear-algebra)
- [NumPy Linear Algebra Documentation](https://numpy.org/doc/stable/reference/routines.linalg.html)
- [Seaborn Tutorial](https://seaborn.pydata.org/tutorial.html)
- [Matplotlib Tutorials](https://matplotlib.org/stable/tutorials/index.html)
- [Seaborn MPG Dataset](https://github.com/mwaskom/seaborn-data)
