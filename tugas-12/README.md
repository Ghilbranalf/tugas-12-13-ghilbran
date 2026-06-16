# 📱 Praktikum 12 — Kamera & Notifikasi

Aplikasi Flutter sederhana untuk praktikum mata kuliah Pengembangan Aplikasi Berbasis Platform (ABP) yang mengimplementasikan akses kamera perangkat, pemilihan foto dari galeri, dan notifikasi lokal.

---

## 👤 Identitas Mahasiswa

| Atribut | Keterangan |
|---|---|
| Nama | Ghilbran Alfaries Pryma |
| NIM | 2311102267 |
| Mata Kuliah | Pemrograman Aplikasi Berbasis Platform |
| Pertemuan | Praktikum 12 |

---

## ✨ Fitur

- **Kamera Perangkat** — Mengambil foto secara langsung menggunakan `camera` package.
- **Galeri Foto** — Memilih foto dari galeri lokal dengan `image_picker`.
- **Preview Gambar** — Menampilkan foto yang berhasil diambil/dipilih di halaman utama dengan desain elegan.
- **Notifikasi Lokal** — Menampilkan notifikasi lokal instan setiap kali foto berhasil diambil atau dipilih menggunakan `flutter_local_notifications`.
- **Tes Notifikasi** — Tombol pintas pada AppBar untuk memicu pengujian notifikasi secara manual.

---

## 🛠️ Teknologi & Dependensi

- **Flutter SDK**
- **camera** (Akses API Kamera)
- **image_picker** (Akses Galeri Gambar)
- **flutter_local_notifications** (Sistem Notifikasi Lokal)

---

## 📁 Struktur Project (Restructured)

```
lib/
├── main.dart                       # Entry point aplikasi & inisialisasi awal
├── screens/
│   ├── home_screen.dart            # Halaman Utama dengan UI Premium
│   └── camera_screen.dart          # Halaman Preview & Capture Kamera
└── services/
    └── notification_service.dart   # Manajemen Notifikasi Lokal
```
