# Refleksi Tim

> Jawaban dalam Bahasa Indonesia. Maksimal 1 halaman (~500 kata). Yang dinilai adalah **kedalaman pemahaman**, bukan panjang tulisan.

---

## 1. Parameter vs Hyperparameter

Berdasarkan eksperimen yang kalian lakukan, jelaskan dengan **kata-kata kalian sendiri**:
- Apa yang termasuk **parameter** dalam model kalian, dan apa yang termasuk **hyperparameter**?
- Manakah yang berubah saat training berjalan, dan manakah yang ditentukan oleh kalian sebelum training?

**Jawaban:**
>Dalam model kami, parameter adalah bobot (weights) dan bias yang ada di setiap lapisan Dense. Sedangkan hyperparameter mencakup variabel yang kami tentukan di panel konfigurasi, seperti Learning Rate, Batch Size, Epochs, dan jumlah Hidden Units.

---

## 2. Hyperparameter dengan Dampak Terbesar

Dari semua hyperparameter yang kalian eksperimen, mana yang menurut kalian memberikan **dampak paling besar** terhadap akurasi? Mengapa demikian — apa yang kalian amati pada kurva loss/accuracy?

**Jawaban:**
>Berdasarkan pengamatan kami, Learning Rate memiliki dampak paling signifikan. Jika Learning Rate terlalu kecil, kurva loss turun sangat lambat (model malas belajar). Namun, jika sedikit saja terlalu besar, kurva loss menjadi tidak stabil atau bahkan melonjak naik (explode). Kami mengamati bahwa tanpa Learning Rate yang tepat, penambahan layer atau neuron tidak akan memberikan peningkatan akurasi yang berarti.

---

## 3. Learning Rate

Coba set `LEARNING_RATE = 1.0` (atau bahkan lebih besar) dan jalankan sekali. Apa yang terjadi pada kurva loss? Hubungkan jawaban kalian dengan rumus:

$$W_j = W_j - \lambda \frac{\partial F(W_j)}{\partial W_j}$$

**Jawaban:**
>Saat kami mengatur LEARNING_RATE = 1.0, kurva loss menjadi sangat kacau atau langsung menunjukkan angka yang sangat tinggi (NaN).

---

## 4. Batch Size & Trade-off

Bandingkan eksperimen dengan **batch size kecil** (misal 16) vs **batch size besar** (misal 256). Apa yang kalian amati dari sisi:
- Waktu training?
- Stabilitas kurva loss?
- Akurasi akhir?

Apakah pengamatan ini sesuai dengan teori di slide kuliah?

**Jawaban:**
>Batch size besar (256) jauh lebih cepat menyelesaikan satu epoch karena memanfaatkan paralelisasi GPU, sedangkan batch size kecil (16) terasa lebih lambat. Batch size 16 menghasilkan kurva loss yang lebih "berisik" atau fluktuatif karena setiap update hanya berdasarkan sedikit sampel. Batch size 256 menghasilkan kurva yang lebih halus. Batch size kecil seringkali memberikan akurasi final yang sedikit lebih baik karena sifatnya yang "berisik" membantu model keluar dari local minima. Hal ini sesuai dengan teori di kuliah bahwa ada trade-off antara kecepatan komputasi dan kualitas generalisasi model.

---

## 5. Feed Forward & Back Propagation

Pada saat kalian menekan `model.fit(...)`, sebenarnya proses feed forward dan back propagation berjalan **ribuan kali**. Hitung kira-kira berapa kali back propagation terjadi pada salah satu eksperimen kalian.

> Petunjuk: `(jumlah_sample_training / batch_size) × epochs`

Jelaskan apa yang terjadi pada **bobot** dan **bias** model kalian di antara iterasi pertama dan terakhir.

**Jawaban:**
>Jika kita menggunakan 60.000 sampel training, batch_size = 32, dan epochs = 10:
Iterasi per epoch = 60.000 / 32 = 1.875 kali.
Total backpropagation = 1.875 × 10 = 18.750 kali.
Di antara iterasi pertama dan terakhir, bobot model berubah dari nilai acak (random initialization) menjadi nilai yang terstruktur yang mampu merepresentasikan pola visual pakaian (seperti garis tepi tas atau bentuk lengan baju).

---

## 6. Kapan Deep Learning Tepat Digunakan?

Berdasarkan pengalaman kalian dengan Fashion-MNIST, menurut kalian apakah masalah ini *benar-benar* membutuhkan deep learning, atau bisa diselesaikan dengan machine learning klasik (misal Logistic Regression atau Random Forest)? Beri argumen.

**Jawaban:**
>Untuk Fashion-MNIST, Machine Learning klasik seperti Random Forest sebenarnya sudah bisa mencapai akurasi ~85-88%. Namun, Deep Learning (terutama jika menggunakan CNN) lebih tepat jika kita menginginkan akurasi di atas 90% tanpa perlu melakukan feature engineering manual. DL "belajar" fitur sendiri, sedangkan ML klasik sangat bergantung pada bagaimana kita merepresentasikan data mentah tersebut.

---

## 7. Refleksi Tim

- Tantangan apa yang paling sulit?
- Apa pelajaran terpenting yang kalian dapat dari aktivitas ini?
- Jika diberi waktu lebih, apa yang ingin kalian coba lagi?

**Jawaban:**
>Tantangan: Menemukan kombinasi "manis" antara jumlah neuron dan learning rate agar model tidak overfitting.
>Pelajaran Terpenting: Perubahan kecil pada hyperparameter bisa mengubah model dari "sangat cerdas" menjadi "sama sekali tidak belajar".
>Eksperimen Lanjutan: Kami ingin mencoba teknik Regularization seperti Dropout untuk melihat apakah stabilitas akurasi pada data validasi bisa meningkat lebih jauh.
