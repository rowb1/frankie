# Frankie: Puck.js Decorative Lamp Controller

This project uses an **Espruino Puck.js v2.1** to provide smart, wireless control over a decorative string of 4V LED light bulbs. The system features a mobile-friendly web interface and optimized power management for long-lasting battery performance.

## Features
* **Web Control**: Toggle between "Always On" and "Flashing" modes via a browser shortcut.
* **Adjustable Frequency**: Set flashing speeds from $0.2\text{ Hz}$ (one flash every 5 seconds) up to $10\text{ Hz}$.
* **Physical Master Toggle**: Use the Puck's built-in button to turn the system ON or OFF.
* **Battery Monitoring**: Real-time tracking of the Puck's CR3032 battery level.
* **Deep Sleep Mode**: Automatically enters an ultra-low-power `NRF.sleep()` state after 30 seconds of inactivity to preserve battery life.

## Hardware Requirements
* **Puck.js v2.1** (powered by a CR3032 coin cell).
* **4V LED Light String** (typically drawing ~40mA).
* **3x AA Battery Pack** (4.5V external power source for the lights).

## Wiring Instructions
To ensure the Puck's low-side FET switch can properly control the lights, the following wiring is required:

1.  **Positive Power**: Connect the **4.5V positive (+)** from the AA battery pack directly to the **Anode (positive side)** of the LED string.
2.  **Light Return**: Connect the **Cathode (return side)** of the LED string to the pad labeled **"FET"** on the back of the Puck.js.
3.  **Common Ground**: Connect the **negative (-)** terminal of the AA battery pack to the **GND pad** on the Puck.js.
    * *Note: A solid common ground is essential for the FET to "sink" the current and complete the circuit.*

## User Instructions

### Physical Button Control
* **Turn ON**: Press the Puck button. The onboard LED will flash **GREEN** for 0.5s, and the system will resume its last active mode.
* **Turn OFF**: Press the Puck button. The onboard LED will flash **RED** for 0.5s.
    * The unit enters **Standby Mode** for 30 seconds (still visible via Bluetooth) before entering **Deep Sleep** to save power.

### Web Interface Control
1.  Host the project via **GitHub Pages** (e.g., `https://rowb1.github.io/frankie/`).
2.  Open the link in a Bluetooth-capable browser (Chrome/Edge) on your Android device.
3.  Tap **"Connect Lamp"** to establish a secure Web Bluetooth session.
4.  Use the **Mode Selector** and **Frequency Slider** to adjust your lighting.
5.  The onboard **BLUE LED** on the Puck will pulse in sync with the lamp for visual status confirmation.

## Technical Logic
The system is driven by the built-in `FET` object in the Espruino firmware, which controls the N-channel MOSFET connected to pin **D28**. When in deep sleep, all Bluetooth advertising is disabled until the physical button is pressed to trigger `NRF.wake()`.