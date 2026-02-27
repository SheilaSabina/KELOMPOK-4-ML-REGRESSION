# 🎵 Analisis Regresi Popularitas Lagu Spotify
**Evaluasi Baseline Linier vs. Huber Regressor Melalui Pengujian Stress Test**

Repositori ini berisi keseluruhan proyek Machine Learning untuk memprediksi popularitas lagu di Spotify menggunakan metrik fisika audio. Proyek ini membandingkan algoritma Regresi Linier konvensional (OLS) dengan model *Robust Regression* (Huber Regressor Murni) dalam menangani data anomali (*outlier*).

## 👥 Tim Pengembang (Kelompok 4)
1. Dina Izzati Elfadheya (2310817120001)
2. Muhammad Nurwahyudi Adhitama (2310817310005)
3. M Samil Rendy Nor Saleh (2310817310004)
4. Sheila Sabina (2310817220028)

## 📁 Struktur Repositori
- `dataset_spotify.csv` : Dataset mentah yang digunakan untuk pelatihan dan pengujian.
- `ML_REGRESSION EXPERIMENT.ipynb` : File kode eksperimen awal (Jupyter Notebook) yang berisi rekam jejak pencarian model, termasuk pengujian berbagai algoritma (*Ridge, Lasso, OLS*) sebelum menemukan arsitektur yang paling optimal.
- `ML_REGRESSION HASIL IMPROVE.ipynb` : File kode utama versi final yang memuat *pipeline preprocessing* bersih, komparasi langsung (Baseline OLS vs Huber Regressor), evaluasi K-Fold, *Stress Test*, hingga cetak visualisasi grafik.
- `LAPORAN ML REGRESSION.pdf` : Dokumen laporan lengkap yang membahas landasan teori, analisis metrik komparatif, literatur ilmiah, dan kesimpulan eksperimen.
- `EXPERIMENT_LOG.md` : Rekapitulasi hasil evaluasi metrik (Performa Normal vs Stress Test).
- `LOG_PROMPT.md` : Catatan interaksi prompt AI dan bukti keterbaruan/modifikasi mandiri dari tim pengembang.

## 🚀 Kesimpulan Utama
Berdasarkan eksperimen dan *Outlier Stress Test*, model **Huber Regressor** terbukti jauh lebih tangguh (*robust*) dibandingkan OLS. Huber Regressor secara cerdas mampu mempertahankan akurasi prediksi untuk mayoritas populasi lagu normal dan menolak mengubah rumus regresi dasarnya hanya demi mengakomodasi data anomali (lagu dengan popularitas absolut 0 secara administratif).
