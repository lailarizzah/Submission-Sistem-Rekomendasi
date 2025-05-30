# Laporan Proyek Machine Learning - Laila Rohmatul I'zzah

## Project Overview

Industri skincare di Indonesia mengalami pertumbuhan yang sangat pesat dalam beberapa tahun terakhir. Beragamnya produk dari berbagai merek membuat konsumen sering kali kesulitan menentukan pilihan yang tepat sesuai dengan jenis dan kondisi kulit mereka. Kesalahan dalam pemilihan produk tidak hanya menyebabkan hasil yang kurang efektif, tetapi juga berisiko menimbulkan efek samping seperti jerawat, iritasi, hingga kerusakan kulit dalam jangka panjang.

Salah satu penyebab utama masalah ini adalah minimnya pengetahuan konsumen mengenai kandungan bahan aktif dalam produk skincare. Banyak konsumen hanya mengandalkan rekomendasi dari influencer atau iklan, yang tidak selalu sesuai dengan kebutuhan pribadi mereka. Oleh karena itu, dibutuhkan sebuah solusi berupa sistem yang mampu memberikan rekomendasi produk secara otomatis, personal, dan relevan.

Solusi ini diwujudkan melalui pengembangan sistem rekomendasi cerdas berbasis data. Studi oleh Putri et al. (2024) menunjukkan bahwa sistem rekomendasi skincare dapat meningkatkan kepuasan pengguna secara signifikan, dengan tingkat presisi mencapai 0.776 dan skor CSAT sebesar 80% melalui pendekatan hybrid filtering [1].

Berangkat dari latar belakang tersebut, proyek ini bertujuan untuk membangun sistem rekomendasi produk skincare yang mampu membantu pengguna menemukan produk yang sesuai dengan preferensi mereka. Sistem akan dikembangkan dengan dua pendekatan utama, yaitu:

- Content-Based Filtering, yang merekomendasikan produk berdasarkan kemiripan fitur seperti kategori, harga, merek, dan nama produk.
- Collaborative Filtering, yang memanfaatkan data preferensi pengguna lain untuk menyarankan produk dengan pola kesukaan serupa.

Dengan adanya sistem ini, pengguna dapat lebih mudah menemukan produk yang sesuai tanpa harus mengalami proses trial-and-error yang berisiko bagi kesehatan kulit mereka.

**Referensi**

Yanisa Putri, K. S., I Made Agus Dwi Suarjaya, & Wayan Oger Vihikan. (2024). Sistem Rekomendasi Skincare Menggunakan Metode Content Based Filtering dan Collaborative Filtering. Decode: Jurnal Pendidikan Teknologi Informasi, 4(3), 764–774. https://doi.org/10.51454/decode.v4i3.601 

## Business Understanding

### Problem Statements

- **Konsumen kesulitan memilih produk skincare yang sesuai dengan kondisi dan kebutuhan kulit mereka.**
Banyaknya variasi produk dari berbagai merek menyebabkan pengguna seringkali kebingungan dalam menentukan produk yang tepat. Pemilihan yang keliru tidak hanya tidak efektif tetapi juga dapat menimbulkan masalah kulit seperti iritasi atau jerawat.
- **Konsumen cenderung memilih produk berdasarkan iklan atau rekomendasi influencer tanpa pemahaman kandungan dan kecocokan produk.**
Kurangnya literasi terhadap bahan aktif dalam produk skincare menyebabkan keputusan pembelian menjadi kurang informatif dan berisiko terhadap hasil yang tidak diharapkan.
- **Tidak adanya sistem yang memberikan rekomendasi produk skincare secara personal dan berbasis data.**
Saat ini, konsumen belum memiliki alat atau sistem yang mampu memberikan saran produk berdasarkan kebutuhan pribadi maupun pengalaman pengguna lain yang serupa.

### Goals
- **Membangun sistem rekomendasi yang mampu membantu pengguna menemukan produk skincare yang sesuai dengan preferensi dan kebutuhan kulit mereka.**
Sistem ini bertujuan meminimalisir kesalahan dalam memilih produk dan mengurangi ketergantungan pada rekomendasi yang tidak terverifikasi secara ilmiah.
- **Memberikan rekomendasi produk berdasarkan karakteristik produk dan preferensi pengguna melalui analisis konten.**
Sistem akan memanfaatkan informasi seperti kategori produk, merek, harga, dan fitur lainnya untuk menghasilkan saran produk yang mirip dengan produk yang disukai pengguna sebelumnya (content-based).
- **Mengintegrasikan pengalaman pengguna lain dalam sistem rekomendasi untuk meningkatkan relevansi hasil.**
Dengan memanfaatkan data rating dan ulasan pengguna lain, sistem dapat merekomendasikan produk berdasarkan pola perilaku pengguna yang memiliki preferensi serupa (collaborative filtering).

### Solution Approach
Untuk mencapai tujuan di atas, digunakan dua pendekatan utama:

#### 1. Content-Based Filtering
  - Sistem merekomendasikan produk yang memiliki fitur serupa dengan produk yang pernah disukai pengguna.
  - Pendekatan ini memanfaatkan informasi dari data seperti kategori, nama produk, harga, dan brand.
  - Implementasi dilakukan dengan mentransformasikan fitur-fitur produk menjadi vektor numerik menggunakan TfidfVectorizer, OneHotEncoder, dan StandardScaler, kemudian mengukur kemiripan antar produk dengan cosine similarity.

#### 2. Collaborative Filtering dengan SVD (Singular Value Decomposition)
  - Sistem memprediksi preferensi pengguna terhadap produk baru berdasarkan interaksi dari pengguna lain yang memiliki pola serupa.
  - Model ini mengurai matriks rating menjadi faktor-faktor laten pengguna dan item, kemudian mengalikan vektor-vektor ini untuk memprediksi rating produk yang belum pernah dilihat pengguna.
  - Algoritma ini diimplementasikan dengan library scikit-surprise, dan dipilih karena skalabilitas dan performanya yang baik pada dataset besar dan sparse.

## Data Understanding

### Ringkasan Dataset
Proyek ini menggunakan dua buah dataset utama yang berasal dari [Kagle Dataset Skincare Review](https://www.kaggle.com/datasets/hafidahmusthaanah/skincare-review), yang dikompilasi oleh Hafidah Mustha’anah. Dataset ini diambil dari situs Female Daily pada tanggal 18 September 2020, dengan konten ulasan ditulis dalam Bahasa Indonesia oleh konsumen lokal Indonesia. Produk-produk dalam dataset ini meliputi brand populer yang mencerminkan dinamika pasar skincare di Indonesia, di antaranya:

| Nama Brand             | Nama Brand                    | Nama Brand                     |
|-------------------------|-----------------------------|-----------------------------|
| AVOSKIN                 | Kiehl's                     | Pond's                      |
| Acnes                   | Kiss Me                     | Probio C                    |
| Avene                   | Klairs                      | Pulchra                     |
| Azarine Cosmetics       | Kleveru Organics            | Purbasari                   |
| Banila Co               | Kracie                      | Pyunkang Yul                |
| Benton                  | Krave Beauty                | QIANSOTO                    |
| Bioaqua                 | L'Oreal Paris               | RDL                         |
| Bioderma                | L.A. Girl                   | Raiku Beauty                |
| Biokos                  | LT PRO                      | RapidLash                   |
| Biore                   | LUSH                        | Ristra                      |
| Botanicabeauty.id       | La Mer                      | Roro Mendut                 |
| Breylee                 | La Roche-Posay              | Rose All Day Cosmetics      |
| Brunbrun Paris          | La Tulipe                   | SADA by Cathy Sharon        |
| Caladine                | Lacoco                      | SHILLS                      |
| Celebon                 | Laneige                     | SK-II                       |
| CeraVe                  | Larissa                     | Safi                        |
| Cetaphil                | Lionesse Gem Skin Care      | Sariayu                     |
| Charis                  | Luxcrime                    | Saripohatji                 |
| Citra                   | MY SCHEMING                 | Secret Key                  |
| Clean And Clear         | Madame Gie                  | Senka                       |
...

Dataset terbagi menjadi dua yang berisi informasi dan review produk skincare.

**Dataset 1** — Ulasan Produk Skincare (review_produk.csv)
Dataset ini berisi 8.646 baris data yang merekam interaksi pengguna terhadap berbagai produk skincare, termasuk ulasan, rating, serta kondisi kulit pengguna.

**Dataset 2** — Informasi Produk Skincare (info_produk.csv)
Dataset ini berisi 861 baris data yang mencakup informasi inti mengenai produk skincare yang tersedia, seperti nama, kategori, harga, dan rating rata-rata.

### Variabel pada Dataset
`review_produk.csv`

Dataset ini mencatat interaksi pengguna terhadap produk skincare. Terdiri dari 7 kolom:
1. Product : Nama produk yang diulas oleh pengguna. 
2. UserName : Nama atau ID pengguna yang memberikan ulasan.
3. SkinCond_Age : Kondisi kulit pengguna beserta usia, dalam format gabungan seperti “Oily,23” atau “Dry, 30”.
4. Recommend : Indikator apakah pengguna merekomendasikan produk tersebut (biasanya berisi “Yes” atau “No”).
5. PostDate : Tanggal ulasan diposting.
6. Review : Ulasan teks atau opini pengguna terhadap produk yang digunakan.
7. Rating : Skor penilaian terhadap produk, dalam skala 1–5.

`info_produk.csv`

Dataset ini mencatat metadata produk skincare. Terdiri dari 6 kolom:
1. Category : Kategori produk skincare, seperti Cleanser, Serum, Moisturizer, dll.
2. Merk : Nama merek atau brand dari produk (misalnya Wardah, Emina, Scarlett, dll).
3. Product : Nama lengkap produk skincare.
4. Price : Harga produk dalam satuan Rupiah.
5. OverallRating : Rata-rata rating produk dari seluruh pengguna.
6. Reviewer : Jumlah reviewer yang pernah memberikan ulasan terhadap produk tersebut.
7. 
**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
