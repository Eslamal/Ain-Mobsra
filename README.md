# 📱 Ain Mubsira App - Enterprise Optometry & Clinic Management System

A production-ready, Enterprise-Level Android application custom-built for **"Ain Mubsira Center" (مركز عين مبصرة)** in Saudi Arabia. The system digitalizes the entire clinic workflow—from advanced optical measurements and lens inventory cataloging to live license control, offline-first synchronization, and hardware-level thermal prescription printing.

---

## 📸 Screenshots & UI 

<div align="center">

| | | |
|:---:|:---:|:---:|
| <img src="screens/1.jpg" width="250" /> | <img src="screens/2.jpg" width="250" /> | <img src="screens/3.jpg" width="250" /> |
| <img src="screens/4.jpg" width="250" /> | <img src="screens/5.jpg" width="250" /> | <img src="screens/6.jpg" width="250" /> |
| <img src="screens/7.jpg" width="250" /> | <img src="screens/8.jpg" width="250" /> | <img src="screens/9.jpg" width="250" /> |
| <img src="screens/10.jpg" width="250" /> | <img src="screens/11.jpg" width="250" /> | <img src="screens/12.jpg" width="250" /> |
| <img src="screens/13.jpg" width="250" /> | <img src="screens/14.jpg" width="250" /> | <img src="screens/15.jpg" width="250" /> |
| <img src="screens/16.jpg" width="250" /> | <img src="screens/17.jpg" width="250" /> | <img src="screens/18.jpg" width="250" /> |
| <img src="screens/19.jpg" width="250" /> | <img src="screens/20.jpg" width="250" /> | <img src="screens/21.jpg" width="250" /> |
| <img src="screens/22.jpg" width="250" /> | 
</div>
---

## 🎯 Core Problems Solved for Ain Mubsira Center

1. **Slow Prescription Writing:** Doctors previously spent valuable time rewriting identical drug lists and diagnostic statements. The built-in **Smart Templates Manager** allows prescribing with a single tap.
2. **Scattered Patient History:** Tracking whether a patient's vision (SPH/CYL) has deteriorated over months used to require manual paperwork. The app provides a localized **Medical History Timeline** comparing previous measurements instantly.
3. **Hardware & Arabic Text Incompatibility:** POS thermal printers natively distort Arabic font connections. Our customized bitmap graphics pipeline bypasses hardware limitations to output pristine Arabic receipts.
4. **Internet Instability in Medical Rooms:** X-ray or shielded concrete exam rooms often drop Wi-Fi signals. The app uses a strict **Offline-First Cache Architecture** ensuring zero downtime.

---

## 🛠️ Tech Stack & Advanced Architecture

* **UI Toolkit:** Jetpack Compose (Modern Material Design 3 utilizing Custom Glassmorphism UI wrappers).
* **Architecture:** Strict Clean Architecture (Separated Data, Domain, and Presentation layers) paired with MVVM.
* **Reactive Stream & Async Pipeline:** Kotlin Coroutines, StateFlow, SharedFlow, and cold Flow wrappers (`callbackFlow`).
* **Dependency Injection:** Dagger Hilt (Custom scoped components for continuous app stability).
* **Database & Cloud Management:** 
  * Firebase Cloud Firestore (Configured with a persistent 100MB offline hardware cache).
  * Firebase Authentication & Cloud Storage.
  * Firebase Crashlytics (For remote, real-time telemetry and crash monitoring).
* **External Integration & Rendering:** Google ZXing (Dynamic QR Code generation), Native Android `PdfDocument` engine, and Bluetooth ESC/POS terminal drivers.

---

## 🚨 Technical Challenges Faced & Resolutions

### 1. Memory Leaks and 'Unresolved Reference: awaitClose' in FireStore Flows
* **The Issue:** Attempting to stream real-time patient documents directly into the presentation state using standard asynchronous listeners caused memory leaks because listeners remained active after screen destruction. Trying to wrap them inside a `callbackFlow` block resulted in compilation errors due to missing channel lifecycle extensions.
* **The Resolution:** Imported `kotlinx.coroutines.channels.awaitClose` and refactored the stream into a clean reactive API wrapper. The Firestore `addSnapshotListener` is now strictly unregistered inside the `awaitClose` closure block, safeguarding the channel from memory leakage during runtime recompositions.

### 2. Disconnecting Real-Time Licensing (Global Live Kill-Switch)
* **The Issue:** Initially, checking the remote SaaS license subscription was bound directly to the `ActivationScreen`'s lifecycle. Once the user passed validation and navigated to the Dashboard, the screen’s `ViewModel` cleared out, effectively killing the snapshot listener. If a client's license was suspended remotely mid-session, they could continue using the app indefinitely until a manual restart.
* **The Resolution:** Implemented state-hoisting by moving the `LicenseViewModel` directly into the root `IbsarNavGraph` scope. By coupling an active app-wide `LaunchedEffect` block with an instantaneous `popUpTo(0)` navigational wipeout, the application now enforces real-time license suspension within milliseconds across any operational view.

### 3. Multi-Input Rendering Bottlenecks & UX Flow Sluggishness
* **The Issue:** Capturing comprehensive optometry results involves managing over 20 concurrent textual variables (SPH, CYL, AXIS for distance and near sight across both eyes). Relying on separate `remember { mutableStateOf("") }` constructs caused aggressive state overhead and fragmented recompositions, while shifting focus manually between fields degraded clinical efficiency.
* **The Resolution:** Bundled all atomic properties into a singular, immutable immutable data structural record named `ExaminationUiState`. Input fields were equipped with a standardized keyboard focus dispatcher mapping `ImeAction.Next` actions to localized `FocusManager` shifts, decreasing the form-completion time by roughly 70%.

### 4. Arabic Typography Distortion & Custom Printing on 58mm Devices
* **The Issue:** Standard low-cost 58mm Bluetooth thermal printers lack internal glyph libraries for standard right-to-left connected Arabic text layouts, outputting broken, reversed characters.
* **The Resolution:** Developed a programmatic raster graphics rendering channel. The system takes text strings, maps them onto a custom programmatic `StaticLayout` with specific geometric dimensions, renders the company logos, appends a dynamically built client metadata `QR Code` using Google ZXing, draws everything onto a white-background graphics `Canvas` bitmap image, and converts the pixel brightness values straight into hard-coded ESC/POS binary matrix command arrays (`GS v 0`).

---

## ⚙️ Setup Instructions

To run this project locally, please ensure the following steps are completed when setting up the project on a new machine:

1. **Firebase Configuration:** * Download the latest `google-services.json` file from your Firebase Console.
   * Place it inside the `app/` directory. *(Note: This file is git-ignored for security)*.
2. **SHA-1 Fingerprint:**
   * To enable Google Sign-In, ensure your local machine's `SHA-1` and `SHA-256` fingerprints are added to the Firebase Project settings.
3. **Database Security Rules:**
   * Ensure Firestore and Storage security rules are configured to allow read/write access only to authenticated users.

---

## 📌 Future Enhancements (V2.0 Roadmap)
- [ ] **Bulk Import:** Implement Excel/CSV parsing to upload hundreds of lenses simultaneously.
- [ ] **Barcode/QR Scanner:** Integrate camera scanning for instant lens retrieval.
- [ ] **Stock Management:** Add inventory tracking with low-stock alerts.
- [ ] **POS & Invoicing:** Build a cart system to generate client invoices directly from the app.

---

## 👨‍💻 Developer
**Eslam Ali**
* Android Software Engineer
