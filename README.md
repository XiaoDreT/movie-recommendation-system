# Sistem Rekomendasi Film

## Project Overview

Dalam era digital saat ini, konsumsi konten film semakin meningkat pesat. Seiring dengan itu, jumlah platform streaming dan film yang tersedia juga terus bertambah. Hal ini menyebabkan kelebihan informasi yang membuat pengguna kesulitan menemukan film yang sesuai dengan minat dan preferensi mereka. Kurangnya personalisasi dalam rekomendasi film juga menjadi masalah umum, di mana pengguna seringkali mendapatkan saran film yang tidak relevan. **[1]**

Pengguna saat ini menginginkan pengalaman yang lebih personal dan efisien. Mereka tidak ingin menghabiskan waktu berjam-jam untuk mencari film yang tepat. Di sinilah peran sistem rekomendasi film menjadi sangat krusial.

Oleh karena itu, sebuah sistem rekomendasi menjadi sebuah kebutuhan yang sangat penting dimana sistem rekomendasi ini dapat menjadi sebuah solusi pada tingginya permintaan akan pengalaman pengguna yang lebih baik dan personal serta menjadi sebuah keunggulan yang kompetitif dalam persaingan platform streaming. 


Referensi: 

**[1]** [Agustian, E. R., Munir, D., & Nugroho, E. P. (2020). Sistem Rekomendasi Film Menggunakan Metode Collaborative Filtering dan K-Nearest Neighbors. Jurnal Aplikasi Dan Teori Ilmu Komputer, 3(1), 18–21](https://ejournal.upi.edu/index.php/JATIKOM/article/view/33208/).

## Business Understanding

### Problem Statements

- Bagaimana cara mengatasi masalah kelebihan informasi pada platform streaming sehingga pengguna dapat dengan mudah menemukan film yang sesuai dengan preferensi mereka serta cara meningkatkan relevansi rekomendasi film yang diberikan oleh platform streaming agar sesuai dengan minat individu pengguna?

### Goals

- Mengembangkan sistem rekomendasi yang mampu memberikan saran film yang relevan dan personal, sehingga meningkatkan kepuasan dan pengalaman menonton film yang lebih menyenangkan bagi pengguna.   

### Solution statements
- Dalam mencapai tujuan yang diinginkan, proyek ini dibuat dengan dua pendekatan algoritma dalam menentukan sistem rekomendasi yang relevan bagi pengguna dalam meningkatkan pengalaman pengguna menonton film yaitu Content-Based Filtering dan Collaborative Filtering. 

## Data Understanding
Data yang digunakan pada proyek ini diambil dari data The Movie Database (TMDb) yang didapat dari hasil generate The Movie Database API dimana pada dataset ini berisikan tentang 5000 film yang disajikan dalam sebuah dataset format CSV dengan berbagai macam variabel seperti ID film, judul film, cast, crew, dan lain-lain. 

Proyek ini menggunakan 2 dataset sebagai bahan dalam membuat sistem rekomendasi film ini, dimana 2 dataset ini digunakan untuk memprediksi peringkat atau preferensi yang akan diberikan pengguna pada suatu item.

Pada dataset TMDB 5000 Movie Dataset, jumlah data yang digunakan pada proyek ini dari dataset tersebut berjumlah **5000 data dengan matriks baris dan kolom sebanyak 5000 baris dan 24 kolom** yang berupa film-film yang akan diolah dalam membuat sebuah sistem rekomendasi. Kondisi data yang digunakan pada proyek ini masih terlihat **noise** untuk dilatih dalam model rekomendasi dengan adanya beberapa variabel yang masih memiliki **nilai null atau missing value**. 

Sedangkan, pada Dataset Rating Film, jumlah data yang digunakan berkisar **100.000 data rating yang dari 700 pengguna dalam 9000 film**. Dataset ini menjadi bahan perbandingan dengan fitur 'id' pada dataset TMDB 5000 Movie Dataset dalam membuat Model dengan Collaborative Filtering. Dataset ini **tidak memiliki nilai null atau missing value** dari setiap fitur atau variabelnya. Jumlah baris dan kolom pada dataset ini berkisar **100000 baris yang mewakili rating pengguna dan 4 kolom**. 

Dataset:
[TMDB 5000 Movie Dataset](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata/data) & [Dataset Rating Film](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset?select=ratings_small.csv)  

**Variabel-variabel pada TMDB 5000 Movie Dataset adalah sebagai berikut:**
- movie_id : merupakan id unik setiap film. 
- cast : merupakan variabel yang berisi informasi mengenai nama aktor dan karakter yang dimainkan.
- title: merupakan variabel yang berisi judul-judul film. 
- crew : merupakan variabel yang berisi informasi mengenai sutradara film, produser, dan kru lainnya. 
- budget : merupakan anggaran produksi film (dolar AS).
- genres : merupakan genre film seperti aksi, komedi, horror, dan sebagainya.
- homepage : merupakan URL halaman web resmi film.
- id : merupakan id unik setiap film. 
- keywords : merupakan kata kunci yang menggambarkan film.
- original_language : merupakan bahasa yang digunakan dalam pembuatan film.
- original_title : merupakan judul film dalam tulisan bahasa aslinya.
- title : merupakan judul film dalam distribusi internasional.
- overview: merupakan sinopsis singkat tentang film.
- popularity : merupakan skor popularitas film. 
- production_companies : merupakan kumpulan perusahaan yang terlibat dalam pembuatan film. 

**Variabel pada Dataset Rating Film adalah sebagai berikut:**
- userId : merupakan id unik setiap pengguna.
- movidId : merupakan id unik setiap film.
- rating : merupakan kumpulan rating atau penilaian film yang diberikan oleh pengguna dengan skala 0.5 stars - 5.0 stars.
- timestamp : merupakan variabel yang merepresentasikan detik sejak tengah malam Waktu Universal Terkoordinasi (UTC).

**Exploratory Data Analysis (EDA)**

- Melakukan penggabungan data pada kolom id dalam dataset TMDB 5000 Movie Dataset. 
    
    Penggabungan data pada kolom id digunakan untuk mendapatkan keseluruhan data yang ada pada file credits dan file movie pada dataset TMDB 5000 Movie Dataset. 

    Output:
    
        Index(['budget', 'genres', 'homepage', 'id', 'keywords', 'original_language',
        'original_title', 'overview', 'popularity', 'production_companies',
        'production_countries', 'release_date', 'revenue', 'runtime',
        'spoken_languages', 'status', 'tagline', 'title', 'vote_average',
        'vote_count', 'tittle', 'cast', 'crew'],
        dtype='object')

- **Melakukan pengecekan missing value pada dataset gabungan.** 

    Tahapan ini merupakan pengecekan nilai null pada variabel-variabel yang ada dalam dataset gabungan. Pengecekan ini merupakan hal yang krusial karena dalam membuat sistem rekomendasi, model rekomendasi bisa dilatih berdasarkan data yang lengkap dan akurat. 

    Output:
    
        budget                     0
        genres                     0
        homepage                3091
        id                         0
        keywords                   0
        original_language          0
        original_title             0
        overview                   3
        popularity                 0
        production_companies       0
        production_countries       0
        release_date               1
        revenue                    0
        runtime                    2
        spoken_languages           0
        status                     0
        tagline                  844
        title                      0
        vote_average               0
        vote_count                 0
        tittle                     0
        cast                       0
        crew                       0
        dtype: int64

## Data Preparation

- **Membersihkan missing value dan mengecek kembali missing value pada dataset gabungan.**

    Melakukan pembersihan missing value pada dataset merupakan suatu tahapan yang diperlukan agar data yang akan dilatih model pada sistem rekomendasi memiliki data yang lengkap dan akurat. Pembersihan missing value ini dilakukan agar tidak akan menimbulkan noise dalam data sehingga model yang akan dilatih dapat fokus pada informasi yang relevan. 

    Output:

        budget                  0
        genres                  0
        homepage                0
        id                      0
        keywords                0
        original_language       0
        original_title          0
        overview                0
        popularity              0
        production_companies    0
        production_countries    0
        release_date            0
        revenue                 0
        runtime                 0
        spoken_languages        0
        status                  0
        tagline                 0
        title                   0
        vote_average            0
        vote_count              0
        tittle                  0
        cast                    0
        crew                    0
        dtype: int64

#### Data Preparation untuk Pelatihan Model Content-Based Filtering:

- **Mengecek fitur 'overview' pada dataset gabungan.**

    Melakukan pengecekan fitur overview untuk dilakukan vektorisasi. 

        Output:
        0    In the 22nd century, a paraplegic Marine is di...
        1    Captain Barbossa, long believed to be dead, ha...
        2    A cryptic message from Bond’s past sends him o...
        3    Following the death of District Attorney Harve...
        4    John Carter is a war-weary, former military ca...
        Name: overview, dtype: object

- **Menghitung vektor pada setiap 'overview' dengan menggunakan teknik Term Frequency-Inverse Document Frequency (TF-IDF).** 
    
    Ini akan memberikan sebuah matriks dimana setiap kolom mewakili sebuah kata dalam overview kosakata (semua kata yang muncul di setidaknya satu dokumen) dan setiap baris mewakili sebuah film, seperti sebelumnya, hal ini dilakukan untuk mengurangi pentingnya kata-kata yang sering muncul di overview plot dan oleh karena itu, pentingnya kata-kata tersebut dalam penghitungan nilai kemiripan akhir.

- **Membuat reverse map dari indeks dan judul film.**

    Hal ini merupakan tahapan yang bertujuan untuk memetakan judul film pada indeks aslinya. 

#### Data Preparation untuk Pelatihan Model Collaborative Filtering:
- **Menginisialisasi dataframe dari dataset rating.** 

    Melakukan inisialisasi dataframe yang diambil dari dataset rating untuk pembuatan model rekomendasi dengan menyandikan fitur, melakukan mapping, dan membagi dataset menjadi data train dan data validasi.

- **Menyandikan data-data yang ada pada fitur 'userId' dan fitur 'movieId' ke dalam indeks integer.**

    Hal ini bertujuan untuk mengubah data-data pada fitur userId dan movieId yang bertipe object menjadi data numerik agar model dapat dengan mudah mempelajari setiap data. 

        Output encoding fitur userId:
        list userId:  [1, 2, 3, 4, 5, dst]
        encoded userId :  {1: 0, 2: 1, 3: 2, 4: 3, 5: 4, dst}
        encoded angka ke userId:  {0: 1, 1: 2, 2: 3, 3: 4, 4: 5, 5: 6, dst}

        Output encoding fitur movieId:
        list movieId:  [31, 1029, 1061, 1129, 1172, dst]
        encoded movieId :  {31: 0, 1029: 1, 1061: 2, 1129: 3, 1172: 4, dst}
        encoded angka ke movieId:  {0: 31, 1: 1029, 2: 1061, 3: 1129, 4: 1172, dst}

- **Melakukan mapping pada userId dan movieId ke dataframe yang berkaitan yaitu 'user' dan 'movie'.** 

    Mapping dilakukan dengan memetakan userId dan movieId ke dalam dataframe yang berkaitan seperti 'user' dan 'movie' untuk mempermudah pengenalan terhadap setiap fitur tersebut. 

- **Mengecek jumlah user, jumlah movie, nilai minimum rating, dan nilai maksimum rating.**

    Melakukan pengecekan terhadap jumlah user, jumlah movie, nilai minimum rating, dan nilai maksimum rating seperti output berikut:

        Output:
        671
        9066
        Number of User: 671, Number of Movie: 9066, Min Rating: 0.5, Max Rating: 5.0

## Modeling
Pada tahap ini, proyek ini menerapkan 2 model rekomendasi antara lain sebagai berikut:

### Model Development dengan Cosine Similarity

#### Dalam model rekomendasi ini, fitur film (overview, cast, crew, keyword, dll) digunakan untuk menemukan kemiripannya dengan film lain. Kemudian film yang paling mungkin mirip akan direkomendasikan.

**Proses dan tahapan pembuatan model dengan cosine similarity:**

    1. Melakukan pengecekan pada fitur 'overview' pada dataset gabungan. 

    2. Menghitung vektor pada setiap 'overview' dengan menggunakan teknik Term Frequency-Inverse Document Frequency (TF-IDF). 
       Ini akan memberikan sebuah matriks dimana setiap kolom mewakili sebuah kata dalam overview kosakata (semua kata yang muncul di setidaknya satu dokumen) dan 
       setiap baris mewakili sebuah film, seperti sebelumnya, hal ini dilakukan untuk mengurangi pentingnya kata-kata yang sering muncul di overview plot dan 
       oleh karena itu, pentingnya kata-kata tersebut dalam penghitungan nilai kemiripan akhir.

       Output ukuran matriks setelah melakukan vektorisasi dengan TF-IDF:

       (4803, 20978)

    3. Cosine Similarity. 
        Digunakan untuk menghitung kuantitas numerik yang menunjukkan kemiripan antara dua film dan menggunakan skor kemiripan kosinus karena 
        skor ini tidak bergantung pada besaran dan relatif mudah dan cepat untuk dihitung.

        Output:

        array([[1.        , 0.        , 0.        , ..., 0.        , 0.        ,
                   0.        ],
               [0.        , 1.        , 0.        , ..., 0.02160533, 0.        ,
                   0.        ],
               [0.        , 0.        , 1.        , ..., 0.01488159, 0.        ,
                   0.        ],
               ...,
               [0.        , 0.02160533, 0.01488159, ..., 1.        , 0.01609091,
                   0.00701914],
               [0.        , 0.        , 0.        , ..., 0.01609091, 1.        ,
                   0.01171696],
               [0.        , 0.        , 0.        , ..., 0.00701914, 0.01171696,
                   1.        ]])

    4. Membuat reverse map dari index dan judul film. Hal ini bertujuan untuk memetakan judul film ke dalam indeks aslinya dalam dataset gabungan.

    5. Membuat sebuah function untuk mendapatkan rekomendasi dengan mengembalikan data berupa top 10 film yang paling mirip dengan indeks aslinya. 

    6. Mendapatkan rekomendasi film. 

**Parameter Cosine Similarity:**

 
**Hasil Rekomendasi:**

    # Mendapatkan rekomendasi film yang mirip dengan The Dark Knight Rises
    film_recommendations('The Dark Knight Rises')

    Output:

    65                              The Dark Knight
    299                              Batman Forever
    428                              Batman Returns
    1359                                     Batman
    3854    Batman: The Dark Knight Returns, Part 2
    119                               Batman Begins
    2507                                  Slow Burn
    9            Batman v Superman: Dawn of Justice
    1181                                        JFK
    210                              Batman & Robin
    Name: title, dtype: object

**Kelebihan**: 
    
- Intuitif dan Mudah Dipelajari: Konsep cosine similarity cukup mudah dipahami, yaitu mengukur kemiripan antara dua vektor berdasarkan sudut antara keduanya. Ini membuatnya menjadi model yang populer dan sering digunakan.
- Efisien Komputasi: Perhitungan cosine similarity relatif cepat, terutama untuk dataset yang besar.
- Performa Baik untuk Data Sparse: Model ini bekerja dengan baik pada data yang memiliki banyak nilai nol (sparse), seperti matriks rating film di mana sebagian besar pengguna belum memberikan rating untuk semua film.
- Menangkap Kemiripan Berdasarkan Pola: Cosine similarity tidak hanya melihat nilai rating yang sama, tetapi juga pola keseluruhan dari rating yang diberikan oleh pengguna. Misalnya, dua pengguna yang memberikan rating tinggi pada film-film genre yang sama akan dianggap memiliki kesamaan yang tinggi.

**Kekurangan**:

- Tidak Memperhatikan Nilai Absolut Rating: Model ini hanya memperhatikan arah vektor, bukan panjangnya. Artinya, perbedaan besar dalam nilai rating (misalnya, rating 1 vs 5) dianggap sama pentingnya dengan perbedaan kecil (misalnya, rating 4 vs 5).
- Tidak Mempertimbangkan Konteks: Cosine similarity tidak mempertimbangkan konteks di mana rating diberikan. Misalnya, seorang pengguna yang baru saja menonton banyak film aksi mungkin akan memberikan rating yang lebih tinggi untuk film aksi berikutnya, terlepas dari kualitas sebenarnya dari film tersebut.
- Asumsi Kemerdekaan Fitur: Model ini mengasumsikan bahwa setiap fitur (dalam hal ini, setiap film) adalah independen. Padahal, dalam kenyataannya, film-film seringkali memiliki keterkaitan (misalnya, film sekuel, film yang dibintangi aktor yang sama).
- Sensitif terhadap Normalisasi: Hasil perhitungan cosine similarity dapat sangat dipengaruhi oleh cara data dinormalisasi.

### Model Development dengan Keras (RecommenderNet) 

#### Dalam sistem rekomendasi ini, model akan merekomendasikan film-film yang mirip dengan preferensi pengguna di masa lalu.

**Proses dan tahapan pembuatan model dengan collborative filtering:**
    
    1. Mengacak dataset. Hal ini dilakukan agar distribusinya menjadi random. 

    2. Membagi dataset menjadi data train dan data validasi. Pembagian dataset menjadi data train dan data validasi dilakukan dengan rasio 80% data train dan 20% data validasi. 

    3. Membuat class RecommenderNet dengan Keras Model Class. 

       Parameter yang digunakan pada pembuatan Model Keras (RecommenderNet):

       - num_users, num_movie: Jumlah pengguna dan film dalam dataset.
       - embedding_size: Dimensi ruang embedding.
       - embeddings_initializer: Inisialisasi bobot embedding.
       - embeddings_regularizer: Regularisasi untuk mencegah overfitting.

    4. Melakukan proses compile pada model yang telah dibuat.
    
       Model ini menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation. 

    5. Melakukan training pada model rekomendasi.

       Output: 

       Epoch 90/100
       10001/10001 [==============================] - 56s 6ms/step - loss: 0.5793 - root_mean_squared_error: 0.1813 - val_loss: 0.6059 - val_root_mean_squared_error: 0.2071
       Epoch 91/100
       10001/10001 [==============================] - 56s 6ms/step - loss: 0.5795 - root_mean_squared_error: 0.1816 - val_loss: 0.6059 - val_root_mean_squared_error: 0.2070
       Epoch 92/100
       10001/10001 [==============================] - 51s 5ms/step - loss: 0.5794 - root_mean_squared_error: 0.1815 - val_loss: 0.6058 - val_root_mean_squared_error: 0.2069
       Epoch 93/100
       10001/10001 [==============================] - 55s 5ms/step - loss: 0.5794 - root_mean_squared_error: 0.1815 - val_loss: 0.6059 - val_root_mean_squared_error: 0.2069
       Epoch 94/100
       10001/10001 [==============================] - 50s 5ms/step - loss: 0.5794 - root_mean_squared_error: 0.1814 - val_loss: 0.6056 - val_root_mean_squared_error: 0.2068
       Epoch 95/100
       10001/10001 [==============================] - 52s 5ms/step - loss: 0.5791 - root_mean_squared_error: 0.1811 - val_loss: 0.6055 - val_root_mean_squared_error: 0.2065
       Epoch 96/100
       10001/10001 [==============================] - 52s 5ms/step - loss: 0.5795 - root_mean_squared_error: 0.1816 - val_loss: 0.6059 - val_root_mean_squared_error: 0.2070
       Epoch 97/100
       10001/10001 [==============================] - 51s 5ms/step - loss: 0.5795 - root_mean_squared_error: 0.1814 - val_loss: 0.6062 - val_root_mean_squared_error: 0.2073
       Epoch 98/100
       10001/10001 [==============================] - 50s 5ms/step - loss: 0.5792 - root_mean_squared_error: 0.1813 - val_loss: 0.6061 - val_root_mean_squared_error: 0.2072
       Epoch 99/100
       10001/10001 [==============================] - 51s 5ms/step - loss: 0.5792 - root_mean_squared_error: 0.1812 - val_loss: 0.6064 - val_root_mean_squared_error: 0.2074
       Epoch 100/100
       10001/10001 [==============================] - 55s 6ms/step - loss: 0.5796 - root_mean_squared_error: 0.1817 - val_loss: 0.6066 - val_root_mean_squared_error: 0.2076

    6. Mendapatkan rekomendasi film berupa "Top 10 Movies Recommendation". 


**Hasil Rekomendasi**:

    Output:

    9/9 [==============================] - 0s 2ms/step
    Showing recommendations for users: 500
    ===========================
    Movie with high ratings from user
    --------------------------------
    --------------------------------
    Top 10 movie recommendation
    --------------------------------
    Spider-Man 3
    Speed Racer
    Ice Age: The Meltdown
    Changeling
    You, Me and Dupree
    Love in the Time of Cholera
    1408
    The Helpers
    Before Sunset
    Orgazmo

**Kelebihan**:

- Fleksibilitas: Model keras menawarkan fleksibilitas yang tinggi dalam desain arsitektur. Anda dapat dengan mudah menggabungkan berbagai lapisan (layer) seperti embedding, fully connected, dan convolutional untuk menangkap berbagai pola kompleks dalam data.
- Kinerja Tinggi: Dengan memanfaatkan kekuatan komputasi GPU dan library deep learning seperti TensorFlow atau Keras, model keras dapat melatih model yang besar dan kompleks dalam waktu yang relatif singkat.
- Penanganan Data Sparse: Model keras dapat menangani data yang sparse dengan baik, seperti matriks rating film yang memiliki banyak nilai yang hilang. Teknik seperti embedding layer dapat membantu mengatasi masalah ini.
- Pembelajaran Fitur Otomatis: Model keras dapat belajar fitur-fitur laten yang relevan secara otomatis dari data, tanpa perlu melakukan feature engineering secara manual.
- Integrasi dengan Informasi Tambahan: Model keras dapat dengan mudah mengintegrasikan informasi tambahan seperti genre film, aktor, atau profil pengguna untuk meningkatkan kualitas rekomendasi.

**Kekurangan**:

- Kompleksitas: Model keras seringkali membutuhkan lebih banyak data dan sumber daya komputasi dibandingkan model yang lebih sederhana seperti matrix factorization.
- Overfitting: Model keras rentan terhadap overfitting, terutama jika data pelatihan tidak cukup banyak atau jika model terlalu kompleks. Teknik regularisasi seperti dropout dan L1/L2 regularization dapat membantu mengatasi masalah ini.
- Interpretasi: Model keras yang kompleks sulit diinterpretasi, sehingga sulit untuk memahami alasan di balik rekomendasi yang diberikan.
- Waktu Pelatihan: Pelatihan model keras dapat memakan waktu yang cukup lama, terutama untuk dataset yang besar.
- Hyperparameter Tuning: Menentukan nilai hyperparameter yang optimal untuk model keras dapat menjadi tugas yang menantang dan memakan waktu.

## Evaluation

### Evaluasi Model Content-Based Filtering

Tahap evaluasi model ini menggunakan metrik presisi (precision metric).

**Penjelasan Metrik Evaluasi**
Metrik Presisi (Precision Metric) melakukan perbandingan antara rekomendasi film yang relevan dan rekomendasi yang diberikan sistem. Untuk jelasnya, bisa diliat rumus daripada Presisi Sistem Rekomendasi berikut ini:  

![Rumus Presisi](https://github.com/user-attachments/assets/83777201-c68b-45dd-a23d-5dc85e2df07d)

Jika dilihat dari output hasil rekomendasi yang diberikan sistem rekomendasi pada Modeling Content-Based Filtering, dimana 10 film yang direkomendasikan, terdapat 8 film yang similar (mirip) dengan indeks film aslinya ("The Dark Knight Rises"). Jika diformulakan dengan rumus presisi akan mendapatkan hasil sebagai berikut:

    film yang relevan/rekomendasi film yang diberikan sistem = 8/10. 

Presisi yang didapat adalah 80%. 

### Evaluasi Model Collaborative Filtering

Tahap evaluasi model pada proyek Sistem Rekomendasi ini menggunakan metrik Root Mean Squared Error (RMSE). 

**Penjelasan Metrik Evaluasi**

Root Mean Squared Error (RMSE):

Root Mean Squared Error (RMSE) adalah metrik evaluasi yang umum digunakan untuk mengukur seberapa baik suatu model prediksi, termasuk model sistem rekomendasi, dalam memprediksi nilai numerik. Dalam konteks sistem rekomendasi, RMSE digunakan untuk mengukur perbedaan antara rating yang diprediksi oleh model dengan rating aktual yang diberikan pengguna. Berikut adalah cara kerja dan formula RMSE:

- Hitung Selisih: Untuk setiap item yang diberi rating oleh pengguna, hitung selisih antara rating yang diprediksi oleh model dengan rating aktual yang diberikan pengguna.
- Kuadratkan Selisih: Kuadratkan setiap selisih untuk memberikan bobot yang lebih besar pada kesalahan prediksi yang lebih besar.
- Hitung Rata-rata: Hitung rata-rata dari semua kuadrat selisih.
- Akar Kuadrat: Ambil akar kuadrat dari rata-rata kuadrat selisih. Hasilnya adalah RMSE.

![Rumus RMSE](https://github.com/user-attachments/assets/a6c07ba0-2e0e-4829-b08d-44c34dae4d6b)

Dimana: 
- yi: Rating aktual dari pengguna i untuk item j
- ŷi: Rating yang diprediksi oleh model untuk pengguna i dan item j
- n: Jumlah pasangan pengguna-item

**Visualisasi Metrik Root Mean Squared Error (RMSE)**

![Metrik RMSE](https://github.com/user-attachments/assets/86d9ee32-80b6-410d-8f1f-d2c0391d8118)

Proses training model cukup smooth dan model konvergen pada epochs sekitar 100. Dari proses ini, dapat diperoleh nilai error akhir sebesar sekitar 0.18 dan error pada data validasi sebesar 0.21. Nilai tersebut cukup bagus untuk sistem rekomendasi dalam memberikan rekomendasi film kepada pengguna. 

### Kesimpulan

*Dengan adanya dua pendekatan algoritma dalam membuat sistem rekomendasi yaitu Content-Based Filtering dan Collaborative Filtering dengan menggunakan metrik evaluasi Precision dan Root Mean Squared Error (RMSE), ini telah menjawab problem statements dan goals yang telah dijabarkan sebelumnya dan membuktikan bahwa dua pendekatan algoritma ini dapat membuat dan mengembangkan sistem rekomendasi film yang mampu memberikan saran film yang relevan dan personal sehingga pengguna mendapatkan kepuasan dan pengalaman yang menyenangkan dalam menonton film. Solution statements ini dapat dibuktikan dengan adanya sistem rekomendasi yang memberikan "Top 10 Movie Recommendation" kepada pengguna.*
