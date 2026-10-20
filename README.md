# UTS Machine Learning

Repositori ini berisi pengerjaan Ujian Tengah Semester (UTS) mata kuliah Machine Learning, meliputi implementasi algoritma **Linear Regression** dan **Logistic Regression** yang dibangun secara manual menggunakan pustaka dasar NumPy (from scratch), serta evaluasi dan analisis datanya.

## 👤 Identitas
* **Nama**  : Nurhayati
* **NIM**   : 241011401992
* **Kelas** : 05TPLE005
Kelas       : ~~Reg B~~ / Reg C *(coret salah satu)*

---

## Ringkasan Eksekutif & Hasil Eksperimen

Seluruh proses pemodelan dan pengujian dalam proyek ini dikendalikan menggunakan penetapan `random_state = 92` saat melakukan pembagian proporsi data *training* dan *testing*.

### Bagian A: Linear Regression (Prediksi Penjualan)
Fokus pada bagian ini adalah memodelkan secara linear pengaruh **Biaya Iklan** terhadap tingkat **Penjualan** menggunakan dataset `Ads_Data.csv`.
* **Metode Pendekatan**: Normal Equation dan Gradient Descent.
* **Persamaan Garis Regresi**: $\hat{y} = 27.7242 + 9.1831X$
* **Evaluasi Model (Data Testing)**:
  * **RMSE**: 4.21
  * **$R^2$ Score**: 0.973 (97.3%)
* **Analisis Singkat**: 
  Model menunjukkan kecocokan yang sangat baik dengan data ($R^2$ mendekati 1) dan mampu menggeneralisasi data baru tanpa *overfitting* (RMSE testing lebih rendah dari training). Melalui eksperimen *learning rate* pada algoritma Gradient Descent, nilai `0.02` terbukti sebagai yang paling optimal untuk mencapai konvergen, sedangkan `0.001` berjalan terlalu lambat dan `0.1` menyebabkan *divergen* (gagal konvergen). Prediksi ekstrapolasi untuk biaya iklan 12 juta yang menghasilkan angka 137.92 dinilai kurang realistis, karena tidak memperhitungkan batas jenuh pasar dan hukum *diminishing returns* di dunia nyata.

### Bagian B: Logistic Regression (Filter Spam Email)
Bagian ini dirancang untuk membangun sistem klasifikasi *filter spam* yang mampu mendeteksi kategori email berdasarkan atribut jumlah *link* dan kata promo dari `Email_Data.csv`.
* **Metode Pendekatan**: Gradient Descent Manual (Learning Rate = 0.1, 10.000 iterasi).
* **Persamaan Probabilitas**: $P(\text{Spam}) = \sigma(-8.9171 + 0.7964 \cdot \text{JumlahLink} + 0.7573 \cdot \text{KataPromo})$
* **Evaluasi Model (Data Testing)**:
  * **Akurasi**: 100%
  * **Precision**: 100%
  * **Recall**: 100%
  * **F1-Score**: 100%
* **Analisis Singkat**: 
  Algoritma berhasil memisahkan data klasifikasi secara sempurna tanpa adanya kesalahan *False Positives* maupun *False Negatives*. Dari uji eksperimen ambang batas (*threshold*), disimpulkan bahwa probabilitas **0.5** memberikan keseimbangan performa paling ideal. Namun, dalam skenario implementasi sistem *filter spam* sesungguhnya di mana mencegah kesalahan blokir email penting (mengurangi FP) menjadi prioritas utama, *threshold* adaptif di angka **0.7** dapat menjadi pilihan strategi yang lebih aman.

### Bagian Bonus: Komparasi Terhadap Scikit-Learn
* **Perbandingan Linear Regression**: 
  Nilai dari perhitungan titik potong (*intercept*), koefisien garis, beserta indikator metrik *error* (RMSE) antara kalkulasi *Normal Equation* NumPy dengan modul `sklearn.linear_model.LinearRegression` menunjukkan hasil akhir yang **identik (sama persis)**.
* **Perbandingan Logistic Regression**: 
  Terdapat perbedaan marjinal pada nilai bobot implementasi manual jika disandingkan dengan fungsi bawaan (*default*) `LogisticRegression` pada Scikit-Learn. Perbedaan ini disebabkan oleh penerapan **regularisasi L2** (`penalty='l2'`) yang otomatis menyala pada parameter *default* Scikit-Learn. Saat parameter regularisasi tersebut dinonaktifkan (`penalty=None`), kalkulasi bobot yang dihasilkan kembali setara dengan metode *Gradient Descent* manual yang telah dikerjakan di atas.

---
**Struktur Direktori Repositori:**
- `README.md` : Dokumentasi proyek dan rangkuman hasil.
- `tugas_UTS.ipynb` : *Jupyter Notebook* utama yang berisi semua kode baris per baris, plot visualisasi, dan analisa pengerjaan.
- `Ads_Data.csv` : Arsip dataset pendukung yang digunakan untuk tahap Regresi Linear.
- `Email_Data.csv` : Arsip dataset pendukung yang digunakan untuk tahap Regresi Logistik.
