# Panduan Membuat API Key YouTube Data API v3

## A. Tujuan
Pada praktikum ini, mahasiswa membuat **API Key** di Google Cloud untuk mengakses **YouTube Data API v3**.

API Key ini dapat digunakan untuk mengambil data publik YouTube, seperti:

- Data video
- Judul dan deskripsi video
- Nama channel
- Jumlah views, likes, dan komentar
- Hasil pencarian video

> Catatan: API Key berbeda dengan password akun Google. Jangan dibagikan ke orang lain dan jangan diunggah ke repository publik.

---

## B. Persiapan
Siapkan hal berikut:

1. Akun Google/Gmail aktif.
2. Browser (disarankan Google Chrome).
3. Koneksi internet stabil.

---

## C. Langkah 1 - Buka Google Cloud Console
1. Buka halaman: [Google Cloud Console](https://console.cloud.google.com/)
2. Login menggunakan akun Google Anda.
3. Jika muncul Terms of Service, ikuti proses persetujuan.

---

## D. Langkah 2 - Buat Project Baru
1. Klik **Select a project** di bagian atas.
2. Klik **NEW PROJECT**.
3. Isi **Project name**.

Contoh nama project:

- `Praktikum YouTube API - NamaMahasiswa`
- `YouTubeAPI_Nama_NIM`

4. Klik **CREATE**.

> Saran: Setiap mahasiswa membuat project masing-masing agar quota dan credential tidak tercampur.

---

## E. Langkah 3 - Pilih Project
1. Klik **Select a project** lagi.
2. Pilih project yang baru dibuat.
3. Pastikan nama project aktif terlihat di bagian atas halaman.

---

## F. Langkah 4 - Aktifkan YouTube Data API v3
1. Buka halaman: [YouTube Data API v3](https://console.cloud.google.com/apis/library/youtube.googleapis.com)
2. Pastikan project aktif sudah benar.
3. Klik **YouTube Data API v3**.
4. Klik **ENABLE**.

Jika berhasil, status API akan aktif di project tersebut.

---

## G. Langkah 5 - Buat API Key
1. Buka menu **APIs & Services** > **Credentials**.
2. Atau buka langsung: [Google Cloud Credentials](https://console.cloud.google.com/apis/credentials)
3. Klik **+ CREATE CREDENTIALS**.
4. Pilih **API key**.

Google Cloud akan menampilkan API Key Anda.

Contoh format API Key:

`AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX`

> Jangan gunakan contoh di atas. Gunakan API Key milik Anda sendiri.

---

## H. Langkah 6 - Simpan API Key dengan Aman
Lakukan hal berikut:

1. Salin API Key.
2. Simpan di tempat aman.
3. Jangan kirim ke grup kelas.
4. Jangan tampilkan API Key di screenshot.
5. Jangan commit API Key ke GitHub/repo publik.

Contoh penyimpanan sederhana di Python:

```python
API_KEY = "API_KEY_MILIK_ANDA"
```

Untuk project serius, simpan API Key di environment variable atau file `.env`.

---

## I. Langkah 7 - Batasi API Key (Disarankan)
Agar lebih aman:

1. Di halaman **Credentials**, klik API Key yang baru dibuat.
2. Pada **API restrictions**, pilih **Restrict key**.
3. Pilih **YouTube Data API v3**.
4. Klik **SAVE**.

Dengan pembatasan ini, key hanya bisa dipakai untuk API yang dipilih.

---

## J. Langkah 8 - Uji API Key
Gunakan endpoint berikut:

```text
https://www.googleapis.com/youtube/v3/videos
```

Parameter yang diperlukan:

- `part=snippet,statistics`
- `id=VIDEO_ID`
- `key=API_KEY_ANDA`

Contoh request:

```text
https://www.googleapis.com/youtube/v3/videos?part=snippet,statistics&id=7lCDEYXw3mM&key=API_KEY_ANDA
```

Ganti `API_KEY_ANDA` dengan key Anda.

---

## K. Hasil yang Diharapkan
Jika berhasil, browser akan menampilkan response JSON, misalnya:

```json
{
	"kind": "youtube#videoListResponse",
	"items": [
		{
			"id": "VIDEO_ID",
			"snippet": {
				"title": "Judul Video"
			},
			"statistics": {
				"viewCount": "12345",
				"likeCount": "100"
			}
		}
	]
}
```

Artinya API Key sudah valid dan bisa mengakses data publik YouTube.

---

## L. Memahami Struktur URL API
Contoh URL:

```text
https://www.googleapis.com/youtube/v3/videos?part=snippet,statistics&id=VIDEO_ID&key=API_KEY_ANDA
```

Keterangan komponen:

| Komponen | Fungsi |
|---|---|
| `/youtube/v3/videos` | Endpoint data video |
| `part=snippet,statistics` | Bagian data yang diminta |
| `id=VIDEO_ID` | ID video target |
| `key=API_KEY_ANDA` | API Key aplikasi |

---

## M. Alternatif Uji dengan Google APIs Explorer
Anda juga bisa uji API tanpa coding:

1. Buka [Google APIs Explorer](https://developers.google.com/apis-explorer)
2. Cari **YouTube Data API v3**
3. Pilih endpoint yang ingin diuji

Cara ini cocok untuk memahami parameter sebelum membuat script Python.

---

## N. Hal yang Perlu Diperhatikan
### 1. API Key bersifat rahasia
Jangan membagikan API Key ke orang lain.

### 2. Setiap request menggunakan quota
YouTube Data API memiliki batas quota. Hindari request berulang tanpa kebutuhan.

### 3. API Key tidak selalu cukup
Untuk akses data publik, API Key biasanya cukup. Untuk data yang membutuhkan izin pengguna, gunakan OAuth 2.0.

---

## O. Checklist Praktikum
Pastikan semua poin berikut sudah terpenuhi:

- Memiliki akun Google.
- Membuat project baru.
- Memilih project yang benar.
- Mengaktifkan YouTube Data API v3.
- Membuat API Key.
- Membatasi API Key ke YouTube Data API v3.
- Melakukan test request.
- Mendapatkan response JSON.
- Tidak membagikan API Key.
- Tidak mengunggah API Key ke repo publik.

---

## P. Alur Singkat
Urutan proses:

1. Google Account
2. Google Cloud Console
3. Create Project
4. Enable YouTube Data API v3
5. Credentials
6. Create API Key
7. Restrict API Key
8. Test API
9. Mendapatkan data YouTube (JSON)

---

## Referensi Resmi
- [YouTube Data API - Getting Started](https://developers.google.com/youtube/v3/getting-started)

