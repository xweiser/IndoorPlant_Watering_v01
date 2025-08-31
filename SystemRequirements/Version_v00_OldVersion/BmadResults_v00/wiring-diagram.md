# IoT Plant Watering System - Detailed Wiring Diagram

## System Overview
```
ESP32 (MicroPython) ←→ Arduino Nano (Watchdog) ←→ Sensors & Actuators
```

## ESP32 DevKit Pin Assignments

### Power & Communication
| Pin | Function | Connection | Notes |
|-----|----------|------------|-------|
| **3V3** | Power Output | Sensors VCC | 3.3V regulated output |
| **5V** | Power Input | External 5V supply | From buck converter |
| **GND** | Ground | Common ground | Multiple ground connections |
| **GPIO21** | I2C SDA | Arduino Nano A4 | Communication bus |
| **GPIO22** | I2C SCL | Arduino Nano A5 | Communication bus |

### Touch Display (SPI)
| Pin | Function | Connection | Display Pin |
|-----|----------|------------|-------------|
| **GPIO23** | MOSI | TFT MOSI | Data to display |
| **GPIO19** | MISO | TFT MISO | Data from display |
| **GPIO18** | SCK | TFT SCK | SPI clock |
| **GPIO5** | CS | TFT CS | Chip select |
| **GPIO2** | DC | TFT DC | Data/Command |
| **GPIO4** | RST | TFT RST | Reset |
| **GPIO15** | Touch CS | Touch CS | Touch chip select |
| **GPIO27** | Touch IRQ | Touch IRQ | Touch interrupt |

### Sensors
| Pin | Function | Connection | Sensor |
|-----|----------|------------|---------|
| **GPIO13** | Digital Input | HC-SR04 Echo | Ultrasonic distance |
| **GPIO12** | Digital Output | HC-SR04 Trig | Ultrasonic trigger |
| **GPIO32** | ADC Input | Moisture Sensor 1 | Plant 1 soil moisture |
| **GPIO33** | ADC Input | Moisture Sensor 2 | Plant 2 soil moisture |

### Pump Control & Status
| Pin | Function | Connection | Device |
|-----|----------|------------|--------|
| **GPIO25** | Digital Output | Pump Relay IN | Main pump control |
| **GPIO26** | Digital Output | Valve 1 Relay | Plant 1 solenoid |
| **GPIO14** | Digital Output | Valve 2 Relay | Plant 2 solenoid |
| **GPIO16** | Digital Input | Pressure Switch | Pump protection |

### Status LEDs
| Pin | Function | Connection | LED Color |
|-----|----------|------------|-----------|
| **GPIO17** | Digital Output | Status LED Red | System error |
| **GPIO0** | Digital Output | Status LED Green | System OK |
| **GPIO35** | Digital Input | Float Switch | Water level backup |

## Arduino Nano (Watchdog) Pin Assignments

### Power & Communication
| Pin | Function | Connection | Notes |
|-----|----------|------------|-------|
| **5V** | Power Input | 5V regulated supply | From main power |
| **GND** | Ground | Common ground | Shared with ESP32 |
| **A4** | I2C SDA | ESP32 GPIO21 | Communication |
| **A5** | I2C SCL | ESP32 GPIO22 | Communication |

### Battery & Charging
| Pin | Function | Connection | Device |
|-----|----------|------------|--------|
| **A0** | ADC Input | Battery voltage divider | Battery monitoring |
| **D3** | Digital Output | TP4056 Enable | Charging control |
| **A1** | ADC Input | Charging status | TP4056 status |

### Alert & Control
| Pin | Function | Connection | Device |
|-----|----------|------------|--------|
| **D8** | Digital Output | Piezo Buzzer | Acoustic alarms |
| **D7** | Digital Output | ESP32 Reset | System recovery |
| **D6** | Digital Input | Manual silence button | User alarm acknowledge |

### Independent Monitoring
| Pin | Function | Connection | Sensor |
|-----|----------|------------|--------|
| **D4** | Digital Input | Power supply monitor | Main power status |
| **D5** | Digital Output | Independent LED | Watchdog status |
| **A2** | ADC Input | 12V rail monitor | Pump power status |

## Complete Wiring Diagram

```
                    ┌─────────────────────────────────────────────────────────┐
                    │                 MAIN ENCLOSURE                          │
                    │                                                         │
  ┌─────────────────┼─────────────────────────────────────────────────────────┼─────────────────┐
  │                 │                                                         │                 │
  │    ESP32        │                     Arduino Nano                        │   Power Supply  │
  │   DevKit        │                     (Watchdog)                          │                 │
  │                 │                                                         │   230V → 12V/5V │
  │ GPIO21 ●────────┼──────────● A4 (SDA)              D8 ●──────────────────┼─── [BUZZER]     │
  │ GPIO22 ●────────┼──────────● A5 (SCL)              D7 ●──────────────────┼─── ESP32 RST    │
  │                 │                                                         │                 │
  │ GPIO23 ●────────┼─── TFT MOSI          A0 ●─── Battery Monitor           │   ┌──────────┐  │
  │ GPIO19 ●────────┼─── TFT MISO          A1 ●─── Charge Status             │   │ TP4056   │  │
  │ GPIO18 ●────────┼─── TFT SCK           D3 ●─── Charge Enable             │   │ Charger  │  │
  │ GPIO5  ●────────┼─── TFT CS            D4 ●─── Power Monitor             │   │          │  │
  │ GPIO2  ●────────┼─── TFT DC            D5 ●─── Status LED               │   │ [BATTERY]│  │
  │ GPIO4  ●────────┼─── TFT RST           D6 ●─── Silence Button           │   └──────────┘  │
  │ GPIO15 ●────────┼─── Touch CS          A2 ●─── 12V Monitor               │                 │
  │ GPIO27 ●────────┼─── Touch IRQ                                           │                 │
  │                 │                                                         │                 │
  │ GPIO13 ●────────┼─────────────────────────────── HC-SR04 Echo            │                 │
  │ GPIO12 ●────────┼─────────────────────────────── HC-SR04 Trig            │                 │
  │                 │                                                         │                 │
  │ GPIO25 ●────────┼─────────────────────────────── [PUMP RELAY]            │                 │
  │ GPIO26 ●────────┼─────────────────────────────── [VALVE 1 RELAY]         │                 │
  │ GPIO14 ●────────┼─────────────────────────────── [VALVE 2 RELAY]         │                 │
  │ GPIO16 ●────────┼─────────────────────────────── Pressure Switch         │                 │
  │                 │                                                         │                 │
  │ GPIO32 ●────────┼─────────────────────────────── Moisture Sensor 1       │                 │
  │ GPIO33 ●────────┼─────────────────────────────── Moisture Sensor 2       │                 │
  │                 │                                                         │                 │
  │ GPIO17 ●────────┼─────────────────────────────── [RED LED]               │                 │
  │ GPIO0  ●────────┼─────────────────────────────── [GREEN LED]             │                 │
  │ GPIO35 ●────────┼─────────────────────────────── Float Switch (backup)   │                 │
  │                 │                                                         │                 │
  └─────────────────┼─────────────────────────────────────────────────────────┼─────────────────┘
                    │                                                         │
                    └─────────────────────────────────────────────────────────┘
```

## Sensor Connection Details

### HC-SR04 Ultrasonic Sensor (Water Level)
```
HC-SR04          ESP32
───────          ─────
VCC    ────────  3V3
GND    ────────  GND  
Trig   ────────  GPIO12
Echo   ────────  GPIO13
```

### Capacitive Soil Moisture Sensors
```
Moisture Sensor 1    ESP32          Moisture Sensor 2    ESP32
─────────────────    ─────          ─────────────────    ─────
VCC              ──  3V3            VCC              ──  3V3
GND              ──  GND            GND              ──  GND
AOUT             ──  GPIO32         AOUT             ──  GPIO33
```

### Touch TFT Display (ILI9341)
```
TFT Display      ESP32
───────────      ─────
VCC          ──  3V3
GND          ──  GND
CS           ──  GPIO5
RESET        ──  GPIO4
DC           ──  GPIO2
MOSI         ──  GPIO23
SCK          ──  GPIO18
LED          ──  3V3 (via 100Ω resistor)
MISO         ──  GPIO19
T_CLK        ──  GPIO18
T_CS         ──  GPIO15
T_DIN        ──  GPIO23
T_DO         ──  GPIO19
T_IRQ        ──  GPIO27
```

## Power Distribution

### Main Power Supply (230V → 12V/5V)
```
230V AC Input
     │
┌────▼────┐
│ SMPS    │  ──── 12V/3A ──── Pump System
│ 60W     │  
└─────────┘  ──── 5V/2A ──── Arduino Nano + Buzzer
     │
     └─── Buck Converter ──── 3.3V/1A ──── ESP32 + Sensors
```

### Battery Backup System
```
5V Supply ──── TP4056 Charger ──── 18650 Li-ion Battery
                     │                    │
                     └──── Arduino Nano ──┘
                           (during power outage)
```

## I2C Communication Protocol

### ESP32 ↔ Arduino Communication
```python
# ESP32 (Master) - MicroPython
i2c = machine.I2C(0, scl=machine.Pin(22), sda=machine.Pin(21))
WATCHDOG_ADDR = 0x42

# Send heartbeat every 30 seconds
heartbeat_data = b'ALIVE'
i2c.writeto(WATCHDOG_ADDR, heartbeat_data)

# Read watchdog status
status = i2c.readfrom(WATCHDOG_ADDR, 1)
```

```cpp
// Arduino Nano (Slave) - C++
#include <Wire.h>
#define WATCHDOG_ADDR 0x42

void setup() {
  Wire.begin(WATCHDOG_ADDR);
  Wire.onReceive(receiveEvent);
  Wire.onRequest(requestEvent);
}

void receiveEvent(int bytes) {
  // Handle ESP32 heartbeat
  last_heartbeat = millis();
}

void requestEvent() {
  // Send watchdog status to ESP32
  Wire.write(system_status);
}
```

## Safety & Protection Features

### Pump Protection Circuit
```
12V Supply ──── Fuse (5A) ──── Relay Contact ──── Pump Motor
                                    │
ESP32 GPIO25 ──── Relay Coil ──── Flyback Diode ──── GND
                                    │
Pressure Switch ──── ESP32 GPIO16 ──┘
```

### Emergency Shutdown Sequence
1. **Watchdog detects failure** → **Arduino D7** → **ESP32 Reset**
2. **Low battery** → **Disable pump** → **Alert only**
3. **Pressure switch open** → **Emergency pump stop** → **Acoustic alarm**
4. **Manual silence** → **Arduino D6** → **Stop buzzer**

## Component Specifications Summary

| Component | Voltage | Current | Interface | Purpose |
|-----------|---------|---------|-----------|---------|
| **ESP32** | 3.3V | 500mA | WiFi/I2C/SPI | Main controller |
| **Arduino Nano** | 5V | 50mA | I2C | Watchdog system |
| **TFT Display** | 3.3V | 200mA | SPI | User interface |
| **HC-SR04** | 3.3V | 15mA | Digital | Water level |
| **Moisture Sensors** | 3.3V | 10mA each | Analog | Soil monitoring |
| **Water Pump** | 12V | 2-3A | Relay | Water delivery |
| **Solenoid Valves** | 12V | 500mA each | Relay | Flow control |
| **Piezo Buzzer** | 5V | 30mA | Digital | Acoustic alerts |
| **18650 Battery** | 3.7V | 3000mAh | Direct | Backup power |

## PCB Layout Recommendations

### Main Board Layout (ESP32)
- **Power section**: Left side with proper decoupling
- **Communication**: I2C pullups (4.7kΩ) near ESP32
- **Sensor inputs**: Right side with filtering caps
- **Display connector**: Top edge with short traces
- **Relay outputs**: Bottom with flyback diodes

### Watchdog Board Layout (Arduino)
- **Battery management**: Dedicated section with TP4056
- **Alert section**: Buzzer and LED indicators
- **Communication**: I2C connector to main board
- **Reset control**: Protected ESP32 reset circuit

This wiring diagram provides complete connectivity for your ESP32-Arduino dual-controller plant watering system with comprehensive monitoring and safety features.