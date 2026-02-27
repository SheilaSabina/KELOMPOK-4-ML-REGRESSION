# Log Prompt AI & Bukti Keterbaruan Pemodelan

Dokumen ini berisi rekam jejak (*log prompt*) interaksi kritis kami dengan asisten AI selama proses pengembangan model regresi. Log ini membuktikan bahwa kami tidak menerima kode AI secara mentah (*copy-paste*), melainkan secara aktif mengevaluasi arsitektur, mencegah *overfitting*, dan merancang skenario pengujian kustom.

### Tahap 1: Evaluasi Arsitektur & Menjaga Keadilan Komparasi (Apple-to-Apple)
Pada draf awal, AI merekomendasikan penggunaan `HuberRegressor` yang digabungkan dengan `PolynomialFeatures`. Kami menolak arsitektur tersebut karena berpotensi merusak *baseline* perbandingan dan menyebabkan *overfitting*.

> **Prompt Kami kepada AI:**
> *"Setelah kami run kode darimu, Huber dengan Polynomial memang tangguh. TAPI, penambahan polinomial bisa overfitting terhadap noise dan sebenarnya datanya tidak adil, karena baseline preprocessingnya hanya menggunakan 62 data latih. Sebagai bentuk improvement, coba untuk MENGHAPUS POLINOMIAL. Tolong perbarui kodenya dengan menghapus fungsi PolynomialFeatures. Kita akan menggunakan model Huber Regressor MURNI agar perbandingannya adil (apple-to-apple) dengan Baseline OLS dan apakah hasilnya lebih bagus?"*

**Keterbaruan Kami:** Memaksa AI kembali ke arsitektur Regresi Linier murni tanpa manipulasi ekspansi polinomial. Ini membuktikan bahwa kami memahami syarat utama komparasi model: untuk membandingkan performa murni fungsi *Loss* (MSE vs Huber Loss), kedua algoritma harus disuplai dengan dimensi fitur yang persis sama.

### Tahap 2: Validasi Silang (Cross-Validation) yang Valid
Untuk memastikan model Huber murni kami tervalidasi secara statistik dan tidak terpengaruh oleh kebocoran data acak, kami menuntut penggunaan metode standar industri.

> **Prompt Kami kepada AI:**
> *"Tolong tambahkan perhitungan metrik evaluasi MAE, RMSE, R2, dan MAPE menggunakan fungsi cross_validate standar dari Scikit-Learn untuk model Huber murni tadi."*

### Tahap 3: Perancangan Outlier Stress Test Kustom Berbasis EDA
Alih-alih membiarkan AI menggunakan metode deteksi anomali otomatis yang buta konteks, kami membangun kerangka pengujian (Stress Test) secara mandiri. Kami menggunakan *domain knowledge* dari data asli (berdasarkan *Exploratory Data Analysis*) bahwa anomali di Spotify bersifat administratif.

> **Prompt Kami kepada AI:**
> *"Bagaimana cara terbaik untuk menguji seberapa kuat (robust) model Huber kami saat dihadapkan pada outlier ekstrem ini? Berdasarkan hasil Exploratory Data Analysis (EDA) dari si yang punya data di kaggle, anomali ini bersifat administratif di mana popularitas lagu yang wajar disandingkan dengan lagu yang popularitasnya mutlak 0. Saya ingin membuat kerangka 'Outlier Stress Test' kustom. Tolong buatkan skrip logika filter boolean untuk memecah X_test dan y_test menjadi dua kondisi terpisah: Kondisi Normal (y > 0) dan Kondisi Anomali Ekstrem (y == 0), lalu hitung MAE pada kedua kondisi tersebut secara terpisah."*

**Keterbaruan Kami:** Inovasi *Stress Test* ini murni berasal dari logika filter *boolean* yang kami temukan sendiri. Evaluasi ini membuktikan bahwa kode tidak di-*generate* secara generik, melainkan dirancang eksklusif untuk menyelesaikan masalah spesifik pada dataset Spotify.
