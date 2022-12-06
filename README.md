# Sistem Rekomendasi Buku Berdasarkan Penilaian
---
## Domain Proyek
---
### Latar Belakang
  Sistem rekomendasi buku merupakan sebuah sistem yang berfungsi untuk merekomendasikan kepada pembaca khususnya para penggemar buku. Sistem rekomendasi pada umumnya ditujukan untuk individu yang kekurangan pengalaman atau kompetensi yang cukup untuk mengevaluasi banyaknya jumlah alternatif item yang ada pada suatu kasus tertentu. Saat ini pemanfaatan sistem rekomendasi sudah diterapkan disetiap sudut aspek kehidupan seperti pada e-commerce : Bukalapak.com, amazon.com dan Google Play Store yang memanfaatkan metode Collabrativefiltering dan berjalan dengan baik, akan tetapi metode tersebut belum terpakai pada sebuah buku bacaan.
 
 Membaca merupakan kegiatan menerima akan tetapi, untuk mendapatkan pemahaman yang baik dan menyeluruh, kita tidak melakukannya dengan berpasrah diri. Untuk memperoleh itu, kita secara aktif bekerja mengolah teks bacaan menjadi bahan yang bermakna. Ghazali (2010: 208) mengemukakan bahwa membaca adalah proses pemecahan sandi terhadap simbol-simbol tertulis, karena di awali dengan memahami segmen-segmen terkecil (huruf, suku kata, kata) dalam teks dan kemudian dibangun agar mencakup unit-unit yang lebih besar. Membaca dapat juga diartikan sebagai berpikir secara abstrak, yaitu membayangkan suatu benda atau kejadian tanpa melihat atau mengalaminya sendiri tetapi hanya melalui bacaan.
 
 Kurangnya minat untuk membaca dikalangan masyarakat menjadi sebuah persoalan yang sangat kronis. hal tersebut pastinya dipengaruhi oleh beberapa faktor terkait, seperti susahnya pencarian dari buku yang dingginkan, dan review sebuah buku yang kurang maksimal, Oleh sebab itu, perlu dibuatkannya sistem rekomendasi yang berguna untuk membantu para pembaca untuk memilih dan juga melihat rating penilaian dari buku dengan mudah, maka dari itu harpannya dapat mendongkrak dan dapat lebih meningkatkan minat baca dari masyarakat.
  
## Business Understanding
---
### Problem Statement
Mengacuu pada latar belakang yang sudah disebutkan, dapat dirumuskan bagaimana cara agar dapat merekomendasikan buku sesuai dengan baik dan relevan kepada pembaca buku

### Goals 
Menciptakan sistem rekomendasi yang akurat berdasarkan penilaian dan aktivitas pengguna yang lampau

### Solution Approch
Solusi yang dapat mendukung agar proyek ini dapat berjalan dengan lancar dan sesuai dengan tujuan yaitu dengan melakukan implementasi algoritma Content Based Filtering implementasi algortima Collaborative Filltering. Masing - masing algoritma memiliki kegunaan yang berbeda sesuai dengan fungsinya tersendiri.

### Data Understanding
Dataset yang digunakan pada proyek ini mengambil dari site Kaggle dengan URL https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset

Pada Dataset tersebut, terdapat 3 file data yang tersedia :
* Books.csv
* Ratings.csv
* Users.csv

Proyek ini akan mengacu pada 2 data file yang penting untuk digunakan.
* Books.csv
  Terdiri atas variable :
  * ISBN : Kode unik dari identitas sebuah buku
  * Book-Title : Judul dari buku
  * Book-Author : Penulis atau Pengarang buku
  * Year-of-Publication : Tahun diterbitkannya buku
  * Publisher : Penerbit Buku
  * Image-URL-S : Tautan Link sampul buku (kecil)
  * Image-URL-M : Tautan link sampul buku (Sedang)
  * Image-URL-L : Tautan link sampul buku (Besar)
  Dan tercatat memiliki 271360 sample dan 8 kolom. Data ini juga memiliki total 6 nilai yang kosong.
  
  Tabel 
  
| #  | Column              | Non-Null Count  | Dtype  |
|----|---------------------|-----------------|--------|
| 1  | ISBN                | 271360 non-null | object |
| 2  | Book-Title          | 271360 non-null | object |
| 3  | Book-Author         | 271359 non-null | object |
| 4  | Year-Of-Publication | 271360 non-null | object |
| 5  | Publisher           | 271358 non-null | object |
| 6  | Image-URL-S         | 271360 non-null | object |
| 7  | Image-URL-M         | 271360 non-null | object |
| `8 | Image-URL-L         | 271357 non-null | object |

* Ratings.csv
  Terdiri atas variable :
  * User-ID : Nomor identitas pengguna
  * ISBN : Kode unik dari identitas sebuah buku
  * Book-Rating : Skor penilaian dari masing - masing buku
  Tercatat memiliki 1149780 sample dan 3 kolom. Sementara data ini tercatat tidak memiliki nilai yang kosong.
 
 Tabel 
 | # | Column      | Non-Null Count   | Dtype  |
|---|-------------|------------------|--------|
| 1 | User-ID     | 1149780 non-null | int64  |
| 2 | ISBN        | 1149780 non-null | object |
| 3 | Book-Rating | 1149780 non-null | int64  |

### Exploratory Data Analysis
Sebelumsampai ke tahap pelatihan, diperlukan eksplorasi data yang akan digunakan lebih mendalam.
* Checking Missing Values pada masing masing data

 * Books.csv
 
 | # | Column              | Total |
|---|---------------------|-------|
| 1 | ISBN                | 0     |
| 2 | Book-Title          | 0     |
| 3 | Book-Author         | 1     |
|  4 | Year-Of-Publication | 0     |
|  5| Publisher           | 2     |
|  6 | Image-URL-S         | 0     |
|  7 | Image-URL-M         | 0     |
|  8 | Image-URL-L         | 3     |

 * Ratings.csv
 
 | # | Column      | Total |
|---|-------------|-------|
| 1 | User-ID     | 0     |
| 2 | ISBN        | 0     |
| 3 | Book-Rating | 0     |

* Checking Data Duplicate pada masing - masing data 
 * Books.csv
 
 | # | Column              | Total  |
|---|---------------------|--------|
| 1 | ISBN                | 0      |
| 2 | Book-Title          | 29225  |
| 3 | Book-Author         | 169336 |
| 4  | Year-Of-Publication | 271158 |
|  5 | Publisher           | 254552 |
|   6| Image-URL-S         | 316    |
|  7 | Image-URL-M         | 316    |
|  8 | Image-URL-L         | 318    |

* Ratings.csv

| # | Column      | Total   |
|---|-------------|---------|
| 1 | User-ID     | 1044497 |
| 2 | ISBN        | 809224  |
| 3 | Book-Rating | 1149769 |

Dari tabel Book.csv  8 kolom yang tersedia, Kolom ISBN sendiri yang tidak memiliki duplikasi data. Berbeda dengan kolom yang lain yang memiliki duplikasi yang berbeda - beda. berbeda dengan dat Rating yang semua kolom memiliki duplikasi data yang nilainya cukup besar dan berbeda - beda. hal ini menjadi wajar pada data ratings.csv karena banyaknya volume seorang dalam memberikan nilai kepada buku yang berbeda.

## Data Preparation
Langkah selanjutnya yaitu mempersiapkan data agar ketika dilakukan proses pengembangan model atau sistem dapat menghasilkan rekomendasi dengan baik. Untuk mempersiapkannya maka diperlukan.
* Menghilangkan data yang tidak digunakan
Untuk melakukan dan menjalankan permodelan dengan baik. sistem ini hanya perlu menggunakan data *author* dan *rating*. Karena implementasi ini kita menggunakan teknik *Content-based Filtering* dan teknik *Collaborative Filtering*, maka kita kan menghapus kolom *Year-of-Publication, Publisher, Image-URL-M, Image-URL-L, Book-Author, dan Num-Rating*.

* Merge Data
Karena disini menggunakan 2 data yang beda, maka kita perlu menjadikan satu data yang sudah ada agar dapat memudahkan dalam pembuatan model pelatihan nanti.

* Menghapus Duplikasi Data
Penghapusan duplikasi data yang dilakukan pada proyek ini yaitu penghapusan data yang memiliki judul buku yang sama tetapi memiliki ISBN yang berbeda. Sehingga 1 judul buku hanya akan memiliki 1 ISBN yang mana akan mempermudah dalam proses mendapatkan rekomendasi.

* Mengatur Missing Values pada Data
Untuk mengatasi nilai kosong pada data yang sudah diketahui sebelumnya, dengan mudah cukup mengahpus baris yang tidak memiliki nilai. Dengan begitu, data yang memiliki nilai kosong akan hilang, sehingga akan menghasilkan permodelan machine learning yang lebih baik untuk nantinya.

* Seleksi Data
Pada proses seleksi data dengan menggunakan teknik *Content-Based Filtering* disini akan diambil data buku dengan minimal penilaian diatas skor 60. Ini berarti sistem akan merkomendasikan buku dengan kriteria diatas nilai 60.

* Normalisasi Data
Melakukan transformasi pada data fitur fitur yang akan dipelajari oleh model menggunakan library MinMaxScaler. MinMaxScaler mentransformasikan fitur dengan menskalakan setiap fitur ke rentang tertentu. Library ini menskalakan dan mentransformasikan setiap fitur secara individual sehingga berada dalam rentang yang diberikan pada set pelatihan, pada library ini memiliki range default antara 0 dan 1.

* Split Dataset
Split Dataset Membagi dataset menjadi 2 bagian, sebagai test data dan train data. Untuk pembagiannya masing - masing memiliki porsi senilai 80% untuk train data dan 20% sebagai test data

## Modeling dan Result
teknik yang digunakan pada proyek ini menggunkana teknik *Content-Based Filtering dan Collaborative Filtering*

### *Content Based Filtering*
Metode ini melakukan feature engineering dengan mengandalkan library *TfidVectorizer* dari library scikit-learn. Metode ini memiliki tujuan untuk memprediksi persamaan sejumlah informasi yang didapat dari pengguna. Dalam pengaplikasiannya, *content based filtering* menggunakan konsep perhitungan TF-IDF dan Cosine Similarity yang bermaksud mengkonversikan data/teks menjadi berbentuk vector.

![image](https://user-images.githubusercontent.com/75149615/205967282-56ea5375-598d-4a82-a6f0-78587d41ed7d.png)

Tak lain dari itu, teknik ini memiliki beberapa Kelebihan dan Kekurangan, diantaranya.

* Kelebihan
  * Semakin banyak data yang didapat, akurasi akan semakin baik

* Kekurangan
  * Hanya dapat diimplementasikan pada hal yang bersifat sangat spesifik, seperti berita, buku, dan dokumen yang lain,
  
Judul buku yang akan dijdadikan sebagai acuan pencarian rekomendasi buku.

| Book-Title    |  Book-Author | Image-URL-S                                       |
|---------------|-------------:|---------------------------------------------------|
| The Testament | John Grisham | http://images.amazon.com/images/P/0440234743.0... |

Sehingga menghasilkan 6 rekomendasi buku dengan author yang sama sesuai dengan acuan dari buku yang kita cari

|   | Book-Title         |  Book-Author | Image-URL-S                                       |
|---|--------------------|-------------:|---------------------------------------------------|
| 0 | Bleachers          | John Grisham | http://images.amazon.com/images/P/0385511612.0... |
| 1 | The Partner        | John Grisham | http://images.amazon.com/images/P/0385472951.0... |
| 2 | The Client         | John Grisham | http://images.amazon.com/images/P/038542471X.0... |
| 3 | The Street Lawyer  | John Grisham | http://images.amazon.com/images/P/0440225701.0... |
| 4 | The Last Juror     | John Grisham | http://images.amazon.com/images/P/0385510438.0... |
| 5 | Skipping Christmas | John Grisham | http://images.amazon.com/images/P/0385505833.0... |
| 6 |  The King of Torts | John Grisham | http://images.amazon.com/images/P/0385508042.0... |

### Collaborative Filtering
Pada teknik ini proses pembuatan rekomendasi menggunakan model Deep Learning. Langkah yang pertama yaitu dengan menggabungkan data buku dan rating. Setelah itu melakukan penyandian terhadap data User-ID dan ISBN dan memisahkan data latih dan data validasi dengan ratio 80:20. Membuat model untuk dilakukannya pelatihan pada data. Model ini menggunakan operasi perkalian dot product antara embedding *user* dan *book*. Skor kecocokan ditetapkan dalam skala [0,1] dengan fungsi aktivasi sigmoid. Untuk mendapatkan hasil rekomendasi, dipilih User-ID secara acak dan akan dilakukan penyaringan daftar buku yang belum pernah dibaca oleh user.
Setelah model dibuat dan dilatih, berikut adalah hasil rekomendasi dari model ini.

|              Book With high Ratings from User             |                                 Les Fleurs Du Mal                                 |
|:---------------------------------------------------------:|:---------------------------------------------------------------------------------:|
|                         The Client                        |                               Elements of Style 3ED                               |
|                      Of Mice and Men                      |             Fox in Socks (I Can Read it All by Myself Beginner Books)             |
| Dont Roll Your Eyes at Me, Young Man! A Zits SketchBook 3 | The Baby Book: Everything You Need To Know Abaout Your Baby from Birth to Age Two |
|                                                           |                                    Harry Potter                                   |
|                                                           |                               A Kiss for Little Bear                              |
|                                                           |                                     The Lorax                                     |
|                                                           |                The Blue Day Book : A Lesson in Cheering Yourself Up               |
|                                                           |                            Le Combat ordinaire, tome 1                            |
|                                                           |                 The Art of Shen Ku : The Ultimate Traveleres Guide                |

# Evaluation
---
Evaluasi yang digunakan pada proyek ini yaitu menggunakan 2 teknik evaluasi.
1. Evaluasi Precision untuk *Content-Based Filltering
2. Teknik evaluasi RMSE (Root Mean Squared Error) untuk Collaborative Filtering.

### Evaluasi Content Based Filtering
Evaluasi pada teknik ini menggunakan metrik precision content untuk menghitung tingkat presisi sistem dari rekomendasi yang dibuat.

![image](https://user-images.githubusercontent.com/75149615/205974701-8b66404b-8a36-40d3-ba5d-793ca30ee5e0.png)

Sebagai Contoh kita mencari buku dengan pengaran *John Grishm*:
| Book-Title    |  Book-Author | Image-URL-S                                       |
|---------------|-------------:|---------------------------------------------------|
| The Testament | John Grisham | http://images.amazon.com/images/P/0440234743.0... |

Hasil :
|   | Book-Title         |  Book-Author | Image-URL-S                                       |
|---|--------------------|-------------:|---------------------------------------------------|
| 0 | Bleachers          | John Grisham | http://images.amazon.com/images/P/0385511612.0... |
| 1 | The Partner        | John Grisham | http://images.amazon.com/images/P/0385472951.0... |
| 2 | The Client         | John Grisham | http://images.amazon.com/images/P/038542471X.0... |
| 3 | The Street Lawyer  | John Grisham | http://images.amazon.com/images/P/0440225701.0... |
| 4 | The Last Juror     | John Grisham | http://images.amazon.com/images/P/0385510438.0... |
| 5 | Skipping Christmas | John Grisham | http://images.amazon.com/images/P/0385505833.0... |
| 6 |  The King of Torts | John Grisham | http://images.amazon.com/images/P/0385508042.0... |

dari hasil yang ditampilkan, tingkat presisi pada sistem yaitu 6/6 atau dapat dikatakan sempurna. Karena data yang ditampilkan keseluruhan semuanya melampirkan pengarang yang bersumber dari *John Grisham*

### Evaluasi Collaborative Filtering
Pada model ini menggunakan metrik evaluasi RMSE. RMSE adalah metode pengukuran dengan mengukur perbedaan nilai dari prediksi sebuah model sebagai estimasi atas nilai yang diobservasi. Metode estimasi yang mempunyai Root Mean Square Error (RMSE) lebih kecil dikatakan lebih akurat daripada metode estimasi yang mempunyai Root Mean Square Error (RMSE) lebih besar.

![image](https://user-images.githubusercontent.com/75149615/205975930-0a1b2b9e-63ac-413b-aae5-204a1c6add61.png)

![image](https://user-images.githubusercontent.com/75149615/205976224-9beedecb-99df-4dce-b35c-f4f78f3141a3.png)

Dari hasil pelatihan yang dilakukan. Dapat dilihat bahwa nilai konvergen metrik RMSE berada di sekitar 0.30 untuk training dan disekitar 0.34 untuk validasi.

### Preferences
---
* Miraldi, R. N., Christanto, A. R., & Susanto, B. (2015). IMPLEMENTASI ALGORITMA FP-GROWTH UNTUK SISTEM REKOMENDASI BUKU DI PERPUSTAKAAN UKDW. Jurnal Informatika, 10(1).
* Herdi Hafi, 2013. Sekilas Tentang Sistem Rekomendasi (Recommender System).
* Masruri, Farid, 2007. Personalisasi Web E- Commerce Menggunakan RecommenderSystem dengan Metode Item-BasedCollaborative Filtering
