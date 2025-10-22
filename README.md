# Home Assistant E-Paper Weather Station

A smart home dashboard using a 7.5" E-Paper display powered by XIAO ESP32-C3, integrated with Home Assistant on Raspberry Pi 4B. Features real-time weather data, room temperature monitoring, and automated relay control.

![Project Status](https://img.shields.io/badge/Status-Active-success)
![ESPHome](https://img.shields.io/badge/ESPHome-Compatible-blue)
![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Integrated-orange)

## 📸 Project Demo

Video demonstration (https://www.youtube.com/watch?v=QzmY-1wLoSE)

## ✨ Features

- **7.5" E-Paper Display** - Large, easy-to-read interface with low power consumption
- **Weather Information** - Real-time temperature, humidity, and wind speed via OpenWeather API
- **Room Monitoring** - Local temperature tracking using Seeed temperature sensor
- **Date & Time Display** - Always up-to-date clock with last refresh timestamp
- **Fast Refresh Rate** - Updates every 30 seconds for near real-time data
- **Home Automation** - Integrated relay control for appliances (XIAO ESP32-C6)
- **Wireless Updates** - OTA (Over-The-Air) firmware updates via ESPHome

## 🛠️ Hardware Components

### Display Module
- **XIAO ESP32-C3** - Main controller for E-Paper display
- **7.5" E-Paper Panel** - High-resolution display module
- **Seeed Temperature Sensor** - For room temperature monitoring

### Automation Module
- **XIAO ESP32-C6** - Relay controller
- **5V DC Relay Module** (Seeed) - For appliance control

### Backend
- **Raspberry Pi 4B** - Running Home Assistant
- **Home Assistant** - Smart home automation platform
- **ESPHome** - Device configuration and management

## 📋 Bill of Materials

| Component | Quantity | Purpose | Link |
|-----------|----------|---------|------|
| XIAO ESP32-C3 | 1 | Display Controller | [Seeed Studio](https://www.seeedstudio.com/Seeed-XIAO-ESP32C3-p-5431.html) |
| XIAO ESP32-C6 | 1 | Relay Controller | [Seeed Studio](https://www.seeedstudio.com/Seeed-XIAO-ESP32C6-p-5884.html) |
| 7.5" E-Paper Display | 1 | Visual Output | Check compatible models |
| Seeed Temperature Sensor | 1 | Room Temperature | [Seeed Studio](https://www.seeedstudio.com/) |
| 5V DC Relay Module | 1 | Appliance Control | [Seeed Studio](https://www.seeedstudio.com/) |
| Raspberry Pi 4B | 1 | Home Assistant Server | - |
| USB-C Cables | 2 | Power Supply | - |

## 🔧 Software Requirements

- **Home Assistant** (installed on Raspberry Pi 4B)
- **ESPHome** Add-on for Home Assistant
- **OpenWeather API Key** (free tier available)
- **ESPHome Dashboard** for device management

## 🚀 Quick Start

### 1. Home Assistant Setup

```bash
# Install ESPHome add-on in Home Assistant
# Go to Settings > Add-ons > Add-on Store
# Search for "ESPHome" and install
```

### 2. Get OpenWeather API Key

1. Sign up at [OpenWeatherMap](https://openweathermap.org/api)
2. Generate a free API key
3. Add to Home Assistant configuration

### 3. Flash ESPHome to XIAO Boards

```bash
# Connect XIAO ESP32-C3 via USB
# In ESPHome Dashboard, create new device
# Upload the configuration from /config/epaper-display.yaml
```

### 4. Configure Home Assistant

- Copy configuration files from `/config/` folder
- Update with your API keys and credentials
- Restart Home Assistant

## 📁 Repository Structure

```
.
├── README.md                          # This file
├── config/
│   ├── epaper-display.yaml           # ESPHome config for display
│   ├── relay-controller.yaml         # ESPHome config for relay
│   └── homeassistant-config.yaml     # Home Assistant integration
├── docs/
│   ├── hardware-setup.md             # Wiring and assembly guide
│   ├── software-setup.md             # Detailed installation steps
│   ├── troubleshooting.md            # Common issues and solutions
│   └── customization.md              # How to customize the display
├── images/
│   ├── wiring-diagram.png
│   ├── setup-photos/
│   └── demo-video.mp4
└── examples/
    └── alternative-layouts.md         # Different display configurations
```

## 💻 Configuration

### Display Layout

The E-Paper display shows:

```
┌─────────────────────────────────────────┐
│  Date: Tuesday, Oct 21, 2025            │
│  Time: 14:30:45                         │
├─────────────────────────────────────────┤
│  Weather (Outdoor)                      │
│  🌡️  Temperature: 28°C                  │
│  💧 Humidity: 65%                       │
│  💨 Wind: 12 km/h                       │
├─────────────────────────────────────────┤
│  Room Temperature: 24°C                 │
├─────────────────────────────────────────┤
│  Last Updated: 14:30:15                 │
└─────────────────────────────────────────┘
```

### Customization

You can customize:
- Refresh rate (default: 30 seconds)
- Display layout and fonts
- Weather data fields
- Temperature units (Celsius/Fahrenheit)

See [docs/customization.md](docs/customization.md) for details.

## 🔌 Wiring

The wiring is straightforward with minimal connections:

**XIAO ESP32-C3 to E-Paper Display:**
- Simple SPI connection (details in [docs/hardware-setup.md](docs/hardware-setup.md))

**XIAO ESP32-C6 to Relay Module:**
- Direct GPIO to relay control pin
- 5V power supply connection

**Temperature Sensor:**
- I2C or analog connection to XIAO ESP32-C3

*Detailed wiring diagrams available in `/images/wiring-diagram.png`*

## 📊 Features Demonstration

### Weather Integration
- Pulls data from OpenWeather API via Home Assistant
- Displays current conditions
- Updates every 30 seconds

### Room Temperature Monitoring
- Uses Seeed temperature sensor
- Logs historical data in Home Assistant
- Can trigger automations based on temperature

### Relay Control
- XIAO ESP32-C6 controls appliances
- Integrated with Home Assistant automations
- Can be triggered manually or automatically

## 🐛 Troubleshooting

### Display not updating?
- Check WiFi connection on XIAO ESP32-C3
- Verify Home Assistant is running
- Check ESPHome logs in Home Assistant

### Weather data not showing?
- Verify OpenWeather API key is correct
- Check API quota (free tier has limits)
- Ensure Home Assistant has internet access

### Temperature sensor not responding?
- Check I2C connections
- Verify sensor address in ESPHome config
- Try scanning I2C bus for devices

More solutions in [docs/troubleshooting.md](docs/troubleshooting.md)

## 🎓 What I Learned

This project was developed during my internship at **TechieSmS** (June 2025 - Present), where I:
- Implemented OTA updates for embedded devices
- Integrated multiple sensors with Home Assistant
- Designed efficient refresh algorithms for E-Paper displays
- Worked with ESPHome for IoT device management

## 🔮 Future Enhancements

- [ ] Add battery power with solar charging
- [ ] Implement deep sleep mode for power saving
- [ ] Add more weather information (forecast, UV index)
- [ ] Create mobile app for remote configuration
- [ ] Add touch interface for manual control
- [ ] Integrate calendar events display

## 🤝 Contributing

Suggestions and improvements are welcome! Feel free to:
- Open an issue for bugs or feature requests
- Submit pull requests
- Share your own customizations

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

## 👤 Author

**Madhav Maheshwari**
- IoT Engineer Intern @ TechieSmS
- B.Tech in Electronics & Communication Engineering, Nirma University
- GitHub: [@CosmicMadhav](https://github.com/CosmicMadhav)
- Email: madhavmaheshwari415@gmail.com

## 🙏 Acknowledgments

- **TechieSmS** for the internship opportunity
- **Seeed Studio** for excellent hardware documentation
- **Home Assistant Community** for ESPHome support
- **OpenWeather** for free API access

---

⭐ If you find this project useful, please consider giving it a star!

**Part of my IoT and Embedded Systems portfolio. Check out my other projects!**