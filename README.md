# Capstone_Project_Modul_3_Machine_Learning_THotel_Booking
Anthonius Valentino B. P. | Purwadhika JCDS Bandung

## A. Business Problem Understanding

### Context
Dalam industri perhotelan, manajemen pendapatan yang efektif sangat penting karena inventaris yang tetap dan sifat kamar hotel yang mudah kadaluarsa. Pemesanan menjadi dasar untuk peramalan, namun pembatalan menjadi risiko signifikan yang memengaruhi pendapatan dan efisiensi operasional. Tujuan proyek ini adalah mengembangkan model pembelajaran mesin untuk memprediksi pembatalan pemesanan, sehingga mengoptimalkan manajemen inventaris, mengurangi biaya, dan meningkatkan strategi retensi pelanggan.

### Problem Statement
Proyek ini mengeksplorasi bagaimana pembatalan mempengaruhi enam metrik inti dalam operasi hotel: Biaya per Kamar yang Terisi (CPOR), Pendapatan per Kamar yang Tersedia (RevPAR), Biaya per Kamar yang Tersedia (CostPAR), Laba Operasi Kotor per Kamar yang Tersedia (GOPPAR), Tenaga Kerja per Kamar yang Tersedia (LPAR), dan Biaya Akuisisi Tamu (GAC). Pembatalan pemesanan yang signifikan mengganggu metrik ini, mengakibatkan penurunan profitabilitas dan peningkatan biaya operasional.

### Goals
Mengembangkan model prediksi menggunakan pembelajaran mesin untuk mengidentifikasi potensi pembatalan pemesanan, sehingga memungkinkan pengambilan keputusan yang lebih baik dalam manajemen pendapatan dan alokasi sumber daya.

## B. Data Understanding

Dataset `data_hotel_booking_demand.csv` mencakup kolom utama seperti `country`, `market_segment`, `previous_cancellations`, `booking_changes`, `deposit_type`, `days_in_waiting_list`, `customer_type`, `reserved_room_type`, dan `is_canceled`. 

- **Variabel Numerik:** Dievaluasi distribusi dan korelasinya dengan variabel target (`is_canceled`).
- **Variabel Kategorikal:** Kardinalitas tinggi pada `country` diatasi dengan mengelompokkan kategori yang jarang muncul di bawah "Other."

## C. Data Preprocessing

- **Duplikasi:** Menghapus 87,79% baris duplikat untuk mencegah overfitting model.
- **Nilai Hilang:** Mengimput nilai yang hilang di kolom `country` dan menangani kardinalitas tinggi dengan mengelompokkan kategori langka.
- **Outlier:** Menangani outlier di `booking_changes` dan `required_car_parking_spaces` menggunakan winsorization.
- **Data Tidak Seimbang:** Menggunakan Random Over Sampling (ROS) dan SMOTE untuk menangani ketidakseimbangan kelas dalam variabel target (`is_canceled`).

## D. Exploratory Data Analysis (EDA)

Dilakukan analisis univariat dan bivariat untuk memahami hubungan antara fitur dan pembatalan. Wawasan utama:
- **Pola Pemesanan:** Pembatalan lebih tinggi terkait dengan segmen pasar tertentu (misalnya, Agen Perjalanan Online) dan tipe pelanggan (misalnya, pelanggan transit).
- **Transformasi Fitur:** Mengonversi fitur numerik ke kategori untuk interpretasi model yang lebih baik.

## E. Modeling

Sepuluh model berbeda diuji, dengan fokus mengoptimalkan skor F0.5 yang menyeimbangkan presisi dan recall, menekankan meminimalkan false positive karena dampaknya terhadap biaya operasional.

**Model Terbaik Setelah Hyperparameter Tuning:**
1. **Stacking Classifier:** Model berkinerja terbaik dengan skor F0.5 sebesar 0.6218, menggabungkan Decision Tree, KNN, Gradient Boosting, dan Logistic Regression.
2. **Gradient Boosting Classifier:** Mencapai skor F0.5 sebesar 0.5307.
3. **AdaBoost Classifier:** Meningkatkan skor F0.5 menjadi 0.5319.
4. **XGBoost Classifier:** Mencapai skor F0.5 sebesar 0.5336.
5. **Logistic Regression:** Mencapai skor F0.5 setelah tuning sebesar 0.5011.

### Best Model: Stacking Classifier
- **Kinerja:** Skor F0.5 tertinggi menunjukkan keseimbangan yang baik antara presisi dan recall, menjadikannya yang paling efektif untuk meminimalkan false positive sambil mengidentifikasi pembatalan yang benar.
- **Analisis Confusion Matrix:** Menunjukkan tingkat true negative dan true positive yang kuat, mengurangi baik false positive maupun false negative.

### Feature Importance
Prediktor kunci pembatalan termasuk:
- **`days_in_waiting_list`:** Waktu tunggu yang lebih lama berkorelasi dengan tingkat pembatalan yang lebih tinggi.
- **`country`:** Negara tertentu (misalnya, Portugal) menunjukkan kecenderungan pembatalan yang lebih tinggi.
- **`customer_type`:** Pelanggan transit lebih mungkin membatalkan.
- **`market_segment`:** Pemesanan melalui Agen Perjalanan Online memiliki tingkat pembatalan yang lebih tinggi.
- **`deposit_type`:** Deposit yang tidak dapat dikembalikan berkorelasi dengan pembatalan yang lebih rendah.

## E. Conclusion & Recommendations

### Kesimpulan
1. **Kinerja Model:** Stacking Classifier adalah model yang paling efektif, memberikan keseimbangan tinggi antara presisi dan recall untuk memprediksi pembatalan.
2. **Dampak Pembelajaran Mesin:** Menggunakan pembelajaran mesin mengurangi CPOR sebesar 67,98%, meningkatkan RevPAR dari $30,14 menjadi $31,51, dan menurunkan GAC dari 16,36% menjadi 13,91%, menunjukkan manfaat operasional dan finansial yang signifikan.
3. **Wawasan Fitur:** Fitur utama yang memengaruhi pembatalan, seperti `days_in_waiting_list` dan `market_segment`, memberikan wawasan yang dapat ditindaklanjuti untuk meningkatkan kebijakan pemesanan dan strategi retensi pelanggan.

### Rekomendasi
1. **Tingkatkan Pengumpulan Data:** Kumpulkan lebih banyak data untuk meningkatkan akurasi dan generalisasi model.
2. **Optimalkan Strategi Penetapan Harga:** Gunakan prediksi untuk menerapkan penetapan harga dinamis dan promosi yang ditargetkan.
3. **Tingkatkan Retensi Pelanggan:** Kembangkan penawaran yang dipersonalisasi dan kebijakan yang fleksibel untuk mengurangi pembatalan di antara pelanggan berisiko tinggi.
4. **Manfaatkan Prediksi untuk Manajemen Sumber Daya:** Gunakan output model untuk mengalokasikan staf dan sumber daya dengan lebih baik, terutama selama periode berisiko tinggi.
5. **Evaluasi Model Secara Berkala:** Perbarui dan validasi model secara berkala dengan data baru untuk menjaga akurasi dan relevansi.
