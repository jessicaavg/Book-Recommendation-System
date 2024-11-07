# Laporan Proyek Machine Learning - Jessica Vega Nainggolan

## Project Overview

Di era digital yang serba cepat, jumlah buku yang diterbitkan terus melonjak. Hal ini membuat pembaca semakin sulit menemukan bacaan yang sesuai dengan minat dan preferensi mereka di tengah lautan pilihan. Padahal, setiap pembaca memiliki selera yang unik, mulai dari genre favorit hingga gaya penulisan yang disukai.

**Sistem rekomendasi buku** berbasis machine learning dapat menjadi solusi dalam menjawab tantangan ini. Melalui teknologi ini, algoritma machine learning mampu menganalisis berbagai fitur buku, seperti judul atau genre untuk memberikan rekomendasi yang akurat dan relevan. Tujuan utama proyek ini adalah mengembangkan sistem rekomendasi yang dapat memberikan saran buku yang relevan berdasarkan genre, sehingga pembaca dapat dengan mudah menemukan bacaan yang sesuai dengan minat mereka.

# Mengapa Proyek ini Penting Untuk Diselesaikan?

Sistem rekomendasi buku memiliki banyak manfaat, yaitu: 
- **Meningkatkan Pengalaman Pengguna**: Sistem rekomendasi yang akurat dapat membantu pengguna menemukan buku yang relevan, menarik, dan sesuai dengan preferensi pribadi pengguna, sehingga membuat pengalaman membaca lebih memuaskan dan personal.
- **Mempercepat Akses ke Konten yang Relevan**: Dengan sistem rekomendasi, pengguna dapat menemukan buku yang diinginkan dengan lebih mudah dan cepat tanpa harus mencari satu per satu.
- **Peningkatan Penjualan**: Dengan memberikan rekomendasi yang tepat, sistem ini dapat meningkatkan kemungkinan pengguna membeli buku, sehingga dapat meningkatkan pendapatan.
- **Peningkatan Keterlibatan Pengguna**: Rekomendasi yang relevan akan membuat pengguna lebih sering mengunjungi platform dan berinteraksi dengan konten, sehingga meningkatkan engagement.
- **Mengembangkan industri penerbitan**: Sistem ini dapat membantu penulis dan penerbit menemukan audiens yang tepat untuk karya mereka.

**Referensi**:

[1] Mobius. "Book Recommendation Dataset". Dataset publik dari platform Kaggle dan dapat diakses melalui (https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset)

[2] R. Afika *et al*.  "Machine Learning Journal Article Recommendation System Using Content Based Filtering". (http://juti.if.its.ac.id/index.php/juti/article/view/1193/507)

---

## Business Understanding

Bagian ini adalah penguraian proses pengidentifikasian permasalahan yang menjadi fokus utama proyek ini.

### Problem Statements
1. Bagaimana cara sistem dapat mengidentifikasi kesamaan antara buku berdasarkan judul dan genre untuk menghasilkan rekomendasi yang relevan?

2. Apa metode terbaik untuk mengukur kesamaan antara buku agar hasil rekomendasi lebih akurat?

3. Bagaimana cara meningkatkan tingkat kepuasan pengguna terhadap layanan yang diberikan oleh platform buku online?

### Goals
1. **Mengidentifikasi Kesamaan Buku Berdasarkan Judul dan Genre** agar sistem mampu memberikan rekomendasi buku yang memiliki konten atau tema yang mirip dengan buku yang pernah dipilih atau disukai pengguna.

2. **Memilih Metode Terbaik untuk Mengukur Kesamaan Buku** sehingga menghasilkan sistem yang mampu mengenali kemiripan antar buku dengan lebih baik dan menghasilkan rekomendasi yang relevan dan sesuai dengan preferensi pengguna.

3. **Memberikan rekomendasi buku yang relevan** agar pengguna merasa lebih terbantu dalam menemukan buku yang sesuai minatnya, serta meningkatkan kenyamanan dan keterlibatan pengguna terhadap platform buku online. 


### Solution Statements
1. Menggunakan pendekatan **Content-Based Filtering** dimana sistem akan merekomendasikan buku yang mirip dengan yang dicari atau disukai oleh pengguna di masa lalu. 

2. Mengimplementasikan metode **Cosine Similarity** untuk melakukan perhitungan terkait kesamaan antar judul buku.

3. Menggunakan model **Word2Vec** untuk mempelajari representasi vektor dari kata-kata dalam judul buku yang memungkinkan sistem rekomendasi untuk memahami hubungan semantik di antara kata-kata tersebut. Dengan cara ini, sistem dapat menangkap makna konteks dari judul, menghasilkan rata-rata vektor yang representatif, dan membandingkannya dengan genre yang telah ditentukan.

---

## Data Understanding
Dataset yang digunakan dalam proyek ini adalah **Book Recommendation Dataset** dari platform Kaggle [1] yang dipublish pada tahun 2024. Memiliki 3 data terpisah, yaitu data **"Books", "Ratings", dan "Users"**.

### Informasi Dataset
1) **Jumlah Data**: 
    - **Dataset Books** = 271.360 baris data dan 8 kolom.
    - **Dataset Ratings** = 1.149.780 baris data dan 3 kolom.
    - **Dataset Users** =  278.858 baris data dan 3 kolom.

2) **Missing Value**:
    - **Dataset Books** = Terdapat missing value pada kolom "Book-Author" (3), "Publisher" (2), dan "Image-URL-L" (2).
    - **Dataset Ratings** = Tidak ada missing value pada data.
    - **Dataset Users** =  Terdapat missing value pada kolom "Age" (110.762).

### Variabel-Variabel Pada Book Recommendation Dataset adalah sebagai berikut:
1. Data **"Books"**:
    - **ISBN**: Kode unik pengidentifikasian buku (tipe data`object`)
    - **Book-Title**: Judul buku (tipe data`object`)
    - **Book-Author**; Penulis buku (tipe data`object`)
    - **Year-Of-Publication**: Tahun publikasi buku (tipe data`object`)
    - **Publisher**: Pihak yang mempublikasi buku (tipe data`object`)
    - **Image-URL-S**: URL yang tertaut kepada gambar sampul, kecil (tipe data`object`)
    - **Image-URL-M**: URL yang tertaut kepada gambar sampul, sedang (tipe data`object`)
    - **Image-URL-L**. URL yang tertaut kepada gambar sampul, besar (tipe data`object`)

2. Data **"Ratings"**:
    - **User-ID**: ID pengguna (tipe data`int`)
    - **ISBN**: Kode unik pengidentifikasian buku (tipe data`object`)
    - **Book-Rating**: Rating buku yang diberikan oleh pengguna (tipe data`int`)

3. Data **"Users"**:
    - **User-ID**: ID pengguna (tipe data`int`)
    - **Location**: Lokasi pengguna (tipe data`object`)
    - **Age**: Umur pengguna (tipe data`float`)

### Visualisasi Data

 ![](https://raw.githubusercontent.com/jessicaavg/Book-Recommendation-System/main/image-1.png)

Visualisasi diatas menunjukkan jumlah buku yang diterbitkan setiap tahunnya dari 1978-2004. Buku paling banyak diterbitkan berada pada tahun **2002**, dan paling sedikit berada pada tahun **1978**.

---

## Data Preparation
Proses persiapan data memiliki peran yang krusial untuk memastikan bahwa model dapat beroperasi dengan efisien dan tepat. Berikut adalah langkah-langkah dalam proses ini:

1. **Menggabungkan Data "Books", "Ratings", dan "Users"**
  - Karena data mentah terdari dari 3 data yang berbeda, maka perlu menggabungkan semua data menjadi satu terlebih dahulu.
  - Data **"Ratings"** dan **"Books"** digabungkan berdasarkan nilai **ISBN**.
  - Data gabungan dari ratings dan books digabungkan lagi dengan data **"Users"** berdasarkan nilai **"User-ID"**.

2. **Mengurangi jumlah data karena device tidak kuat melakukan running**
  - Karena banyaknya jumlah data, device tidak kuat untuk melakukan running. Oleh karena itu, dilakukan pengurangan jumlah data dan hanya menggambil 250.000 data saja.
  - Pengambilan data dilakukan secara acak/random.

3. **Menghapus kolom "Image-URL-L", "Image-URL-m" dan "Location"**
  - Dalam pembuatan sistem rekomendasi buku terdapat 3 kolom yang tidak akan digunakan, yaitu **"Image-URL-L", "Image-URL-m" dan "Location"**. Maka dari itu, kolomnya dihapus.

4. **Mengatasi Missing Value**
  - Pada data **"Books"**. Mengisi missing value pada kolom "Book Author" dan "Publisher" dengan nilai modus.
  - Pada data **"Users"**. Mengisi missing value pada kolom "Age" dengan nilai median.
  - Missing value ditangani agar tidak menggangu ataupun mengurangi performa model pada proses selanjutnya. 

5. **Mengubah tipe data kolom "Age" menjadi numerik**
  - Proses ini mengkonversi data dalam kolom "Age" menjadi tipe data `int`.
  - Mengganti nilai non-numerik menjadi 0.

6. **Mengatasi Outlier untuk data "Age" dan "Year-of-Publication**
  - Sebelumnya, data "Age" dan "Year-of-Publication** memiliki nilai min dan nilai max yang tidak masuk akal. 
  - Proses ini mengidentifikasi dan menghapus outlier dari dua kolom yaitu kolom "Age" dan "Year-Of-Publication".
  - Tujuan utama proses ini adalah untuk membersihkan dataset dari data yang tidak konsisten atau tidak valid (outlier) yang dapat mempengaruhi kinerja model.

7. **Mendefinisikan Genre Tiap Judul Buku**
  - Mendefinisikan genre-genre buku yang akan digunakan sebagai label untuk memprediksi genre berdasarkan judul.
  - Membuat list sentences, yang merupakan daftar kata dari setiap judul buku di kolom **"Book-Title"** dimana setiap judul buku dipisahkan menjadi kata-kata.
  - Menggunakan model **Word2Vec** untuk menghasilkan representasi vektor dari kata-kata dalam judul buku.
  - Setelah mendefinisikan genre dari setiap buku, ditambahkan kolom **"Genre"** ke dalam keseluruhan data.
  - Karena proses ini, sistem akan memberikan rekomendasi genre buku yang lebih akurat berdasarkan judul buku.

8. **Menghapus Duplikasi Judul Buku**
  - Pada proses ini, buku yang memiliki judul yang terduplikat akan dihapus. Berfungsi untuk memastikan bahwa setiap judul hanya terdapat satu, tidak ada duplikasi lain.

9. **TF-IDF (Term Frequency-Inverse Document Frequency)**
  - Proses ini membuat teks dalam kolom **"Book-Title"** diubah menjadi representasi vektor yang akan digunakan untuk menghitung kesamaan antar buku.
  - Proses ini bertujuan untuk mengetahui tingkat kemiripan dari setiap buku berdasarkan judul, sehingga sistem dapat memberikan rekomendasi berdasarkan tingkat kemiripannya.

Proses persiapan data ini menjamin bahwa sistem dapat beroperasi dengan efisien dan tepat, sekaligus mengurangi kemungkinan terjadinya kesalahan dalam analisis.

---

## Modeling
Pada proyek ini, digunakan pendekatan **Content-Based Filtering** yang memanfaatkan judul buku untuk merekomendasikan buku yang mirip dengan yang dicari atau disukai oleh pengguna. 

**Cosine Similarity**
 - Setelah teks diubah menjadi representasi vektor, digunakan metode **Cosine Similarity** untuk menghitung kemiripan antara vektor dari judul buku. Dengan menggunakan cosine similarity, sistem dapat menentukan seberapa mirip dua buku berdasarkan konten teks mereka.

 - Cara Kerja:
   1. Menghitung kesamaan antara setiap pasangan vektor dalam matriks TF-IDF [2].
   2. Hasil cosine similarity adalah sebuah matriks yang menyimpan nilai kesamaan (similarity score) untuk setiap pasangan buku. Nilai berkisar antara 0 (tidak mirip) hingga 1 (sangat mirip).
   3. Setelah itu, menampilkan sampel acak dari matriks cosine similarity. Berguna untuk melihat nilai kesamaan antara beberapa buku tanpa harus menampilkan seluruh matriks.

 - Parameter yang Digunakan:
   - Tidak ada parameter khusus, cosine similarity bekerja secara otomatis tanpa perlu pengaturan tambahan.

### Output
Sistem ini menghasilkan **Top-N Recommendation**, yaitu 5 rekomendasi buku yang paling mirip dengan buku yang sedang dicari atau disukai oleh pengguna. Sebagai contoh, pengguna memilih buku "Void Moon", maka sistem akan memberikan 5 rekomendasi buku yang memiliki kemiripan dengan buku tersebut. Output dari 5 rekomendasi tersebut terlihat seperti berikut: 

  ![](https://raw.githubusercontent.com/jessicaavg/Book-Recommendation-System/main/image-2.png)

### Kelebihan dan Kekurangan 
  - **Kelebihan**: Sistem tidak memerlukan informasi tentang preferensi pengguna lain. Rekomendasi hanya didasarkan pada karakteristik buku itu sendiri dan profil pengguna aktif.
  - **Kekurangan**: Sistem hanya dapat merekomendasikan buku yang memiliki kesamaan dengan buku yang sudah diketahui oleh sistem.


## Evaluation
Metrik evaluasi yang digunakan dalam proyek ini adalah **Precision**, yang merujuk pada kemampuan sistem untuk memberikan rekomendasi yang relevan terhadap preferensi pengguna.

**Precision** adalah metrik evaluasi yang digunakan untuk mengukur keakuratan dari prediksi yang benar-benar positif di antara semua prediksi positif yang dihasilkan oleh model. 

  **Formula**:
      $$
      \text{Precision} = \frac{\text{True Positives (TP)}}{\text{True Positives (TP)} + \text{False Positives (FP)}}
      $$

### Penjelasan:
- **Jumlah Rekomendasi Relevan:** Jumlah item yang direkomendasikan oleh sistem dan dianggap relevan oleh pengguna.
- **Jumlah Rekomendasi yang Diberikan:** Total item yang direkomendasikan oleh sistem.

### Hasil Evaluasi
Sistem rekomendasi yang dibangun berhasil memberikan rekomendasi yang relevan dengan buku yang sedang dicari atau disukai oleh pengguna. Untuk model content-based filtering ini, metrik precision dapat dihitung sebagai berikut:

| **Parameter**                       | **Nilai**  |
|-------------------------------------|------------|
| Jumlah Rekomendasi yang Relevan     | 4          |
| Jumlah Item yang Direkomendasikan   | 5          |
| **Precision**                       | **0.8**    |

---

## Kesimpulan
Dengan menggunakan model **Based-Content Filtering**, sistem dapat memberikan rekomendasi buku yang cukup baik meskipun data pengguna masih terbatas, dengan memanfaatkan informasi yang ada seperti judul dan genre, tanpa perlu menggunakan data pengguna. Sistem mampu mengidentifikasi kesamaan antara buku-buku yang berbeda, sehingga dapat memberikan rekomendasi yang relevan berdasarkan kemiripan konten. Namun, untuk mendapatkan hasil yang lebih optimal, perlu dilakukan pengembangan lebih lanjut dengan mempertimbangkan faktor-faktor seperti kualitas data, pemilihan fitur, dan kombinasi dengan metode lain.