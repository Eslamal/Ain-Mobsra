# 📱 Ibsar - Enterprise Optometry & Clinic Management System

A production-grade, Enterprise-Level Android application engineered for optometry clinics and medical eye-care centers. The system digitizes the entire clinical workflow—ranging from advanced optical vision measurements and inventory cataloging to ZATCA-compliant E-Invoicing, offline-first synchronization, and hardware-level typography rendering for thermal POS printing.
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
</table>

</div>

---

## 🎯 Core Problems Solved for Modern Clinical Environments

1. Smart Optometry Formulations: Optometrists previously spent significant time rewriting repetitive drug dosages and diagnostic notes. The built-in Smart Templates Manager accelerates this process, allowing full prescription entries with a single tap.

2. Medical History Timeline: Tracking visual metric deterioration (SPH / CYL / AXIS) across months used to require manual paperwork. The app introduces a localized timeline comparing current and historical metrics instantly.

3. ZATCA-Compliant POS & E-Invoicing: Fully integrated Point of Sale (POS) system generating real-time tax invoices with cryptographic TLV Base64 QR Codes, ensuring 100% Phase-1 compliance with the Saudi Zakat, Tax and Customs Authority (ZATCA).

4. Offline-First Resilience: Heavily shielded concrete medical environments often drop Wi-Fi signals. The architecture implements a strict Offline-First Hardware Cache System combined with atomic transaction operations, ensuring uninterrupted clinical and sales workflows.

5. Hardware-Level Arabic Thermal Printing: Standard Bluetooth POS thermal printers natively distort right-to-left Arabic fonts. A custom-built programmatic bitmap graphics pipeline was engineered to override hardware deficits, printing flawless, fully connected Arabic receipts.

6. Invoices Archive System: Centralized and searchable digital archive allowing instant retrieval, visual PDF exporting, and re-printing of historical sales invoices.
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

## 👨‍💻 Engineering & Development
**Eslam Ali**
* Android Software Engineer & SaaS Architect
