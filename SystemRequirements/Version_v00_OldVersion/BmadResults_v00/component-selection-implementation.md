# IoT Plant Watering System - Component Selection & Implementation

## Detailed Component List

### Primary Controller System
| Component | Model/Type | Specifications | Est. Price | Source |
|-----------|------------|----------------|------------|---------|
| **ESP32 Dev Board** | ESP32-WROOM-32 | WiFi, Bluetooth, 32 pins, MicroPython ready | €12-15 | AliExpress/Amazon |
| **Touch TFT Display** | 3.2" ILI9341 | 320x240, capacitive touch, SPI interface | €15-20 | AliExpress |
| **MicroSD Card** | 8-16GB Class 10 | Data logging, web files storage | €5 | Local electronics |

### Watchdog System
| Component | Model/Type | Specifications | Est. Price | Source |
|-----------|------------|----------------|------------|---------|
| **Arduino Nano** | ATmega328P | 5V/16MHz, compact, reliable | €8-12 | AliExpress |
| **18650 Battery** | Li-ion 3000mAh | Protected, rechargeable | €6-8 | Battery specialist |
| **TP4056 Module** | Charging board | USB-C, protection circuit | €3-5 | AliExpress |
| **Piezo Buzzer** | Active buzzer | 5V, 85dB, alarm patterns | €2-3 | Electronics store |

### Sensors & Monitoring
| Component | Model/Type | Specifications | Est. Price | Source |
|-----------|------------|----------------|------------|---------|
| **Ultrasonic Sensor** | HC-SR04 | 2-400cm range, waterproof version | €5-8 | AliExpress |
| **Soil Moisture Sensors** | Capacitive v1.2 | 2x units, corrosion resistant | €6-10 | AliExpress |
| **Status LEDs** | 5mm RGB LEDs | Common cathode, various colors | €2-3 | Electronics store |

### Pump & Water System
| Component | Model/Type | Specifications | Est. Price | Source |
|-----------|------------|----------------|------------|---------|
| **Water Pump** | 12V Diaphragm | 6-8L/min, 8m head, self-priming | €25-35 | Amazon/Pumps24 |
| **Solenoid Valves** | 12V NC valves | 2x units, 1/4" connections | €20-30 | AliExpress |
| **Pump Relay** | 12V 30A relay | High current switching | €3-5 | Electronics store |
| **Pressure Switch** | Adjustable | Pump protection, dry run prevention | €8-12 | Pumps24 |

### Power & Electrical
| Component | Model/Type | Specifications | Est. Price | Source |
|-----------|------------|----------------|------------|---------|
| **Power Supply** | 230V→12V/5V | 5A capacity, dual output | €20-25 | Electronics store |
| **Buck Converter** | 12V→3.3V | For ESP32 stable power | €3-5 | AliExpress |
| **Voltage Dividers** | Resistor networks | Battery monitoring circuits | €2-3 | Electronics store |

### Enclosure & Assembly
| Component | Model/Type | Specifications | Est. Price | Source |
|-----------|------------|----------------|------------|---------|
| **Main Enclosure** | IP65 plastic box | 200x150x75mm, wall mount | €15-20 | Electronics store |
| **Watchdog Enclosure** | Smaller IP54 box | 100x75x50mm, battery compartment | €8-12 | Electronics store |
| **Cable Glands** | PG7/PG9 | Waterproof cable entries | €5-8 | Electronics store |
| **PCB/Stripboard** | Prototype board | Component mounting | €5-10 | Electronics store |

**Total Estimated Cost: €180-250**

## Implementation Timeline

### Phase 1: Core System Development (Weeks 1-2)
**Week 1: Hardware Setup & Basic Framework**
- [ ] Order and receive all components
- [ ] Set up MicroPython development environment
- [ ] Flash ESP32 with latest MicroPython firmware
- [ ] Test basic sensor readings (ultrasonic, moisture)
- [ ] Implement touch display basic interface

**Week 2: Core Logic Implementation**
- [ ] Develop water level monitoring with ultrasonic sensor
- [ ] Implement moisture sensor reading and calibration
- [ ] Create basic pump control logic with safety features
- [ ] Build touch interface for manual controls
- [ ] Test pump system with pressure/flow validation

### Phase 2: Watchdog & Safety Systems (Weeks 3-4)
**Week 3: Watchdog Development**
- [ ] Program Arduino Nano watchdog controller
- [ ] Implement I2C communication between ESP32 and watchdog
- [ ] Create heartbeat monitoring and failure detection
- [ ] Add battery monitoring and charging system
- [ ] Test acoustic alarm patterns and volume levels

**Week 4: Integration & Safety**
- [ ] Integrate watchdog with main system
- [ ] Implement emergency shutdown procedures
- [ ] Add pump dry-run protection with pressure switch
- [ ] Create comprehensive error handling and recovery
- [ ] Test system failure scenarios and recovery

### Phase 3: User Interface & Automation (Weeks 5-6)
**Week 5: Advanced Features**
- [ ] Complete touch interface with all menus and settings
- [ ] Implement web dashboard with real-time data
- [ ] Add scheduling system with time-based watering
- [ ] Create water usage calculation and logging
- [ ] Implement iPhone-optimized web interface

**Week 6: Testing & Deployment**
- [ ] Comprehensive system testing with real plants
- [ ] User acceptance testing with both technical/non-technical users
- [ ] Performance optimization and bug fixes
- [ ] Final installation in basement and plant locations
- [ ] Create user documentation and maintenance guide

## System Architecture Diagram

```
┌─────────────────────┐    ┌──────────────────┐
│   LIVING ROOM       │    │    BASEMENT      │
│                     │    │                  │
│  ┌─────────────┐   │    │ ┌──────────────┐ │
│  │   Plant 1   │   │    │ │ Main Control │ │
│  │ (Moisture)  │───┼────┼→│   ESP32      │ │
│  └─────────────┘   │    │ │ + Touch LCD  │ │
│                     │    │ └──────────────┘ │
│  ┌─────────────┐   │    │                  │
│  │   Plant 2   │   │    │ ┌──────────────┐ │
│  │ (Moisture)  │───┼────┼→│   Watchdog   │ │
│  └─────────────┘   │    │ │ Arduino Nano │ │
│                     │    │ │ + Battery    │ │
│       ↑ Water       │    │ │ + Buzzer     │ │
│       Tubes         │    │ └──────────────┘ │
│                     │    │                  │
└─────────────────────┘    │ ┌──────────────┐ │
                           │ │ Water System │ │
                           │ │ Pump+Solenoid│ │
                           │ │ Ultrasonic   │ │
                           │ │ Reservoir    │ │
                           │ └──────────────┘ │
                           └──────────────────┘
```

## MicroPython Development Setup

### Required Libraries
```python
# Core MicroPython libraries
import machine
import network
import uasyncio
import ujson
import utime

# Additional libraries to install
# - lvgl (touch display)
# - umqtt.simple (MQTT communication)
# - urequests (HTTP requests)
```

### Development Environment
1. **IDE**: Thonny or VS Code with MicroPython extension
2. **File Transfer**: ampy or Thonny file manager
3. **Debugging**: REPL over USB/WiFi
4. **Version Control**: Git for code management

### Key MicroPython Advantages
- **Interactive Development**: Edit files directly on ESP32
- **No Compilation**: Instant code changes and testing
- **Rich Ecosystem**: Extensive library support
- **Async Support**: uasyncio for concurrent operations
- **Memory Efficiency**: Optimized for microcontroller constraints

## Testing & Validation Procedures

### Hardware Testing
1. **Power System**: Voltage stability, battery backup duration
2. **Sensors**: Accuracy, reliability, environmental conditions
3. **Pump System**: Pressure, flow rate, reliability over time
4. **Communication**: ESP32-Watchdog I2C reliability
5. **Touch Interface**: Responsiveness, accuracy, durability

### Software Testing
1. **Core Logic**: Watering algorithms, safety shutoffs
2. **User Interface**: Touch responsiveness, web dashboard
3. **Error Handling**: Failure recovery, graceful degradation
4. **Performance**: Memory usage, response times
5. **Integration**: End-to-end system operation

### User Acceptance Testing
1. **Technical User**: Full system configuration and troubleshooting
2. **Non-Technical User**: Basic operation, emergency procedures
3. **Long-term Testing**: 2-week autonomous operation validation
4. **Edge Cases**: Power outages, network failures, sensor malfunctions

## Next Steps Priority List

1. **[IMMEDIATE]** Order components based on selection list
2. **[WEEK 1]** Set up development environment and basic ESP32 framework
3. **[WEEK 1]** Test individual sensors and actuators
4. **[WEEK 2]** Implement core watering logic and safety systems
5. **[WEEK 3]** Develop and integrate watchdog system
6. **[WEEK 4]** Create touch interface and user experience
7. **[WEEK 5]** Build web dashboard and iPhone interface
8. **[WEEK 6]** Final testing, installation, and documentation

## Success Metrics
- [ ] 7-day autonomous operation without intervention
- [ ] Both users can operate system independently
- [ ] Water usage optimization within 15% of baseline
- [ ] System failure detection within 5 minutes
- [ ] Touch interface usability by non-technical user
- [ ] Total project cost under €250