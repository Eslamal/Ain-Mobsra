<h1 align="center">📱 Ibsar - Lens Management ERP</h1>

<p align="center">
  <strong>A robust, enterprise-grade Android application tailored for optical centers to manage inventory, host product galleries, and generate dynamic PDF catalogs.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Kotlin-100%25-blue?logo=kotlin" alt="Kotlin">
  <img src="https://img.shields.io/badge/UI-Jetpack%20Compose-success?logo=android" alt="Jetpack Compose">
  <img src="https://img.shields.io/badge/Architecture-Clean%20Architecture%20%2B%20MVVM-orange" alt="Architecture">
  <img src="https://img.shields.io/badge/Backend-Firebase-yellow?logo=firebase" alt="Firebase">
</p>

---

## 📖 Overview

**Ibsar** translates complex inventory data into a seamless mobile experience. Designed specifically for optical centers, the app allows administrators to categorize lenses, input detailed specifications, upload multiple high-resolution images, and export fully styled PDF catalogs directly from the device.

## ✨ Key Features

* **Advanced PDF Engine:** Programmatically generates professional PDF catalogs (spec sheets and grid layouts) with asynchronous image downloading and hardware-acceleration handling.
* **Smart Inventory Management:** Add, update, delete, and quick-edit lens data (Name, Code, Price, Description) across dynamically created categories.
* **Interactive Image Galleries:** Upload multiple images per product with full-screen, swipeable gallery support.
* **Real-Time Filtering:** Instant, state-driven search mechanism across categories and product codes.
* **Secure Authentication:** Integrated Firebase Auth supporting both Email/Password and **Google Sign-In**.
* **Modern UI/UX:** Fully responsive design adapting to mobile and tablet layouts, complete with system-aware Dark/Light mode.

## 🛠️ Tech Stack & Architecture

This project was built with scalability and maintainability in mind, strictly adhering to **Clean Architecture** principles and the **MVVM** design pattern.

* **Language:** Kotlin
* **UI Framework:** Jetpack Compose (Material Design 3)
* **Dependency Injection:** Dagger Hilt
* **Asynchronous Operations:** Kotlin Coroutines & StateFlow
* **Image Processing:** Coil
* **Backend as a Service (BaaS):** * Firebase Authentication
  * Cloud Firestore (NoSQL Database)
  * Firebase Cloud Storage
* **PDF Generation:** Native Android `PdfDocument` API

---

## 📸 Screenshots

*(Replace the placeholder links below with your actual screenshot links)*

| Home & Categories | Lens Grid & Search | Details & Gallery |
| :---: | :---: | :---: |
| <img src="LINK_1" width="220"/> | <img src="LINK_2" width="220"/> | <img src="LINK_3" width="220"/> |
| **Dark Mode Support** | **Quick Edit Dialog** | **Generated PDF Output** |
| <img src="LINK_4" width="220"/> | <img src="LINK_5" width="220"/> | <img src="LINK_6" width="220"/> |

---

## ⚙️ Running the Project

To run this project locally, you need to configure your own Firebase environment:

1. Clone this repository.
2. Create a new project in the [Firebase Console](https://console.firebase.google.com/).
3. Enable **Authentication** (Email/Password & Google), **Firestore**, and **Storage**.
4. Download the `google-services.json` file and place it in the `app/` directory.
5. Add your machine's `SHA-1` and `SHA-256` keys to the Firebase project settings to enable Google Sign-In.
6. Build and run the project via Android Studio.

---

## 👨‍💻 Developer

Developed by **Eslam Ali**
* 💼 **LinkedIn:** [Insert Your LinkedIn Link]
* 📧 **Email:** [Insert Your Email]
* 🛠️ **Role:** Android Software Engineer
