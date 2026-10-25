# Proposal Penelitian

## Judul
**Klasifikasi Citra Roti Segar dan Berjamur Menggunakan EfficientNet-B0 dengan Visualisasi Grad-CAM**

## 1. Latar Belakang
Di gerai Burger Bangor Kupang Jaya, roti burger dipersiapkan untuk memenuhi kebutuhan operasional. Berdasarkan pengamatan awal yang disampaikan peneliti, sebagian roti dapat berjamur dan terbuang ketika persiapan melebihi kebutuhan. Pemeriksaan kondisi roti saat ini mengandalkan pengamatan visual. Penggunaan klasifikasi citra berpotensi membantu menguji apakah pola visual pada gambar dapat digunakan untuk membedakan roti segar dan roti berjamur.

Penelitian ini mengusulkan EfficientNet-B0 sebagai model klasifikasi citra dan Grad-CAM untuk memvisualisasikan area gambar yang berkontribusi terhadap prediksi model. Dataset awal berasal dari sumber publik, bukan kumpulan foto terverifikasi dari gerai. Karena itu, penelitian ini merupakan evaluasi awal dan tidak langsung membuktikan bahwa sistem dapat mengurangi limbah dalam kegiatan operasional.

## 2. Rumusan Masalah
1. Bagaimana menyiapkan dataset citra roti dengan label `fresh` dan `moldy` yang terdokumentasi serta layak digunakan?
2. Bagaimana kinerja EfficientNet-B0 dalam mengklasifikasikan citra roti segar dan berjamur pada data uji terpisah?
3. Bagaimana Grad-CAM dapat digunakan untuk menampilkan area citra yang memengaruhi prediksi model?

## 3. Tujuan
1. Mendokumentasikan dan menyiapkan dataset citra roti untuk klasifikasi dua kelas.
2. Mengimplementasikan EfficientNet-B0 dengan transfer learning untuk klasifikasi `fresh` dan `moldy`.
3. Mengevaluasi model menggunakan confusion matrix, accuracy, precision, recall, dan F1-score.
4. Menghasilkan visualisasi Grad-CAM sebagai alat interpretasi prediksi, bukan sebagai bukti tunggal bahwa model memahami jamur.

## 4. Manfaat
- **Akademis:** menjadi latihan penerapan klasifikasi citra dan interpretabilitas model.
- **Praktis:** memberi gambaran awal apakah pendekatan berbasis citra layak diteliti lebih lanjut untuk inspeksi visual roti.
- **Metodologis:** mendokumentasikan keterbatasan label, sumber data, dan risiko data leakage.

## 5. Batasan Penelitian
1. Klasifikasi hanya dua kelas: `fresh` dan `moldy`; penelitian ini tidak mengklasifikasikan tahap pertumbuhan jamur.
2. Model yang direncanakan adalah EfficientNet-B0 dengan transfer learning.
3. Grad-CAM digunakan untuk visualisasi area yang berkontribusi terhadap prediksi.
4. Dataset awal berasal dari sumber publik Roboflow dan Kaggle sesuai berkas yang tersedia di proyek.
5. Label yang belum terverifikasi secara visual tidak boleh dianggap sebagai ground truth yang pasti.
6. Data harus dibagi menjadi training, validation, dan test tanpa kebocoran dari gambar sumber yang sama atau augmentasi turunannya.
7. Penelitian tidak mengklaim pengurangan limbah, keamanan pangan, atau kesiapan penggunaan di gerai tanpa evaluasi lapangan.
8. Jumlah berkas dataset akhir mengikuti hasil audit aktual dan tidak melebihi 1.500 berkas; jumlah foto sumber unik harus dihitung terpisah dari hasil augmentasi.

## 6. Penelitian Terdahulu
Treepong dan Theera-Ampornpunt (2023) meneliti deteksi awal jamur roti menggunakan gambar mikroskopis yang diambil dengan lensa tambahan 50× pada smartphone. Mereka membandingkan beberapa konfigurasi CNN dan transfer learning pada roti putih dan gandum utuh, serta melaporkan F1-score terbaik 0,9948 dan 0,9972 untuk dua dataset mereka. Angka tersebut adalah hasil penelitian mereka, bukan hasil yang dapat dipindahkan ke dataset penelitian ini. Perbedaan utama adalah penelitian terdahulu menggunakan gambar mikroskopis dan proses pengumpulan terkontrol, sedangkan penelitian ini merencanakan klasifikasi gambar biasa dari dataset publik dan menambahkan visualisasi Grad-CAM.

EfficientNet diperkenalkan oleh Tan dan Le (2019) dengan gagasan menyeimbangkan kedalaman, lebar, dan resolusi jaringan melalui compound scaling. Artikel tersebut menjadi dasar pemilihan keluarga model, tetapi tidak secara khusus membuktikan performa pada dataset roti yang digunakan di sini.

## 7. Metodologi
### 7.1 Audit dan persiapan data
- Inventarisasi jumlah dan format gambar dari setiap sumber.
- Periksa label, kualitas gambar, file rusak, gambar duplikat, dan gambar yang berasal dari sumber sama.
- Pisahkan gambar dengan label meragukan ke daftar karantina; jangan memasukkannya ke data terverifikasi.
- Catat nama berkas, kelas, sumber, status verifikasi, dan kelompok sumber asli pada manifest.
- Periksa lisensi serta ketentuan atribusi sumber.

### 7.2 Preprocessing
- Membaca gambar dengan pemeriksaan format.
- Mengubah ukuran gambar sesuai kebutuhan input EfficientNet-B0 (umumnya 224 × 224 untuk konfigurasi standar).
- Mengonversi gambar menjadi RGB dan menerapkan preprocessing yang sesuai dengan bobot pretrained yang dipakai.
- Augmentasi hanya pada data training. Augmentasi tidak boleh dilakukan sebelum pembagian data jika hasil turunannya dapat masuk ke subset berbeda.

### 7.3 Pemodelan
- Menggunakan EfficientNet-B0 pretrained sebagai ekstraktor fitur awal.
- Mengganti lapisan klasifikasi akhir menjadi dua kelas: `fresh` dan `moldy`.
- Melatih dengan transfer learning; konfigurasi dan seed dicatat.
- Gunakan validation set untuk memilih konfigurasi, bukan test set.

### 7.4 Interpretasi
Buat visualisasi Grad-CAM untuk contoh prediksi benar dan salah. Interpretasi hanya menunjukkan area yang berhubungan dengan aktivasi model; visualisasi tidak membuktikan sebab-akibat dan tidak menggantikan pemeriksaan label.

### 7.5 Evaluasi
Uji model satu kali pada test set yang tidak digunakan untuk pelatihan atau pemilihan model. Laporkan confusion matrix, accuracy, precision, recall, F1-score, jumlah sampel per kelas, dan keterbatasan. Untuk kelas positif `moldy`, recall penting untuk melihat berapa banyak gambar berjamur yang berhasil ditemukan.

## 8. Tahapan Penelitian
1. Studi literatur dan penetapan ruang lingkup.
2. Audit sumber dan label dataset.
3. Penyusunan manifest dan pencegahan data leakage.
4. Preprocessing dan pembagian data.
5. Implementasi EfficientNet-B0.
6. Pelatihan dan pemilihan model menggunakan validation set.
7. Evaluasi akhir pada test set.
8. Visualisasi Grad-CAM dan analisis kesalahan.
9. Penulisan kesimpulan sesuai hasil aktual.

## Daftar Pustaka
1. Treepong, P., & Theera-Ampornpunt, N. (2023). *Early bread mold detection through microscopic images using convolutional neural network*. Current Research in Food Science, 7, 100574. https://doi.org/10.1016/j.crfs.2023.100574
2. Tan, M., & Le, Q. V. (2019). *EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks*. Proceedings of the 36th International Conference on Machine Learning. https://arxiv.org/abs/1905.11946
3. Selvaraju, R. R., Cogswell, M., Das, A., Vedantam, R., Parikh, D., & Batra, D. (2020). Grad-CAM: Visual explanations from deep networks via gradient-based localization. *International Journal of Computer Vision*, 128, 336–359. https://doi.org/10.1007/s11263-019-01228-7
4. Roboflow. (2026). *Moldy & Fresh Bread Dataset* (Version 3) [Dataset]. Roboflow Universe. https://universe.roboflow.com/dataset-roti-tawar/moldy-fresh-bread/dataset/3 (Lisensi: CC BY 4.0)
