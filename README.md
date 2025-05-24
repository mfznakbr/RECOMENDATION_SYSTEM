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

  - "Banyak dari siswa berasal dari Group C yaitu 49.43%"
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
