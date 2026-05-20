# Experiment Log

Catat setiap percobaan hyperparameter di sini. **Minimal 5 eksperimen.**

> Tips: ubah **satu hyperparameter pada satu waktu** agar bisa mengisolasi efeknya. Setelah memahami efek tiap variabel, baru gabungkan untuk hasil terbaik.

---

## 📋 Tabel Ringkasan

Isi tabel ini setelah selesai semua eksperimen.

| # | Hidden | Neurons | Activation | Optimizer | LR     | Batch | Epochs | Dropout | Test Acc | Train Time |
|---|--------|---------|------------|-----------|--------|-------|--------|---------|----------|------------|
| 0 | 1      | 64      | relu       | sgd       | 0.01   | 32    | 10     | 0.0     | ~85%     | ~30s       |
| 1 |   17    |     64    |      relu      |    sgd       |    0.01    |  32   |    10    |    0.0     |     84.38%     |      69.6s      |
| 2 |    4    |     64    |     elu       |      sgd     |   0.01     |   32    |   10    |    0.0     |    85.91%      |     57.6s       |
| 3 |   3     |     128    |    elu        |      adamax     |     0.001   |    64   |   10     |    0.0     |     87.57%     |       49.6s     |
| 4 |   3     |    256     |    elu        |     adamax      |    0.01    |   64    |   10     |    0.0     |     88.09%     |     84.9s       |
| 5 |   2     |    512     |    relu        |     adam      |    0.001    |   128    |   20     |    0.2     |     89.02%     |     179.3s       |

> **Eksperimen #0** = baseline (jangan ubah, ini patokan kalian).

---

## 🧪 Detail Setiap Eksperimen

Gunakan template di bawah untuk SETIAP eksperimen.

---

### Eksperimen #1

**Apa yang diubah dari baseline:**
> Menambah jumlah Hidden layer secara ekstrem dari 1 menjadi 17, sedangkan parameter lainnya tetap sama.

**Hipotesis sebelum run:**
> Menambah kedalaman jaringan hingga 17 layer akan meningkatkan kapasitas model untuk mempelajari pola kompleks, tetapi tanpa normalisasi atau penyesuaian optimizer, model berisiko mengalami vanishing gradient dan waktu training akan membengkak.

**Hasil:**
- Test accuracy: 84.38%
- Train accuracy: 86.97%
- Validation accuracy: 84.55%
- Train time: 69.6 detik
- Apakah overfit/underfit? Underfit / Mengalami kendala optimasi. Meskipun jaringan jauh lebih dalam, akurasi tesnya justru turun dibanding baseline (~85%).

**Observasi & Insight:**
>Menambah kedalaman layer secara drastis menggunakan optimizer SGD tanpa modifikasi lain (seperti residual connections atau batch normalization) justru memperburuk performa dan menggandakan waktu training akibat masalah vanishing gradient.

---

### Eksperimen #2

**Apa yang diubah:**
>Menambah jumlah Hidden layer secara moderat dari 1 menjadi 4 dan mengubah fungsi aktivasi dari relu menjadi elu.

**Hipotesis:**
>Fungsi aktivasi ELU dapat mencegah masalah dying ReLU karena memiliki nilai negatif yang halus, dan penambahan 4 layer akan menaikkan performa akurasi tanpa membebani komputasi secara berlebihan.

**Hasil:**
- Test accuracy: 85.91%
- Train accuracy: 87.74%
- Validation accuracy: 86.75%
- Train time: 57.6 detik
- Apakah overfit/underfit? Good fit (Performa meningkat secara sehat dibanding baseline).

**Observasi:**
>Kombinasi penambahan layer yang ideal (4 layer) dan transisi ke aktivasi elu terbukti efektif. Model berhasil melampaui performa baseline dengan kenaikan waktu training yang masih sangat wajar.

---

### Eksperimen #3

**Apa yang diubah:**
>Mengurangi Hidden menjadi 3 layer, melipatgandakan Neurons menjadi 128, menggunakan optimizer adaptif adamax, menurunkan LR menjadi 0.001, serta menaikkan Batch size menjadi 64.

**Hipotesis:**
>Optimizer adaptif (adamax) dengan learning rate yang lebih kecil akan membuat konvergensi jauh lebih stabil, sementara peningkatan jumlah neuron (128) akan memperluas kapasitas representasi fitur.

**Hasil:**
- Test accuracy: 87.57%
- Train accuracy: 89.85%
- Validation accuracy: 88.03%
- Train time: 49.6 detik
- Apakah overfit/underfit? Good fit (Mengarah ke titik optimal).

**Observasi:**
>Eksperimen ini memberikan peningkatan akurasi yang signifikan (87.57%). Menariknya, penambahan batch size ke 64 dan penggunaan optimizer adaptif justru memangkas waktu training menjadi lebih cepat (49.6 detik) dibanding Eksperimen #2.

---

### Eksperimen #4

**Apa yang diubah:**
>Menggandakan jumlah Neurons dari 128 menjadi 256 dan menaikkan kembali LR dari 0.001 menjadi 0.01.

**Hipotesis:**
>Kapasitas model akan semakin besar dengan 256 neuron, namun menaikkan learning rate pada optimizer adaptif berisiko membuat proses training tidak stabil (overshooting), walaupun mungkin bisa sedikit mendongkrak akurasi jika beruntung.

**Hasil:**
- Test accuracy: 88.09%
- Train accuracy: 89.93%
- Validation accuracy: 85.75%
- Train time: 84.9 detik
- Apakah overfit/underfit? Cenderung Good fit menuju Overfit ringan (Akurasi naik tipis, namun peningkatan performa tidak sebanding dengan pembengkakan waktu latih).

**Observasi:**
>Akurasi meningkat sedikit menjadi 88.09%, tetapi waktu latih membengkak hampir dua kali lipat menjadi 84.9 detik karena beban komputasi dimensi matriks neuron yang semakin besar.

---

### Eksperimen #5

**Apa yang diubah:**
>Mengurangi Hidden menjadi 2 layer, melonjakkan jumlah Neurons secara masif menjadi 512, mengembalikan aktivasi ke relu, mengganti optimizer ke adam, menetapkan LR di 0.001, menaikkan Batch ke 128, memperpanjang Epochs menjadi 20, dan mengaktifkan Dropout sebesar 0.2.

**Hipotesis:**
>Model dengan 512 neuron dan 20 epoch memiliki risiko tinggi terkena overfitting. Namun, penambahan teknik regularisasi Dropout (0.2) diharapkan mampu meredam overfitting tersebut sehingga model mendapatkan performa terbaiknya.

**Hasil:**
- Test accuracy: 89.02%
- Train accuracy: 92.12%%
- Validation accuracy: 89.45%
- Train time: 179.3 detik
- Apakah overfit/underfit? Good fit / Well-regularized (Mencapai performa tertinggi dengan generalisasi yang baik berkat bantuan Dropout).

**Observasi:**
>Konfigurasi ini sukses menghasilkan akurasi tertinggi di antara seluruh percobaan (89.02%). Jumlah epoch yang lebih banyak dan kapasitas neuron yang besar memberikan ruang bagi model untuk belajar lebih maksimal, sementara dropout menjaga model agar tidak overfit. Konsekuensinya, waktu latih menjadi yang paling lama (179.3 detik).
---

## 🏆 Konfigurasi Terbaik

Setelah semua eksperimen, salin konfigurasi terbaik kalian ke sini:

```python
HIDDEN_LAYERS     = 2
NEURONS_PER_LAYER = 512
ACTIVATION        = relu
DROPOUT_RATE      = 0.2
OPTIMIZER         = adam
LEARNING_RATE     = 0.001
BATCH_SIZE        = 128
EPOCHS            = 20
```

**Test accuracy final: 89.02%**
