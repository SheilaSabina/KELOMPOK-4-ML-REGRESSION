# Log Eksperimen & Hasil Metrik Evaluasi

Berikut adalah rekapitulasi hasil pelatihan model regresi linier pada dataset Spotify, dievaluasi menggunakan *Hold-Out Validation* (80:20) dan *5-Fold Cross Validation*.

### 1. Komparasi Performa Model Utama
| Metrik Evaluasi | Baseline (OLS Biasa) | Improved (Huber Regressor) | Keterangan |
| :--- | :---: | :---: | :--- |
| **MAE** | 5.60 | **5.57** | **Huber Lebih Baik:** Rata-rata tebakan popularitas harian lebih presisi. |
| **RMSE** | **11.04** | 11.05 | *OLS menang tipis karena memang didesain mengejar kuadrat error.* |
| **R-Squared (R2)** | **0.7544** | 0.7539 | *Sama dengan RMSE, OLS tinggi artifisial akibat mengejar outlier.* |
| **K-Fold R2 (Rata-rata)** | 0.7497 | 0.7491 | Stabilitas model saat divalidasi silang sangat konsisten. |

### 2. Hasil Uji Ketahanan (Outlier Stress Test)
Pengujian khusus pada model Huber Regressor untuk melihat perilakunya saat menghadapi data normal vs data anomali (popularitas mutlak 0).

| Skenario Uji | Jumlah Data | MAE (Error) | Analisis |
| :--- | :---: | :---: | :--- |
| **Performance (Lagu Normal > 0)** | 13.468 baris | **5.15** | Prediksi sangat akurat untuk mayoritas populasi lagu. |
| **Stress Test (Anomali = 0)** | 2.114 baris | **8.27** | Model "menolak" tebakan 0 dan memprediksi kualitas audio sewajarnya (8-9). |
