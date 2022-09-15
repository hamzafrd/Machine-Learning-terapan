# Laporan Proyek Machine Learning - Hamza Firdaus
## Domain Proyek

Domain proyek yang dipilih dalam proyek machine learning ini adalah mengenai keuangan dan cryptocurrency dengan judul proyek _"Predictive Analysis - Crypto Currency Historical Prices (DogeCoin)"_

### Latar Belakang

 Dogecoin merupakan mata uang crypto yang ditemukan oleh insinyur perangkat lunak Billy Markus, yang memutuskan untuk membuat sistem pembayaran yang bebas dari biaya perbankan tradisional. DogeCoin dengan cepat mengembangkan komunitas online-nya sendiri, mencapai kapitalisasi pasar sebesar US $ 70.355.561.773 pada 16 April 2021. Dengan semakin maraknya pemakaian _cryptocurrency_ dan mata uang digital di era sekarang, apalagi saat era covid, Dibutuhkan keputusan yang kuat dan analisis terproses agar dapat meminimalisir kesalahan dalam mengambil keputusan yang mengakibatkan kerugian dan pengaruh dalam transaksi aset digital tersebut di masa mendatang terutama pada transaksi **DogeCoin** yang akan kita bahas dalam laporan ini.

Pada proyek ini akan dibangun model machine learning untuk memprediksi kapitalisasi pasar **DogeCoin**. Model machine learning ini di harapkan dapat membantu dan memudahkan analisa serta dapat mengambil keputusan yang tepat mengenai strategi berinvestasi dalam dunia cryptocurrency, melihat dari besaran kapital pasar yang telah ada selama ini sehingga dapat meminimalisir kesalahan investasi dan kerugian di masa mendatang. Diharapkan, dengan dibuatnya model machine learning ini, bukan hanya untuk edukasi, tetapi bisa menjadi langkah awal menuju dunia machine learning industri yang sebenarnya.


## Business Understanding

### Problem Statements
Berdasarkan pada latar belakang di atas, permasalahan yang dapat diselesaikan pada proyek ini adalah sebagai berikut:

-   Bagaimana cara menganalisa data harga **DogeCoin** yang baik ?
-   Bagaimana cara memprediksi kapitalisasi pasar **DogeCoin** ?
-   Bagaimana cara membangun model yang dapat memprediksi harga pasar terhadap **DogeCoin** dengan baik ?

### Goals
Tujuan dibuatnya proyek ini adalah sebagai berikut:

-   Menganalisis data harga **DogeCoin** menggunakan model yang optimal.
-   Membangun _machine learning_ untuk memprediksi kapitalisasi pasar **DogeCoin**  di masa mendatang.
-   Memproses model dengan grid search, yaitu teknik untuk menentukan model yang dapat memproses data latih dengan baik.

### Solution statements
Solusi yang dapat dilakukan untuk memenuhi tujuan dari proyek ini di antaranya:

- **Pra-pemrosesan Data**. Pada pra-pemrosesan data dapat dilakukan beberapa tahapan, antara lain:

    -   Deskripsikan variable yang ada pada dataset.
    -   Lakukan _dropping_ terhadap data yang tidak digunakan.
    -   Menangani missing value pada data.
    -   Menangani Outliner pada data menggunakan box plot dan IQR method.
    -   Normalisasi fitur numerik pada dataset.
  
- **Pembangunan Model**. Pada pembangunan model terdapat beberapa algoritma yang digunakan, antara lain:
  - **Grid Search**
  - **K-Nearest Neighbor** 
  - **Random Forest**
  - **Gradient Boosting Algorithm**
  - **Support Vector Regression**
    
## Data Understanding
- **Informasi Dataset**
  <br> Dataset yang digunakan pada proyek ini yaitu dataset lengkap dengan riwayat harga **DogeCoin**, informasi lebih lanjut mengenai dataset tersebut dapat lihat pada tabel berikut:

  | Jenis                   | Keterangan                                                                              |
  | ----------------------- | --------------------------------------------------------------------------------------- |
  | Sumber                  | Dataset: [Kaggle](https://www.kaggle.com/datasets/sudalairajkumar/cryptocurrencypricehistory?select=coin_Dogecoin.csv) |
  | Dataset Owner           | sudalairajkumar                                                                           |
  | Lisensi                 | CC0: Public Domain                                                                        |
  | Kategori                | Cryptorrency, Currencies                                                                    |
  | Usability               | 9.71                                                                                       |
  | Jenis dan Ukuran Berkas | CSV (394.81 kB)                                                                           |

  Dataset ini memiliki format .csv yang mempunyai total 2760 data dengan 10 kolom `SNo, Name, Symbol, Date, High, Low, Open, Close, Volume, Marketcap` yang tidak memiliki missing value pada masing-masing kolom dengan informasi sebagai berikut :  
  

---


-   Sno : adalah nomer tabel
-   Name : Nama Cryptocurrency
-   Symbol : Simbol pada cryptocurrency
-   Date : Tanggal pencatatan data
-   Open : harga pembukaan hari itu
-   Close : harga penutupan hari itu
-   Low : harga terendah hari itu
-   High : harga tertinggi hari itu
-   Volume : volume transaksi perhari
-   Market Cap : Kapitalisasi Pasar berdasarkan USD

Dari output terlihat bahwa:

- Terdapat 3 kolom dengan tipe object, yaitu: name, symbol, dan date. Kolom ini merupakan categorical features (fitur non-numerik).
- Terdapat 6 kolom numerik dengan tipe data float64 yaitu: High, Low, Open, Volume, Close, dan Marketcap.   
- Marketcap merupakan target fitur kali ini.

#### **Exploratary Data Analysist**
  <br> Berikut merupakan visualisasi data yang menunjukkan sebaran/distribusi data pada setiap fitur-fitur numerik (`Volume, Marketcap, High`) sebagai example :
  
  - Mengidentifikasi Missing Value dan Outlier
    <br>
    - Fitur High
    <image src='https://github.com/hamzafrd/Machine-Learning-terapan/blob/ebdb036d8ea21216afcb582a22fdc6383765bbac/images/high.png' width= 300/>
    <br>
    - Fitur marketplace
    <br>
    <image src='https://github.com/hamzafrd/Machine-Learning-terapan/blob/ebdb036d8ea21216afcb582a22fdc6383765bbac/images/marketplace.png' width= 300/>
    <br>
    - Fitur  volume
    <br>
    <image src='https://github.com/hamzafrd/Machine-Learning-terapan/blob/ebdb036d8ea21216afcb582a22fdc6383765bbac/images/volume.png' width= 300/>
    <br> Terlihat jika di atas banyak terdapat outlier pada setiap variabel, lalu untuk mengatasinya nantinya penulis akan menerapkan batas bawah dan batas atas menggunakan metode IQR
    <br> Setelah beberapa kali melakukan IQR, berikut hasilnya :
    
    - Fitur MarketPlace
    <image src='https://github.com/hamzafrd/Machine-Learning-terapan/blob/07225ebf9fef1741d754e547f1ed495820db5835/images/aftermarket.png' width= 300/>
    <br>
    - Fitur High
    <br>
    <image src='https://github.com/hamzafrd/Machine-Learning-terapan/blob/07225ebf9fef1741d754e547f1ed495820db5835/images/afterhigh.png' width= 300/>
    <br>
    - Fitur  Close
    <br>
    <image src='https://github.com/hamzafrd/Machine-Learning-terapan/blob/07225ebf9fef1741d754e547f1ed495820db5835/images/afterclose.png' width= 300/>
    <br>
    
  - Univariate Analysis
    <br>
    <image src='https://github.com/hamzafrd/Machine-Learning-terapan/blob/03b5a313282b61bf6c154e58c97b66aea63083e9/images/univariate.png' width= 500/>
    <br> Terlihat pada grafik bahwa semua data cenderung distribusi nilainya membentuk seperti camel (naik dan turun). Walaupun ada yang berbeda yaitu pada Volume yang naik pada bagian kiri (left-skewed).
    
  - Multivariate Analysis
    <br>
    <image src='https://github.com/hamzafrd/Machine-Learning-terapan/blob/03b5a313282b61bf6c154e58c97b66aea63083e9/images/multivariat.png' width= 500/>
    <br> Terlihat bahwa numerical features memiliki korelasi yang tinggi.
    
  - Mengevaluasi Skor Korelasi dengan fungsi curr()
    <br>
    <image src='https://github.com/hamzafrd/Machine-Learning-terapan/blob/03b5a313282b61bf6c154e58c97b66aea63083e9/images/korelasi.png' width= 500/>
    <br> Terlihat pada matriks korelasi di atas dapat disimpulkan bahwa hampir semua variabel memiliki keterikatan dan korelasi yang kuat antar variabel lainnya, dimana nilai korelasi antar variabel bernilai lebih dari 0.9 atau mendekati 1.
    <br> Volume memiliki korelasi yang sangat lemah dengan yang lain, artinya jumlah transaksi (volume) tidak ada hubungannya dengan fitur lain dan bisa di drop. 
 
   - Melakukan drop terhadap fitur tidak signifikan
     <br>
     <br> Disini penulisan melakukan drop pada 'Volume','Name', 'Symbol', 'Date' karena akan meganggu proses pembuatan model.
     
## Data Preparation
Berikut ini merupakan tahapan-tahapan dalam melakukan pra-pemrosesan data:
  - **Melakukan pembagian dataset**
    <br> Dataset akn dibagai menjadi 2 yaitu sebagai *train* data dan *test* . Train data digunakan untuk *training* model dan *test* data digunakan sebagai validasi model. Proposi yang saya gunakan disini adalah 80:20, 80% sebagai *train* data dan 20% sebagai *test* data.
    
  - **Normalisasi data**
  <br>Normalisasi membantu untuk membuat semua fitur numerik berada dalam skala data yang kecil (0 - 1) dan membuat fitur data menjadi bentuk yang lebih mudah diolah oleh algoritma. Pada dataset ini saya menggunakan **MinMaxScaler** untuk melakukan normalisasi pada kategori numerik.
  
## Modeling
Pada proyek ini, Proses modeling dalam proyek ini menggunakanModel yang akan digunakan proyek kali ini yaitu *Support Vector Regression, Gradient Boosting, Random Forest* dan  *K-Nearest Neighbors*. kemudian membandingkan performanya.

- **K-Nearest Neighbor**
  <br> K-Nearest Neighbors* merupakan algoritma machine learning yang bekerja dengan mengklasifikasikan data baru menggunakan kemiripan antara data baru dengan sejumlah data (k)
  -   Kelebihan:
      -   Algoritma KNN merupakan algoritma yang sederhana dan mudah untuk diimplementasikan.
      -   Dapat di implementasikan pada beberapa kasus seperti klasifikasi, regresi dan pencarian.
  -   Kekurangan:
      -   Algoritma KNN menjadi lebih lambat secara signifikan seiring meningkatnya jumlah sampel dan/atau variabel independen.

- **Random Forest**
  <br> Algoritma ini disusun dari banyak algoritma pohon (decision tree) yang pembagian data dan fiturnya dipilih secara acak.
  -   Kelebihan :
      -   Algoritma Random Forest merupakan algoritma dengan pembelajaran paling akurat yang tersedia. Untuk banyak kumpulan data, algoritma ini menghasilkan pengklasifikasi yang sangat akurat.
      -   Berjalan secara efisien pada data besar.
      -   Dapat menangani ribuan variabel input tanpa penghapusan variabel.
      -   Memberikan perkiraan variabel apa yang penting dalam klasifikasi.
      -   Memiliki metode yang efektif untuk memperkirakan data yang hilang dan menjaga akurasi ketika sebagian besar data hilang.
  -   Kekurangan :
      -   Algoritma Random Forest overfiting untuk beberapa kumpulan data dengan tugas klasifikasi/regresi yang _bising/noise_.
      -   Untuk data yang menyertakan variabel kategorik dengan jumlah level yang berbeda, Random Forest menjadi bias dalam mendukung atribut dengan level yang lebih banyak. Oleh karena itu, skor kepentingan variabel dari Random Forest tidak dapat diandalkan untuk jenis data ini.

- **Support Vector Regression**
  <br>*Support Vector Regression* memiliki prinsip yang sama dengan SVM, namun SVM biasa digunakan dalam klasifikasi. Pada SVM, algoritma tersebut berusaha mencari jalan terbesar yang bisa memisahkan sampel dari kelas berbeda, sedangkan SVR mencari jalan yang dapat menampung sebanyak mungkin sampel di jalan. Untuk hyper parameter yang digunakan pada model ini adalah sebagai berikut :
  <br>
  <br>*C* : Hyperparameter ini adalah parameter regularisasi digunakan untuk menukar klasifikasi yang benar dari contoh *training* terhadap maksimalisasi margin fungsi keputusan.
  <br>*gamma* :Hyperparameter ini digunakan untk menetukan seberapa jauh pengaruh satu contoh pelatihan mencapai, dengan nilai rendah berarti jauh dan nilai tinggi berarti dekat.
  <br>*kernel* : menentukan kernel untuk matriks  
 
  -   Kelebihan :
      -   Lebih efektif pada data dimensi tinggi (data dengan jumlah fitur yang banyak)
      -   Memori lebih efisien karena menggunakan subset poin pelatihan

  -   Kekurangan :
      -   Tidak cocok untuk data berukuran besar

- **Gradient boosting Algorithm**
  <br> Gradient Boosting adalah algoritma machine learning yang menggunakan teknik *ensembel learning* dari *decision tree* untuk memprediksi nilai. Gradient Boosting sangat mampu menangani pattern yang kompleks dan data ketika linear model tidak dapat menangani. Untuk hyperparameter yang digunakan pada model ini ada 3 yaitu :
  <br>*learning_rate* : Hyperparameter training yang digunakan untuk menghitung nilai koreksi bobot padad waktu proses training. Umumnya nilai learning rate berkisar antara 0 hingga 1
  <br>*n_estimators* : Jumlah tahapan boosting yang akan dilakukan.
  <br>*criterion* : Hyperparameter yang digunakan untuk menemukan fitur dan ambang batas optimal dalam membagi data
  -   Kelebihan :
      -   Algoritma Boosting dapat mengurangi bias pada data.
      -   Hasil pemodelan yang lebih akurat.
      -   Algoritma ini sangat powerful dalam meningkatkan akurasi prediksi.
  -   Kekurangan :
      -   Waktu komputasi dan desain tinggi.
      -   Tingkat kesulitan yang tinggi dalam pemilihan model

## Evaluation   
Untuk evaluasi, metrik yang digunakan adalah *mean squared error (mse)*. Dimana metrik ini mengukur seberapa dekat garis pas dengan titik data.  
<image src='https://github.com/hamzafrd/Machine-Learning-terapan/blob/8cbab7aca53d33482a26a55f535867db2b312ed5/images/mse.png' width= 500/>  
<br> Keterangan:
- N = jumlah dataset
- yi = nilai sebenarnya
- yi^ = nilai prediksi

Sebelum menggunakan metrik MSE, harus dilakukan scaling fitur numerik terlebih dahulu pada data uji untuk menghindari kebocoran data. Setelah melakukan evaluasi berdasarkan metrik MSE dan tingkat akurasi prediksi pada model, penulis mencoba memprediksi harga untuk 30 hari ke depan dengan model KNN dan hasilnya cukup memuaskan karena nilainya tidak jauh berbeda dengan data sebelumnya.

Berikut ini perbandingan grafik metrik MSE pada keempat model:
<br>
<image src='https://github.com/hamzafrd/Machine-Learning-terapan/blob/03b5a313282b61bf6c154e58c97b66aea63083e9/images/plottingfinal.png' width= 500/>
<br> Untuk proyek kali ini model SVM merupakan model yang berjalan dengan performa paling optimal sehingga dapat disimpulkan bahwa model dapat memprediksi harga dari pasar dogecoin dari data tes dengan baik. Sehingga kedepannya dapat membantu para trader dalam melakukan keputusan pembelian/penjualan pasar.
