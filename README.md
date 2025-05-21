# Laporan Proyek Machine Learning - Muhammad Fauzani Akbar

## Project Overview
Proyek ini bertujuan mengembangkan sistem rekomendasi gaya belajar siswa berbasis data performa akademik dan karakteristik demografis. Masalah ini penting karena banyak siswa mengalami kesulitan dalam menentukan metode belajar yang paling sesuai dengan kondisi pribadi mereka. Gaya belajar yang tidak sesuai dapat berdampak pada rendahnya pemahaman materi dan performa akademik.

Dengan bantuan sistem rekomendasi, pendekatan belajar yang disarankan akan lebih relevan dan personal. Sistem ini memanfaatkan teknik content-based filtering untuk mencocokkan karakteristik siswa dengan siswa lain yang memiliki profil serupa, lalu memberikan saran gaya belajar berdasarkan pola yang ditemukan.

**Tambahan**
1. Masalah ini bersifat masig dan berdampak langsung terhadap kualitas pembelajaran siswa secara umum, dimana tidak semua siswa atau bahkan guru memiliki kemampuan untuk mengenali gaya belajar yang tepat, sehingga perlu bantuan sistem rekomendasi dengan basis data.
2. **Refrensi :**
   - J. Bobadilla, F. Ortega, A. Hernando, dan A. Gutiérrez, "Recommender systems survey," *Knowledge-Based Systems*, vol. 46, hal. 109-132, 2013. [https://doi.org/10.1016/j.knosys.2013.03.012](https://doi.org/10.1016/j.knosys.2013.03.012)
   - S. Zhang, L. Yao, A. Sun, dan Y. Tay, "Deep learning based recommender system: A survey and new perspectives," *ACM Computing Surveys*, vol. 52, no. 1, hal. 1-38, 2019. [https://doi.org/10.1145/3285029](https://doi.org/10.1145/3285029)

## Business Understanding

### Proble Statement
* Siswa kesulitan menentukan metode belajar yang efektif sesua dengan kondisi dan kemampuan masing - masing.

### Goal
* Mengembangkan sistem rekomendasi gaya belajar berbasis content based filtering menggunakan data karakteristik siswa.

## Data Understanding
**Sumber :** [*kagle*] [https://www.kaggle.com/datasets/qasimrajput/perfume-recomendation](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams)

Dataset yang digunakan dalam proyek ini berisi 1000 entri data, dataset ini bersih dari missing value atau duplicated value, terdiri dari 3 variabel numerik dan 5 variabel object. 

Berikut adalah penjelasan dari masing - masing variabel dalam dataset :
* `gender`: jenis kelamin (female/male)
* `race/ethnicity`: kelompok etnis (group A-E)
* `parental level of education`: pendidikan tertinggi orang tua
* `lunch`: jenis makan siang (standard, free/reduced)
* `test preparation course`: status mengikuti kursus persiapan tes (none/completed)
* `math score`, `reading score`, `writing score`: skor ujian siswa mulai dari 0 - 100.

**TAMBAHAN**
* Univariate analysis : fokus pada satu variabel saja.
* Melakukan fungsi seperti value_counts() dan normalize = True untuk melihat distribusi kategori adalah bentuk analisis univariat terhadap fitur kategorikal.
* Output seperti :
  - "Female mendominasi gender sebesar 52%"
  - "Banyak dari siswa berasal dari Group C yaitu 31.9%"
  - ![image](https://github.com/user-attachments/assets/72eff71a-8fd0-4278-af0c-b69f7e5924f0)
 
## DATA PREPARATION
Tahapan data preparation adalah sebagai berikut :
- Encoding
- Standarisasi

**Tambahan :**
1. Encoding
   - Metode : Melakukan transformasi fitur kategorikal menjadi fitur numerik biner menggunakan OneHotEncode dari sklearn
   - Alasan :
     * Algoritma machine learning tidak bisa bekerja langsung dengan data kategorikal
     * OneHotEncoding membuat data kategorikal bisa diproses sebagai input numerik
2. Standarisasi
   - Metode : Melakukan standarisasi fitur numerik menggunakan StandardScaler dari sklearn
   - Alasan : Standarisasi memastikan semua fitur numerik berkonstribusi secara seimbang dalam perhitungan model.
  
## MODELING
Tahapan modeling pada proyek ini menggunakan pendekatan Content-Based-Filtering. Sistem ini merekomendasikan gaya belajar kepada siswa berdasarkan kesaman fitur antar siswa satu dengan yang lain, seperti skor ujian, status kursus persiapan, dan fitur demografis lainnya.
**Cara Kerja :**
1. Representasi Fitur : Semua fitur (baik itu num atau categorical) diproses dan disatukan. Data ini disimpan dalam sebuah *numpy array* bernama `FITUR`.yang diambil dari dataframe hasil *preprocessing* : `FITUR = df_preparasi.values`.
2. Menghitung Similarity : Mengukur kemiripan antar siswa, menggunakan cosine similarity, yaitu ukuran kesamaan sudut antara dua vektor : `similarity_matrix = cosine_similarity(FITUR)`.
3. Top-N Recomendation
