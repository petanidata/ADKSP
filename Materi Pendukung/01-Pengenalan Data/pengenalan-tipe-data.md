# Pengenalan & Tipe Data dalam Data Mining

## 1. Mengapa Tipe Data Penting?

Memahami tipe data adalah **fondasi utama** dalam analitika data. Pemilihan metode analisis, visualisasi, dan preprocessing sangat bergantung pada jenis data yang kita miliki.

> **Analogi:** Seperti memilih alat masak — panci untuk merebus, wajan untuk menggoreng. Salah memilih alat → hasil tidak optimal. Begitu pula dalam analisis data: salah memahami tipe data → analisis yang misleading.

---

## 2. Klasifikasi Tipe Data

Tipe data dibagi menjadi dua kelompok utama. Untuk data **Numerik**, terdapat tambahan pembagian berdasarkan **Skala Pengukuran**.

### 2.1 Tipe Data

```mermaid
flowchart TD
    TD(["Tipe Data"])
    TD --> KAT["Kategorikal\nData berupa kategori/label"]
    TD --> NUM["Numerik\nData berupa angka yang dapat\ndihitung atau diukur"]

    KAT --> NOM["Nominal\nTidak memiliki urutan\nContoh: Jenis Kelamin | Provinsi | Agama"]
    KAT --> ORD["Ordinal\nMemiliki urutan/peringkat\nContoh: Predikat Kinerja | Tingkat Pendidikan | Ranking"]

    NUM --> DIS["Diskrit\nHasil perhitungan (count),\numumnya bilangan bulat\nContoh: Jumlah Pegawai | Jumlah SKPD | Jumlah Program"]
    NUM --> KON["Kontinu\nHasil pengukuran (measurement),\ndapat bernilai pecahan\nContoh: Anggaran APBD | Pendapatan | Berat Badan"]

    style KAT fill:#ffe0b2,stroke:#e65100
    style NUM fill:#e3f2fd,stroke:#1565c0
    style NOM fill:#fff9c4,stroke:#f57f17
    style ORD fill:#fff9c4,stroke:#f57f17
    style DIS fill:#e1f5fe,stroke:#01579b
    style KON fill:#e1f5fe,stroke:#01579b
```

### 2.2 Skala Pengukuran Numerik

Khusus untuk data **Numerik**, terdapat dua skala pengukuran yang menentukan makna nilai nol dan jenis operasi yang valid:

```mermaid
flowchart TD
    SPN(["Skala Pengukuran Numerik"])

    SPN --> INT["Interval\nNol relatif (0 ≠ tidak ada)\nSelisih bermakna\nContoh: Tahun Lahir | Suhu Celsius | Suhu Fahrenheit"]
    SPN --> RAS["Rasio\nNol absolut (0 = tidak ada)\nSelisih dan perbandingan bermakna\nContoh: Jumlah Pegawai | Anggaran APBD | Berat Badan"]

    style SPN fill:#f3e5f5,stroke:#6a1b9a
    style INT fill:#e3f2fd,stroke:#1565c0
    style RAS fill:#e8f5e9,stroke:#1b5e20
```

---

## 3. Penjelasan Detail & Contoh dalam Konteks APBD

### 3.1 Data Kategorikal — Nominal

- **Definisi:** Kategori **tanpa urutan** atau peringkat
- **Operasi valid:** Hanya bisa dibandingkan sama (=) atau tidak sama (≠)
- **Representasi:** Kode, nama, label

| Kode_Pemda | Provinsi      | Jenis_Pemda |
|------------|---------------|-------------|
| PEMDA001   | Jawa Barat    | Kabupaten   |
| PEMDA002   | Jawa Tengah   | Kota        |
| PEMDA003   | Banten        | Provinsi    |
| PEMDA004   | Jawa Barat    | Kota        |

> ⚠️ Tidak ada urutan antara "Kabupaten", "Kota", dan "Provinsi" — ketiganya setara sebagai kategori

---

### 3.2 Data Kategorikal — Ordinal

- **Definisi:** Kategori **dengan urutan/peringkat** yang bermakna
- **Operasi valid:** Bisa dibandingkan lebih besar/kecil, tapi **jarak antar nilai tidak pasti sama**
- **Representasi:** Label bertingkat

| Kode_Pemda | Predikat_Kinerja | Skor Urutan |
|------------|------------------|-------------|
| PEMDA001   | Kurang           | 1           |
| PEMDA002   | Cukup            | 2           |
| PEMDA003   | Baik             | 3           |
| PEMDA004   | Sangat Baik      | 4           |

> ⚠️ "Baik" > "Cukup" > "Kurang" ✓, tapi **selisih** antara level tidak tentu sama — tidak bisa langsung dijumlah atau dirata-rata

---

### 3.3 Data Numerik — Diskrit

- **Definisi:** Nilai **bilangan bulat**, tidak ada nilai pecahan di antara dua nilai berurutan
- **Operasi valid:** Semua operasi aritmetika (tapi hanya nilai bulat)

| Kode_Pemda | Jumlah_SKPD | Jumlah_Program | Jumlah_ASN |
|------------|-------------|----------------|------------|
| PEMDA001   | 32          | 145            | 5.420      |
| PEMDA002   | 28          | 112            | 3.890      |
| PEMDA003   | 41          | 203            | 7.215      |

> ⚠️ Tidak ada "32,5 SKPD" atau "112,7 program" — nilainya selalu bulat

---

### 3.4 Data Numerik — Kontinu

- **Definisi:** Nilai **dapat berupa pecahan**, hasil pengukuran (measurement)
- **Operasi valid:** Semua operasi aritmetika, termasuk nilai desimal
- **Catatan:** Data kontinu diukur dengan **Skala Interval** atau **Skala Rasio** (lihat Bagian 4)

| Kode_Pemda | Anggaran_APBD   | Realisasi_APBD  | % Realisasi |
|------------|-----------------|-----------------|-------------|
| PEMDA001   | 2.350.000.000   | 2.112.500.000   | 89,89%      |
| PEMDA002   | 1.870.000.000   | 1.289.300.000   | 68,95%      |
| PEMDA003   | 950.000.000     | 190.000.000     | 20,00%      |

> ✅ Anggaran APBD dan Realisasi APBD adalah data Kontinu berskala **Rasio** (nol = benar-benar tidak ada anggaran)

---

## 4. Skala Pengukuran Numerik

Untuk data numerik (baik Diskrit maupun Kontinu), terdapat dua skala pengukuran yang menentukan makna nilai nol dan operasi yang diperbolehkan.

### 4.1 Skala Interval

- **Nol bersifat relatif:** nilai 0 adalah titik referensi, bukan berarti "tidak ada"
- **Selisih bermakna:** jarak antar nilai dapat dibandingkan
- **Perbandingan (kali lipat) TIDAK bermakna**

> Contoh: Suhu 0°C bukan berarti "tidak ada suhu". Suhu 20°C tidak bisa dikatakan "2× lebih panas" dari 10°C.

| Contoh Data     | Keterangan                          |
|-----------------|-------------------------------------|
| Tahun Lahir     | Tahun 0 bukan "tidak ada tahun"     |
| Suhu Celsius    | 0°C bukan "tidak ada suhu"          |
| Suhu Fahrenheit | 0°F bukan "tidak ada suhu"          |

### 4.2 Skala Rasio

- **Nol bersifat absolut:** nilai 0 berarti benar-benar "tidak ada"
- **Selisih bermakna:** jarak antar nilai dapat dibandingkan
- **Perbandingan (kali lipat) BERMAKNA**

> Contoh: Anggaran Rp 0 berarti benar-benar tidak ada anggaran. Anggaran Rp 2 M = 2 kali lipat Anggaran Rp 1 M ✓

| Contoh Data     | Keterangan                                    |
|-----------------|-----------------------------------------------|
| Jumlah Pegawai  | 0 pegawai = benar-benar tidak ada pegawai     |
| Anggaran APBD   | Rp 0 = benar-benar tidak ada anggaran         |
| Berat Badan     | 0 kg = benar-benar tidak ada berat            |

### 4.3 Perbandingan Skala Pengukuran Numerik

| Skala        | Nol      | Selisih Bermakna | Perbandingan Bermakna | Contoh dalam APBD         |
|--------------|:--------:|:----------------:|:---------------------:|---------------------------|
| **Interval** | Relatif  | ✓                | ✗                     | Tahun Lahir, Skor Indeks  |
| **Rasio**    | Absolut  | ✓                | ✓                     | Anggaran, Realisasi, PAD  |

---

## 5. Diagram Alir Identifikasi Tipe Data

```mermaid
flowchart TD
    A(["Data / Kolom"])
    A --> B{"Berupa angka?"}
    B -- Tidak --> C["KATEGORIKAL"]
    B -- Ya --> D["NUMERIK"]

    C --> E{"Ada urutan bermakna?"}
    E -- Tidak --> F["Nominal\nContoh: Kode_Pemda, Provinsi,\nJenis Kelamin, Agama"]
    E -- Ya --> G["Ordinal\nContoh: Predikat Kinerja,\nTingkat Pendidikan, Ranking"]

    D --> H{"Hanya nilai bulat\nhasil perhitungan?"}
    H -- Ya --> I["Diskrit\nContoh: Jumlah SKPD,\nJumlah ASN, Jumlah Program"]
    H -- Tidak --> J["Kontinu\nContoh: Anggaran APBD,\nPendapatan, Berat Badan"]

    I --> K{"Nol = tidak ada?"}
    J --> K

    K -- Tidak --> L["Skala Interval\nContoh: Tahun Lahir,\nSuhu Celsius, Suhu Fahrenheit"]
    K -- Ya --> M["Skala Rasio\nContoh: Jumlah Pegawai, Anggaran,\nRealisasi, PAD, Berat Badan"]

    style F fill:#fff9c4,stroke:#f57f17
    style G fill:#fff9c4,stroke:#f57f17
    style I fill:#e1f5fe,stroke:#01579b
    style J fill:#e1f5fe,stroke:#01579b
    style L fill:#e3f2fd,stroke:#1565c0
    style M fill:#e8f5e9,stroke:#1b5e20
```

> ℹ️ **Skala Interval** dan **Skala Rasio** adalah **Skala Pengukuran Numerik** — berlaku untuk data Diskrit maupun Kontinu.

---

## 6. Konsep Feature / Atribut / Dimensi

Dalam **Data Mining**, setiap **kolom** dalam dataset disebut **feature**, **atribut**, atau **dimensi**.

```mermaid
graph LR
    DS[("📁 Dataset\nkeuangan_pemda.csv\n103 baris × 12 kolom")] --> F1["Feature 1\nKode_Pemda\n(Nominal)"]
    DS --> F2["Feature 2\nTahun\n(Diskrit)"]
    DS --> F3["Feature 3\nAnggaran_APBD\n(Kontinu - Rasio)"]
    DS --> F4["Feature 4\nRealisasi_APBD\n(Kontinu - Rasio)"]
    DS --> F5["Feature 5\nPAD\n(Kontinu - Rasio)"]
    DS --> FN["... (7 kolom lagi)"]
    DS --> TG["🎯 TARGET\nPredikat\n(Ordinal)"]

    style TG fill:#ff6666,stroke:#cc0000,color:#fff
    style DS fill:#4a90d9,stroke:#2255aa,color:#fff
```

| Istilah             | Makna                                      | Contoh dalam APBD                        |
|---------------------|--------------------------------------------|------------------------------------------|
| **Feature / Atribut** | Variabel/karakteristik input             | `Anggaran_APBD`, `Realisasi_APBD`, `PAD` |
| **Dimensi**         | Jumlah total feature dalam dataset         | 11 feature = 11 dimensi                  |
| **Instance / Record** | Satu baris data (satu pengamatan)        | Data PEMDA001 tahun 2024                 |
| **Dataset**         | Kumpulan seluruh instance & feature        | `keuangan_pemda.csv` (103+ baris)        |

### Jenis Feature

```mermaid
mindmap
  root((Feature))
    Input Features
      Independen
      Prediktor
      Variabel X
      Cth: Anggaran, PAD
    Target Feature
      Dependen
      Label / Class
      Variabel Y
      Cth: Predikat
```

---

## 7. Konsep Class / Label / Target

**Class / Label / Target** adalah **output yang ingin diprediksi** oleh model Data Mining.

### Ilustrasi Alur Prediksi

```
╔═══════════════════════════════╗       ╔═════════════╗       ╔══════════════════╗
║     INPUT (Features)          ║       ║             ║       ║  OUTPUT (Target) ║
║                               ║       ║   MODEL     ║       ║                  ║
║  Anggaran_APBD  = 5,2 M       ║  ──►  ║     AI      ║  ──►  ║  "Sangat Baik"   ║
║  Realisasi_APBD = 4,8 M       ║       ║   Klasifi-  ║       ║                  ║
║  PAD            = 1,2 M       ║       ║   kasi      ║       ║                  ║
║  Dana_Transfer  = 3,1 M       ║       ║             ║       ║                  ║
╚═══════════════════════════════╝       ╚═════════════╝       ╚══════════════════╝
```

| Konsep          | Definisi                                        | Contoh APBD                              |
|-----------------|-------------------------------------------------|------------------------------------------|
| **Class/Label** | Nilai yang diprediksi (kategorikal)             | Predikat: "Baik", "Kurang"               |
| **Target**      | Kolom tujuan prediksi                           | Kolom `Predikat`                         |
| **Ground Truth**| Label yang sudah diketahui (data latih)         | Predikat yang dihitung manual            |
| **Prediction**  | Output model untuk data baru                    | Predikat untuk PEMDA baru tahun depan    |

### Tugas dalam Data Mining Berdasarkan Target

| Jenis Tugas       | Target                | Contoh dalam APBD                         |
|-------------------|-----------------------|-------------------------------------------|
| **Klasifikasi**   | Kategorikal (class)   | Prediksi Predikat Kinerja (Baik/Kurang)   |
| **Regresi**       | Numerik (kontinu)     | Estimasi nilai Realisasi APBD tahun depan |
| **Clustering**    | Tidak ada (unsupervised) | Pengelompokan PEMDA berdasarkan profil |
| **Association**   | Tidak ada             | Pola hubungan antar komponen anggaran     |

---

## 8. Visualisasi Lengkap Dataset APBD

```
keuangan_pemda.csv — Peta Tipe Data

┌──────────┬──────┬──────────────┬──────────────┬──────────┬──────────────┬──────────┐
│Kode_Pemda│Tahun │Anggaran_APBD │Realisasi_APBD│    PAD   │Dana_Transfer │ Predikat │
│ Nominal  │Disk. │  Kontinu     │  Kontinu     │ Kontinu  │  Kontinu     │ Ordinal  │
│          │      │  (Rasio)     │  (Rasio)     │ (Rasio)  │  (Rasio)     │          │
├──────────┼──────┼──────────────┼──────────────┼──────────┼──────────────┼──────────┤
│ PEMDA001 │ 2024 │2.350.000.000 │2.112.500.000 │450000000 │ 1.800.000.000│  Baik    │
│ PEMDA002 │ 2024 │1.870.000.000 │1.289.300.000 │  NaN  ←──┤ 1.200.000.000│  Cukup   │ ← Missing
│ PEMDA003 │ 2024 │    NaN    ←──┤  900.000.000 │120000000 │   500.000.000│   ?      │ ← Missing
│ PEMDA101 │ 2024 │-10.000.000.000←  1.000.000.000│300000000│  700.000.000│  Kurang  │ ← Negatif
└──────────┴──────┴──────────────┴──────────────┴──────────┴──────────────┴──────────┘
                                    ↑                ↑
                              Tipe: Rasio      Ada Missing Value!
                              (Nol = tidak ada anggaran)
```

---

## 9. Ringkasan

### Tipe Data

| Tipe Data    | Kelompok     | Contoh Kolom APBD          | Operasi yang Valid          |
|--------------|:------------:|----------------------------|-----------------------------|
| **Nominal**  | Kategorikal  | Kode_Pemda, Provinsi       | = , ≠                       |
| **Ordinal**  | Kategorikal  | Predikat_Kinerja           | = , ≠ , < , >               |
| **Diskrit**  | Numerik      | Tahun, Jumlah_SKPD         | +, −, ×, ÷ (nilai bulat)    |
| **Kontinu**  | Numerik      | Anggaran, Realisasi, PAD   | +, −, ×, ÷                  |

### Skala Pengukuran Numerik

| Skala        | Nol      | Selisih Bermakna | Perbandingan Bermakna | Contoh                      |
|--------------|:--------:|:----------------:|:---------------------:|-----------------------------|
| **Interval** | Relatif  | ✓                | ✗                     | Tahun Lahir, Suhu Celsius   |
| **Rasio**    | Absolut  | ✓                | ✓                     | Anggaran, Realisasi, PAD    |

---

## 10. Referensi

- Han, J., Kamber, M., & Pei, J. (2012). *Data Mining: Concepts and Techniques* (3rd ed.). Morgan Kaufmann.
- Fayyad, U. et al. (1996). *From Data Mining to Knowledge Discovery in Databases*. AAAI Press.
- Stevens, S. S. (1946). On the theory of scales of measurement. *Science*, 103(2684), 677–680.

---

*Materi: Analitika Data Keuangan Sektor Publik | Program DIV*
