# UTS Riset Informatika

**Judul:** Klasifikasi Citra Roti Segar dan Berjamur Menggunakan EfficientNet-B0 dengan Visualisasi Grad-CAM  
**Semester:** 7  
**Terakhir diperbarui:** 22 Oktober 2026

---

## Daftar Berkas

| No | Berkas | Keterangan | Status |
|----|--------|-----------|--------|
| 1 | `01_Proposal_Penelitian.md` | Latar belakang, rumusan masalah, tujuan, manfaat, batasan, penelitian terdahulu, metodologi, tahapan, dan daftar pustaka | Perlu pemeriksaan akhir terhadap referensi dan pedoman dosen |
| 2 | `02_Dokumentasi_Dataset.md` | Sumber, struktur aktual, jumlah gambar, format, keterbatasan, manifest yang disarankan | Dokumentasi berdasarkan laporan lokal per 22 Okt 2026; perlu dicocokkan ulang |
| 3 | `03_Research_Gap.md` | Tabel penelitian terdahulu, peluang, dan batas klaim | Perlu pemeriksaan akhir terhadap referensi dan pedoman dosen |
| 4 | `04_Research_Mind_Map.md` | Alur penelitian dalam format Mermaid flowchart | Selesai — sintaks Mermaid valid |
| 5 | `05_Rencana_Evaluation_Metric.md` | Confusion matrix, metrik, prosedur evaluasi yang benar | Selesai |
| 6 | `README.md` | Berkas ini | Diperbarui |

---

## Status Dataset

Dataset final dilaporkan tersedia di `dataset_final/` (satu level di atas folder `UTS/`). Angka dan isi folder perlu diperiksa lagi di komputer sebelum dikumpulkan:

| Kelas | Jumlah | Sumber | Verifikasi |
|-------|-------:|--------|-----------|
| `fresh` | 86 gambar | Roboflow V3 (prefix `rb_`) | Terverifikasi via anotasi YOLO |
| `moldy` | 141 gambar | Roboflow 87 (prefix `rb_`) + Kaggle 54 (prefix `kg_`) | Roboflow: YOLO. Kaggle: **belum visual** |
| **Total** | **227** | | |

- Dataset asli tidak diubah: `dataset/` (63 file) dan `roblofow_v3/` (349 file) utuh.
- Laporan audit menyatakan tidak ada duplikat MD5 antar-sumber; ini belum menyingkirkan duplikasi visual atau hubungan augmentasi.
- 9 file Kaggle berformat WebP (tersamar sebagai `.jpg`/`.jpeg`) **tidak dimasukkan** — perlu Pillow untuk konversi.
- Laporan menyebut 103 foto sumber Roboflow menghasilkan 173 berkas/gambar setelah augmentasi. Karena itu, 227 berkas dalam dataset_final tidak boleh disebut 227 foto sumber unik. **Pembagian train/val/test harus menggunakan source_group, bukan acak per gambar.**

---

## Referensi yang Digunakan

| No | Referensi | DOI / URL |
|----|-----------|-----------|
| 1 | Treepong & Theera-Ampornpunt (2023) — deteksi jamur roti via CNN | https://doi.org/10.1016/j.crfs.2023.100574 |
| 2 | Tan & Le (2019) — EfficientNet | https://arxiv.org/abs/1905.11946 |
| 3 | Selvaraju et al. (2020) — Grad-CAM | https://doi.org/10.1007/s11263-019-01228-7 |
| 4 | Roboflow dataset (2026) — Moldy & Fresh Bread V3 | https://universe.roboflow.com/dataset-roti-tawar/moldy-fresh-bread/dataset/3 |

---

## Pekerjaan yang Masih Harus Dilakukan

Sebelum eksperimen:
1. **Audit visual** 54 gambar Kaggle (prefix `kg_`) di `dataset_final/moldy/`.
2. **Buat manifest CSV** dengan kolom: `filename`, `label`, `source`, `source_group`, `visual_verified`, `true_format`, `split`.
3. **Bagi data** berdasarkan `source_group` (sebelum `.rf.` pada nama file Roboflow) — bukan acak per gambar.
4. **Konversi 9 file WebP** dari Kaggle jika ingin digunakan (jalankan `buat_dataset_final.py` setelah `pip install Pillow`).
5. **Minta persetujuan dosen** untuk ruang lingkup dan format akhir dokumen.

Setelah eksperimen:
6. Isi tabel hasil di `05_Rencana_Evaluation_Metric.md` dengan angka aktual.
7. Tambahkan visualisasi Grad-CAM ke laporan.
8. Tulis kesimpulan berdasarkan hasil aktual — bukan perkiraan.

---

## Hal yang Tidak Boleh Diklaim Sebelum Ada Bukti

- Akurasi, precision, recall, atau F1-score model.
- Pengurangan limbah atau manfaat operasional gerai.
- Bahwa dataset bebas dari data leakage (belum ada split yang dibuat).
- Bahwa semua label sudah benar (label Kaggle belum diverifikasi visual).





## Catatan penting sebelum publikasi GitHub
- Jangan mengunggah dataset gambar ke repository publik sebelum memastikan lisensi, atribusi, ukuran file, dan izin redistribusi. Untuk tugas, repository dapat berisi dokumen, skrip, manifest, dan tautan sumber; dataset dapat tetap lokal.
- Jangan mengunggah kredensial, token GitHub, atau file konfigurasi rahasia.
- Sebelum commit, periksa perubahan dengan `git status` dan `git diff`.
- “Deploy ke GitHub” untuk dokumen Markdown biasanya berarti push ke repository. GitHub Pages hanya diperlukan jika dosen meminta situs web; file Markdown tidak perlu di-deploy sebagai aplikasi.
- Dokumen ini perlu dicocokkan dengan instruksi resmi dosen. Kesempurnaan akademik tidak dapat dipastikan tanpa rubrik tugas tersebut.
