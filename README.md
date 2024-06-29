# Final Project Teknologi Komputasi Awan
TKA Kelas B
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
![WhatsApp Image 2024-06-25 at 22 55 21_06b9f5f8](https://github.com/v0rein/fp-tka/assets/143814923/c70fc200-9a0e-47f8-a206-59e63029af2e)

Untuk tabel harga dari desain rancangan arsitektur komputasi awan kami adalah sebagai berikut.
![WhatsApp Image 2024-06-25 at 22 55 25_f8d72088](https://github.com/v0rein/fp-tka/assets/143814923/da3e2c84-644c-4bf0-ac88-f524e88d4bab)

---
# Implementasi
### 1. Setup MongoDB
![image](https://github.com/haidarRA/fp-tka/assets/143814923/a3227ec5-13c0-41a4-859c-bddfe06cd3ff)

### 2. Setup 2 Droplet 8$ untuk Back-End
![image](https://github.com/v0rein/fp-tka/assets/143814923/bf75806d-f4ba-48d1-b360-4084ceb11622)

![image](https://github.com/v0rein/fp-tka/assets/143814923/379990eb-747a-43c8-a2ac-39adec756cb7)

### 3. Setup 1 Droplet 8$ untuk Front-End
![image](https://github.com/v0rein/fp-tka/assets/143814923/23e35837-6a4b-4465-974e-a12854ea0b81)

### 4. Setup Front-End
- Install apache2 dengan command `sudo apt-get install apache2`
- Konfigurasi index.html dan styles.css
- Masukkan command `systemctl restart apache2` untuk restart service apache2 agar konfigurasi bisa terpakai
- Akses web melalui IP Droplet atau IP Loadbalancer

![image](https://github.com/haidarRA/fp-tka/assets/143814923/3cd33dbb-4499-438b-8543-7244f6fe1f72)

![image](https://github.com/v0rein/fp-tka/assets/143814923/731324d4-027e-4733-bb5a-7d0b5d5888aa)

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
- Nyalakan dengan command `gunicorn -b 0.0.0.0:5000 sentiment_analysis:app --daemon` agar tetap berjalan ketika device server dimatikan

![image](https://github.com/v0rein/fp-tka/assets/143814923/0f675575-e283-4fc0-82ae-f6185d95401c)

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
Apabila kita mencari rps maksimum secara rata-rata maka hasilnya kita dapatkan pada peak concurrency 4000 user dengan spawn rate 100
![image](https://github.com/haidarRA/fp-tka/assets/143814923/6b496578-16c2-430a-963f-3dde57b3a693)
Kita mendapat rata-rata RPS yaitu 124,5.
Sedangkan apabila kita mencari rps maksimum atau peak rps maka hasilnya kita dapatkan pada peak concurrency 1500 user dengan spawn rate 500
![image](https://github.com/haidarRA/fp-tka/assets/143814923/b49e5535-fe1a-4fa8-9f85-a1deb8781647)
Kita mendapat peak RPS di 290,71.

3. Jumlah peak concurrency maksimum yang dapat ditangani oleh server dengan spawn rate 50 dan durasi waktu load testing 60 detik
![image](https://github.com/haidarRA/fp-tka/assets/143814923/c71bca16-3b4c-4066-968b-d7672769f038)

Saat pengujian dengan spawn rate 50, didapatkan peak concurrency maksimum 5000 dengan failure 0% serta peak RPS 215,9 dengan rata-rata rps 118,5.

3. Jumlah peak concurrency maksimum yang dapat ditangani oleh server dengan spawn rate 100 dan durasi waktu load testing 60 detik
![image](https://github.com/haidarRA/fp-tka/assets/143814923/6b496578-16c2-430a-963f-3dde57b3a693)

Saat pengujian dengan spawn rate 100, didapatkan peak concurrency maksimum 4000 dengan failure serta rata-rata RPS 124,5 dengan peak RPS 239,8.

4. Jumlah peak concurrency maksimum yang dapat ditangani oleh server dengan spawn rate 200 dan durasi waktu load testing 60 detik
![image](https://github.com/haidarRA/fp-tka/assets/143814923/0df46e05-3a3f-43fd-9026-6d64de8a6405)

Saat pengujian dengan spawn rate 200, didapatkan peak concurrency maksimum 3000 dengan failure 0% serta rata-rata RPS 88,7 dengan peak RPS 285,3.

5. Jumlah peak concurrency maksimum yang dapat ditangani oleh server dengan spawn rate 500 dan durasi waktu load testing 60 detik
![image](https://github.com/haidarRA/fp-tka/assets/143814923/b49e5535-fe1a-4fa8-9f85-a1deb8781647)

Saat pengujian dengan spawn rate 500, didapatkan peak concurrency maksimum 1500 dengan failure 0% serta rata-rata RPS 107,4 dengan peak RPS 290,71.
# Kesimpulan
Berdasarkan pengetesan yang kita lakukan menggunakan locust yang telah disediakan, ada beberapa faktor yang memengaruhi pengetesan tersebut yaitu koneksi internet, peak concurrency yang diinput, spawn rate dalam bentuk users/second yang diinput serta spesifikasi dari vm yang akan diisi dengan backend. Lalu dalam pengetesan ini juga kami menggunakan mongodb Compass yang merupakan GUI dari jenis database yang kita gunakan untuk menghapus data dari pengetesan sebelumnya untuk melakukan pengetesan baru agar optimal.

Berdasarkan pengetesan yang kita dapat juga bisa diambil bahwa semakin banyak spawn rate yang kita gunakan, semakin kecil peak concurrency dari stress test ini lalu RPS atau Request Per Second akan semakin tinggi.
Apabila dalam projek kedepannya diperlukan vm serta pengujian yang mementingkan titik kerja dalam backend maka kita memerlukan vm yang diperuntukkan dalam keperluan backend yang lebih banyak dan membuat load balancer untuk vm-vm tersebut serta membuat vm-vm yang diperlukan untuk back-end tersebut dengan spesifikasi yang maksimal serta storage yang cukup untuk keperluan database.

# Link Video Demo
https://youtu.be/vkOEGvMzrnw
