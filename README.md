# PLAYBULB Candle - Bluetooth Control Demo

A web-based application that allows you to control a PLAYBULB Candle device via Bluetooth Low Energy (BLE) from your browser. Change colors, apply effects, monitor battery level, and customize the device name—all through a simple, interactive web interface.

![PLAYBULB Candle Demo](https://github.com/mathemagie/candle-bluetooth)

## 📋 Table of Contents

- [Features](#-features)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Usage](#-usage)
- [Project Structure](#-project-structure)
- [How It Works](#-how-it-works)
- [Technologies Used](#-technologies-used)
- [Original Codelab](#-original-codelab)
- [License](#-license)

## ✨ Features

- **Bluetooth Connection**: Connect to your PLAYBULB Candle device directly from your web browser
- **Color Picker**: Interactive color wheel to select any color for your candle
- **Multiple Effects**: Choose from various lighting effects:
  - No Effect (solid color)
  - Candle Effect (flickering candle simulation)
  - Flashing (rapid color changes)
  - Pulse (gentle color pulsing)
  - Rainbow (smooth color transitions)
  - Rainbow Fade (soft rainbow transitions)
- **Device Customization**: Change the device name (up to 20 characters)
- **Battery Monitoring**: View the current battery level of your candle
- **Responsive Design**: Works on desktop and mobile devices

## 🔧 Prerequisites

Before you can use this application, make sure you have:

1. **A PLAYBULB Candle Device**: This app is designed specifically for PLAYBULB Candle Bluetooth LED devices
2. **A Modern Web Browser**: The application uses the Web Bluetooth API, which is supported in:
   - Chrome/Edge (version 56+)
   - Opera (version 43+)
   - Samsung Internet (version 7+)
   - **Note**: Web Bluetooth is not supported in Firefox or Safari
3. **HTTPS or Localhost**: Web Bluetooth API requires a secure context (HTTPS) or localhost for security reasons
4. **Bluetooth Enabled**: Make sure Bluetooth is enabled on your device

## 🚀 Installation

1. **Clone or download this repository**:
   ```bash
   git clone https://github.com/mathemagie/candle-bluetooth.git
   cd candle-bluetooth
   ```

2. **Open the application**:
   
   **Option A: Using a local server (Recommended)**
   
   If you have Python installed:
   ```bash
   # Python 3
   python -m http.server 8000
   
   # Python 2
   python -m SimpleHTTPServer 8000
   ```
   
   Then open your browser and navigate to: `http://localhost:8000`
   
   **Option B: Direct file access**
   
   Simply open `index.html` in a supported browser (Chrome, Edge, or Opera)
   
   **Option C: Deploy to a web server**
   
   Upload all files to any web server with HTTPS enabled

## 📱 Usage

1. **Open the application** in a supported web browser
2. **Click the "CONNECT" button** to search for and connect to your PLAYBULB Candle
3. **Wait for connection**: The app will search for nearby PLAYBULB Candle devices
4. **Once connected**, you'll see:
   - A color wheel (canvas) to select colors
   - A text input field showing/editing the device name
   - Radio buttons for selecting different effects
   - The battery level displayed as a percentage
5. **Select a color** by clicking anywhere on the color wheel
6. **Choose an effect** using the radio buttons
7. **Change the device name** by typing in the text input field (changes save automatically)

### Tips for Best Experience

- Make sure your candle is powered on and within Bluetooth range
- The color wheel is interactive—click any color to apply it to your candle
- Device name changes are limited to 20 characters
- The battery level updates when you first connect

## 📁 Project Structure

```
candle-bluetooth/
├── index.html          # Main HTML file with the user interface
├── app.js              # Application logic and event handlers
├── playbulbCandle.js   # Bluetooth communication and candle control logic
├── styles.css          # Styling for the application
├── color-wheel.png     # Color picker image
├── favicon.png         # Website icon
└── README.md           # This file
```

### File Descriptions

- **`index.html`**: Contains the HTML structure of the web page, including buttons, color wheel canvas, and input fields
- **`app.js`**: Handles user interactions (button clicks, color selection, effect changes) and updates the display
- **`playbulbCandle.js`**: Contains the `PlaybulbCandle` class that manages Bluetooth connections and communicates with the candle device
- **`styles.css`**: Defines the visual appearance and layout of the application

## 🔍 How It Works

### Web Bluetooth API

This application uses the **Web Bluetooth API**, which allows web pages to communicate with Bluetooth Low Energy (BLE) devices directly from the browser. This is a modern web standard that doesn't require any plugins or additional software.

### Connection Process

1. When you click "CONNECT", the app uses `navigator.bluetooth.requestDevice()` to search for devices
2. It filters for devices with the PLAYBULB Candle service UUID (0xFF02)
3. Once a device is selected, it establishes a GATT (Generic Attribute Profile) connection
4. The app can then read and write to specific characteristics (services) on the device:
   - Device name (UUID: 0xFFFF)
   - Color control (UUID: 0xFFFC)
   - Effect control (UUID: 0xFFFB)

### Color Selection

- The color wheel image is displayed on an HTML5 `<canvas>` element
- When you click the canvas, the app:
  1. Calculates the exact pixel position you clicked
  2. Reads the RGB color values from that pixel
  3. Sends those values to the candle via Bluetooth
  4. Draws a white circle marker at the clicked position

### Effect Control

Each effect is sent as a specific command to the candle's effect characteristic. The app switches between different methods based on your selection:
- Solid color uses `setColor()`
- Candle effect uses `setCandleEffectColor()`
- Flashing uses `setFlashingColor()`
- Pulse uses `setPulseColor()`
- Rainbow effects use `setRainbow()` or `setRainbowFade()`

## 🛠 Technologies Used

- **HTML5**: Structure of the web page
- **CSS3**: Styling and layout
- **JavaScript (ES6+)**: Application logic and Bluetooth communication
- **Web Bluetooth API**: Browser API for Bluetooth Low Energy communication
- **Material Design Lite**: Google's Material Design components for the UI
- **HTML5 Canvas**: For the interactive color wheel

## 📚 Original Codelab

This project is based on the Google Codelab tutorial:

🔗 [Candle Bluetooth Codelab](https://codelabs.developers.google.com/codelabs/candle-bluetooth/)

The original working version can be found at:
🔗 [Google Codelabs Demo](https://googlecodelabs.github.io/candle-bluetooth/)

This repository contains a working implementation of the codelab tutorial.

## 📝 License

This project is open source and available for educational purposes. Please refer to the original Google Codelab for licensing information.

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](https://github.com/mathemagie/candle-bluetooth/issues) if you want to contribute.

## 💡 Learning Resources

If you're new to web development or Bluetooth programming, here are some helpful resources:

- [Web Bluetooth API Documentation](https://developer.mozilla.org/en-US/docs/Web/API/Web_Bluetooth_API)
- [JavaScript Promises Tutorial](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
- [HTML5 Canvas Tutorial](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial)
- [Bluetooth Low Energy Basics](https://www.bluetooth.com/learn-about-bluetooth/)

---

**Note**: Make sure your PLAYBULB Candle is powered on and in pairing mode before attempting to connect!
