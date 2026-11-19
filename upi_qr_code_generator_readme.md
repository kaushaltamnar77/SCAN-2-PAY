# 📲 SCAN 2 PAY — UPI QR Code Generator

A lightweight, client-side web application for instantly generating dynamic and static **Unified Payments Interface (UPI)** QR codes. Built with zero backend dependencies, **SCAN 2 PAY** allows users to create custom payment QRs, store frequently used UPI IDs locally, and view, download, or natively share generated QR codes across devices.

---

## 📋 Table of Contents

* [Overview](#-overview)
* [Key Features](#-key-features)
* [How It Works (UPI Deep Linking)](#-how-it-works-upi-deep-linking)
* [Tech Stack](#-tech-stack)
* [Project Structure](#-project-structure)
* [Getting Started](#-getting-started)
* [Usage Guide](#-usage-guide)
* [Browser Compatibility & Privacy](#-browser-compatibility--privacy)
* [Future Enhancements](#-future-enhancements)

---

## 🔍 Overview

**SCAN 2 PAY** streamlines peer-to-peer and merchant UPI transactions in India by generating standard NPCI-compliant `upi://pay` QR codes directly inside the browser. Whether you need a quick one-off payment QR with a pre-filled amount or want to save up to 10 frequently used Virtual Payment Addresses (VPAs) for rapid access, the entire workflow runs instantaneously on the client side without transmitting any financial data to external servers.

---

## ✨ Key Features

* **Dual Generation Modes:**
  * **Standard QR Generator:** Generate custom QR codes on the fly by entering any UPI ID (`VPA`) and an optional fixed INR (`₹`) amount.
  * **Quick Pay (Saved IDs):** Save up to **10 frequently used UPI IDs** in browser `localStorage` for one-click selection and rapid QR generation.
* **Interactive QR Actions:**
  * **Full-Screen Modal Preview:** Enlarge the generated QR code in a clean overlay modal for effortless scanning from another device.
  * **One-Click PNG Download:** Export the generated QR code directly to your device as `upi-qr-code.png`.
  * **Native Web Share Integration:** Uses the browser's `navigator.share` API to share the QR image directly to WhatsApp, Gmail, Telegram, or Messages (with automatic download fallback on unsupported desktop browsers).
* **Zero-Setup Single-File Architecture:** Runs completely standalone in any modern web browser with CDN-loaded Tailwind CSS and `QRCode.js`.
* **100% Client-Side Privacy:** No databases, tracking, or backend API calls—saved UPI IDs stay strictly on the user's local device.

---

## ⚙️ How It Works (UPI Deep Linking)

The application encodes payment parameters into the standard **NPCI UPI Deep Link URI** specification and renders it as a Level-M error-corrected QR code (`200x200px`):

* **Without Fixed Amount (Open Payment):**
  ```text
  upi://pay?pa=<UPI_ID>&pn=User
  ```
* **With Fixed Amount (Locked INR Amount):**
  ```text
  upi://pay?pa=<UPI_ID>&pn=User&am=<AMOUNT>&cu=INR
  ```

| Parameter | Description |
| :--- | :--- |
| `pa` | Payee Virtual Payment Address (e.g., `example@oksbi`) |
| `pn` | Payee Name (`User`) |
| `am` | Transaction Amount in Indian Rupees |
| `cu` | Currency Code (`INR`) |

---

## 🛠 Tech Stack

* **Markup:** HTML5
* **Styling:** Tailwind CSS (v4 Browser CDN)
* **Logic & Storage:** Vanilla JavaScript (ES6+), Web Storage API (`localStorage`), Web Share API (`navigator.share`)
* **QR Rendering Engine:** [QRCode.js](https://davidshimjs.github.io/qrcodejs/) (`v1.0.0`)

---

## 📁 Project Structure

```text
scan-2-pay/
│
├── index.html       # Complete single-file application (HTML, Tailwind UI, JS logic)
└── README.md        # Project documentation
```

---

## 🚀 Getting Started

Because **SCAN 2 PAY** is built as a self-contained client-side application, no build tools, Node.js packages, or backend servers are required.

### 1. Clone the Repository
```bash
git clone https://github.com/<your-username>/scan-2-pay.git
cd scan-2-pay
```

### 2. Run Locally
* **Option A (Direct Open):** Double-click `index.html` to open it directly in Chrome, Edge, Safari, or Firefox.
* **Option B (Local Development Server):** Use the **Live Server** extension in VS Code or run Python's built-in HTTP server:
  ```bash
  python -m http.server 8080
  ```
  Then visit `http://localhost:8080` in your browser.

---

## 📖 Usage Guide

1. **Generate a Custom QR Code:**
   * Stay on the **Standard QR Generator** tab.
   * Enter a valid UPI ID (e.g., `merchant@okaxis`) and optionally enter an amount in `₹`.
   * Click **Generate QR Code**.
2. **Manage & Use Saved UPI IDs:**
   * Switch to the **Quick Pay (Saved IDs)** tab.
   * Expand **Manage Saved UPI IDs (Max 10)** to add or remove frequent VPAs.
   * Select an account from the dropdown, enter the amount, and click **Generate Quick QR**.
3. **View, Share, or Download:**
   * Once generated, use **View QR Code** for a high-contrast modal view, **Share QR Code** to send via mobile apps, or **Download QR Code** to save as a PNG file.

---

## 🔒 Browser Compatibility & Privacy

* **Data Privacy:** Saved UPI IDs are stored exclusively under the `quick_upi_ids` key in your browser's `localStorage`. Clearing browser site data will remove saved IDs.
* **Web Share API Support:** Native image file sharing (`navigator.canShare({ files })`) works seamlessly on mobile browsers (Android Chrome, iOS Safari). On desktop browsers where file sharing is unsupported, clicking **Share QR Code** automatically downloads the PNG file as a fallback.

---

## 🔮 Future Enhancements

* [ ] **Custom Payee Name & Transaction Note:** Add optional `pn` (Payee Name) and `tn` (Transaction Note/Remarks) input fields.
* [ ] **UPI ID Format Validation:** Add regex validation (`username@bankhandle`) before generating or saving VPAs.
* [ ] **Branded QR Card Export:** Export a downloadable payment card displaying the UPI ID, formatted amount, and supported UPI app logos alongside the QR code.
* [ ] **PWA Support:** Add a `manifest.json` and Service Worker so users can install **SCAN 2 PAY** as an offline-capable mobile app.