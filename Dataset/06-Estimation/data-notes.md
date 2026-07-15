# Data Notes - Estimation

Deskripsi: Catatan data untuk dataset estimasi, termasuk variabel input, target numerik, dan konteks pengukuran nilai.

## Dataset

1. **01-Estimasi Harga Rumah** — estimasi harga jual rumah berdasarkan luas tanah/bangunan, jumlah kamar, lantai, usia bangunan, jarak ke pusat kota, dan kategori lokasi. Target: `Harga_Rumah_Juta`.
2. **02-Estimasi Harga Sewa Rumah** — estimasi harga sewa tahunan berdasarkan luas bangunan, jumlah kamar, status furnished, jarak ke pusat kota, fasilitas parkir, dan tipe properti. Target: `Harga_Sewa_Juta_per_Tahun`.
3. **03-Estimasi Kebutuhan Anggaran** — estimasi kebutuhan anggaran satker/OPD berdasarkan jumlah penduduk terlayani, jumlah program kegiatan, jumlah pegawai, luas wilayah, realisasi anggaran tahun lalu, jumlah unit kerja, dan tingkat inflasi. Target: `Kebutuhan_Anggaran_Juta`.

Setiap dataset memiliki `training_dataset.csv` (500 baris) dan `testing_dataset.csv` (100 baris). Data bersifat sintetis, dibangkitkan dengan formula + noise acak untuk keperluan latihan regresi/estimasi.
