# Laporan Proyek Machine Learning - Andreas Wirawan Dananjaya

## Project Overview
Di era digital saat ini, ledakan informasi telah mengubah cara kita mengonsumsi konten, termasuk film. Dengan ribuan judul film yang tersedia di berbagai platform streaming, pengguna seringkali merasa kewalahan dan kesulitan dalam menemukan konten yang benar-benar relevan dengan preferensi mereka. Fenomena ini, yang dikenal sebagai information overload, dapat menyebabkan paradox of choice, di mana terlalu banyak pilihan justru menghambat pengambilan keputusan dan berpotensi mengurangi kepuasan pengguna (Romero Meza et al., 2024). Akibatnya, platform penyedia film menghadapi tantangan besar dalam mempertahankan engagement pengguna dan memastikan discovery konten yang efektif. Tanpa panduan yang efektif, pengguna mungkin melewatkan film-film berkualitas yang sebenarnya akan mereka nikmati, yang pada akhirnya dapat berdampak negatif pada retensi pengguna dan potensi pendapatan platform (Zakaria et al., 2024).

Salah satu pendekatan yang paling populer dan efektif dalam membangun sistem rekomendasi adalah Collaborative Filtering. Pendekatan ini bekerja dengan mengidentifikasi pola preferensi di antara sekelompok besar pengguna. Intinya, jika pengguna A memiliki selera yang mirip dengan pengguna B, maka film yang disukai pengguna A (tetapi belum ditonton oleh pengguna B) kemungkinan besar juga akan disukai pengguna B. Metode ini sangat kuat karena tidak memerlukan metadata film yang kompleks, melainkan hanya mengandalkan interaksi pengguna dengan item (Zhang, S et al., 2020). Sistem rekomendasi muncul sebagai solusi esensial untuk mengatasi information overload ini. Dengan menganalisis preferensi pengguna di masa lalu dan pola perilaku kolektif, sistem rekomendasi dapat secara cerdas menyaring dan menyajikan konten yang paling mungkin disukai oleh pengguna individual. Pendekatan ini tidak hanya meningkatkan pengalaman pengguna dengan mempersonalisasi discovery film, tetapi juga memberikan nilai signifikan bagi penyedia layanan dengan meningkatkan engagement, loyalitas pelanggan, dan pendapatan (Minaee, S et al., 2022).

Dalam pengembangan sistem rekomendasi, dua pendekatan utama sering digunakan untuk mempersonalisasi pengalaman pengguna. Pertama Content-Based Filtering (CBF), pendekatan ini merekomendasikan item kepada pengguna yang serupa dengan item yang disukai pengguna di masa lalu, berdasarkan atribut atau metadata dari item itu sendiri. Contohnya, jika seorang pengguna menyukai film-film bergenre 'Action' dan 'Sci-Fi', sistem akan merekomendasikan film-film lain yang juga bergenre 'Action' dan 'Sci-Fi' atau memiliki aktor/sutradara yang sama (Satapathy, S. et al., 2019). Kelebihan utama dari CBF adalah kemampuannya dalam merekomendasikan item baru yang belum memiliki riwayat interaksi (masalah cold start untuk item) dan memberikan rekomendasi yang lebih mudah dijelaskan karena didasarkan pada karakteristik konten yang eksplisit. Kedua adalah Collaborative Filtering, endekatan ini bekerja dengan mengidentifikasi pola preferensi di antara sekelompok besar pengguna. Intinya, jika pengguna A memiliki selera yang mirip dengan pengguna B, maka film yang disukai pengguna A (tetapi belum ditonton oleh pengguna B) kemungkinan besar juga akan disukai pengguna B. Metode ini sangat kuat karena tidak memerlukan metadata film yang kompleks, melainkan hanya mengandalkan interaksi pengguna dengan item (Fareed et al., 2023). Pemilihan arsitektur berbasis Deep Learning memungkinkan model untuk menangkap pola interaksi yang lebih kompleks dan non-linear antar pengguna dan film, mengatasi keterbatasan metode Collaborative Filtering tradisional seperti masalah skalabilitas dan penanganan data yang jarang (sparsity) (Althbiti et al., 2021).

Proyek ini berfokus pada pengembangan sistem rekomendasi film dengan mengimplementasikan kedua pendekatan utama ini: Collaborative Filtering dan Content-Based Filtering. Kami akan memanfaatkan dataset MovieLens Small Latest untuk membangun model Collaborative Filtering berbasis Deep Learning (RecommenderNet) untuk memprediksi rating film, serta menerapkan teknik Content-Based Filtering menggunakan vektorisasi TF-IDF dan Cosine Similarity pada fitur genre film. Dengan demikian, proyek ini bertujuan untuk menunjukkan efektivitas kedua paradigma ini dalam memberikan rekomendasi film yang relevan dan meningkatkan pengalaman discovery konten bagi pengguna.

Riset Penelitian Sebelumnya
- Penelitian yang dilakukan oleh Fajriansyah et al. (2021) dari Universitas Brawijaya mengembangkan sistem rekomendasi film berbasis Content-Based Filtering (CBF) yang memanfaatkan informasi berupa sinopsis dan judul film untuk memberikan rekomendasi yang relevan bagi pengguna. Metode yang digunakan dalam penelitian ini adalah TF-IDF untuk pembobotan term pada hasil pre-processing teks, yang kemudian diukur kesamaannya menggunakan Cosine Similarity. Hasil pembobotan ini selanjutnya difilter berdasarkan genre untuk mempertajam relevansi rekomendasi. Penelitian ini diuji dengan dataset sebanyak 4000 film dan melibatkan tiga partisipan untuk mengukur performa sistem, di mana pengukuran akurasi dilakukan dengan metrik Mean Average Precision @K (MAP@K). Hasil evaluasi menunjukkan bahwa sistem rekomendasi memiliki nilai MAP@K sebesar 0,8232 untuk kueri tunggal dan 0,7500 untuk multiple seeds, yang mengindikasikan bahwa pendekatan dengan satu referensi film lebih efektif dalam memberikan rekomendasi. Studi ini menekankan pentingnya analisis konten berbasis teks dan filtering berbasis genre dalam membangun sistem rekomendasi film yang mampu menyesuaikan dengan selera unik tiap pengguna.

- Penelitian yang dipublikasikan pada IEEE IAS Global Conference on Emerging Technologies (GlobConET) 2022 ini mengembangkan sistem rekomendasi film hybrid yang menggabungkan metode content-based filtering dan collaborative filtering. Pendekatan hibrida ini bertujuan untuk mengatasi kelemahan masing-masing metode dengan memanfaatkan kekuatan gabungan dalam hal efisiensi sistem, akurasi, dan relevansi rekomendasi. Untuk meningkatkan kualitas rekomendasi, penelitian ini juga mengintegrasikan teknik clustering, similarity, dan klasifikasi, yang terbukti menurunkan Mean Absolute Error (MAE) serta meningkatkan precision dan accuracy sistem. Sistem ini beroperasi menggunakan ID film tunggal, di mana rekomendasi diberikan berdasarkan prediksi dari perilaku pengguna sebelumnya tanpa mempertimbangkan genre film, menjadikannya cukup fleksibel namun juga fokus. Penelitian ini juga menyinggung bahwa filtering berbasis demografis masih sangat dasar dan tidak cukup kuat untuk implementasi praktis, sedangkan content-based dan collaborative filtering menunjukkan hasil yang saling melengkapi, khususnya dalam sistem rekomendasi hybrid. Dalam konteks yang lebih luas, penelitian ini mencerminkan evolusi sistem rekomendasi yang kini telah menjadi bagian integral dari berbagai bidang seperti e-commerce dan media sosial, serta menunjukkan bagaimana integrasi machine learning berperan penting dalam meningkatkan personalisasi dan prediktivitas rekomendasi berbasis data pengguna.



## Business Understanding
### Problem Statements

Berdasarkan latar belakang yang telah diidentifikasi sebelumnya, berikut adalah problem statements dari proyek ini :
- Bagaimana rekomendasi film dapat dihasilkan berdasarkan atribut konten eksplisit, seperti genre, untuk memastikan relevansi langsung dengan jenis film yang telah disukai pengguna?
- Bagaimana presisi sebuah model Machine Learning dalam memprediksi rating numerik yang kemungkinan akan diberikan pengguna pada film yang belum pernah ditonton?
- Bagaimana suatu sistem dapat secara efektif menyajikan daftar rekomendasi film yang dipersonalisasi untuk setiap pengguna, berdasarkan analisis pola preferensi historis user?

### Goals
Berdasarkan pernyataan masalah yang telah diidentifikasi, proyek ini memiliki tujuan utama sebagai berikut:
- Mengembangkan sistem yang mampu merekomendasikan film berdasarkan kemiripan atribut konten (misalnya, genre) dengan film yang disukai pengguna. Validasi dilakukan melalui inspeksi kualitatif, memastikan rekomendasi memiliki karakteristik konten yang identik atau sangat mirip dengan film referensi.
- Menciptakan model Machine Learning yang mampu memprediksi rating numerik film (skala 0.5-5.0) dengan meminimalkan error prediksi,
- Mengimplementasikan kapabilitas untuk menghasilkan daftar film yang direkomendasikan secara personal (Top-N rekomendasi) untuk pengguna, berdasarkan film-film dengan prediksi rating tertinggi yang belum pernah ditonton.

### Solution statements
- Pengguaan Content-Based Filtering dengan Vektorisasi TF-IDF dan Cosine Similarity.  Metode ini memanfaatkan metadata film, khususnya genre, untuk membangun representasi numerik (vektor TF-IDF) dari setiap film. Kemiripan antar film kemudian diukur menggunakan Cosine Similarity. Rekomendasi dihasilkan dengan mengidentifikasi film-film yang memiliki kemiripan konten tertinggi dengan film yang telah disukai pengguna di masa lalu.
- Pengunaan Collaborative Filtering via Matrix Factorization. model ini adalah RecommenderNet berbasis TensorFlow atau Keras yang mempelajari embedding vektor untuk setiap pengguna dan film, memprediksi rating melalui dot product serta bias, dan dioptimasi dengan Mean Squared Error untuk menghasilkan prediksi rating yang akurat dalam kondisi data yang jarang, sekaligus membentuk dasar rekomendasi personal.
- Top-N Recommendation Generation Based on Predicted Ratings. Setelah model terlatih, sistem akan menghasilkan rekomendasi dengan memprediksi rating untuk semua film yang belum ditonton pengguna, mengurutkannya berdasarkan nilai prediksi tertinggi, lalu menyajikan daftar Top-N film yang paling relevan secara personal.

## Data Understanding
Dataset yang digunakan dalam proyek ini adalah MovieLens Small Latest Dataset. Dataset ini merupakan koleksi aktivitas rating bintang 5 dan tagging teks bebas dari layanan rekomendasi film MovieLens. Sumber asli data ini adalah GroupLens, sebuah grup riset di Universitas Minnesota, dan dapat diunduh melalui platform Kaggle. dataset bisa diunduh melalui link berikut :
https://www.kaggle.com/datasets/shubhammehta21/movie-lens-small-latest-dataset 
Data ini mencakup 100.836 rating dan 3.683 aplikasi tag pada 9.742 film. Interaksi ini dilakukan oleh 610 pengguna antara 29 Maret 1996 hingga 24 September 2018. Pengguna yang disertakan dalam dataset ini dipilih secara acak, dengan setiap pengguna telah memberikan setidaknya 20 rating.

Dataset MovieLens Small Latest terdiri dari empat file CSV: links.csv, movies.csv, ratings.csv, dan tags.csv. Untuk keperluan proyek ini, yang berfokus pada pembangunan sistem rekomendasi berbasis Collaborative Filtering dengan embedding untuk memprediksi rating film, hanya dua file yang relevan dan esensial yang digunakan: movies.csv dan ratings.csv. Pada proyek ini hanya menggunakan ratings.csv dan movies.csv karena keduanya menyediakan data inti yang dibutuhkan untuk membangun model Collaborative Filtering berbasis embedding, yakni interaksi eksplisit pengguna–film (userId, movieId, rating) dan metadata film untuk identifikasi hasil rekomendasi. 

Variabel-variabel pada movies.csv :
- movieId: Merupakan ID unik untuk setiap film. Tipe data: int64. Tidak ada nilai null.
- title: Merupakan judul lengkap dari film, seringkali disertai dengan tahun rilis. Tipe data: object (string). Tidak ada nilai null.
- genres: Merupakan kategori genre film, dipisahkan oleh karakter pipa (|) jika film memiliki lebih dari satu genre. Tipe data: object (string). Tidak ada nilai null.

Variabel-variabel pada ratings.csv :
- userId: Merupakan ID unik untuk setiap pengguna. Tipe data: int64. Tidak ada nilai null.
- movieId: Merupakan ID unik dari film yang diberi rating. Tipe data: int64. Tidak ada nilai null.
- rating: Merupakan rating yang diberikan pengguna untuk film, dalam skala 0.5 hingga 5.0. Tipe data: float64. Tidak ada nilai null.
- timestamp: Merupakan waktu ketika rating diberikan, dalam format Unix epoch seconds. Tipe data: int64. Tidak ada nilai null.

Tidak terdapat data duplikat maupun missing value pada dataset ini (Jumlah duplikasi: 0).
### Analisis Fitur Konten Content-Based Filtering (CBF)
#### Fitur Genre Film
Terdapat 20 genre Unik yang menunjukkan keragaman genre dalam dataset, yang menjadi dasar bagi model Content-Based Filtering.

- **Distribusi Frekuensi Genre**
![alt text](https://github.com/andreaswd31/Sistem-Rekomendasi-Film/blob/main/Top%2010%20Genre%20Paling%20Sering%20Muncul.png?raw=true)
Top 10 Genre Paling Sering Muncul:

    | No. | Genre      | Number of Movies |
    |-----|------------|------------------|
    | 1   | Drama        | 4361             |
    | 1   | Comedy     | 3756             |
    | 2   | Thriller   | 1894             |
    | 3   | Action     | 1828             |
    | 4   | Romance    | 1596             |
    | 5   | Adventure  | 1263             |
    | 6   | Crime      | 1199             |
    | 7   | Sci-Fi     | 980              |
    | 8   | Horror     | 978              |
    | 9   | Fantasy    | 779              |


Data menunjukkan bahwa 'Drama' dan 'Comedy' adalah genre yang paling dominan, diikuti oleh 'Thriller' dan 'Action'. Ini mengindikasikan bahwa sebagian besar koleksi film dalam dataset MovieLens Small terfokus pada genre-genre populer ini. Hal ini penting untuk Content-Based Filtering, karena film-film yang direkomendasikan kemungkinan besar akan cenderung ke genre-genre yang dominan ini, mencerminkan komposisi dataset itu sendiri.


- **Rata-rata Jumlah Genre per Film**

    ![alt text](https://github.com/andreaswd31/Sistem-Rekomendasi-Film/blob/main/Distribusi%20Jumlah%20Genre%20per%20Film.png?raw=true)
  
    Distribusi Jumlah Genre per Film:

    | Jumlah Genre | Jumlah Film |
    |-------------|------------|
    | 1           | 2851       |
    | 2           | 3218       |
    | 3           | 2338       |
    | 4           | 987        |
    | 5           | 271        |
    | 6           | 63         |
    | 7           | 12         |
    | 8           | 1          |
    | 10          | 1          |

    Distribusi ini menunjukkan bahwa mayoritas film memiliki 1, 2, atau 3 genre. Hanya sedikit film yang memiliki 4 genre atau lebih. Ini berarti representasi TF-IDF untuk sebagian besar film tidak akan terlalu "padat" (banyak fitur), dan kemiripan akan lebih mudah dihitung karena jumlah genre per film tidak terlalu bervariasi secara ekstrem.

### Analisis Fitur Konten Colaborative Filtering (CF)
#### Kelangkaan Data (Sparsity)
Salah satu karakteristik terpenting dalam sistem rekomendasi adalah kelangkaan data, di mana pengguna hanya berinteraksi dengan sebagian kecil dari total item yang tersedia.
Statistik Sparsity:
- **Jumlah Pengguna Unik: 610**
- **Jumlah Film Unik: 9724**
- **Total Kemungkinan Rating: 5931640 (610 users * 9724 movies)**
- **Jumlah Rating Aktual: 100836**
- **Sparsity Dataset: 98.30%**

Tingkat sparsity yang sangat tinggi (98.30%) menegaskan bahwa dataset interaksi pengguna-film sangat jarang. Ini adalah karakteristik fundamental yang membuat model Collaborative Filtering sangat relevan dan diperlukan, karena model harus mampu memprediksi preferensi dari data yang sangat terbatas in

#### Pola Interaksi Rating, Film dan, Pengguna
* **Distribusi Rating Film**

    ![alt text](https://github.com/andreaswd31/Sistem-Rekomendasi-Film/blob/main/Distribusi%20Rating%20Film1.png?raw=true)
  
    Mayoritas rating terkonsentrasi pada nilai 3.0, 4.0, dan 5.0, dengan rating 4.0 menjadi yang paling dominan. Rating di bawah 2.5 memiliki frekuensi yang jauh lebih rendah. Hal ini mengindikasikan bahwa pengguna cenderung memberikan rating yang cukup tinggi, menunjukkan preferensi umum terhadap film-film yang dinilai baik.

* **Distribusi jumlah rating per pengguna**

    ![alt text](https://github.com/andreaswd31/Sistem-Rekomendasi-Film/blob/main/Distribusi%20Jumlah%20Rating%20per%20Pengguna.png?raw=true)

    Statistik Jumlah Rating per Pengguna:
    | Statistik | Nilai        |
    |-----------|-------------|
    | Count     | 610         |
    | Mean      | 165.304918  |
    | Std Dev   | 269.480584  |
    | Min       | 20.000000   |
    | 25%       | 35.000000   |
    | 50%       | 70.500000   |
    | 75%       | 168.000000  |
    | Max       | 2698.000000 |

    Terdapat variasi signifikan dalam aktivitas pengguna, dengan rentang rating dari minimal 20 hingga maksimum 2698. Hal ini menunjukkan keberadaan "pengguna super aktif" (power users) yang memberikan banyak rating, serta mayoritas pengguna yang lebih pasif. Model perlu mampu menangani spektrum aktivitas ini.

* **Distribusi jumlah rating per film**

    ![alt text](https://github.com/andreaswd31/Sistem-Rekomendasi-Film/blob/main/Distribusi%20jumlah%20rating%20per%20film.png?raw=true)

    Statistik Jumlah Rating per Film:
    | Statistik | Nilai        |
    |-----------|-------------|
    | Count     | 9724        |
    | Mean      | 10.369807   |
    | Std Dev   | 22.401005   |
    | Min       | 1.000000    |
    | 25%       | 1.000000    |
    | 50%       | 3.000000    |
    | 75%       | 9.000000    |
    | Max       | 329.000000  |

    Mirip dengan pengguna, ada film yang sangat populer (menerima ratusan rating) dan banyak film yang hanya menerima sedikit rating (minimal 1 rating). Film dengan sedikit data mungkin menjadi tantangan dalam hal prediksi yang akurat (masalah cold start untuk item), sementara film populer memiliki data yang kaya.

* **Top 10 Film dan Pengguna**

    ![alt text](https://github.com/andreaswd31/Sistem-Rekomendasi-Film/blob/main/Top%2010%20Film%20dengan%20Jumlah%20Rating%20Terbanyak.png?raw=true)
    Film-film seperti 'Forrest Gump', 'Shawshank Redemption', dan 'Pulp Fiction' mendominasi dengan jumlah rating terbanyak. Ini umumnya adalah film-film populer yang dikenal luas, menunjukkan bahwa dataset mencerminkan pola popularitas film di dunia nyata.

* **Top 10 Pengguna dengan Jumlah Rating Terbanyak**

    ![alt text](https://github.com/andreaswd31/Sistem-Rekomendasi-Film/blob/main/Top%2010%20Pengguna%20dengan%20Jumlah%20Rating%20Terbanyak.png?raw=true)
    Grafik ini secara visual mengkonfirmasi keberadaan "power users" seperti Pengguna 414 dan Pengguna 599 yang telah memberikan ribuan rating. Kelompok pengguna ini merupakan sumber data interaksi yang sangat kaya dan berkontribusi signifikan terhadap volume data dalam dataset.

## Data Preparation
Pada bagian ini, data mentah yang telah dipahami melalui EDA akan diubah dan diformat sedemikian rupa agar siap untuk diolah oleh kedua pendekatan sistem rekomendasi: Collaborative Filtering dan Content-Based Filtering. Tujuan utama dari tahapan ini adalah untuk memastikan data dalam format yang optimal untuk pelatihan model dan untuk meningkatkan efisiensi komputasi.

### Data Case-Based Filtering (CBF)
Untuk pendekatan Content-Based Filtering, berfokus pada informasi deskriptif film, khususnya kolom genres dari movies.csv. Tujuan dari bagian ini adalah untuk mengubah informasi tekstual genre menjadi representasi numerik yang dapat digunakan untuk menghitung kemiripan antar film.
* **Pra-pemrosesan Fitur genres**
    ```python
    movies['genres'] = movies['genres'].fillna('')
    ```
    Berikut adalah daftar genre yang terdapat dalam dataset:
  
    ![alt text](https://github.com/andreaswd31/Sistem-Rekomendasi-Film/blob/main/Screenshot%202025-05-28%20235826.png?raw=true)
    
    Kolom genres yang berisi string dengan genre dipisahkan oleh tanda pipa (|) adalah fitur utama untuk Content-Based Filtering. Memastikan tidak ada nilai kosong (NaN) sangat penting agar proses vektorisasi tekstual tidak terganggu dan setiap film memiliki representasi genre yang valid.
* **Vektorisasi Fitur Konten (TF-IDF Vectorizer)**
TF-IDF (Term Frequency-Inverse Document Frequency) Vectorizer untuk mengubah deskripsi genre setiap film menjadi vektor numerik. TF-IDF memberikan bobot pada setiap genre (kata) berdasarkan frekuensinya dalam satu film relatif terhadap frekuensinya di seluruh koleksi film.
    ```python
    tfidf_vectorizer = TfidfVectorizer(stop_words='english')
    tfidf_matrix = tfidf_vectorizer.fit_transform(movies['genres'])
    ```
    Hasil TF-IDF terdapat 9.742 film (sesuai jumlah film unik) dan TF-IDF Vectorizer berhasil mengidentifikasi 23 genre/kata unik dari seluruh koleksi genre. Ini menunjukkan bahwa vektorisasi berhasil menciptakan representasi numerik untuk setiap film berdasarkan genrenya,
    kata/token yang dianggap sebagai fitur oleh TF-IDF. Kehadiran 'fi' (dari 'Sci-Fi') menunjukkan bahwa TfidfVectorizer memisahkan kata dengan benar meskipun ada tanda hubung. Semua genre utama terlihat di sini, menunjukkan bahwa proses ini berhasil menangkap karakteristik konten film.
    
    Model berbasis kemiripan tidak dapat bekerja langsung dengan teks mentah. TF-IDF adalah teknik yang efektif untuk mengubah data tekstual (genre) menjadi representasi numerik yang padat, di mana setiap film diwakili oleh sebuah vektor. Bobot TF-IDF secara cerdas menangkap pentingnya suatu genre bagi sebuah film dalam konteks seluruh dataset, bukan hanya frekuensi kemunculannya.   
    
* **Penghitungan Kemiripan Konten (Cosine Similarity)**
cosine similarity untuk mengukur kemiripan antar item (film) berdasarkan fitur kontennya (misalnya genre yang sudah diolah menjadi TF-IDF). 
    ```python
    cosine_sim = cosine_similarity(tfidf_matrix, tfidf_matrix)
    cosine_sim_df = pd.DataFrame(cosine_sim, index=movies['title'].values, columns=movies['title'].values)
    ```
    Hasil dari Matriks ini adalah *Shape (9742, 9742)* mengkonfirmasi bahwa kemiripan telah dihitung antara setiap film dengan setiap film lainnya. Ini adalah matriks kemiripan yang  dibutuhkan untuk Content-Based Filtering.
    * Nilai Kemiripan :
        * Nilai diagonal utama (misal 1.000000) menunjukkan kemiripan film dengan dirinya sendiri, yang selalu 1.
        * Nilai off-diagonal (misal 0.81357774 antara Toy Story dan Jumanji) menunjukkan kemiripan antar film. Nilai yang tinggi (0.81) menunjukkan kemiripan yang kuat, sementara nilai yang rendah (0.0, 0.15) menunjukkan kemiripan yang rendah. Ini masuk akal, karena Toy Story dan Jumanji keduanya memiliki genre Adventure|Children|Fantasy (Toy Story memiliki Animation|Comedy tambahan), sehingga wajar jika mirip. Film Grumpier Old Men (Comedy|Romance) memiliki kemiripan 0 dengan Jumanji yang tidak memiliki genre Comedy/Romance.
    * DataFrame cosine_sim_df adalah format yang sangat berguna karena memungkinkan untuk dengan mudah mencari kemiripan berdasarkan judul film, yang akan sangat membantu dalam fungsi rekomendasi nanti.
    
### Data Preparation Collaborative Filtering (CF)
#### Encoding ID Pengguna dan Film
Langkah pertama dalam persiapan data Collaborative Filtering adalah melakukan encoding pada userId dan movieId. ID asli yang mungkin tidak berurutan atau memiliki celah (gap) diubah menjadi indeks numerik berurutan yang dimulai dari 0. Proses ini melibatkan pembuatan pemetaan (mapping) dari ID asli ke ID ter-encoded, dan juga pemetaan sebaliknya untuk keperluan rekonstruksi dan interpretasi hasil rekomendasi di kemudian hari.

- Membuat variabel unik untuk user dan movie ID
    ```python
    user_ids = ratings['userId'].unique().tolist()
    movie_ids = ratings['movieId'].unique().tolist()
    ```
- Melakukan encoding user ID
    ```python
    user_to_user_encoded = {x: i for i, x in enumerate(user_ids)}
    user_encoded_to_user = {i: x for i, x in enumerate(user_ids)}
    ```
- Menambahkan kolom encoded ke dataframe ratings
    ```python
    ratings['user'] = ratings['userId'].map(user_to_user_encoded)
    ratings['movie'] = ratings['movieId'].map(movie_to_movie_encoded)
    ```
DataFrame Ratings setelah Encoding
| userId | movieId | rating | timestamp | user | movie |
|--------|---------|--------|-----------|------|-------|
| 1      | 1       | 4.0    | 964982703 | 0    | 0     |
| 1      | 3       | 4.0    | 964981247 | 0    | 1     |
| 1      | 6       | 4.0    | 964982224 | 0    | 2     |
| 1      | 47      | 5.0    | 964983815 | 0    | 3     |
| 1      | 50      | 5.0    | 964982931 | 0    | 4     |

Jumlah Pengguna Unik (setelah encoding): **610**  
Jumlah Film Unik (setelah encoding): **9724**
Terlihat bahwa satu pengguna dapat memberikan rating pada berbagai film, dan seluruh interaksi ini akan digunakan sebagai data pelatihan untuk mempelajari preferensi pengguna secara efisien. Dataset ini terdiri dari 610 pengguna unik dan 9724 film unik, yang menunjukkan skala dan keragaman data interaksi yang tersedia untuk proses pembelajaran model rekomendasi.

Model neural network, khususnya embedding layers, memerlukan input berupa indeks numerik yang berurutan dan padat (dense) dimulai dari 0. ID asli userId dan movieId seringkali tidak berurutan dan memiliki celah yang besar, yang dapat menyebabkan alokasi memori yang tidak efisien dan pelatihan model yang kurang optimal jika digunakan secara langsung sebagai indeks embedding. Encoding ini memastikan bahwa setiap pengguna dan film memiliki indeks unik yang sesuai untuk lapisan embedding, sekaligus memudahkan pemetaan kembali ke ID asli untuk interpretasi rekomendasi.

#### Persiapan Variabel dan Pembagian Data (Train-Validation Split)
Setelah ID di-encode, variabel-variabel penting seperti jumlah total pengguna dan film unik, serta rentang rating, diidentifikasi.
* Persiapan Variabel untuk Model
    ```python
    num_users = len(user_to_user_encoded)
    num_movies = len(movie_to_movie_encoded)
    min_rating = ratings['rating'].min()
    max_rating = ratings['rating'].max()
    ```
    Jumlah pengguna dan film yang terlibat dalam model masing-masing adalah 610 dan 9724, sesuai dengan hasil encoding. Rentang rating yang digunakan dalam pelatihan model berkisar dari 0.5 hingga 5.0, mencerminkan skala penilaian yang digunakan pengguna dalam dataset MovieLens. Untuk proyek ini, rating target (y) dipertahankan dalam skala aslinya (0.5 hingga 5.0) tanpa normalisasi, memungkinkan model untuk memprediksi nilai dalam rentang tersebut secara langsung.
    
    Mengetahui num_users dan num_movies sangat penting karena ini menentukan ukuran embedding layers dalam model. min_rating dan max_rating digunakan sebagai referensi untuk memahami rentang prediksi model.
* Pembagian Data (Train-Validation Split)
    ```python
    X = ratings[['user', 'movie']].values  
    y = ratings['rating'].values          
    X_train, X_val, y_train, y_val = train_test_split(X,y,test_size=0.2,)
    ```
    Data interaksi pengguna dan film dipisahkan menjadi fitur (X) yang berisi pasangan user dan movie, serta label (y) yang berisi rating. Kemudian dilakukan pembagian data sebanyak 80% untuk training (X_train: 80.668 baris) dan 20% untuk validation (X_val: 20.168 baris). Ukuran y_train dan y_val juga mengikuti pembagian yang sama, menunjukkan bahwa proses split berhasil dilakukan dengan proporsi yang seimbang dan siap digunakan dalam pelatihan dan evaluasi model.
    
    Pembagian dataset menjadi training dan validation set adalah praktik standar dalam Machine Learning. Training set digunakan untuk melatih model, sementara validation set digunakan untuk mengevaluasi kinerja model pada data yang belum pernah dilihat selama pelatihan. Hal ini krusial untuk mengukur kemampuan generalisasi model dan mendeteksi overfitting. Proporsi 80:20 untuk training dan validation adalah pilihan umum yang memberikan cukup data untuk kedua tujuan. random_state digunakan untuk memastikan pembagian data yang sama setiap kali kode dijalankan, menjamin reproduktibilitas hasil.

## Modeling
Tahap Modeling adalah inti dari proyek ini, di mana sistem rekomendasi dibangun dan dilatih (untuk CF) atau diimplementasikan logikanya (untuk CBF) untuk memprediksi rating film dan menghasilkan rekomendasi. Model-model yang dikembangkan bertujuan untuk mengatasi problem statements yang telah diuraikan, khususnya dalam memprediksi preferensi pengguna dan menyediakan rekomendasi yang dipersonalisasi.

### Pendekatan Content-Based Filtering (CBF)
Pendekatan Content-Based Filtering berfokus pada kemiripan atribut konten antar film untuk menghasilkan rekomendasi. Model ini tidak melibatkan pelatihan neural network dalam artian tradisional, melainkan serangkaian langkah pra-pemrosesan dan komputasi kemiripan.
Setelah fitur genre film diubah menjadi representasi numerik (TF-IDF) dan matriks kemiripan kosinus antar film dihitung di tahap Data Preparation, sebuah fungsi rekomendasi diimplementasikan. Fungsi ini menerima judul film referensi dan menggunakan matriks kemiripan untuk menemukan film-film lain yang paling serupa secara konten.

Fungsi ini adalah inti operasional dari Content-Based Filtering. Ia memungkinkan sistem untuk secara cepat dan efisien mengidentifikasi film-film dengan karakteristik konten yang paling serupa dengan film yang disukai pengguna, berdasarkan metrik kemiripan yang telah dihitung. Implementasi ini secara langsung menjawab kebutuhan untuk menghasilkan rekomendasi berdasarkan atribut eksplisit film.
- Kelebihan:
    * Mengatasi Cold Start Item: Model ini mampu merekomendasikan film baru yang belum memiliki riwayat rating karena rekomendasinya murni berdasarkan atribut konten film tersebut. Selama film memiliki metadata (genre, deskripsi, dll.), ia dapat direkomendasikan.
    * Rekomendasi yang dihasilkan lebih transparan dan mudah dijelaskan kepada pengguna (misalnya, "Kami merekomendasikan film ini karena genre-nya mirip dengan film yang Anda sukai").
    * Rekomendasi tidak dipengaruhi oleh preferensi pengguna lain, yang berarti tidak ada masalah "kembaran" yang aneh atau preferensi grup.

- Kekurangan:
    * Model cenderung merekomendasikan film yang sangat mirip dengan yang sudah disukai pengguna, membatasi discovery film yang beragam atau di luar zona nyaman pengguna (serendipity).
    * Kualitas rekomendasi sangat bergantung pada kelengkapan dan kualitas metadata item. Jika metadata kurang atau tidak akurat, rekomendasi bisa menjadi buruk.
    * Model ini kesulitan merekomendasikan kepada pengguna baru yang belum memiliki riwayat preferensi yang cukup untuk membangun profil konten mereka.

- **Output Top-10 Rekomendasi Film Content-Based Filtering**
    ![alt text](https://github.com/andreaswd31/Sistem-Rekomendasi-Film/blob/main/Uji%20Tes%20Rekomendasi%20Content-Based%20Filtering.png?raw=true)
    Hasil uji coba menunjukkan bahwa model Content-Based Filtering berhasil merekomendasikan film-film yang memiliki kemiripan konten sangat tinggi, dengan similarity score sebesar 1.00. Semua film yang direkomendasikan memiliki genre Drama|Thriller yang identik dengan film referensi 'Girl with the Dragon Tattoo, The (2011)'. Ini memvalidasi bahwa sistem secara efektif dapat merekomendasikan film berdasarkan atribut konten eksplisit, secara langsung menjawab Problem Statement 3 tentang relevansi rekomendasi berbasis konten.

### Pendekatan Collaborative Filtering (CF)
Pendekatan Collaborative Filtering, khususnya dengan Matrix Factorization berbasis embedding, memprediksi rating film berdasarkan pola interaksi kolektif pengguna. Model ini memprediksi rating antara pengguna dan item (film) berdasarkan dot product dari vektor embedding pengguna dan item, ditambah dengan bias pengguna dan item.
**Rumus Prediksi Rating:**
$$\hat{r}_{ui} = \vec{p}_u \cdot \vec{q}_i + b_u + b_i$$
**Keterangan:**
- $$\hat{r}_{ui}$$: rating yang diprediksi oleh pengguna $u$ terhadap item $i$
- $$\vec{p}_u$$: vektor embedding pengguna $u$
- $$\vec{q}_i$$: vektor embedding item $i$
- $$b_u$$: bias pengguna $u$
- $$b_i$$: bias item $i$

* **Arsitektur Model: RecommenderNet**
Model RecommenderNet diimplementasikan menggunakan TensorFlow dan Keras. Arsitektur ini menggunakan embedding layers untuk merepresentasikan pengguna dan film dalam ruang vektor berdimensi rendah.
Fungsi loss yang digunakan untuk melatih model biasanya berupa Mean Squared Error (MSE)
$$\mathcal{L} = \frac{1}{N} \sum_{(u,i) \in K} \left( r_{ui} - \hat{r}_{ui} \right)^2$$
    - $$K$$: himpunan semua pasangan user-item dalam data pelatihan
    - $$r_{ui}$$: rating aktual
    - $$\hat{r}_{ui}$$: rating hasil prediksi
    - $$N$$: jumlah total data dalam $K$

    RecommenderNet adalah model rekomendasi berbasis Matrix Factorization yang dibangun menggunakan Keras subclassing. Model ini mempelajari embedding (representasi vektor) untuk pengguna dan film.
    - self.user_embedding dan self.movie_embedding: Mewakili setiap pengguna dan film sebagai vektor berdimensi tetap (embedding_size). 
    - Bobot awal diinisialisasi dengan he_normal, dan regularisasi L2 digunakan untuk menghindari overfitting.
    
    Pada metode call, model:
    - Mengambil embedding dan bias berdasarkan input ID pengguna dan film.
    - Menghitung prediksi rating melalui dot product antara user dan movie vector, lalu ditambahkan dengan bias masing-masing.
    - Fungsi tf.squeeze() digunakan agar output berbentuk satu dimensi ((batch_size,)), sesuai format rating sebenarnya.
    - self.user_bias dan self.movie_bias: Menambahkan nilai bias spesifik untuk masing-masing pengguna dan film.


* **Inisialisasi dan Kompilasi Model**
Model Collaborative Filtering dikompilasi menggunakan Adam optimizer dan Mean Squared Error (MSE) sebagai loss function, dengan Root Mean Squared Error (RMSE) dipantau sebagai metrik. Model dilatih menggunakan data X_train (pasangan user-movie ID ter-encoded) dan y_train (rating asli), dengan validasi pada X_val dan y_val.
RecommenderNet adalah model rekomendasi berbasis collaborative filtering yang memanfaatkan embedding untuk merepresentasikan pengguna dan film dalam ruang vektor berdimensi 50 (EMBEDDING_SIZE=50). Model dikompilasi menggunakan: 
    * optimizer=Adam(learning_rate=0.001): Optimizer Adam dipilih karena efisien dan cocok untuk data sparse.
    * loss=MeanSquaredError(): Fungsi loss ini digunakan karena target yang diprediksi adalah rating dalam skala kontinu (0.5–5.0), bukan kelas diskrit.
    * metrics=RootMeanSquaredError(): Digunakan untuk mengukur rata-rata kesalahan prediksi, agar mudah diinterpretasikan dalam skala rating.

* **Training Model RecommenderNet**
    Model dilatih menggunakan data input berupa pasangan ID pengguna dan ID film (X_train) serta target rating aktual (y_train). Proses pelatihan dilakukan selama 20 epoch, di mana pada setiap epoch, model mencoba meminimalkan loss (Mean Squared Error) antara prediksi dan rating sebenarnya. Data validasi (X_val, y_val) digunakan untuk memantau performa model di data yang tidak dilatih, membantu mendeteksi overfitting sejak dini. Parameter verbose=1 digunakan untuk menampilkan progres pelatihan secara rinci. Model berhasil dilatih selama 20 epoch, dengan perbaikan bertahap pada nilai loss dan root mean squared error (RMSE) di data pelatihan maupun validasi. Pada epoch awal, RMSE validasi masih tinggi (sekitar 7.80), namun seiring pelatihan, nilai tersebut terus menurun, mencapai sekitar 0.82 - 0,87 di akhir pelatihan. Hal ini menunjukkan bahwa model mulai mampu memberikan prediksi rating yang mendekati nilai sebenarnya, meskipun fluktuasi ringan tetap terlihat, yang wajar dalam proses pembelajaran model rekomendasi berbasis embedding.
    Penggunaan optimizer Adam dan loss function MSE merupakan pilihan standar dan efektif untuk melatih model regresi berbasis neural network. Pemantauan RMSE memungkinkan evaluasi yang intuitif terhadap akurasi prediksi. Proses pelatihan memungkinkan model untuk belajar pola interaksi dari data dan menyesuaikan bobotnya agar dapat memprediksi rating secara akurat.

**Kelebihan dan Kekurangan Pendekatan Collaborative Filtering**
- **kelebihan**
    * Menemukan Pola Tersembunyi: Model ini dapat menemukan hubungan dan pola preferensi antar pengguna/item yang mungkin tidak terdeteksi secara eksplisit oleh fitur konten. Ini memungkinkan rekomendasi film yang 'tidak terduga' tetapi relevan (serendipity).
    * Tidak Membutuhkan Metadata Item: CF tidak memerlukan informasi detail tentang item itu sendiri (seperti genre, deskripsi, dll.) untuk berfungsi, hanya data interaksi pengguna-item.
    * Dinamis terhadap Tren: Preferensi pengguna dapat berubah seiring waktu, dan model CF dapat menyesuaikan rekomendasi berdasarkan interaksi terbaru dari komunitas pengguna.
- **Kekurangan**
    * Masalah Cold Start (Pengguna & Item Baru): Model kesulitan merekomendasikan film baru yang belum memiliki rating atau untuk pengguna baru yang belum memberikan rating yang cukup, karena tidak ada data interaksi yang cukup untuk mempelajari embedding mereka
    * Sparsity: Meskipun diatasi sebagian oleh embedding, data yang sangat jarang masih menjadi tantangan bagi CF. Kualitas rekomendasi mungkin berkurang untuk pengguna atau item dengan sedikit interaksi.
    * Skalabilitas: Meskipun Matrix Factorization lebih baik dari User-Based tradisional, membangun model yang sangat besar untuk jutaan pengguna/item masih memerlukan sumber daya komputasi yang signifikan.
    
* Hasil Proyek Berdasarkan Metrik Evaluasi (Uji Tes Rekomendasi)
Untuk lebih lanjut mengevaluasi kemampuan model dalam menghasilkan rekomendasi yang dipersonalisasi, uji tes dilakukan dengan memilih Pengguna ID 525 dan menghasilkan 10 rekomendasi film teratas berdasarkan prediksi rating.
    - Memilih Pengguna Uji 
    Dipilih satu pengguna dari data validasi (`X_val`) untuk dijadikan subjek uji. Misalnya Pengguna ID Asli: 525  (Encoded ID: 524)
    - Menampilkan Film yang Sudah Ditonton
    Ditampilkan daftar film yang sebelumnya sudah diberi rating oleh pengguna tersebut untuk mengetahui preferensi awalnya. Contoh:

    ![alt text](https://github.com/andreaswd31/Sistem-Rekomendasi-Film/blob/main/model11.png?raw=true)
  
    - Menentukan Film yang Belum Ditonton
    Dengan menyaring semua film yang tidak terdapat dalam daftar rating pengguna, diperoleh daftar film yang **belum ditonton**. Jumlahnya:  9224
    - Prediksi Rating untuk Film yang Belum Ditonton
    Menggunakan model yang telah dilatih, dilakukan prediksi terhadap seluruh film yang belum ditonton oleh pengguna tersebut.

        | movieId | predicted_rating |
        |---------|------------------|
        | 3       |  2.428719            |
        | 6       | 3.238611             |
        | 70       |  2.828757            |
        | 101      | 3.202521             |
        | 110     | 3.334437             |

    - Output Top-10 Rekomendasi Film Collaborative Filtering
    Film dengan prediksi rating tertinggi kemudian diurutkan dan ditampilkan sebagai rekomendasi utama.
    **Top 10 Rekomendasi Film untuk Pengguna 525:**
      ![alt text](https://github.com/andreaswd31/Sistem-Rekomendasi-Film/blob/main/Screenshot%202025-05-30%20141910.png?raw=true)
      
    - Analisis Hasil Uji Tes Rekomendasi
      Model Collaborative Filtering berhasil menghasilkan 10 rekomendasi film teratas untuk Pengguna ID 525, dengan prediksi rating berkisar antara 3.81 hingga 3.99. Perbandingan dengan film-film yang sebelumnya diberi rating tinggi (4.5) oleh Pengguna 525, seperti Planet Earth (Dokumenter), Mad Max: Fury Road (Action|Adventure|Sci-Fi|Thriller), Kingsman: The Secret Service (Action|Adventure|Comedy|Crime), Robin Hood: Men in Tights (Komedi), dan True Lies (Action|Adventure|Comedy|Romance|Thriller), menunjukkan bahwa rekomendasi CF mencakup beragam genre. Contohnya termasuk Crime|Drama (Godfather, The), Adventure|Drama|War (Bridge on the River Kwai), Drama|Western (High Noon), Fantasy|Sci-Fi (Brazil), dan Comedy|Crime|Thriller (Snatch). Keberagaman genre ini mengindikasikan bahwa model CF mampu merekomendasikan film berdasarkan pola preferensi dari pengguna lain yang serupa, tidak hanya terpaku pada genre yang sama persis. Hal ini memungkinkan sistem untuk menawarkan discovery film yang lebih luas dan beragam di luar kebiasaan genre pengguna

## Evaluation
Dalam proyek ini, evaluasi dilakukan untuk kedua pendekatan: Collaborative Filtering (CF) dan Content-Based Filtering (CBF), menggunakan metrik dan metode yang sesuai dengan karakteristik masing-masing model.

### Evaluasi Content-Based Filtering (CBF)
Evaluasi untuk model Content-Based Filtering berfokus pada relevansi kualitatif rekomendasi yang dihasilkan, karena model ini tidak memprediksi rating numerik secara langsung.
- Metrix Evaluasi
    Untuk Content-Based Filtering, evaluasi dilakukan secara kualitatif melalui inspeksi langsung terhadap daftar rekomendasi yang dihasilkan. Ini bertujuan untuk memverifikasi apakah film-film yang direkomendasikan secara intuitif relevan dengan atribut konten (genre) dari film yang menjadi referensi.
- Formula & Cara Kerja:
    - TF-IDF (Term Frequency-Inverse Document Frequency): Bobot suatu genre (t) dalam film (d) dari korpus film (D) dihitung sebagai:
        $$\text{tf-idf}(t,d,D) = \text{tf}(t,d) \times \text{idf}(t,D)$$
        - **tf(t,d)** = Frekuensi suatu kata **t** dalam dokumen **d**.
        - **idf(t,D)** = Log dari rasio jumlah total dokumen **D** dengan jumlah dokumen yang mengandung kata **t**.
        
        Rumus IDF dihitung sebagai:
        $$\text{idf}(t,D) = \log\left(\frac{|D|}{|\{d \in D : t \in d\}|}\right)$$

    - Cosine Similarity: Metrik ini mengukur kemiripan antara dua film berdasarkan vektor TF-IDF mereka. Untuk dua vektor film
    $$\text{sim}(A, B) = \cos(\theta) = \frac{A \cdot B}{\|A\| \times \|B\|}$$

    **Keterangan:**
    - $$A$$ dan $$B$$: vektor fitur dari dua film yang ingin dibandingkan (misalnya, hasil dari TF-IDF)
    - $$A$$ $$\cdot$$ $$B$$: hasil dot product antara vektor $A$ dan $B$
    - $$\|A\|$$: norma (panjang) dari vektor $A$
    - $$\|B\|$$: norma (panjang) dari vektor $B$
    - $$\text{sim}(A, B)$$: nilai kemiripan kosinus antara dua film, berada dalam rentang $[-1, 1]$, tapi untuk TF-IDF umumnya bernilai $$[0, 1]$$
    
    **Interpretasi:**
    - Nilai mendekati 1 → Film sangat mirip secara konten
    - Nilai mendekati 0 → Film tidak mirip
    - Nilai negatif → Jarang terjadi pada TF-IDF, tapi secara teori berarti sangat tidak mirip
    
    Nilai berkisar antara 0 (tidak mirip) hingga 1 (sangat mirip). Semakin tinggi nilai kemiripan, semakin relevan rekomendasinya secara konten.

- **Hasil Metrik Evaluasi**

    ![alt text](https://github.com/andreaswd31/Sistem-Rekomendasi-Film/blob/main/CBF%20Rekom.png?raw=true)
  
    Hasil uji coba menunjukkan bahwa model Content-Based Filtering berhasil merekomendasikan film-film yang memiliki kemiripan konten sangat tinggi, dengan similarity score sebesar 1.00. Semua film yang direkomendasikan memiliki genre Drama|Thriller yang identik dengan film referensi 'Girl with the Dragon Tattoo, The (2011)'. Ini memvalidasi bahwa sistem secara efektif dapat merekomendasikan film berdasarkan atribut konten eksplisit, 

### Evaluasi Collaborative Filtering (CF)
Evaluasi model Collaborative Filtering berfokus pada akurasi prediksi rating numerik yang dihasilkan oleh model.

- **Metrik Evaluasi**
    - Metode Evaluasi: Untuk Collaborative Filtering, kinerja model diukur menggunakan Root Mean Squared Error (RMSE). Metrik ini sangat cocok karena model memprediksi nilai kontinu (rating). RMSE mengukur rata-rata magnitudo kesalahan dalam prediksi, dengan memberikan bobot lebih besar pada kesalahan yang lebih besar. 
    $$\text{RMSE} = \sqrt{ \frac{1}{n} \sum_{i=1}^{n} (\hat{y}_i - y_i)^2 }$$

    **Keterangan:**
    - $$n$$: jumlah total sampel (data prediksi)
    - $$\hat{y}_i$$: rating film hasil prediksi model pada data
    - $$y_i$$: rating aktual dari pengguna 
    - $$\text{RMSE}$$: rata-rata akar dari kuadrat error prediksi terhadap nilai aktual
    
    **Interpretasi:**
    - Semakin kecil nilai RMSE, maka prediksi model semakin mendekati rating yang sebenarnya.
    - Nilai RMSE umumnya berada dalam skala yang sama dengan skala rating (contoh: 0.5–5.0).
    - RMSE sensitif terhadap error besar karena menggunakan kuadrat perbedaan.
    
    
- **Hasil Proyek Berdasarkan Metrik Evaluasi**
Model Collaborative Filtering dilatih selama 20 epoch, dan kinerja dipantau menggunakan loss (Mean Squared Error) dan RMSE pada training dan validation set.
    - Visualisasi Hasil Pelatihan:
    Plot Loss

    ![alt text](https://github.com/andreaswd31/Sistem-Rekomendasi-Film/blob/main/LOS1.png?raw=true)
  
    Plot RMSE

    ![alt text](https://github.com/andreaswd31/Sistem-Rekomendasi-Film/blob/main/RMSE.png?raw=true)
    - Nilai RMSE Akhir:
    Final Training RMSE: 0.9269
    Final Validation RMSE: 0.9780
    - Analisis Hasil
    Dari plot dan nilai RMSE akhir, terlihat bahwa model Collaborative Filtering berhasil mengkonvergen selama pelatihan. Training Loss dan Validation Loss menurun tajam pada epoch awal dan kemudian stabil, dengan gap yang minim, menunjukkan bahwa model tidak mengalami overfitting yang signifikan.  Baik kurva loss maupun RMSE (untuk Training dan Validation) menunjukkan penurunan yang sangat cepat pada beberapa epoch awal, dan kemudian cenderung stabil pada nilai yang rendah. Ini mengindikasikan bahwa model belajar dengan efisien dan mencapai kinerja yang konsisten setelah beberapa iterasi. Nilai Final Training RMSE mencapai 0.9269 dan Final Validation RMSE mencapai 0.9780. Mengingat rentang rating asli (0.5 hingga 5.0), nilai Validation RMSE ini mengindikasikan bahwa rata-rata kesalahan prediksi model adalah sekitar 0.98 poin rating.

### Kesimpulan Evaluasi Menjawab Business Understanding
Evaluasi ini didasarkan pada hasil implementasi kedua pendekatan sistem rekomendasi: Content-Based Filtering (CBF) dan Collaborative Filtering (CF). Diperoleh sejumlah temuan yang merefleksikan keterkaitan langsung antara performa model dengan problem statements serta sejauh mana capaian terhadap tujuan yang telah ditetapkan dalam Business Understanding.

1. Relevansi Rekomendasi Berdasarkan Konten Film
- Problem Statement: Bagaimana sistem dapat merekomendasikan film berdasarkan atribut eksplisit seperti genre?
- Goal: Mengembangkan sistem rekomendasi berbasis kemiripan konten film.
- Evaluasi: 
Model Content-Based Filtering yang diimplementasikan berhasil dengan sangat efektif. Melalui penggunaan TF-IDF Vectorizer pada fitur genre film dan penghitungan Cosine Similarity, sistem dapat secara akurat mengidentifikasi film-film yang memiliki kemiripan konten yang tinggi. Hal ini terbukti dari hasil uji coba rekomendasi untuk film 'Girl with the Dragon Tattoo, The (2011)', di mana semua 10 film yang direkomendasikan memiliki genre Drama|Thriller yang identik dengan film referensi dan menunjukkan similarity score sebesar 1.00. Ini secara langsung memvalidasi kemampuan sistem untuk menghasilkan rekomendasi yang relevan dan dapat dijelaskan berdasarkan preferensi konten eksplisit pengguna.

2. Presisi Prediksi Rating Menggunakan Collaborative Filtering
- Problem Statement: Bagaimana presisi model dalam memprediksi rating film yang belum ditonton pengguna?
- Goal: Mengembangkan model ML untuk memprediksi rating numerik secara akurat.
- Evaluasi 
Model Collaborative Filtering berbasis Matrix Factorization (RecommenderNet) berhasil menunjukkan presisi yang baik dalam memprediksi rating numerik. Evaluasi menggunakan metrik Root Mean Squared Error (RMSE) pada validation set menunjukkan nilai RMSE sebesar 0.9780. Mengingat skala rating asli (0.5 hingga 5.0), nilai RMSE ini mengindikasikan bahwa rata-rata kesalahan prediksi model berada pada angka sekitar 0.98 poin rating. Ini merupakan akurasi yang memadai untuk sistem rekomendasi  terkait presisi prediksi rating. Kurva pelatihan model juga menunjukkan konvergensi yang stabil tanpa indikasi overfitting yang signifikan.

3. Kemampuan Sistem dalam Memberikan Rekomendasi Personal
- Problem Statement: Bagaimana sistem menyajikan daftar rekomendasi yang dipersonalisasi secara efektif?
- Goal: Menghasilkan daftar Top-N rekomendasi berdasarkan preferensi pengguna.
- Evaluasi 
Model Collaborative Filtering yang dilatih terbukti mampu menghasilkan rekomendasi film yang dipersonalisasi secara efektif. Demonstrasi uji coba untuk Pengguna ID 525 menghasilkan 10 rekomendasi film teratas dengan prediksi rating yang konsisten dengan rentang rating asli (misalnya, High Noon dengan prediksi 3.93 dan film-film lain di sekitar 3.99). Ini menunjukkan bahwa rekomendasi Collaborative Filtering mampu mencakup berbagai genre yang mungkin relevan dengan preferensi pengguna yang kompleks, tidak hanya terpaku pada kemiripan konten langsung. Proyek ini sukses tentang kemampuan sistem dalam menyajikan rekomendasi film yang dipersonalisasi berdasarkan pola preferensi historis pengguna.

## Daftar Pustaka
- Althbiti, A., Alshamrani, R., Alghamdi, T., Lee, S., & Ma, X. (2021). Addressing data sparsity in collaborative filtering based recommender systems using clustering and artificial neural network. 2021 IEEE 11th Annual Computing and Communication Workshop and Conference (CCWC), 0218–0227. https://doi.org/10.1109/CCWC51732.2021.9376008
- Fajriansyah, M., Adikara, P. P., & Widodo, A. W. (2021). Sistem Rekomendasi Film Menggunakan Content Based Filtering (Vol. 5, Issue 6). http://j-ptiik.ub.ac.id
- Fareed, A., Hassan, S., Belhaouari, S. B., & Halim, Z. (2023). A collaborative filtering recommendation framework utilizing social networks. Machine Learning with Applications, 14, 100495. https://doi.org/10.1016/j.mlwa.2023.100495
- Minaee, S., Kalchbrenner, N., Cambria, E., Nikzad, N., Chenaghlu, M., & Gao, J. (2022). Deep learning--based text classification: A comprehensive review. ACM Computing Surveys, 54(3), 1–40. https://doi.org/10.1145/3439726
- Mohammad, J. F., & Urolagin, S. (2022). Movie recommender system using content-based and collaborative filtering. 2022 IEEE IAS Global Conference on Emerging Technologies (GlobConET), 963–968. https://doi.org/10.1109/GlobConET53749.2022.9872515
- Romero Meza, L., & D’Urso, G. (2024). User’s dilemma: A qualitative study on the influence of netflix recommender systems on choice overload. Psychological Studies, 69(3), 349–367. https://doi.org/10.1007/s12646-024-00807-0
- Satapathy, S. C., Bhateja, V., & Das, S. (Ed.). (2019). Smart intelligent computing and applications: Proceedings of the second international conference on sci 2018, volume 1 (Vol. 104). Springer Singapore. https://doi.org/10.1007/978-981-13-1921-1
- Zakaria, M. M. A., Doheir, M., Akmaliah, N., & Yaacob, N. B. M. (2024). Infinite potential of ai chatbots: Enhancing user experiences and driving business transformation in e-commerce: case of palestinian e-commerce. Journal of Ecohumanism, 3(5), 216–229. https://doi.org/10.62754/joe.v3i5.3896
- Zhang, S., Yao, L., Sun, A., & Tay, Y. (2020). Deep learning based recommender system: A survey and new perspectives. ACM Computing Surveys, 52(1), 1–38. https://doi.org/10.1145/3285029
