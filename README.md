# IntegrasiData_ETS

Repository ini berisi implementasi dan penjelasan mengenai **Deteksi Anomali Pengadaan Barang/Jasa (PBJ)** menggunakan pendekatan **Klasifikasi Berbobot**.

---

## 📌 Deskripsi Metode

Pembobotan dilakukan secara manual untuk mengidentifikasi, khususnya pada kolom **pagu**, pasangan atau kelompok antar baris yang memiliki nilai paling mendekati satu sama lain. Dengan pendekatan ini, tingkat kemiripan antar data dapat dianalisis secara lebih terarah.

Proses ini mencakup:
- Penentuan bobot pada setiap komponen yang relevan  
- Transformasi data agar dapat dibandingkan secara adil  
- Perhitungan skor kemiripan antar baris secara sistematis  

Hasil akhirnya merepresentasikan **kedekatan nilai antar data** dengan lebih akurat.

---

## 📊 Tiga Metrik Kesamaan

### 1. 📝 Kesamaan Paket *(Bobot: 10%)*  
Membandingkan deskripsi teks setiap paket tender dengan target menggunakan **TF-IDF vectorization** dengan n-gram (1–2 kata).

- Mengubah teks menjadi vektor numerik  
- Menggunakan **cosine similarity** untuk mengukur kemiripan  
- Baris dengan susunan kata yang serupa akan mendapatkan skor lebih tinggi  

---

### 2. 💰 Kesamaan Pagu *(Bobot: 70%)*  
Membandingkan nilai anggaran secara numerik.

- Menggunakan transformasi **log (log1p)** untuk mengurangi skala ekstrem  
- Normalisasi ke rentang **[0, 1]** menggunakan min-max scaling  
- Rumus kesamaan:
- similarity = 1 - |perbedaan|
- - Nilai anggaran yang lebih dekat menghasilkan skor lebih tinggi  

⚠️ Metrik ini memiliki kontribusi terbesar terhadap skor akhir.

---

### 3. 🏢 Kesamaan isUMKM *(Bobot: 20%)*  
Perbandingan sederhana berbasis nilai boolean.

- `1` → jika status UMKM sama  
- `0` → jika berbeda  

---

## ⚖️ Komposisi Skor Akhir

Skor akhir dihitung berdasarkan kombinasi berbobot:

- Paket: 10%  
- Pagu: 70%  
- UMKM: 20%  

Pendekatan ini memastikan bahwa faktor anggaran menjadi penentu utama, namun tetap mempertimbangkan konteks deskripsi dan status UMKM.

---

## 🚀 Cara Menjalankan

*(Tambahkan step-by-step di sini, misalnya install requirements, run script, dll)*

```bash
pip install -r requirements.txt
python main.py
