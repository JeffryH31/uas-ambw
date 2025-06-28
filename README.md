## 1. Judul Aplikasi: Daily Planner - Flutter App

## 2. Penjelasan Fitur

- **Get Started Screen**: Tampil hanya satu kali saat aplikasi pertama kali diinstal.
- **User Authentication**:
  - Sign Up (Daftar) dengan Email & Password.
  - Sign In (Masuk) dengan akun yang sudah ada.
  - Sign Out (Keluar).
  - Validasi input dan penanganan pesan error.
- **Cloud Database (Firestore)**:
  - Setiap pengguna memiliki daftar tugasnya sendiri.
  - Tambah, lihat, perbarui (tandai selesai), dan hapus tugas.
- **Session Management**:
  - Pengguna tetap login meskipun aplikasi ditutup dan dibuka kembali.

---

## 3. Langkah Install & Build

1.  **Konfigurasi Firebase**:

    - Buat proyek baru di [Firebase Console](https://console.firebase.google.com/).
    - Aktifkan **Authentication** dengan metode **Email/Password**.
    - Buat **Cloud Firestore** database dalam mode produksi dan sesuaikan _Rules_ untuk pengembangan (lihat di bawah).
    - Daftarkan aplikasi Android/iOS Anda dan unduh file konfigurasi (`google-services.json` untuk Android atau `GoogleService-Info.plist` untuk iOS).
    - Letakkan file `google-services.json` di dalam folder `android/app/`.

2.  **Aturan Keamanan Firestore (Rules)**:
    Untuk tujuan pengembangan, gunakan aturan ini agar pengguna yang sudah login dapat membaca/menulis datanya sendiri. Buka `Firestore Database > Rules` dan paste kode berikut:

    ```
    rules_version = '2';
    service cloud.firestore {
      match /databases/{database}/documents {
        // Hanya izinkan pengguna yang login untuk mengakses koleksi 'tasks'
        match /tasks/{taskId} {
          allow read, write: if request.auth != null && request.auth.uid == resource.data.userId;
        }
      }
    }
    ```

3.  **Clone Repositori**:

    ```bash
    git clone [https://github.com/NAMA_USER_ANDA/NAMA_REPO_ANDA.git](https://github.com/NAMA_USER_ANDA/NAMA_REPO_ANDA.git)
    cd NAMA_REPO_ANDA
    ```

4.  **Install Dependencies**:

    ```bash
    flutter pub get
    ```

5.  **Jalankan Aplikasi**:
    ```bash
    flutter run
    ```

---

## 4 .Teknologi yang Digunakan

- **Framework**: Flutter
- **Backend & Database**: Firebase (Authentication & Cloud Firestore)
- **Penyimpanan Lokal**: SharedPreferences (untuk flag Get Started screen)
- **State Management**: Provider
- **Styling**: Google Fonts

---

## 5. Dummy untuk Testing

- **Email**: `user.test@example.com`
- **Password**: `123456`
