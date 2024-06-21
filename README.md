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

# Hasil Pengujian
1. Jumlah RPS maksimum
![image](https://github.com/haidarRA/fp-tka/assets/149871906/94530114-2ba9-4424-b6ae-c0d96de522da)
Untuk mencari jumlah RPS maksimum, berikut adalah konfigurasi locust kami.

* Number of users: 1000

* Users per second: 50

* RPS maksimum: 30,3

* Failures: 0%

2. 
