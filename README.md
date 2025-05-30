# Laporan Proyek Machine Learning - Nuansa Syafrie Rahardian

###### Disusun oleh : Nuansa Syafrie Rahardian

Ini adalah proyek kedua, membuat sistem rekomendasi untuk memenuhi submission Dicoding Kelas *machine learning* Terapan. 

## 1. Project Overview

### Latar belakang

Di era digital, akses terhadap konten hiburan seperti film menjadi semakin mudah melalui berbagai platform streaming seperti Netflix, Disney+, HBO Max, dan lainnya. Meski memberikan banyak pilihan, keberagaman tersebut sering kali membuat pengguna kesulitan memilih film yang sesuai dengan preferensi mereka. Berdasarkan laporan dari Deloitte (2023), lebih dari 40% pengguna layanan streaming merasa kesulitan menentukan film apa yang akan ditonton, meskipun memiliki langganan aktif di beberapa platform.

Masalah ini menunjukkan pentingnya keberadaan sistem rekomendasi yang dapat membantu pengguna menemukan film sesuai dengan preferensinya secara efisien dan personal. Salah satu pendekatan efektif dalam sistem rekomendasi adalah Content-Based Filtering, yaitu metode yang merekomendasikan item berdasarkan kesamaan konten antar item, seperti genre, kata kunci, aktor, sutradara, atau sinopsis.

Melalui proyek ini, penulis membangun sebuah sistem rekomendasi film menggunakan pendekatan Content-Based Filtering. Sistem ini dirancang untuk merekomendasikan film-film yang mirip dengan film yang disukai pengguna, berdasarkan metadata deskriptif film tersebut. Dataset yang digunakan bersumber dari The Movie Database (TMDB) yang menyediakan ribuan metadata film, termasuk overview, genre, dan informasi kru.

#### Mengapa Masalah Ini Penting untuk Diselesaikan?
Penerapan sistem rekomendasi memiliki nilai strategis yang sangat penting, baik dari sisi pengguna maupun pelaku bisnis. Bagi pengguna, sistem rekomendasi dapat meningkatkan kepuasan dalam menikmati layanan karena mampu menyarankan film-film yang relevan dan menarik sesuai dengan preferensi pribadi. Dengan demikian, pengguna tidak perlu lagi merasa kebingungan atau membuang waktu terlalu lama untuk mencari film yang ingin ditonton.

Dari sisi efisiensi, sistem ini membantu mempercepat proses navigasi dalam menjelajahi ribuan konten yang tersedia, sehingga pengalaman pengguna menjadi lebih nyaman dan menyenangkan. Lebih jauh lagi, secara bisnis, sistem rekomendasi terbukti mampu meningkatkan waktu tonton (watch time), memperkuat loyalitas pengguna terhadap platform, serta mengurangi kemungkinan pengguna berhenti berlangganan (churn rate). Oleh karena itu, pengembangan sistem rekomendasi yang cerdas dan adaptif menjadi salah satu kebutuhan utama dalam ekosistem layanan hiburan digital saat ini.

### Referensi Terkait
Ricci, F., Rokach, L., & Shapira, B. (2011). Introduction to Recommender Systems Handbook. Springer. https://doi.org/10.1007/978-0-387-85820-3

Aggarwal, C. C. (2016). Recommender Systems: The Textbook. Springer. https://doi.org/10.1007/978-3-319-29659-3

Deloitte Insights. (2023). Digital Media Trends: 17th Edition. [Online] https://www2.deloitte.com/us/en/pages/technology-media-and-telecommunications/articles/digital-media-trends-survey.html

## 2. Business Understanding

### Problem Statements

- Pengguna layanan streaming film kerap merasa kewalahan oleh banyaknya pilihan film yang tersedia. Tanpa panduan yang tepat, pengguna harus menelusuri satu per satu, yang sering kali memakan waktu lama dan mengurangi kenyamanan dalam menikmati layanan.

- Sistem rekomendasi yang hanya mengandalkan popularitas film atau penilaian umum belum tentu sesuai dengan preferensi pribadi setiap pengguna. Hal ini menyebabkan rekomendasi yang diberikan terasa generik dan kurang relevan secara personal.

- Banyak sistem belum memanfaatkan secara optimal informasi deskriptif dari film seperti genre, sinopsis, aktor, dan sutradara. Padahal, informasi ini dapat menjadi dasar penting untuk memahami kesamaan antar film dan menyusun rekomendasi yang lebih tepat sasaran.

### Goals

- Mengembangkan sistem rekomendasi yang dapat membantu pengguna menemukan film-film baru yang relevan dengan minat mereka dengan cara menyarankan film yang memiliki karakteristik konten yang serupa dengan film yang disukai sebelumnya.

- Meningkatkan kualitas dan relevansi rekomendasi dengan memanfaatkan metadata film, seperti genre, overview (sinopsis), nama aktor, dan sutradara, sehingga hasil rekomendasi terasa lebih personal dan sesuai dengan selera pengguna.

- Meningkatkan efisiensi waktu pencarian film serta memberikan pengalaman pengguna yang lebih menyenangkan dan efisien, yang pada akhirnya dapat mendorong peningkatan waktu tonton dan loyalitas pengguna terhadap platform.

### Solution Approach

- Proyek ini mengadopsi pendekatan **Content-Based Filtering**, yaitu metode sistem rekomendasi yang menyarankan item (film) berdasarkan kemiripan karakteristik konten dengan item yang telah disukai oleh pengguna.

- Untuk menerapkan pendekatan ini, dilakukan ekstraksi fitur-fitur konten dari dataset seperti genre, overview (sinopsis film), serta nama aktor dan sutradara. Fitur-fitur teks ini kemudian diolah menggunakan teknik **TF-IDF (Term Frequency–Inverse Document Frequency)** untuk mengubahnya menjadi representasi vektor numerik.

- Selanjutnya, digunakan metode **Cosine Similarity** untuk mengukur sejauh mana kemiripan antar film berdasarkan vektor konten yang telah dibentuk. Semakin tinggi nilai kemiripan antar film, semakin besar kemungkinan film tersebut relevan bagi pengguna.

- Pendekatan ini dipilih karena tidak memerlukan data eksplisit dari pengguna seperti rating atau riwayat tontonan yang tidak tersedia dalam dataset, sehingga sangat cocok digunakan ketika hanya tersedia metadata film (bukan interaksi pengguna). Ini memungkinkan sistem tetap memberikan rekomendasi yang baik meskipun dalam kondisi data terbatas.


## 3. Data Understanding
Dataset yang digunakan dalam proyek ini adalah [Movies Dataset](https://www.kaggle.com/datasets/abdallahwagih/movies) yang disediakan oleh Abdallah Wagih di Kaggle. Dataset ini berisi informasi metadata dari berbagai film, yang dapat dimanfaatkan untuk membangun sistem rekomendasi berbasis konten.

- **Jumlah data**: 4.803 entri film
- **Format**: CSV
- **Ukuran file**: 22.3 MB
- **Sumber**: [Kaggle - Movies Dataset by Abdallah Wagih](https://www.kaggle.com/datasets/abdallahwagih/movies)


Tabel 1. Contoh Data pada Dataset
| id | budget     | genres                                  | homepage                                 | imdb_id | keywords                                                       | original_language | original_title                                 | overview                                                                                           | popularity  | runtime | spoken_languages                                            | status   | tagline                                    | title                                        | vote_average | vote_count | cast                                                        | crew                                                | director         |
|----|------------|------------------------------------------|------------------------------------------|---------|----------------------------------------------------------------|-------------------|--------------------------------------------------|---------------------------------------------------------------------------------------------------|-------------|---------|-------------------------------------------------------------|----------|--------------------------------------------|---------------------------------------------|---------------|------------|-------------------------------------------------------------|-------------------------------------------------------|------------------|
| 0  | 237000000  | Action Adventure Fantasy Science Fiction | http://www.avatarmovie.com/              | 19995   | culture clash future space war space colony...                 | en                | Avatar                                           | In the 22nd century, a paraplegic Marine is dispatched...                                           | 150.437577 | 162.0   | [{"iso_639_1": "en", "name": "English"}, {...}]              | Released | Enter the World of Pandora.               | Avatar                                       | 7.2           | 11800      | Sam Worthington Zoe Saldana Sigourney Weaver...          | [{'name': 'Stephen E. Rivkin', ...}]               | James Cameron     |
| 1  | 300000000  | Adventure Fantasy Action                 | http://disney.go.com/disneypictures/... | 285     | ocean drug abuse exotic island east india trade...             | en                | Pirates of the Caribbean: At World's End         | Captain Barbossa, long believed to be dead, has returned...                                          | 139.082615 | 169.0   | [{"iso_639_1": "en", "name": "English"}]                    | Released | At the end of the world, the adventure begins. | Pirates of the Caribbean: At World's End      | 6.9           | 4500       | Johnny Depp Orlando Bloom Keira Knightley...              | [{'name': 'Dariusz Wolski', ...}]                  | Gore Verbinski    |
| 2  | 245000000  | Action Adventure Crime                   | http://www.sonypictures.com/movies/spectre/ | 206647  | spy based on novel secret agent sequel mi6                    | en                | Spectre                                         | A cryptic message from Bond’s past sends him on a trail...                                            | 107.376788 | 148.0   | [{"iso_639_1": "fr", "name": "Français"}, {...}]             | Released | A Plan No One Escapes                     | Spectre                                      | 6.3           | 4466       | Daniel Craig Christoph Waltz Léa Seydoux...              | [{'name': 'Thomas Newman', ...}]                   | Sam Mendes        |
| 3  | 250000000  | Action Crime Drama Thriller              | http://www.thedarkknightrises.com/       | 49026   | dc comics crime fighter terrorist secret identity...           | en                | The Dark Knight Rises                          | Following the death of District Attorney Harvey Dent...                                              | 112.312950 | 165.0   | [{"iso_639_1": "en", "name": "English"}]                    | Released | The Legend Ends                           | The Dark Knight Rises                         | 7.6           | 9106       | Christian Bale Michael Caine Gary Oldman...              | [{'name': 'Hans Zimmer', ...}]                     | Christopher Nolan |
| 4  | 260000000  | Action Adventure Science Fiction         | http://movies.disney.com/john-carter     | 49529   | based on novel mars medallion space travel prince...           | en                | John Carter                                    | John Carter is a war-weary, former military captain...                                               | 43.926995  | 132.0   | [{"iso_639_1": "en", "name": "English"}]                    | Released | Lost in our world, found in another.       | John Carter                                  | 6.1           | 2124       | Taylor Kitsch Lynn Collins Samantha Morton...            | [{'name': 'Andrew Stanton', ...}]                  | Andrew Stanton     |


### Variabel-variabel pada dataset Movies
| No. | Nama Kolom             |  Penjelasan                                                                   |
| --- | ---------------------- | ---------------------------------------------------------------------------- |
| 1   | `index`                |  Nomor urut baris dalam dataset (bukan fitur penting, hanya penomoran).       |
| 2   | `budget`               |  Total anggaran produksi film dalam USD.                                      |
| 3   | `genres`               |  Genre film (bisa satu atau lebih, misalnya: Action, Drama).                  |
| 4   | `homepage`             |  URL situs resmi film (jika tersedia).                                        |
| 5   | `id`                   |  ID unik film dari TMDB (The Movie Database).                                 |
| 6   | `keywords`             |  Kata kunci yang menggambarkan tema atau isi film.                            |
| 7   | `original_language`    |  Bahasa asli film, dalam kode ISO (misalnya "en", "fr").                      |
| 8   | `original_title`       |  Judul asli film sesuai bahasa produksinya.                                   |
| 9   | `overview`             |  Ringkasan atau sinopsis film.                                                |
| 10  | `popularity`           |  Skor popularitas film berdasarkan metrik dari TMDB.                          |
| 11  | `production_companies` |  Perusahaan-perusahaan yang memproduksi film.                                 |
| 12  | `production_countries` |  Negara-negara tempat produksi film dilakukan.                                |
| 13  | `release_date`         |  Tanggal rilis film (biasanya dalam format string, misal "2012-07-20").       |
| 14  | `revenue`              |  Total pendapatan (box office) film dalam USD.                                |
| 15  | `runtime`              |  Durasi film dalam menit (tipe object karena kemungkinan ada data non-angka). |
| 16  | `spoken_languages`     |  Bahasa-bahasa yang digunakan dalam film, sering dalam format JSON string.    |
| 17  | `status`               |  Status film, misalnya "Released", "Post Production", dll.                    |
| 18  | `tagline`              |  Kalimat promosi atau slogan film.                                            |
| 19  | `title`                |  Judul film dalam versi internasional.                                        |
| 20  | `vote_average`         |  Rata-rata nilai (rating) dari pengguna TMDB (skala 0–10).                    |
| 21  | `vote_count`           |  Jumlah vote atau rating yang diberikan oleh pengguna.                        |
| 22  | `cast`                 |  Daftar nama aktor/aktris pemeran film (bisa berupa list atau string JSON).   |
| 23  | `crew`                 |  Informasi tentang kru film, biasanya dalam format JSON string.               |
| 24  | `director`             |   Nama sutradara utama film.                                                   |


Tabel 2. Tipe Data Tiap Kolom pada Dataset
```sh
RangeIndex: 4803 entries, 0 to 4802
Data columns (total 24 columns):
 #   Column                Non-Null Count  Dtype  
---  ------                --------------  -----  
 0   index                 4803 non-null   int64  
 1   budget                4803 non-null   int64  
 2   genres                4803 non-null   object 
 3   homepage              4803 non-null   object 
 4   id                    4803 non-null   int64  
 5   keywords              4803 non-null   object 
 6   original_language     4803 non-null   object 
 7   original_title        4803 non-null   object 
 8   overview              4803 non-null   object 
 9   popularity            4803 non-null   float64
 10  production_companies  4803 non-null   object 
 11  production_countries  4803 non-null   object 
 12  release_date          4803 non-null   object 
 13  revenue               4803 non-null   int64  
 14  runtime               4803 non-null   object 
 15  spoken_languages      4803 non-null   object 
 16  status                4803 non-null   object 
 17  tagline               4803 non-null   object 
 18  title                 4803 non-null   object 
 19  vote_average          4803 non-null   float64
 20  vote_count            4803 non-null   int64  
 21  cast                  4803 non-null   object 
 22  crew                  4803 non-null   object 
 23  director              4803 non-null   object 
dtypes: float64(2), int64(5), object(17)
```
Dari data di atas, terdapat tiga jenis tipe data yang digunakan dalam dataset, yaitu int64, float64, dan object. Tipe int64 digunakan untuk menyimpan data numerik diskret seperti budget, id, vote_count, dan index, yang jumlahnya ada 5 kolom. Tipe float64 digunakan untuk data numerik kontinu, seperti popularity dan vote_average, yang berjumlah 2 kolom. Sementara itu, tipe object adalah tipe data yang paling banyak digunakan dalam dataset ini, mencakup 17 kolom. Tipe object umumnya digunakan untuk teks atau data kompleks seperti string JSON (misalnya pada kolom genres, spoken_languages, crew, dan cast). Pembagian ini menunjukkan bahwa dataset ini sebagian besar berisi informasi berbasis teks atau semi-struktural, yang cocok untuk analisis Natural Language Processing (NLP) maupun pemrosesan data berbasis string lainnya.

Berikut adalah contoh penulisan bagian **Deteksi Missing Value** dan **Deteksi Duplikasi** dalam laporan proyekmu, jika memang tidak ditemukan nilai kosong dan tidak ada data duplikat:

---

### Deteksi Missing Value

Pemeriksaan terhadap data dilakukan untuk memastikan tidak adanya nilai kosong (missing value) pada fitur-fitur penting yang akan digunakan dalam proses pembuatan sistem rekomendasi. Hasil dari pengecekan menunjukkan **terdapat missing value** dengan keterangan sebagai berikut:

| No | Kolom                 | Jumlah Kosong |
| -- | --------------------- | ------------- |
| 1  | index                 | 0             |
| 2  | budget                | 0             |
| 3  | genres                | 28            |
| 4  | homepage              | 3091          |
| 5  | id                    | 0             |
| 6  | keywords              | 412           |
| 7  | original\_language    | 0             |
| 8  | original\_title       | 0             |
| 9  | overview              | 3             |
| 10 | popularity            | 0             |
| 11 | production\_companies | 0             |
| 12 | production\_countries | 0             |
| 13 | release\_date         | 1             |
| 14 | revenue               | 0             |
| 15 | runtime               | 2             |
| 16 | spoken\_languages     | 0             |
| 17 | status                | 0             |
| 18 | tagline               | 844           |
| 19 | title                 | 0             |
| 20 | vote\_average         | 0             |
| 21 | vote\_count           | 0             |
| 22 | cast                  | 43            |
| 23 | crew                  | 0             |
| 24 | director              | 30            |


Fitur-fitur yang memiliki nilai kosong (missing value) namun dianggap penting dan dipilih dalam proses seleksi fitur (feature selection) akan diproses lebih lanjut pada tahap data preparation. 

---

### Deteksi Duplikasi

Langkah awal dalam pembersihan data juga mencakup pemeriksaan terhadap kemungkinan adanya baris data yang duplikat. Pemeriksaan dilakukan menggunakan metode `.duplicated().sum()` pada keseluruhan dataframe. Hasil dari pengecekan ini menunjukkan bahwa **tidak terdapat data yang duplikat**.

Dengan demikian, semua entri dalam dataset merupakan film yang unik berdasarkan kombinasi informasi yang tersedia, seperti judul film, sinopsis, genre, aktor, dan sutradara. Hal ini memastikan bahwa model rekomendasi tidak akan bias terhadap data yang berulang, dan dapat memberikan hasil rekomendasi yang lebih akurat serta beragam.

---


## 4. Data Preparation

Pada tahap ini, dilakukan beberapa langkah untuk mempersiapkan data sebelum digunakan dalam pemodelan sistem rekomendasi berbasis konten (content-based filtering). Berikut adalah tahapan yang dilakukan secara berurutan:

### Feature Selection

Langkah pertama adalah memilih fitur-fitur yang relevan untuk menggambarkan konten dari setiap film. Fitur-fitur yang dipilih antara lain:
- `genres`
- `keywords`
- `tagline`
- `cast`
- `director`

Fitur-fitur ini dianggap mampu merepresentasikan isi atau karakteristik utama dari film, yang nantinya digunakan untuk menghitung kemiripan antar film.

---

### Handling Missing Values
Setelah fitur dipilih, dilakukan pemeriksaan dan penanganan nilai yang hilang (missing values). Semua nilai kosong pada kolom fitur diisi dengan string kosong (`''`) agar tidak mengganggu proses penggabungan dan transformasi data pada tahap selanjutnya.

---

### Combine Features
Semua fitur yang telah dipilih dan dibersihkan digabungkan menjadi satu kolom baru bernama `combined_features`. Kolom ini berisi representasi teks dari setiap film yang merupakan gabungan dari semua fitur yang dipilih.

#### Contoh Data pada Kolom `combined_features`

| Title                                 | Combined Features                                                                                     |
|---------------------------------------|--------------------------------------------------------------------------------------------------------|
| Avatar                                | Action Adventure Fantasy Science Fiction cultu...
| Pirates of the Caribbean: At World's End | Adventure Fantasy Action ocean drug abuse exo... |
| Spectre                               | Action Adventure Crime spy based on novel secr...|
| The Dark Knight Rises                 | Action Crime Drama Thriller dc comics crime fi...|
| John Carter                           | Action Adventure Science Fiction based on nove... |

### Text Cleaning
Setelah penggabungan fitur, dilakukan proses pembersihan teks seperti:
- Mengubah semua huruf menjadi huruf kecil
- Menghapus karakter khusus atau tanda baca (jika diperlukan)
- Menghilangkan stop words (dilakukan saat TF-IDF)

#### Contoh Data setelah Kolom `combined_features` di cleaning

| Index | combined_features |
|-------|-------------------|
| 0 | action adventure fantasy science fiction culture clash future space war space colony society enter the world of pandora sam worthington zoe saldana sigourney weaver stephen lang michelle rodriguez james cameron |
| 1 | adventure fantasy action ocean drug abuse exotic island east india trading company love of ones life at the end of the world the adventure begins johnny depp orlando bloom keira knightley stellan skarsguerd chow yunfat gore verbinski |
| 2 | action adventure crime spy based on novel secret agent sequel mi a plan no one escapes daniel craig christoph waltz luea seydoux ralph fiennes monica bellucci sam mendes |
| 3 | action crime drama thriller dc comics crime fighter terrorist secret identity burglar the legend ends christian bale michael caine gary oldman anne hathaway tom hardy christopher nolan |
| 4 | action adventure science fiction based on novel mars medallion space travel princess lost in our world found in another taylor kitsch lynn collins samantha morton willem dafoe thomas haden church andrew stanton |


Proses ini bertujuan untuk meningkatkan akurasi dan konsistensi pada saat transformasi teks menjadi vektor numerik.

---
### 1. *TF-IDF Vectorizer*
Tahap ini melibatkan penggunaan TF-IDF (Term Frequency-Inverse Document Frequency) Vectorizer untuk mengubah teks pada `combined_features` menjadi representasi numerik. TF-IDF mengukur pentingnya suatu kata dalam dokumen berdasarkan frekuensi kemunculan kata tersebut dalam dokumen dan inversi frekuensi kemunculan kata tersebut dalam seluruh koleksi dokumen. *TF-IDF Vectorizer* menghasilkan vektor fitur yang merepresentasikan konten film.

```sh
	with 108015 stored elements and shape (4803, 17199)>
  Coords	Values
  (0, 83)	0.07882862673780648
  (0, 157)	0.09044195197854715
  (0, 5215)	0.11136877588095699
  (0, 13719)	0.10390557242105192
  (0, 5378)	0.10390557242105192
  (0, 3588)	0.2144670618479119
  (0, 2967)	0.22264985192867037
  (0, 5784)	0.165094834077864
  (0, 14505)	0.34049320567457786
  (0, 16458)	0.12581419860737125
  (0, 3130)	0.2502378442888809
  (0, 14399)	0.2144670618479119
  (0, 4876)	0.24087092482877231
  (0, 16861)	0.13026399231101188
  (0, 11595)	0.28600862672985
  (0, 13471)	0.15059552102661708
  (0, 16873)	0.2370359127984507
  (0, 17169)	0.20249395427966976
  (0, 13441)	0.2183020738782335
  (0, 14188)	0.20648588212861024
  (0, 16539)	0.19893842868080436
  (0, 14741)	0.15189290258743376
  (0, 8766)	0.2276689933383421
  (0, 10270)	0.160996177130589
  (0, 13140)	0.1947312986648133
  :	:
  (4801, 283)	0.18067157687184213
  (4801, 4764)	0.2518715803601968
  (4801, 17146)	0.2941381493757195
  (4801, 13961)	0.284038806495114
  (4801, 13291)	0.2941381493757195
  (4801, 17020)	0.3083723736984483
  (4801, 3416)	0.3083723736984483
  (4801, 14075)	0.3083723736984483
  (4801, 7222)	0.3083723736984483
  (4802, 11238)	0.17863873110016232
  (4802, 4441)	0.16781146268389566
  (4802, 2004)	0.3099042947390819
  (4802, 4913)	0.16074873043389704
  (4802, 6105)	0.18118427189025468
  (4802, 3340)	0.21749102578985727
  (4802, 4451)	0.19500602389807956
  (4802, 1191)	0.19603591994568106
  (4802, 13105)	0.17008084939034054
  (4802, 4295)	0.1537934884621648
  (4802, 6371)	0.21749102578985727
  (4802, 4539)	0.239976027681635
  (4802, 2313)	0.239976027681635
  (4802, 3561)	0.2624610295734127
  (4802, 5309)	0.22964570686743288
  (4802, 6945)	0.5698920629303811
```

Output di atas merupakan representasi TF-IDF (Term Frequency-Inverse Document Frequency) dari kolom `combined_features` yang telah diproses menggunakan TfidfVectorizer. Hasilnya adalah sebuah sparse matrix berukuran (4803, 17199), yang menunjukkan bahwa terdapat 4803 dokumen (film) dan 17199 fitur unik (kata-kata penting yang muncul setelah preprocessing).

Setiap baris pada output (misalnya (0, 83) 0.0788) menunjukkan bahwa pada dokumen ke-0, terdapat fitur (kata) pada indeks ke-83 dengan bobot TF-IDF sebesar 0.0788. Nilai ini mencerminkan pentingnya kata tersebut dalam dokumen relatif terhadap seluruh korpus. Karena data TF-IDF umumnya sangat jarang (sparse) — sebagian besar elemen bernilai nol — maka hanya nilai-nilai yang bukan nol yang ditampilkan.

Matrix inilah yang menjadi representasi numerik (feature vector) dari setiap film yang kemudian digunakan untuk menghitung kemiripan antar film menggunakan metode seperti cosine similarity dalam tahap modeling sistem rekomendasi berbasis konten.

## 5. Modeling and Result

Pada tahap ini, dilakukan pembangunan model sistem rekomendasi film dengan pendekatan content-based filtering. Tujuannya adalah untuk merekomendasikan film kepada pengguna berdasarkan kemiripan konten dari film yang mereka sukai dengan film lainnya dalam dataset. Konten yang dianalisis mencakup informasi seperti genre, nama aktor, sutradara, hingga sinopsis dan kata kunci terkait. Proses modeling dimulai dengan perhitungan kemiripan antarfilm menggunakan cosine similarity. Hasil akhir dari proses ini adalah daftar rekomendasi film yang memiliki tingkat kemiripan konten tertinggi dengan film yang dipilih oleh pengguna.

### *Content-Based Filtering*
*Content-Based Filtering* adalah pendekatan dalam sistem rekomendasi yang mengandalkan analisis konten dari item yang direkomendasikan. 


Teknik Perhitungan Similarity:
1. *Cosine Similarity*: *Cosine Similarity* mengukur kesamaan antara dua vektor dengan menghitung kosinus sudut antara vektor-vektor tersebut. Dalam konteks *Content-Based Filtering*, *Cosine Similarity* digunakan untuk mengukur kesamaan antara vektor representasi film berdasarkan `combined_feature`. Nilai *Cosine Similarity* berkisar antara -1 hingga 1, di mana nilai 1 menunjukkan kesamaan yang sempurna dan nilai -1 menunjukkan perbedaan yang sempurna.



### Tahapan yang dilakukan dengan pendekatan *Content-Based Filtering*
Selama pendekatan ini, proses modeling dilakukan berdasar urutan sebagai berikut ini:


  
1. *Cosine Similarity*: Setelah mendapatkan vektor fitur menggunakan *TF-IDF Vectorizer*, tahap selanjutnya adalah menghitung kesamaan antara film  menggunakan metode *Cosine Similarity*. *Cosine Similarity* mengukur kesamaan arah antara dua vektor dalam ruang vektor. Pada konteks Content-Based Filtering, *Cosine Similarity* digunakan untuk mengukur kesamaan antara vektor fitur film berdasarkan deskripsi, topik, atau keterampilan yang terkait. Semakin tinggi nilai *Cosine Similarity*, semakin mirip kedua film dalam hal fitur-fitur yang diamati.

Tabel 3. Hasil Perhitungan Cosine Similarity pada Matrix TF-IDF

```sh
[[1.         0.04851609 0.03831059 ... 0.         0.         0.        ]
 [0.04851609 1.         0.02178729 ... 0.01299526 0.         0.        ]
 [0.03831059 0.02178729 1.         ... 0.         0.05562139 0.        ]
 ...
 [0.         0.01299526 0.         ... 1.         0.         0.02728976]
 [0.         0.         0.05562139 ... 0.         1.         0.        ]
 [0.         0.         0.         ... 0.02728976 0.         1.        ]]
```


Tahapan-tahapan di atas merupakan bagian dari proses *Content-Based Filtering* yang bertujuan untuk menganalisis dan membandingkan konten film berdasarkan vektor fitur yang dihasilkan menggunakan *TF-IDF Vectorizer*. 

Penggunaan metode *Cosine Similarity* mengukur kesamaan arah antara vektor fitur, memungkinkan untuk mengukur kesamaan atau perbedaan antara film-film dalam hal konten yang diamati.

Hasil uji coba dari modeling diatas adalah sebagai berikut:

```sh
Masukkan judul Film Favorit anda: The Avengers

Rekomendasi Film jika anda suka 'The Avengers':

1. Avengers: Age of Ultron
2. Captain America: The Winter Soldier
3. Captain America: Civil War
4. Iron Man 2
5. Thor: The Dark World
6. The Incredible Hulk
7. Thor
8. X-Men
9. X-Men: Apocalypse
10. Ant-Man
11. X2
12. X-Men: Days of Future Past
13. Captain America: The First Avenger
14. X-Men: The Last Stand
15. The Image Revolution
```
### Nilai Similiarity Score untuk Rekomendasi Film berdasarkan 'The Avengers'

| Rank | Movie Title                              | Similarity Score |
|------|------------------------------------------|------------------|
| 1    | Avengers: Age of Ultron                  | 0.8023           |
| 2    | Captain America: The Winter Soldier      | 0.4391           |
| 3    | Captain America: Civil War               | 0.4186           |
| 4    | Iron Man 2                               | 0.4133           |
| 5    | Thor: The Dark World                     | 0.3157           |
| 6    | The Incredible Hulk                      | 0.2935           |
| 7    | Thor                                     | 0.2880           |
| 8    | X-Men                                    | 0.2850           |
| 9    | X-Men: Apocalypse                        | 0.2768           |
| 10   | Ant-Man                                  | 0.2765           |
| 11   | X2                                       | 0.2694           |
| 12   | X-Men: Days of Future Past               | 0.2504           |
| 13   | Captain America: The First Avenger       | 0.2494           |
| 14   | X-Men: The Last Stand                    | 0.2493           |
| 15   | The Image Revolution                     | 0.2348           |

Dari hasil output diatas ditunjukkan 15 film rekomendasi yang memiliki kesamaan atau kemiripan berdasarkan nilai cosine similiarity terdekat dengan parameter parameter fitur yang dipilih.

## 6. Evaluation


### Interpretasi Evaluasi

Model rekomendasi ini menggunakan pendekatan **Content-Based Filtering** dengan metode **Cosine Similarity**. Sistem menghitung kemiripan antar film berdasarkan kombinasi fitur seperti genre, karakter, alur cerita, dan elemen sinematik lainnya.

Meskipun tidak semua film berasal dari Marvel Cinematic Universe (MCU), seperti seri *X-Men*, semua film yang direkomendasikan masih termasuk dalam kategori **film superhero berbasis komik**, dan mengandung elemen yang mirip seperti aksi, fiksi ilmiah, pahlawan dengan kekuatan super, kesamaan tokoh atau aktor, serta alur cerita yang berkelanjutan.

---

### Evaluasi Subjektif

Dari sisi pengguna, hasil rekomendasi dinilai **relevan dan masuk akal**. Film-film yang muncul dalam daftar memiliki kemiripan tema dengan *The Avengers*, meskipun berasal dari waralaba yang berbeda. Hal ini menunjukkan bahwa sistem mampu mengidentifikasi kesamaan konteks dan genre dengan baik.

---

### Evaluasi Presisi Sederhana

Karena tidak tersedia label relevansi eksplisit atau data umpan balik pengguna, evaluasi presisi dilakukan secara subjektif berdasarkan analisis konten film.

Dari 15 film teratas yang direkomendasikan berdasarkan *The Avengers*, sebanyak **14 film** dinilai relevan secara tematik dan genre. Hanya satu film, yaitu *The Image Revolution*, yang tidak termasuk kategori film superhero.

```text
Precision = True Positives / (True Positives + False Positives)
Precision = 14 / (14 + 1) = 0.9333 atau 93.3%
```

Dengan nilai presisi sebesar **93.3%**, sistem menunjukkan performa yang sangat baik dalam memberikan rekomendasi yang relevan dan berkaitan dengan film favorit pengguna.

---


## 7. Kesimpulan

Dalam proyek ini, telah berhasil dibangun sebuah sistem rekomendasi film menggunakan pendekatan **Content-Based Filtering**, yang memanfaatkan teknik **TF-IDF Vectorization** dan **Cosine Similarity**. Sistem ini merekomendasikan film berdasarkan kemiripan konten seperti genre, alur cerita, karakter, dan aspek sinematik lainnya.

Hasil evaluasi menunjukkan bahwa sistem mampu memberikan rekomendasi yang relevan terhadap film favorit pengguna, seperti *The Avengers*. Rekomendasi yang dihasilkan mencakup film-film superhero dari Marvel Cinematic Universe (MCU) maupun dari waralaba lain seperti *X-Men*, namun tetap konsisten dalam tema: aksi, pahlawan super, dan fiksi ilmiah.

Secara metrik, sistem memperoleh nilai **presisi sebesar 93.3%**, dengan 14 dari 15 film rekomendasi dinilai relevan. Ini menunjukkan bahwa pendekatan content-based yang digunakan cukup efektif dalam memahami dan mencocokkan preferensi pengguna, bahkan tanpa data eksplisit mengenai interaksi atau riwayat pengguna.

Ke depan, sistem ini masih memiliki ruang untuk ditingkatkan, seperti dengan menggabungkan pendekatan lain seperti **Collaborative Filtering** atau membangun **Hybrid Recommender System**, serta menambahkan mekanisme feedback dari pengguna guna memperkuat personalisasi dan akurasi hasil rekomendasi.

---

## 8. Referensi

1. Ricci, F., Rokach, L., & Shapira, B. (2015). *Recommender Systems Handbook*. Springer.
2. Aggarwal, C. C. (2016). *Recommender Systems: The Textbook*. Springer.
3. Scikit-learn: TF-IDF Vectorizer  
   https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html
4. Cosine Similarity – Towards Data Science  
   https://towardsdatascience.com/cosine-similarity-how-does-it-measure-the-similarity-maths-behind-and-python-implementation-50ad30aad7db
5. MovieLens Dataset – GroupLens  
   https://grouplens.org/datasets/movielens/

