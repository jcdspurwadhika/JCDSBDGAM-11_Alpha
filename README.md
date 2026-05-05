# JCDSBDGAM-11_Alpha
****
# Hotel Cancellation Risk Prediction
****
### Latar Belakang
****
Sebuah hotel di Portugal mengalami penurunan pendapatan tahunan sebesar ~37% akibat pembatalan reservasi. Setiap kamar yang tidak terisi adalah perishable inventory berpotensi pendapatan hilang selamanya. Manajemen tidak memiliki sistem peringatan dini untuk mengidentifikasi pemesanan berisiko tinggi. 

Akibatnya:

- Tidak bisa melakukan overbooking yang terukur.

- Tidak bisa menawarkan intervensi preventif (misal: upsell, reminder, deposit non‑refundable).

- Efisiensi operasional terganggu (staffing, persediaan, revenue management).

[*Industri perhotelan*](https://link.springer.com/article/10.1007/s40558-025-00349-9) merupakan sektor jasa yang sangat bergantung pada kemampuan dalam mengelola permintaan pelanggan secara efektif.Permintaan terhadap kamar hotel tidak bersifat konstan, melainkan berfluktuasi seiring waktu akibat berbagai faktor seperti musim, perilaku wisatawan, serta dinamika ekonomi. Oleh karena itu, pemahaman terhadap pola permintaan menjadi aspek penting dalam menjaga kinerja operasional dan finansial hotel.

Salah satu mekanisme utama dalam pengelolaan permintaan adalah sistem reservasi, di mana pelanggan melakukan pemesanan sebelum tanggal kedatangan. Meskipun sistem ini membantu perencanaan, fleksibilitas yang diberikan kepada pelanggan juga memunculkan potensi pembatalan reservasi. [**Tingginya tingkat pembatalan dapat menyebabkan ketidaksesuaian antara permintaan yang diperkirakan dengan realisasi hunian**](https://www.hftp.org/news/4128776/free-hotel-cancellations-smart-strategy-or-revenue-risk)

---
****
### Problem Statement
****
## 1. Permasalahan Utama (Primary Problem) Hypothesis
Tingginya tingkat pembatalan reservasi **(cancellation rate)** menyebabkan ketidakpastian dalam perencanaan okupansi, yang berdampak langsung terhadap potensi kehilangan pendapatan **(revenue loss)** dan inefisiensi operasional hotel.

Untuk mengatasi permasalahan tersebut, diperlukan pendekatan berbasis data yang mampu mengidentifikasi reservasi dengan risiko pembatalan sejak awal proses pemesanan.

Oleh karena itu **Permasalahan utama dalam project ini adalah:**
<blockquote style="background: #CDDDF6; padding: 10px; border-left: 4px solid #A6C5F2; margin: 10px 0;">
<ul>
    <li>Bagaimana memanfaatkan data historis pemesanan untuk memprediksi probabilitas pembatalan reservasi secara akurat, .</li>
    <li>sehingga hotel dapat melakukan intervensi proaktif (seperti reminder, penyesuaian kebijakan deposit, atau strategi overbooking) guna meminimalkan revenue loss.</li>
</ul>
</blockquote>

Model yang dikembangkan bertujuan sebagai early warning system yang dapat membantu tim revenue management dan operasional dalam mengambil keputusan berbasis risiko.

Sebagai target performa, model diharapkan:

- Mampu mencapai recall ≥ 0,75 pada kelas pembatalan, untuk meminimalkan risiko false negative (booking berisiko tinggi yang tidak terdeteksi)

- Dengan tetap mempertimbangkan trade-off terhadap precision agar intervensi tetap efisien secara operasional

---

## 2. Pertanyaan Analitis Spesifik (Specific Analytical Questions)

Untuk menjawab permasalahan utama, project ini dirumuskan ke dalam beberapa pertanyaan analitis berikut:

| No | Pertanyaan Analitis                                                             | Tujuan                                               |
| -- | ------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| 1  | Berapa tingkat pembatalan dan apakah terjadi class imbalance?                   | Menentukan baseline risiko dan kebutuhan strategi modeling |
| 2  | Faktor apa yang paling mempengaruhi pembatalan?                                 | Mengidentifikasi driver utama untuk intervensi             |
| 3  | Bagaimana perilaku customer berisiko tinggi? (lead_time, deposit, segment, dll) | Membentuk segmentasi risiko                                |
| 4  | Model mana yang paling optimal dalam mendeteksi pembatalan?                     | Memilih model terbaik untuk implementasi                   |
| 5  | Berapa potensi revenue yang dapat diselamatkan jika model digunakan?            | Justifikasi bisnis implementasi model                      |


---
****
### Goals
****
Analisis difokuskan untuk menjawab pertanyaan kunci:

**“Booking seperti apa yang berisiko tinggi dibatalkan, dan bagaimana hotel dapat bertindak sebelum pembatalan terjadi?”**

Dengan pendekatan ini, model yang dikembangkan tidak hanya berfungsi sebagai alat prediksi, tetapi diharapkan juga sebagai:

- Risk scoring system untuk mengklasifikasikan tingkat risiko pembatalan pada setiap reservasi

- Early warning system untuk mendeteksi potensi pembatalan sejak awal proses booking

- Decision support tool untuk membantu tim operasional dan revenue management dalam menentukan strategi intervensi yang lebih tepat sasaran

| Tahapan                                 | Fokus Utama                                                                                                               | Output yang Diharapkan                |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------- |
| **Data Understanding**                  | Mengidentifikasi struktur data, kualitas data, serta potensi risiko seperti missing value, duplicate, dan class imbalance | Pemahaman awal + potensi issue        |
| **EDA (Hypothesis-driven)**             | Menguji hipotesis terkait faktor pembatalan (lead time, deposit, segment, dll)                                            | Insight tentang driver cancellation   |
| **Data Cleaning & Feature Engineering** | Memastikan data siap modeling dan mencerminkan perilaku customer                                                          | Dataset yang lebih representatif      |
| **Modeling**                            | Membangun model untuk mengidentifikasi booking berisiko tinggi                                                            | Model prediksi risiko                 |
| **Evaluation (Business-oriented)**      | Evaluasi model dengan fokus pada recall dan trade-off bisnis                                                              | Model yang relevan secara operasional |
| **Business Impact Analysis**            | Mengukur potensi pengurangan cancellation dan peningkatan revenue                                                         | Justifikasi implementasi model        |
| **Deployment Scenario**                 | Simulasi penggunaan model dalam sistem operasional                                                                        | Gambaran implementasi nyata           |
****
### Analytical Approach
****
1. Data Collection & Preprocessing
- Handling missing values, duplicate removal
- Feature engineering dan selection
  
2. Exploratory Data Analysis (EDA)

Analisis distribusi target is_canceled:
- Proporsi booking dibatalkan (1) vs tidak dibatalkan (0)
- Cek keseimbangan data (imbalanced vs balanced)
  
Univariate Analysis (Analisis Satu Variabel)
- Variabel numerik: Statistik deskriptif, Distribusi (histogram / boxplot)
- Variabel kategorikal: Frekuensi tiap kategori, Proporsi kategori

Bivariate Analysis (Analisis Dua Variabel), Melihat hubungan antara fitur dengan target (is_canceled):
- deposit_type vs cancellation
- lead_time vs cancellation
- market_segment vs cancellation
- Visualisasi:
- Bar chart
- Boxplot
- Crosstab

Multivariate Analysis, Korelasi antar variabel numerik:
- Heatmap korelasi
- Identifikasi fitur yang paling berpengaruh terhadap target

3. Machine Learning Modeling
- Binary classification problem (canceled vs non-canceled)
- Algoritma: Logistic Regression, Decision Tree, Random Forest, XGBoost
- Handling imbalanced data: SMOTE, RandomOverSampler, RandomUnderSampler, NearMiss, class_weight='balanced'
- Hyperparameter tuning: RandomizedSearchCV
  
4. Model Interpretation
SHAP values untuk explainability

****
### Metrics Evaluation
****
- **Data Tidak Seimbang**: Dengan hanya 28% kelas positif, akurasi akan menyesatkan karena akan selalu memprediksi "tidak ada pembatalan"
- **Pertimbangan Biaya**: Rasio biaya FP/FN yang dramatis (3:1) membuat false positive jauh lebih mahal dibandingkan false negative
- **Metrik yang Dipilih**: **F-beta** adalah metrik optimal untuk skenario ini karena kita mementingkan kedua metrik antara recall dan precision
  
$$F_\beta = \frac{1 + \beta^2}{\frac{\beta^2}{\text{Recall}} + \frac{1}{\text{Precision}}}$$

Keterangan:
- untuk **F-0.5 Score, β = 0.5**
- **Presisi** = TP / (TP + FP) - Proporsi pengunjung yang diprediksi akan membatalkan pemesanan dan benar-benar membatalkan pemesanan

- **Recall** = TP / (TP + FN) - Proporsi pelanggan yang benar-benar membatalkan pemesanan dan teridentifikasi dengan tepat

- **β = 0.5** berarti precision diberi bobot **4x** lebih penting daripada recall

****
### Dataset Description
****
- Dataset: Kaggle-Hotel booking demand
- Total Data: 86,940 Transaksi pemesanan kamar hotel
- Features: 32 columns (setelah cleaning dan feature engineering)
- Target Variable: is_canceled (Yes/No atau 1/0)
- Key Features:
<div style="padding:6px 10px; margin:12px 0; background-color:#368412; color:white; font-weight:600; border-radius:6px;">
    Struktur Variabel
</div>

<table style="border-collapse:collapse; width:100%;">
<thead>
<tr style="background-color:#f2f2f2;">
<th style="padding:8px; border:1px solid #ddd;">Kategori</th>
<th style="padding:8px; border:1px solid #ddd;">Contoh Variabel</th>
<th style="padding:8px; border:1px solid #ddd;">Peran dalam Analisis</th>
</tr>
</thead>
<tbody>
<tr>
<td style="padding:8px; border:1px solid #ddd;"><b>Waktu & Durasi</b></td>
<td style="padding:8px; border:1px solid #ddd;">lead_time, arrival_date_month, stays_in_week_nights</td>
<td style="padding:8px; border:1px solid #ddd;">Menentukan pola waktu dan perilaku booking</td>
</tr>
<tr>
<td style="padding:8px; border:1px solid #ddd;"><b>Profil Tamu</b></td>
<td style="padding:8px; border:1px solid #ddd;">adults, children, country</td>
<td style="padding:8px; border:1px solid #ddd;">Segmentasi customer</td>
</tr>
<tr>
<td style="padding:8px; border:1px solid #ddd;"><b>Market & Channel</b></td>
<td style="padding:8px; border:1px solid #ddd;">market_segment, distribution_channel</td>
<td style="padding:8px; border:1px solid #ddd;">Sumber demand</td>
</tr>
<tr>
<td style="padding:8px; border:1px solid #ddd;"><b>Perilaku Customer</b></td>
<td style="padding:8px; border:1px solid #ddd;">previous_cancellations, booking_changes</td>
<td style="padding:8px; border:1px solid #ddd;">Indikator risiko pembatalan</td>
</tr>
<tr>
<td style="padding:8px; border:1px solid #ddd;"><b>Finansial</b></td>
<td style="padding:8px; border:1px solid #ddd;">adr, deposit_type</td>
<td style="padding:8px; border:1px solid #ddd;">Nilai revenue & komitmen pembayaran</td>
</tr>
<tr>
<td style="padding:8px; border:1px solid #ddd;"><b>Status Akhir</b></td>
<td style="padding:8px; border:1px solid #ddd;">reservation_status</td>
<td style="padding:8px; border:1px solid #ddd;">Outcome (tidak digunakan untuk modeling)</td>
</tr>
</tbody>
</table>

****
### Business Insight & Findings
****
**Key Findings**

<li><b>Cancellation adalah masalah multi-faktor, bukan single driver</b><br>
Tidak ada variabel tunggal dengan korelasi kuat terhadap pembatalan. 
Risk terbentuk dari kombinasi <b>timing (lead time), value (ADR), dan behavior (customer intent)</b>.</li>

<li><b>Lead time adalah driver paling konsisten</b><br>
Semakin jauh waktu booking, semakin tinggi ketidakpastian -> cancel rate meningkat signifikan hingga >50% pada very early booking.</li>

<li><b>Harga (ADR) memperbesar risiko pada kondisi tertentu</b><br>
ADR bukan faktor utama secara linear, tetapi menjadi <b>risk amplifier</b> ketika dikombinasikan dengan lead time tinggi.</li>

<li><b>Customer behavior lebih penting daripada pricing</b><br>
- Special requests -> menurunkan cancel (indikasi komitmen)<br>
- Previous cancellations -> meningkatkan cancel (repeat behavior)</li>

<li><b>Channel & segment menentukan tingkat fleksibilitas</b><br>
- OTA / Online TA -> cancel rate tinggi (fleksibel)<br>
- Direct / Corporate -> lebih stabil (komitmen tinggi)</li>

<li><b>Deposit policy adalah kontrol paling efektif terhadap revenue risk</b><br>
- No deposit -> risiko kehilangan revenue tertinggi<br>
- Non refundable -> cancel tinggi, tapi revenue relatif aman</li>

**1. Faktor Utama Penyebab Cancellation**
</div>

<ul>
<li><b>Lead Time (Driver Utama)</b><br>
Semakin jauh waktu booking, semakin tinggi ketidakpastian maka risiko cancel meningkat signifikan</li>

<li><b>Customer Intent (Penentu Komitmen)</b><br>
- Special requests : menurunkan cancel (high intent)<br>
- Previous cancellations : meningkatkan cancel (repeat behavior)</li>

<li><b>Pricing sebagai Risk Amplifier</b><br>
Harga tidak berdampak secara langsung, tetapi memperbesar risiko pada booking dengan lead time tinggi</li>
</ul>

---
 **2. Segmentasi High-Risk Customer**
</div>

<ul>
<li><b>High Risk Segment</b><br>
Booking dengan <b>lead time panjang + harga tinggi</b> -> probabilitas cancel tertinggi</li>

<li><b>Low Risk Segment</b><br>
Booking last minute : menunjukkan komitmen tinggi dan cancel rate rendah</li>

<li><b>Behavioral Risk</b><br>
Customer dengan riwayat cancel : akan cenderung mengulang perilaku yang sama</li>

</ul>

---
  **3. Channel dengan Risiko Tertinggi**
</div>

<ul>
<li><b>Online TA / OTA</b><br>
Memiliki cancel rate tertinggi karena fleksibilitas tinggi dalam perubahan booking</li>

<li><b>Direct & Corporate</b><br>
Lebih stabil karena komitmen lebih tinggi dan proses booking lebih terkontrol</li>

<li><b>Channel = Level of Control</b><br>
Semakin fleksibel channel, semakin tinggi risiko pembatalan</li>
</ul>

---

 **4. Dampak terhadap Revenue & Occupancy**
</div>

<ul>
<li><b>Cancellation tidak selalu berarti revenue loss</b><br>
Pada booking non refundable, hotel tetap menerima pembayaran meskipun terjadi pembatalan</li>

<li><b>Revenue Risk berasal dari No Deposit</b><br>
Booking tanpa deposit memiliki risiko kehilangan revenue tertinggi</li>

<li><b>Peluang Double Revenue</b><br>
Jika kamar dari no show dapat dijual kembali, hotel berpotensi mendapatkan revenue tambahan</li>

<li><b>Fokus utama: Revenue Risk, bukan Cancellation Rate</b><br>
Strategi bisnis harus berfokus pada dampak finansial, bukan hanya jumlah pembatalan</li>
</ul>

****
### Machine Learning Results
****
- Model Terbaik: XGBoost Classifier + class_weight
- Hyperparameters:
param_spacexgb = {

    "model__max_depth"        : [3, 4, 5, 6],
  
    "model__min_child_weight" : [3, 5, 7, 10],
  
    "model__gamma"            : [0.1, 0.3, 0.5],
  
    "model__subsample"        : [0.6, 0.7, 0.8],
  
    "model__colsample_bytree" : [0.6, 0.7, 0.8],
  
    "model__reg_alpha"        : [0.1, 0.5, 1.0],
  
    "model__reg_lambda"       : [1.0, 2.0, 5.0],
  
    "model__learning_rate"    : [0.01, 0.05, 0.1],
  
    "model__n_estimators"     : [100, 200, 300],
  
    "model__scale_pos_weight" : [1, 2, 3]}

**Performance Metrics:**
- *Sebelum Tunning*: basexgb MODEL
  
fbeta Train = 67.34%

fbeta Test = 62.86%

- *Setelah Tunning*: bestxgb MODEL
  
fbeta Train = 75.62%

fbeta Test = 70.87%

**Business Impact**

*Tanpa Model:*

- Prediksi semua = 0 (tidak batal) --->
Total Cost: 4,761 x -105 euro = **-499,905 euro**
- Prediksi semua = 1 (batal) ---> 
Total Cost: 2,268 × 300 = **-3,680,400 euro**

*Dengan Model:*

- Base Model --->
Total Cost= **-894,585 euro**
- Best Model --->
Total Cost: **-484,115 euro** ->
Penghematan: **15,75 euro**

Model XGBoost best dapat mengidentifikasi tamu hotel yang kemungkinan besar akan membatalkan pemesanan mereka dengan **akurasi 75.14%**, artinya dari setiap 100 tamu yang diprediksi akan membatalkan, sekitar 75 tamu benar-benar akan membatalkan pemesanan, sehingga hotel dapat melakukan intervensi yang lebih tepat sasaran dan efisien.

**Business Recommendations**

- **Terapkan model dalam sistem manajemen pemesanan hotel** untuk menandai tamu berisiko tinggi pembatalan pada saat pemesanan dilakukan, memungkinkan tim revenue management untuk secara selektif melakukan tindakan intervensi hanya kepada tamu yang diprediksi akan membatalkan, dengan target penghematan **15,750 euro per 17.029 pemesanan** dibandingkan tidak menggunakan model sama sekali, dan **410,430 euro** dibandingkan model tanpa tuning.
-  **Prioritaskan penanganan segmen pasar berisiko tinggi** yang diidentifikasi oleh SHAP plot seperti segmen **Online Travel Agent (OTA)** dan tamu dengan **histori pembatalan sebelumnya**, dengan menerapkan kebijakan pemesanan yang lebih ketat seperti deposit wajib atau batas waktu konfirmasi lebih awal, untuk menekan angka **2.011 pembatalan yang tidak terdeteksi** dan mengurangi kerugian FN sebesar **211,155 euro**

- **Integrasikan model dengan sistem Early Warning Dashboard** yang menampilkan daftar tamu berisiko tinggi secara real-time kepada tim operasional hotel setiap hariny

**Fitur yang mempengaruhi pembatalan berdasarkan SHAP**

- `country_6`; Tamu yang berasal dari negara tertentu (nilai merah/tinggi) mendorong prediksi ke arah pembatalan secara signifikan. Hal ini menunjukkan bahwa asal negara tamu merupakan faktor paling dominan dalam menentukan risiko pembatalan, kemungkinan mencerminkan perbedaan budaya pemesanan, kebijakan visa, jarak perjalanan, serta kebiasaan perencanaan liburan antar negara yang berbeda-beda, sehingga tamu dari negara tertentu secara konsisten menunjukkan pola pembatalan yang lebih tinggi dibandingkan negara lainnya.

- `lead_time`; Tamu yang memesan jauh hari sebelum tanggal kedatangan (nilai merah/tinggi) mendorong prediksi ke arah pembatalan secara kuat. Hal ini menunjukkan bahwa semakin panjang jarak waktu antara tanggal pemesanan dan tanggal kedatangan, semakin tinggi ketidakpastian rencana perjalanan tamu, sementara tamu yang memesan mendekati tanggal kedatangan cenderung memiliki komitmen yang lebih kuat dan jarang membatalkan pemesanan mereka.

- `required_car_parking_spaces`; Tamu yang memesan tempat parkir kendaraan (nilai merah/tinggi) justru mendorong prediksi menjauh dari pembatalan. Hal ini mengindikasikan bahwa tamu yang meminta fasilitas parkir memiliki tingkat komitmen dan keseriusan yang lebih tinggi terhadap rencana menginap mereka, karena mereka telah merencanakan perjalanan secara lebih detail termasuk transportasi pribadi, sehingga menjadi indikator loyalitas tamu yang kuat.

- `total_of_special_requests`; Tamu dengan jumlah permintaan khusus yang sedikit (nilai biru/rendah) cenderung mendorong prediksi menjauh dari pembatalan, sementara tamu dengan banyak permintaan khusus (nilai merah/tinggi) sedikit mendorong ke arah pembatalan. Hal ini menunjukkan bahwa tamu yang memiliki banyak ekspektasi spesifik terhadap layanan hotel lebih rentan membatalkan pemesanan apabila permintaan mereka tidak dapat dipenuhi atau terdapat ketidaksesuaian antara harapan dan kondisi aktual hotel.

- `market_segment`; Segmen pasar tertentu (ditangkap melalui pengkodean biner) mendorong prediksi ke arah pembatalan secara berbeda-beda. Hal ini menunjukkan bahwa saluran pemesanan memainkan peran penting dalam perilaku pembatalan tamu, di mana segmen Online Travel Agent (OTA) cenderung memiliki tingkat pembatalan lebih tinggi karena kemudahan proses pembatalan dan kebijakan refund yang fleksibel, sementara tamu yang memesan secara langsung (direct booking) menunjukkan komitmen yang lebih kuat terhadap pemesanan mereka.

- `adr (Average Daily Rate)`; Tamu yang memesan kamar dengan harga per malam yang tinggi (nilai merah/tinggi) mendorong prediksi ke arah pembatalan. Hal ini menunjukkan bahwa tamu yang membayar tarif kamar lebih mahal cenderung lebih sensitif terhadap perubahan harga dan kondisi, lebih sering membandingkan pilihan akomodasi lain, serta lebih berani membatalkan pemesanan apabila menemukan penawaran yang lebih baik atau terjadi perubahan rencana perjalanan.

- `deposit_type_Non Refund`; Tamu yang memilih tipe deposit Non-Refund (nilai merah/tinggi) mendorong prediksi menjauh dari pembatalan secara signifikan. Hal ini membuktikan bahwa kebijakan deposit Non-Refund sangat efektif dalam mencegah pembatalan, karena tamu yang telah membayar deposit yang tidak dapat dikembalikan memiliki konsekuensi finansial yang jelas apabila membatalkan pemesanan, sehingga mendorong mereka untuk tetap melanjutkan rencana menginap.

- `previous_cancellations`; Tamu yang memiliki riwayat pembatalan sebelumnya yang tinggi (nilai merah/tinggi) mendorong prediksi ke arah pembatalan dengan kuat. Hal ini menegaskan bahwa histori perilaku pembatalan merupakan prediktor yang sangat kuat, di mana tamu yang pernah membatalkan pemesanan di masa lalu memiliki kecenderungan yang jauh lebih tinggi untuk kembali membatalkan pemesanan berikutnya, sehingga riwayat tamu perlu menjadi pertimbangan utama dalam strategi manajemen risiko pembatalan hotel.
****
### Tech Stack 
****
- Data Processing & Analysis: Python, pandas, numpy, scipy, statsmodels
- Visualization: matplotlib, seaborn, folium (geospatial heatmap), Tableau Public
- Machine Learning:scikit-learn, XGBoost, imbalanced-learn, SHAP, category-encoders
- Deployment: Streamlit, pickle (model persistence)
****
**Link Tableau** : https://public.tableau.com/views/PortugalHotelBookingDemandDashboard/Dashboard?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link

**Link Streamlit**: https://finpro-ds-it39wabbxb2kztzj9axplu.streamlit.app/

**Link PPT**: https://canva.link/wa75modrbdwgi1t

****
### Dokumentasi
****
**Dokumentasi Tableau**
<img width="750" height="544" alt="Dasboard" src="https://github.com/user-attachments/assets/67a094f9-37e9-4ef5-bdb5-bb8acce54731" />

**Dokumentasi Streamlit**
<img width="1920" height="812" alt="App streamlit" src="https://github.com/user-attachments/assets/01aea18b-714e-4fe7-8412-5ec23d907cfe" />
