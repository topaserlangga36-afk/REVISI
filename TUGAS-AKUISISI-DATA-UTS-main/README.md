# Tugas UTS — Akuisisi Data Pariwisata Bali

## Identitas Mahasiswa
* **Nama:** I Kadek Topas Erlangga
* **NIM:** 2501010328
* **Program Studi:** Teknik Informatika — INSTIKI
* **Mata Kuliah:** Akuisisi Data

## Deskripsi Proyek
Proyek ini mengintegrasikan data kunjungan wisatawan domestik bulanan dari Badan Pusat Statistik (BPS) Provinsi Bali, data historis cuaca dari Open-Meteo Historical Weather API untuk enam titik destinasi pariwisata di Bali, serta data administratif wilayah Bali hasil *ethical web scraping* dari Wikipedia.

## Struktur Direktori
* `notebooks/akuisisi_data_uts.ipynb` : Notebook utama berisi kode pembacaan berkas & estimasi *storage* (Soal 1), etika data & `robots.txt` (Soal 2 & 4), akuisisi API Open-Meteo & *scraping* Wikipedia (Soal 3 & 4), pencatatan *provenance* MD5, serta penggabungan data & presentasi (Soal 5).
* `data/raw/` : Menyimpan berkas mentah hasil akuisisi (`dataset_bps.xlsx`, `weather_api_raw.json`, `wikipedia_bali_raw.html`, `wikipedia_robots.txt`).
* `data/processed/` : Menyimpan data hasil pembersihan, transformasi format panjang (*long format*), agregasi cuaca bulanan, dan hasil penggabungan (`bps_wisatawan_long.csv`, `weather_api_daily.csv`, `weather_api_monthly.csv`, `wikipedia_bali_table.csv`, `hasil_merge_bps_weather.csv`).
* `metadata/` : Menyimpan dokumen kepatuhan etika data (`data_ethics_checklist.csv`), silsilah dan integritas hash MD5 (`provenance.csv`), serta metadata penggabungan (`merge_metadata.json`).

## Cara Menjalankan Notebook
1. Pastikan seluruh dependensi terpasang (`pandas`, `openpyxl`, `requests`, `beautifulsoup4`, `lxml`, `matplotlib`).
2. Jalankan seluruh sel di `notebooks/akuisisi_data_uts.ipynb` secara berurutan dari direktori utama repositori (`TUGAS-AKUISISI-DATA-UTS-main/`).
