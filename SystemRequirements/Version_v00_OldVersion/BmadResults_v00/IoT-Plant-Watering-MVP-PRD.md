# MVP Product Requirements: IoT Plant Watering System

**Version:** 1.0 - MVP Focused  
**Date:** August 6, 2025  
**Timeline:** 6 weeks  
**Budget:** €200  
**Status:** Ready for Development  

## 1. MVP Vision & Strategy

### 1.1 Core Problem
**Manual plant watering is inconsistent and requires constant attention** for 2 plants in living room windows with limited access.

### 1.2 MVP Solution
**Single ESP32-based automated watering system** with moisture monitoring, web dashboard, and basic manual controls.

### 1.3 Success Definition
✅ **5-day autonomous watering** without manual intervention  
✅ **Both users can operate** touch controls independently  
✅ **Basic iPhone monitoring** with status/alerts  
✅ **€200 budget compliance** with reliable operation  

## 2. MVP Scope (What's IN)

### 2.1 Core Features ✅

**🌱 Automated Watering**
- 2x moisture sensor monitoring 
- Configurable thresholds per plant
- Volume-based watering (100ml-500ml range)
- Safety shutoffs (max time, max volume)
- Time window controls (no night watering)

**💧 Basic Volume Control**
- Ultrasonic level sensor (before/after measurement)
- Simple volume calculation (sufficient accuracy)
- Basic usage logging
- Low water level alerts

**📱 Essential Interface**
- Touch display with basic controls (manual water, status, settings)
- Web dashboard (iPhone-optimized)
- Real-time status and sensor readings
- Manual watering controls

**🔔 Simple Alerts**
- Touch display notifications
- Web dashboard alerts
- Basic email notifications (when WiFi available)
- Low water level warnings

**⚡ Core Reliability**
- Offline operation (local storage)
- Basic pump safety (timeout, leak detection)
- Simple error recovery (system restart)

### 2.2 Hardware (Simplified) 💰

**Primary System (~€150):**
- ESP32 DevKit (€15)
- 2.8" Touch TFT Display (€25)
- HC-SR04 Ultrasonic Sensor (€5)
- 2x Capacitive Moisture Sensors (€20)
- 12V Water Pump (€35)
- Power Supply 230V→12V/5V (€25)
- Relays, wiring, enclosure (€25)

**Budget Reserve (€50):**
- Contingency for pump upgrades
- Additional safety components
- Testing materials

## 3. MVP Scope (What's OUT - Phase 2)

### 3.1 Advanced Features ⏭️
- ❌ Independent watchdog microcontroller
- ❌ Battery backup system
- ❌ Acoustic alert system
- ❌ Precise flow measurement sensors
- ❌ Advanced failure detection
- ❌ Weather API integration
- ❌ Home automation integration

### 3.2 Why These Are Phase 2
**Complexity Reduction:** Single microcontroller = faster development  
**Budget Focus:** Core functionality vs. premium features  
**Risk Mitigation:** Prove basic concept before advanced monitoring  
**Timeline Reality:** 6 weeks for reliable core system  

## 4. User Stories (MVP Only)

### 4.1 Technical User Stories
- **As technical user**, I want configurable moisture thresholds **so I can** optimize per plant
- **As technical user**, I want web dashboard access **so I can** monitor remotely  
- **As technical user**, I want manual override controls **so I can** handle edge cases
- **As technical user**, I want basic system logs **so I can** troubleshoot issues

### 4.2 Non-Technical User Stories  
- **As non-technical user**, I want simple touch controls **so I can** water plants manually
- **As non-technical user**, I want clear status display **so I can** see if action needed
- **As non-technical user**, I want refill alerts **so I know** when to add water
- **As non-technical user**, I want iPhone notifications **so I know** system status

## 5. MVP Requirements

### 5.1 Functional Requirements (Simplified)

**FR-001: Basic Moisture Monitoring**
- Monitor 2 sensors every 30 seconds
- Trigger watering when threshold exceeded
- Configurable thresholds (0-100%)
- Time window restrictions (8AM-8PM only)

**FR-002: Simple Volume Control** 
- Fixed volume per plant (200ml default, 100-500ml configurable)
- Ultrasonic before/after level measurement
- Basic volume calculation and logging
- Max watering time safety (60 seconds)

**FR-003: Touch Interface**
- System status display (sensor readings, last watering)
- Manual water buttons (Plant 1, Plant 2)  
- Basic settings (thresholds, volumes)
- Low water level display

**FR-004: Web Dashboard**
- iPhone-optimized responsive design
- Real-time sensor data
- Manual watering buttons
- Basic historical data (last 7 days)
- Simple alert notifications

**FR-005: Basic Alerts**
- Touch display notifications
- Email alerts for critical issues (pump failure, empty reservoir)
- iPhone push notifications via web app

### 5.2 Non-Functional Requirements (Realistic)

| Requirement | MVP Target | Measurement |
|-------------|------------|-------------|
| Autonomous Operation | 5 days | Continuous test |
| System Response | <5 seconds | Touch to pump action |
| Web Dashboard Load | <5 seconds | iPhone over WiFi |
| Budget Compliance | €200 total | Component cost tracking |
| Setup Time | <30 minutes | Both users |

## 6. Technical Architecture (Simplified)

### 6.1 Hardware Design
```
ESP32 DevKit
├── Touch TFT Display (GPIO pins)
├── HC-SR04 Ultrasonic (GPIO pins)  
├── 2x Moisture Sensors (ADC pins)
├── Pump Relay (GPIO pin)
└── Power Supply (12V/5V)
```

### 6.2 Software Stack
- **Platform:** MicroPython on ESP32
- **Web Server:** Simple HTTP server (uasyncio)
- **Data Storage:** JSON files on flash
- **Communication:** WiFi only (no MQTT complexity)
- **UI:** Basic HTML/CSS responsive design

### 6.3 Safety Systems (Essential Only)
- Maximum watering time (60s timeout)
- Pump dry-run protection (level check before start)
- Basic leak detection (continuous pumping alert)
- Manual emergency stop via touch interface

## 7. 6-Week Development Plan

### Week 1: Hardware & Foundation
- [ ] Component procurement and testing
- [ ] ESP32 development environment setup  
- [ ] Basic sensor reading (moisture + ultrasonic)
- [ ] Pump control and safety testing

### Week 2: Core Logic
- [ ] Watering logic implementation
- [ ] Volume calculation system
- [ ] Basic data logging
- [ ] Safety system integration

### Week 3: Touch Interface
- [ ] TFT display setup and basic UI
- [ ] Status display and manual controls
- [ ] Settings configuration interface
- [ ] Alert display system

### Week 4: Web Dashboard  
- [ ] HTTP server implementation
- [ ] iPhone-optimized web interface
- [ ] Real-time data API
- [ ] Manual control web interface

### Week 5: Integration Testing
- [ ] End-to-end system testing
- [ ] 5-day autonomous operation test
- [ ] User acceptance testing
- [ ] Performance optimization

### Week 6: Deployment & Documentation
- [ ] Final installation and calibration
- [ ] User training and handoff
- [ ] Basic documentation
- [ ] Phase 2 planning

## 8. Success Criteria (MVP)

### 8.1 Go-Live Requirements ✅
- [ ] **5-day test passed:** System operates autonomously for 5 days
- [ ] **User adoption:** Both users can operate touch interface independently  
- [ ] **No plant damage:** Zero over/under watering events in testing
- [ ] **Budget compliance:** Total cost ≤€200
- [ ] **Basic reliability:** System recovers from WiFi outages automatically
- [ ] **iPhone access:** Web dashboard functional on iPhone

### 8.2 30-Day Success Metrics
- **Plant Health:** No manual watering needed (autonomous success)
- **User Satisfaction:** Both users rate usability ≥4/5
- **System Uptime:** 90%+ operational time (realistic for prototype)
- **Support Requests:** <1 per week average

## 9. Risk Management (Simplified)

### 9.1 High-Risk Items ⚠️
| Risk | Probability | Mitigation |
|------|-------------|------------|
| Pump insufficient pressure | Medium | Early pressure testing, backup pump option |
| Touch display reliability | Medium | Protective enclosure, humidity consideration |
| User adoption (non-technical) | Medium | Simple UI design, extensive testing |

### 9.2 Budget Risk Mitigation
- **Component buffer:** €50 reserve for upgrades
- **Pump sizing:** Test pressure requirements before final selection  
- **Display choice:** 2.8" vs 3.2" based on budget/usability balance

## 10. Phase 2 Roadmap (Post-MVP)

### 10.1 Enhanced Reliability (Weeks 7-10)
- Independent watchdog system
- Battery backup for monitoring
- Acoustic alert system
- Advanced failure detection

### 10.2 Smart Features (Weeks 11-14)  
- Precise flow measurement
- Weather API integration
- Advanced analytics and optimization
- Home automation integration prep

### 10.3 Integration (Weeks 15-18)
- ioBroker/Home Assistant compatibility  
- Voice control capabilities
- Mobile app (if needed)
- Multi-location expansion

## 11. Definition of Done

**MVP is complete when:**
✅ Both users can successfully operate the system independently  
✅ System runs autonomously for 5 days without intervention  
✅ Web dashboard provides real-time status on iPhone  
✅ No false watering events during 48-hour test period  
✅ Total component cost documented at ≤€200  
✅ Basic user documentation created  
✅ Phase 2 requirements and timeline defined  

---

**🎯 Focus Statement:** "Build a reliable, simple automated watering system that both users can confidently operate within 6 weeks and €200 budget."

**Next Action:** Component procurement and development environment setup (Week 1)