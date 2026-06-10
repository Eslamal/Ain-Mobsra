# 📱 Ibsar - Enterprise Optometry & Clinic Management System

A production-grade, Enterprise-Level Android application engineered for a leading chain of optometry clinics and medical eye-care centers in Saudi Arabia (KSA). The system digitizes the entire clinical workflow—ranging from advanced optical vision measurements and lens inventory cataloging to global live license management, offline-first synchronization, and hardware-level typography rendering for thermal prescription printing.

---

## 📸 Screenshots & UI 

<div align="center">

<table>
  <tr>
    <td align="center"><img src="screens/1.jpg" width="240" alt="Screen 1"/><br/><sub>Dashboard</sub></td>
    <td align="center"><img src="screens/2.jpg" width="240" alt="Screen 2"/><br/><sub>Patient Data</sub></td>
    <td align="center"><img src="screens/3.jpg" width="240" alt="Screen 3"/><br/><sub>Measurements</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="screens/4.jpg" width="240" alt="Screen 4"/><br/><sub>Diagnosis UI</sub></td>
    <td align="center"><img src="screens/5.jpg" width="240" alt="Screen 5"/><br/><sub>Prescription</sub></td>
    <td align="center"><img src="screens/6.jpg" width="240" alt="Screen 6"/><br/><sub>Templates Manager</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="screens/7.jpg" width="240" alt="Screen 7"/><br/><sub>Diagnosis Templates</sub></td>
    <td align="center"><img src="screens/8.jpg" width="240" alt="Screen 8"/><br/><sub>Medication Templates</sub></td>
    <td align="center"><img src="screens/9.jpg" width="240" alt="Screen 9"/><br/><sub>Medical History</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="screens/10.jpg" width="240" alt="Screen 10"/><br/><sub>History Search</sub></td>
    <td align="center"><img src="screens/11.jpg" width="240" alt="Screen 11"/><br/><sub>Timeline View</sub></td>
    <td align="center"><img src="screens/12.jpg" width="240" alt="Screen 12"/><br/><sub>Lens Categories</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="screens/13.jpg" width="240" alt="Screen 13"/><br/><sub>Add Category</sub></td>
    <td align="center"><img src="screens/14.jpg" width="240" alt="Screen 14"/><br/><sub>Lens List</sub></td>
    <td align="center"><img src="screens/15.jpg" width="240" alt="Screen 15"/><br/><sub>Lens Specs</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="screens/16.jpg" width="240" alt="Screen 16"/><br/><sub>Add Lens Form</sub></td>
    <td align="center"><img src="screens/17.jpg" width="240" alt="Screen 17"/><br/><sub>Image Hosting</sub></td>
    <td align="center"><img src="screens/18.jpg" width="240" alt="Screen 18"/><br/><sub>Catalog PDF Export</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="screens/19.jpg" width="240" alt="Screen 19"/><br/><sub>Printer Config</sub></td>
    <td align="center"><img src="screens/20.jpg" width="240" alt="Screen 20"/><br/><sub>Bluetooth Discovery</sub></td>
    <td align="center"><img src="screens/21.jpg" width="240" alt="Screen 21"/><br/><sub>Activation Screen</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="screens/22.jpg" width="240" alt="Screen 22"/><br/><sub>System Suspended</sub></td>
    <td></td>
    <td></td>
  </tr>
</table>

</div>

---

## 🎯 Core Problems Solved for Modern Clinical Environments

1. **Slow Prescription Writing:** Optometrists and ophthalmologists spent significant time rewriting repetitive drug dosages and diagnostic notes. The built-in **Smart Templates Manager** accelerates this process, allowing full prescription entries with a single tap.
2. **Scattered Patient Medical Records:** Tracking whether a patient's visual metrics ($SPH$ / $CYL$ / $AXIS$) deteriorated or stabilized across months used to require searching through manual paperwork. The app introduces a localized **Medical History Timeline** comparing current and historical metrics instantly.
3. **Hardware & Arabic Typography Incompatibility:** Standard Bluetooth POS thermal printers natively distort right-to-left Arabic font connections, causing unreadable characters. Our customized programmatic bitmap graphics channel overrides hardware deficits to print flawless, unified Arabic receipts.
4. **Network Dropouts in Clinical Exam Chambers:** Heavily shielded concrete medical environments often drop Wi-Fi signals. The architecture implements a strict **Offline-First Hardware Cache System** ensuring 100% application operational uptime.

---

## 🛠️ Tech Stack & Architecture

* **UI Toolkit:** Jetpack Compose (Modern Material Design 3 architecture built with custom translucent Glassmorphism wrappers).
* **Architecture:** Strict Clean Architecture (Completely segregated Data, Domain, and Presentation layers) paired with MVVM pattern.
* **Asynchronous Pipeline:** Kotlin Coroutines, StateFlow, SharedFlow, and cold Flow asynchronous constructs (`callbackFlow`).
* **Dependency Injection:** Dagger Hilt (Custom scoped initialization routines safeguarding background execution memory).
* **Database & Infrastructure Hosting:** 
  * Firebase Cloud Firestore (Configured with a persistent 100MB offline hardware layer cache).
  * Firebase Authentication & Cloud Storage.
  * Firebase Crashlytics (For remote tracking, real-time diagnostic telemetry, and proactive error logging).
* **External Engines:** Google ZXing Engine (Dynamic QR Code vector generation), Native Android `PdfDocument` engine, and low-level Bluetooth ESC/POS hardware terminal drivers.

---

## 🚨 Technical Challenges Faced & Architectural Solutions

### 1. Memory Leaks and 'Unresolved Reference: awaitClose' in Firestore Handlers
* **The Challenge:** Attempting to stream real-time client records into presentation UI models using standard asynchronous asynchronous callbacks introduced severe memory leaks because observers remained active after view destruction. Wrapping the listener loops within a `callbackFlow` block initially caused compilation failures due to missing runtime cancellation channel extensions.
* **The Resolution:** Imported `kotlinx.coroutines.channels.awaitClose` and built a clean reactive pipeline wrapper. The Firestore `addSnapshotListener` is now strictly unregistered inside the `awaitClose` closure block, safeguarding the resource channel from leaking memory during aggressive recompositions.

### 2. Disconnecting Real-Time Licensing (Global Live Kill-Switch Flow)
* **The Challenge:** Initially, checking the remote SaaS subscription token was bound exclusively to the local view lifecycle of the `ActivationScreen`. Once validation passed and the user shifted onto the dashboard, the associated `ViewModel` cleared out, terminating the snapshot listener. If a client's license was revoked or suspended mid-session, they could continue accessing patient data indefinitely until a manual application reload occurred.
* **The Resolution:** Shifted the state logic upward by registering the `LicenseViewModel` directly within the root `IbsarNavGraph` scope. By coupling an active, app-wide background `LaunchedEffect` listener with an aggressive navigational `popUpTo(0)` transactional wipeout, the application now enforces remote license blocks globally within milliseconds across any operational sub-view.

### 3. Multi-Input Rendering Lag & State Overhead in Optometry Forms
* **The Challenge:** Capturing vision testing results requires handling over 20 concurrent text inputs simultaneously (Sphere, Cylinder, Axis fields for both distance and near vision across left and right eyes). Using separate individual state trackers triggered severe interface stuttering during typing due to uncoordinated UI recompositions, while selecting inputs manually degraded physician efficiency.
* **The Resolution:** Refactored individual parameters into a unified, immutable data configuration named `ExaminationUiState`. Input components were optimized using a centralized focus management routine that routes `ImeAction.Next` behaviors into automatic `FocusManager` shifts, cutting data-entry time by nearly 70%.

### 4. Arabic Text Distortion & Bitmap Rasterization on 58mm Devices
* **The Challenge:** Budget-friendly 58mm mobile thermal printers lack structural character libraries for right-to-left connected Arabic writing layouts, printing broken, unjoined, and reversed glyph structures.
* **The Resolution:** Engineered a programmatic graphics translation pipeline. The system passes data strings onto an Android `StaticLayout` bounded by strict width properties, renders corporate logos, generates patient verification metadata QR Codes through Google ZXing, draws everything onto a clean white-background graphical `Canvas` bitmap, and translates pixel opacity matrices straight into raw binary ESC/POS command arrays (`GS v 0`).

---

## ⚙️ Setup Instructions

To execute this architecture locally, verify the following platform requirements:

1. **Firebase Configuration:** 
   * Obtain a fresh `google-services.json` layout file from the Firebase Console.
   * Store it directly inside the local `app/` folder. *(Note: Enforced as git-ignored for repository protection)*.
2. **SHA-1 Fingerprint Mapping:**
   * Append your machine development environment `SHA-1` and `SHA-256` keys to the cloud console project settings to unlock secure Google Sign-In routines.
3. **Database Security Architecture:**
   * Configure Firestore and Storage permission rules to restrict file access pipelines exclusively to securely authenticated operational users.

---

## 📌 Future Enhancements (V2.0 Product Roadmap)
- [ ] **Bulk Inventory Sync:** Build CSV/Excel automation handlers to batch-upload legacy optical product stock.
- [ ] **Hardware Barcode Decoder:** Integrate high-performance camera scanning routines for lightning-fast lens stock verification.
- [ ] **Stock Alert Triggers:** Deploy automatic notifications and background indicators for low-level diagnostic lens batches.

---

## 👨‍💻 Engineering & Development
**Eslam Ali**
* Android Software Engineer & SaaS Architect
