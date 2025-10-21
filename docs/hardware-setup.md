# Hardware Setup Guide

# 📦 Required Components

Before starting, ensure you have all the components from the Bill of Materials in the main README.

# 🔌 Wiring Connections

# E-Paper Display Module

**XIAO ESP32-C3 to 7.5" E-Paper Display:**

The E-Paper display uses SPI communication. Connect as follows:

| E-Paper Pin | XIAO ESP32-C3 Pin | Description |
|-------------|-------------------|-------------|
| VCC         | 3.3V              | Power Supply|
| GND         | GND               | Ground      |
| DIN (MOSI)  | D10               | SPI Data In |
| CLK (SCK)   | D8                | SPI Clock   |
| CS          | D7                | Chip Select |
| DC          | D6                | Data/Command|
| RST         | D5                | Reset       |
| BUSY        | D4                | Busy Signal |

**Note:** Pin numbers may vary based on your specific E-Paper model. Refer to your display's datasheet.

# Temperature Sensor

**Seeed Temperature Sensor to XIAO ESP32-C3:**

| Sensor Pin | XIAO ESP32-C3 Pin  | Description |
|------------|--------------------|-------------|
| VCC        | 3.3V               | Power Supply|
| GND        | GND                | Ground      |
| SDA        | D4 (I2C SDA)       | I2C Data    |
| SCL        | D5 (I2C SCL)       | I2C Clock   |

# Relay Control Module

**XIAO ESP32-C6 to 5V DC Relay:**

| Relay Pin | XIAO ESP32-C6 Pin | Description    |
|-----------|-------------------|----------------|
| VCC       | 5V                | Power Supply   |
| GND       | GND               | Ground         |
| IN        | D10               | Control Signal |

## 🔧 Assembly Steps

# Step 1: Prepare the XIAO Boards

1. Unbox the XIAO ESP32-C3 and ESP32-C6 boards
2. Check for any visible damage
3. Keep the boards on an anti-static surface

# Step 2: Connect E-Paper Display

1. Identify the SPI pins on the E-Paper display connector
2. Use jumper wires to connect according to the wiring table above
3. **Important:** Ensure all GND connections are common
4. Double-check VCC is connected to 3.3V (NOT 5V!)

# Step 3: Connect Temperature Sensor

1. Identify the I2C pins on the Seeed temperature sensor
2. Connect SDA and SCL to the XIAO ESP32-C3 I2C pins
3. Connect VCC to 3.3V and GND to ground

# Step 4: Connect Relay Module

1. Connect the relay control pin (IN) to a GPIO pin on XIAO ESP32-C6
2. Connect relay VCC to 5V power supply
3. Connect relay GND to common ground

# Step 5: Power Supply

**For XIAO ESP32-C3 (Display Module):**
- Connect USB-C cable for power
- Power consumption: ~200mA during refresh, <50mA idle

**For XIAO ESP32-C6 (Relay Module):**
- Connect USB-C cable for power
- Ensure adequate current for relay operation (typically 100-200mA)

# ⚠️ Important Notes

# Power Considerations
- E-Paper displays are very power efficient
- Refresh operations draw more current briefly
- Use quality USB cables to prevent voltage drop

# Wiring Tips
- Keep wires as short as possible
- Use color coding: Red (VCC), Black (GND), Other colors for signals
- Test continuity with a multimeter before powering on

## Safety Precautions
- Never connect 5V to 3.3V pins
- Always connect GND first, power last
- Disconnect power before making wiring changes
- The relay controls AC power - ensure proper isolation and safety

# 🧪 Testing

## Basic Connectivity Test

1. **Power On Check:**
   - Connect XIAO ESP32-C3 via USB
   - LED should blink (bootloader)
   - No smoke or burning smell

2. **E-Paper Display Test:**
   - Display should initialize (flicker black/white)
   - May show random pattern initially (normal)

3. **Temperature Sensor Test:**
   - Will verify after software installation
   - Should appear on I2C bus scan

4. **Relay Test:**
   - Relay should click when triggered
   - LED indicator (if present) should light up

# 📸 Visual Reference

Refer to the photos in `/images/setup-photos/` for visual guidance:
- `full-setup.jpg` - Complete assembled system
- `hardware-components.jpg` - Individual components
- `wiring-closeup.jpg` - Detailed wiring connections

# 🔍 Troubleshooting Hardware Issues

# E-Paper Display Not Responding
- Check SPI connections (MOSI, SCK, CS)
- Verify 3.3V power supply
- Check BUSY pin connection
- Try a different USB cable/power source

# Temperature Sensor Not Detected
- Verify I2C connections (SDA, SCL)
- Check I2C address (typically 0x48 or 0x4A)
- Try different I2C pins
- Ensure pull-up resistors (usually built-in)

### Relay Not Switching
- Check control signal voltage (should be 3.3V)
- Verify relay coil voltage rating (5V)
- Ensure adequate power supply current
- Test relay manually with a wire to VCC

# ✅ Hardware Setup Complete!

Once all connections are verified and tested, proceed to the [Software Setup Guide](software-setup.md) to configure ESPHome and Home Assistant.

# 📞 Need Help?

If you encounter issues not covered here:
1. Check the [Troubleshooting Guide](troubleshooting.md)
2. Open an issue on GitHub
3. Refer to official documentation:
   - [XIAO ESP32-C3 Wiki](https://wiki.seeedstudio.com/XIAO_ESP32C3_Getting_Started/)
   - [XIAO ESP32-C6 Wiki](https://wiki.seeedstudio.com/xiao_esp32c6_getting_started/)
   - [ESPHome Documentation](https://esphome.io/)