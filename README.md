# Learning Strategy pada Klasifikasi MNIST

Tugas Assignment 2 — Mata Kuliah Pembelajaran Mesin Mendalam (Deep Learning)

Eksperimen ini menguji beberapa teknik regularisasi pada model klasifikasi MNIST sederhana (Flatten → Dense(64) → Dense(10)) untuk melihat pengaruhnya terhadap overfitting dan akurasi.

## Skenario yang diuji

| Skenario | Teknik | Parameter |
|---|---|---|
| Baseline | - | - |
| 2(a) | L1 Regularization | λ = 1e-4 pada Dense(64) |
| 2(b) | L2 Regularization | λ = 1e-3 pada Dense(64) |
| 2(c) | Dropout | rate = 0,1 setelah Dense(64) |
| 2(d) | Early Stopping | monitor `val_loss`, patience = 3, `restore_best_weights=True` |
| 2(e) | L1 + Dropout | λ = 1e-4, rate = 0,1 |

Validasi menggunakan data uji (test set), bukan split terpisah dari data latih.

## Hasil

| Skenario | Epoch | Akurasi uji | Gap akurasi | Loss uji | Gap loss |
|---|---|---|---|---|---|
| Baseline | 10 | 97,27% | 1,40 | 0,0890 | 0,0422 |
| 2(a) L1 | 10 | 97,22% | 0,61 | 0,1726 | 0,0127 |
| 2(b) L2 | 10 | 97,08% | 0,65 | 0,1548 | 0,0150 |
| 2(c) Dropout | 10 | 97,47% | 1,23 | 0,0850 | 0,0388 |
| 2(d) Early Stopping | 14 (bobot terbaik: epoch 11) | 97,22% | 1,55 | 0,0883 | 0,0457 |
| 2(e) L1 + Dropout | 10 | 97,40% | 0,54 | 0,1764 | 0,0143 |

Gap akurasi = akurasi latih − akurasi uji. Gap loss = loss uji − loss latih (indikator overfitting utama).

Ringkasan: Dropout memberi akurasi tertinggi, L1 (disusul L1+Dropout) memberi generalisasi paling stabil, dan Early Stopping berguna secara praktis (tidak perlu menebak jumlah epoch) meski tidak menurunkan overfitting seperti teknik lain.


## Cara menjalankan

1. Buka notebook di Google Colab atau Jupyter.
2. Jalankan seluruh cell secara berurutan (Run all).
3. Seed acak (`SEED = 42`) sudah diset agar hasil training konsisten.

## Penulis

Azhar Maulana — 24/533487/PA/22582
