# Laporan Proyek Machine Learning - [Nama Anda]

## Domain Proyek
Proyek ini berfokus pada prediksi kemungkinan seseorang menderita diabetes berdasarkan berbagai fitur medis seperti glukosa, tekanan darah, indeks massa tubuh (BMI), dan lainnya. Diabetes merupakan salah satu penyakit kronis yang banyak diderita masyarakat dunia dan dapat menyebabkan komplikasi serius jika tidak ditangani sejak dini.

Menurut data dari WHO (World Health Organization), lebih dari 422 juta orang di dunia hidup dengan diabetes, dan angka ini terus meningkat setiap tahunnya. Oleh karena itu, deteksi dini melalui metode prediksi berbasis data menjadi penting untuk mencegah risiko yang lebih besar.

**Referensi:**
- World Health Organization: Diabetes

## Business Understanding

### Problem Statements
1. Bagaimana cara memprediksi apakah seseorang menderita diabetes berdasarkan data medis?
2. Apakah pengolahan data seperti imputasi nilai nol dan transformasi fitur dapat meningkatkan performa model?
3. Algoritma machine learning mana yang paling efektif untuk prediksi diabetes pada dataset ini?

### Goals
1. Membangun model prediksi diabetes dengan tingkat akurasi yang tinggi.
2. Meningkatkan kualitas data melalui proses data cleaning dan feature engineering.
3. Mengevaluasi performa beberapa model dan memilih yang terbaik berdasarkan metrik evaluasi.

### Solution Statements
- Menggunakan Logistic Regression sebagai baseline model.
- Meningkatkan performa model dengan melakukan imputasi pada nilai-nilai nol menggunakan median atau mean berdasarkan distribusi data.
- Melakukan feature transformation seperti eksponensiasi dan teknik polynomial untuk mencoba meningkatkan akurasi.
- Melakukan hyperparameter tuning pada Logistic Regression.
- Menguji model dengan beberapa nilai `test_size` dan memilih model terbaik berdasarkan hasil evaluasi.

## Data Understanding

Dataset yang digunakan berasal dari Pima Indians Diabetes Database dan terdiri dari 768 baris dan 9 kolom. Dataset ini umum digunakan dalam studi prediksi diabetes.

**Fitur-fitur yang tersedia:**
- **Pregnancies**: Jumlah kehamilan
- **Glucose**: Konsentrasi glukosa plasma
- **BloodPressure**: Tekanan darah diastolik (mm Hg)
- **SkinThickness**: Ketebalan lipatan kulit triceps (mm)
- **Insulin**: Kadar insulin serum 2 jam (mu U/ml)
- **BMI**: Indeks massa tubuh (berat dalam kg/(tinggi dalam m)^2)
- **DiabetesPedigreeFunction**: Fungsi silsilah diabetes
- **Age**: Umur (tahun)
- **Outcome**: 1 jika menderita diabetes, 0 jika tidak

Data ditemukan tidak memiliki missing values secara eksplisit, tetapi terdapat nilai 0 pada beberapa fitur medis yang tidak realistis (misalnya: Glucose, BloodPressure, SkinThickness, Insulin, BMI), sehingga dilakukan proses imputasi.

## Data Preparation

Langkah-langkah data preparation:
- Mengecek missing values dan duplicate data
- Imputasi nilai nol berdasarkan distribusi:
  - Fitur dengan distribusi miring seperti Glucose, Insulin, dan SkinThickness diimputasi dengan median.
  - Fitur dengan distribusi normal seperti BloodPressure dan BMI diimputasi dengan mean.
- Membuat beberapa fitur baru hasil transformasi polynomial (pangkat tiga) untuk uji performa model.

## Modeling

Model baseline yang digunakan adalah **Logistic Regression**. Untuk mengembangkan model:
- Dilakukan eksperimen dengan mengubah `test_size` (0.2, 0.25, 0.3)
- Dilakukan hyperparameter tuning pada Logistic Regression
- Percobaan menambahkan fitur hasil transformasi dan dot product antar fitur

Model lain sempat diuji tetapi Logistic Regression memberikan hasil yang paling stabil dan akurat berdasarkan evaluasi metrik.

### Kelebihan dan Kekurangan Logistic Regression
**Kelebihan:**
- Interpretasi hasil model cukup mudah
- Cepat dan efisien untuk dataset kecil-menengah

**Kekurangan:**
- Kurang efektif jika relasi antar fitur dan target bersifat non-linear
- Rentan terhadap outlier

## Evaluation

### Metrik Evaluasi yang Digunakan
- **Accuracy**: Persentase prediksi yang benar
- **Precision**: Kemampuan model untuk memprediksi positif secara benar
- **Recall**: Kemampuan model untuk menemukan semua kasus positif
- **F1 Score**: Harmonik rata-rata dari precision dan recall

### Hasil Evaluasi
- Akurasi terbaik diperoleh saat `test_size = 0.2`
- Model memberikan keseimbangan yang cukup baik antara precision dan recall
- Metrik F1 menunjukkan performa model yang konsisten dan tidak bias terhadap kelas mayoritas

### Formula Metrik
- Accuracy = (TP + TN) / (TP + TN + FP + FN)
- Precision = TP / (TP + FP)
- Recall = TP / (TP + FN)
- F1 Score = 2 × (Precision × Recall) / (Precision + Recall)
