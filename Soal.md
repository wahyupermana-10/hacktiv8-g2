_Graded Challenge ini dibuat guna mengevaluasi pembelajaran pada Hacktiv8 Data Science Fulltime Program khususnya pada Mathematics and Statistics._

---

## Dataset Description

* Pada graded challenge ini, data diakses menggunakan `bigquery-public-data` pada Google Cloud Big Query.
* Buka [Google Cloud Platform](https://console.cloud.google.com/), masuk ke BigQuery, lalu buka tab `bigquery-public-data` atau klik link [berikut](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=samples&page=dataset&_ga=2.245085957.1471931019.1642739417-486643658.1638156099) atau link [berikut](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=austin_waste&t=waste_and_diversion&page=table) untuk langsung menuju ke tabel.

```{attention}
Perhatikan petunjuk penggunaan dataset!
```

1. Gunakan tabel `waste_and_diversion` pada dataset `austin_waste`.
2. Buatlah query dengan kriteria sebagai berikut:
   - Pilih **HANYA** kolom `report_date`,`load_time`, `load_type`, `load_weight`, `dropoff_site`.

   - Ambil data tahun 2021 saja (data hanya sampai tanggal 9 Juli 2021).

3. Simpan dataset dalam bentuk csv, dengan nama `h8dsft_P0GC2_<nama-students>.csv`.
4. Salin query yang telah dibuat di Google Cloud Platform, tulislah pada bagian atas notebook!
5. Tampilkan `head` dan `tail` dari dataset pada notebook!


## Assignment Problems

Kamu adalah anggota tim Data Science di Austin Smart City dan sedang mengerjakan projek analisa sistem pembuangan dan pengelolaan sampah di kota tersebut. Sebagai anggota tim, berdasarkan data yang tersedia, coba analisa data tersebut menggunakan statistik deskriptif dan inferensial, serta berikan insight kepada pemerintah kota Austin mengenai kondisi sistem pembuangan dan pengelolaan sampah. Gunakan guideline/langkah berikut untuk mempermudah kamu dalam menganalisa.

### Problem 1 (Stats)

1. Sebelum melakukan perhitungan dan analisa statistik, lakukan pembersihan data terlebih dahulu. Pastikan tidak ada missing value, dsb.

2. Selanjutnya, lakukan eksplorasi data sederhana guna mengetahui dan mengenali data yang kamu punya. Kamu bisa lakukan hal-hal berikut untuk mengeksplorasi data kamu.
  - Melihat rentang waktu pengambilan data
  - Ada apa saja tipe load sampah di kota Austin berdasarkan data
  - Mengetahui tempat pembuangan sampah ada dimana saja
  - dsb.

3. Berdasarkan central tendency (mean, median, dan modus) untuk masing-masing site, insight/informasi apa yang bisa kamu sampaikan kepada pemerintah kota? (**Caution:** Jangan gunakan pd.DataFrame.describe())

4. Pilih site yang paling menarik perhatian kamu, dan berikan alasannya.

5. Gunakan site yang kamu pilih untuk dicek apakah data `load_weight` ada outlier atau tidak. *Gunakan teknik yang tepat sesuai dengan distribusi dari datanya!*. Jika iya, berapa persen jumlah outliernya? dan bandingkan central tendency data yang telah dikeluarkan outliernya dengan yang belum (hasil dari perhitungan nomor 3).

6. Gunakan site yang telah kamu pilih untuk dihitung range, variance, dan standar deviasi untuk data `load_weight`. Berikan insight dari hasil perhitunganmu kepada pemerintah kota (`Pastikan data yang digunakan adalah data yang sudah dibersihkan dari outlier`).

7. Pemerintah kota berencana menambah site baru. Berikan analisa dan saran terkait berapa kapasitas penampungan di site baru berdasarkan perhitungan `confidence interval`. Data apa yang kamu gunakan, apakah hanya dari satu site saja atau dari keseluruhan site?

8. Buatlah `analisa uji hipotesis` dari data tersebut dari data yang tersedia (kasusnya dibebaskan). Definisikan H0 dan H1 nya serta lakukan perhitungan menggunakan t-test yang sesuai dengan hipotesis kamu. Tulis kesimpulan dari hasil perhitunganmu kepada pemerintah kota (**Ingat!** pemerintah kota tidak mengerti p-value, hipotesis diterima/tidak diterima, jadi gunakan bahasa yang lebih manusiawi!).


**Jawab pertanyaan berikut untuk mengasah pemahaman konsepmu!**

1. Teknik apa yang kamu pilih untuk handling outlier? jelaskan alasannya!
2. Apa konsep dibalik confidence interval sehingga kita dapat menggunakannya untuk menyelesaikan langkah pada nomor 7?
3. Jelaskan jenis uji hipotesis apa yang kamu terapkan dan mengapa?

### Problem 2 (Math/Calculus)

Pada permasalahan yang sama, pemerintah ingin tau berapa banyak load sampah dalam kg di kota Austin di hari berikutnya (10 Juli 2021). Dalam hal ini, pemerintah menginginkan kamu melakukan forecasting untuk memprediksi nilai di masa depan. Ada banyak teknik forecasting yang bisa dilakukan tapi kamu tidak perlu khawatir, kita akan menggunakan yang metode yang sangat sederhana yaitu menggunakan rumus kecepatan.

Asumsikan bahwa laju penambahan sampah tiap harinya dapat ditulis menggunakan rumus berikut:
<img src="https://latex2png.com/pngs/d095b902113a1ef68d07fd786e4be428.png"></img>

dimana `1` notasi hari ini dan `0` notasi hari kemarin.

Jika kita ingin memprediksi jumlah load sampah hari esok maka bisa digunakan rumus:

<img src="https://latex2png.com/pngs/50dc63299a1860b10a15346a9ca3a42e.png"></img>

Dimana `v` akan dihitung nilainya menggunakan turunan pertama dari data `load_weight` yang sebelumnya harus di-group-by berdasarkan `report_date` dan jangan lupa setelah itu `report_date` harus diurutkan dari tanggal terkecil hingga terbesar. `Δt` **bernilai 1** karena hanya ingin memprediksi nilai di satu hari kedepan.

**Catatan tambahan**: Untuk menghitung turunan, harus ditentukan terlebih dahulu sumbu x dan y nya. Jadikan `load_weight` sebagai sumbu y dan untuk sumbu x, dapat gunakan index dataframe hasil groupby jika indeksnya berupa nomor urut dari 0 hingga N-1. Jika tidak, bisa buat menggunakan `range()`.

Gunakan hasil turunan pertama pada baris terakhir dari data untuk digunakan sebagai `v`.

**Jawab pertanyaan berikut untuk mengasah pemahaman konsepmu!**

1. Untuk menghitung turunan pertama dapat digunakan metode simbolik dan numerik, untuk kasus ini, teknik apa yang kamu gunakan?
2. Apakah kamu membutuhkan fungsi matematis untuk menghitung turunannya? (ya/tidak) berikan alasanmu!
3. Berapa load weight yang kamu perkirakan di hari esok (10 Juli 2021)?


### Poin Analisis

Tarik benang merah dan kesimpulan dari perhitungan dan analisa yang kamu telah lakukan di langkah-langkah sebelumnya dari kedua problem. Ceritakan kesimpulanmu kepada pemerintah kota dan **hindari** bahasa teknis yang tidak dimengerti oleh orang yang bukan data scientist!


## Assignment Submission

- Simpan assignment pada sesi ini dengan nama `h8dsft_P0W2_<nama-student>.ipynb`, misal `h8dsft_P0W2_raka_ardhi.ipynb`.
- Push Assigment yang telah kalian buat ke akun Github masing-masing student.

## Assignment Objectives

*Graded Challenge 3* ini dibuat guna mengevaluasi Statistics Descriptive dan Inferential sebagai berikut:

- Mampu memperoleh data menggunakan BigQuery
- Mampu melakukan pemrosesan data sebelum melakukan perhitungan
- Mampu menerapkan konsep statistics descriptive dan inferential pada suatu permasalahan
- Mampu memahami konsep statistics descriptive dan inferential

---

## Assignment Rubrics

### Code Review

| Criteria | Meet Expectations | Points |
| --- | --- | --- |
| Data Retrieve | Mampu memperoleh data menggunakan SQL BigQuery, melingkupi kesesuaian kode dengan tabel yang dihasilkan | 5 pts |
| Data Preprocessing | Mampu memroses data sampai siap digunakan dalam perhitungan | 4 pts |
| Data Exploratory | Mampu melakukan eksplorasi data sederhana | 4 pts |
| Central Tendency | Mampu menerapkan perhitungan mean, median, modus di kode (2 pts each). `Jika menggunakan .describe(), tidak akan mendapat nilai` | 6 pts |
| Outlier Handling | Mampu menerapkan pendeteksian dan handling outlier di kode | 3 pts |
| Measure of Variance | Mampu menerapkan perhitungan range, variance, dan standar deviasi di kode (2 pts each) | 6 pts |
| Confidence Interval | Mampu menerapkan perhitungan confidence interval pada kode | 3 pts |
| Hypothesis Testing | Mampu mendefinisikan H0 dan H1 serta menerapkan perhitungan uji hipotesis di kode| 4 pts |
|Mathematics| Mampu menerapkan/menghitung turunan menggunakan code | 2 pts |


### Concepts

| Criteria | Meet Expectations | Points |
| --- | --- | --- |
| Statistics | Mampu menjawab pertanyaan dengan singkat, jelas, dan padat serta sesuai dengan konsep dan logika yang ada (5 each) | 15 pts |
| Mathematics | Mampu menjawab pertanyaan dengan singkat, jelas, dan padat serta sesuai dengan konsep dan logika yang ada (5 each) | 15 pts |


### Analysis

| Criteria | Meet Expectations | Points |
| --- | --- | --- |
| Central Tendency | Mampu memberikan kesimpulan/insight dari hasil perhitungan central tendency | 5 pts |
| Outlier Analysis | Mampu memberikan kesimpulan/insight dari hasil pendeteksian/handling outlier | 5 pts |
| Variance | Mampu memberikan kesimpulan/insight dari hasil perhitungan range, variance, dan standar deviasi | 5 pts |
| Confidence Interval | Mampu memberikan kesimpulan/insight/saran dari hasil perhitungan confidence interval | 5 pts |
| Hypothesis Testing | Mampu memberikan kesimpulan/insight/saran dari hasil perhitungan hypothesis testing | 5 pts |
| Overall Analysis/Poin Analisis | Mampu menarik kesimpulan dari seluruh perhitungan dan analisa yang dilakukan serta menggunakan bahasa yang dipahami orang awam| 10 pts |


### Readability

| Criteria | Meet Expectations | Points |
| --- | --- | --- |
| Tertata Dengan Baik | Semua baris kode terdokumentasi dengan baik dengan menggunakan Markdown untuk penjelasan kode. | 5 pts |

---

```
Total Points : 100
```

## Score Reduction

Pengurangan poin akan diberlakukan jika Student terlambat mengumpulkan tugas yang telah diberikan. Adapun besarnya pengurangan adalah :

| Criteria | Max Points GC2 |
| --- | --- |
| Keterlambatan kurang dari 1 jam setelah deadline | 75 pts (75 %) |
| Keterlambatan lebih dari 1 jam - 1 hari setelah deadline | 50 pts (50 %) |
| Keterlambatan lebih dari 1 hari setelah deadline | 0 pts (0 %) |
