# Vault — Desktop

A local, encrypted notes vault for Linux and macOS. This is a desktop port of the original [Android Vault app](https://github.com/bezau1/vaultapp), built with [Tauri](https://tauri.app).

All encryption/decryption happens locally in the browser engine via the WebCrypto API (AES-256-GCM). Notes never leave the device, and the app makes no network requests.
## Note: the app is basically a html wrapper, at least a secure one I guess
---

## Install

### Arch Linux (AUR)

```bash
yay -S vaultapp
```

### Debian / Ubuntu

Download the latest `.deb` from [Releases](../../releases) and install:

```bash
sudo dpkg -i Vault_<version>_amd64.deb
```

### Other Linux distros (AppImage)

Download the latest `.AppImage` from [Releases](../../releases):

```bash
chmod +x Vault_<version>_amd64.AppImage
./Vault_<version>_amd64.AppImage
```

### macOS

No prebuilt release yet build from source (see below). It's the same project; Tauri just needs to compile on an actual Mac to produce a `.app`/`.dmg`.

---

## Building from source

Requires [Rust](https://rustup.rs) and [Node.js](https://nodejs.org).

```bash
git clone https://github.com/bezau1/vault-desktop.git
cd vault-desktop
npm install
npm run tauri build
```

The built app/installer will be in `src-tauri/target/release/bundle/`.

For local development with hot reload:

```bash
npm run tauri dev
```

Devtools (right-click → Inspect Element, or F12) are enabled in both dev and release builds for debugging.

---

## Project structure

```
vault-desktop/
├── src/
│   └── index.html         ← The full Vault web app (UI, crypto, storage — all of it)
├── src-tauri/
│   ├── src/
│   │   ├── main.rs
│   │   └── lib.rs          ← Minimal native shell, no app logic here
│   ├── icons/               ← App icons (also used for the iOS/Android ports)
│   └── tauri.conf.json      ← Window config, bundle metadata
├── package.json
└── PKGBUILD                 ← Arch/AUR packaging
```

The native side is intentionally almost empty everything the app does lives in `src/index.html`, shared basically same with the Android version.

---

## Security notes

- No internet access
- The encryption/decryption happens via the WebCrypto API (AES-256-GCM)
- All notes are stored on-device

---

## Other platforms

- Android: [vaultapp](https://github.com/bezau1/vaultapp) (The original)
- iOS port: planned
