# Connecting EC11 Encoder to CYD Display with bruce firmware

## 1. Hardware Connection

The CYD display has a limited number of free pins. To connect an EC11 encoder, use the expansion ports:

| Encoder Function | GPIO ESP32 | Connector on CYD  |
| ---------------- | ---------- | ----------------- |
| CLK (Pin A)      | GPIO 35    | P3                |
| DT (Pin B)       | GPIO 22    | P3 or CN1         |
| SW (Button)      | GPIO 27    | CN1               |
| Power (VCC)      | 3.3V       | Corresponding pin |
| Ground (GND)     | GND        | Corresponding pin |

## 2. Bruce Firmware Configuration

Bruce firmware is originally optimized for devices with encoders (such as LilyGo T-Embed). To make the encoder work on CYD:

1. **Flashing the device:**

    - Use the official web flasher: [bruce.computer/flasher](https://bruce.computer/flasher)

2. **Web interface configuration:**

    - After flashing, the ESP32 will create an access point "Bruce-AP" (or similar)
    - Connect to this network via browser
    - Go to **Settings** → **Configuration**

3. **GPIO Configuration:**
   Ensure the assigned pins match the functions:
    - Encoder A → GPIO 35
    - Encoder B → GPIO 22
    - Button → GPIO 27

## 3. Troubleshooting

### Direction Inversion

If scrolling goes left when rotating the encoder right:

-   **Option 1:** Swap wires on GPIO 35 and GPIO 22
-   **Option 2:** Change the direction in firmware settings

### Unstable Operation

Internal pull-up resistors on some ESP32 pins may be weak. Solution:

-   Add external 10 kΩ pull-up resistors to the 3.3V line

### Alternative Control

If you lack free pins:

-   Bruce supports operation via the **CYD touch screen** (enabled by default in recent builds)
-   Touch control can completely replace the encoder

## Notes

-   Make all connections with power disconnected
-   Check connection reliability in connectors
-   For stable operation, use shielded wires for long connections
