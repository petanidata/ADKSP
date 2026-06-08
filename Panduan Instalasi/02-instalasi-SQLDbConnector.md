File panduan ini: `Panduan Instalasi/02-instalasi-SQLDbConnector.md`
## Simulasi langkah (dengan contoh gambar)
Berikut contoh urutan langkah yang bisa ditunjukkan dengan screenshot saat mengajar. Pada contoh caption saya sudah gunakan `nama-user` sebagai placeholder; jika screenshot yang Anda miliki masih menampilkan `muttaqin.zaenul`, Anda bisa mengganti teks pada gambar sebelum digunakan (instruksi singkat di bawah).
1) Buka Orange → tambahkan Widget `Python Script`. (Gambar 1)
2) Di editor widget, jalankan:

```
import sys
print(sys.executable)
```

3) Salin output yang muncul di konsol. Contoh output (tampilkan pada gambar dengan `nama-user`):

```
C:\Users\nama-user\AppData\Local\Programs\Orange\python.exe
```

4) Buka Command Prompt / PowerShell, lalu jalankan (contoh):

```powershell
"C:\Users\nama-user\AppData\Local\Programs\Orange\python.exe" -m pip install psycopg2-binary
```

5) Kembali ke Widget `Python Script`, uji import:

```
import psycopg2
print('psycopg2 OK')
```

Gambar yang sesuai:
- Gambar 1: Panel widget dan ikon `Python Script`.
- Gambar 2: Editor `Python Script` dengan kode `print(sys.executable)` dan hasil di Console.
- Gambar 3: Contoh perintah `pip install` di Command Prompt (gunakan path dari output di langkah 3).
- Gambar 4: Hasil tes import `psycopg2` di Console widget.

Instruksi singkat mengubah teks username pada screenshot (opsi manual)
- Windows Paint (cepat): buka gambar → gunakan tool `Rectangle` untuk menutupi teks lama → gunakan `Text` untuk menulis `nama-user` pada posisi yang sama → simpan.
- PowerPoint: sisipkan gambar → gunakan `Shapes` (rectangle) dengan warna latar yang cocok untuk menutupi username lama → tambah `Text Box` dengan `nama-user` → ekspor slide sebagai gambar.
- Editor gratis (GIMP / Photopea): gunakan `Clone` atau `Healing` untuk hapus teks lalu `Text` untuk tulis `nama-user`.

Jika Anda ingin saya mengganti teks pada screenshot secara langsung, unggah file gambar sumber (asli) di chat — saya akan menggantinya dan mengembalikan versi yang sudah diedit.

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
