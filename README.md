# Klasifikasi Penyakit Kulit Melanoma Menggunakan ReXNet-150 & Grad-CAM

[![Python](https://img.shields.io/badge/Python-3.10-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/Framework-PyTorch-orange.svg)](https://pytorch.org/)
[![Academic](https://img.shields.io/badge/Thesis-Telkom%20University-red.svg)](https://openlib.telkomuniversity.ac.id/)

Repositori ini berisi *source code* untuk proyek Tugas Akhir (TA) Sarjana Teknologi Informasi, Fakultas Informatika, Universitas Telkom. Penelitian ini berfokus pada pengembangan sistem deteksi dini kanker kulit melanoma yang akurat, efisien secara komputasi, dan transparan (Explainable AI) menggunakan arsitektur **ReXNet-150** dan visualisasi **Grad-CAM**.

---

## 📌 Latar Belakang
Melanoma merupakan salah satu jenis kanker kulit paling mematikan karena kemampuannya untuk bermetastasis ke organ vital. Diagnosis konvensional berbasis dermoskopi sering terkendala oleh subjektivitas klinis. Di sisi lain, model Deep Learning standar seperti ResNet50 dan VGG16 memiliki beban komputasi tinggi dan bersifat *black-box*. 

Proyek ini mengusulkan penggunaan **ReXNet-150** yang menerapkan *Linear Channel Scaling* untuk mengeliminasi *representational bottleneck*, dikombinasikan dengan **Grad-CAM** untuk memberikan justifikasi visual (*heatmap*) area lesi secara presisi bagi tenaga medis.

---

## 🛠️ Spesifikasi Sistem & Framework
* **Bahasa Pemrograman:** Python 3.10
* **Deep Learning Framework:** PyTorch
* **Pre-trained Model Repository:** `timm` (PyTorch Image Models)
* **XAI Library:** `pytorch-grad-cam`
* **Dataset:** ISIC Archive via Kaggle (3.600 citra dermoskopi seimbang antara kelas *benign* dan *malignant*)

---

## 📊 Hasil Eksperimen & Perbandingan Model
Berdasarkan pengujian komprehensif pada kondisi perangkat keras yang identik (NVIDIA Tesla T4 GPU), model ReXNet-150 terbukti unggul signifikan dalam efisiensi komputasi dan performa diagnostik:

| Model | Akurasi | Presisi | Recall | F1-Score | Ukuran Model (MB) | Waktu Inferensi |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **ReXNet-150 (Proposed)** | **0.86** | **0.86** | **0.86** | **0.86** | **30.2 MB** | **58.2 ms ($p < 0.05$)** |
| ResNet50 | 0.74 | 0.79 | 0.74 | 0.73 | 90.0 MB | 159.8 ms |
| VGG16 | 0.78 | 0.87 | 0.78 | 0.79 | 512.2 MB | 628.5 ms |

### Key Findings:
1. **Model Lightweight:** Ukuran checkpoint ReXNet-150 (30.2 MB) terbukti **3x lebih kecil** dari ResNet50 dan **17x lebih kecil** dari VGG16, menjadikannya sangat layak diimplementasikan pada perangkat *mobile*/*edge computing*.
2. **Inferensi Real-Time:** Rata-rata waktu inferensi berada di angka **58.2 ms**, memenuhi ambang batas responsivitas aplikasi medis *real-time* (< 60 ms).
3. **Validasi Klinis XAI:** Visualisasi Grad-CAM menunjukkan bahwa model secara aktif memfokuskan ekstraksi fitur pada area lesi aktual (spektrum merah-kuning) dan berhasil mengabaikan artefak non-medis seperti rambut atau pantulan cahaya.

---

## 📁 Struktur Direktori
```text
project_MelanomaDetection/
├── dataset/               # Tempat menyimpan subset dataset ISIC
├── notebooks/
│   └── melanoma_training.ipynb  # Jupyter Notebook untuk training, komparasi & Grad-CAM
├── models/                # Folder penyimpanan checkpoint model (.pth)
├── outputs/               # Hasil visualisasi heatmap Grad-CAM
├── requirements.txt       # Daftar dependensi pustaka python
└── README.md              # Dokumentasi proyek
