# CLAUDE.md - PersonalMonitor Buddy

## 1. Project Vision

**PersonalMonitor Buddy** is a high-performance iOS utility designed for musicians performing live. It provides a simplified, "no-manual-needed" interface to control personal monitor mixes (Bus/Aux) from digital mixers without the complexity of full-scale mixing apps.

### Core Values

* **Performance First:** Zero-latency feel and high-contrast visuals for stage environments.
* **Safety:** Large touch targets and "Lock Mode" to prevent accidental volume spikes.
* **Simplicity:** Connect, select Bus, and play.

---

## 2. Technical Specifications

### Tech Stack

* **Framework:** SwiftUI (Targeting iOS 16+)
* **Networking:** `Network.framework` for UDP/OSC (Open Sound Control) and TCP communication.
* **Localization:** String Catalogs (.xcstrings) supporting **English** and **Italian** initially.
* **In-App Purchases:** RevenueCat or StoreKit 2 for managing Pro features.

### Connectivity Logic

1. **Discovery:** SSDP/mDNS and custom UDP broadcast to identify Behringer (X32/M32/XAir) and Soundcraft (Ui series) consoles.
2. **Protocol Handlers:**
* *Behringer:* OSC over UDP (Port 10023).
* *Soundcraft:* WebSockets/HTTP (Port 80/443) for Ui series.



---

## 3. User Interface Design

The UI must prioritize visibility under stage lights and ease of use with one hand.

### UI Components

* **The Mega-Fader:** A custom-built vertical slider occupying the majority of the screen.
* **Visual Feedback:** Real-time VU meter integrated into the fader track.
* **The "Buddy" Bar:** A persistent top bar showing connection status and current Bus name.
* **Quick-Switch:** A "Swipe from Edge" gesture to quickly change between pre-assigned Bus/Aux sends.

---

## 4. Monetization Strategy (In-App Purchases)

The app follows a "Freemium" model:

* **Free Tier:** Full control of 1 Bus/Aux for a single mixer type.
* **Pro License (One-time or Sub):**
* Multi-Mixer support (Unlock both Behringer and Soundcraft).
* Custom naming and icons for Busses.
* "Panic Mute" and "Safe-Limit" features.
* Ad-free setup screens.



---

## 5. Development Guidelines

### Localization Pattern

All strings must use `NSLocalizedString` or SwiftUI `Text(localizedKey)`.

* *English (Source):* "Connect to Mixer"
* *Italian:* "Connettiti al Mixer"

### Coding Standards

* **State Management:** Use `@Observable` (Swift 5.9+) or `ObservableObject` to ensure the fader reflects external mixer changes instantly.
* **Error Handling:** If the heartbeat to the mixer is lost, overlay a "Reconnecting..." blurred view to prevent stale control inputs.

---

## 6. Initial Implementation Roadmap

1. **Setup Localization:** Initialize `.xcstrings` for IT/EN.
2. **OSC Engine:** Implement the basic UDP client for Behringer X-AIR discovery.
3. **The Fader:** Create the custom SwiftUI Fader component with Haptic Feedback.
4. **Bus Selection:** Build the simple "Settings" overlay to pick the target Aux.