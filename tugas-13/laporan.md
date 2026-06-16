# Laporan Praktikum - Tugas 13: State Management & Notifikasi
**Nama**: Ghilbran Alfaries Pryma  
**NIM**: 2311102267  

---

## 1. Cara Kerja Provider pada Aplikasi

Provider adalah library state management berbasis `InheritedWidget` yang digunakan untuk memisahkan logika bisnis (state) dengan tampilan (UI). Pada aplikasi ini, alur kerja Provider adalah sebagai berikut:

1. **Definisi State (`CounterProvider`)**:  
   Kelas `CounterProvider` dideklarasikan dengan mewarisi `ChangeNotifier`. Kelas ini menyimpan variabel state utama `_counter`.
2. **Pemicu Perubahan (`increment`)**:  
   Ketika tombol **Tambah Counter** ditekan, metode `increment()` dipanggil. Metode ini melakukan penambahan nilai `_counter` dan memanggil `notifyListeners()`.
3. **Pemberitahuan Listener (`notifyListeners`)**:  
   Fungsi `notifyListeners()` mengirimkan sinyal ke seluruh widget yang mendengarkan (subscribe) bahwa terjadi perubahan state.
4. **Penyediaan State (`ChangeNotifierProvider`)**:  
   Di dalam `main.dart`, aplikasi dibungkus menggunakan `ChangeNotifierProvider`, sehingga instans dari `CounterProvider` dapat diakses oleh semua widget di bawahnya (widget tree).
5. **Konsumsi State (`Consumer`)**:  
   Widget `Consumer<CounterProvider>` digunakan di `HomeScreen` untuk mendengarkan perubahan state. Ketika `notifyListeners()` dipanggil, hanya bagian widget di dalam `Consumer` yang akan dibangun ulang (rebuild) secara efisien untuk menampilkan nilai counter terbaru.

---

## 2. Cara Kerja Notifikasi pada Aplikasi

Aplikasi menggunakan paket `flutter_local_notifications` untuk mengirimkan notifikasi lokal secara langsung di dalam perangkat tanpa memerlukan server eksternal (seperti FCM). Cara kerjanya adalah sebagai berikut:

1. **Inisialisasi (`NotificationService.init`)**:  
   Saat aplikasi pertama kali dibuka (di dalam `main.dart`), kelas utility `NotificationService.init()` dipanggil untuk menyiapkan setelan platform. Icon notifikasi diatur menggunakan ikon aplikasi bawaan (`@mipmap/ic_launcher`).
2. **Permintaan Izin (Permission Request)**:  
   Pada perangkat Android 13 ke atas (API level 33+), sistem operasi mewajibkan izin notifikasi secara eksplisit. Aplikasi memicu dialog persetujuan izin (`requestNotificationsPermission()`) saat inisialisasi awal.
3. **Konfigurasi Channel Notifikasi**:  
   Untuk platform Android, notifikasi wajib dikelompokkan ke dalam "Channel" (`AndroidNotificationDetails`). Kita membuat channel bernama `Counter Updates` dengan tingkat kepentingan maksimal (`Importance.max` dan `Priority.high`) agar notifikasi muncul sebagai banner pop-up instan (heads-up) di atas layar.
4. **Pemicuan Notifikasi (`showNotification`)**:  
   Ketika counter bertambah di `CounterProvider`, fungsi `showNotification()` dipanggil. Fungsi ini mengirimkan parameter ID, Judul (`Counter Update`), dan Pesan berisi nilai counter terbaru (`Nilai counter saat ini: X`) ke OS untuk ditampilkan secara real-time di tray notifikasi sistem.
