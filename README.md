<div align="center">

# 🛡️ C Y P H E R C H A T
### *End-to-End Encrypted Messaging for Android.*

[![Status](https://img.shields.io/badge/Status-Alpha-50fa7b?style=flat-square)]()
[![Platform](https://img.shields.io/badge/Platform-Android_24%2B-4c566a?style=flat-square&logo=android)]()
[![License](https://img.shields.io/badge/license-MIT-f1fa8c?style=flat-square)](LICENSE)

**[📲 Download APK](https://github.com/earnerbaymalay/cyph3rchat/releases)** · **[🌐 Sideload Hub](https://earnerbaymalay.github.io/sideload/)** · **[📖 Usage Guide](docs/USAGE.md)** · **[🔧 Troubleshooting](TROUBLESHOOTING.md)**

</div>

---

![Cyph3rChat Crypto](docs/media/hero.svg)

---

![Cyph3rChat Screenshots](docs/media/screenshot.svg)

## What is Cyph3rChat?

**Cyph3rChat encrypts every message using the Double Ratchet protocol and AES-256-GCM. Instead of creating an account, you generate a unique keypair. Messages are encrypted on your device before transmission, ensuring the relay server only handles ciphertext and has no knowledge of sender or recipient identities.**

---

## Quick Start

### Install on Android

1. Download the latest APK from [GitHub Releases](https://github.com/earnerbaymalay/cyph3rchat/releases)
2. Enable "Install unknown apps" in Android settings
3. Install and open — no account, no phone number, no server

### Install via Sideload Hub (iPhone PWA)

📲 **[Open Cyph3rChat PWA](https://earnerbaymalay.github.io/sideload/cypherchat/)** — install from Safari on iPhone, or any browser on desktop. WebCrypto encryption runs entirely in your browser.

### Build from Source

```bash
git clone https://github.com/earnerbaymalay/cyph3rchat.git
cd cyph3rchat
```

Open in Android Studio → Sync Gradle → Run (Minimum SDK 24, Target SDK 34, JDK 17 required).

---

## Cryptography

- **Key storage**
  - Algorithm: Android Keystore (hardware-backed)
  - Purpose: Generates and protects AES-256-GCM keys.
- **Symmetric encryption**
  - Algorithm: AES-256-GCM
  - Purpose: Encrypts message payloads with 128-bit authentication tag.
- **Key derivation**
  - Algorithm: HKDF-SHA256 (RFC 5869)
  - Purpose: Derives message keys from the root chain.
- **Key agreement**
  - Algorithm: ECDH (P-256 / secp256r1)
  - Purpose: Diffie-Hellman key exchange for Double Ratchet.
- **Double Ratchet**
  - Algorithm: Root chain + Message chains
  - Purpose: Forward secrecy and break-in recovery.
- **Database at rest**
  - Algorithm: SQLCipher (AES-256-CBC)
  - Purpose: Encrypts entire database file.

Plaintext messages are never written to disk; only ciphertext is stored. Chain keys and passphrases are securely erased from memory after use.

---

## Architecture

```
cyph3rchat/
├── app/
│   ├── Cyph3rChatApplication
│   ├── MainActivity
│   └── ui/screen/
│       ├── OnboardingScreen
│       ├── ChatListScreen
│       └── ConversationScreen
├── core/
│   ├── common/
│   ├── crypto/
│   ├── database/
│   └── network/
└── design/cypherchat-ui.html
```

- `app/` — Jetpack Compose UI, Koin DI
- `app/MainActivity` — NavHost, PIN lock, JSON export
- `core/common/` — SecureResult<T>, Logger, DispatcherProvider
- `core/crypto/` — KeyStoreManager, AesGcmCipher, HkdfDerivation, DoubleRatchetState
- `core/database/` — SQLCipher Room database
- `core/network/` — SimplexTransport interface
- `design/cypherchat-ui.html` — UI reference mockup

---

## Screens & Workflow

<div align="center">

- ![Onboarding](docs/media/screenshot_onboarding.svg)
  - Chat List: ![Chat List](docs/media/screenshot_chat_list.svg)
  - Conversation: ![Conversation](docs/media/screenshot_conversation.svg)

</div>

### Starting a Conversation

1. Tap the **'+' button** to generate an invitation link.
2. **Share the link** securely via a trusted channel (in person, encrypted email).
3. Once your contact accepts, the chat appears.
4. Messages are encrypted automatically — zero configuration needed.

---

## Build and Run

### Android

```bash
git clone https://github.com/earnerbaymalay/cyph3rchat.git
cd cyph3rchat
```

Open in Android Studio → Sync Gradle → Run (Minimum SDK 24, Target SDK 34, JDK 17 required).

### Running Tests

```bash
./gradlew test                 # Unit tests
./gradlew connectedAndroidTest # Instrumentation tests (device/emulator)
./gradlew lintDebug            # Lint checks
./gradlew assembleRelease      # Build release APK
```

---

## Related Projects

<div align="center">

- **🌗 **Gloam****
  - Platform: 📱 Android / 🖥️ Desktop
  - Description: Solar-timed CBT journal
  - Link: [Source →](https://github.com/earnerbaymalay/Gloam)
- **🌌 **Aether****
  - Platform: 📱 Android (Termux)
  - Description: Local-first AI workstation
  - Link: [Source →](https://github.com/earnerbaymalay/aether)
- **📲 **Sideload Hub****
  - Platform: 🌐 Web / PWA
  - Description: Central app distribution
  - Link: [Open Hub →](https://earnerbaymalay.github.io/sideload/)
- **🧰 **Termux-Vault****
  - Platform: 📱 Android
  - Description: Encrypted secrets manager
  - Link: [Source →](https://github.com/earnerbaymalay/Termux-Vault)

</div>

---

## Documentation

- **[📖 Usage Guide](docs/USAGE.md)** — Installation, starting conversations, security best practices, privacy details.
- **[🔧 Troubleshooting](TROUBLESHOOTING.md)** — Build issues, messaging problems, database corruption recovery.
- **[🗺️ Roadmap](docs/ROADMAP.md)** — Planned: SimpleX SDK integration, media support, backup/restore, F-Droid submission.
- **[📐 Architecture](docs/ARCHITECTURE.md)** — Module breakdown, DI setup, crypto flow.
- **[🔒 Security](docs/SECURITY.md)** — Threat model, cryptographic audit details, key management.
- **[🤝 Contributing](CONTRIBUTING.md)** — How to contribute, code of conduct.

---

## Privacy

- **No accounts:** No phone numbers, usernames, or server registration.
- **End-to-end encryption:** Every message encrypted with AES-256-GCM + Double Ratchet.
- **No cloud storage:** Messages encrypted on-device, relay server sees only ciphertext.
- **No analytics:** No tracking, crash reporting, or telemetry.
- **Hardware-backed keys:** Android Keystore protects encryption keys in TEE.
- **Clean uninstall:** All data deleted on uninstall, nothing persists on any server.

---

[MIT License](LICENSE)
