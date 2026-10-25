# Research Gap

## 1. Penelitian Terdahulu yang Dapat Diverifikasi

| Sumber | Tujuan dan data | Metode | Hasil yang dilaporkan sumber | Keterbatasan / relevansi |
|---|---|---|---|---|
| Treepong & Theera-Ampornpunt (2023), *Early bread mold detection through microscopic images using convolutional neural network* | Deteksi awal jamur pada roti putih dan roti gandum utuh; gambar mikroskopis 50x yang dikumpulkan peneliti | Perbandingan berbagai CNN dengan transfer learning, preprocessing, resolusi, dan augmentasi | F1-score terbaik dilaporkan 0,9948 untuk roti putih dan 0,9972 untuk roti gandum utuh | Data menggunakan gambar mikroskopis dengan pengumpulan terkontrol; tidak dapat diasumsikan setara dengan gambar biasa dari dataset publik atau roti burger. Artikel juga memisahkan subset berdasarkan potongan roti untuk menghindari kebocoran. |
| Tan & Le (2019), *EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks* | Mengembangkan pendekatan scaling arsitektur CNN; eksperimen pada beberapa dataset visi komputer | Compound scaling yang menyeimbangkan depth, width, dan resolution; memperkenalkan keluarga EfficientNet | Melaporkan performa pada benchmark umum, termasuk ImageNet dan dataset transfer learning | Bukan penelitian khusus klasifikasi roti berjamur dan tidak membuktikan kinerja pada dataset proyek ini. Menjadi dasar arsitektur, bukan bukti hasil penelitian lokal. |
| Selvaraju et al. (2020), *Grad-CAM: Visual Explanations from Deep Networks via Gradient-based Localization* | Mengembangkan metode visualisasi area aktivasi pada model CNN tanpa memodifikasi arsitektur | Menggunakan gradien dari prediksi kelas terhadap feature map konvolusi terakhir untuk membuat heatmap | Menunjukkan Grad-CAM dapat mengidentifikasi area yang relevan pada berbagai arsitektur CNN di dataset gambar umum | Grad-CAM memvisualisasikan area aktivasi, bukan membuktikan model "memahami" jamur secara kausal. Interpretasi visual harus dilengkapi evaluasi metrik. |

## 2. Gap dan Peluang Penelitian
Berdasarkan tiga sumber ilmiah di atas, penelitian deteksi jamur roti dengan CNN dan transfer learning sudah pernah dilakukan. Karena itu, penelitian ini **tidak boleh mengklaim sebagai metode pertama** untuk klasifikasi roti berjamur.

Peluang yang lebih terukur untuk penelitian ini:
1. Menguji EfficientNet-B0 pada dataset publik yang tersedia di proyek, dengan dokumentasi label dan sumber yang transparan.
2. Menambahkan Grad-CAM untuk memeriksa apakah area yang ditonjolkan model secara visual relevan dengan indikasi jamur.
3. Menekankan audit label, pemisahan berdasarkan sumber gambar, dan pencegahan data leakage sebagai bagian dari metode.
4. Membahas keterbatasan penerapan hasil dataset publik terhadap foto roti burger di lingkungan gerai.

## 3. Rumusan Gap
Penelitian terdahulu oleh Treepong dan Theera-Ampornpunt membahas klasifikasi jamur pada gambar mikroskopis dan mengevaluasi beberapa konfigurasi CNN. Penelitian ini berfokus pada implementasi EfficientNet-B0 untuk klasifikasi dua kelas `fresh` dan `moldy` dari dataset publik yang tersedia, disertai visualisasi Grad-CAM dan audit potensi kebocoran data. Kontribusi yang diusulkan terletak pada konteks dataset, transparansi proses persiapan, dan interpretasi model, bukan klaim bahwa klasifikasi jamur roti belum pernah diteliti.

## 4. Batas Bukti
- Belum dilakukan tinjauan sistematis terhadap seluruh literatur terkait.
- Klaim gap di atas bersifat sementara dan hanya didasarkan pada sumber yang tercantum.
- Keterbatasan yang tidak dinyatakan langsung oleh artikel tidak ditulis sebagai kelemahan yang pasti; perbedaan jenis gambar dan konteks hanya dipakai untuk menjelaskan batas penerapan hasil.
- Kinerja EfficientNet-B0 dan manfaat Grad-CAM pada dataset proyek masih harus dibuktikan melalui eksperimen.

## Daftar Pustaka
1. Treepong, P., & Theera-Ampornpunt, N. (2023). *Early bread mold detection through microscopic images using convolutional neural network*. Current Research in Food Science, 7, 100574. https://doi.org/10.1016/j.crfs.2023.100574
2. Tan, M., & Le, Q. V. (2019). *EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks*. https://arxiv.org/abs/1905.11946
3. Selvaraju, R. R., Cogswell, M., Das, A., Vedantam, R., Parikh, D., & Batra, D. (2020). Grad-CAM: Visual explanations from deep networks via gradient-based localization. *International Journal of Computer Vision*, 128, 336–359. https://doi.org/10.1007/s11263-019-01228-7


## 5. Tautan sumber primer untuk pemeriksaan
- Treepong & Theera-Ampornpunt (2023), halaman PubMed Central: https://pmc.ncbi.nlm.nih.gov/articles/PMC10474362/
- Tan & Le (2019), Proceedings of Machine Learning Research: https://proceedings.mlr.press/v97/tan19a.html
- Selvaraju et al., Grad-CAM, halaman IEEE: https://doi.org/10.1109/ICCV.2017.74

Catatan: artikel Grad-CAM memiliki versi konferensi ICCV 2017 dan versi jurnal yang lebih lanjut. Pastikan entri bibliografi yang dipilih sesuai dengan versi yang benar-benar dirujuk dan gunakan satu format sitasi secara konsisten.
