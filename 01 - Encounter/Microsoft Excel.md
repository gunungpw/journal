# Vlookup and Index Match

[

![My Skill](https://miro.medium.com/v2/resize:fill:88:88/1*uFch7F6KU0emVZ3lXv1mog.png)









](https://medium.com/@myskill.id?source=post_page-----e6ccc68b90e4--------------------------------)

[My Skill](https://medium.com/@myskill.id?source=post_page-----e6ccc68b90e4--------------------------------)

·

[Follow](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fuser%2Fbef0fc5592f0&operation=register&redirect=https%3A%2F%2Fmedium.com%2F%40myskill.id%2Fvlookup-and-index-match-e6ccc68b90e4&user=My+Skill&userId=bef0fc5592f0&source=post_page-bef0fc5592f0----e6ccc68b90e4---------------------post_header-----------)

3 min read

·

Sep 9, 2023

[

](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fvote%2Fp%2Fe6ccc68b90e4&operation=register&redirect=https%3A%2F%2Fmedium.com%2F%40myskill.id%2Fvlookup-and-index-match-e6ccc68b90e4&user=My+Skill&userId=bef0fc5592f0&source=-----e6ccc68b90e4---------------------clap_footer-----------)

65

[](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fbookmark%2Fp%2Fe6ccc68b90e4&operation=register&redirect=https%3A%2F%2Fmedium.com%2F%40myskill.id%2Fvlookup-and-index-match-e6ccc68b90e4&source=-----e6ccc68b90e4---------------------bookmark_footer-----------)

_Microsoft Excel Intermediate Series from Microsoft Excel Path MySkill.id_

> [Yuk subscribe](https://medium.com/@myskill.id/subscribe) untuk mendapatkan email notifikasi setiap ada artikel terbaru oleh MySkill

# **VLookup**

VLOOKUP adalah salah satu fungsi pencarian yang paling umum digunakan di Excel. Ini memungkinkan untuk mencari nilai dalam tabel dan mengembalikan nilai yang sesuai dari kolom yang berdekatan. Digunakan mencari data pada tabel referensi lain menggunakan sebuah nilai kunci yang spesifik/unik. Pencarian bersifat satu dimensi.

![](https://miro.medium.com/v2/resize:fit:624/1*hk3S8N_WEKkf6bJQhzrA-A.png)

Fungsi Vlookup. Sumber: Bitlabs

**Fungsi:** =VLOOKUP(lookup_value, table_array, col_index_nura, [range_lookup])

- **Lookup value:** Nilai yang akan dicari pada kolom pertama Tabel Referensi (table array)
- **Table array :** Table referensi dimana nilai yang dicari berada pada kolom pertama table
- **Col index num:** Nomor kolom pada Tabel Referensi yang akan diambil nilainya
- **Range lookup :**

-True: pencarian yang sama persis atau mendekati

-False: pencarian hanya yang sama persis

Contoh :=VLOOKUP (A1;C1:G1000;4;FALSE)

# **IF ERROR**

Berfungsi untuk mengembalikan nilai sesuai dengan yang ditentukan saat terjadi error, seperti #NA dan DIV/O. Biasanya terletak didepan fungsi/formula excel lainnya.

![](https://miro.medium.com/v2/resize:fit:612/1*zOgY4THAY16b4jcP6NW1Iw.png)

Fungsi If Error. Sumber: Educba

- **Fungsi:** =IFERROR(value, value_if_error)
- **Value:** Argumen yang akan diperiksa apakah terjadi kesalahan apa tidak.
- **Value_if_error:** Nilai yang akan dikembalikan jika rumus menemukan nilai kesalahan.

Contoh: =IFERROR(A3/B3;”Invalid””)

# **Index Match**

## **Fungsi Match**

Fungsi MATCH digunakan untuk mencari nilai tertentu dalam rentang data dan mengembalikan posisinya (baris atau kolom) dalam rentang tersebut.

![](https://miro.medium.com/v2/resize:fit:398/1*_vui9ZyapP_A7KZ5LSUdcg.png)

Fungsi Match. Sumber: Ablebits

- **Fungsi :** MATCH (lookup_value, lookup_array, [match_type])
- **Lookup value:** nilai yang akan dicari.
- **Lookup Array:** range data yang dicari.
- **Match type:**

- 1, menemukan nilai terdekat yang <= lookup Value

- 0, menemukan nilai yang lookup value

- (-1), menemukan nilai terdekat yang >= lookup Value

Dalam fungsi Indexmatch, Match merupakan bagian dari fungsi Index.

## **Fungsi Index**

Fungsi INDEX digunakan untuk mengambil nilai dari tabel atau rentang data berdasarkan posisi baris dan kolomnya. Fungsi ini sangat fleksibel dan memungkinkan untuk mengambil nilai dari tabel dalam berbagai cara. Dapat digunakan juga untuk memperoleh/menampilkan nilai data di dalam tabel berdasarkan lokasi.

![](https://miro.medium.com/v2/resize:fit:549/1*gexPWJD8XBlp8f3_-PNGtw.png)

Fungsi Index Match. Sumber: Wallstreetmojo

- **Fungsi:** INDEX( array, row_num, [col_num ])
- **Array:** Range data atau table
- **Row Num:** Nomor baris di dalam array yang akan ditampilkan nilainya
- **Col Num:** Nomor kolom di dalam array yang akan ditampilkan nilainya

**Contoh :**

=INDEX(A1:C7;4;2)

=INDEX(D2:D8;MATCH(C10;B2:B8;0))

=INDEX(C2:E7;MATCH(B9;A2:A7;0);MATCH(B10;C1:E1;0))

# **Perbedaan Vlookup dan Index Match**

Perbedaan utama antara keduanya adalah bahwa VLOOKUP bekerja berdasarkan kolom, sedangkan INDEX MATCH bekerja berdasarkan posisi baris dan kolom. INDEX MATCH juga lebih fleksibel dan dapat digunakan untuk pencarian yang lebih kompleks, sementara VLOOKUP lebih mudah digunakan dalam kasus sederhana di mana kita hanya perlu mencari data dalam satu kolom.

## **Vlookup**

![](https://miro.medium.com/v2/resize:fit:523/1*a2_pksjKU0iL5vV0CuWutg.png)

Contoh Penggunaan Vlookup. Sumber: Educba

- VLOOKUP digunakan untuk mencari nilai dalam kolom tertentu dalam tabel atau rentang data dan mengembalikan nilai yang sesuai dari kolom yang berdekatan.
- Satu Fungsi
- Mencari data satu dimensi saja
- Mudah dimengerti
- Ukuran file besar

## **Index Match**

![](https://miro.medium.com/v2/resize:fit:498/1*nmrLZrIerNyuNgfG3qvoFA.png)

Penggunaan Indeks Match. Sumber: Educba

- Digunakan untuk mencari posisi (baris atau kolom) dari nilai tertentu dalam range.
- Pencarian yang lebih fleksibel dan presisi.
- Terdiri dari 2 fungsi
- Mencari data satu dan dua dimensi
- Lebih kompleks
- Ukuran file kecil

Learn more via: [https://myskill.id/course/vlookup-index-match](https://myskill.id/course/vlookup-index-match)