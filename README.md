# DJobs - Aplikasi Pencari Lowongan Kerja Android

Bahasa: [Indonesia](README.md) | [English](README_EN.md)

DJobs adalah aplikasi Android untuk mencari dan menyimpan informasi lowongan pekerjaan yang bersumber dari platform Dicoding Jobs. Aplikasi ini dibangun dengan menerapkan prinsip Clean Architecture dan berbagai praktik terbaik pengembangan Android modern.

---

## Fitur Utama

- **Daftar Lowongan Kerja** - Menampilkan daftar lowongan pekerjaan secara real-time dari API Dicoding Jobs.
- **Detail Lowongan** - Melihat informasi lengkap suatu lowongan, termasuk deskripsi pekerjaan, lokasi, tipe pekerjaan, pengalaman minimum, logo perusahaan, dan tautan untuk melamar secara langsung.
- **Favorit** - Menyimpan dan mengelola lowongan favorit secara lokal menggunakan Room Database. Fitur ini diimplementasikan sebagai Dynamic Feature Module.
- **Splash Screen** - Tampilan pembuka saat aplikasi pertama kali dijalankan.
- **Loading Animation** - Animasi Lottie sebagai indikator pemuatan data.

---

## Arsitektur dan Teknologi

Proyek ini menggunakan pola **Clean Architecture** yang dipisahkan menjadi tiga modul utama:

| Modul | Deskripsi |
|---|---|
| `app` | Modul utama yang berisi lapisan presentasi (UI, ViewModel, DI) |
| `core` | Modul pustaka yang berisi domain, data, dan logika bisnis |
| `favorite` | Dynamic Feature Module untuk fitur penyimpanan favorit |

### Tumpukan Teknologi

- **Bahasa**: Kotlin
- **Arsitektur**: Clean Architecture (Data, Domain, Presentation Layer)
- **Dependency Injection**: Koin
- **Jaringan**: Retrofit 2 + OkHttp (dengan SSL/Certificate Pinning)
- **Database Lokal**: Room + SQLCipher (database terenkripsi)
- **Concurrency**: Kotlin Coroutines & Flow
- **Pemuatan Gambar**: Glide
- **Animasi**: Lottie
- **Dynamic Feature**: Google Play Core (SplitInstall)
- **Keamanan**: SSL Certificate Pinning, Enkripsi Database (SQLCipher), ProGuard/R8 Obfuscation
- **Debug Tools**: Chucker (HTTP Inspector), LeakCanary (Memory Leak Detector)
- **Minimum SDK**: 21 (Android 5.0 Lollipop)
- **Target SDK**: 34 (Android 14)

### Lapisan Arsitektur

```
Presentation Layer (app)
        |
    Domain Layer (core)
    - UseCase / Interactor
    - Repository Interface
    - Domain Model
        |
    Data Layer (core)
    - Repository Implementation
    - Remote Data Source (Retrofit)
    - Local Data Source  (Room)
    - Data Mapper
```

---

## Keamanan

Aplikasi ini menerapkan beberapa lapisan keamanan:

- **SSL Certificate Pinning**: Memastikan komunikasi jaringan hanya terjadi dengan server yang terpercaya (`jobs.dicoding.com`).
- **Enkripsi Database**: Semua data lokal dienkripsi menggunakan SQLCipher untuk melindungi data pengguna yang tersimpan.
- **Code Obfuscation**: ProGuard/R8 aktif pada build `release` maupun `debug` untuk mempersulit rekayasa balik.

---

## Cara Memulai

### Prasyarat

- Android Studio Hedgehog atau yang lebih baru
- JDK 8 atau yang lebih baru
- Koneksi internet aktif

### Langkah Instalasi

1. Clone repositori ini:
   ```bash
   git clone https://github.com/alhifnywahid/djobs-android.git
   ```

2. Buka proyek di Android Studio.

3. Tunggu proses Gradle Sync selesai.

4. Jalankan aplikasi pada emulator atau perangkat fisik melalui menu **Run > Run 'app'**.

---

## Struktur Proyek

```
expert/
├── app/                            # Modul aplikasi utama
│   └── src/main/
│       ├── di/                     # Konfigurasi Dependency Injection (Koin)
│       └── presentation/
│           ├── home/               # Layar daftar lowongan
│           └── detail/             # Layar detail lowongan
│
├── core/                           # Modul pustaka inti
│   └── src/main/
│       ├── data/
│       │   └── source/
│       │       ├── local/          # Room DAO, Entity, Database
│       │       └── remote/         # Retrofit ApiService, NetworkBoundSource
│       ├── domain/
│       │   ├── model/              # Model domain (Jobs, dll.)
│       │   ├── repository/         # Antarmuka Repository
│       │   └── usecase/            # UseCase / Interactor
│       ├── ui/                     # Adapter RecyclerView
│       └── utils/                  # Helper & DataMapper
│
└── favorite/                       # Dynamic Feature Module favorit
    └── src/main/
        ├── di/                     # Modul Koin untuk fitur favorit
        └── presentation/           # Layar daftar favorit
```

---

## API

Aplikasi ini mengonsumsi **Dicoding Jobs API**:

- **Base URL**: `https://jobs.dicoding.com/api/`
- **GET** `/vacancies` - Mendapatkan daftar lowongan kerja
- **GET** `/vacancies/detail?id={id}` - Mendapatkan detail lowongan berdasarkan ID

---

## Lisensi

Proyek ini dilisensikan di bawah **MIT License**. Lihat berkas [LICENSE](LICENSE) untuk informasi selengkapnya.

---

## Pembuat

Dibuat oleh **Alhifny Wahid**
