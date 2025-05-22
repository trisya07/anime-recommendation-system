# Laporan Proyek Machine Learning - Trisya Nurmayanti

## Project Overview

Laju pertumbuhan industri anime yang sangat pesat dalam beberapa tahun terakhir menyebabkan jumlah judul anime yang tersedia di berbagai platform streaming dan komunitas daring semakin melimpah. Kondisi ini menimbulkan permasalahan utama bagi pengguna, yaitu kesulitan dalam menemukan anime yang benar-benar sesuai dengan preferensi dan minat mereka di tengah banjir informasi dan pilihan yang sangat banyak. Banyak pengguna merasa kebingungan dalam memilih anime berikutnya untuk ditonton, sehingga pengalaman menonton menjadi kurang optimal dan potensi eksplorasi anime baru pun terhambat [[1](https://jurnal.harianregional.com/jnatia/id-92538)].

Masalah ini semakin kompleks karena preferensi setiap pengguna sangat beragam, baik dari segi genre, tema, maupun gaya penceritaan. Selain itu, rekomendasi manual dari teman atau komunitas seringkali belum cukup efektif, karena tidak sepenuhnya mempertimbangkan riwayat dan pola perilaku pengguna secara personal. Tanpa sistem rekomendasi yang cerdas, pengguna cenderung hanya menonton anime yang populer atau sudah banyak dibicarakan, sehingga judul-judul anime yang lebih spesifik dan sesuai selera pribadi sering terlewatkan [[2](http://repository.uin-malang.ac.id/18842/1/18842.pdf)].

Permasalahan lain yang muncul adalah banyaknya data rating dan ulasan yang dihasilkan pengguna, namun belum dimanfaatkan secara maksimal untuk memberikan rekomendasi yang relevan dan personal. Sistem pencarian konvensional yang hanya berbasis kata kunci atau filter sederhana juga belum mampu mengatasi kebutuhan akan personalisasi rekomendasi secara mendalam. Hal ini berpotensi menurunkan kepuasan pengguna, mengurangi engagement, serta berdampak pada loyalitas pengguna terhadap platform streaming atau komunitas anime yang ada [[3](https://sistemasi.ftik.unisi.ac.id/index.php/stmsi/article/viewFile/2473/)].

Oleh karena itu, pengembangan sistem rekomendasi anime yang mampu menggabungkan informasi konten seperti genre dengan data interaksi pengguna seperti riwayat rating menjadi hal yang krusial. Sistem rekomendasi yang andal dapat mempercepat proses pencarian anime yang sesuai dengan selera pengguna secara lebih tepat, sehingga memperkaya pengalaman menonton sekaligus mendorong pengguna untuk menemukan judul-judul baru yang sebelumnya belum mereka kenal. Bagi penyedia layanan streaming atau platform anime, sistem semacam ini juga berperan penting dalam meningkatkan kepuasan dan loyalitas pengguna, serta memberikan nilai tambah dalam menghadapi persaingan di industri hiburan digital. Dengan memahami tantangan ini, penerapan pendekatan content-based filtering dan collaborative filtering menjadi langkah strategis yang tepat untuk membantu pengguna menjelajahi berbagai pilihan anime yang tersedia saat ini.

## Referensi: 

- [[1]](https://ejournal.bsi.ac.id/ejurnal/index.php/khatulistiwa/article/view/9859) Implementasi Metode Collaborative Filtering untuk Sistem Rekomendasi Penjualan pada Toko Mebel
- [[2]](https://publikasi.dinus.ac.id/index.php/technoc/article/view/8556) Implementasi Metode Content-Based Filtering dan Collaborative Filtering pada Sistem Rekomendasi Wisata di Bali
- [[3]](https://socjs.telkomuniversity.ac.id/ojs/index.php/ijoict/article/view/747) Movie Recommendation System Based on Synopsis Using Content-Based Filtering with TF-IDF and Cosine Similarity
- [[4]](https://openlibrarypublications.telkomuniversity.ac.id/index.php/engineering/article/view/21368/0) Sistem Rekomendasi Buku Dengan Collaborative Filtering Menggunakan Metode Singular Value Decomposition (SVD)

## Business Understanding

Dengan semakin banyaknya judul anime yang tersedia di berbagai platform, pengguna sering kali mengalami kesulitan dalam memilih tontonan yang sesuai dengan preferensi mereka. Untuk mengatasi permasalahan ini, dibutuhkan sistem rekomendasi yang dapat membantu menyaring dan menyajikan daftar anime yang relevan secara otomatis. Pada proyek ini menggunakan content based filtering dengan TF IDF + Cosine Similarity dan Collaborative Filtering dengan Singular Value Decomposition (SVD).

### Problem Statements

- Bagaimana membangun sistem rekomendasi berdasarkan kemiripan konten (genre) agar pengguna dapat menemukan anime yang sejenis dengan preferensi sebelumnya?
- Bagaimana membangun sistem rekomendasi berdasarkan perilaku pengguna (riwayat rating) untuk menyarankan anime yang disukai oleh pengguna dengan pola serupa?
- Bagaimana mengukur dan mengevaluasi kualitas hasil rekomendasi dari kedua pendekatan tersebut?

### Goals

- Membangun model content-based filtering menggunakan representasi teks (TF-IDF) dan pengukuran kesamaan (Cosine Similarity) dari genre anime.
- Membangun model collaborative filtering menggunakan algoritma Singular Value Decomposition (SVD) untuk mempelajari pola rating pengguna.
- Mengevaluasi performa model menggunakan metrik seperti Precision, Recall, RMSE, dan MAE.

### Solution statements

- Sistem rekomendasi menggunakan pendekatan content-based filtering dengan merepresentasikan genre anime dalam bentuk vektor TF-IDF, lalu menghitung kesamaan antar-anime menggunakan Cosine Similarity. Rekomendasi diberikan berdasarkan anime yang memiliki kemiripan tinggi dengan anime yang disukai pengguna sebelumnya.
- Sistem menggunakan algoritma SVD dari pustaka surprise pada collborative filtering untuk mempelajari pola rating dan preferensi pengguna. Model ini mampu memberikan prediksi rating terhadap anime yang belum diberi rating oleh pengguna dan menyarankan anime dengan prediksi rating tertinggi.

## Data Understanding

### Informasi Dataset

Proyek ini menggunakan data dari [Kaggle](https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database) yang berisi informasi terkait anime dan interaksi pengguna terhadap anime tersebut. Pada proyek ini, digunakan dua dataset utama yaitu anime dan rating. Dataset anime berisi informasi mengenai anime dengan total 12.294 baris dan 7 kolom, yang meliputi anime_id, name, genre, type, episodes, rating, dan members. Kolom-kolom tersebut memberikan gambaran lengkap tentang setiap anime, mulai dari identitas unik, nama judul, genre yang mengkategorikan konten, tipe anime, jumlah episode, nilai rating rata-rata, hingga jumlah anggota pengguna yang telah menonton atau memberikan rating.

Sementara itu, dataset rating terdiri dari data interaksi pengguna dengan anime berupa rating yang diberikan. Dataset ini jauh lebih besar, dengan total 7.813.737 baris dan 3 kolom yaitu user_id, anime_id, dan rating. Dataset rating ini merekam bagaimana preferensi pengguna terhadap berbagai anime berdasarkan nilai rating yang mereka berikan. Kedua dataset ini nantinya akan digunakan secara bersama-sama untuk membangun sistem rekomendasi berbasis content filtering dan collaborative filtering.

### Deskripsi Variabel

**1. Dataset Anime**

Dataset anime berisi informasi detail mengenai berbagai judul anime yang tersedia pada platform MyAnimeList. Berikut adalah deskripsi variabel yang terdapat pada dataset ini:
| Variabel  | Deskripsi                                                                             |
| --------- | ------------------------------------------------------------------------------------- |
| anime_id  | ID unik dari MyAnimeList yang mengidentifikasi setiap anime secara spesifik           |
| name      | Nama lengkap anime                                                                    |
| genre     | Daftar genre yang dipisahkan dengan koma, menggambarkan kategori atau tema anime      |
| type      | Jenis anime, misalnya Movie, TV, OVA, dan lain-lain                                   |
| episodes  | Jumlah episode yang ada dalam anime tersebut (nilai 1 jika berupa film/movie)         |
| rating    | Nilai rata-rata rating anime berdasarkan penilaian pengguna, dengan skala maksimal 10 |
| members   | Jumlah anggota komunitas yang menambahkan anime ini ke daftar mereka (member count)   |

**2. Dataset Rating**

Dataset rating berisi data interaksi pengguna dengan anime berupa rating yang diberikan oleh pengguna terhadap judul anime tertentu. Berikut adalah deskripsi variabel dalam dataset ini:

| Variabel  | Deskripsi                                                                                                                                               |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| user_id   | ID pengguna yang bersifat anonim dan dihasilkan secara acak, untuk mengidentifikasi pengguna unik                                                       |
| anime_id  | ID anime yang diberikan rating oleh pengguna                                                                                                            |
| rating    | Nilai rating yang diberikan pengguna terhadap anime tersebut, dengan skala 1 sampai 10. Nilai -1 berarti pengguna menonton tapi tidak memberikan rating |

### Exploratory Data Analysis (EDA)

- Metode `info()` digunakan untuk menampilkan ringkasan struktur DataFrame, seperti jumlah baris, tipe data setiap kolom, serta jumlah nilai yang tidak kosong (non-null) pada tiap kolom. Hal ini membantu mengidentifikasi apakah ada nilai yang hilang dan tipe data yang perlu disesuaikan. Pada kedua dataset proyek ini memiliki struktur dataset sebagai berikut.
  
  <img width="328" alt="info" src="https://github.com/user-attachments/assets/310a635e-29b1-421a-b54f-3598ba07b688" />

  Dari hasil pengecekan ditemukan beberapa kolom yang memiliki nilai kosong (missing value) pada kolom genre, type dan arting. Hal ini menunjukkan bahwa tidak semua data anime memiliki informasi lengkap pada kolom tersebut, sehingga perlu dilakukan penanganan missing value sebelum proses analisis dan pemodelan agar tidak menimbulkan error atau bias. Selain itu pada kolom `episodes` memiliki tipe data object, seharusnya bertipe data integer, untuk itu perlu dianalisis lebih lanjut mengenai penyebab ketidaksesuaian ini. Untuk dataset rating semua kolom bertipe integer dan tidak ditemukan missing value, yang berarti data rating cukup lengkap dan siap dipakai untuk pemodelan. Secara keseluruhan, kedua dataset memiliki struktur data yang jelas dengan sebagian kecil nilai yang hilang di dataset anime, dan tipe data yang tidak sesuai. Penanganan missing value dan konversi tipe data menjadi tahap penting untuk memastikan kualitas data sebelum analisis lebih lanjut.
  
- Metode `describe()` memberikan ringkasan statistik dasar untuk kolom numerik maupun kategorikal, termasuk nilai rata-rata, standar deviasi, nilai minimum dan maksimum, serta jumlah nilai unik pada kolom kategorikal. Ini berguna untuk mendapatkan gambaran umum distribusi data.
  - Dataset Anime
    
    <img width="442" alt="describe anime" src="https://github.com/user-attachments/assets/a3a14b2d-8239-4e67-acb1-c85dc2f6314d" />

    Hasil dari fungsi `describe()` pada dataset anime menunjukkan bahwa sebagian besar nilai numerik memiliki rentang yang wajar dan tidak menunjukkan adanya anomali ekstrem. Misalnya, rating memiliki nilai antara sekitar 1.0 hingga 10.0, dan members memiliki jumlah keanggotaan yang tinggi pada beberapa anime populer, sesuai ekspektasi. Oleh karena itu, tidak ditemukan nilai yang mencurigakan pada data numerik anime berdasarkan hasil statistik deskriptif ini.
    
  - Dataset Rating

    <img width="230" alt="describe rating" src="https://github.com/user-attachments/assets/057fc0dd-9552-402a-9b55-1470b43146a3" />

    Pada dataset rating, kolom rating ditemukan memiliki nilai minimum -1, yang secara jelas merupakan anomali. Namun, berdasarkan deskripsi variabel, nilai -1 ini bukan error, melainkan merupakan kode khusus untuk menunjukkan bahwa seorang user telah menonton anime tersebut tetapi tidak memberikan rating. Oleh karena itu, nilai -1 harus ditangani secara khusus sebelum digunakan dalam pelatihan model prediksi rating.

- Metode `unique()` digunakan untuk melihat secara langsung nilai-nilai unik dalam suatu kolom. Hal ini membantu dalam mendeteksi ketidakkonsistenan data, seperti penulisan genre, serta mengetahui kemungkinan nilai yang tidak valid seperti 'Unknown' atau karakter khusus. Pada proyek ini dilakukan pengecekan pada kolom `name`, `genre`, dan `episodes`.

  <img width="421" alt="nilai unik" src="https://github.com/user-attachments/assets/d72ebc9e-0a5b-4bb3-a77f-5bfb478a2d25" />

  Pada kolom genre, ditemukan bahwa nilai-nilainya merupakan daftar genre yang dipisahkan dengan koma, dan beberapa genre menggunakan tanda hubung (-), seperti sci-fi. Penggunaan tanda hubung ini dapat menyebabkan genre seperti sci-fi dianggap sebagai dua token terpisah saat diterapkan teknik pemrosesan teks. Oleh karena itu, diperlukan penyesuaian agar genre dengan tanda hubung dianggap sebagai satu kesatuan. Sementara itu, pada kolom episodes, ditemukan adanya nilai 'Unknown' yang menunjukkan jumlah episode tidak diketahui. Nilai ini tidak cocok dengan tipe data numerik dan dapat mengganggu analisis lebih lanjut, terutama jika ingin mengubah tipe data menjadi integer atau melakukan analisis kuantitatif berdasarkan jumlah episode.

Eksplorasi nilai unik ini hanya dilakukan pada dataset anime karena dari hasil describe() pada dataset rating, tidak ditemukan anomali lain selain nilai -1 pada kolom rating, yang sebelumnya sudah teridentifikasi sebagai penanda bahwa pengguna tidak memberikan rating. Selebihnya, nilai-nilai pada dataset rating terlihat wajar dan sesuai dengan deskripsi variabel. 

- Untuk mengecek nilai yang hilang (missing values), dilakukan pengecekan dengan metode seperti `isnull().sum()`, yang menghitung jumlah data kosong di setiap kolom agar dapat diatasi sebelum proses pemodelan.
  - Dataset Anime
 
    <img width="89" alt="missing value anime" src="https://github.com/user-attachments/assets/24f5020c-752a-4d6c-8d63-87c3e9576633" />

    Pada dataset anime ditemukan adanya missing value pada beberapa kolom, yaitu `genre`, `type`, dan `rating`. Keberadaan nilai yang hilang ini perlu ditangani karena dapat memengaruhi proses analisis dan pemodelan.
    
  - Dataset Rating
 
    <img width="82" alt="missing value rating" src="https://github.com/user-attachments/assets/8df3d899-9879-4e45-88bf-960817f732cc" />

    Pada dataset rating tidak ditemukan nilai yang hilang pada kolom manapun. Semua entri memiliki user_id, anime_id, dan rating, sehingga tidak memerlukan penanganan nilai kosong lebih lanjut pada tahap ini.
    
- Pemeriksaan data duplikat juga dilakukan dengan `duplicated().sum()` untuk memastikan tidak ada entri data yang berulang, sehingga menjaga kualitas dataset. Berikut adalah hasil dari pengecekan data duplikat pada kedua dataset.

  <img width="216" alt="cek data duplikat" src="https://github.com/user-attachments/assets/80e44be6-6def-4bfd-b2b4-c5a20c0a74c9" />

  Berdasarkan gambar di atas menunjukkan bahwa pada dataset anime tidak ditemukan data duplikat, sehingga seluruh baris dianggap unik berdasarkan kombinasi nilai pada tiap kolom. Sementara itu, pada dataset rating ditemukan 1 baris data duplikat, yang kemungkinan disebabkan oleh pengguna yang secara tidak sengaja memberikan rating yang sama untuk anime yang sama lebih dari sekali. Oleh karena itu, satu entri duplikat tersebut dihapus agar tidak mengganggu integritas data dalam proses pemodelan sistem rekomendasi.

- Distribusi genre dalam dataset anime dianalisis dengan memisahkan genre-genre yang tercantum pada tiap entri, kemudian menghitung frekuensi kemunculannya. Hasilnya divisualisasikan dalam bentuk bar chart untuk menunjukkan 15 genre terpopuler.
  
  ![visualisasi distribusi genre](https://github.com/user-attachments/assets/4140447b-e44c-4510-ae5c-cac5a3972285)

  Visualisasi distribusi genre menunjukkan bahwa genre Comedy merupakan genre yang paling dominan dalam dataset anime, dengan frekuensi kemunculan lebih dari 4.000 kali. Disusul oleh genre Action, Adventure dan Fantasy. Dominasi genre-genre tersebut menunjukkan bahwa anime dengan elemen komedi dan aksi merupakan jenis yang paling banyak diproduksi atau paling sering dikategorikan dalam basis data ini. Hal ini memberikan gambaran awal bahwa preferensi genre di industri anime cenderung condong ke arah genre yang menghibur dan penuh aksi.

- Visualisasi distribusi rating anime dilakukan untuk memahami pola persebaran nilai yang diberikan pengguna terhadap berbagai judul anime.
  
  ![visualisasi rating](https://github.com/user-attachments/assets/0c9b6ab3-6844-4d04-b672-4b41a89cdf92)

  Visualisasi distribusi rating pada dataset menunjukkan bahwa terdapat sejumlah besar pengguna yang tidak memberikan penilaian terhadap anime yang mereka tonton, ditandai dengan banyaknya data pada nilai rating -1, menjadikannya kategori terbanyak kedua dalam grafik. Untuk rating eksplisit, distribusi terlihat tidak merata. Rating antara 1 hingga 3 memiliki jumlah yang sangat sedikit, hampir tidak terlihat dalam grafik, sedangkan mulai dari rating 4 hingga 7 jumlahnya mulai meningkat secara perlahan. Puncak distribusi berada pada rating 8, yang menunjukkan bahwa sebagian besar pengguna memberikan penilaian tinggi terhadap anime yang mereka tonton. Temuan ini mengindikasikan kecenderungan pengguna untuk memberi penilaian positif dan menunjukkan bahwa sistem rekomendasi harus memperhatikan bias ini dalam proses pelatihan model.
  
## Data Preparation

### 1. Content-Based Filtering

#### Menstandarkan Format Genre

Menstandarkan format teks pada kolom genre, dilakukan penggantian karakter strip (-) menjadi underscore (_). Hal ini bertujuan agar kolom genre yang terdiri dari dua kata seperti sci-fi tidak dipisahkan saat diproses oleh algoritma ekstraksi fitur TF-IDF. Proses ini dilakukan dengan metode str.replace() pada seluruh entri di kolom genre. Dengan begitu, genre-genre tersebut tetap dikenali sebagai satu token yang utuh dalam proses tokenisasi.
```python
anime['genre'] = anime['genre'].str.replace('-', '_')
```

#### Pembersihan Data: Penanganan Missing Value dan Nilai Tidak Valid

Meskipun pada Content-based filtering proyek ini berfokus pada variabel `genre` pembersihan pada dilakukan pada seluruh kolom untuk memastikan integritas data secara keseluruhan. 
- Menghapus nilai missing value
  Pada missing value kolom `genre` dan `type` dilakukan penghapusan yang diawali dengan mengubah nilai kosong menjadi string kosong ('') agar tidak menyebabkan error saat proses pemrosesan teks. Selanjutnya, baris yang masih memiliki nilai kosong pada kolom `genre` dan `type` dihapus menggunakan `dropna()`.
  ```python
  anime['genre'] = anime['genre'].fillna('')
  anime = anime.dropna(subset=['genre', 'type']).reset_index(drop=True)
  ```
  
- Mengisi nilai yang hilang dengan Mean
  Untuk missing value pada kolom `rating`, nilai kosong diisi dengan nilai rata-rata dari seluruh rating menggunakan fillna(), guna mempertahankan data sebanyak mungkin tanpa mengabaikan kualitas.
  ```python
  anime['rating'] = anime['rating'].fillna(anime['rating'].mean())
  ``` 
- Menghapus nilai yang tidak valid
  Pada kolom `episodes` terdapat nilai `Unknown` yang terlihat pada pengecekan nilai unik sebelumnya, pada proyek ini dihapus karena nilai tersebut tidak valid.
  ```python
  anime = anime[anime['episodes'] != 'Unknown']
  ```

setelah dilakukan pembersihan pada dataset anime memiliki 11954 baris dan 7 kolom.

#### Konversi Tipe Data Kolom episodes

Kolom episodes secara default dibaca sebagai tipe data objek (string), padahal secara semantik nilainya bersifat numerik. Itu dikarenakan sebelumnya terdapat nilai yang berisi `Unknown` sehingga bertipe data objek. Oleh karena itu, dilakukan konversi tipe data ke dalam bentuk integer. Proses ini penting untuk memastikan data mempunyai data yang berkualitas.

```python
anime['episodes'] = anime['episodes'].astype(int)
```

### Penerapan TF-IDF pada Fitur Genre

Pada metode content-based filtering, digunakan teknik TF-IDF (Term Frequency–Inverse Document Frequency) sebagai metode ekstraksi fitur untuk mengubah data teks pada kolom genre menjadi representasi numerik. Proses ini dilakukan menggunakan `TfidfVectorizer` dari pustaka `Scikit-learn`, yang menghitung bobot setiap genre berdasarkan frekuensi kemunculannya relatif terhadap seluruh data anime. Untuk meningkatkan kualitas representasi, digunakan parameter `stop_words='english'` guna menghilangkan kata-kata umum dalam bahasa Inggris yang tidak memiliki makna penting dalam konteks analisis (meskipun dalam kolom genre hal ini relatif jarang muncul, namun tetap disertakan sebagai langkah antisipatif). Hasil dari proses ini adalah sebuah matriks TF-IDF yang merepresentasikan setiap anime dalam bentuk vektor. Matriks ini kemudian digunakan untuk menghitung similarity antar anime berdasarkan kemiripan genre, sebagai dasar dalam sistem rekomendasi berbasis konten.
```python
tfidf = TfidfVectorizer(stop_words='english')
tfidf_matrix = tfidf.fit_transform(anime['genre'])
```

### 2. Collaborative Filtering

#### Menghapus kolom `rating` yang bernilai `-1`

Pada dataset rating pada kolom `rating` terdapat yang bernilai `-1` yang merepresentasikan bahwa pengguna belum memberikan rating sebenarnya terhadap suatu anime. Data semacam ini dapat mengganggu proses pelatihan model karena tidak mencerminkan preferensi pengguna yang valid. Oleh karena itu, nilai rating -1 dihapus agar hanya data dengan rating eksplisit yang digunakan dalam sistem rekomendasi.
  ```python
  rating = rating[rating['rating'] != -1]
  ```
setelah dilakukan pembersihan pada dataset rating memiliki 6337241 baris dan 3 kolom.

#### Menghapus Duplikasi Dataset Rating

berdasarkan pengecekan data duplikat sebelumnya, pada dataset rating terdapat data duplikat sebanyak satu data. Untuk itu dilakukan penghapusan untuk menajga intergritas data. penghapusan data duplikat menggunakan `drop_duplicates()`

#### Menentukan Skala Rating

Sistem rekomendasi ini menggunakan data rating dari pengguna terhadap anime dengan skala 1 hingga 10. Oleh karena itu, objek Reader dari library Surprise didefinisikan dengan `rating_scale=(1, 10)`. Informasi ini penting untuk memberi tahu algoritma batas bawah dan atas nilai rating yang digunakan.
```python
reader = Reader(rating_scale=(1, 10))
```

#### Mengonversi DataFrame ke Format Surprise

Dataset asli yang berisi tiga kolom (user_id, anime_id, dan rating) dikonversi ke format internal Surprise menggunakan fungsi `Dataset.load_from_df()`. Format ini dibutuhkan agar data dapat dibaca dan diproses oleh model collaborative filtering yang akan digunakan. Proses konversi ini menghasilkan objek dataset yang siap untuk dibagi menjadi data pelatihan dan pengujian.
```python
data = Dataset.load_from_df(rating[['user_id', 'anime_id', 'rating']], reader)
```

#### Pembagian data pelatihan dan data testing

Setelah data rating dikonversi ke dalam format yang sesuai dengan pustaka `Surprise`, langkah selanjutnya adalah membagi data menjadi dua bagian, yaitu data pelatihan (training set) dan data pengujian (test set). Pembagian ini dilakukan dengan proporsi 80:20, di mana 80% data digunakan untuk melatih model dan 20% sisanya digunakan untuk menguji performa model terhadap data yang belum pernah dilihat sebelumnya. Selain itu, nilai `random_state` juga ditentukan agar proses pembagian data bersifat reproducible, sehingga hasil evaluasi model tetap konsisten apabila dijalankan ulang di waktu yang berbeda. Pada proyek ini data pelatihan terdiri sebanyak 5.069.792 data dan data testing sebanyak 1.267.448 data.

## Modeling
ahapan ini membahas model sistem rekomendasi yang digunakan untuk memberikan rekomendasi anime kepada pengguna. Dua pendekatan utama yang digunakan dalam proyek ini adalah Content-Based Filtering dan Collaborative Filtering. Masing-masing pendekatan memiliki mekanisme dan keunggulannya sendiri, serta menghasilkan output berupa Top-N Recommendation.

**1. Content-Based Filtering dengan Cosine Similarity**

Tahapan modeling sistem rekomendasi ini menggunakan pendekatan content-based filtering, yaitu metode yang merekomendasikan anime lain berdasarkan kemiripan konten yaitu kolom `genre` dengan anime yang menjadi input pengguna. Genre yang sebelumnya telah direpresentasikan dalam bentuk matriks TF-IDF, digunakan untuk menghitung kesamaan antar anime. Adapun tahapan dalam proses modeling ini adalah sebagai berikut:
- Menghitung Cosine Similarity
  Langkah awal dalam modeling adalah menghitung tingkat kemiripan antar anime berdasarkan representasi fitur dari kolom genre yang telah diubah ke dalam bentuk numerik menggunakan TF-IDF. Kemiripan ini dihitung dengan metode Cosine Similarity menggunakan fungsi `cosine_similarity` dari sklearn.metrics.pairwise. Hasil dari proses ini berupa matriks dua dimensi berukuran n x n, di mana n adalah jumlah anime, dan setiap nilai di dalamnya mencerminkan tingkat kemiripan antar dua anime.
  
- Memetakan Judul Anime ke Indeks DataFrame
  Untuk memudahkan pengambilan data berdasarkan judul anime, dibuat sebuah struktur data berupa Series yang memetakan setiap judul anime ke indeks barisnya dalam DataFrame. Sebelumnya, DataFrame di-reset terlebih dahulu untuk memastikan indeks urut dan konsisten.
  
- Membangun Fungsi Rekomendasi
  Selanjutnya, dibuat fungsi `content_based_recommendation(title, top_n=10)` yang menerima input judul anime dan jumlah rekomendasi yang diinginkan. Fungsi ini akan mencari indeks anime input, kemudian mengambil daftar anime dengan nilai kemiripan tertinggi (kecuali dirinya sendiri). Output dari fungsi ini adalah daftar anime yang paling mirip berdasarkan `genre`.
  
**Kelebihan:**
- Tidak membutuhkan interaksi dari banyak pengguna (hanya butuh data item).
- Cocok untuk pengguna baru yang belum memiliki banyak histori rating (cold-start problem dari sisi user bisa diatasi).

**Kekurangan:**
- Rekomendasi terbatas pada kemiripan konten saja, sehingga sistem kurang mampu menyarankan item yang berbeda tetapi mungkin disukai.
- Bergantung pada kualitas representasi fitur konten yang pada proyek ini variabel `genre`.


**2. Collaborative Filtering dengan Singular Value Decomposition (SVD)** 

Tahapan modeling selanjutnya menggunakan pendekatan Collaborative Filtering, yaitu merekomendasikan anime berdasarkan pola perilaku pengguna lain dengan preferensi serupa. Metode ini tidak bergantung pada konten (genre), tetapi pada interaksi pengguna–item dalam bentuk rating. Model yang digunakan adalah SVD (Singular Value Decomposition) dari library `Surprise`. Tahapan yang dilakukan:
- Pelatihan Model SVD
  Dataset yang sudah dibagi menjadi data training dan data testing kemudian model SVD dibuat dan dilatih menggunakan data pelatihan (trainset) dengan fungsi `fit()`. Model ini akan belajar memetakan representasi laten dari user dan item berdasarkan pola rating yang tersedia.
- Prediksi Rating di Test Set
  Setelah dilatih, model melakukan prediksi terhadap data pengujian (testset) menggunakan model.test(). Prediksi ini akan digunakan untuk evaluasi dan penentuan rekomendasi.
- Fungsi Evaluasi Top-N
  Fungsi get_top_n() dibuat untuk mengambil N anime terbaik bagi setiap pengguna berdasarkan hasil prediksi rating tertinggi. Fungsi ini akan mengurutkan prediksi per pengguna dan mengembalikan daftar item dengan estimasi terbaik.
- Menghitung Precision dan Recall
  Fungsi precision_recall_at_k() digunakan untuk menghitung performa model dalam konteks sistem rekomendasi. Metrik ini mengukur berapa banyak rekomendasi yang benar-benar relevan (berdasarkan threshold rating ≥ 4.0), dibandingkan total rekomendasi yang diberikan.
- Rekomendasi untuk Pengguna Tertentu
  Untuk menunjukkan hasil nyata dari model, sistem merekomendasikan 10 anime dengan prediksi rating tertinggi kepada pengguna dengan ID tertentu (misalnya user_id = 40115). Daftar anime yang belum pernah dirating oleh pengguna tersebut diprediksi rating-nya, kemudian diurutkan berdasarkan estimasi tertinggi.

**Kelebihan:**

- Mampu memberikan rekomendasi lintas genre atau kategori karena didasarkan pada preferensi pengguna, bukan konten.
- Potensi personalisasi yang lebih tinggi.

**Kekurangan:**

- Rentan terhadap masalah cold-start jika pengguna atau anime baru tidak memiliki cukup data interaksi.
- Memerlukan dataset rating yang besar dan cukup padat.

**Hasil Content-Based Filtering**

Setelah membangun model content-based filtering berdasarkan kemiripan genre menggunakan TF-IDF dan Cosine Similarity, sistem dapat menghasilkan rekomendasi anime yang mirip dengan input yang diberikan. Sebagai contoh, ketika pengguna memberikan judul "Under World" sebagai input.
```python
query = 'Under World'
print(f"Rekomendasi Content-Based untuk '{query}':")
print(content_based_recommendation(query, top_n=10))
```

<img width="279" alt="hasil content-based filtering" src="https://github.com/user-attachments/assets/d3563abf-fcf1-4448-9a84-b9bf4b506425" />

Berdasarkan hasil rekomendasi, sistem menghasilkan 10 judul anime yang memiliki kemiripan genre dengan "Under World". Beberapa anime yang muncul dalam daftar rekomendasi tidak secara eksplisit terhubung dalam data awal pengguna, namun sistem tetap dapat mengidentifikasi kesamaan konten berdasarkan genre. Hal ini menunjukkan bahwa pendekatan content-based filtering dengan representasi fitur TF-IDF mampu mengenali keterkaitan antar anime secara kontekstual, meskipun tidak secara langsung berhubungan dalam data historis.

**Hasil Collaborative Filtering**
Setelah model selesai dilatih, sistem merekomendasikan 10 anime terbaik untuk user tertentu (misalnya user dengan user_id=40115). Rekomendasi diambil berdasarkan prediksi rating tertinggi dari anime yang belum pernah diberikan rating oleh user tersebut.

<img width="268" alt="Hasil collaborative Filtering" src="https://github.com/user-attachments/assets/58625edd-cde5-4b46-b4c0-92f4d6e6b831" />

Berdasarkan hasil rekomendasi untuk user dengan ID 40115 seperti yang terlihat pada gambar di atas, sistem mampu memberikan 10 anime dengan estimasi rating tinggi yang sesuai dengan preferensi user. Hal ini menunjukkan kemampuan model untuk memprediksi anime yang berpotensi disukai user berdasarkan pola rating historis.

## Evaluation
Pada tahap evaluasi, dilakukan pengukuran performa kedua metode sistem rekomendasi yang telah dibuat, yaitu Content-Based Filtering dan Collaborative Filtering. Evaluasi dilakukan dengan menggunakan metrik-metrik yang sesuai dengan konteks rekomendasi anime.

**1. Content Based Filtering**

Pada Content-Based Filtering, metrik evaluasi yang digunakan adalah Precision, yaitu ukuran proporsi rekomendasi yang relevan di antara top-k rekomendasi yang diberikan. Precision dihitung dengan formula:

![rumus presisi content](https://github.com/user-attachments/assets/761e1bcc-5a80-4c1a-9154-1c71ab298163)

Dimana rekomendasi dianggap relevan jika memiliki setidaknya satu genre yang sama dengan anime input. Precision memberikan gambaran seberapa akurat rekomendasi yang diberikan sistem dalam memenuhi preferensi pengguna. Cara kerjanya yaitu sistem memberikan top-k rekomendasi berdasar kemiripan genre (berdasarkan TF-IDF dan cosine similarity). Kemudian, dihitung berapa banyak dari rekomendasi tersebut yang memiliki genre sama dengan anime input sebagai ukuran relevansi.

Hasil dari content based filtering yaitu:

<img width="289" alt="evaluasi content" src="https://github.com/user-attachments/assets/3a46afa1-b8e5-4eee-98f0-0e877b58391a" />

Precision untuk query "Under World" adalah 1.00, artinya semua rekomendasi yang diberikan sangat relevan dengan anime input, menunjukkan sistem berhasil memberikan rekomendasi yang akurat.

**2. Collaborative Filtering**

Beberapa metrik evaluasi yang digunakan:
- Root Mean Squared Error (RMSE) : Mengukur seberapa jauh rata-rata prediksi rating model dari rating asli pengguna. Nilai RMSE yang lebih kecil menunjukkan model yang lebih akurat.

  ![rmse](https://github.com/user-attachments/assets/1d71178d-53d0-44b9-81cd-d4869e9c7c5d)
 
- Mean Absolute Error (MAE): Mirip dengan RMSE, namun menghitung rata-rata selisih absolut antara prediksi dan rating asli. Nilai MAE juga semakin kecil, semakin baik.

  ![rumus mae](https://github.com/user-attachments/assets/5e202d6a-f73d-4b29-9d85-440aa190c33b)

- Precision dan Recall: Precision mengukur proporsi rekomendasi yang relevan di antara rekomendasi teratas. Recall mengukur seberapa banyak item yang relevan berhasil direkomendasikan oleh sistem dalam top-k. Formula presisi sama dengan yang ada di content-based filtering, sedangkan berikut merupakan formula dari recall

  <img width="369" alt="recall" src="https://github.com/user-attachments/assets/2535637c-65bd-4730-90e5-ce29d47cf039" />

Hasil dari Collaborative Filtering:
| Metrik     | Nilai  |
|------------|---------|
| RMSE       | 1.1326  |
| MAE        | 0.8445  |
| Precision  | 0.7199  |
| Recall     | 0.7132  |

<img width="268" alt="Hasil collaborative Filtering" src="https://github.com/user-attachments/assets/2d51ddf8-ff3e-43dc-ab5f-4d259bb150cf" />

Berdasarkan hasil evaluasi model Collaborative Filtering, diperoleh nilai RMSE sebesar 1.1326 dan MAE sebesar 0.8445. RMSE (Root Mean Square Error) dan MAE (Mean Absolute Error) merupakan metrik yang digunakan untuk mengukur seberapa jauh prediksi rating model mendekati rating asli yang diberikan oleh pengguna. Nilai RMSE dan MAE yang lebih kecil menunjukkan prediksi yang lebih akurat. Dalam konteks ini, nilai RMSE dan MAE yang didapatkan sudah cukup baik untuk sebuah sistem rekomendasi berbasis rating dengan rentang skala 1 hingga 10.

Selain itu, untuk mengukur kualitas rekomendasi yang diberikan, dilakukan evaluasi menggunakan metrik Precision dan Recall dengan ambang batas rating 4.0 pada top-10 rekomendasi. Precision sebesar 0.7199 menunjukkan bahwa sekitar 72% dari rekomendasi yang diberikan kepada pengguna memang relevan (sesuai preferensi). Sedangkan Recall sebesar 0.7132 mengindikasikan bahwa sistem mampu menemukan sekitar 71% dari semua item relevan yang seharusnya direkomendasikan. Dengan kata lain, sistem Collaborative Filtering ini efektif dalam memberikan rekomendasi yang sesuai dengan minat pengguna. Rekomendasi yang dihasilkan untuk user dengan ID 40115 juga menunjukkan kualitas tinggi, dimana sebagian besar anime yang direkomendasikan memiliki prediksi rating sangat tinggi (di atas 9.5), yang menandakan anime tersebut diperkirakan sangat disukai oleh pengguna berdasarkan pola rating pengguna lain.

**Kesimpulan**
Untuk metode Content-Based Filtering, hasil evaluasi menunjukkan precision sebesar 1.00 pada rekomendasi top-10 untuk anime "Under World". Ini berarti semua rekomendasi yang diberikan berdasarkan kesamaan genre anime tersebut benar-benar relevan. Hal ini menunjukkan bahwa Content-Based Filtering unggul dalam hal relevansi konten, terutama jika input berupa judul dengan genre yang spesifik dan kaya fitur.

Namun, Content-Based Filtering memiliki keterbatasan, yaitu rekomendasi cenderung monoton dan kurang bervariasi karena hanya didasarkan pada fitur konten yang sama. Sementara Collaborative Filtering mampu memanfaatkan pola rating dari banyak pengguna, sehingga dapat memberikan rekomendasi yang lebih beragam dan personalisasi berdasarkan preferensi kolektif.

**---Ini adalah bagian akhir laporan---**
