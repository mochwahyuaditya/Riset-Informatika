# Rencana Evaluation Metric

## 1. Tujuan Evaluasi
Evaluasi digunakan untuk mengukur kemampuan EfficientNet-B0 mengklasifikasikan gambar ke kelas `fresh` atau `moldy`. Tidak ada nilai performa yang dapat dicantumkan sebelum eksperimen selesai.

Tetapkan kelas positif sebagai **`moldy`** agar precision dan recall mudah ditafsirkan dalam konteks pencarian gambar berjamur.

## 2. Confusion Matrix
Confusion matrix membandingkan label sebenarnya dengan prediksi model.

| | Prediksi `moldy` | Prediksi `fresh` |
|---|---:|---:|
| Aktual `moldy` | True Positive (TP) | False Negative (FN) |
| Aktual `fresh` | False Positive (FP) | True Negative (TN) |

- **TP:** gambar berjamur diprediksi berjamur.
- **FN:** gambar berjamur keliru diprediksi segar.
- **FP:** gambar segar keliru diprediksi berjamur.
- **TN:** gambar segar diprediksi segar.

## 3. Metrik dan Rumus
### Accuracy
Proporsi seluruh prediksi yang benar.

\[
Accuracy = \frac{TP + TN}{TP + TN + FP + FN}
\]

### Precision untuk kelas `moldy`
Dari semua gambar yang diprediksi berjamur, berapa bagian yang benar-benar berjamur.

\[
Precision = \frac{TP}{TP + FP}
\]

Precision rendah berarti banyak gambar segar yang salah ditandai sebagai berjamur.

### Recall untuk kelas `moldy`
Dari semua gambar yang benar-benar berjamur, berapa bagian yang berhasil dikenali.

\[
Recall = \frac{TP}{TP + FN}
\]

Recall rendah berarti banyak gambar berjamur yang terlewat. Dalam konteks inspeksi, FN perlu diperhatikan secara khusus.

### F1-score
Rata-rata harmonik precision dan recall.

\[
F1 = 2 \times \frac{Precision \times Recall}{Precision + Recall}
\]

F1 membantu merangkum precision dan recall dalam satu angka. Jika penyebut bernilai nol, jelaskan penanganan perhitungan yang digunakan oleh pustaka evaluasi.

## 4. Prosedur Evaluasi yang Benar
1. Audit label dan identifikasi gambar sumber serta turunannya.
2. Pisahkan dataset menjadi training, validation, dan test berdasarkan kelompok gambar sumber asli. Jangan membagi hasil augmentasi dari gambar yang sama ke subset berbeda.
3. Lakukan augmentasi hanya pada training set.
4. Latih model dengan training set dan gunakan validation set untuk memilih konfigurasi.
5. Setelah konfigurasi final ditetapkan, evaluasi pada test set yang belum digunakan selama pelatihan maupun pemilihan model.
6. Laporkan confusion matrix, accuracy, precision, recall, F1-score, jumlah sampel aktual per kelas, serta metode pembagian data.
7. Cantumkan seed, preprocessing, bobot pretrained, parameter pelatihan, dan versi dataset agar hasil dapat direproduksi.
8. Analisis kesalahan dengan meninjau false positive dan false negative. Gunakan Grad-CAM sebagai bantuan interpretasi pada contoh yang dipilih, bukan pengganti metrik.

## 5. Catatan Interpretasi
- Jika kelas tidak seimbang, accuracy saja dapat menyesatkan; baca bersama precision, recall, dan F1-score.
- Jika terdapat label yang salah atau meragukan, metrik yang dihitung terhadap label tersebut tidak mencerminkan kinerja sebenarnya.
- Jika gambar dari sumber yang sama muncul di training dan test, hasil dapat terlalu optimistis karena data leakage.
- Hasil dari dataset publik tidak langsung menunjukkan kinerja pada roti burger di gerai.
- Tidak boleh menyimpulkan limbah berkurang hanya berdasarkan metrik klasifikasi. Klaim itu membutuhkan evaluasi operasional terpisah.

## 6. Tabel Hasil Eksperimen (Isi Setelah Pengujian)
| Metrik | Nilai |
|---|---|
| Jumlah sampel test | Belum diukur |
| TP / FP / FN / TN | Belum diukur |
| Accuracy | Belum diukur |
| Precision (`moldy`) | Belum diukur |
| Recall (`moldy`) | Belum diukur |
| F1-score (`moldy`) | Belum diukur |

**Penting:** tabel ini sengaja tidak diisi dengan angka perkiraan. Masukkan hasil aktual setelah evaluasi selesai.
