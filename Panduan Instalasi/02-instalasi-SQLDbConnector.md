# Panduan Instalasi Connector PostgreSQL untuk Orange

Panduan ini menjelaskan langkah singkat memasang PostgreSQL connector (`psycopg2-binary`) sehingga dapat digunakan oleh widget SQL di Orange. Panduan ditujukan untuk instalasi Orange standalone (Windows / macOS).

## Prasyarat
- Orange sudah terpasang dan dapat dijalankan.
- Koneksi internet untuk mengunduh paket Python.
- Hak akses untuk menjalankan `pip` pada interpreter Orange (jalankan terminal sebagai Administrator jika perlu).

## Langkah 1 — Cek interpreter Python yang dipakai Orange
1. Buka Orange, tambahkan dan buka Widget `Python Script`.
2. Jalankan kode berikut di widget:

```
import sys
print(sys.executable)
```

3. Catat path yang ditampilkan. Contoh:
- Windows: `C:\Users\<nama-user>\AppData\Local\Programs\Orange\python.exe`
- macOS: `/Applications/Orange.app/Contents/MacOS/python` atau `/Users/<nama-user>/Library/Application Support/Orange/python/bin/python3`

> Semua perintah `pip install` harus dijalankan terhadap interpreter ini.

## Langkah 2 — Pasang `psycopg2-binary`
Jalankan perintah `pip install` dengan memanggil modul `pip` via interpreter dari Langkah 1.

Contoh Windows (ganti `<path_python_orange>` sesuai hasil Langkah 1):

```powershell
"<path_python_orange>" -m pip install psycopg2-binary
```

Contoh macOS:

```bash
<path_python_orange> -m pip install psycopg2-binary
```

Catatan: `psycopg2-binary` direkomendasikan untuk lingkungan pembelajaran karena mudah dipasang.

## Langkah 3 — Verifikasi pemasangan
- Cek paket terpasang dari terminal:

```bash
"<path_python_orange>" -m pip show psycopg2-binary
```

- Atau uji dari Widget `Python Script` di Orange:

```
import psycopg2
print('psycopg2 OK')
```

## Troubleshooting singkat
- Error "pg_config not found" atau error compile:
  - macOS: jalankan `xcode-select --install` lalu ulangi pemasangan.
  - Linux: pasang `libpq-dev` dan `python3-dev` (tidak umum untuk instalasi standalone Orange).
- Jika pemasangan tidak terlihat di Orange, pastikan Anda memanggil `pip` pada path `sys.executable` yang benar.
