# Product Requirements Document: IoT Plant Watering System

**Version:** 1.0  
**Date:** August 5, 2025  
**Owner:** Product Manager  
**Status:** Draft  

## 1. Executive Summary

### 1.1 Product Vision
An intelligent, automated plant watering system that provides 95%+ automated care with precise volume control, independent health monitoring, and seamless user experience for both technical and non-technical users.

### 1.2 Strategic Objectives
- **Automation:** Achieve 1+ week autonomous operation with minimal user intervention
- **Reliability:** 99%+ system uptime with independent watchdog monitoring
- **Precision:** ±5% water volume measurement accuracy for optimized plant care
- **Usability:** Intuitive touch interface accessible to non-technical users
- **Integration:** Future-ready for home automation ecosystem expansion

## 2. Problem Definition

### 2.1 Current State Pain Points
| Problem | Impact | Evidence |
|---------|---------|----------|
| Manual watering inconsistency | Plant health risk | Two-window setup with limited access |
| Remote monitoring gaps | User anxiety when away | Need for iPhone notifications |
| Technical complexity barriers | User adoption risk | Mixed technical skill levels in household |
| System failure detection | Potential plant loss | No current monitoring infrastructure |

### 2.2 Market Opportunity
- **Primary Market:** Tech-savvy homeowners with existing smart home infrastructure
- **Use Case:** Premium indoor plant care automation with professional-grade monitoring
- **Differentiation:** Independent watchdog system + precise volume control + offline capability

## 3. Product Strategy

### 3.1 Target User Segments

**Primary Persona: Technical Homeowner**
- Role: System administrator, configurator, troubleshooter
- Needs: Advanced controls, detailed analytics, system integration
- Pain Points: Complex manual setup, system maintenance overhead
- Success Metrics: Configuration flexibility, integration capabilities

**Secondary Persona: Non-Technical User**
- Role: Daily monitor, manual override operator
- Needs: Simple status checks, intuitive controls, clear alerts
- Pain Points: Technical intimidation, complex interfaces
- Success Metrics: Touch interface usability, alert clarity

### 3.2 Product Positioning
"Professional-grade plant automation with consumer-friendly operation"

## 4. Functional Requirements

### 4.1 Core Features (MVP)

#### 4.1.1 Automated Watering System
**FR-001: Moisture-Based Watering**
- **Description:** System monitors 2 soil moisture sensors and triggers watering when thresholds are exceeded
- **Acceptance Criteria:**
  - Configurable moisture thresholds per plant (0-100% scale)
  - Time window restrictions (prevent night watering)
  - Volume-based watering with precise measurement
  - Safety shutoffs (max volume, max duration)
- **Priority:** P0

**FR-002: Precise Volume Control**
- **Description:** Accurate water delivery measurement using ultrasonic level sensing
- **Acceptance Criteria:**
  - ±5% volume accuracy for 50ml-500ml deliveries
  - Pre/post watering level measurements
  - Volume logging per watering event
  - Configurable volume per plant
- **Priority:** P0

#### 4.1.2 Independent Health Monitoring
**FR-003: Watchdog System**
- **Description:** Secondary microcontroller monitors primary system health
- **Acceptance Criteria:**
  - 30-second health check intervals
  - ESP32 heartbeat monitoring
  - Sensor validation checks
  - Automatic recovery actions (reset, safe mode)
  - Independent alert mechanisms
- **Priority:** P0

**FR-004: Failure Detection & Alerts**
- **Description:** Multi-channel alert system for system failures
- **Acceptance Criteria:**
  - Acoustic alerts (critical/warning/info patterns)
  - Visual LED status indicators
  - Touch display notifications
  - Email/Telegram notifications when online
  - Progressive escalation for unacknowledged alerts
- **Priority:** P0

#### 4.1.3 User Interface
**FR-005: Touch Display Interface**
- **Description:** Primary local control interface for both user types
- **Acceptance Criteria:**
  - Intuitive navigation for non-technical users
  - Real-time system status display
  - Manual watering controls with volume selection
  - Settings access with technical/basic modes
  - Alert acknowledgment and silence controls
- **Priority:** P0

**FR-006: Web Dashboard**
- **Description:** Remote monitoring and control via web interface
- **Acceptance Criteria:**
  - iPhone-optimized responsive design
  - Real-time system status and sensor readings
  - Historical data visualization (daily/weekly/monthly)
  - Remote manual controls
  - Push notifications for critical alerts
- **Priority:** P0

#### 4.1.4 System Management
**FR-007: Water Level Monitoring**
- **Description:** Reservoir level tracking with refill alerts
- **Acceptance Criteria:**
  - Continuous ultrasonic level monitoring
  - Configurable low-level thresholds
  - Refill reminders via all alert channels
  - Usage calculations and trend analysis
- **Priority:** P0

**FR-008: Offline Operation**
- **Description:** Full functionality during network outages
- **Acceptance Criteria:**
  - Local data storage and processing
  - Touch interface remains fully functional
  - Acoustic alerts continue operating
  - Data sync when connectivity restored
- **Priority:** P0

### 4.2 Phase 2 Features (Post-MVP)

**FR-009: Weather Integration**
- Skip watering during forecasted rain
- Outdoor humidity adjustments

**FR-010: Advanced Analytics**
- Plant health trending
- Watering efficiency optimization
- Seasonal adjustment recommendations

**FR-011: Home Automation Integration**
- ioBroker/Home Assistant compatibility
- KNX system integration
- Voice control support

## 5. Non-Functional Requirements

### 5.1 Performance Requirements
| Requirement | Target | Measurement |
|-------------|---------|-------------|
| System Response Time | <2 seconds | Touch interface actions |
| Web Dashboard Load Time | <3 seconds | iPhone over WiFi |
| Sensor Reading Frequency | 30 seconds | Moisture/level monitoring |
| Pump Response Time | <5 seconds | Watering trigger to flow |

### 5.2 Reliability Requirements
| Requirement | Target | Measurement |
|-------------|---------|-------------|
| System Uptime | 99%+ | Excluding power outages |
| Failure Detection Time | <5 minutes | Watchdog monitoring |
| Battery Backup Duration | 24-48 hours | Watchdog operation |
| Volume Measurement Accuracy | ±5% | 50ml-500ml range |

### 5.3 Usability Requirements
- Touch interface operable by non-technical users within 2 minutes training
- Web dashboard accessible on iPhone with no scrolling for key functions
- Alert acknowledgment within 3 taps maximum
- Visual status indicators visible from 3 meters distance

### 5.4 Security Requirements
- Local network operation (no cloud dependencies)
- Optional secure remote access via VPN
- Configuration backup/restore capability
- Fail-safe pump shutoff mechanisms

## 6. Technical Architecture

### 6.1 Hardware Components
**Primary Controller:**
- ESP32 DevKit (WiFi, MicroPython)
- 3.2" Capacitive Touch TFT Display
- Ultrasonic Water Level Sensor (HC-SR04)
- 2x Capacitive Soil Moisture Sensors

**Independent Watchdog:**
- Arduino Nano/ATtiny85
- 18650 Li-ion Battery + TP4056 Charger
- Status LED Array
- Piezo Buzzer

**Power & Pump System:**
- 230V AC to 12V/5V Power Supply
- Water Pump (5m lift + 10m horizontal capability)
- Safety Relays and Shutoff Valves

### 6.2 Software Stack
- **Primary:** MicroPython on ESP32
- **Communication:** MQTT Protocol
- **Web Server:** uasyncio-based HTTP server
- **UI Framework:** LVGL MicroPython bindings
- **Data Storage:** JSON files with SQLite migration path
- **Dashboard:** Responsive HTML/CSS/JavaScript

### 6.3 Integration Points
- **Current:** WiFi network, iPhone notifications
- **Future:** ioBroker, Home Assistant, KNX, Voice assistants

## 7. Success Metrics & KPIs

### 7.1 Product Success Metrics
| Metric | Target | Measurement Method |
|--------|---------|-------------------|
| Autonomous Operation | 7+ days | Continuous operation test |
| User Satisfaction | 4.5/5 | Both user personas survey |
| System Reliability | 99%+ uptime | Watchdog monitoring logs |
| Water Usage Accuracy | ±5% variance | Volume measurement validation |
| Alert Response Time | <5 minutes | Failure simulation tests |

### 7.2 User Experience Metrics
| Metric | Target | Measurement Method |
|--------|---------|-------------------|
| Touch Interface Adoption | 100% by non-technical user | Usage analytics |
| Setup Time | <30 minutes | Initial configuration tracking |
| False Alert Rate | <1 per month | Alert log analysis |
| Manual Override Usage | <1 per week | System usage logs |

## 8. Implementation Roadmap

### 8.1 MVP Development (6 Weeks)

**Week 1: Foundation & Design**
- Component selection and procurement
- PCB design and development environment setup
- Basic ESP32 framework and sensor integration

**Weeks 2-3: Core Systems**
- Watering logic with safety systems
- Watchdog implementation and testing
- Volume measurement system development

**Weeks 4-5: User Interfaces**
- Touch display interface development
- Web dashboard creation and iPhone optimization
- Alert system implementation and testing

**Week 6: Integration & Testing**
- End-to-end system testing with live plants
- User acceptance testing with both personas
- Documentation and handoff preparation

### 8.2 Post-MVP Phases

**Phase 2 (Months 2-3): Intelligence**
- Weather API integration
- Advanced analytics and trending
- Optimization algorithms

**Phase 3 (Months 4-6): Integration**
- Home automation platform integration
- Voice control capabilities
- Mobile app development (if required)

## 9. Risk Assessment

### 9.1 Technical Risks
| Risk | Probability | Impact | Mitigation Strategy |
|------|------------|---------|-------------------|
| Pump pressure insufficient | Medium | High | Early pressure testing, backup pump options |
| Volume measurement accuracy | Medium | Medium | Multiple sensor validation, calibration procedures |
| Watchdog system complexity | High | Medium | Simplified initial implementation, iterative enhancement |
| WiFi reliability issues | Low | Medium | Robust offline mode, local data storage |

### 9.2 User Experience Risks
| Risk | Probability | Impact | Mitigation Strategy |
|------|------------|---------|-------------------|
| Non-technical user adoption | Medium | High | Extensive usability testing, simplified interface |
| Alert fatigue | Medium | Medium | Smart escalation, configurable sensitivity |
| Maintenance complexity | Medium | Medium | Clear documentation, diagnostic tools |

## 10. Success Criteria & Go-Live Requirements

### 10.1 MVP Launch Criteria
✅ **Technical Validation:**
- [ ] 7-day autonomous operation test passed
- [ ] Volume measurement accuracy validated (±5%)
- [ ] Watchdog system detects simulated failures
- [ ] Both users can operate touch interface independently
- [ ] Web dashboard responsive on iPhone
- [ ] No false positive/negative watering events in 48-hour test

✅ **User Acceptance:**
- [ ] Non-technical user can acknowledge alerts within 2 attempts
- [ ] Technical user can configure thresholds and schedules
- [ ] Both users rate interface usability ≥4/5
- [ ] Emergency manual controls accessible and functional

✅ **System Reliability:**
- [ ] Offline operation maintains full functionality
- [ ] Battery backup provides 24+ hours of monitoring
- [ ] Acoustic alerts audible throughout target range
- [ ] System recovery after simulated failures

### 10.2 Post-Launch Success Indicators (30 days)
- Zero unplanned watering events
- <2 support requests per month
- 95%+ automated watering (minimal manual intervention)
- User satisfaction maintained ≥4/5 for both personas

## 11. Appendices

### 11.1 User Stories
**As a technical user, I want** detailed system analytics **so that** I can optimize watering schedules and detect trends.

**As a non-technical user, I want** simple status indicators **so that** I can quickly understand if action is needed.

**As any user, I want** immediate alerts for system failures **so that** I can prevent plant damage.

**As a technical user, I want** manual override controls **so that** I can handle edge cases and maintenance.

**As a non-technical user, I want** one-touch watering **so that** I can supplement automatic care when needed.

### 11.2 Technical Specifications
[Detailed component specifications, wiring diagrams, and API documentation to be maintained in separate technical documents]

### 11.3 Competitive Analysis
[Analysis of existing plant watering solutions and differentiation strategy]

---

**Document Status:** ✅ Ready for stakeholder review  
**Next Review Date:** August 12, 2025  
**Approval Required:** Technical Lead, End Users