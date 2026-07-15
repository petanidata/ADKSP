# Data Notes - Estimation

Deskripsi: Catatan data untuk dataset estimasi, termasuk variabel input, target numerik, dan konteks pengukuran nilai.

## Dataset

1. **harga_rumah** (`harga_rumah_training_dataset.csv`, `harga_rumah_testing_dataset.csv`) — estimasi harga jual rumah berdasarkan luas tanah/bangunan, jumlah kamar, lantai, usia bangunan, jarak ke pusat kota, dan kategori lokasi. Target: `Harga_Rumah_Juta`.
2. **harga_sewa_rumah** (`harga_sewa_rumah_training_dataset.csv`, `harga_sewa_rumah_testing_dataset.csv`) — estimasi harga sewa tahunan berdasarkan luas bangunan, jumlah kamar, status furnished, jarak ke pusat kota, fasilitas parkir, dan tipe properti. Target: `Harga_Sewa_Juta_per_Tahun`.
3. **kebutuhan_anggaran** (`kebutuhan_anggaran_training_dataset.csv`, `kebutuhan_anggaran_testing_dataset.csv`) — estimasi kebutuhan anggaran satker/OPD berdasarkan jumlah penduduk terlayani, jumlah program kegiatan, jumlah pegawai, luas wilayah, realisasi anggaran tahun lalu, jumlah unit kerja, dan tingkat inflasi. Target: `Kebutuhan_Anggaran_Juta`.

Setiap dataset memiliki file `*_training_dataset.csv` (500 baris) dan `*_testing_dataset.csv` (100 baris). Data bersifat sintetis, dibangkitkan dengan formula + noise acak untuk keperluan latihan regresi/estimasi.
