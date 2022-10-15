# RFM Analysis
Roy Andhika Satria, [satriaroy70@gmail.com](mailto:satriaroy70@gmail.com).

## Customer Segmentation using RFM 
Pengelompokan customer berdasarkan kebiasaan belanjanya  
[***R***] Recency     = Berapa lama sejak customer melakukan transaksi (tanggal sekarang - tanggal terakhir transaksi)  
[***F***] Frequency   = Berapa kali customer melakukan transaksi (jumlah transaksi atas 1 customer)  
[***M***] Monetary    = Total uang yang dibelanjakan customer

## Dataset
Data bersumber dari [Kaggle](https://www.kaggle.com/code/nazlisener/customer-segmentation-using-rfm/notebook).  
Dataset disini berisi transaksi yang berasal dari salah satu retail di UK dari 2009 - 2011.

## Tujuan
Manajemen bisa membagi customer ke dalam kelompok berdasarkan cara berbelanjanya dan harapannya bisa membuat iklan  dan promosi yang lebih spesifik ke masing - masing kelompok customer.

### Problem Statement :
1. Produk paling laris?
1. Negara dengan total belanja terbanyak?
1. Biaya termahal dalam sekali transaksi?
1. Customer paling banyak belanja?

## Penjelasan Dataset 
Data memiliki `1067371` baris dan `8` kolom

| No | __Nama Fitur__ | __Penjelasan__ |
| - | - | - |
| 1 | Invoice | Nomer invoice unik untuk setiap transaksi berbeda, jika ada "C" berarti cancel atau dibatalkan | 
| 2 | StockCode | Kode produk unik untuk setiap item |
| 3 | Description | Nama item |
| 4 | Quantity | Jumlah item yang terjual dalam 1 transaksi |
| 5 | InvoiceDate | Tanggal transaksi | 
| 6 | Price | Harga 1 item |
| 7 | Customer ID | ID unik untuk setiap customer |
| 8 | Country | Negara asal customer |


---
## Steps
1. Data Understanding
2. Exploratory Data Analysis (EDA)
3. Preprocessing 
4. Modeling & Conclusion 

### 1. Data Understanding
1. Terdapat 8 fitur pada tabel
2. Memiliki 4382 null di Description dan 243007 null di Customer ID (treatment menyusul)
3. Data semuanya sudah dalam bentuk kategorikal
4. Perbandingan data target e & p sudah seimbang

### 2. Ringkasan Exploratory Data Analysis (EDA)
1. Jamur yang bisa dimakan, 80% memiliki **odor = n** atau tidak berbau.  
![graph2](https://raw.githubusercontent.com/royandhika/classification-mushroom/main/assets/odor.png)
2. Hampir keseluruhan data memiliki fitur **gill-attachment = f** baik edible maupun poisonous, fitur kurang relevan dan dipertimbangkan untuk menghapus fitur ini.  
![graph1](https://raw.githubusercontent.com/royandhika/classification-mushroom/main/assets/gill-attachment.png)
3. Jamur beracun **97%** memiliki **gill-spacing = c**.  
![graph3](https://raw.githubusercontent.com/royandhika/classification-mushroom/main/assets/gill-spacing.png)
4. Jamur beracun **44%** memiliki **gill-color = b** atau kuning ke-krem-an, sedangkan jamur yang bisa dimakan tidak memiliki warna ini sehingga dapat dipastikan jika menemukan jamur dengan **gill-color = b pasti beracun**.  
![graph4](https://raw.githubusercontent.com/royandhika/classification-mushroom/main/assets/gill-color.png)
5. **veil-color** mayoritas data memiliki warna putih, fitur kurang relevan dan dipertimbangkan untuk menghapus fitur ini.  
![graph5](https://raw.githubusercontent.com/royandhika/classification-mushroom/main/assets/veil-color.png)

### 3. Preprocessing
| Target |	Persentase	| 
| - | - | 
| Edible	| 51.79% |	
| Poisonous	| 48.21%	| 

Data target sudah cukup seimbang, tidak perlu dilakukan balancing  
Kemudian data kategorikal semuanya diubah ke dalam bentuk 1 dan 0 menggunakan One-hot-encoding

### 4. Base Model / Benchmarking
Menggunakan single testing dan kemudian divalidasi ulang menggunakan stratifiedKFold dengan k = 10. Scoring yang digunakan adalah 'f1-score'.

| Model | F1 score | 10-fold validation (mean) | Waktu |
|:-:|:-:|:-:|:-:|
| Logistic Regression | 1.00 | 1.00 | 0.9s |
| Categorical Naive Bayes | 0.94 | 0.939 | 0.7s |
| Decision Tree | 1.00 | 1.00 | 0.6s |
| K Nearest Neighbor | 1.00 | 1.00 | 1.3s |
| Random Forest | 1.00 | 1.00 | 3.2s |
| Support Vector Classification | 1.00 | 1.00 | 8.8s |

Berdasarkan hasil confusion matrix dan waktu processing, kita dapati bahwa 3 performa teratas adalah Decision Tree, KNN, dan Logistic Regression. 

### 5. Learning Curve
Learning curve menggunakan 10 fold validation  
1. Decision Tree  
![graph6](https://raw.githubusercontent.com/royandhika/classification-mushroom/main/assets/val_tree.png)
2. KNN  
![graph7](https://raw.githubusercontent.com/royandhika/classification-mushroom/main/assets/val_knn.png)
3. Logistic Regression  
![graph7](https://raw.githubusercontent.com/royandhika/classification-mushroom/main/assets/val_log.png)
