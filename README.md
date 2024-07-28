# Laporan Proyek Machine Learning - Nama Anda

## Project Overview

Dalam era digital saat ini, konsumsi konten film semakin meningkat pesat. Seiring dengan itu, jumlah platform streaming dan film yang tersedia juga terus bertambah. Hal ini menyebabkan kelebihan informasi yang membuat pengguna kesulitan menemukan film yang sesuai dengan minat dan preferensi mereka. Kurangnya personalisasi dalam rekomendasi film juga menjadi masalah umum, di mana pengguna seringkali mendapatkan saran film yang tidak relevan.

Pengguna saat ini menginginkan pengalaman yang lebih personal dan efisien. Mereka tidak ingin menghabiskan waktu berjam-jam untuk mencari film yang tepat. Di sinilah peran sistem rekomendasi film menjadi sangat krusial.

Oleh karena itu, sebuah sistem rekomendasi menjadi sebuah kebutuhan yang sangat penting dimana sistem rekomendasi ini dapat menjadi sebuah solusi pada tingginya permintaan akan pengalaman pengguna yang lebih baik dan personal serta menjadi sebuah keunggulan yang kompetitif dalam persaingan platform streaming. 

[Sistem Rekomendasi Film Menggunakan Metode Collaborative Filtering dan K-Nearest Neighbors](https://ejournal.upi.edu/index.php/JATIKOM/article/view/33208/).

## Business Understanding

### Problem Statements

- Bagaimana cara mengatasi masalah kelebihan informasi pada platform streaming sehingga pengguna dapat dengan mudah menemukan film yang sesuai dengan preferensi mereka serta cara meningkatkan relevansi rekomendasi film yang diberikan oleh platform streaming agar sesuai dengan minat individu pengguna?

### Goals

- Mengembangkan sistem rekomendasi yang mampu memberikan saran film yang relevan dan personal, sehingga meningkatkan kepuasan dan pengalaman menonton film yang lebih menyenangkan bagi pengguna.   

### Solution statements
- Dalam mencapai tujuan yang diinginkan, proyek ini dibuat dengan dua pendekatan algoritma dalam menentukan sistem rekomendasi yang relevan bagi pengguna dalam meningkatkan pengalaman pengguna menonton film yaitu Content-Based Filtering dan Collaborative Filtering. 

## Data Understanding
Data yang digunakan pada proyek ini diambil dari data The Movie Database (TMDb) yang didapat dari hasil generate The Movie Database API dimana pada dataset ini berisikan tentang 5000 film yang disajikan dalam sebuah dataset format CSV dengan berbagai macam variabel seperti ID film, judul film, cast, crew, dan lain-lain. 

Dataset:
[TMDB 5000 Movie Dataset](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata/data) & [Data Rating Film](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset?select=ratings_small.csv)  

**Variabel-variabel pada TMDB 5000 Movie Dataset adalah sebagai berikut:**
- movie_id : merupakan id unik setiap film. 
- title : merupakan nama atau judul pada film.
- cast : merupakan variabel yang berisi informasi mengenai nama aktor dan karakter yang dimainkan.
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

**Exploratory Data Analysis (EDA)**

- Melakukan penggabungan data antara pada kolom id dalam dataset TMDB 5000 Movie Dataset. 
    
    Output:
    
        Index(['budget', 'genres', 'homepage', 'id', 'keywords', 'original_language',
        'original_title', 'overview', 'popularity', 'production_companies',
        'production_countries', 'release_date', 'revenue', 'runtime',
        'spoken_languages', 'status', 'tagline', 'title', 'vote_average',
        'vote_count', 'tittle', 'cast', 'crew'],
        dtype='object')

## Data Preparation

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

## Modeling
Pada tahap ini, proyek ini menerapkan 2 model rekomendasi antara lain sebagai berikut:

- **Model Development dengan Content-Based Filtering.** 

    Dalam model rekomendasi ini, fitur film (overview, cast, crew, keyword, dll) digunakan untuk menemukan kemiripannya dengan film lain. Kemudian film yang paling mungkin mirip akan direkomendasikan. 

    **Kelebihan**: 
        
    - *Personalisasi Tinggi:* Rekomendasi sangat disesuaikan dengan preferensi individu berdasarkan karakteristik item yang sudah pernah disukai.
    - *Tidak Membutuhkan Data Pengguna Lain:* Hanya membutuhkan informasi tentang item dan preferensi pengguna saat ini.
    - *Mudah Diterapkan:* Relatif mudah untuk diimplementasikan dan dijelaskan secara intuitif.
    - *Cocok untuk Item Baru:* Dapat merekomendasikan item baru yang belum memiliki rating dari pengguna lain.
    
    **Kekurangan**:

    - *Cold Start Problem:* Sulit memberikan rekomendasi kepada pengguna baru yang belum memiliki sejarah interaksi.
    - *Spektrum Rekomendasi Terbatas:* Rekomendasi cenderung terbatas pada item yang serupa dengan yang sudah pernah disukai, sehingga kurang mengeksplorasi item baru yang mungkin menarik.
    - *Tergantung Kualitas Metadata:* Kualitas metadata item sangat berpengaruh pada akurasi rekomendasi.

    **Hasil Rekomendasi**:

        # Mendapatkan rekomendasi film yang mirip dengan Spider-Man 3
        film_recommendations('Spider-Man 3')

        Output:

        159                   Spider-Man
        30                  Spider-Man 2
        20        The Amazing Spider-Man
        38      The Amazing Spider-Man 2
        1318                   The Thing
        4664                     Bronson
        1888             Eddie the Eagle
        1179             I Love You, Man
        196                     Megamind
        641                     Due Date
        Name: title, dtype: object


- **Model Development dengan Collaborative Filtering.** 

    Dalam sistem rekomendasi ini, model akan merekomendasikan film-film yang mirip dengan preferensi pengguna di masa lalu.

    **Kelebihan**:

    - *Rekomendasi Berdasarkan Kesamaan Preferensi:* Mampu menemukan pola yang lebih kompleks dalam preferensi pengguna, sehingga rekomendasi lebih akurat.
    - *Mengatasi Cold Start Problem:* Dapat memberikan rekomendasi kepada pengguna baru berdasarkan kesamaan dengan pengguna lain yang memiliki sejarah interaksi.
    - *Menemukan Item yang Tidak Terduga:* Mampu merekomendasikan item yang tidak memiliki kesamaan fitur dengan item yang sudah pernah disukai, namun mungkin menarik bagi pengguna.

    **Kekurangan**:

    - *Sparsity Problem:* Jika data interaksi pengguna sangat jarang, model akan kesulitan menemukan pola yang signifikan.
    - *Scalability:* Model bisa menjadi kompleks dan lambat untuk dilatih ketika jumlah pengguna dan item sangat besar.
    - *Tidak Menjelaskan Alasan Rekomendasi:* Sulit untuk menjelaskan mengapa suatu item direkomendasikan, sehingga kurang transparan.

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

## Evaluation

Tahap evaluasi model pada proyek Predictive Analytics ini menggunakan metrik Root Mean Squared Error (RMSE).

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

![Metriks RMSE](https://github.com/user-attachments/assets/86d9ee32-80b6-410d-8f1f-d2c0391d8118)

Berdasarkan metrik evaluasi diatas, model telah dilatih untuk menerapkan sistem rekomendasi dengan memberikan rekomendasi film berupa "Top 10 Rekomendasi Film" seperti yang telah dijabarkan pada output dalam tahap Modeling. 

**Kesimpulan**

*Dengan adanya dua pendekatan algoritma dalam membuat sistem rekomendasi yaitu Content-Based Filtering dan Collaborative Filtering dengan menggunakan metrik evaluasi Root Mean Squared Error (RMSE), ini telah menjawab problem statements dan goals yang telah dijabarkan sebelumnya dan membuktikan bahwa dua pendekatan algoritma ini dapat membuat dan mengembangkan sistem rekomendasi film yang mampu memberikan saran film yang relevan dan personal sehingga pengguna mendapatkan kepuasan dan pengalaman yang menyenangkan dalam menonton film. Solution statements ini dapat dibuktikan dengan adanya sistem rekomendasi yang memberikan "Top 10 Movie Recommendation" kepada pengguna.*
