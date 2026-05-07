# Frankie: Puck.js Magic Lamp Controller

This project uses an **Espruino Puck.js v2.1** to provide immersive, wireless control over a decorative jar of LED fairy lights. The system features a custom "Glassmorphism" web interface designed to match the warm amber and cork aesthetic of the lamp.

## Features
* **Three Lighting Modes**:
    * **Always On**: A steady, warm glow.
    * **Flashing**: Classic rhythmic blinking.
    * **Breathing**: An organic, sinusoidal pulse using Hardware PWM for a "living" effect.
* **Advanced Customization**: A hidden configuration panel to fine-tune device behavior without re-uploading code.
* **Physical Master Toggle**: Use the Puck's built-in button to wake the lamp (Green flash) or enter standby (Red flash).
* **Power Management**: Automatically enters `NRF.sleep()` (Deep Sleep) after a configurable standby period to maximize coin-cell life.
* **Safety Features**: Includes a hardcoded safety timer to automatically turn the lamp off if left active.

## Hardware Wiring
To ensure the Puck's low-side FET switch functions correctly:
1.  **Positive (+)**: 4.5V from the AA pack goes to the LED Anode.
2.  **Return**: LED Cathode goes to the **"FET"** pad on the Puck.
3.  **Common Ground**: AA negative (-) must connect to the Puck **GND** pad.

## Advanced Parameters & Safety Rails
The system enforces the following safety limits for all parameters:
* **Min Frequency**: 0.02 Hz (up to a 50-second cycle).
* **Max Frequency**: 20.0 Hz.
* **Deep Sleep Delay**: Minimum 10 seconds of standby.
* **Safety Auto-Off**: Minimum 5 minutes.

## Installation
1.  Upload the `.js` code to your **Puck.js** via the Espruino IDE.
2.  Host the `index.html`, `manifest.json`, and `icon.png` on **GitHub Pages**.
3.  Open the URL on Android and select **"Install"** to add "Frankie's Magic Lamp" to your home screen with its custom icon and amber theme.