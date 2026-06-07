# Preprocessing Data

## 1. Apa itu Preprocessing Data?

Preprocessing data adalah serangkaian **proses membersihkan dan menyiapkan data mentah** menjadi format yang siap dianalisis oleh algoritma Data Mining.

Dalam praktik nyata, data keuangan pemerintah daerah sering mengandung masalah:

| Masalah Umum       | Contoh dalam Data APBD                                |
|--------------------|-------------------------------------------------------|
| Nilai hilang       | Kolom Anggaran_APBD kosong / NaN                      |
| Nilai tidak wajar  | Anggaran_APBD bernilai negatif                        |
| Outlier            | Realisasi 200% dari anggaran                          |
| Duplikasi          | PEMDA yang sama muncul dua kali di tahun yang sama    |
| Inkonsistensi      | "Jawa Barat" vs "jawa barat" vs "JABAR"               |
| Tipe data salah    | Kolom angka tersimpan sebagai teks                    |

> **Fakta Industri:** Ilmuwan data menghabiskan **60–80% waktu** mereka untuk preprocessing data, bukan untuk membangun model.

---

## 2. Alur Kerja Preprocessing

```mermaid
flowchart TD
    A["📂 Raw Data\n(Data Mentah)"] --> B["🔍 Data Understanding\nPahami struktur, tipe & isi"]
    B --> C["🧹 Data Cleaning\nBersihkan data kotor"]
    C --> D["🔗 Data Integration\nGabungkan sumber data berbeda"]
    D --> E["🔄 Data Transformation\nUbah format & skala"]
    E --> F["✂️ Data Reduction\nKurangi dimensi/record tidak relevan"]
    F --> G["✅ Clean Data\nData Siap Analisis"]
    G --> H["🤖 Analisis / Modeling"]

    style A fill:#ff9999,stroke:#cc0000
    style G fill:#99ff99,stroke:#007700
    style H fill:#99ccff,stroke:#0055cc
```

---

## 3. Tahap 1: Data Understanding (Pemahaman Data)

Sebelum membersihkan data, **kenali datamu terlebih dahulu**.

```mermaid
mindmap
  root((Data Understanding))
    Dimensi
      Berapa baris?
      Berapa kolom?
    Tipe Data
      Numerik atau Kategorikal?
      Sudah sesuai?
    Statistik Deskriptif
      Min, Max
      Mean, Median
      Std Deviasi
    Nilai Unik
      Berapa nilai berbeda?
      Ada nilai aneh?
    Missing Values
      Kolom mana yang kosong?
      Berapa persen?
```

### Fungsi Python yang Digunakan

```python
import pandas as pd

df = pd.read_csv('keuangan_pemda.csv')

df.shape           # Dimensi: (baris, kolom)
df.dtypes          # Tipe data setiap kolom
df.info()          # Info lengkap + missing values
df.describe()      # Statistik deskriptif kolom numerik
df.head(5)         # 5 baris pertama
df.isnull().sum()  # Jumlah missing per kolom
df.nunique()       # Jumlah nilai unik per kolom
```

---

## 4. Tahap 2: Data Cleaning (Pembersihan Data)

### 4.1 Penanganan Missing Values (Nilai Hilang)

```mermaid
flowchart TD
    A["Deteksi Missing Values\ndf.isnull().sum()"] --> B{"Seberapa\nbanyak?"}
    B -- "< 5%" --> C["Hapus baris\ndropna()"]
    B -- "5–30%" --> D{"Tipe\ndata?"}
    B -- "> 30%" --> E["Pertimbangkan\nhapus kolom\ndrop(column)"]

    D -- Numerik --> F["Isi dengan\nMean atau Median\nfillna(median)"]
    D -- Kategorikal --> G["Isi dengan\nModus\nfillna(mode)"]
    D -- "Time Series" --> H["Forward/Backward Fill\nffill() atau bfill()"]

    style A fill:#fff3cd
    style E fill:#ff9999
    style F fill:#d4edda
    style G fill:#d4edda
    style H fill:#d4edda
```

**Contoh Kasus Data APBD:**

```
Sebelum:
┌──────────┬──────────────────┐
│Kode_Pemda│ Anggaran_APBD    │
├──────────┼──────────────────┤
│ PEMDA001 │ 2.350.000.000    │
│ PEMDA002 │ NaN              │  ← Missing!
│ PEMDA003 │ 1.390.000.000    │
└──────────┴──────────────────┘

Sesudah (diisi median):
┌──────────┬──────────────────────────────┐
│Kode_Pemda│ Anggaran_APBD                │
├──────────┼──────────────────────────────┤
│ PEMDA001 │ 2.350.000.000                │
│ PEMDA002 │ 1.870.000.000  ← nilai median│
│ PEMDA003 │ 1.390.000.000                │
└──────────┴──────────────────────────────┘
```

> **Mengapa median?** Karena data keuangan sering memiliki distribusi miring (skewed). Median lebih robust terhadap outlier dibanding mean.

---

### 4.2 Penanganan Outlier (Pencilan)

**Apa itu Outlier?** Nilai yang sangat jauh dari distribusi normal data.

```mermaid
graph TD
    A["Deteksi Outlier"] --> B["Z-Score\n|z| > 3\nz = (x-μ)/σ"]
    A --> C["IQR Method\n< Q1 - 1.5×IQR\n> Q3 + 1.5×IQR"]
    A --> D["Visualisasi\nBoxplot / Histogram"]

    B --> E{"Pilihan\nPenanganan"}
    C --> E
    D --> E

    E --> F["🗑️ Hapus record\njika error input"]
    E --> G["📏 Cap / Winsorize\nGanti dengan nilai batas"]
    E --> H["📐 Transformasi\nlog(), sqrt()"]
    E --> I["✅ Pertahankan\njika valid secara bisnis"]

    style F fill:#ff9999
    style G fill:#ffcc99
    style H fill:#99ccff
    style I fill:#99ff99
```

**Contoh — IQR Method pada Data APBD:**

```
Data Anggaran_APBD (Miliar Rp):
Q1 = 5.2 Miliar
Q3 = 18.7 Miliar
IQR = 13.5 Miliar

Batas bawah = 5.2 - (1.5 × 13.5) = -14.95 Miliar
Batas atas  = 18.7 + (1.5 × 13.5) = 38.95 Miliar

Outlier terdeteksi:
- PEMDA101: Anggaran = -10 Miliar  → negatif → kemungkinan error input
- PEMDA050: Anggaran = 500 Miliar  → sangat besar → perlu verifikasi
```

---

### 4.3 Penanganan Data Duplikat

```python
# Deteksi duplikat
print(df.duplicated().sum())

# Lihat baris duplikat
print(df[df.duplicated()])

# Hapus duplikat
df = df.drop_duplicates()

# Hapus duplikat berdasarkan kolom tertentu
df = df.drop_duplicates(subset=['Kode_Pemda', 'Tahun'])
```

---

### 4.4 Penanganan Inkonsistensi Nilai

```
Masalah Umum pada Data Pemerintah:
┌────────────────────┬───────────────────────────────────┐
│ Inkonsistensi      │ Contoh                            │
├────────────────────┼───────────────────────────────────┤
│ Kapitalisasi       │ "Jawa Barat" vs "jawa barat"      │
│ Singkatan          │ "Jawa Barat" vs "Jabar" vs "JaBar"│
│ Format angka       │ "1.000.000" vs "1000000"          │
│ Spasi ekstra       │ "Kurang " vs "Kurang"             │
│ Nilai tak bermakna │ "N/A", "-", ".", "#REF!"          │
└────────────────────┴───────────────────────────────────┘
```

```python
# Standarisasi teks
df['Provinsi'] = df['Provinsi'].str.strip().str.title()

# Ganti nilai tidak konsisten
df['Predikat'] = df['Predikat'].str.strip()
df['Predikat'] = df['Predikat'].replace({'sangat baik': 'Sangat Baik',
                                          'BAIK': 'Baik'})
```

---

## 5. Tahap 3: Data Transformation (Transformasi Data)

### 5.1 Normalisasi — Min-Max Scaling

Mengubah nilai ke rentang **[0, 1]**

$$X_{norm} = \frac{X - X_{min}}{X_{max} - X_{min}}$$

**Kapan digunakan?** Algoritma berbasis jarak: KNN, K-Means, Neural Network

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
df[['Anggaran_APBD', 'Realisasi_APBD']] = scaler.fit_transform(
    df[['Anggaran_APBD', 'Realisasi_APBD']]
)
```

---

### 5.2 Standardisasi — Z-Score

Mengubah distribusi ke **mean = 0, std = 1**

$$Z = \frac{X - \mu}{\sigma}$$

**Kapan digunakan?** Algoritma berbasis asumsi normal: regresi, SVM, PCA

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
df[['Anggaran_APBD', 'Realisasi_APBD']] = scaler.fit_transform(
    df[['Anggaran_APBD', 'Realisasi_APBD']]
)
```

---

### 5.3 Encoding Variabel Kategorikal

Algoritma Machine Learning **tidak bisa membaca teks** → harus diubah ke angka

| Metode              | Kapan Digunakan          | Contoh                                              |
|---------------------|--------------------------|-----------------------------------------------------|
| **Label Encoding**  | Data Ordinal             | Kurang=0, Cukup=1, Baik=2, Sangat Baik=3            |
| **One-Hot Encoding**| Data Nominal             | Provinsi → kolom terpisah (JaBar, JaTeng, dll.)     |
| **Binary Encoding** | Nominal + banyak kategori| Hemat memori dibanding One-Hot                      |

```python
# Label Encoding (untuk Ordinal)
from sklearn.preprocessing import LabelEncoder
le = LabelEncoder()
df['Predikat_Encoded'] = le.fit_transform(df['Predikat'])

# One-Hot Encoding (untuk Nominal)
df = pd.get_dummies(df, columns=['Provinsi'], prefix='Prov')
```

---

### 5.4 Feature Engineering

Membuat **fitur baru** dari fitur yang sudah ada untuk meningkatkan performa model.

```python
# Persen realisasi (fitur paling informatif!)
df['Pct_Realisasi'] = df['Realisasi_APBD'] / df['Anggaran_APBD'] * 100

# Rasio PAD terhadap total anggaran (kemandirian fiskal)
df['Rasio_Kemandirian'] = df['PAD'] / df['Anggaran_APBD'] * 100

# Selisih anggaran dan realisasi (sisa anggaran)
df['Sisa_Anggaran'] = df['Anggaran_APBD'] - df['Realisasi_APBD']
```

---

## 6. Tahap 4: Data Reduction (Reduksi Data)

```mermaid
graph TD
    A["Data Reduction"] --> B["Feature Selection\nPilih fitur relevan"]
    A --> C["Dimensionality Reduction\nPCA, LDA"]
    A --> D["Sampling\nAmbil subset representatif"]

    B --> E["Filter Methods\nKorelasi, Chi-Square"]
    B --> F["Wrapper Methods\nRFE — Recursive Feature Elimination"]
    B --> G["Embedded Methods\nLasso, Tree Feature Importance"]
```

---

## 7. Checklist Preprocessing

```
CHECKLIST PREPROCESSING DATA APBD
══════════════════════════════════════════════════════

✅ FASE 1 — DATA UNDERSTANDING
   □ df.shape → cek dimensi (baris × kolom)
   □ df.dtypes → cek tipe data setiap kolom
   □ df.describe() → statistik deskriptif
   □ df.isnull().sum() → deteksi missing values
   □ df.duplicated().sum() → deteksi duplikat

✅ FASE 2 — DATA CLEANING
   □ Tangani missing values (hapus/imputasi)
   □ Tangani outlier (hapus/cap/transform)
   □ Hapus baris duplikat
   □ Perbaiki inkonsistensi format/nilai
   □ Perbaiki tipe data yang salah

✅ FASE 3 — DATA TRANSFORMATION
   □ Encode variabel kategorikal
   □ Normalisasi/standardisasi nilai numerik
   □ Buat fitur baru jika relevan (feature engineering)

✅ FASE 4 — VALIDASI AKHIR
   □ Tidak ada missing values tersisa
   □ Semua tipe data sudah benar
   □ Range nilai masuk akal
   □ Distribusi data wajar
```

---

## 8. Dampak Jika Preprocessing Diabaikan

```mermaid
graph LR
    A["❌ Missing Values"] --> B["Error runtime\natau bias model"]
    C["❌ Outlier"] --> D["Mean terdistorsi\nModel tidak akurat"]
    E["❌ Skala berbeda"] --> F["Fitur besar mendominasi\nhasil analisis"]
    G["❌ Encoding salah"] --> H["Model tidak bisa\nbaca data kategorikal"]
    I["❌ Data duplikat"] --> J["Model overfitting\npada data tertentu"]

    style A fill:#ff9999
    style C fill:#ff9999
    style E fill:#ff9999
    style G fill:#ff9999
    style I fill:#ff9999
```

---

## 9. Studi Kasus: Dataset keuangan_pemda.csv

```
AUDIT DATA: keuangan_pemda.csv
═══════════════════════════════════════════════════════════════
MASALAH YANG DITEMUKAN:

┌─────────────────────────────────────────────────────────────┐
│ No │ Masalah               │ Kolom              │ Aksi      │
├────┼───────────────────────┼────────────────────┼───────────┤
│  1 │ Missing Values        │ Anggaran_APBD      │ Imputasi  │
│  2 │ Nilai Negatif         │ Anggaran_APBD      │ Verifikasi│
│  3 │ Outlier Ekstrem       │ Realisasi > 100%   │ Cap/hapus │
│  4 │ Inkonsistensi Predikat│ Predikat           │ Rekalk.   │
│  5 │ Data Duplikat (potens.)│ Kode_Pemda+Tahun  │ Deduplikasi│
└────┴───────────────────────┴────────────────────┴───────────┘

ATURAN BISNIS PREDIKAT:
  Sangat Baik  : Realisasi / Anggaran  > 90%
  Baik         : Realisasi / Anggaran 80%–90%
  Cukup        : Realisasi / Anggaran 60%–80%
  Kurang       : Realisasi / Anggaran  < 60%
═══════════════════════════════════════════════════════════════
```

---

## 10. Referensi

- Han, J., Kamber, M., & Pei, J. (2012). *Data Mining: Concepts and Techniques* (3rd ed.). Morgan Kaufmann.
- García, S., et al. (2015). *Data preprocessing in data mining*. Springer.
- McKinney, W. (2017). *Python for Data Analysis* (2nd ed.). O'Reilly Media.

---

*Materi: Analitika Data Keuangan Sektor Publik | Program DIV*
