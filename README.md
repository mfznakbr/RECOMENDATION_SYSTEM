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

Dataset yang digunakan dalam proyek ini berisi 2017 entri data, dataset ini bersih dari missing value atau duplicated value, terdiri dari 15 variabel numerik dan 2 variabel object. 

Berikut adalah penjelasan dari masing - masing variabel dalam dataset :
* `Unnamed: 0`: ID unik setiap baris data
* `acousticness`: tingkat keakustikan lagu, nilai antara 0-1 (semakin tinggi makin akustik)
* `danceability`: seberapa cocok lagu untuk menari, nilai antara 0-1
* `duration_ms`: durasi lagu dalam milidetik
* `energy`: intensitas dan kekuatan lagu, nilai antara 0-1
* `instrumentalness`: seberapa instrumental sebuah lagu, nilai antara 0-1
* `key`: nada dasar lagu dalam angka (0-11)
* `liveness`: kemungkinan ada suara penonton/live, nilai antara 0-1
* `loudness`: tingkat keras lagu dalam decibel (dB)
* `mode`: mode musik (mayor = 1, minor = 0)
* `speechiness`: seberapa banyak elemen bicara dalam lagu, nilai antara 0-1
* `tempo`: kecepatan lagu dalam BPM (beats per minute)
* `time_signature`: jumlah ketukan per birama
* `valence`: kesan emosional lagu (bahagia/sedih), nilai antara 0-1
* `target`: label target, bisa berarti lagu disukai atau tidak (0/1)
* `song_title`: judul lagu
* `artist`: nama artis atau band pembuat lagu

**TAMBAHAN**
* Univariate analysis : fokus pada satu variabel saja.
* Melakukan fungsi seperti value_counts() dan normalize = True untuk melihat distribusi kategori adalah bentuk analisis univariat terhadap fitur kategorikal. Serta menggunakan heatmap untuk melihat korelasi antar fitur numerik
* Output seperti :
  - "Disukai mendominasi target sebesar 50.57%"
  - ![image](https://github.com/user-attachments/assets/5b372454-a6f0-4691-a7df-010d4a9b32b6)

  - "terdapat korelasi tinggi antar fitur tertentu, seperti energy dan loudness (0.76)"
  - ![image](https://github.com/user-attachments/assets/095f0abb-87a9-4b31-96f5-e8de9036d162)

 
## DATA PREPARATION
Tahapan data preparation adalah sebagai berikut :
- Pengecekan missing value dan duplicated value
- Ekstraksi Fitur ke List
- Buat Dataframe Untuk Model Sistem Rekomendasi
- Normalisasi Fitur Numerik.

**Tambahan :**
1. Pengecekan Missing Value dan Duplicate Value
   - Metode : menggunakan fungsi isna().sum() untuk melihat jumlah missing value dan fungsi dupilcated().sum() untuk melihat adakah indikasi duplicate
   - Hasil : Tidak ada missing value ataupun duplicated value dalam dataset.
   - Alasan : Penting untuk memastikan integritas data sebelum lanjut ke tahap modeling atau tahap preparation selanjutnya. 
2.    Ekstrasi Fitur ke List
   - Metode : Menggunakan fungsi tolist() untuk beberapa kolom ialah :
     * artist
     * single_title
     * valence
     * danceability
     * duration_ms
   - Alasan :
     * fitur tersebut mewakili karakteristik konten lagu yang akan digunakan dalam model rekomendasi berbasis content-based-filtering.
     * fitur numerik seperti valence, danceability, dan duration_ms dipilih karena memiliki konstribusi signifikan dalam mengukur kemiripan antar lagu 
3. Buat Dataframe untuk Sistem Rekomendasi.
   - Metode : Menggunakan fungsi pd.DataFrame untuk membuat dataframe dari kolom yg telah di ekstraksi. Mengubah nama kolom agar lebih mudah dibaca seperti :
     * "song_title" diubah menjadi "Judul Lagu"
     * "artist" tetap
     * "duration_ms" menjadi "Durasi /mildetik"
     * "danceability" tetap
     * "valence" menjadi "tingkat keceriaan"
   - Alasan : Dengan menggabungkan semua fitur yang dipilih ke dalam dataframe, proses seperti normalisasi akan jadi lebih efisien
4. Normalisasi Fitur Numerik.
   - Metode: Menggunakan `MinMaxScaler` dari `sklearn.preprocessing` untuk menormalisasi kolom:
  * `valence`
  * `danceability`
  * `duration_ms`
   - Alasan : Normalisasi penting agar fitur-fitur tersebut berada dalam skala yang sama (0–1), sehingga tidak ada fitur yang mendominasi perhitungan kemiripan
  
## MODELING
🎵 **Penjelasan Sistem Rekomendasi Sistem Content-Based Filtering**

Sistem rekomendasi yang digunakan pada proyek ini adalah content-based-filtering yaitu teknik yang memberikan rekomendasi berdasarkan kemiripan konten (fitur) dari item yang sudah dipilih pengguna. Dalam kasusu ini, sistem akan memberikan rekomendasi lagu - lagu yang memiliki karakteristik serupa dengan lagu yang dipilih, berdasarkan fitur seperti : 
* durasi (durasi lagu dalam mildetik)
* danceability(seberapa cocok lagu untuk dance)
* valence (tingkat keceriaan lagu)

♦️ **Alasan Pemilihan Cosine Similarity** 
Untuk mengukur kemiripan antar lagu berdasarkan ketiga fitur tersebut, digunakan **Cosine Similarity**. Cosine Similarity menghitung sudut antar dua vektor dalam ruang multidimensi, bukan jarak absolut. Ini cocok digunakan karena :
1. Independen terhadap skala fitur: Cosine similarity mempertimbangkan arah vektor, bukan besarnya, sehingga cocok saat fitur sudah dinormalisasi.
2. Fokus pada pola, bukan magnitude: Dua lagu dengan nilai absolut yang berbeda tapi pola fitur yang mirip (misalnya valence tinggi dan danceability tinggi) tetap dianggap mirip.
3. Sesuai untuk data numerik berdimensi rendah hingga sedang, seperti tiga fitur musik yang digunakan di sini.

🦾 **Cara Kerja Fungsi rekomendasi_lagu**
berikut beberapa langkah - langkah pada fungsi :
1. Validasi input : cek apakah lagu yang diminta ada pada dataset.
2. Ambil index lagu : cari posisi lagu pada data frame.
3. Hitung skor similarity : Menggunakan cosine_similarity antar lagu yang sudah dinormalisasi.
4. Urutkan skor tertinggi: Lagu-lagu lain diurutkan berdasarkan kemiripan terhadap lagu input.
5. Ambil Top-k: Mengambil k lagu dengan skor kemiripan tertinggi (tidak termasuk lagu itu sendiri).
6. Tampilkan output: Lagu-lagu mirip ditampilkan berdasarkan fitur kontennya.

Tujuan proyek ini adalah membuat ssitem yang dapat merekomendasikan lagu berdasarkan beberapa fitur, bukan berdasarkan popularitas atau perilaku pengguna. Oleh karena itu, pendekatan content based filtering sangat cocok, karena :
- Tidak bergantung pada histori pengguna
- Rekomendasi berbasis karakteristik produk itu sendiri which is lagu pada project ini.
  
## EVALUASI 
Untuk mengevaluasi performa sistem rekomendasi berbasis content based filtering digunakan metrik precision. Metrik ini digunakan untuk mengukur proporsi lagu yang relevan (disukai) dari total lagu yang direkomendasikan.

**Alasan Pemilihan Metrik Precision :**
Karena sistem ini merekomendasikan lagu berdasarkan kemiripan fitur kontennya (durasi, danceability, dan valence), maka kita perlu tahu apakah lagu-lagu tersebut benar-benar sesuai dengan preferensi pengguna. Label target (1 = suka, 0 = tidak suka) digunakan sebagai indikator relevansi. Oleh karena itu, precision adalah metrik yang paling tepat digunakan.

**Kesimpulan** :
Dengan nilai **precision sebesar 60%**, sistem rekomendasi ini telah berhasil memberikan hasil yang relevan untuk sebagian besar lagu yang direkomendasikan. Ini menunjukkan bahwa pendekatan **content-based filtering** dengan **cosine similarity** pada fitur-fitur musik seperti **durasi**, **danceability**, dan **valence** mampu mengenali karakteristik lagu yang mirip dan menyajikan rekomendasi yang sesuai dengan preferensi pengguna.

Hal ini sejalan dengan **problem statement** yang diangkat, yaitu **pengguna sering kesulitan menemukan lagu yang benar-benar sesuai dengan preferensi dan suasana hati mereka secara cepat dan akurat**, terutama di tengah banyaknya pilihan lagu yang tersedia. Sistem ini membantu mengatasi masalah tersebut dengan menyaring dan menyarankan lagu-lagu yang secara konten memiliki kemiripan tinggi dengan lagu favorit pengguna.

Selain itu, hasil ini juga mendukung **goal proyek**, yaitu mengembangkan sistem rekomendasi berbasis content-based filtering yang dapat **meningkatkan pengalaman dan kepuasan pengguna dalam mendengarkan musik**. Dengan mempertimbangkan aspek-aspek musikal seperti *mood* (valence), *energi* lagu (danceability), dan *durasi*, sistem ini memberikan rekomendasi yang tidak hanya teknis relevan, tetapi juga sesuai dengan emosi atau suasana yang diinginkan pengguna.

Namun demikian, hasil precision sebesar 60% juga menunjukkan bahwa masih ada **ruang untuk peningkatan**, misalnya dengan menambahkan fitur lain (seperti genre, artist similarity, atau mood tagging) atau menggabungkan pendekatan ini dengan metode hybrid agar hasil rekomendasi menjadi lebih personal dan akurat.

**Tambahan**
### Precision
**Precision** adalah metrik evaluasi yang digunakan untuk mengukur seberapa banyak item yang direkomendasikan benar-benar relevan.

**Rumus precision:**

$$
\text{Precision} = \frac{\text{Jumlah lagu relevan yang direkomendasikan}}{\text{Jumlah total lagu yang direkomendasikan (k)}}
$$

**Contoh cara kerja:**

Jika dari 5 lagu yang direkomendasikan, terdapat 3 lagu yang sesuai preferensi pengguna (label `target = 1`), maka precision-nya:

$$
\frac{3}{5} = 0.60 \text{ atau } 60\%
$$

**Kenapa cocok?**
Karena dalam sistem rekomendasi, kita ingin memastikan **lagu-lagu yang ditampilkan memang sesuai minat pengguna**. Metrik ini fokus pada **akurasi hasil yang ditampilkan**, bukan jumlah total yang tersedia.
