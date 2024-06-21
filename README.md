# fp-tka
Final Project Teknologi Komputasi Awan 2024
# KELOMPOK B3 #
| Nama      | NRP         |
  |-----------|-------------|
  | Hazwan Adhikara Nasution | 5027231017   |
  | Rafael Gunawan | 5027231019  |  
  | Haidar Rafi Aqyla  | 5027231029  |
  | Dionisius Marcell Putra Indranto  | 5027231044  |
  | Muhammad Andrean Rizq Prasetio  | 5027231052  |

---
# Permasalahan #
Anda adalah seorang lulusan Teknologi Informasi, sebagai ahli IT, salah satu kemampuan yang harus dimiliki adalah Keampuan merancang, membangun, mengelola aplikasi berbasis komputer menggunakan layanan awan untuk memenuhi kebutuhan organisasi.

Pada suatu saat anda mendapatkan project untuk mendeploy sebuah aplikasi Sentiment Analysis dengan komponen Backend menggunakan python: sentiment-analysis.py.

Kemudian juga disediakan sebuah Frontend sederhana menggunakan index.html dan styles.css dengan tampilan antarmuka sebagai berikut.
![image](https://github.com/haidarRA/fp-tka/assets/149871906/eaad3cf1-0214-492a-b506-6882d98b5e53)

Kemudian anda diminta untuk mendesain arsitektur cloud yang sesuai dengan kebutuhan aplikasi tersebut. Apabila dana maksimal yang diberikan adalah 1 juta rupiah per bulan (65 US$) konfigurasi cloud terbaik seperti apa yang bisa dibuat?

---
# Desain Rancangan Arsitektur Komputasi Awan dan Tabel Harga #
Untuk cloud service provider yang kami gunakan untuk final project ini adalah Digital Ocean karena penggunaannya yang mudah dan harganya yang cukup terjangkau bagi kami.
Berikut adalah desain rancangan arsitektur komputasi awan kami untuk final project ini.
![image](https://github.com/haidarRA/fp-tka/assets/149871906/6519a2c2-4620-495d-b06d-dd0a926b124a)

Untuk tabel harga dari desain rancangan arsitektur komputasi awan kami adalah sebagai berikut.
![tabel harga final](https://github.com/haidarRA/fp-tka/assets/149871906/37452e73-5086-4d69-92c4-27f9bba19e6f)
---
# Implementasi
### 1. Setup MongoDB
![image](https://github.com/haidarRA/fp-tka/assets/143814923/a3227ec5-13c0-41a4-859c-bddfe06cd3ff)

### 2. Setup 2 Droplet 6$ untuk Back-End
![image](https://github.com/haidarRA/fp-tka/assets/143814923/8d28f95f-b7e8-4da7-a3be-5d1485678a41)

![image](https://github.com/haidarRA/fp-tka/assets/143814923/dab1d9c3-dabd-4dfe-9475-e5315bace3f4)

### 3. Setup 1 Droplet 12$ untuk Front-End
![image](https://github.com/haidarRA/fp-tka/assets/143814923/9a6a25ed-02b1-401d-af74-6aa2789f179a)

### 4. Setup Front-End
- Install apache2 dengan command `sudo apt-get install apache2`
- Konfigurasi index.html dan styles.css
- Masukkan command `systemctl restart apache2` untuk restart service apache2 agar konfigurasi bisa terpakai
- Akses web melalui IP Droplet atau IP Loadbalancer

![image](https://github.com/haidarRA/fp-tka/assets/143814923/3cd33dbb-4499-438b-8543-7244f6fe1f72)

![image](https://github.com/haidarRA/fp-tka/assets/143814923/dfb7ed43-7a37-48e1-b337-85e954798f67)

### 5. Setup Back-End
- Install python3 dengan command `sudo apt-get install python3`
- Install dependencies yang diperlukan :
  - `sudo apt-get install python3-pip`
  - `pip install flask`
  - `pip install flask_cors`
  - `pip install textblob`
  - `pip install pymongo`
  - `pip install gunicorn`
- Lakukan konfigurasi terhadap sentiment_analysis.py
- Nyalakan dengan command `gunicorn -b 0.0.0.0:80 sentiment_analysis:app --daemon` agar tetap berjalan ketika device server dimatikan

![image](https://github.com/haidarRA/fp-tka/assets/143814923/eea9f2bc-bfe5-4012-a5fe-ee7df87e152d)

### 6. Locustfile
- Lakukan deploy terhadap locustfile menggunakan `locust -f locustfile.py --host http://(IP backend):80`

# Pengujian API

### 1. Analyze text
- Akses melalui ip-address-frontend/analyze

![image](https://github.com/haidarRA/fp-tka/assets/143814923/711f59ab-c788-4568-9431-cd42f25b3622)

### 2. Retrieve History
- Akses melalui ip-address-backend/history

![image](https://github.com/haidarRA/fp-tka/assets/143814923/3249bb87-a5e8-44fc-9798-334e31b184f5)

# Hasil Load Testing
1. Jumlah RPS maksimum selama 60 detik
![Screenshot from 2024-06-21 12-49-44](https://github.com/haidarRA/fp-tka/assets/149871906/6a6d32ef-f72b-4260-839d-21a5aa1333be)
Untuk mencari jumlah RPS maksimum, berikut adalah konfigurasi locust kami.

* Number of users: 1500

* Users per second: 50

* RPS maksimum: 63,7

* Failures: 0%

2. Jumlah peak concurrency maksimum yang dapat ditangani oleh server dengan spawn rate 50 dan durasi waktu load testing 60 detik
![Screenshot from 2024-06-21 12-54-55](https://github.com/haidarRA/fp-tka/assets/149871906/ca3cf27b-0d98-4449-a217-15f06a247ccb)
Saat pengujian dengan spawn rate 50, didapatkan peak concurrency maksimum 2900 dengan failure 0%.

3. Jumlah peak concurrency maksimum yang dapat ditangani oleh server dengan spawn rate 100 dan durasi waktu load testing 60 detik
![Screenshot from 2024-06-21 12-59-27](https://github.com/haidarRA/fp-tka/assets/149871906/170d0710-bafb-4e19-856f-34a5299b1021)
Saat pengujian dengan spawn rate 50, didapatkan peak concurrency maksimum 5400 dengan failure 0%.

4. Jumlah peak concurrency maksimum yang dapat ditangani oleh server dengan spawn rate 200 dan durasi waktu load testing 60 detik


