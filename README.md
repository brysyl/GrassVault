<div align="center">

# GrassVault ⚡☁️
### Edge-First Cross-Platform Personal Intelligence & Security Vault

[![Firebase AI Logic](https://img.shields.io/badge/Firebase-AI%20Logic-orange?style=for-the-badge&logo=firebase)](https://firebase.google.com)
[![Manifest V3](https://img.shields.io/badge/Chrome-Extension%20V3-blue?style=for-the-badge&logo=google-chrome)](https://developer.chrome.com)
[![BuildHybridAI 2026](https://img.shields.io/badge/Hackathon-%23BuildHybridAI%202026-purple?style=for-the-badge)]()

</div>

---

## Overview

**GrassVault** is a zero-latency, local-first personal intelligence and security vault designed to capture, organize, and secure snippets, documents, and code blocks seamlessly across **Web, Android, and iOS**. 

By leveraging the **Firebase AI Logic SDK**, GrassVault intelligently routes tasks based on context and device capabilities: executing privacy-sensitive, short-form tasks entirely on-device via **Gemini Nano** (Web/Android) and **Apple Foundation Models** (iOS), while falling back gracefully to cloud inference for heavy multi-document synthesis and cross-device graph routing.

---

## Key Architectural Highlights

- **Multi-Platform Unification:** Single cohesive codebase and state architecture bridging Chrome Extensions (Manifest V3), Android, and iOS clients.
- **Hybrid Inference Router:** Intelligent client-side routing that checks local model availability (`window.ai` / native bindings) before scaling up to cloud endpoints.
- **Zero-Latency Privacy:** Local-first processing ensures sensitive code snippets and clipboard data never leave the device unless explicitly required.
- **Secure Cloud Sync:** Real-time synchronization powered by Firebase Firestore, secured with Firebase App Check.

---

## Systems Architecture 🏦


```mermaid
graph TB
    subgraph Client_Tier ["Edge Client Tier (Cross-Platform)"]
        direction TB
        Web["Chrome Extension (Manifest V3)"]
        Android["Android Client"]
        iOS["iOS Client"]
    end

    subgraph Edge_Inference ["On-Device Inference Tier"]
        direction LR
        GeminiWeb["Gemini Nano (Web)"]
        GeminiAndroid["Gemini Nano (Android)"]
        AppleModel["Apple Foundation Models (iOS)"]
    end

    subgraph Hybrid_Router ["Hybrid Inference Router"]
        Engine["hybridEngine.js <br/>• Token Check (<4k) <br/>• Local Fallback Switch"]
    end

    subgraph Cloud_Tier ["Firebase Cloud Backend Tier"]
        direction TB
        AppCheck["Firebase App Check"]
        CloudAI["Cloud Gemini API"]
        Firestore["Firebase Firestore (Sync)"]
    end

    Web --> Engine
    Android --> Engine
    iOS --> Engine

    Engine -->|Local Ready| GeminiWeb
    Engine -->|Local Ready| GeminiAndroid
    Engine -->|Local Ready| AppleModel

    GeminiWeb -.-> Web
    GeminiAndroid -.-> Android
    AppleModel -.-> iOS

    Engine -->|Exceeds Token Limit| AppCheck
    AppCheck --> CloudAI
    CloudAI --> Engine

    Web & Android & iOS --> Firestore

```

---

## Tech Stack

- **Client Core:** Vite, Vanilla ES6+, Tailwind CSS (Dark Mode / Glassmorphic UI)
- **Extension Engine:** Chrome Extension Manifest V3 (Service Workers, Content Scripts, MutationObservers)
- **AI & Logic:** Firebase AI Logic SDK, Gemini Nano, Apple Foundation Models
- **Backend & Sync:** Firebase Firestore, Firebase Auth, App Check

---

## Project Structure

```text
grassvault/
├── package.json
├── tailwind.config.js
├── vite.config.js
├── src/
│   ├── manifest.json
│   ├── background/
│   │   └── service-worker.js
│   ├── content/
│   │   └── contentScript.js
│   ├── popup/
│   │   ├── popup.html
│   │   ├── popup.js
│   │   └── popup.css
│   ├── dashboard/
│   │   ├── index.html
│   │   └── app.js
│   └── shared/
│       ├── firebaseConfig.js
│       └── hybridEngine.js
└── README.md

```

---

## Getting Started in GitHub Codespaces
 * Open in Codespaces: Launch this repository directly inside a GitHub Codespace container.
 * Install Dependencies:
   npm install

 * Configure Environment: Create a .env file in the root directory and add your Firebase configuration keys.
 * Build the Extension:
   npm run build

 * Load in Chrome: Navigate to chrome://extensions, enable Developer mode, click Load unpacked, and select the dist/ directory.

---
## License
MIT License — built for the #BuildHybridAI 2026 Hackathon.


