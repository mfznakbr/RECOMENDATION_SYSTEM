# Laporan Proyek Machine Learning - Muhammad Fauzani Akbar

## Project Overview
Di era digital saat ini, jumlah lagu dan konten musik yang tersedia secara online terus meningkat secara eksponensial. Hal ini membuat pendengar seringkali kesulitan menemukan lagu-lagu yang sesuai dengan selera dan suasana hati mereka. Oleh karena itu, sistem rekomendasi musik menjadi solusi penting untuk membantu pengguna menemukan lagu yang relevan dan personal tanpa harus mencari secara manual.

Proyek ini mengembangkan sistem rekomendasi lagu berbasis analisis fitur audio seperti durasi, danceability, dan valence, yang bertujuan memberikan rekomendasi lagu-lagu yang memiliki karakteristik mirip dengan lagu favorit pengguna. Dengan pendekatan ini, diharapkan pengalaman mendengarkan musik menjadi lebih menyenangkan dan sesuai dengan preferensi tiap individu, sekaligus meningkatkan keterlibatan pengguna terhadap platform musik digital.

**Tambahan**
1. Masalah kesulitan menemukan lagu yang tepat sesuai selera pengguna perlu diselesaikan karena dapat mengurangi kenyamanan dan kepuasan dalam menikmati musik digital yang semakin melimpah. Dengan mengembangkan sistem rekomendasi berbasis fitur audio yang akurat dan personal, pengguna dapat dengan mudah mendapatkan lagu-lagu yang relevan tanpa harus melakukan pencarian manual yang memakan waktu. Pendekatan ini tidak hanya meningkatkan pengalaman pengguna tetapi juga membantu platform musik dalam mempertahankan dan memperluas basis penggunanya.
2. **Refrensi :**
   - J. Bobadilla, F. Ortega, A. Hernando, dan A. Gutiérrez, "Recommender systems survey," *Knowledge-Based Systems*, vol. 46, hal. 109-132, 2013. [https://doi.org/10.1016/j.knosys.2013.03.012](https://doi.org/10.1016/j.knosys.2013.03.012)
   - S. Zhang, L. Yao, A. Sun, dan Y. Tay, "Deep learning based recommender system: A survey and new perspectives," *ACM Computing Surveys*, vol. 52, no. 1, hal. 1-38, 2019. [https://doi.org/10.1145/3285029](https://doi.org/10.1145/3285029)

## Business Understanding

### Proble Statement
* Pengguna terkadang kesulitan menemukan lagu yang benar - benar sesuai dengan prefensi dan suasana hati mereka secara cepat dan akurat karena jumlah lagu yang tersedia sangat banyak.

### Goal
* Mengembangkan sistem rekomendasi lagu berbasis content-based filtering yang memanfaatkan fitur durasi, danceability, dan valence untuk memberikan rekomendasi lagu-lagu yang paling mirip dan relevan dengan lagu favorit pengguna, sehingga meningkatkan kepuasan dan pengalaman mendengarkan musik.

## Data Understanding
**Sumber :** [*kagle*] [[https://www.kaggle.com/datasets/qasimrajput/perfume-recomendation](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams)](https://www.kaggle.com/datasets/geomack/spotifyclassification/data)

Dataset yang digunakan dalam proyek ini berisi 2017 entri data, dataset ini bersih dari missing value atau duplicated value, terdiri dari 3 variabel numerik dan 5 variabel object. 

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
3. Top-N Recomendation : 5 siswa yang paling mirip dengan siswa ke-9 
   [(914, np.float64(0.9259905979991441)),
 (794, np.float64(0.9223807734647653)),
 (396, np.float64(0.9208315030860833)),
 (842, np.float64(0.9040530058932298)),
 (980, np.float64(0.9032403073536728))]

## EVALUASI 
Untuk mengevaluasi sistem rekomendasi ini, digunakan Cosine Similarity sebagai metrik utama. Metrik ini umum digunakan dalam sistem rekomendasi berbasis content-based filtering karena mampu mengukur tingkat kemiripan antar entitas berdasarkan sudut antar vektor fitur.
Berdasarkan output, siswa ke-9 paling mirip dengan siswa ke-914, 794, 396, dst., dengan skor kemiripan lebih dari 0.90. Ini menunjukkan bahwa sistem dapat mengidentifikasi kelompok siswa yang memiliki karakteristik belajar yang sangat serupa.

Metrik ini sesuai terutama dengan problem statement dan Goals, karena :
* Cosine similarity menghitung seberapa mirip dua siswa berdasarkan fitur-fitur mereka (nilai matematika, membaca, menulis, dan status kursus).
* Dengan nilai similarity yang tinggi, kita bisa yakin bahwa dua siswa tersebut memiliki profil belajar yang mirip.
* Maka, gaya belajar yang cocok untuk siswa A kemungkinan besar juga akan cocok untuk siswa B jika similarity-nya tinggi.

**Tambahan**
### Formula Cosine Similarity

$$
\text{Cosine Similarity} = \frac{A \cdot B}{\|A\| \|B\|}
$$

Di mana:

* \$A\$ dan \$B\$ adalah **vektor fitur dua siswa**
* \$A \cdot B\$ adalah **perkalian dot product** antara kedua vektor
* \$|A|\$ dan \$|B|\$ adalah **magnitudo (panjang)** dari masing-masing vektor

Nilai Cosine Similarity berada dalam rentang **0 hingga 1**:

* **1** berarti dua siswa sangat mirip
* **0** berarti mereka sangat berbeda
