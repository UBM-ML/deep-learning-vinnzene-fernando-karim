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
> Contoh: Mengganti optimizer dari `sgd` → `adam`, sisanya tetap.

**Hipotesis sebelum run:**
> Contoh: Adam adalah optimizer adaptif, kami menduga konvergensi akan lebih cepat dan akurasi naik.

**Hasil:**
- Test accuracy: ___%
- Train accuracy: ___%
- Validation accuracy: ___%
- Train time: ___ detik
- Apakah overfit/underfit? ___

**Observasi & Insight:**
>

**Rencana eksperimen berikutnya:**
>

---

### Eksperimen #2

**Apa yang diubah:**

**Hipotesis:**

**Hasil:**

**Observasi:**

---

### Eksperimen #3

**Apa yang diubah:**

**Hipotesis:**

**Hasil:**

**Observasi:**

---

### Eksperimen #4

**Apa yang diubah:**

**Hipotesis:**

**Hasil:**

**Observasi:**

---

### Eksperimen #5

**Apa yang diubah:**

**Hipotesis:**

**Hasil:**

**Observasi:**

---

## 🏆 Konfigurasi Terbaik

Setelah semua eksperimen, salin konfigurasi terbaik kalian ke sini:

```python
HIDDEN_LAYERS     = ?
NEURONS_PER_LAYER = ?
ACTIVATION        = ?
DROPOUT_RATE      = ?
OPTIMIZER         = ?
LEARNING_RATE     = ?
BATCH_SIZE        = ?
EPOCHS            = ?
```

**Test accuracy final: ___%**
