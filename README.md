
# 📄 README - Klasifikasi Kelayakan Kredit Komputer

## 📌 Deskripsi Dataset
Dataset ini berisi data dummy terkait pengajuan kredit komputer. Fitur-fitur yang digunakan antara lain:

- `Age`: Kategori usia (Muda, Sedang, Tua)
- `Income`: Tingkat pendapatan (Rendah, Sedang, Tinggi)
- `Student`: Status pelajar (Yes/No)
- `Credit_Rating`: Kualitas kredit (Baik/Buruk)
- `Buys_Computer`: Label target, 1 = Layak kredit, 0 = Tidak layak

---

## 🔧 Tahapan Pembuatan Model Klasifikasi (Decision Tree)

### 1. Load dan Eksplorasi Data
- Import data ke dalam DataFrame
- Cek struktur data, tipe data, jumlah data duplikat
- Hapus data duplikat (terdapat 949 duplikat)

### 2. Preprocessing
- Lakukan **One-Hot Encoding** pada semua fitur kategorikal:
  - `Age`, `Income`, `Student`, `Credit_Rating`
- Pisahkan fitur (`X`) dan label (`y`)
- Lakukan pembagian data menjadi training dan test set (80:20)

### 3. Pelatihan Model
- Model yang digunakan: `DecisionTreeClassifier`
- Parameter awal: `criterion='gini'`, `random_state=42`
- Dilatih menggunakan data training

### 4. Evaluasi Awal
- Hasil akurasi: **80.5%**
- Confusion Matrix:
  ```
  [[ 57  14]
   [ 25 104]]
  ```
- Precision & Recall menunjukkan performa cukup seimbang, namun recall untuk kelas 1 lebih tinggi.

### 6. Visualisasi
- Visualisasi Decision Tree (struktur pohon)

---

## 📈 Kode Penting

### One-Hot Encoding:
```python
df_encoded = pd.get_dummies(df, columns=['Age', 'Income', 'Student', 'Credit_Rating'], drop_first=True)
```

### Split Data:
```python
X = df_encoded.drop('Buys_Computer', axis=1)
y = df_encoded['Buys_Computer']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

### Model Training & Evaluasi:
```python
model = DecisionTreeClassifier(criterion='gini', random_state=42)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
```

---

## 🔍 Kesimpulan

- Decision Tree berhasil memberikan performa **akurat dan seimbang** meskipun dataset terbatas.
- **Overfitting minimal** dengan model default.
- Visualisasi decision boundary dan pohon dapat membantu menjelaskan cara kerja model ke pengguna non-teknis.
