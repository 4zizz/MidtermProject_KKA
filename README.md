# MidtermProject_KKA

## 1. Hill-Climbing with Random Restart
* **Mekanisme Dasar:** Algoritma pencarian lokal (*local search*) yang memperbaiki solusi secara bertahap dengan memilih jadwal tetangga yang memiliki nilai *cost* (konflik) lebih rendah[cite: 5, 8]. Algoritma hanya mau menerima perubahan yang memperbaiki kondisi[cite: 2].
* **Penanganan Optimum Lokal:** Karena hanya menerima perbaikan, algoritma ini sangat rentan terjebak pada *local minimum* (kondisi di mana pemindahan satu ujian apa pun sudah tidak bisa menurunkan *cost* lagi, padahal belum tentu optimal secara global)[cite: 2, 5, 8]. Untuk mengatasinya, digunakan teknik *Random Restart*, yaitu menjalankan ulang pencarian dari titik awal acak yang berbeda sebanyak 50 kali[cite: 8, 12].
* **Hasil Kinerja:** Berhasil menurunkan jumlah mahasiswa bentrok hingga 99,3% (dari 2.812 menjadi 16 mahasiswa) dalam waktu sekitar 29 detik[cite: 8, 12]. Namun, nilai *cost* akhirnya masih bervariasi antara 16 sampai 37 karena setiap *restart* berhenti di *local optimum* yang berbeda-beda[cite: 8, 12].

## 2. Simulated Annealing
* **Mekanisme Dasar:** Algoritma optimasi probabilistik yang terinspirasi dari proses pendinginan logam (*annealing*)[cite: 5, 6].
* **Cara Keluar dari Local Optimum:** Berbeda dengan *Hill Climbing*, Simulated Annealing memiliki mekanisme unik yaitu dapat menerima solusi yang lebih buruk (meningkatkan *cost*) dengan probabilitas tertentu menggunakan fungsi eksponensial berdasarkan temperatur ($T$)[cite: 5, 6].
* **Jadwal Pendinginan (*Cooling Schedule*):** Di awal pencarian (saat temperatur tinggi), algoritma lebih bebas menerima solusi buruk untuk mengeksplorasi ruang pencarian luas dan keluar dari *local optimum*[cite: 6]. Seiring berjalan waktu, temperatur diturunkan secara bertahap sehingga peluang menerima solusi buruk semakin kecil, dan algoritma berfokus melakukan eksploitasi (*fine-tuning*) di sekitar solusi yang baik[cite: 6].
* **Hasil Kinerja:** Merupakan algoritma terbaik dalam pengujian ini karena berhasil mencapai nilai *Cost* 0 (seluruh 18.835 mahasiswa / 100% bebas dari bentrok jadwal) dengan waktu komputasi tercepat sekitar 18 detik melalui 569.515 langkah pencarian[cite: 9, 10, 12].

## 3. Genetic Algorithm (GA)
* **Mekanisme Dasar:** Algoritma optimasi berbasis populasi yang meniru proses seleksi alam dan evolusi biologis[cite: 6]. Alih-alih mengelola satu jadwal saja, algoritma ini memelihara sekumpulan kandidat jadwal sekaligus (populasi)[cite: 6].
* **Tahapan Utama:**
  * **Inisialisasi:** Membentuk populasi awal berisi sejumlah jadwal acak (individu/kromosom)[cite: 9].
  * **Seleksi (*Tournament Selection*):** Memilih individu-individu terbaik dari populasi untuk dijadikan induk (*parent*)[cite: 9].
  * **Crossover:** Menggabungkan bagian penempatan slot dari dua induk untuk melahirkan keturunan (*offspring*) baru[cite: 6, 9].
  * **Mutasi:** Mengubah penempatan slot beberapa ujian secara acak guna menjaga keragaman genetik dalam populasi[cite: 6, 9].
  * **Elitism:** Memastikan individu terbaik dari satu generasi otomatis lolos ke generasi berikutnya agar kualitas terbaik tidak hilang[cite: 9].
* **Hasil Kinerja:** Menghasilkan nilai *cost* berbobot sebesar 294 (159 pasangan ujian bentrok, berdampak pada 292 mahasiswa)[cite: 9, 12]. Pada generasi-generasi akhir, kurva penurunan *cost* melandai dan cenderung mendatar (*stagnant*)[cite: 9, 12]. Hal ini terjadi karena operator *crossover* dan mutasi yang sifatnya acak pada masalah penjadwalan skala besar berisiko merusak struktur jadwal yang sebelumnya sudah cukup baik, sehingga perbaikan di tahap akhir menjadi sangat lambat[cite: 12].
