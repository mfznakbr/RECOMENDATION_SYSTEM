# Laporan Proyek Machine Learning - Muhammad Fauzani Akbar

## Project Overview
Pada era digital saat ini, konsumen dihadapkan dengan berbagai pilihan produk, termasuk parfum. Meskipun banyaknya pilihan dapat menguntungkan, hal ini seringkali membuat pengguna kesulitan dalam menentukan produk yang paling sesuai dengan prefensi mereka. Setiap individu memiliki selera unik terhadap aroma, intensitas, frekuensi penggunaan, hingga loyalitas terhadap merek tertentu.

Sementara itu, brand - brand parfum juga menghadapi tantangan dalam menyajikan produk yang tepat kepada target pasar yang beragam secara demografis dan psikografis. Oleh karena itu, dibutuhkan sebuah solusi yang dapat menghubungkan prefensi pengguna dengan karakteristik produk parfum secara personal dan efisien.

Beberapa studi telah menunjukan bahwa dengan memanfaatakn data historis pengguna misalnya seperti usia, gender, negara, dll, sebuah sistem rekomendasi berbasis machine learning dapat dibangun. Sistem ini akan membantu penggguna menemukan parfum paling sesuai dengan selera dan kebiasan mereka, serta meningkatkan kepuasan pelanggan dan loyalitas terhadap merek.

Proyek ini bertujuan untuk membangun sistem rekomendasi parfum yang cerdas, dengan memanfaatkan data pengguna yang kaya informasi. Dengan pendekatan ini, diharapkan pengguna dapat lebih cepat menemukan parfum ideal mereka, dan brand dapat meningkatkan efektivitas strategi pemasaran produknya.

**Tambahan**
1. Memilih parfum yang tepat bisa jadi sulit karena banyaknya pilihan produk, sehingga sering menyebabkan pembelian yang kurang memuaskan dan pemborosan. Sistem rekomendasi yang personal dapat membantu meningkatkan kepuasan pelanggan dengan memberikan saran produk yang sesuai preferensi individu. Selain itu, sistem ini membantu brand menargetkan pemasaran dengan lebih efektif berdasarkan pola perilaku konsumen. Studi menyatakan bahwa sistem rekomendasi berbasis machine learning meningkatkan akurasi rekomendasi dan pengalaman pengguna
2. **Refrensi :**
   - J. Bobadilla, F. Ortega, A. Hernando, dan A. Gutiérrez, "Recommender systems survey," *Knowledge-Based Systems*, vol. 46, hal. 109-132, 2013. [https://doi.org/10.1016/j.knosys.2013.03.012](https://doi.org/10.1016/j.knosys.2013.03.012)
   - S. Zhang, L. Yao, A. Sun, dan Y. Tay, "Deep learning based recommender system: A survey and new perspectives," *ACM Computing Surveys*, vol. 52, no. 1, hal. 1-38, 2019. [https://doi.org/10.1145/3285029](https://doi.org/10.1145/3285029)

## Business Understanding

### Proble Statement
* Pengguna seringkali mengalami kebingungan dalam memilih parfum yang sesuai dengan prefensi mereka karena banyaknya variasi aroma dan merek yang tersedia di pasaran. Ketidasesuaian pilihan parfum menyebabkan ketidakpuasan, pemborosan biaya, dan kurangnya loyalitas terhadap merek.

### Goal
Membangun sistem rekomendasi parfum berbasis machine learning mampu memberikan saran produk secara personal berdasarkan data demografis dan perilaku pengguna, sehingga dapat membantu pengguna untuk menentukan parfum yang paling sesuai dengan selera dan kebiasaanya.

## Data Understanding
**Sumber :** [*kagle*] https://www.kaggle.com/datasets/qasimrajput/perfume-recomendation

Dataset yang digunakan dalam proyek ini berisi 78.095 data pengguna parfum yang mencakup berbagai aspek demografis, psikografis, dan prefensi pengguna terhadap parfum. Dataset ini tidak memiliki missing value, duplicate value, dan tidak terindikasi outlier. 

Berikut adalah penjelasan dari masing - masing variabel dalam dataset :

### Fitur Numerik:

* **user\_id**: ID unik pengguna (tidak digunakan dalam pemodelan karena hanya sebagai identitas).
* **age**: Usia pengguna dalam tahun.
* **past\_purchase\_rating**: Rating pembelian parfum sebelumnya (1–5), merepresentasikan kepuasan atau kesesuaian produk.

### Fitur Kategorikal:

* **gender**: Jenis kelamin pengguna (`Male`, `Female`, `Other`).
* **country**: Negara asal pengguna (`India`, `US`, `Pakistan`, `UAE`, `UK`, `France`).
* **region**: Wilayah geografis pengguna (`Region-1` s.d. `Region-5`).
* **preferred\_fragrance\_family**: Jenis aroma parfum yang disukai (`Floral`, `Fruity`, `Woody`, dll).
* **budget\_range**: Rentang anggaran belanja pengguna (`Low`, `Medium`, `High`, `Luxury`).
* **brand\_loyalty**: Tingkat loyalitas pengguna terhadap merek parfum (`Low`, `Moderate`, `High`).
* **concentration\_preference**: Preferensi konsentrasi parfum (`EDP`, `EDT`, `Extrait`).
* **scent\_intensity**: Intensitas aroma yang disukai (`Light`, `Moderate`, `Strong`).
* **usage\_frequency**: Frekuensi penggunaan parfum (`Monthly`, `Quarterly`, `Yearly`).
* **rating\_sensitivity**: Seberapa sensitif pengguna dalam memberi rating produk (`Low`, `Medium`, `High`).

**TAMBAHAN**
* Univariate analysis : fokus pada satu variabel saja.
* Melakukan fungsi seperti value_counts() dan normalize = True untuk melihat distribusi kategori adalah bentuk analisis univariat terhadap fitur kategorikal.
* Output seperti :
  - "Moderate mendominasi brand_loyalty sebesar 50%"
  - "EDP jadi konsentrasi paling disukai 40%"
