# Laporan Penjelasan Source Code & Widget
## Praktikum 12 — Notifikasi & API Perangkat Keras

**Identitas Mahasiswa:**
* **Nama**: Ghilbran Alfaries Pryma
* **NIM**: 2311102267
* **Mata Kuliah**: Pemrograman Aplikasi Berbasis Platform

---

### 1. Struktur Folder (Restructured)
Untuk menjaga keterbacaan, kebersihan kode (*clean code*), dan memisahkannya dari milik mahasiswa lain, struktur proyek dipecah menjadi beberapa bagian modular:

* `lib/main.dart` — Titik awal (entrypoint) jalannya aplikasi dan inisialisasi awal.
* `lib/services/notification_service.dart` — Utility kelas yang membungkus fungsi inisialisasi dan pemanggilan notifikasi lokal.
* `lib/screens/home_screen.dart` — Layar utama yang memuat UI Identitas, Container preview gambar, serta tombol aksi.
* `lib/screens/camera_screen.dart` — Layar pemotretan langsung menggunakan kamera perangkat.

---

### 2. Penjelasan Singkat File & Widget

#### A. `main.dart`
* **`main()`**: Fungsi utama bertipe *asynchronous* yang memanggil `WidgetsFlutterBinding.ensureInitialized()` untuk memastikan framework Flutter siap, lalu menginisialisasi `NotificationService` sebelum menjalankan aplikasi.
* **`MyApp` (StatelessWidget)**: Mengembalikan widget `MaterialApp` dengan skema warna berbasis `Color(0xFF6366F1)` (Indigo) dan mengatur halaman pembuka (`home`) menuju `HomeScreen`.

#### B. `services/notification_service.dart`
* **`NotificationService`**: Kelas pembungkus untuk memanipulasi local notifications.
* **`initialize()`**: Menyiapkan pengaturan notifikasi lokal untuk Android (`AndroidInitializationSettings`) menggunakan icon launcher default, dan secara otomatis meminta izin notifikasi untuk perangkat Android 13 ke atas (`requestNotificationsPermission`).
* **`showNotification()`**: Menampilkan notifikasi instan secara *head-up* (prioritas tinggi) menggunakan pengaturan channel tertentu (`ghilbran_kamera_notif_channel`).

#### C. `screens/home_screen.dart`
* **`HomeScreen` (StatefulWidget)**: Menampung state dari media yang diambil (`_imageFile`) dan menampilkan tata letak halaman utama.
* **`_takePhoto()`**: Metode untuk berpindah ke layar kamera (`CameraScreen`) guna mengambil gambar. Setelah gambar berhasil diambil, state `_imageFile` diperbarui dan notifikasi lokal dipicu.
* **`_pickImage()`**: Metode untuk membuka galeri foto lokal menggunakan plugin `image_picker`. Jika foto dipilih, state diperbarui dan notifikasi lokal dipicu.
* **`Identity Card` (Container)**: Berisi informasi identitas mahasiswa (Nama dan NIM) dengan desain premium bermotif gradasi warna Indigo ke Violet.
* **`Preview Container`**: Menampilkan preview foto jika `_imageFile` tidak bernilai null, atau ikon placeholder jika foto belum dipilih.
* **`Kamera & Galeri Buttons`**: Tombol aksi berdesain premium modern untuk memicu pemotretan kamera atau pemilihan galeri.

#### D. `screens/camera_screen.dart`
* **`CameraScreen` (StatefulWidget)**: Digunakan untuk berinteraksi langsung dengan API Kamera perangkat.
* **`_setupCameras()`**: Mencari daftar kamera yang tersedia pada perangkat fisik, menggunakan kamera belakang (`cameras.first`), lalu menginisialisasinya.
* **`CameraPreview`**: Widget bawaan package `camera` yang merender tangkapan lensa kamera secara real-time ke layar.
* **`Capture Button`**: Tombol lingkaran putih di bagian bawah layar untuk memicu fungsi `_capturePhoto()` yang menyimpan berkas gambar sementara dan mengembalikannya ke `HomeScreen` via `Navigator.pop`.
