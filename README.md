# 🎬 Frontend Dashboard

![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/css3-%231572B6.svg?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white)

**AnimeSync** adalah antarmuka web (Frontend) untuk sistem **AniLog**. Aplikasi ini berfungsi sebagai *Client-Side Aggregator* yang menggabungkan data dari dua layanan mikro terpisah: **AniLog Service** (Katalog Anime) dan **Tracker Service** (User Data) menjadi satu tampilan dashboard yang terintegrasi.

## 🌟 Fitur Utama

* **🔍 Real-time Search:** Pencarian judul anime dengan fitur *debounce* untuk mengurangi beban request ke server.
* **📂 My Collection:** Menampilkan daftar tontonan pengguna (Watchlist) yang diambil dari *Tracker Service* dan diperkaya detailnya oleh *AniLog Service*.
* **📄 Anime Details:** Halaman detail yang menampilkan sinopsis, statistik skor, dan genre.
* **💡 Smart Recommendations:** Menampilkan rekomendasi anime serupa berdasarkan algoritma *Content-Based Filtering*.
* **⚡ Lightweight:** Dibangun menggunakan Vanilla JS, HTML, dan CSS tanpa framework berat, dioptimalkan untuk performa tinggi.

## 🏗️ Arsitektur Integrasi

Sistem ini menerapkan pola **Client-Side Aggregation**. Browser pengguna bertugas memanggil dan menggabungkan data dari endpoint yang berbeda:

1.  **GET /anime**: Mengambil metadata katalog dari `AniLog Service`.
2.  **GET /collection**: Mengambil ID anime yang disimpan user dari `Tracker Service`.
3.  **Data Merging**: Frontend mencocokkan ID dari Tracker dengan Metadata dari AniLog untuk merender Sidebar koleksi.

```mermaid
graph LR
    Browser[AnimeSync Frontend]
    ServiceA[AniLog API]
    ServiceB[Tracker API]

    Browser -- 1. Search/Get Details --> ServiceA
    Browser -- 2. Get User Watchlist --> ServiceB
    Browser -- 3. Add to Collection --> ServiceB
