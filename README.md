# Analisis Regresi Popularitas Lagu Spotify
**Evaluasi Baseline Linier vs. Huber Regressor Melalui Pengujian Stress Test**

Repositori ini berisi keseluruhan proyek Machine Learning untuk memprediksi popularitas lagu di Spotify menggunakan metrik fisika audio. Proyek ini membandingkan algoritma Regresi Linier konvensional (OLS) dengan model *Robust Regression* (Huber Regressor) dalam menangani data anomali (*outlier*).

## Tim Pengembang (Kelompok X)
1. Dina Izzati Elfadheya (2310817120001)
2. Muhammad Nurwahyudi Adhitama (2310817310005)
3. M Samil Rendy Nor Saleh (2310817310004)
4. Sheila Sabina (2310817220028)

## Struktur Repositori
- `dataset_spotify.csv`: Dataset mentah yang digunakan untuk pelatihan dan pengujian.
- `ML_REGRESI.ipynb`: Kode sumber utama (Jupyter Notebook) berisi *pipeline preprocessing*, pemodelan, evaluasi, hingga visualisasi grafik.
- `LAPORAN ML REGRESSION.pdf`: Dokumen laporan lengkap yang membahas landasan teori, analisis metrik, dan kesimpulan eksperimen.
- `EXPERIMENT_LOG.md`: Rekapitulasi hasil evaluasi metrik dari model yang diuji.
- `LOG_PROMPT.md`: Catatan modifikasi mandiri terhadap *output* AI (Keterbaruan).

## Kesimpulan Utama
Berdasarkan eksperimen *Stress Test*, model **Huber Regressor** terbukti lebih tangguh (*robust*) dibandingkan OLS. Huber Regressor mampu mempertahankan akurasi prediksi untuk mayoritas lagu normal dan menolak mengubah rumus regresi dasar hanya demi mengejar data anomali (lagu dengan popularitas absolut 0 secara administratif).
