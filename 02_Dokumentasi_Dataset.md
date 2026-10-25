# Dokumentasi Dataset

## 1. Gambaran Umum

Dokumentasi ini menjelaskan sumber, struktur, distribusi, dan keterbatasan dataset yang direncanakan untuk penelitian **Klasifikasi Citra Roti Segar dan Berjamur Menggunakan EfficientNet-B0 dengan Visualisasi Grad-CAM**. Informasi kuantitatif berikut mengacu pada laporan pemeriksaan folder proyek per 22 Oktober 2026.

| Sumber data | Jumlah berkas pada dataset final | Label | Status pemeriksaan label |
|---|---:|---|---|
| Roboflow V3 | 86 | `fresh` | Mengacu pada anotasi kelas sumber |
| Roboflow V3 | 87 | `moldy` | Mengacu pada anotasi kelas sumber `mold` |
| Kaggle | 54 | `moldy` | Berdasarkan nama berkas; belum diverifikasi secara visual |
| **Total** | **227** | **86 `fresh`, 141 `moldy`** | **Sebagian label masih memerlukan verifikasi** |

Jumlah 227 menunjukkan banyaknya berkas gambar yang tercatat pada `dataset_final/`, bukan jumlah foto sumber unik yang telah terkonfirmasi. Sembilan berkas dari folder Kaggle tidak disalin ke dataset final karena format sebenarnya teridentifikasi sebagai WebP, meskipun ekstensi berkasnya `.jpg` atau `.jpeg`.

## 2. Sumber Dataset

### 2.1 Roboflow V3

- **Nama dataset:** Moldy Fresh Bread, versi 3.
- **URL:** https://universe.roboflow.com/dataset-roti-tawar/moldy-fresh-bread/dataset/3
- **Kelas sumber:** `fresh` (indeks 0) dan `mold` (indeks 1), berdasarkan `data.yaml`.
- **Lisensi yang tercantum pada berkas sumber:** CC BY 4.0.
- **Struktur:** `train/`, `valid/`, `test/`, dan `data.yaml`.
- **Format anotasi:** bounding box YOLO.
- **Jumlah gambar:** laporan lokal mencatat 173 berkas gambar Roboflow, yang berasal dari 103 foto sumber sebelum augmentasi.
- **Augmentasi yang tercatat:** pembalikan horizontal/vertikal, rotasi 90 derajat, variasi kecerahan, dan Gaussian blur.

Pada `dataset_final/`, kelas sumber `mold` disimpan dengan nama folder `moldy` agar penamaan kelas konsisten dengan rancangan penelitian. Perubahan nama ini tidak mengubah label sumber yang tercatat pada dataset Roboflow.

### 2.2 Kaggle

- **Nama dataset yang dicatat:** Moldy Bread Image Dataset.
- **URL kandidat:** https://www.kaggle.com/datasets/teranekerimova/moldy-bread-image-dataset
- **Folder lokal:** `dataset/`.
- **Jumlah berkas:** 63.
- **Pemeriksaan format berkas:** 49 JPEG, 5 PNG, dan 9 WebP yang menggunakan ekstensi `.jpg` atau `.jpeg`.
- **Dasar label pada dataset final:** nama berkas yang mengandung teks `moldy_bread`.

Label pada 54 gambar Kaggle yang disalin ke kelas `moldy` belum dikonfirmasi melalui pemeriksaan visual. Oleh karena itu, label tersebut masih bersifat sementara dan status sumber Kaggle perlu dicocokkan dengan dataset yang benar-benar diunduh sebelum sitasi akhir disusun.

## 3. Struktur Folder Lokal

Struktur berikut merangkum folder yang tercatat dalam pemeriksaan proyek pada 22 Oktober 2026.

```text
Riset Informatika/
├── dataset/                       # 63 berkas sumber Kaggle
├── roblofow_v3/                   # Folder lokal; nama mengandung salah ketik
│   ├── train/images/
│   ├── valid/images/
│   ├── test/images/
│   ├── data.yaml
│   └── README.dataset.txt
├── dataset_final/
│   ├── fresh/                     # 86 gambar
│   ├── moldy/                     # 141 gambar
│   └── quarantine/                # 0 gambar pada laporan pemeriksaan
├── buat_dataset_final.py
├── audit_kaggle.txt
├── audit_roboflow.txt
├── laporan_dataset_final.md
└── UTS/
```

Nama `roblofow_v3/` di atas merupakan nama folder lokal yang tercatat pada laporan, bukan nama resmi dataset. Jumlah berkas di dalam folder dapat berubah apabila dilakukan pemeriksaan atau pemrosesan lanjutan.

## 4. Distribusi Kelas

| Kelas | Jumlah gambar | Persentase | Komposisi sumber |
|---|---:|---:|---|
| `fresh` | 86 | 37,9% | Roboflow V3: 86 |
| `moldy` | 141 | 62,1% | Roboflow V3: 87; Kaggle: 54 |
| **Total** | **227** | **100%** | **Roboflow V3: 173; Kaggle: 54** |

Distribusi kelas belum seimbang. Jumlah berkas kelas `moldy` sekitar 1,64 kali jumlah berkas kelas `fresh`. Dampak ketidakseimbangan ini akan dipertimbangkan dalam proses pelatihan dan interpretasi hasil evaluasi.

## 5. Format Gambar pada Dataset Final

| Kelas | `.jpg` | `.jpeg` | `.png` | Total |
|---|---:|---:|---:|---:|
| `fresh` | 86 | 0 | 0 | 86 |
| `moldy` | 134 | 2 | 5 | 141 |
| **Total** | **220** | **2** | **5** | **227** |

## 6. Keterbatasan dan Risiko Dataset

1. **Verifikasi label Kaggle.** Label 54 gambar Kaggle didasarkan pada nama berkas, bukan pemeriksaan visual. Status ini harus diperhitungkan saat menetapkan label acuan (*ground truth*).
2. **Konversi anotasi.** Anotasi bounding box Roboflow digunakan untuk menentukan label kelas gambar. Proses tersebut menghasilkan label tingkat gambar dan tidak mempertahankan informasi lokasi jamur sebagai keluaran klasifikasi.
3. **Ketergantungan antar-gambar.** Laporan sumber menyebut 173 berkas Roboflow berasal dari 103 foto sumber. Gambar hasil augmentasi yang berasal dari foto yang sama berpotensi menimbulkan kebocoran data apabila tersebar pada subset pelatihan, validasi, dan pengujian.
4. **Perbedaan domain.** Dataset publik belum tentu mewakili kondisi roti burger di gerai, termasuk jenis roti, pencahayaan, sudut pengambilan gambar, kemasan, dan kondisi penyimpanan.
5. **Jumlah data.** Terdapat 227 berkas pada dataset final, sedangkan jumlah foto sumber unik belum dikonfirmasi secara menyeluruh. Generalisasi model perlu ditafsirkan sesuai keterbatasan tersebut.
6. **Berkas WebP.** Sembilan berkas WebP dari folder Kaggle belum termasuk dataset final. Berkas tersebut memerlukan konversi format sebelum dapat dipertimbangkan untuk digunakan.
7. **Lisensi dan atribusi.** Informasi lisensi yang tercantum pada sumber Roboflow adalah CC BY 4.0. Ketentuan penggunaan dan redistribusi setiap sumber tetap menjadi bagian dari pemeriksaan sebelum dataset dipublikasikan.

## 7. Metadata Dataset

Untuk mendukung keterlacakan data, metadata setiap gambar dapat dicatat dalam berkas CSV dengan kolom berikut.

| Kolom | Deskripsi |
|---|---|
| `filename` | Nama berkas gambar pada dataset final |
| `label` | Kelas `fresh` atau `moldy` |
| `source` | Sumber gambar, yaitu `roboflow` atau `kaggle` |
| `source_group` | Identitas foto sumber; untuk Roboflow, kelompok ditentukan dari nama sumber sebelum penanda augmentasi `.rf.` jika tersedia |
| `visual_verified` | Status verifikasi visual label |
| `true_format` | Format berkas yang teridentifikasi dari isi berkas |
| `split` | Subset data setelah pembagian train/validation/test ditetapkan |

Metadata tersebut dapat digunakan untuk memeriksa konsistensi label, menelusuri asal gambar, dan mendokumentasikan pembagian dataset.

## 8. Tahapan Pemeriksaan Sebelum Eksperimen

Sebelum pelatihan EfficientNet-B0, tahapan pemeriksaan dataset meliputi:

1. Meninjau secara visual gambar Kaggle yang labelnya saat ini ditentukan berdasarkan nama berkas.
2. Menyusun metadata yang memuat label, sumber, status verifikasi, dan kelompok foto sumber.
3. Membagi data berdasarkan kelompok foto sumber agar hasil augmentasi dari satu foto tidak tersebar di subset yang berbeda.
4. Melakukan augmentasi hanya pada subset pelatihan setelah pembagian data selesai.
5. Mencatat versi dataset dan perubahan yang dilakukan selama proses persiapan.

## 9. Catatan tentang Jumlah Foto Sumber

Angka 227 merupakan jumlah berkas pada dataset final berdasarkan laporan lokal. Laporan Roboflow mencatat 173 berkas gambar yang berasal dari 103 foto sumber sebelum augmentasi. Dengan demikian, jumlah foto sumber unik dalam keseluruhan dataset belum dapat ditetapkan hanya dari total berkas. Pemeriksaan berdasarkan kelompok sumber dan kemiripan visual diperlukan untuk memperoleh estimasi yang lebih akurat. Tidak ditemukannya berkas dengan hash MD5 identik tidak dengan sendirinya membuktikan bahwa semua gambar berbeda secara visual.
