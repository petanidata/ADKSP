# Panduan Instalasi Database Connector (PostgreSQL) untuk Widget di Orange

Tujuan: memasang driver PostgreSQL agar widget SQL (mis. `SQL Table`) di Orange dapat terhubung ke database PostgreSQL. Petunjuk berikut memastikan `pip install` dijalankan pada lokasi Python yang digunakan oleh instalasi Orange di setiap laptop mahasiswa.

**Prasyarat**
- **Orange terpasang**: Pastikan Orange sudah terinstal dan bisa dijalankan.
- **Koneksi internet**: untuk mengunduh paket Python.
- **Hak akses**: beberapa metode membutuhkan hak Administrator / sudo.

**Ringkasan langkah (cepat)**
- **Temukan Python yang dipakai Orange**: cari folder instalasi Orange dan gunakan `python.exe`/`python3` di folder yang sama.
- **Jalankan pip lewat Python itu**: `path/to/python -m pip install psycopg2-binary`
- **Jika perlu dependensi sistem** (Linux/macOS): install library `libpq`/header sebelum memasang `psycopg2` (lihat bagian Troubleshooting).

**Langkah tambahan (cara utama - gunakan Widget Python Script di Orange)**

1. Buka Widget `Python Script` di Orange lalu jalankan kode berikut untuk mengetahui interpreter Python yang dipakai Orange:

```
import sys
print(sys.executable)
```

2. Output akan menampilkan path lengkap ke `python.exe` (contoh hasil):

```
C:\Users\muttaqin.nama-user\AppData\Local\Programs\Orange\python.exe
```

3. Artinya: semua perintah `pip install` harus dijalankan terhadap interpreter tersebut, mis.:

```
"C:\Users\muttaqin.nama-user\AppData\Local\Programs\Orange\python.exe" -m pip install psycopg2-binary
```

Tips: di widget `Python Script` ada tombol `Run` dan tombol salin output — minta mahasiswa menyalin hasil `sys.executable` untuk memastikan mereka menjalankan `pip` pada interpreter yang benar.


**1. Cara menemukan lokasi instalasi Orange (Windows)**
- **Metode Shortcut**: buka Start Menu → cari Orange → klik kanan → More → Open file location → klik kanan pada shortcut → Properties → lihat field `Target`.
- **Metode File Explorer**: periksa kemungkinan folder:
	- `C:\Users\<Nama>\AppData\Local\Programs\Orange\`
	- `C:\Program Files\Orange\`
- Setelah ketemu folder Orange, cari `python.exe` atau file `orange-canvas.exe`. Biasanya `python.exe` berada di folder yang sama atau di subfolder `python`.

Contoh (Windows) — jalankan perintah di Command Prompt (ganti path sesuai instalasi):

```
"C:\Users\Nama\AppData\Local\Programs\Orange\python.exe" -m pip install psycopg2-binary
```

Atau, jika berada di folder Orange, buka PowerShell di folder tersebut dan jalankan:

```
.\python.exe -m pip install psycopg2-binary
```

Catatan: `psycopg2-binary` adalah paket yang mudah dipasang untuk pengembangan/kelas. Untuk penggunaan produksi, pertimbangkan `psycopg2` dan install dependensi sistem terlebih dahulu.

**Catatan untuk instalasi standalone (Windows / macOS)**
- Jika Anda menginstal Orange menggunakan installer (standalone) di Windows atau macOS, biasanya tidak perlu mengelola `virtualenv` atau `conda`.
- Gunakan langkah pada bagian "Langkah tambahan" (cek `sys.executable` dari Widget `Python Script`) lalu jalankan `pip install` terhadap interpreter yang ditunjukkan.

**3. Petunjuk macOS / Linux**
- Temukan `orange-canvas` dengan `which orange-canvas` atau cari folder instalasi. Jika ditemukan path ke `orange-canvas`, cari interpreter Python relatif terhadap file tersebut.
- Contoh umum (Linux):

```
/opt/Orange/bin/python3 -m pip install psycopg2-binary
```

- Jika pip membangun modul dan gagal karena header C hilang, pasang dependensi sistem (Debian/Ubuntu):

```
sudo apt update
sudo apt install build-essential libpq-dev python3-dev
```

Di macOS, gunakan `brew install postgresql` jika menggunakan Homebrew untuk mendapatkan library `libpq`.

**4. Troubleshooting umum**
- Error: "pg_config executable not found" → pasang `libpq-dev` (Linux) atau `postgresql` (macOS) sebelum menginstal `psycopg2`.
- Jika tidak menemukan `python.exe` di folder Orange, jalankan Orange, buka Help → About (jika tersedia) untuk melihat path instalasi, atau periksa properties shortcut.
- Jika pemasangan gagal karena hak akses, jalankan Command Prompt sebagai Administrator (Windows) atau gunakan `sudo` (Linux/macOS) — namun hati-hati karena ini akan mengubah environment global.
- Jika ingin memasang hanya untuk user saat tidak punya hak Administrator, gunakan opsi `--user` dengan Python yang sama:

```
"C:\path\to\python.exe" -m pip install --user psycopg2-binary
```

**5. Verifikasi instalasi**
- Jalankan Python yang sama dengan Orange dan cek import:

```
"C:\path\to\python.exe" -c "import psycopg2; print(psycopg2.__version__)"
```

Jika tampil versi tanpa error berarti pemasangan berhasil.

**6. Keterangan gambar (contoh dialog `SQL Table` di Orange)**
- Gambar menunjukkan dialog `SQL Table` pada Orange:
	1) **Server dropdown**: pilih `PostgreSQL` sebagai tipe server.
	2) **Field Server/Database/Username/Password**: masukkan host, nama database, user, dan password.
	3) **Tombol Connect**: klik setelah mengisi detail untuk menguji koneksi.
	4) **Data Selection**: pilih `Table` atau `Custom SQL` untuk mengambil data.
	5) **Auto-discover categorical variables**: opsi untuk deteksi otomatis variabel kategorikal.

Gunakan keterangan di atas untuk menjelaskan tampilan pada slide atau screenshot saat mengajar.

---
Jika Anda ingin, saya bisa:
- Menambahkan perintah spesifik untuk contoh path Windows tiap mahasiswa (buat skrip batch sederhana).
- Menyertakan cuplikan gambar yang diberi nomor/panah (butuh file gambar asli untuk diedit).

File panduan ini: [Panduan Instalasi/02-instalasi-SQLDbConnector.md](Panduan%20Instalasi/02-instalasi-SQLDbConnector.md#L1)

