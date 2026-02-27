# Log Prompt & Keterbaruan Kode

Kami menggunakan bantuan AI (Gemini) untuk menstrukturisasi sintaks dasar *K-Fold Validation*. Namun, untuk memastikan orisinalitas dan kesesuaian dengan karakteristik data Spotify, kami melakukan modifikasi fundamental secara mandiri berikut ini:

1. **Inovasi Target Encoding Manual:** AI menyarankan penggunaan `LabelEncoder` untuk fitur teks. Kami menolak saran ini karena menyebabkan cacat ordinal matematis pada Regresi Linier. Kami membangun algoritma *Target Encoding* mandiri dengan fungsi `.groupby().mean()` untuk mengonversi artis dan genre menjadi probabilitas. Inovasi ini mendongkrak R2 dari ~2% menjadi ~75%.
2. **Penyederhanaan Arsitektur Model (Penghapusan Polynomial Features):** Rekomendasi draf awal dari AI menyarankan penggabungan Huber Regressor dengan *Polynomial Features*. Kami secara sadar menghapus fungsi polinomial tersebut dari *pipeline* untuk menjaga keadilan perbandingan (*apple-to-apple*) dengan model *baseline* (Regresi Linier murni), dan menekan beban memori komputasi.
3. **Penanganan Matematis MAPE:** Fungsi bawaan `cross_validate` Scikit-Learn mengalami *crash (ZeroDivisionError)* karena dataset target bernilai 0. Kami mandiri menyuntikkan nilai epsilon `1e-10` pada pembagi metrik MAPE.
4. **Desain Kustom Stress Test:** Kerangka pengujian anomali tidak menggunakan templat AI, melainkan kami bangun menggunakan logika boolean `y == 0` dan `y > 0` hasil temuan *Exploratory Data Analysis* (EDA) kami sendiri.
