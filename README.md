# 🔒 Vault Notes

**Vault Notes** is a secure, single-file, local-first notes application designed for Android. Built entirely with HTML, CSS, and JavaScript, it runs completely inside a WebView and requires no internet connection, no servers, and no cloud accounts.

Your notes stay on your device, and sensitive information is protected by AES-GCM encryption.

---

## ✨ Features

### 🔐 Security & Privacy
*   **Encrypted Notes:** Lock individual notes with a password (AES-GCM 256-bit, PBKDF2 600,000 iterations).
*   **Encrypted Backups:** Export your entire vault as a password-protected `.vault.json` file.
*   **App Passcode:** Protect the entire app with a PIN or password.
*   **Escalating Lockout:** Protects against brute-force attempts (up to 24-hour lockout).
*   **Privacy Cover:** Hides your notes when the app is backgrounded.
*   **Auto-Lock:** Lock the app or notes automatically after a period of inactivity or when the app loses focus.

### 📝 Rich Text & Organization
*   **Rich Text Editor:** Bold, italic, underline, strikethrough, text colors, and highlight colors.
*   **Markdown Support:** Toggle between a WYSIWYG editor and Markdown source mode.
*   **Lists & Checklists:** Bulleted lists, numbered lists, and interactive checklists.
*   **Tables:** Fully featured table editor with the ability to insert, delete, color cells, and adjust column widths.
*   **Attachments:** Attach images, PDFs, and files (up to 10MB) directly to notes. 
*   **Sketches:** Built-in canvas for handwriting and drawing.
*   **Note Links:** Link one note to another for easy navigation.
*   **Code Blocks:** Syntax-friendly code blocks with a "Copy" button.

### 🗂️ Organization
*   **Folders:** Create, rename, move, and delete nested folders.
*   **Tags:** Organize notes with tags and a quick-filter tag cloud.
*   **Favourites & Pinning:** Pin important notes to the top or mark them as favourites.
*   **Smart Views:** "Recently Edited" and "Favourites" virtual folders.
*   **Recycle Bin:** Deleted notes are kept temporarily, with options to restore or delete permanently.
*   **Advanced Filters:** Filter by date, tags, state, word target, and page color.

### 🎨 Appearance & UX
*   **Themes:** Light, Dark, Black (OLED), Ocean, and Sepia modes.
*   **Accent Colors:** Choose from multiple accent colors to personalize the UI.
*   **Reading Mode:** A distraction-free, full-screen reading experience with custom fonts and line heights.
*   **PDF Export:** Print or save notes as multi-page PDFs.
*   **Word Count Goal:** Set a word target for a note and track your progress.

---

## 🚀 How to Run / Build

Vault Notes is a **single HTML file**. It is designed to be compiled into an APK using local app builders on Android.

### Compiling to APK
1. Copy the `vault-notes.html` source code to your phone.
2. Download a Web-to-APK builder from the Google Play Store (e.g., **AppMint**, **WebToApk**, or similar).
3. Select **HTML to APK** (or ZIP to APK if you are using a modular version).
4. Select your `vault-notes.html` file.
5. Set the App Name (e.g., "Vault Notes") and App Icon.
6. Build and install the APK.

*Note: If you are testing locally, you can simply open the HTML file in Chrome or Firefox.*

---

## 🛠️ Tech Stack & Architecture

*   **Frontend:** Vanilla HTML5, CSS3, JavaScript (ES6+).
*   **Storage:** IndexedDB (for larger storage capacity) with a `localStorage` fallback.
*   **Encryption:** Web Crypto API (`window.crypto.subtle`).
    *   Symmetric Encryption: AES-GCM (256-bit).
    *   Key Derivation: PBKDF2 (SHA-256, 600,000 iterations).
*   **No Dependencies:** Zero external libraries, frameworks, or CDNs. Everything is self-contained.

---

## 🗺️ Roadmap & Known Quirks

**Known Quirks:**
*   When printing/exporting to PDF on Samsung devices, the system print spooler may capture the app's "Privacy Lock Screen" if the app is set to lock immediately on losing focus. 
    *   *Workaround:* Temporarily disable "Lock on blur" in the App Passcode settings before exporting a PDF.
*   The table width adjustment buttons (↔+ / ↔−) remain visible in the toolbar until the text cursor is moved completely out of the table.

**Planned / Discussed Features (Not Implemented):**
*   *Hidden Folders:* A secondary vault requiring a separate PIN.
*   *Encrypted Attachments:* Encrypting the file names and contents of attachments inside locked notes.
*   *Cloud Sync:* BYOK (Bring Your Own Key) encrypted blob storage sync (WebDAV/S3).

---

## ⚠️ Security Disclaimer

Vault Notes is designed to keep your data local and private. However, because it runs in an Android WebView, you should understand the limits of its security model:

1. **Unlocked notes are stored in plaintext.** Only notes you explicitly "Lock" are encrypted at rest. Anyone with access to the app's data directory (via root, ADB, or a compromised device) can read unlocked notes, folder names, and tags.
2. **Locked notes are cryptographically secure.** If you lock a note with a strong, unique password (12+ characters), its contents cannot be read by a forensic extraction of the phone. The encryption (AES-GCM + PBKDF2) holds up against brute-force attacks.
3. **Metadata and attachments leak.** Even on a locked note, the existence of the note is visible, and any attachments (PDFs, images, etc.) attached to the note are stored in plaintext alongside the encrypted note body.
4. **Compromised devices.** Vault Notes cannot protect against active malware, keyloggers, or a compromised operating system that captures your screen or keystrokes while the app is unlocked.
5. **There is no password recovery.** If you forget the password to a locked note or an encrypted backup file, the data is mathematically unrecoverable. Not even the developer can bypass it.

---

## 📄 License

This project is for personal use. Since it is a self-contained HTML file, you are free to modify it, distribute it, and adapt it to your needs.