# IoT Plant Watering System - Project Brief

## Executive Summary

An automated plant watering system using ESP32 microcontroller technology to monitor soil moisture and deliver measured water volumes to plants in two living room windows via a basement-based water reservoir. The system provides high automation with touch display controls, independent watchdog health monitoring, precise water flow measurement, web dashboard monitoring, and future home automation integration capabilities (ioBroker/Home Assistant).

## Problem Statement

**Current Challenge:**
- Manual plant watering requires constant attention and is prone to inconsistency
- Plants located at windows with limited access for regular monitoring  
- Need for remote monitoring while away from home
- Desire for high automation to reduce maintenance burden
- Two-user household with different technical skill levels (technical + non-technical)

**Evidence:**
- Existing infrastructure installed: 10m tubes with 5m height difference, cable runs for sensors
- 230V power available at both locations
- Full WiFi coverage throughout house
- Existing KNX home automation system

## Proposed Solution

**Core System:**
- ESP32-based control unit with touch TFT display and status LEDs
- Independent watchdog system for health monitoring and failure detection
- Moisture sensor monitoring via installed cables
- Ultrasonic water level sensor for reservoir monitoring
- Pump system with pressure capability for 5m lift + 10m horizontal
- Water flow measurement system for precise volume control
- Web dashboard for remote monitoring and control
- Local offline operation capability with full redundancy

**Key Features:**
- Automated watering based on moisture thresholds and time windows with precise volume control
- Touch screen interface for intuitive local operation
- Independent health monitoring system (watchdog) for system failure detection
- Water flow measurement and logging for usage optimization
- iPhone notifications via web dashboard
- Manual override controls with touch interface
- Water level alerts for refill reminders
- Offline/connectivity failure detection and alerts

## Target Users

**Primary Users:**
1. **Technical User** (homeowner): System configuration, troubleshooting, maintenance
2. **Non-Technical User** (spouse): Basic monitoring, manual overrides, refill alerts

**Usage Patterns:**
- Daily: Status checking via iPhone
- Weekly: Reservoir refill monitoring
- Seasonal: Schedule adjustments
- Emergency: Manual overrides during WiFi outages

## Goals & Success Metrics

**Primary Goals:**
- Achieve 95%+ automated watering accuracy with precise volume control
- Enable 1+ week autonomous operation with health monitoring
- Provide reliable iPhone notifications and failure alerts
- Maintain offline functionality during network outages
- Detect and alert on system failures or connectivity issues
- Accurate water usage measurement and optimization

**Success Metrics:**
- Plant health maintained with minimal manual intervention
- Water usage measurement accuracy within ±5%
- System failure detection within 5 minutes
- System uptime >99% (excluding power outages)
- User satisfaction with both technical and non-technical users
- Touch interface usability for non-technical user

## MVP Scope

**Core Features:**
- Moisture sensor monitoring (2 plants)
- Automated pump control with safety shutoffs
- Precise water flow measurement and volume control
- Independent watchdog system with health status reporting
- Water level monitoring with low-level alerts
- Touch TFT display with intuitive interface
- Web dashboard with real-time monitoring and flow data
- iPhone-optimized interface with failure notifications
- Basic scheduling system with volume-based watering
- Manual override capabilities via touch interface

**Success Criteria:**
- 7-day autonomous operation test with health monitoring
- Both users can operate touch interface independently
- No false positive/negative watering events
- Water volume measurement accuracy validated
- Watchdog system detects simulated failures
- Responsive web interface on iPhone with flow data

## Post-MVP Vision

**Phase 2 Enhancements:**
- Weather API integration (skip watering during rain)
- Advanced scheduling with seasonal adjustments
- Historical data analytics and trends
- Multiple plant profiles with individual thresholds

**Phase 3 Integration:**
- ioBroker/Home Assistant integration
- KNX system integration
- Voice control capabilities (Alexa/Google)
- Mobile app development (if needed)
- Expansion to additional plant locations

## Technical Considerations

**Hardware Architecture:**
- ESP32 DevKit with WiFi capability (primary controller) - MicroPython
- Independent watchdog microcontroller (Arduino Nano/ATtiny85) with battery backup
- Touch TFT display (3.2" or larger with capacitive touch) - basement location
- Ultrasonic sensor (HC-SR04 or similar) for water level and usage calculation
- Capacitive soil moisture sensors (2x)
- Water pump with adequate pressure rating
- Piezo buzzer for acoustic alarms
- 18650 Li-ion battery with TP4056 charging module
- Status LEDs for system health indication
- 230V AC to 12V/5V power supply with UPS capability

**Software Stack:**
- MicroPython development environment for rapid iteration
- MQTT protocol for communication
- Web server on ESP32 (MicroPython uasyncio)
- Local data storage (JSON files/SQLite)
- Responsive HTML/CSS/JavaScript dashboard
- Touch display GUI framework (LVGL MicroPython bindings)
- Watchdog communication protocol (I2C/UART)

**Watchdog & Health Monitoring System:**
- **Independent Microcontroller**: Arduino Nano or ATtiny85
- **Health Checks**: ESP32 heartbeat monitoring, WiFi connectivity status, sensor readings validation
- **Failure Detection**: System freeze, communication timeout, sensor malfunction
- **Alert Mechanisms**: Independent LED indicators, buzzer alerts, active push notifications
- **Recovery Actions**: ESP32 reset capability, safe mode activation, pump emergency shutdown
- **Monitoring Interval**: 30-second health checks with escalating alerts
- **Battery Backup**: Li-ion battery for power outage monitoring and critical alerts
- **Active Notifications**: SMS/Email alerts for critical failures (not passive web interface)

**Water Usage Monitoring System:**
- **Primary Method**: Ultrasonic sensor water level measurement (before/after watering)
- **Calculation**: Volume consumed = tank area × water level drop
- **Accuracy**: Sufficient for usage tracking and optimization
- **Data Logging**: Volume per watering event, daily/weekly totals, efficiency trends
- **Implementation**: Software-based calculation using existing ultrasonic sensor
- **Benefits**: No additional hardware cost, reliable measurement method

**Battery Backup System:**
- **Watchdog Power**: 18650 Li-ion battery (3.7V, 2500-3000mAh)
- **Backup Duration**: 24-48 hours for monitoring and alerts
- **Charging**: Integrated TP4056 charging module with protection
- **Power Management**: Low-power sleep modes, wake on critical events
- **Monitoring**: Battery voltage monitoring and low battery alerts
- **Failsafe**: Graceful shutdown sequence when battery critically low

**Active Alert Communication System:**
- **Primary**: Acoustic alarms via piezo buzzer for critical failures
- **Secondary**: Email/Telegram alerts via WiFi (when available) for system status
- **Local Alerts**: LED status indicators and touch display notifications
- **Acoustic Patterns**: 
  - Critical: Continuous beeping (system failure, pump malfunction)
  - Warning: Intermittent beeps (low water level, sensor issues)
  - Info: Single beep (watering completed, maintenance due)
- **Escalation**: Progressive alarm intensity and frequency for unacknowledged issues
- **Silence**: Touch interface button to acknowledge and silence alarms

**Network Requirements:**
- Reliable WiFi throughout house
- Static IP assignment recommended  
- Acoustic range consideration for basement-to-living area alert audibility
- Port forwarding for remote access (optional)

## Constraints & Assumptions

**Budget Constraints:**
- Target hardware cost <€200
- Development time: 4-6 weeks part-time

**Technical Constraints:**
- Manual reservoir refill (no tap water connection)
- Existing tube infrastructure (10m length, 5m height)
- 230V power available at key locations
- Must work offline during WiFi outages

**Assumptions:**
- WiFi reliability is generally good
- Users can perform basic maintenance
- Seasonal watering needs will vary
- Future home automation integration desired

## Risks & Open Questions

**Technical Risks:**
- Pump pressure adequate for 5m lift + friction losses?
- Flow sensor accuracy at low flow rates (plant watering volumes)
- Moisture sensor accuracy and longevity in soil environment
- Water quality effects on pump, sensors, and flow measurement
- Power supply stability and backup during outages
- Watchdog system complexity and potential single points of failure
- Touch display reliability in humid basement environment

**Operational Risks:**
- User adoption of touch interface by non-technical user
- Maintenance complexity of dual-microcontroller system
- System debugging during watchdog-detected failures
- Flow sensor calibration drift over time
- False positive alerts from watchdog system

**Open Questions:**
1. Pump configuration: Single pump + solenoid valves vs. individual pumps?
2. Flow sensor placement: Before pump, after pump, or at plant delivery points?
3. Watchdog communication protocol: I2C, Serial, or dedicated GPIO?
4. Touch display size and resolution requirements for usability?
5. Water reservoir size and refill frequency preferences?
6. Preferred notification timing and escalation procedures?
7. Integration timeline with existing home automation?
8. Battery backup requirements for watchdog system?

## Next Steps

**Immediate Actions (Week 1):**
1. Finalize pump system design and component selection
2. Create detailed component list and cost estimate
3. Design PCB layout for sensor connections
4. Set up development environment and basic ESP32 framework

**Development Phase (Weeks 2-4):**
1. Develop core watering logic and safety systems
2. Implement web dashboard and iPhone interface
3. Create local display interface and manual controls
4. System integration and initial testing

**Testing & Deployment (Weeks 5-6):**
1. Comprehensive system testing with plants
2. User acceptance testing with both users
3. Final installation and configuration
4. Documentation and maintenance procedures

**Success Handoff:**
- Complete system documentation
- User training for both technical and non-technical users
- Maintenance schedule and troubleshooting guide
- Future enhancement roadmap for home automation integration