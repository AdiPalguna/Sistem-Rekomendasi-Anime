# Laporan Proyek Machine Learning – I Wayan Gede Adi Palguna

## Project Overview 
Anime adalah animasi khas Jepang yang digambarkan oleh tangan maupun teknologi komputer. Biasanya, anime dicirikan dengan sebuah gambar-gambar berwarna-warni dan menampilkan tokoh-tokoh di dalam berbagai cerita dan juga lokasi yang ditampilkan kepada berbagai jenis penonton. Saat pertama kali masuk ke Indonesia, anime hanya dapat dinikmati dalam bahasa Indonesia, karena seluruh anime yang ditayangkan di televisi nasional dialihbahasakan ke dalam bahasa Indonesia. Bahkan lagu pembuka dan penutup anime pun dialihbahasakan. Namun, setelah hadirnya internet, penggemar anime menjadi lebih mudah untuk mengakses produk-produk tersebut dalam versi bahasa Jepang.

Salah satu kesulitan yang sering dialami penggemar anime, terutama penonton baru, adalah mencari judul anime yang sesuai dengan genre yang diinginkan. Hal ini dikarenakan banyak anime yang dirilis dalam setiap musimnys. Semakin menyusahkan bagi penggemar anime untuk mencari judul anime yang sesuai dengan anime yang pernah ditonton sebelumnya. Oleh karena itu, seringkali anime yang ingin ditonton menjadi kurang sesuai dengan minat sehingga membuat pengalaman menonton anime menjadi kurang menarik.

Oleh karena itu, perlu adanya sistem rekomendasi anime yang dapat menyelesaikan permasalahan tersebut sehingga dengan adanya sistem rekomendasi tersebut diharapkan dapat mempermudah user untuk mengetahui rekomendasi anime berdasarkan judul anime yang disukai beserta dengan genre dari anime tersebut.

## Business Understanding
Setiap orang tentunya memiliki selera yang berbeda-beda, tidak terkecuali dalam memilih anime berdasarkan hal-hal tertentu genre seperti action, comedy, fantasy, dan lain sebagainya. Selain itu orang-orang juga perlu memperhatikan beberapa anime yang memang tidak diperuntukkan untuk anak-anak dibawah umur. Oleh karena itu, saya membuat sistem rekomendasi anime untuk memberikan rekomendasi anime kepada user dengan memperhatikan beberapa variable.

### Problem Statements
Permasalahan dari proyek tersebut adalah karena banyaknya jenis atau genre anime yang ada sehingga user menjadi bingung untuk memilih anime yang ingin ditonton. Oleh karena itu, perlu adanya sistem rekomendasi dimana sistem tersebut bisa memberi anime yang tepat untuk user.

### Goals
Untuk menjawab pertanyaan tersebut, saya akan membuat model sistem rekomendasi dengan tujuan atau *goals* sebagai berikut.
- Memberikan rekomendasi kepada user berdasarkan genre anime tersebut sebagai dasar pemberian rekomendasi judul anime.

### Solution Approach
Untuk solusi permasalahan tersebut saya menggunakan algoritma sistem rekomendasi, yaitu *Content Based Filtering*. *Content Based Filtering* atau berbasis konten merupakan sistem rekomendasi yang memberikan rekomendasi berdasarkan kemiripan atribut dari item atau barang yang disukai. Contohnya, pada sistem rekomendasi anime kemiripan berdasarkan genre, rating, dan lain sebagainya. Adapun kelebihan dari *Content Based Filtering* yaitu.  
- Memiliki kemampuan untuk merekomendasikan item baru bagi user  
- Merekomendasikan item secara cepat sehingga user tidak perlu menunggu.  

Adapun kekurangan dari *Content Based Filtering* yaitu.  
- Sulit untuk menghasilkan rekomendasi yang tidak terduga
- Kurang handal karena hanya merekomendasikan berdasarkan konten.  

Untuk model yang saya gunakan untuk mendukung *Content Based Filtering* adalah *cosine similarity*.
- *Cosine similarity* merupakan model yang menghitung *similarity* atau kesamaan antar item sehingga bisa dinyatakan bahwa item satu dengan lainnya mirip atau serupa. Adapun formula untuk menghitung *cosine similarity* yaitu.  

![consine similarity formula](https://user-images.githubusercontent.com/72697144/139908696-e5b3b506-f60e-4d33-a74b-cb152122711f.png)

## Data Understanding
Data yang saya gunakan pada proyek ini adalah Anime Recommendation Database 2020 yang diunduh dari [kaggle](https://www.kaggle.com/hernan4444/anime-recommendation-database-2020) yang berisikan data sebanyak 17562 dengan 35 jenis variable. Beberapa diantaranya yaitu.
- *MAL_ID*: *unique* ID yang mendefinisikan suatu anime
- *Name*: Judul dari suatu anime
- *Score*: Rata-rata penilaian dari suatu anime
- *Genres*: Genre dari suatu anime
- *English Name*: Judul anime dalam bahasa inggris
- *Japanese Name*: Judul anime dalam bahasa jepang
- *Type*: Tipe dari suatu anime (TV, *Movie*, dan lain-lain)
- *Episodes*: Jumlah episode dari suatu anime
- *Aired*: Rentang waktu penayangan dari suatu anime
- *Premiered*: Penayangan perdana dari suatu anime.  

Selanjutnya dilakukan visualisasi data pada variable *Genres* pada dataset tersebut menggunakan beberapa library seperti *matplotlib.pyplot* dan *seaborn*. Hasil dari visualisasi data berdasarkan variable *Genres* anime adalah sebagai berikut.  
![visualisasi data](https://user-images.githubusercontent.com/72697144/140025986-42662177-8de0-4f67-bb3a-af68844ad9a2.PNG)

## Data Preparation
Pada tahapan Data Preparation saya menerapkan beberapa teknik yaitu. 
- *Drop* Variable  
Untuk menghapus variable yang sekiranya tidak digunakan dapat menggunakan method *drop()*. Salah satu tujuan dari menghapus atau *drop* variable yang tidak digunakan adalah untuk mempermudah pengguna untuk melihat hasil dari rekomendasi yang diberikan nantinya. Berikut merupakan hasil dari *drop* variable.  
![drop variable](https://user-images.githubusercontent.com/72697144/140515112-6b23d7d1-8f41-4b8b-ae96-04a2d8cfad9b.PNG)

- *Drop* Data Duplikat  
Untuk menghapus atau *drop* data duplikat dapat menggunakan method dari library *pandas* yaitu *drop_duplicates()*. Sama halnya dengan *Missing Value*, data duplikat juga dapat mempengaruhi akurasi dari model sistem rekomendasi. Berikut merupakan hasil dari *drop* data duplikat.  
![drop duplikat](https://user-images.githubusercontent.com/72697144/140515339-605f9d5f-7eeb-46e2-bb1f-6d54e2302232.PNG)

- One-Hot Encoding  
Proses ini nantinya akan digunakan untuk *cosine similarity*. Saya melakukan One-Hot Encoding pada variable *Genres* karena setiap anime memiliki genre yang bervariasi. Saya membuat kolom baru untuk setiap nilai genre yang terdapat dalam variable *Genres*.

## Modeling
Pada tahapan modeling saya menggunakan *cosine similarity* untuk sistem rekomendasi berbasis *Content Based Filtering*.
- Cosine Similarity  
*Cosine similarity* merupakan model yang menghitung *similarity* atau kesamaan antar item sehingga bisa dinyatakan bahwa item satu dengan lainnya mirip atau serupa. Hasil dari model ini adalah rekomendasi 10 anime berdasarkan genre. Berikut adalah hasil dari *cosine similarity*.  

![hasil cosine similarity](https://user-images.githubusercontent.com/72697144/139909939-5deca09d-bc0c-4754-96cf-0dceaf374a87.PNG)  

Dapat dilihat bahwa rekomendasi anime yang diberikan bervariasi serta sesuai dengan genre. Hal ini membuktikan bahwa model rekomendasi yang dibuat sudah baik.

## Evaluation
Pada tahapan evaluasi (Evaluation) dilakukan proses mengevaluasi performa dari model sebelumnya menggunakan *Metrik Precission*.
- Metrik Precision  
*Metrik Precission* menghitung total prediksi rekomendasi berdasarkan genre yang benar dibagi dengan total rekomendasi yang telah diberikan. Saya menggunakan metrik ini karena saya ingin mengetahui apakah model yang dipakai untuk Content Based Filtering dapat memprediksi semua konten bedasarkan genre dengan benar. Selain itu, metrik ini juga digunakan untuk mengevaluasi *cosine similarity*. Dari evaluasi ini, didapatkan hasil bahwa *cosine similarity* berfungsi dengan baik untuk memberikan rekomendasi anime karena hasil dari pengambilan sample secara acak menghasilkan akurasi 100%.
