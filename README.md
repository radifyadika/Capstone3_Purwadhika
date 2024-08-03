# **Churn Analysis: Telco Customer Retention 📡**
### **By : Radif Ramadan (JCDSOL-014)**

**Context**  
Perusahaan telekomunikasi ingin memahami mengapa beberapa pelanggan memutuskan untuk tidak melanjutkan langganan layanan internet mereka. Analisis Churn untuk Telco ini bertujuan untuk dalam mengambil tindakan preventif untuk mencegah pelanggan berhenti berlangganan, serta mengidentifikasi faktor-faktor yang menyebabkan pelanggan berhenti menggunakan layanan mereka, sehingga perusahaan dapat menjaga hubungan dengan pelanggan dan mempertahankan pendapatan yang ada. Mengingat biaya yang dikeluarkan untuk mempertahankan pelanggan lama tidak sebanyak biaya untuk menambah pelanggan baru **(Source: [Link](https://hbr.org/2014/10/the-value-of-keeping-the-right-customers))**

**Problem Statement :**

ustri telekomunikasi berada pada persaingan yang sangat kompetitif. Mempertahankan pelanggan menjadi krusial, tapi juga sangat menantang. Kehilangan kontrol atas loyalitas pelanggan sama saja kehilangan peluang untuk tumbuh dan mendapatkan keuntungan. Semua provider telekomunikasi saat ini berlomba-lomba untuk menambah jumlah pelanggan, namun tantangannya adalah pelanggan yang churn dan pindah ke kompetitor karena alasan seperti kualitas layanan, harga, atau customer service yang lebih baik. Penawaran spesial saja sudah tidak cukup untuk pelanggan yang sudah berencana untuk churn. Ditambah lagi, provider telekomunikasi harus terus berinvestasi besar dalam infrastruktur untuk tetap bisa memberikan layanan yang bagus kepada pelanggan.

Mengingat tantangan-tantangan diatas, jelas bahwa kehilangan pelanggan atau pergantian pelanggan **(Churn)** bisa berdampak besar pada berbagai aspek perusahaan, terutama dari segi keuangan. Jika saja pelanggan memutuskan untuk Churn atau mengakhiri kontrak, hal itu secara langsung mengakibatkan kerugian finansial bagi perusahaan. Baik dari segi cost ataupun pendapatan.

**Goals :**

Berdasarkan permasalahan diatas, perusahaan perlu mengidentifikasi kemungkinan pelanggan akan churn atau tidak. Dengan cara ini, perusahaan bisa mempersiapkan strategi retensi untuk pelanggan yang berisiko Churn.

Selain itu, perusahaan juga perlu memahami karakteristik dan faktor apa saja yang membuat pelanggan berpotensi churn, sehingga perusahaan dapat mengambil langkah-langkah preventif untuk mencegah churn dan mempertahankan pelanggan yang sudah ada.


**Analytic Approach :**

Analisis yang akan dilakukan adalah menemukan pola yang mengakibatkan pelanggan Churn dan yang tidak Churn. Selanjutnya menerapkan model Machine Learning untuk membangun model yang dapat mengklasifikasikan pelanggan Churn atau Tidak, sehingga membantu perusahaan dalam memprediksi kemungkinan pelanggan yang akan Churn

**Metric Evaluation :**

`Type 1 error : False Positive` --> Resiko nya biaya marketing yang sia-sia.

`Type 2 error : False Negative` --> Resiko nya kehilangan pelanggan

Berdasarkan konsekuensinya, `False Negative` memiliki dampak yang lebih merugikan dibandingkan dengan `False Positive`. **Hal ini disebabkan oleh biaya yang lebih tinggi untuk mendapatkan pelanggan baru**. Di sektor telekomunikasi, menjaga pelanggan yang ada lebih ekonomis dibandingkan dengan mencari pelanggan baru, karena pelanggan yang ada sudah familiar dengan layanan dan produk perusahaan. Oleh karena itu, penting untuk meminimalkan kesalahan `False Negative` untuk mengurangi churn dan mengoptimalkan biaya operasional.

# Data Source

- Dataset merupakan data Customer Telecomunication yang Churn.
- Sumber dataset: [Link](https://drive.google.com/drive/folders/1_fR7R0srpZgnFnanbrmELgnK-xmzMAHp)

**Data Description**

| **Column** | **Data Type** | **Description** |
| --- | --- | --- |
| Dependents | Object | Whether the customer has dependents or not |
| Tenure | Int | Number of months the customer has stayed with the company |
| OnlineSecurity | Object | Whether the customer has online security or not |
| OnlineBackup | Object | Whether the customer has online backup or not |
| InternetService | Object | Whether the client is subscribed to Internet service |
| DeviceProtection | Object | Whether the client has device protection or not |
| TechSupport | Object | Whether the client has tech support or not |
| Contract | Object | Type of contract according to duration |
| PaperlessBilling | Object | Bills issued in paperless form |
| MonthlyCharges | Float | CAmount of charge for service on monthly bases |
| Churn | Object | Whether the customer churns or not (Target) |

# Result

Berdasarkan hasil cross-validation dengan `StratifiedKFold(n_splits=5)` dan 3 teknik Resampling (`RandomOverSampler`,`RandomUnderSampler`,`SMOTE`) 5 model klasifikasi, didapatkan model Logistic Regression menjadi model terpilih untuk dilakukan Hyperparameter Tuning dengan Recall tertinggi. Adapun hasil rata-rata Metrics Evaluation tiap modelnya pada **Data Training** adalah :

| Model | Resample | Accuracy | Precision | Recall | F1 |
| --- | --- | --- | --- | --- | --- |
| Logistic Regression | RandomOverSampler | 75.751639 | 50.658568 | 79.867299 | 61.979351 |
| Light GBM | RandomUnderSampler | 73.674064 | 48.697292 | 76.923042 | 59.611764 | 
| XGBoost | RandomUnderSampler | 72.905141 | 48.098345 | 75.592868 | 58.749923 |
| Random Forest | RandomUnderSampler | 69.688671 | 46.172945 | 68.468066 | 55.137465 |
| Decision Tree | RandomUnderSampler | 67.473603 | 43.693053 | 65.905665 | 52.524896 |

Selanjutnya model dilakukan Hyparameter Tuning menggunakan GridSearchCv dan performa model setelah dilakukan tuning juga meningkat tipis. Adapun hasil hyperparameter tuning model dengan **Data Testing** sebagai berikut:
| Prediction by Logistic Regression | Accuracy | Precision | Recall | F1 |
| --- | --- | --- | --- | --- |
| Before Tuning | 72.920892 | 49.521531	| 78.707224	| 60.792952 |
| After Tuning | 73.123732 | 49.757282 | 77.946768 | 60.740741 |
