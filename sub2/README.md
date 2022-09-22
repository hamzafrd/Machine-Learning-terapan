# Laporan Proyek Machine Learning - Hamza Firdaus

---

## Domain Proyek

---

Dokumentasi ini merupakan bagian dari dan dapat diakses melalui : https://github.com/hamzafrd/Machine-Learning-terapan/tree/main/sub2
Domain proyek yang dipilih dalam proyek machine learning ini adalah mengenai edukasi dan hobi dengan judul proyek _"Sistem Rekomendasi - Book Recomendation"_

### Latar Belakang

Buku merupakan sumber berbagai informasi yang dapat membuka wawasan kita tentang berbagai hal seperti ilmu pengetahuan, sosial, budaya, maupun aspek-aspek kehidupan lainnya. Selain itu, dengan membaca, dapat membantu mengubah masa depan, serta dapat menambah kecerdasan akal dan pikiran kita.

Di masa yang semakin maju ini, kegiatan membaca buku bisa dilakukan secara online. Tak dapat dipungkiri, tren membaca buku ini mengalami perubahan yang sangat signifikan terutama pada masa pandemi.Para pembaca saat ini cenderung mengakses dan membeli buku secara online daripada pergi ke toko buku, yang jelas menimbulakan masalah karena dapat meningkatkan pertumbuhan data yang sangat signifikan di internet. Hal ini dapat menyulitkan seseorang untuk mendapatkan informasi buku secara cepat dan pada saat dibutuhkan. Untuk itu diperlukan sistem rekomendasi yang dapat membantu seseorang menemukan informasi sebuah buku yang sesuai dengan kebutuhannya.

## Business Understanding

---

### Problem Statement

Berdasarkan pada latar belakang di atas, permasalahan yang dapat diselesaikan pada proyek ini adalah sebagai berikut:

- Bagaimana cara merekomedasikan buku yang baik ?
- Bagaimana cara membangun model yang dapat merekomedasikan buku sesuai keinginan user ?

### Goals

Tujuan dibuatnya proyek ini adalah sebagai berikut:

- Mengetahui cara merekomendasikan buku yang baik dengan melakukan analisa pada data buku menggunakan model yang optimal.
- Membangun model  _machine learning_ untuk merekomendasikan daftar buku menggunakan _content based filtering_

### Solution Statement

Solusi yang dapat dilakukan untuk memenuhi tujuan dari proyek ini di antaranya:

- **Pra-pemrosesan Data**. Pada prapemrosesan data dapat dilakukan beberapa tahapan, antara lain:

  - Deskripsikan variable yang ada pada dataset.  
  - Melakukan Filtering terhadap data.  
  - Melakukan _merge_ terhadap rating dan books   
  - Menangani missing value pada data.
  - Menangani duplicate value pada data.
  - Lakukan _dropping_ terhadap data yang tidak digunakan.

- **Pembangunan Model**.
  - Membangung sistem rekomendasi menggunakan teknik yang umum digunakan yaitu: Content-Based Filtering

## **Data Understanding**

---

### Informasi Dataset

Dataset yang digunakan pada proyek ini, yaitu dataset lengkap dengan title dan judul banyak buku. Informasi lebih lanjut mengenai dataset tersebut dapat lihat pada tabel berikut:

| Jenis                   | Keterangan                                                                              |
| ----------------------- | --------------------------------------------------------------------------------------- |
| Sumber                  | Dataset: [Kaggle](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset) |
| Dataset Owner           | MÖBIUS                                                                                  |
| Lisensi                 | CC0: Public Domain                                                                      |
| Kategori                | Literature                                                                              |
| Usability               | 10.00                                                                                   |
| Jenis dan Ukuran Berkas | CSV (106.94 MB)                                                                         |

Pada proyek ini kita akan menggunakan 2 dataset yaitu _Books.csv_ dan _Ratings.csv_ yang memiliki data sebagai berikut :

- **_Books.csv_**  
  - `ISBN`: Kode unik buku
  - `title`: Judul Buku.
  - `year`: Tahun penerbitan buku.
  - `publibsher` : Penerbit buku.
  - `author`: Pengarang buku.

- **_Ratings.csv_**  
  - `user_id`: Kode unik user.
  - `ISBN`: Kode unik buku
  - `rating`: Penilaian dari user.

Dari output tersebut dapat di deskripsikan sebagai berikut:

- Terdapat 6 kolom dengan tipe object, yaitu: _`ISBN`, `year`,  `publisher`, `title`, `author`_, dan _`rating`_.  
- terdapat 1 kolom tipe data lainnya yaitu int64 yang terdapat pada _`user id`_.
- Jumlah untuk dataset rating yaitu sebanyak 1149780 dan jumlah dataset books yaitu sebanyak 271360.
- author merupakan target fitur kali ini.

# **Data Preprocessing**

---

### Mengidentifikasi Data dan Merging data

- Melakukan _Filtering_  
  Pada dataset books dan rating terdapat beberapa data yang memiliki value yang dapat menggangu, sehingga penulis melakukan filter terhadap data yang akan di proses seperti data user yang memberikan jumlah rating < 200 dari total buku yang telah dibaca tidak akan di proses.

- Membuat _SUM rating_  
  _SUM rating_ dibuat untuk menghitung banyaknya rating yang diberikan oleh user pada setiap buku.

- _Merge rating and Books_  
  Kedua dataset _`rating`_ dan _`books`_ yang telah di proses digabung melalui tabel _ISBN_ menggunakan _`merge`_.

## Data Preparation

---

### _missing value_ dan _duplicate value_

- Mengatasi _missing value_  
  Pada dataset books terdapat 3 kolom yang memiliki missing value yaitu _SUM rating, author dan _publiser_. Untuk itu penuliskan melakukan drop menggunakan `dropna()`. Adapun dataset rating tidak memiliki _missing value_.

- Mengatasi _duplicate value_  
  Pada tahap ini penulis menghapus _duplicate value_ pada ISBN dan title dengan metode _`drop_duplicate()`_.
  

### Drop fitur tidak signifikan

- Pada tahap ini penulis menghapus beberapa fitur yang tidak memberikan informasi terkait buku seperti, _'year', 'location', dan 'age'_.

### Normalisasi dan splitting

- Normalisasi
  Normalisasi dilakukan menggunakan _`MinMaxScaler`_. Pada proyek ini fitur yang di normalisasi adalah fitur _`rating`_. Berikut adalah tahapannya :  
  - Ambil values yang ada pada fitur rating menggunnakan _`['rating'].values`_ dan masukan dalam sebuah variable.  
  - Reshape variable yang ada dengan _`reshape(-1,1)`_  
  - lakukan transform menggunakan _`MinMaxScaler`_ untuk melakukan normalisasi.
  - 
 -train and test split
  Pada proyek kali ini proses split ini dilakukan dengan cara membagi data dengan perbandingan 9:1 yang mana 90% untuk Train dan 10% untuk test.
  Data yang ada pada train and test adalah data yang sudah di normalisasi.

## **Content Based Filtering**

---

### Menghapus fitur tidak signifikan

Pada proyek ini penulis menggunakan fitur _'title', 'author', dan 'publisher'_, sehingga fitur lain _'ISBN', 'Rating SUM', 'year'_ bisa dihapus. sehingga hasil tabel menjadi sebagai berikut :  
| title                | author               | publisher               |
| -------------------- | -------------------- | ----------------------- |
|The Kitchen God's Wife|Amy Tan	              | Putnam Pub Group        |
|The Testament	       |John Grisham	        | Dell                    |
| Beloved (Plume Contemporary Fiction)  |	Toni Morrison|	Plume         |

## Modeling

Model yang akan digunakan proyek kali ini yaitu menggunakan pendekatan _content based filtering_ menggunakan TfidfVectorizer. Hal pertama yang dilakukan adalah melakukan _`fit()`_ data menggunakan _TfidfVectorizer_ yang selanjutnya di transform menggunakan metode _`fit_transform()`_. Jika sudah, lakukan _densing_ pada data menggunakan metode _`to.dense()`_ untuk menghasilkan vektor tf-idf dalam bentuk matriks. Sekarang, kita akan menghitung derajat kesamaan (similarity degree) antar restoran dengan teknik _cosine similarity_ menggunakan fungsi _`cosine_similarity(tfidf_matrix)`_ dengan begitu kita dapat merekomendasikan daftar author buku mana saja yang mirip dengan author yang sebelumnya pernah dibaca pengguna.

## _Content Based Filtering_

_Content-based filtering_ adalah pemfilteran berbasis konten di mana sistem ini memberikan rekomendasi untuk menebak apa yang disukai pengguna berdasarkan aktivitas pengguna tersebut. Tujuan dari _content based filtering_ adalah untuk memprediksi persamaan sejumlah informasi yang didapat dari pengguna. Sebagai contoh, seorang pembaca sedang membaca buku tentang saham. Platform baca buku online secara sistem akan merekomendasikan si pengguna untuk membaca buku lain yang berhubungan dengan saham.

_Content based filtering_ menggunakan konsep perhitungan _vector_, [TF-IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf), dan [Cosine Similarity](https://en.wikipedia.org/wiki/Cosine_similarity) sehingga data yang ada di dalam dataset terkonversi menjadi vektor.

### Kelebihan

- Dapat merekomendasikan item khusus
- Tidak memerlukan data apapun terhadap pengguna
- Semakin banyak informasi yang diberikan pengguna, semakin baik akurasi sistem rekomendasi

### Kelemahan

- Kelemahan utama pada teknik ini yaitu sistem tidak dapat memberikan rekomendasi apabila belum adanya penilaian pada object yang di rekomendasikan.
- Data yang kurang kurat ketika penilaian pada satu data terlalu sedikit

### Result

Untuk mendapatkan rekomendasi, kita menggunakan buku yang berjudul "_Birthright_" dengan author "_Nora Roberts_". Jika sistem rekomendasi berjalan dengan baik, maka kita akan mendapatkan hasil buku dengan author yang sama yaitu "_Nora Roberts_". Berikut adalah hasilnya :

| title                | author               | publisher               |
| -------------------- | -------------------- | ----------------------- |
|Face the Fire (Three Sisters Island Trilogy) |	Nora Roberts	|Jove Books|
|	Key of Light (Key Trilogy (Paperback))      |	Nora Roberts|	Jove Books|
|	Truly, Madly Manhattan                      |	Nora Roberts	|Silhouette|
|	Engaging The Enemy                          |	Nora Roberts	|Silhouette|
|	Key of Valor (Roberts, Nora. Key Trilogy, 3.)	|Nora Roberts|	Jove Pubns|
|	Sanctuary                                   |	Nora Roberts|	Jove Books|
|	Heaven and Earth (Three Sisters Island Trilogy)|	Nora Roberts|	Jove Books|
|	Heart of the Sea (Irish Trilogy)            |	Nora Roberts|	Jove Books|
|	Macgregor Brides (Macgregors)               |	Nora Roberts|	Silhouette|
|	Sea Swept (Quinn Brothers (Paperback))      |	Nora Roberts|	Jove Books|

Dapat kita lihat bahwa buku yang muncul memiliki author yang sama.

## Evaluation

---

Eevaluasi utnuk sistem rekomendasi dengan pendekatan _content based filtering_ di proyek ini adalah metric yaitu _precision K_ atau _nearest neighbors algorithm_ yang kurang lebih sama dengan algoritma K nearest yang digunakan untuk clustering berdasarkan jarak antar data.

![image](https://user-images.githubusercontent.com/96603987/191609256-82b147a5-6591-4f4f-926b-50ed72bb1f42.png)

Dalam proyek ini , penulis menggunakan _k_ sebesar sepuluh dan menghasilkan output sebanyak 9 data yang mana artinya sebagai berikut :

Relevan : _Rating_ > 5  
Tidak relevan : _Rating_ < 5  
Sehingga bisa dikatakan prediksi yang dilakukan oleh sistem relevan. Dari hasil rekomendasi yang dihasilkan, didapatkan _precision_ sebagai berikut :  

_precision@10 = 9 / 10_  
_precision@10 = 90%_  

Karena terdapat 9 buku yang memiliki rating di atas _threshold_ maka didapatkan 90% _precision_ dari model sistem rekomendasi dengan pendekatan _content based filtering_.
  
# Referensi :

---

-  Brideau, Ryan. (2021). _Precision@k: The Overlooked Metric for Fraud and Lead Scoring Models_. towardsdatascience. Retrieved September 22, 2022, from https://towardsdatascience.com/precision-k-the-overlooked-metric-for-fraud-and-lead-scoring-models-fabad2893c01  
-  Google. (2022). _Content-based Filtering_. Google Developer. Retrieved September 22, 2022, from https://developers.google.com/machine-learning/recommendation/content-based/basics  
-  MONAKA, PMKB. (2018). _Apa sih Manfaat Membaca ?_. sibopaksara. Retrieved September 22, 2022, from http://sibopaksara.kemdikbud.go.id/artikel-detail/apa-sih-manfaat-membaca#:~:text=Buku%20merupakan%20sumber%20berbagai%20informasi,kecerdasan%20akal%20dan%20pikiran%20kita.  
-  Malaeb, M. (2020, September 2). _Recall and precision at K for Recommender Systems. Medium_.  Retrieved September 21, 2022, from https://medium.com/@m_n_malaeb/recall-and-precision-at-k-for-recommender-systems-618483226c54#:~:text=In%20the%20computation%20of%20precision,precision%20at%20k%20to%201.  
-  Deutschman, Z. (2022, July 22). _Recommender Systems: Machine Learning Metrics and business metrics_. neptune.ai.Retrieved September 20, 2022, from https://neptune.ai/blog/recommender-systems-metrics  
