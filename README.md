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

Pemeriksaan terhadap data dilakukan untuk memastikan tidak adanya nilai kosong (missing value) pada fitur-fitur penting yang akan digunakan dalam proses pembuatan sistem rekomendasi. Hasil dari pengecekan menunjukkan bahwa **tidak terdapat missing value** pada kolom-kolom utama yang menjadi kandidat fitur rekomendasi, seperti `title`, `overview`, `genres`, `cast`, dan `director`.

Dengan tidak adanya nilai kosong pada kolom-kolom tersebut, maka tidak diperlukan proses imputasi data maupun pembersihan tambahan. Hal ini menunjukkan bahwa data dalam kondisi bersih dan siap untuk diproses lebih lanjut pada tahap data preparation dan modeling.

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

| Index | combined_features |
|-------|-------------------|
| 0 | action adventure fantasy science fiction culture clash future space war space colony society enter the world of pandora sam worthington zoe saldana sigourney weaver stephen lang michelle rodriguez james cameron |
| 1 | adventure fantasy action ocean drug abuse exotic island east india trading company love of ones life at the end of the world the adventure begins johnny depp orlando bloom keira knightley stellan skarsguerd chow yunfat gore verbinski |
| 2 | action adventure crime spy based on novel secret agent sequel mi a plan no one escapes daniel craig christoph waltz luea seydoux ralph fiennes monica bellucci sam mendes |
| 3 | action crime drama thriller dc comics crime fighter terrorist secret identity burglar the legend ends christian bale michael caine gary oldman anne hathaway tom hardy christopher nolan |
| 4 | action adventure science fiction based on novel mars medallion space travel princess lost in our world found in another taylor kitsch lynn collins samantha morton willem dafoe thomas haden church andrew stanton |
| 5 | fantasy action adventure dual identity amnesia sandstorm love of ones life forgiveness the battle within tobey maguire kirsten dunst james franco thomas haden church topher grace sam raimi |
| 6 | animation family hostage magic horse fairy tale musical theyre taking adventure to new lengths zachary levi mandy moore donna murphy ron perlman mc gainey byron howard |
| 7 | action adventure science fiction marvel comic sequel superhero based on comic book vision a new age has come robert downey jr chris hemsworth mark ruffalo chris evans scarlett johansson joss whedon |
| 8 | adventure fantasy family witch magic broom school of witchcraft wizardry dark secrets revealed daniel radcliffe rupert grint emma watson tom felton michael gambon david yates |
| 9 | action adventure fantasy dc comics vigilante superhero based on comic book revenge justice or revenge ben affleck henry cavill gal gadot amy adams jesse eisenberg zack snyder |

### Text Cleaning
Setelah penggabungan fitur, dilakukan proses pembersihan teks seperti:
- Mengubah semua huruf menjadi huruf kecil
- Menghapus karakter khusus atau tanda baca (jika diperlukan)
- Menghilangkan stop words (dilakukan saat TF-IDF)

Proses ini bertujuan untuk meningkatkan akurasi dan konsistensi pada saat transformasi teks menjadi vektor numerik.

---

1. Drop outliers menggunakan IQR: Mengidentifikasi dan menghapus *outlier* pada dataset menggunakan metode IQR (Interquartile Range).
2. Mengatasi missing value: Melakukan penanganan terhadap nilai yang hilang pada dataset, seperti menghapus baris atau mengisi nilai yang hilang dengan metode tertentu, seperti mean atau median.
3. Mengambil kolom yang diperlukan dan merubah nama kolom: Memilih kolom-kolom yang relevan untuk analisis dan memberikan nama baru jika diperlukan.
4. Exclude rating yang ingin dihapus dari dataset: Menghapus data dengan rating tertentu yang ingin dikecualikan dari analisis.
5. Reset index dataframe untuk menghindari error: Mereset indeks dataframe setelah melakukan operasi penghapusan atau pemrosesan data agar indeks kembali terurut secara berurutan.
6. Convert "rating" column to int64 data type: Mengubah tipe data kolom "rating" menjadi tipe data int64 untuk mempermudah analisis numerik.
7. Mendapatkan list unik kolom kursus dan keahlian: Mengidentifikasi dan mendapatkan daftar unik kolom "courseName" dan "skills" dalam dataset.

## 8. Modeling and Result

Pada tahap ini, dilakukan pembangunan model sistem rekomendasi film dengan pendekatan content-based filtering. Tujuannya adalah untuk merekomendasikan film kepada pengguna berdasarkan kemiripan konten dari film yang mereka sukai dengan film lainnya dalam dataset. Konten yang dianalisis mencakup informasi seperti genre, nama aktor, sutradara, hingga sinopsis dan kata kunci terkait. Proses modeling dimulai dengan mentransformasikan data teks menjadi representasi numerik menggunakan teknik TF-IDF (Term Frequency-Inverse Document Frequency), lalu dilanjutkan dengan perhitungan kemiripan antarfilm menggunakan cosine similarity. Hasil akhir dari proses ini adalah daftar rekomendasi film yang memiliki tingkat kemiripan konten tertinggi dengan film yang dipilih oleh pengguna.

### *Content-Based Filtering*
*Content-Based Filtering* adalah pendekatan dalam sistem rekomendasi yang mengandalkan analisis konten dari item yang direkomendasikan. 

Dalam konteks sistem rekomendasi kursus Coursera, pendekatan ini akan menganalisis fitur-fitur konten dari kursus, seperti deskripsi kursus, topik, rating, atau keterampilan yang terkait, untuk memberikan rekomendasi yang relevan kepada pengguna.

Kelebihan *Content-Based Filtering*:
1. Personalisasi: Pendekatan *Content-Based Filtering* memungkinkan personalisasi yang tinggi, karena rekomendasi didasarkan pada preferensi pengguna yang diungkapkan melalui analisis konten kursus.
2. Tidak tergantung pada data pengguna lain: Pendekatan ini tidak memerlukan informasi tentang preferensi pengguna lain, sehingga tidak bergantung pada data kolaboratif atau historis dari pengguna lainnya.
3. Memperhitungkan kepentingan unik pengguna: Pendekatan ini memperhitungkan preferensi pengguna yang spesifik dan tidak terpengaruh oleh tren atau preferensi umum.

Kekurangan *Content-Based Filtering*:
1. Terbatas pada fitur yang diamati: Pendekatan ini terbatas pada fitur-fitur yang diamati dan dianalisis dalam konten kursus. Rekomendasi mungkin kurang beragam jika tidak ada fitur yang signifikan dalam analisis konten yang dapat membedakan kursus secara signifikan.
2. Tidak memperhitungkan preferensi baru: Pendekatan ini tidak secara otomatis menyesuaikan dengan perubahan preferensi pengguna. Jika preferensi pengguna berubah atau berkembang, rekomendasi mungkin tetap berfokus pada preferensi yang lebih lama.

Teknik Perhitungan Similarity:
1. *Cosine Similarity*: *Cosine Similarity* mengukur kesamaan antara dua vektor dengan menghitung kosinus sudut antara vektor-vektor tersebut. Dalam konteks *Content-Based Filtering*, *Cosine Similarity* digunakan untuk mengukur kesamaan antara vektor representasi fitur kursus berdasarkan deskripsi, topik, atau keterampilan. Nilai *Cosine Similarity* berkisar antara -1 hingga 1, di mana nilai 1 menunjukkan kesamaan yang sempurna dan nilai -1 menunjukkan perbedaan yang sempurna.



Kedua teknik perhitungan *similarity* tersebut digunakan untuk membandingkan kesamaan antara kursus-kursus dalam sistem rekomendasi. 

### Tahapan yang dilakukan dengan pendekatan *Content-Based Filtering*
Selama pendekatan ini, proses modeling dilakukan berdasar urutan sebagai berikut ini:

1. *TF-IDF Vectorizer*: Tahap ini melibatkan penggunaan TF-IDF (Term Frequency-Inverse Document Frequency) Vectorizer untuk mengubah teks pada deskripsi kursus menjadi representasi numerik. TF-IDF mengukur pentingnya suatu kata dalam dokumen berdasarkan frekuensi kemunculan kata tersebut dalam dokumen dan inversi frekuensi kemunculan kata tersebut dalam seluruh koleksi dokumen. *TF-IDF Vectorizer* menghasilkan vektor fitur yang merepresentasikan konten kursus.

```sh
with 46280 stored elements and shape (1930, 8918)>
  Coords	Values
  (0, 38)	0.06775935967259236
  (0, 82)	0.0763854353999596
  (0, 2681)	0.09869592494123809
  (0, 7063)	0.09722062382559164
  (0, 2765)	0.09733188433797436
  (0, 1827)	0.2464279580101801
  (0, 1497)	0.2464279580101801
  (0, 3004)	0.16571973456875344
  (0, 7470)	0.32371811697052594
  (0, 8509)	0.12513827276424433
  (0, 1576)	0.23876881490058302
  (0, 7419)	0.21497734335387975
  (0, 2506)	0.2464279580101801
  (0, 8756)	0.1241504682467639
  (0, 5945)	0.2702194295568834
  (0, 6948)	0.14868011529780778
  (0, 8763)	0.22263648646347683
  (0, 8902)	0.21170593218101175
  (0, 6930)	0.21497734335387975
  (0, 7302)	0.21497734335387975
  (0, 8555)	0.21170593218101175
  (0, 7608)	0.15838905174573564
  (0, 4510)	0.23251083931838432
  (0, 5270)	0.16259723398960357
  (0, 6785)	0.19294645453503562
  :	:
  (1928, 4563)	0.25877464942128814
  (1929, 2267)	0.06987504629324362
  (1929, 3795)	0.17055941539429875
  (1929, 3692)	0.19162472212991682
  (1929, 1591)	0.07319019724182046
  (1929, 6689)	0.14303382155374422
  (1929, 7649)	0.15225226571638636
  (1929, 8545)	0.20761891742283564
  (1929, 172)	0.22446307399886795
  (1929, 5397)	0.2210473140089074
  (1929, 4169)	0.2033977672632499
  (1929, 1947)	0.1756879141259236
  (1929, 2853)	0.20544623074831453
  (1929, 3221)	0.19787326058767568
  (1929, 4638)	0.22446307399886795
  (1929, 8186)	0.1930877152317969
  (1929, 794)	0.17855651304075817
  (1929, 2662)	0.24930432822135967
  (1929, 4976)	0.24277022367678033
  (1929, 3087)	0.21240446277871444
  (1929, 3434)	0.24277022367678033
  (1929, 3118)	0.2179289694542886
  (1929, 4536)	0.23724571700120614
  (1929, 3392)	0.23724571700120614
  (1929, 2026)	0.2821426800903108

```

Output di atas merupakan representasi TF-IDF (Term Frequency-Inverse Document Frequency) dari kolom combined_features yang telah diproses menggunakan TfidfVectorizer. Hasilnya adalah sebuah sparse matrix berukuran (1930, 8918), yang menunjukkan bahwa terdapat 1930 dokumen (film) dan 8918 fitur unik (kata-kata penting yang muncul setelah preprocessing).

Setiap baris pada output (misalnya (0, 38) 0.0677) menunjukkan bahwa pada dokumen ke-0, terdapat fitur (kata) pada indeks ke-38 dengan bobot TF-IDF sebesar 0.0677. Nilai ini mencerminkan pentingnya kata tersebut dalam dokumen relatif terhadap seluruh korpus. Karena data TF-IDF umumnya sangat jarang (sparse) — sebagian besar elemen bernilai nol — maka hanya nilai-nilai yang bukan nol yang ditampilkan.

Matrix inilah yang menjadi representasi numerik (feature vector) dari setiap film yang kemudian digunakan untuk menghitung kemiripan antar film menggunakan metode seperti cosine similarity dalam tahap modeling sistem rekomendasi berbasis konten.
  
2. *Cosine Similarity*: Setelah mendapatkan vektor fitur menggunakan *TF-IDF Vectorizer*, tahap selanjutnya adalah menghitung kesamaan antara kursus menggunakan metode *Cosine Similarity*. *Cosine Similarity* mengukur kesamaan arah antara dua vektor dalam ruang vektor. Pada konteks Content-Based Filtering, *Cosine Similarity* digunakan untuk mengukur kesamaan antara vektor fitur kursus berdasarkan deskripsi, topik, atau keterampilan yang terkait. Semakin tinggi nilai *Cosine Similarity*, semakin mirip kedua kursus dalam hal fitur-fitur yang diamati.

Tabel 3. Hasil Perhitungan Cosine Similarity pada Matrix TF-IDF

```sh
[[1.         0.03938303 0.03464293 ... 0.         0.01380506 0.        ]
 [0.03938303 1.         0.01646641 ... 0.         0.03973226 0.        ]
 [0.03464293 0.01646641 1.         ... 0.         0.         0.        ]
 ...
 [0.         0.         0.         ... 1.         0.00423647 0.07444928]
 [0.01380506 0.03973226 0.         ... 0.00423647 1.         0.0047213 ]
 [0.         0.         0.         ... 0.07444928 0.0047213  1.        ]]
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
9. Ant-Man
10. X-Men: Apocalypse
11. X2
12. Captain America: The First Avenger
13. X-Men: The Last Stand
14. X-Men: Days of Future Past
15. Iron Man
```

Dari hasil output diatas ditunjukkan 15 film rekomendasi yang memiliki kesamaan atau kemiripan berdasarkan nilai cosine similiarity terdekat dengan parameter parameter fitur yang dipilih.

## 6. Evaluation

### Matriks Evaluasi untuk Rekomendasi berdasarkan 'The Avengers'

| Rank | Movie Title                              | Similarity Score |
|------|------------------------------------------|------------------|
| 1    | Avengers: Age of Ultron                  | 0.7907           |
| 2    | Captain America: The Winter Soldier      | 0.4241           |
| 3    | Captain America: Civil War               | 0.4093           |
| 4    | Iron Man 2                               | 0.3956           |
| 5    | Thor: The Dark World                     | 0.2951           |
| 6    | The Incredible Hulk                      | 0.2684           |
| 7    | Thor                                     | 0.2672           |
| 8    | X-Men                                    | 0.2639           |
| 9    | Ant-Man                                  | 0.2496           |
| 10   | X-Men: Apocalypse                        | 0.2471           |
| 11   | X2                                       | 0.2464           |
| 12   | Captain America: The First Avenger       | 0.2361           |
| 13   | X-Men: The Last Stand                    | 0.2289           |
| 14   | X-Men: Days of Future Past               | 0.2269           |
| 15   | Iron Man                                 | 0.2150           |

---

### Interpretasi Evaluasi

Model rekomendasi ini menggunakan pendekatan **Content-Based Filtering** dengan metode **Cosine Similarity**. Sistem menghitung kemiripan antar film berdasarkan kombinasi fitur seperti genre, karakter, alur cerita, dan elemen sinematik lainnya.

Meskipun tidak semua film berasal dari Marvel Cinematic Universe (MCU), seperti seri *X-Men*, semua film yang direkomendasikan masih termasuk dalam kategori **film superhero berbasis komik**, dan mengandung elemen yang mirip seperti aksi, fiksi ilmiah, dan pahlawan dengan kekuatan super.

---

### Evaluasi Subjektif

Dari sisi pengguna, hasil rekomendasi dinilai **relevan dan masuk akal**. Film-film yang muncul dalam daftar memiliki kemiripan tema dengan *The Avengers*, meskipun berasal dari waralaba yang berbeda. Hal ini menunjukkan bahwa sistem dapat mengidentifikasi kesamaan konteks dan genre dengan baik.

---

### Evaluasi Presisi Sederhana

Karena tidak tersedia label relevansi eksplisit atau data umpan balik pengguna, evaluasi presisi dilakukan secara subjektif berdasarkan penilaian terhadap hasil rekomendasi.

Dari 15 film teratas yang direkomendasikan berdasarkan *The Avengers*, sebanyak **10 film** dinilai relevan secara tematik dan genre.

```text
Precision = True Positives / (True Positives + False Positives)
Precision = 10 / (10 + 5) = 0.6667 atau 66.7%
```
Dengan nilai presisi sebesar 66.7%, sistem menunjukkan performa yang cukup baik dalam memberikan rekomendasi yang sesuai dan berkaitan dengan film favorit pengguna.

## 7. Kesimpulan

Dalam proyek ini, telah berhasil dibangun sebuah sistem rekomendasi film menggunakan pendekatan **Content-Based Filtering** dengan pemanfaatan teknik **TF-IDF Vectorization** dan **Cosine Similarity**. Sistem ini mampu merekomendasikan film yang relevan berdasarkan kemiripan konten, seperti genre, alur cerita, karakter, dan aspek sinematik lainnya.

Hasil evaluasi menunjukkan bahwa rekomendasi yang diberikan untuk film favorit pengguna seperti *The Avengers* tergolong relevan dan sesuai secara tematik. Meskipun sebagian film berasal dari waralaba berbeda seperti *X-Men*, kesamaan unsur aksi, superhero, dan latar fiksi ilmiah membuat hasil rekomendasi tetap tepat sasaran.

Dari sisi evaluasi metrik, sistem mencapai nilai **presisi sebesar 66.7%**, yang menunjukkan bahwa mayoritas rekomendasi yang dihasilkan tergolong relevan. Hal ini membuktikan bahwa pendekatan content-based cukup efektif, khususnya ketika data pengguna atau interaksi tidak tersedia.

Sistem ini dapat dikembangkan lebih lanjut dengan mengintegrasikan pendekatan lain seperti **Collaborative Filtering** atau **Hybrid Recommender System**, serta mempertimbangkan feedback eksplisit dari pengguna agar hasil rekomendasi semakin personal dan akurat.

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

