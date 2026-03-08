# DJobs - Android Job Search Application

Language: [Indonesia](README.md) | [English](README_EN.md)

DJobs is an Android application for searching and bookmarking job vacancy information sourced from the Dicoding Jobs platform. The application is built by applying Clean Architecture principles and various modern Android development best practices.

---

## Key Features

- **Job Listing** - Displays a real-time list of job vacancies from the Dicoding Jobs API.
- **Job Detail** - View complete information for a vacancy, including job description, location, job type, minimum experience, company logo, and a direct link to apply.
- **Favorites** - Save and manage favorite vacancies locally using Room Database. This feature is implemented as a Dynamic Feature Module.
- **Splash Screen** - A welcoming intro screen shown when the application first launches.
- **Loading Animation** - Lottie animation as a data loading indicator.

---

## Architecture and Technology

This project uses the **Clean Architecture** pattern, separated into three main modules:

| Module | Description |
|---|---|
| `app` | The main application module containing the presentation layer (UI, ViewModel, DI) |
| `core` | A library module containing the domain, data layer, and business logic |
| `favorite` | A Dynamic Feature Module for the favorites functionality |

### Technology Stack

- **Language**: Kotlin
- **Architecture**: Clean Architecture (Data, Domain, Presentation Layer)
- **Dependency Injection**: Koin
- **Networking**: Retrofit 2 + OkHttp (with SSL/Certificate Pinning)
- **Local Database**: Room + SQLCipher (encrypted database)
- **Concurrency**: Kotlin Coroutines & Flow
- **Image Loading**: Glide
- **Animation**: Lottie
- **Dynamic Feature**: Google Play Core (SplitInstall)
- **Security**: SSL Certificate Pinning, Database Encryption (SQLCipher), ProGuard/R8 Obfuscation
- **Debug Tools**: Chucker (HTTP Inspector), LeakCanary (Memory Leak Detector)
- **Minimum SDK**: 21 (Android 5.0 Lollipop)
- **Target SDK**: 34 (Android 14)

### Architecture Layers

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

## Security

The application applies several layers of security:

- **SSL Certificate Pinning**: Ensures network communication only occurs with the trusted server (`jobs.dicoding.com`).
- **Database Encryption**: All local data is encrypted using SQLCipher to protect stored user data.
- **Code Obfuscation**: ProGuard/R8 is active on both `release` and `debug` builds to hinder reverse engineering.

---

## Getting Started

### Prerequisites

- Android Studio Hedgehog or newer
- JDK 8 or newer
- An active internet connection

### Installation Steps

1. Clone this repository:
   ```bash
   git clone https://github.com/alhifnywahid/djobs-android.git
   ```

2. Open the project in Android Studio.

3. Wait for the Gradle Sync process to complete.

4. Run the application on an emulator or physical device via **Run > Run 'app'**.

---

## Project Structure

```
expert/
├── app/                            # Main application module
│   └── src/main/
│       ├── di/                     # Dependency Injection configuration (Koin)
│       └── presentation/
│           ├── home/               # Job listing screen
│           └── detail/             # Job detail screen
│
├── core/                           # Core library module
│   └── src/main/
│       ├── data/
│       │   └── source/
│       │       ├── local/          # Room DAO, Entity, Database
│       │       └── remote/         # Retrofit ApiService, NetworkBoundSource
│       ├── domain/
│       │   ├── model/              # Domain models (Jobs, etc.)
│       │   ├── repository/         # Repository interface
│       │   └── usecase/            # UseCase / Interactor
│       ├── ui/                     # RecyclerView Adapter
│       └── utils/                  # Helpers & DataMapper
│
└── favorite/                       # Favorites Dynamic Feature Module
    └── src/main/
        ├── di/                     # Koin module for the favorites feature
        └── presentation/           # Favorites list screen
```

---

## API

This application consumes the **Dicoding Jobs API**:

- **Base URL**: `https://jobs.dicoding.com/api/`
- **GET** `/vacancies` - Retrieve a list of job vacancies
- **GET** `/vacancies/detail?id={id}` - Retrieve job detail by ID

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for more details.

---

## Author

Created by **Alhifny Wahid**
