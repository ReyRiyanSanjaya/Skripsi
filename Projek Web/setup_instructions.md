
# INSTALASI DAN SETUP APLIKASI FRAUD DETECTION

## 1. Persiapan Environment

### Install Python Dependencies
```bash
pip install -r requirements.txt
```

### Atau install satu per satu:
```bash
pip install Flask==2.3.3
pip install Flask-SQLAlchemy==3.0.5
pip install Flask-Login==0.6.3
pip install Werkzeug==2.3.7
pip install pandas==2.0.3
pip install numpy==1.24.3
pip install scikit-learn==1.3.0
pip install PyMySQL==1.1.0
pip install matplotlib==3.7.2
pip install seaborn==0.12.2
pip install Jinja2==3.1.2
```

## 2. Setup Database MySQL di XAMPP

### Langkah 1: Start XAMPP
1. Buka XAMPP Control Panel
2. Start Apache dan MySQL services
3. Pastikan kedua services berjalan (hijau)

### Langkah 2: Buat Database
1. Buka browser dan akses http://localhost/phpmyadmin
2. Klik "New" di sidebar kiri
3. Buat database baru dengan nama: `fraud_detection`
4. Pilih Collation: `utf8mb4_general_ci`
5. Klik "Create"

### Langkah 3: Verifikasi Koneksi
Database akan otomatis terbuat tablenya saat aplikasi pertama kali dijalankan.

## 3. Struktur Folder Project

```
fraud_detection/
├── app.py                    # Main Flask application
├── requirements.txt          # Python dependencies
├── templates/               # HTML templates
│   ├── base.html
│   ├── login.html
│   ├── dashboard.html
│   ├── training.html
│   ├── survey.html
│   ├── survey_result.html
│   ├── reports.html
│   ├── report_detail.html
│   └── employees.html
├── uploads/                 # Upload folder (auto-created)
├── fraud_model.pkl          # Trained model (auto-created)
└── fraud_scaler.pkl         # Scaler model (auto-created)
```

## 4. Menjalankan Aplikasi

### Langkah 1: Jalankan Flask App
```bash
python app.py
```

### Langkah 2: Akses Aplikasi
Buka browser dan akses: http://localhost:5000

### Langkah 3: Login
**Default Login Credentials:**
- Admin: username=`admin`, password=`admin123`
- Owner: username=`owner`, password=`owner123`

## 5. Fitur Utama Aplikasi

### 1. Dashboard
- Overview statistik fraud detection
- Metrics model performance terbaru
- Grafik dan visualisasi

### 2. Training Model
- Upload file CSV data training
- Training model Random Forest
- Evaluasi performance metrics

### 3. Survey Karyawan
- Form kuisioner fraud diamond
- Prediksi real-time fraud risk
- Hasil assessment individual

### 4. Reports
- Detailed model performance reports
- Confusion matrix dan ROC curves
- Feature importance analysis
- Export capabilities

### 5. Employee Management
- Daftar karyawan dan risk level
- Historical survey data
- Risk categorization

## 6. Format Data Training CSV

File CSV harus memiliki kolom dengan nama persis seperti ini:
```csv
pressure,opportunity,rationalization,capability,lama_bekerja,skor_audit,indikasi_fraud
3,4,2,3,5,75.5,1
2,3,1,2,3,80.0,0
4,5,4,4,7,65.5,1
1,2,1,1,2,85.0,0
```

**Keterangan Kolom:**
- `pressure`: Skala 1-5 (tekanan finansial/personal)
- `opportunity`: Skala 1-5 (kesempatan untuk fraud)
- `rationalization`: Skala 1-5 (rasionalisasi fraud)
- `capability`: Skala 1-5 (kemampuan melakukan fraud)
- `lama_bekerja`: Tahun bekerja (integer)
- `skor_audit`: Skor audit terakhir (float)
- `indikasi_fraud`: Target variable (1=fraud, 0=tidak fraud)

## 7. Troubleshooting

### Error: "No module named 'MySQLdb'"
```bash
pip install PyMySQL
```

### Error: "Access denied for user 'root'@'localhost'"
1. Pastikan MySQL service di XAMPP sudah running
2. Cek konfigurasi database di app.py
3. Pastikan username/password MySQL benar (default XAMPP: root tanpa password)

### Error: "Unknown database 'fraud_detection'"
1. Buat database 'fraud_detection' di phpMyAdmin
2. Restart aplikasi Flask

### Error: "Port 5000 already in use"
Ubah port di app.py bagian akhir:
```python
app.run(debug=True, port=5001)
```

## 8. Security Notes

⚠️ **PENTING untuk Production:**
1. Ganti SECRET_KEY dengan key yang aman
2. Gunakan environment variables untuk database credentials
3. Aktifkan HTTPS
4. Gunakan database user dengan privileges terbatas
5. Implementasi rate limiting
6. Validasi input yang lebih ketat

## 9. Backup Database

### Export Database:
```bash
mysqldump -u root -p fraud_detection > backup.sql
```

### Import Database:
```bash
mysql -u root -p fraud_detection < backup.sql
```