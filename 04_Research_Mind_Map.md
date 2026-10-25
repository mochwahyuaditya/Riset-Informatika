# Research Mind Map

Mind map berikut menunjukkan alur penelitian yang direncanakan. Ini bukan laporan bahwa eksperimen sudah dilakukan.

```mermaid
flowchart TD
    A["Masalah: pemeriksaan roti masih visual<br/>dan sebagian roti dapat terbuang"] --> B["Dataset citra roti"]
    B --> B1["Roboflow V3<br/>kelas fresh dan mold<br/>173 berkas/gambar, 103 foto sumber menurut laporan"]
    B --> B2["Kaggle<br/>54 gambar, label perlu verifikasi visual"]
    B1 --> C["Audit dataset"]
    B2 --> C
    C --> C1["Validasi label dan format"]
    C --> C2["Cek hash, duplikasi visual,<br/>dan kelompok augmentasi"]
    C --> C3["Manifest: filename, label,<br/>source_group, visual_verified"]
    C1 --> D["Pisahkan data berdasarkan source_group<br/>bukan acak per gambar"]
    C2 --> D
    C3 --> D
    D --> D1["Training set"]
    D --> D2["Validation set"]
    D --> D3["Test set — tidak disentuh<br/>sampai evaluasi akhir"]
    D1 --> E["Augmentasi hanya<br/>pada training set"]
    E --> F["Preprocessing<br/>Resize 224x224, normalisasi ImageNet"]
    D2 --> F
    F --> G["EfficientNet-B0<br/>transfer learning"]
    G --> H["Klasifikasi"]
    H --> H1["fresh"]
    H --> H2["moldy"]
    H --> I["Evaluasi pada test set"]
    I --> I1["Confusion matrix"]
    I --> I2["Accuracy, precision,<br/>recall, F1-score"]
    H --> J["Grad-CAM"]
    J --> J1["Visualisasi area<br/>yang berkontribusi pada prediksi"]
    I --> K["Analisis kesalahan<br/>dan keterbatasan"]
    J1 --> K
    K --> L["Kesimpulan berdasarkan hasil aktual"]
    L --> M["Rencana lanjutan:<br/>validasi foto roti burger nyata"]
```

## Cara membaca
1. Audit label dan duplikasi dilakukan sebelum pembagian data.
2. Training hanya memakai training set; validation set dipakai untuk memilih konfigurasi.
3. Test set digunakan untuk evaluasi akhir dan tidak dipakai untuk memilih model.
4. Grad-CAM membantu melihat area yang memengaruhi prediksi, tetapi tidak membuktikan bahwa prediksi benar atau bahwa model mendeteksi jamur berdasarkan alasan yang tepat.
5. Kesimpulan dan rekomendasi operasional harus mengikuti hasil aktual.
