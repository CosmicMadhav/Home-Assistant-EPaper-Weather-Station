# Software Setup Guide

Complete guide to configuring ESPHome, Home Assistant, and OpenWeather API integration for the E-Paper Weather Station.

## 📋 Prerequisites

Before starting, ensure you have:
- ✅ Hardware assembled (see [Hardware Setup Guide](hardware-setup.md))
- ✅ Raspberry Pi 4B with Home Assistant installed
- ✅ Network connectivity (WiFi/Ethernet)
- ✅ OpenWeather API key (free tier)

## 🏠 Part 1: Home Assistant Setup

### Step 1: Access Home Assistant

1. Open a web browser
2. Navigate to: `http://homeassistant.local:8123`
   - Or use your Raspberry Pi's IP address: `http://192.168.x.x:8123`
3. Log in with your credentials

### Step 2: Install ESPHome Add-on

1. Go to **Settings** → **Add-ons**
2. Click **Add-on Store** (bottom right)
3. Search for **"ESPHome"**
4. Click on **ESPHome** → **Install**
5. Wait for installation to complete
6. Toggle **"Start on boot"** and **"Watchdog"**
7. Click **Start**
8. Click **"Open Web UI"** to access ESPHome Dashboard

### Step 3: Get OpenWeather API Key

1. Visit [OpenWeatherMap.org](https://openweathermap.org/api)
2. Click **"Sign Up"** (free account)
3. Verify your email
4. Go to **API Keys** section
5. Copy your API key (looks like: `abc123def456...`)
6. Keep this safe - you'll need it later

### Step 4: Configure OpenWeather in Home Assistant

1. In Home Assistant, go to **Settings** → **Devices & Services**
2. Click **"+ Add Integration"**
3. Search for **"OpenWeatherMap"**
4. Enter your API key
5. Set your location (latitude/longitude)
6. Select weather data to track:
   - ✅ Temperature
   - ✅ Humidity
   - ✅ Wind Speed
7. Click **Submit**

## 🔧 Part 2: ESPHome Configuration

### Step 1: Create E-Paper Display Device

1. Open **ESPHome Dashboard** (from Home Assistant)
2. Click **"+ New Device"**
3. Enter device name: `epaper-display`
4. Select board: **"Seeed XIAO ESP32C3"**
5. Click **"Install"** → **"Skip"** (we'll configure first)

### Step 2: Edit Configuration

1. Click **"Edit"** on your new device
2. Replace the configuration with the YAML from `/config/epaper-display.yaml`
3. Update these values in the YAML:
   ```yaml
   wifi:
     ssid: "YOUR_WIFI_NAME"
     password: "YOUR_WIFI_PASSWORD"
   ```
4. Click **"Save"**

### Step 3: Flash XIAO ESP32-C3

1. Connect XIAO ESP32-C3 to your computer via USB-C
2. In ESPHome Dashboard, click **"Install"** on `epaper-display`
3. Select **"Plug into this computer"**
4. Choose the USB port (usually `/dev/ttyUSB0` or `COM3`)
5. Wait for compilation and upload (~5 minutes first time)
6. You should see logs indicating successful connection

### Step 4: Create Relay Controller Device

1. Click **"+ New Device"** in ESPHome
2. Enter name: `relay-controller`
3. Select board: **"Seeed XIAO ESP32C6"**
4. Click **"Install"** → **"Skip"**
5. Edit configuration with `/config/relay-controller.yaml`
6. Update WiFi credentials
7. Save and flash to XIAO ESP32-C6

## 🌡️ Part 3: Temperature Sensor Setup

### Step 1: Verify Sensor Connection

The temperature sensor should auto-detect via I2C. To verify:

1. In ESPHome logs, look for:
   ```
   [I2C] Found device at address 0x48
   ```
2. If not found, check hardware connections

### Step 2: Configure in ESPHome

The sensor configuration is already in `epaper-display.yaml`:
```yaml
sensor:
  - platform: [sensor_type]
    name: "Room Temperature"
    update_interval: 30s
```

## 📊 Part 4: Home Assistant Integration

### Step 1: Integrate ESPHome Devices

1. Go to **Settings** → **Devices & Services**
2. ESPHome integration should auto-discover your devices
3. Click **"Configure"** on each device
4. Click **"Submit** to add them

### Step 2: Verify Entities

Check that these entities appear:
- `sensor.epaper_display_room_temperature`
- `sensor.openweathermap_temperature`
- `sensor.openweathermap_humidity`
- `sensor.openweathermap_wind_speed`
- `switch.relay_controller`

### Step 3: Create Dashboard (Optional)

1. Go to **Overview** (home screen)
2. Click **Edit Dashboard**
3. Add cards to display your sensor data
4. Useful for testing before E-Paper display is working

## 🖥️ Part 5: E-Paper Display Configuration

### Step 1: Test Display

1. The display should initialize automatically
2. You'll see it flash black/white (normal)
3. After 30 seconds, data should appear

### Step 2: Customize Display Layout

Edit the display section in `epaper-display.yaml`:

```yaml
display:
  - platform: waveshare_epaper
    # Customize what to show
    lambda: |-
      // Your display code here
      // See examples in config file
```

### Step 3: Adjust Refresh Rate

Default is 30 seconds. To change:
```yaml
display:
  update_interval: 60s  # Change to 60 seconds
```

**Note:** More frequent updates = more power consumption

## ⚡ Part 6: OTA Updates Setup

Over-The-Air updates are already configured in ESPHome!

### To Update Wirelessly:

1. Make changes to YAML configuration
2. Click **"Install"** in ESPHome Dashboard
3. Select **"Wirelessly"**
4. Device will update without USB cable!

**Advantages:**
- No need to physically access device
- Updates in seconds
- Can update from anywhere on network

## 🧪 Testing Everything

### Test Checklist:

1. **WiFi Connection:**
   ```
   ✅ Check ESPHome logs show "WiFi connected"
   ✅ Device appears in Home Assistant
   ```

2. **Weather Data:**
   ```
   ✅ OpenWeather entities show current data
   ✅ Data updates every 30 seconds
   ```

3. **Room Temperature:**
   ```
   ✅ Sensor reading appears in Home Assistant
   ✅ Reading is reasonable (15-35°C)
   ```

4. **E-Paper Display:**
   ```
   ✅ Display shows date and time
   ✅ Weather data appears correctly
   ✅ Room temperature displays
   ✅ Last update time shows
   ```

5. **Relay Control:**
   ```
   ✅ Can toggle relay from Home Assistant
   ✅ Relay clicks when switching
   ✅ Load device responds (if connected)
   ```

## 🔄 Regular Maintenance

### Weekly:
- Check ESPHome logs for errors
- Verify weather API is within free tier limits

### Monthly:
- Update ESPHome to latest version
- Update Home Assistant
- Check display for any burn-in (rare with E-Paper)

### As Needed:
- OTA update when adding new features
- Adjust refresh rate based on usage

## 📱 Mobile Access

Access from anywhere:
1. Install **Home Assistant mobile app**
2. Log in with your credentials
3. View sensor data remotely
4. Control relay from phone

## 🎯 Common Configurations

### Display Only Weather:
```yaml
# Comment out room temperature sensor
# sensor:
#   - platform: temperature_sensor
```

### Change Temperature Units:
```yaml
# In OpenWeather integration
unit_system: imperial  # For Fahrenheit
# Or keep: metric  # For Celsius
```

### Add More Weather Data:
- Forecast (next 3 days)
- UV Index
- Sunrise/Sunset times
- Weather conditions (cloudy, sunny, etc.)

## ✅ Software Setup Complete!

Your E-Paper Weather Station should now be:
- ✅ Displaying live weather data
- ✅ Showing room temperature
- ✅ Updating every 30 seconds
- ✅ Controllable from Home Assistant
- ✅ Updatable via OTA

## 🆘 Troubleshooting

If something isn't working, see the [Troubleshooting Guide](troubleshooting.md).

Common issues:
- ESPHome won't compile → Check YAML syntax
- Device offline → Check WiFi credentials
- No weather data → Verify API key
- Display not updating → Check SPI connections

## 📚 Additional Resources

- [ESPHome Official Docs](https://esphome.io/)
- [Home Assistant Documentation](https://www.home-assistant.io/docs/)
- [XIAO ESP32-C3 Wiki](https://wiki.seeedstudio.com/XIAO_ESP32C3_Getting_Started/)
- [OpenWeatherMap API Docs](https://openweathermap.org/api)

## 🎓 What's Next?

Consider these enhancements:
- Add more sensors (air quality, pressure)
- Create automations based on weather
- Add weather alerts/notifications
- Implement battery power with solar charging
- Create custom display layouts