
# 💄 Sistem Rekomendasi Produk Skincare

Proyek ini merupakan submission akhir dari kelas Machine Learning, yang berfokus pada pembuatan sistem rekomendasi produk skincare. Dua pendekatan utama digunakan:

- **Content-Based Filtering**: merekomendasikan produk berdasarkan kemiripan fitur produk (kategori, nama, brand).
- **Collaborative Filtering**: merekomendasikan produk berdasarkan interaksi pengguna lain, menggunakan algoritma **SVD** dari library `surprise`.


## 📁 Struktur Direktori

| File / Folder                          | Deskripsi                                                               |
|----------------------------------------|-------------------------------------------------------------------------|
| `data/00. InfoProduct.csv`            | Dataset berisi detail produk skincare                                  |
| `data/00. Review.csv`                 | Dataset ulasan dan rating dari pengguna                                |
| `images/`                              | Folder berisi grafik visualisasi dan output evaluasi                   |
| `Submission_Sistem_Rekomendasi.ipynb` | Notebook utama berisi keseluruhan pipeline proyek                      |
| `submission_sistem_rekomendasi.py`    | Alternatif script Python untuk menjalankan sistem rekomendasi          |
| `Laporan-Submission-Rekomendasi.md`   | Laporan akhir dalam format markdown                                    |
| `README.md`                            | Deskripsi umum proyek dan instruksi penggunaan (file ini)              |

## 📦 Requirements

Pastikan semua library berikut terinstall sebelum menjalankan proyek:

```
pandas
numpy
scikit-learn
scikit-surprise
matplotlib
seaborn
```

### 📌 Cara instalasi cepat:
```bash
pip install -r requirements.txt
```

### ⚠️ PENTING: Library `scikit-surprise`

Library ini tidak terinstall secara default. Install secara manual jika belum:

```bash
pip install scikit-surprise
```

> 🔁 **WAJIB RESTART SESI / RUNTIME setelah menginstal `scikit-surprise`**  
> Jika menggunakan Google Colab atau Jupyter Notebook, silakan lakukan:
> - Runtime → Restart Runtime  
> Tanpa restart, modul `surprise` tidak akan dikenali oleh environment.

## ▶️ Cara Menjalankan

1. Buka file `Submission_Sistem_Rekomendasi.ipynb`
2. Jalankan sel-sel secara berurutan.
3. Pastikan file CSV berada dalam folder `data/`.
4. Alternatif: jalankan versi script

```bash
python submission_sistem_rekomendasi.py
```
