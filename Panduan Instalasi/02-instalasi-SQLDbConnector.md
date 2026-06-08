# Panduan singkat: Pasang PostgreSQL connector untuk Orange (psycopg2-binary)

Tujuan singkat: pastikan paket `psycopg2-binary` dipasang ke interpreter Python yang dipakai Orange (bukan ke Python sistem lain).

Langkah 1 — Cek interpreter Orange (di Windows/macOS)
- Buka Widget `Python Script` di Orange dan jalankan:

```
import sys
print(sys.executable)
```

- Catat path yang muncul (contoh Windows: `C:\Users\<nama-user>\AppData\Local\Programs\Orange\python.exe`; macOS: `/Applications/Orange.app/Contents/MacOS/python`).

Langkah 2 — Pasang `psycopg2-binary` ke interpreter tersebut
- Di terminal (Command Prompt / PowerShell / Terminal), jalankan perintah dengan path dari langkah 1:

Windows contoh:

```
"C:\Users\<nama-user>\AppData\Local\Programs\Orange\python.exe" -m pip install psycopg2-binary
```

macOS contoh (jika path dari widget):

```
/Applications/Orange.app/Contents/MacOS/python -m pip install psycopg2-binary
```

Langkah 3 — Verifikasi pemasangan
- Periksa paket terpasang:

```
"<path_python_orange>" -m pip show psycopg2-binary
```

- Atau di widget Python jalankan:

```
import psycopg2
print('psycopg2 OK')
```

Catatan singkat
- Gunakan `psycopg2-binary` untuk kemudahan pada lingkungan pembelajaran. Untuk produksi, pertimbangkan `psycopg2` dan dependensi sistem.
- Jika instalasi gagal karena compiler/header, ikuti instruksi platform:
  - Windows: biasanya tidak perlu; jalankan Command Prompt sebagai Administrator jika perlu.
  - macOS: jalankan `xcode-select --install` jika muncul error compile.

FAQ singkat
- Mengapa harus pakai path dari `sys.executable`? Karena Orange menggunakan interpreter sendiri, paket yang dipasang ke Python lain tidak akan terlihat oleh Orange.

Butuh bantuan tambahan?
- Saya bisa buatkan skrip batch/PowerShell untuk Windows yang menerima path atau mencoba mendeteksi lokasi instalasi Orange secara otomatis.

File panduan ini: [Panduan Instalasi/02-instalasi-SQLDbConnector.md](Panduan%20Instalasi/02-instalasi-SQLDbConnector.md#L1)

