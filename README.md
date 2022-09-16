# Laporan Proyek Machine Learning - Hamza Firdaus



## Domain Proyek

---

Dokumentasi ini merupakan bagian dari dan dapat diakses melalui : https://github.com/hamzafrd/Machine-Learning-terapan
Domain proyek yang dipilih dalam proyek machine learning ini adalah mengenai keuangan dan cryptocurrency dengan judul proyek _"Predictive Analysis - Crypto Currency Historical Prices (DogeCoin)"_

### Latar Belakang

Dogecoin merupakan mata uang crypto yang ditemukan oleh insinyur perangkat lunak Billy Markus, yang memutuskan untuk membuat sistem pembayaran yang bebas dari biaya perbankan tradisional. DogeCoin dengan cepat mengembangkan komunitas online-nya sendiri, mencapai kapitalisasi pasar sebesar US $ 70.355.561.773 pada 16 April 2021. Dengan makin maraknya pemakaian _cryptocurrency_ dan mata uang digital di era sekarang, apalagi saat era covid, Dibutuhkan keputusan yang kuat dan analisis terproses agar dapat meminimalkan kesalahan dalam mengambil keputusan yang mengakibatkan kerugian dan pengaruh dalam transaksi aset digital tersebut di masa mendatang terutama pada transaksi **DogeCoin** yang akan kita bahas dalam laporan ini.

Pada proyek ini akan dibangun model machine learning untuk memprediksi kapitalisasi pasar **DogeCoin**. Model machine learning ini di harapkan dapat membantu dan memudahkan analisis serta dapat mengambil keputusan yang tepat mengenai strategi berinvestasi dalam dunia cryptocurrency, melihat dari besaran kapital pasar yang telah ada selama ini sehingga dapat meminimalkan kesalahan investasi dan kerugian di masa mendatang. Diharapkan, dengan dibuatnya model machine learning ini, bukan hanya untuk edukasi, tetapi bisa menjadi langkah awal menuju dunia machine learning industri yang sebenarnya.

## Business Understanding

---

### Problem Statements
Berdasarkan pada latar belakang di atas, permasalahan yang dapat diselesaikan pada proyek ini adalah sebagai berikut:

-   Bagaimana cara menganalisis data harga **DogeCoin** yang baik ?
-   Bagaimana cara memprediksi kapitalisasi pasar **DogeCoin** ?
-   Bagaimana cara membangun model yang dapat memprediksi harga pasar terhadap **DogeCoin** dengan baik ?

### Goals
Tujuan dibuatnya proyek ini adalah sebagai berikut:

-   Menganalisis data harga **DogeCoin** menggunakan model yang optimal.
-   Membangun _machine learning_ untuk memprediksi kapitalisasi pasar **DogeCoin**  di masa mendatang.
-   Memproses model dengan grid search, yaitu teknik untuk menentukan model yang dapat memproses data latih dengan baik.

### Solution statements
Solusi yang dapat dilakukan untuk memenuhi tujuan dari proyek ini di antaranya:

- **Pra-pemrosesan Data**. Pada prapemrosesan data dapat dilakukan beberapa tahapan, antara lain:

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

---

### **Informasi Dataset**
 Dataset yang digunakan pada proyek ini, yaitu dataset lengkap dengan riwayat harga **DogeCoin**, informasi lebih lanjut mengenai dataset tersebut dapat lihat pada tabel berikut:

| Jenis                   | Keterangan                                                   |
| ----------------------- | ------------------------------------------------------------ |
| Sumber                  | Dataset: [Kaggle](https://www.kaggle.com/datasets/sudalairajkumar/cryptocurrencypricehistory?select=coin_Dogecoin.csv) |
| Dataset Owner           | sudalairajkumar                                              |
| Lisensi                 | CC0: Public Domain                                           |
| Kategori                | Cryptorrency, Currencies                                     |
| Usability               | 9.71                                                         |
| Jenis dan Ukuran Berkas | CSV (394.81 kB)                                              |

Dataset ini memiliki format .csv yang mempunyai total 2760 data dengan 10 kolom `SNo, Name, Symbol, Date, High, Low, Open, Close, Volume, Marketcap` yang tidak memiliki missing value pada masing-masing kolom dengan informasi sebagai berikut :  

---


-   Sno : adalah nomor tabel
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

- Terdapat 3 kolom dengan tipe object, yaitu: name, symbol, dan date. Kolom ini merupakan categorical features (fitur nonnumerik).
- Terdapat 6 kolom numerik dengan tipe data float64, yaitu: High, Low, Open, Volume, Close, dan Marketcap.   
- Marketcap merupakan target fitur kali ini.

## **Exploratary Data Analysist**

---

Berikut merupakan visualisasi data yang menunjukkan sebaran/distribusi data pada setiap fitur-fitur numerik (`Volume, Marketcap, High`) sebagai example :

### Mengidentifikasi Missing Value dan Outlier
- Fitur High  
![high_fitur](https://github.com/hamzafrd/Machine-Learning-terapan/raw/main/images/high.png)
- Fitur marketplace  
![market_place](https://github.com/hamzafrd/Machine-Learning-terapan/blob/main/images/marketplace.png?raw=true)
- Fitur  volume  
![market_place](https://github.com/hamzafrd/Machine-Learning-terapan/blob/main/images/volume.png?raw=true)  

Terlihat jika di atas banyak terdapat outlier pada setiap variabel, lalu untuk mengatasinya nantinya penulis akan menerapkan batas bawah dan batas atas menggunakan metode IQR

Setelah beberapa kali melakukan IQR, berikut hasilnya :
- Fitur MarketPlace  
![high_fitur](https://github.com/hamzafrd/Machine-Learning-terapan/raw/main/images/aftermarket.png)
- Fitur High  
![high_fitur](https://github.com/hamzafrd/Machine-Learning-terapan/raw/main/images/afterhigh.png)
- Fitur  Close  
![high_fitur](https://github.com/hamzafrd/Machine-Learning-terapan/raw/main/images/afterclose.png)

 ### Univariate Analysis
![univariate](https://github.com/hamzafrd/Machine-Learning-terapan/raw/main/images/univariate.png)
Terlihat pada grafik bahwa semua data cenderung distribusi nilainya membentuk seperti camel (naik dan turun). Walaupun ada yang berbeda, yaitu pada Volume yang naik pada bagian kiri (left-skewed).
    
### Multivariate Analysis

---

![multivariate](https://github.com/hamzafrd/Machine-Learning-terapan/raw/main/images/multipredi.png)
Terlihat bahwa numerical features memiliki korelasi yang tinggi, kecuali pada fitur volume yang menunjukkan pesebaran data yang tidak menentu.
#### Mengevaluasi Skor Korelasi dengan fungsi curr()
![multivariate](https://github.com/hamzafrd/Machine-Learning-terapan/raw/main/images/korelasi.png)  
    Terlihat pada matriks korelasi di atas dapat disimpulkan bahwa hampir semua variabel memiliki keterikatan dan korelasi yang kuat antarvariabel lainnya, di mana nilai korelasi antarvariabel bernilai lebih dari 0.9 atau mendekati 1.

 Volume memiliki korelasi yang sangat lemah dengan yang lain, artinya jumlah transaksi (volume) tidak ada hubungannya dengan fitur lain dan bisa di drop. 

#### Melakukan drop terhadap fitur tidak signifikan
 Di sini penulisan melakukan drop pada 'Volume','Name', 'Symbol', 'Date' karena akan meganggu proses pembuatan model.



## Data Preparation

---

Berikut ini merupakan tahapan-tahapan dalam melakukan prapemrosesan data:

### **Melakukan pembagian dataset**
 Dataset akan dibagai menjadi dua, yaitu sebagai *train* data dan *test* . Train data digunakan untuk *training* model dan *test* data digunakan sebagai validasi model. Proposi yang saya gunakan di sini adalah 80 berbanding 20, 80% sebagai *train* data dan 20% sebagai *test* data.

### **Normalisasi data**
Normalisasi membantu untuk membuat semua fitur numerik berada dalam skala data yang kecil (0 - 1) dan membuat fitur data menjadi bentuk yang lebih mudah diolah oleh algoritma. Pada dataset ini saya menggunakan **MinMaxScaler** untuk melakukan normalisasi pada kategori numerik.



## Modeling

---

Pada proyek ini, Proses modeling dalam proyek ini menggunakan empat model, yaitu *Support Vector Regression, Gradient Boosting, Random Forest* dan  *K-Nearest Neighbors*. Kemudian, membandingkan performanya.

### Implementasi Grid Search

Grid Search adalah teknik modeling dengan cara mencari memasukkan berbagai macam parameter untuk menghasillkan model yang terbaik.

####  **K-Nearest Neighbor**  

 *K-Nearest Neighbors* merupakan algoritma machine learning yang bekerja dengan mengklasifikasikan data baru menggunakan kemiripan antara data baru dengan sejumlah data (k). Pada proyek kali ini ada 1 hyper parameter yang digunakan, yaitu :

- `n_neighbors`  yang merupakan Jumlah tetangga untuk yang diperlukan untuk menentukan letak data baru. Pada laporan kali ini penulis menggunakan `n_neighbors`  sebanyak 3 berdasarkan hasil grid search terbaik.

  - Kelebihan:
    - Algoritma KNN merupakan algoritma yang sederhana dan mudah untuk diimplementasikan.
    - Dapat di implementasikan pada beberapa kasus seperti klasifikasi, regresi dan pencarian.


  - Kekurangan:

    - Algoritma KNN menjadi lebih lambat secara signifikan seiring meningkatnya jumlah sampel dan/atau variabel independen.

      

#### **Random Forest**  

 Algoritma ini disusun dari banyak algoritma pohon (decision tree) yang pembagian data dan fiturnya dipilih secara acak. Untuk Parameter yang digunakan pada proyek kali ini ada empat hyper paramater, yaitu : 

- `n_estimator` yang merupakan jumlah *trees* (pohon) di *forest*. Pada proyek ini penulis melakukan *set* nilai `n_estimator` sebesar 70 *trees*. 

- `max_depth` yang merupakan kedalaman atau panjang pohon. Itu merupakan ukuran seberapa banyak pohon dapat membelah (*splitting*). Pada proyek ini penulis melakukan set nilai `max_depth` sebesar 16 *split*. 

- `random_state` digunakan untuk mengontrol *random number generator* yang digunakan. Di proyek ini penulis melakukan *set* nilai pada parameter `random_state` sebesar 55.

-  `n_jobs` yaitu jumlah *job* (pekerjaan) yang digunakan secara paralel. Itu merupakan komponen untuk mengontrol *thread* atau proses yang berjalan secara paralel. `n_jobs = -1` artinya semua proses berjalan secara paralel. Kemudian proses selanjutnya melakukan prediksi menggunakan data uji dan melakukan pengujian.

  -   Kelebihan :
      -   Algoritma Random Forest merupakan algoritma dengan pembelajaran paling akurat yang tersedia. Untuk banyak kumpulan data, algoritma ini menghasilkan pengklasifikasi yang sangat akurat.
      -   Berjalan secara efisien pada data besar.
      -   Dapat menangani ribuan variabel input tanpa penghapusan variabel.
      -   Memberikan perkiraan variabel apa yang penting dalam klasifikasi.
      -   Memiliki metode yang efektif untuk memperkirakan data yang hilang dan menjaga akurasi ketika sebagian besar data hilang.

  -   Kekurangan :
      - Algoritma Random Forest overfiting untuk beberapa kumpulan data dengan tugas klasifikasi/regresi yang _bising/noise_.
      
      - Untuk data yang menyertakan variabel kategorik dengan jumlah level yang berbeda, Random Forest menjadi bias dalam mendukung atribut dengan level yang lebih banyak. Oleh karena itu, skor kepentingan variabel dari Random Forest tidak dapat diandalkan untuk jenis data ini.
      
        

#### **Support Vector Regression**

*Support Vector Regression* memiliki prinsip yang sama dengan SVM, namun SVM biasa digunakan dalam klasifikasi. Pada SVM, algoritma tersebut berusaha mencari jalan terbesar yang bisa memisahkan sampel dari kelas berbeda, sedangkan SVR mencari jalan yang dapat menampung sebanyak mungkin sampel di jalan. Untuk hyper parameter yang digunakan pada model ini adalah sebagai berikut :

- `C` : Hyperparameter ini adalah parameter regularisasi digunakan untuk menukar klasifikasi yang benar dari contoh *training* terhadap maksimalisasi margin fungsi keputusan. Pada proyek kali ini penulis menggunakan *`C`* sebanyak 10000.

- `gamma` :Hyperparameter ini digunakan untk menetukan seberapa jauh pengaruh satu contoh pelatihan mencapai, dengan nilai rendah berarti jauh dan nilai tinggi berarti dekat. Pada proyek ini penulis menggunakan *`gamma`* sebanyak 0,3.

- `kernel` : menentukan kernel untuk matriks . Pada proyek ini digunakan *`kernel`* RBF karena data merupakan data linear.

  - Kelebihan :

    - Lebih efektif pada data dimensi tinggi (data dengan jumlah fitur yang banyak)

    - Memori lebih efisien karena menggunakan subset poin pelatihan

  - Kekurangan :

    - Tidak cocok untuk data berukuran besar

      

#### **Gradient boosting Algorithm**

 Gradient Boosting adalah algoritma machine learning yang menggunakan teknik *ensembel learning* dari *decision tree* untuk memprediksi nilai. Gradient Boosting sangat mampu menangani pattern yang kompleks dan data ketika linear model tidak dapat menangani. Untuk hyperparameter yang digunakan pada model ini ada tiga, yaitu :

- `learning_rate` : Hyperparameter training yang digunakan untuk menghitung nilai koreksi bobot padad waktu proses training. Umumnya nilai learning rate berkisar antara 0 hingga 1. Pada proyek ini penulis menggunakan `learning_rate` sebesar 0,01.
- `n_estimators` : Jumlah tahapan boosting yang akan dilakukan. Pada proyek ini penulis menggunakan `n_estimators` sebesar 1000.
- `criterion` : Hyperparameter yang digunakan untuk menemukan fitur dan ambang batas optimal dalam membagi data. Pada proyek ini penulis menggunakan `criterion` squared error.
  - Kelebihan :
    - Algoritma Boosting dapat mengurangi bias pada data.
    - Hasil pemodelan yang lebih akurat.
    - Algoritma ini sangat powerful dalam meningkatkan akurasi prediksi.
  - Kekurangan :
    - Waktu komputasi dan desain tinggi.
    - Tingkat kesulitan yang tinggi dalam pemilihan model

## Evaluation   
### MSE

Untuk evaluasi, metrik yang digunakan adalah *mean squared error (mse)*. Di mana metrik ini mengukur seberapa dekat garis pas dengan titik data. 
![mse](https://github.com/hamzafrd/Machine-Learning-terapan/raw/main/images/mse.png)
 Keterangan:

- N = jumlah titik data atau banyaknya data pada sebuah dataset/tabel. 

- yi = nilai sebenarnya

- yi^ = nilai prediksi

  

Berikut ini perbandingan grafik metrik MSE pada keempat model:

![plot](https://github.com/hamzafrd/Machine-Learning-terapan/raw/main/images/plottingfinal.png)

Untuk proyek kali ini model SVM merupakan model yang berjalan dengan performa paling optimal sehingga dapat disimpulkan bahwa model dapat memprediksi harga dari pasar dogecoin dari data test dengan baik. Sehingga kedepannya dapat membantu para trader dalam melakukan keputusan pembelian/penjualan pasar.

## Referensi

- Rifan, Aditya. (2021). *Apa Itu Dogecoin ?* . Suara. Retrieved September 15, 2022, from https://www.suara.com/tekno/2021/01/04/110653/apa-itu-dogecoin-simak-fungsi-dan-cara-mendapatkannya-berikut?page=2
- Rizq Widyadana, Pradiska. (2022). *Pengertian, Fungsi, hingga Cara untuk Mendapatkan dogecoin*. Pikiran Rakyat. Retrieved September 15, 2022, from https://beritadiy.pikiran-rakyat.com/author/3472/pradiska-rizq-widyadana
- Chauhan, Ankit .(2021). *Random Forest Classifier and its Hyperparameters*. Medium. Retrieved September 15, 2022, from https://medium.com/analytics-vidhya/random-forest-classifier-and-its-hyperparameters-8467bec755f6
- Aliyev, V. (2020, October 7). *Gradient boosting classification explained through python*. Medium. Retrieved September 15, 2022, from https://towardsdatascience.com/gradient-boosting-classification-explained-through-python-60cc980eeb3d
- Khoiri. (2020). *Cara Menghitung Mean Squared Error (MSE)*. Khoiri. Retrieved September 16, 2022, from https://www.khoiri.com/2020/12/pengertian-dan-cara-menghitung-mean-squared-error-mse.html
