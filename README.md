# Analisis Clustering Kerentanan Izin Operasional Angkutan Perdesaan Kabupaten Bogor Menggunakan Metode K-Prototype
 
Repositori ini berisi implementasi dan dokumentasi skripsi tentang pemetaan kepatuhan legalitas (SK Trayek) angkutan perdesaan di Kabupaten Bogor menggunakan algoritma **K-Prototype** pada data bertipe campuran (kategorikal dan numerik).
 
> **Penulis:** Evan Yudi Pratama
> **Program Studi:** Teknologi Informasi, Universitas Bina Sarana Informatika
> **Tahun:** 2026
 
---
 
## Latar Belakang
 
Surat Keputusan (SK) Trayek merupakan legalitas operasional angkutan perdesaan yang wajib diperpanjang secara berkala. Namun, tingkat kepatuhan pemilik angkutan di Kabupaten Bogor masih rendah, tidak merata antarkecamatan, dan belum terpetakan secara kuantitatif. Data operasional yang tersedia bertipe campuran, sehingga algoritma clustering konvensional seperti K-Means tidak dapat diterapkan secara optimal.
 
Penelitian ini mengisi kesenjangan tersebut dengan menerapkan K-Prototype untuk mengelompokkan kendaraan berdasarkan tingkat kerentanan masa berlaku izin trayeknya.
 
## Tujuan
 
- Mengimplementasikan algoritma K-Prototype untuk mengelompokkan data operasional angkutan perdesaan Kabupaten Bogor.
- Menentukan jumlah cluster optimal menggunakan Elbow Method.
- Mengevaluasi kualitas dan kebermaknaan cluster menggunakan Cramér's V dan Eta kuadrat (η²).
- Menguji hipotesis bahwa K-Prototype mampu menghasilkan pengelompokan yang optimal pada data campuran.

## Metodologi
 
Penelitian mengikuti kerangka **Knowledge Discovery in Databases (KDD)**: 
1. **Pengumpulan data**: data operasional angkutan perdesaan dari Dinas Perhubungan Kabupaten Bogor (6.017 kendaraan, 8 kolom).
2. **Pra-pemrosesan**:
   - Ekstraksi nama kecamatan dari teks alamat menggunakan **Regular Expression (RegEx)** dengan kamus perbaikan typo (100+ entri).
   - Konversi tanggal berakhir SK Trayek menjadi **Unix Timestamp**.
   - Normalisasi **Min-Max** pada fitur numerik.
3. **Pemodelan**: K-Prototype dikembangkan *from scratch* menggunakan Python (jarak Euclidean untuk fitur numerik dan *Simple Matching Dissimilarity* untuk fitur kategorikal, γ = 0,5).
4. **Penentuan K optimal**: Elbow Method (K = 2 sampai 7, `n_init = 3`); model final dilatih dengan `n_init = 10`.
5. **Evaluasi**: Cramér's V (fitur kategorikal) dan Eta kuadrat (fitur numerik).

### Fitur yang Digunakan

| Fitur | Tipe | Keterangan |
|---|---|---|
| Kecamatan | Kategorikal | Hasil ekstraksi RegEx dari Alamat Pemilik |
| Kode Trayek | Kategorikal | Kode rute yang dilayani kendaraan |
| Berakhir SK Trayek | Numerik | Tanggal berakhir SK, dikonversi ke Unix Timestamp |
 
## Hasil Utama

- **K optimal = 3** berdasarkan Elbow Method.
- Tiga cluster terbentuk: **PANJANG (37,1%)**, **BERAKHIR (40,8%)**, dan **RENTAN (22,2%)**.
- Cramér's V: Kode Trayek **0,626** dan Kecamatan **0,583** (kategori kuat).
- Eta kuadrat: Berakhir SK Trayek **0,252** (kategori besar).
- **54,1%** kecamatan dan **51,5%** kode trayek berstatus BERAKHIR, yang mengindikasikan kerentanan bersifat sistemik.
- Keempat indikator pengujian mendukung H1, sehingga H0 ditolak.

## Teknologi
 
- Python 3
- Google Colaboratory
- pandas, NumPy
- matplotlib
- Modul `re` (RegEx) dan `datetime`

## Catatan Data
 
Dataset asli berasal dari Dinas Perhubungan Kabupaten Bogor dan memuat data pribadi pemilik kendaraan (nama dan alamat). **Data mentah tidak disertakan dalam repositori ini** demi menjaga privasi dan kepatuhan terhadap ketentuan penggunaan data.

## Kontak
 
**Evan Yudi Pratama**
Email: evnydprtma@gmail.com