# Akuisisi dan Integrasi Data Pariwisata dan Cuaca di Bali

Dokumentasi teknis Ujian Tengah Semester mata kuliah **Data Acquisition & Management (BIFP-243)**, INSTIKI.

## 1. Identitas Mahasiswa

| Informasi | Keterangan |
| :--- | :--- |
| **Nama** | I Kadek Topas Erlangga |
| **NIM** | 2501010328 |
| **Program Studi** | Informatika |
| **Kelas** | F |
| **Fokus Wilayah** | Provinsi Bali (6 Destinasi Wisata: Kuta, Tanah Lot, Ulun Danu Beratan, Ubud, GWK, dan Kintamani) |

## 2. Tujuan Proyek (Goals)
1. Mengakuisisi data dari tiga mekanisme berbeda: pengunduhan berkas resmi terstruktur (XLSX/CSV), pemanggilan REST API (JSON), dan web scraping statis (HTML).
2. Menyimpan seluruh berkas mentah tanpa modifikasi di `data/raw/` dan hasil olahan bersih di `data/processed/`.
3. Mengevaluasi profil kualitas data (jumlah baris, kolom, tipe data, *missing values*, duplikasi) serta estimasi kebutuhan penyimpanan.
4. Mengintegrasikan seluruh sumber data melalui `pd.merge()` berkunci `periode` (`YYYY-MM`) dengan validasi `many_to_one` bebas duplikasi.
5. Mendokumentasikan silsilah data (`provenance.csv` beserta checksum MD5) dan kepatuhan etika data (daftar periksa 9 butir serta bukti `robots.txt`).

## 3. Sumber Data

| No | Metode | Sumber | URL | Lisensi | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Unduh Berkas XLSX/CSV | Badan Pusat Statistik (BPS) Provinsi Bali | [BPS Bali – Wisatawan Domestik Bulanan 2004–2025](https://bali.bps.go.id/id/statistics-table/1/MjkjMQ%3D%3D/banyaknya-wisatawan-domestik-bulanan-ke-bali-2004-2025.html) | Ketentuan Portal BPS | Tersedia (264 baris format *long*) |
| 2 | REST API | Open-Meteo Historical Weather API | `https://archive-api.open-meteo.com/v1/archive` | CC BY 4.0 | Tersedia (2.190 baris harian / 72 baris bulanan) |
| 3 | Web Scraping (EN) | Wikipedia – Bali | `https://en.wikipedia.org/wiki/Bali` | CC BY-SA 4.0 | Tersedia (Tabel statis halaman Bali) |

## 4. Struktur Direktori Proyek
- `notebooks/`: Berisi file notebook utama (`akuisisi_data_uts.ipynb`) yang lengkap dengan kode sumber dan seluruh hasil eksekusi.
- `data/raw/`: Berkas mentah orisinal (`dataset_bps.xlsx`, `weather_api_raw.json`, `wikipedia_bali_raw.html`, dan `wikipedia_robots.txt`) dalam bentuk *bytes* utuh.
- `data/processed/`: Dataset bersih per sumber (`bps_wisatawan_long.csv`, `weather_api_daily.csv`, `weather_api_monthly.csv`, `wikipedia_bali_table.csv`) serta tabel terpadu hasil penggabungan (`hasil_merge_bps_weather.csv`).
- `metadata/`: Dokumentasi audit dan silsilah data (`provenance.csv`, `data_ethics_checklist.csv`, `merge_metadata.json`).
- `metadata/charts/` *(opsional)*: Grafik visualisasi hasil analisis deskriptif dalam format PNG.

## 5. Perangkat Lunak & Pustaka (Tools)
Python 3, Google Colab, `pandas`, `numpy`, `requests`, `BeautifulSoup4` (`html.parser`), `urllib.robotparser`, `matplotlib`, `pathlib`, dan `hashlib`.

## 6. Catatan Keterbatasan Data
Angka jumlah wisatawan dari BPS merupakan data agregat tingkat **Provinsi Bali**, sedangkan parameter cuaca dikumpulkan pada enam titik koordinat destinasi wisata (Kuta, Tanah Lot, Ulun Danu Beratan, Ubud, GWK, dan Kintamani). Hasil penggabungan (`many_to_one` berdasarkan kunci `periode`) merepresentasikan kondisi cuaca masing-masing destinasi pada bulan tertentu yang disandingkan dengan total kunjungan wisatawan provinsi, **bukan** jumlah kunjungan wisatawan spesifik pada setiap destinasi.