# Detailed User Stories Backlog - Plant Watering System MVP

**Generated:** August 6, 2025  
**Source:** Development-Epics-Breakdown.md  
**Total Stories:** 22  
**Timeline:** 6 weeks  
**Story Points:** 213 total  

---

# EPIC 1: HARDWARE FOUNDATION (Week 1)

## Story E1.1: Component Procurement & Validation
**Story Points:** 5 | **Priority:** P0 | **Sprint:** Week 1 | **Owner:** Technical Lead

### User Story
```
As a technical user
I want all hardware components procured and tested  
So that development can proceed without hardware blockers
```

### Acceptance Criteria
- [ ] **ESP32 DevKit** - Functional and programmable via USB
  - Verify GPIO pins operational (digital/analog/PWM)
  - Test WiFi connectivity and stability
  - Validate power consumption and heat generation
- [ ] **2.8" Touch TFT Display** - Operational with test patterns
  - Touch responsiveness tested across entire screen
  - Color accuracy and brightness suitable for basement environment
  - SPI communication stable with ESP32
- [ ] **HC-SR04 Ultrasonic Sensor** - Accurate distance readings
  - Range testing from 2cm to 400cm
  - Accuracy validation ±2cm across full range
  - Temperature compensation functional
- [ ] **2x Moisture Sensors** - Calibrated 0-100% readings
  - Dry soil calibration (0% baseline)
  - Saturated soil calibration (100% baseline)
  - Linear response curve validation
- [ ] **12V Pump** - Pressure capability tested
  - 5m vertical lift capability confirmed
  - 10m horizontal flow with acceptable pressure
  - Flow rate measurement (L/min)
- [ ] **Power Supply** - Stable 12V/5V with safety margin
  - Load testing at maximum current draw
  - Voltage stability under pump operation
  - Safety shutoff testing
- [ ] **Component Cost Tracking** - Within €150 allocation
  - Detailed cost breakdown with receipts
  - Budget variance analysis
  - Contingency planning for overruns

### Technical Implementation
```python
# Hardware validation test suite
class HardwareValidator:
    def __init__(self):
        self.test_results = {}
    
    def test_esp32_gpio(self):
        # Test all required GPIO pins
        # Return pass/fail status
        
    def test_sensors(self):
        # Validate sensor readings and calibration
        # Document calibration values
        
    def test_pump_pressure(self):
        # Measure actual lift and flow capabilities
        # Document performance characteristics
```

### Testing Strategy
- **Unit Tests:** Individual component functionality
- **Integration Tests:** ESP32-component communication
- **Performance Tests:** Under load conditions
- **Environmental Tests:** Basement temperature/humidity conditions

### Definition of Done
✅ All components tested and documented  
✅ ESP32 development environment functional  
✅ Component compatibility verified  
✅ Budget tracking accurate and on-target  
✅ Next story dependencies met  

---

## Story E1.2: Development Environment Setup
**Story Points:** 3 | **Priority:** P0 | **Sprint:** Week 1 | **Owner:** Technical Lead

### User Story
```
As a developer
I want MicroPython development environment configured
So that I can efficiently write and deploy code
```

### Acceptance Criteria
- [ ] **MicroPython Installation** - Flashed to ESP32 successfully
  - Latest stable MicroPython version installed
  - Boot process verified and stable
  - File system accessible and writable
- [ ] **IDE Configuration** - Configured for ESP32 development
  - Thonny or VSCode with MicroPython extension
  - Serial connection stable and reliable
  - Syntax highlighting and code completion functional
- [ ] **GPIO Pin Mapping** - Documented and tested
  - Physical pin diagram created
  - Pin assignments for all components documented
  - Pin conflict analysis completed
- [ ] **Basic Scripts** - Sensor reading scripts working
  - "Hello World" test script
  - Basic GPIO control (LED blink)
  - Sensor reading examples for all components
- [ ] **File Management** - Transfer to ESP32 operational
  - Code upload/download process defined
  - Project folder structure established
  - Backup and version control procedures
- [ ] **Version Control** - Setup for project
  - Git repository initialized
  - .gitignore configured for MicroPython projects
  - Commit workflow established

### Technical Implementation
```python
# Project structure
/plant_watering_system/
├── main.py                 # Main application entry
├── config.py              # Configuration constants
├── sensors/
│   ├── moisture.py        # Moisture sensor handling
│   ├── ultrasonic.py      # Water level sensing
│   └── __init__.py
├── hardware/
│   ├── pump.py            # Pump control
│   ├── display.py         # TFT display management
│   └── __init__.py
├── utils/
│   ├── logging.py         # Data logging utilities
│   └── wifi.py            # Network management
└── tests/
    └── hardware_tests.py  # Hardware validation tests
```

### Testing Strategy
- **Development Environment Test:** Complete code-compile-deploy cycle
- **Communication Test:** Reliable ESP32-IDE connection
- **File System Test:** Read/write operations on ESP32
- **Version Control Test:** Commit and branch operations

### Definition of Done
✅ MicroPython development environment fully operational  
✅ Code deployment process streamlined (<30 seconds)  
✅ Project structure established and documented  
✅ Version control functional and committed  
✅ Development workflow validated  

---

## Story E1.3: Sensor Integration & Calibration
**Story Points:** 8 | **Priority:** P0 | **Sprint:** Week 1 | **Owner:** Technical Lead

### User Story
```
As a technical user
I want all sensors accurately calibrated and integrated
So that watering decisions are based on reliable data
```

### Acceptance Criteria
- [ ] **Moisture Sensor Calibration** - Accurate 0-100% scale
  - Dry soil calibration procedure documented (0% baseline)
  - Saturated soil calibration procedure documented (100% baseline)
  - Linear interpolation algorithm implemented
  - Calibration values stored in persistent configuration
- [ ] **Ultrasonic Sensor Setup** - ±2cm accuracy for water level
  - Distance measurement algorithm implemented
  - Temperature compensation active
  - Noise filtering for stable readings
  - Edge case handling (no echo, out of range)
- [ ] **Reading Frequency** - 30-second interval system
  - Consistent timing implementation using timers
  - CPU usage optimization for continuous operation
  - Data buffering for temporary storage
- [ ] **Data Filtering** - Noise reduction implemented
  - Moving average filter for sensor stability
  - Outlier detection and rejection
  - Sensor health monitoring (stuck values, drift)
- [ ] **GPIO Integration** - Pin mapping documented and tested
  - Physical wiring diagram created and validated
  - Pin conflict analysis completed
  - Electrical characteristic testing (voltage levels, current draw)
- [ ] **Failure Detection** - Timeout and range checking
  - Sensor timeout handling (unresponsive sensors)
  - Range validation (impossible readings)
  - Graceful degradation procedures
  - Error logging and user notification

### Technical Implementation
```python
# Sensor management system
class SensorManager:
    def __init__(self):
        self.moisture_sensors = [MoistureSensor(pin=32), MoistureSensor(pin=33)]
        self.level_sensor = UltrasonicSensor(trigger_pin=5, echo_pin=18)
        self.calibration = self.load_calibration()
        
    def calibrate_moisture_sensors(self):
        # Interactive calibration procedure
        # Store calibration values to config file
        
    def read_all_sensors(self):
        # Read all sensors with error handling
        # Apply filtering and calibration
        # Return structured sensor data
        
    def validate_readings(self, readings):
        # Range checking and outlier detection
        # Return validated data with quality indicators

class MoistureSensor:
    def __init__(self, pin, calibration_dry=None, calibration_wet=None):
        self.pin = Pin(pin, Pin.IN)
        self.adc = ADC(self.pin)
        self.cal_dry = calibration_dry or 4095  # Default values
        self.cal_wet = calibration_wet or 1500
        
    def read_raw(self):
        return self.adc.read()
        
    def read_percentage(self):
        raw = self.read_raw()
        # Convert to 0-100% scale using calibration
        percentage = ((self.cal_dry - raw) / (self.cal_dry - self.cal_wet)) * 100
        return max(0, min(100, percentage))  # Clamp to 0-100%

class UltrasonicSensor:
    def __init__(self, trigger_pin, echo_pin):
        self.trigger = Pin(trigger_pin, Pin.OUT)
        self.echo = Pin(echo_pin, Pin.IN)
        
    def measure_distance(self):
        # HC-SR04 measurement protocol
        # Return distance in cm with error handling
        
    def measure_water_level(self, tank_height_cm):
        # Calculate water level from distance measurement
        # Return water level percentage
```

### Testing Strategy
- **Calibration Test:** Verify 0% and 100% moisture readings
- **Accuracy Test:** Compare ultrasonic readings with manual measurement
- **Stability Test:** 24-hour continuous reading validation
- **Environmental Test:** Performance in target basement conditions
- **Edge Case Test:** Sensor disconnection, out-of-range scenarios

### Definition of Done
✅ All sensors calibrated and providing accurate readings  
✅ 30-second reading cycle stable and consistent  
✅ Data filtering effective for noise reduction  
✅ Error handling comprehensive and tested  
✅ Documentation complete for maintenance procedures  

---

# EPIC 2: CORE WATERING LOGIC (Week 2)

## Story E2.1: Moisture Monitoring System
**Story Points:** 8 | **Priority:** P0 | **Sprint:** Week 2 | **Owner:** Technical Lead

### User Story
```
As a plant owner  
I want the system to continuously monitor soil moisture
So that my plants receive water when needed
```

### Acceptance Criteria
- [ ] **Continuous Monitoring** - 30-second reading intervals
  - Timer-based sensor reading implementation
  - CPU-efficient monitoring loop
  - Battery usage optimization for future expansion
- [ ] **Individual Thresholds** - Configurable per plant (0-100%)
  - Plant 1 and Plant 2 independent threshold settings
  - Threshold persistence across system restarts
  - Real-time threshold adjustment capability
- [ ] **Trigger Logic** - Threshold breach detection
  - Immediate watering trigger when moisture < threshold
  - Hysteresis implementation to prevent oscillation
  - Multiple reading confirmation before triggering
- [ ] **Time Windows** - 8AM-8PM watering enforcement
  - Configurable start/end times
  - Time zone handling and DST adjustment
  - Override capability for emergency watering
- [ ] **Data Logging** - Timestamped sensor data
  - JSON-based data storage on ESP32 flash
  - Circular buffer for memory management
  - Data export capability for analysis
- [ ] **Failure Handling** - Multiple sensor backup logic
  - Single sensor failure detection and graceful degradation
  - User notification for sensor malfunctions
  - Manual override when sensors unavailable

### Technical Implementation
```python
# Moisture monitoring core system
class MoistureMonitor:
    def __init__(self, sensors, config):
        self.sensors = sensors
        self.config = config
        self.last_readings = {}
        self.watering_history = []
        
    async def monitor_loop(self):
        """Main monitoring loop with 30-second intervals"""
        while True:
            try:
                readings = self.read_all_sensors()
                self.log_readings(readings)
                
                for plant_id, reading in readings.items():
                    if self.should_water(plant_id, reading):
                        await self.trigger_watering(plant_id)
                        
                await asyncio.sleep(30)  # 30-second intervals
                
            except Exception as e:
                self.log_error(f"Monitor loop error: {e}")
                await asyncio.sleep(10)  # Shorter retry interval
                
    def should_water(self, plant_id, moisture_level):
        """Determine if watering is needed"""
        threshold = self.config.get_threshold(plant_id)
        
        # Check moisture level
        if moisture_level >= threshold:
            return False
            
        # Check time window
        if not self.is_watering_time():
            return False
            
        # Check recent watering history (prevent over-watering)
        if self.recently_watered(plant_id, hours=2):
            return False
            
        return True
        
    def is_watering_time(self):
        """Check if current time is within watering window"""
        current_hour = time.localtime()[3]
        start_hour = self.config.watering_start_hour  # 8 (8AM)
        end_hour = self.config.watering_end_hour      # 20 (8PM)
        
        return start_hour <= current_hour <= end_hour

class PlantConfig:
    def __init__(self):
        self.plant_thresholds = {
            'plant1': 30,  # Water when moisture < 30%
            'plant2': 25   # Water when moisture < 25%
        }
        self.watering_volumes = {
            'plant1': 200,  # 200ml default
            'plant2': 200
        }
        self.watering_start_hour = 8   # 8AM
        self.watering_end_hour = 20    # 8PM
        
    def save_config(self):
        """Persist configuration to JSON file"""
        config_data = {
            'thresholds': self.plant_thresholds,
            'volumes': self.watering_volumes,
            'time_window': {
                'start': self.watering_start_hour,
                'end': self.watering_end_hour
            }
        }
        
        with open('/config/plant_config.json', 'w') as f:
            json.dump(config_data, f)
```

### Testing Strategy
- **Monitoring Test:** 24-hour continuous operation validation
- **Threshold Test:** Verify accurate trigger points for both plants
- **Time Window Test:** Confirm watering only occurs during 8AM-8PM
- **Failure Test:** Sensor disconnection and error recovery
- **Data Logging Test:** Verify data persistence and retrieval

### Definition of Done
✅ Continuous monitoring operational for both plants  
✅ Individual thresholds configurable and persistent  
✅ Time window enforcement functional and tested  
✅ Data logging accurate and accessible  
✅ Failure scenarios handled gracefully  

---

## Story E2.2: Volume Control & Measurement
**Story Points:** 13 | **Priority:** P0 | **Sprint:** Week 2 | **Owner:** Technical Lead

### User Story
```
As a technical user
I want precise volume control for each watering event
So that plants receive optimal water amounts without waste
```

### Acceptance Criteria
- [ ] **Volume Calculation** - Using ultrasonic before/after measurement
  - Pre-watering water level measurement
  - Post-watering water level measurement
  - Tank cross-sectional area configuration
  - Volume calculation: (level_drop_cm × tank_area_cm²) ÷ 1000 = liters
- [ ] **Configurable Volumes** - Per plant (100ml-500ml range)
  - Individual volume settings for each plant
  - Real-time volume adjustment capability
  - Volume persistence across restarts
  - Input validation (range checking)
- [ ] **Default Settings** - 200ml per plant baseline
  - Factory default configuration
  - Easy reset to defaults capability
  - Recommended volume guidelines per plant type
- [ ] **Volume Accuracy** - ±10% for plant care (sufficient precision)
  - Accuracy validation through measurement
  - Calibration procedure for tank geometry
  - Error tolerance acceptable for plant health
- [ ] **Event Logging** - Timestamp, volume, plant tracking
  - Detailed watering event records
  - Data export for usage analysis
  - Historical volume tracking and trends
- [ ] **Usage Analytics** - Tracking and optimization
  - Daily/weekly volume summaries
  - Efficiency trending over time
  - Plant-specific consumption patterns

### Technical Implementation
```python
# Volume control and measurement system
class VolumeController:
    def __init__(self, ultrasonic_sensor, pump_controller, config):
        self.level_sensor = ultrasonic_sensor
        self.pump = pump_controller
        self.config = config
        self.tank_area_cm2 = config.tank_cross_sectional_area  # cm²
        
    async def water_plant(self, plant_id, target_volume_ml):
        """Execute controlled watering with volume measurement"""
        try:
            # Pre-watering measurements
            initial_level = self.level_sensor.measure_water_level()
            start_time = time.time()
            
            # Calculate estimated pump duration
            estimated_duration = self.estimate_pump_duration(target_volume_ml)
            
            # Start pumping with monitoring
            self.pump.start(plant_id)
            pumping_start = time.time()
            
            # Monitor pumping with safety timeout
            while (time.time() - pumping_start) < estimated_duration:
                current_level = self.level_sensor.measure_water_level()
                delivered_volume = self.calculate_volume_delivered(initial_level, current_level)
                
                # Check if target volume reached
                if delivered_volume >= target_volume_ml:
                    break
                    
                # Safety timeout (max 60 seconds)
                if (time.time() - pumping_start) > 60:
                    self.log_error("Pump safety timeout reached")
                    break
                    
                await asyncio.sleep(0.5)  # Check every 0.5 seconds
                
            # Stop pump and final measurement
            self.pump.stop()
            await asyncio.sleep(2)  # Allow water level to settle
            
            final_level = self.level_sensor.measure_water_level()
            actual_volume = self.calculate_volume_delivered(initial_level, final_level)
            
            # Log watering event
            watering_event = {
                'timestamp': time.time(),
                'plant_id': plant_id,
                'target_volume_ml': target_volume_ml,
                'actual_volume_ml': actual_volume,
                'accuracy_percent': (actual_volume / target_volume_ml) * 100,
                'duration_seconds': time.time() - start_time,
                'initial_level_cm': initial_level,
                'final_level_cm': final_level
            }
            
            self.log_watering_event(watering_event)
            return watering_event
            
        except Exception as e:
            self.pump.stop()  # Emergency stop
            self.log_error(f"Watering error: {e}")
            raise
            
    def calculate_volume_delivered(self, initial_level_cm, current_level_cm):
        """Calculate volume based on water level change"""
        level_drop_cm = initial_level_cm - current_level_cm
        
        if level_drop_cm <= 0:
            return 0  # No volume delivered or sensor error
            
        # Volume = level_drop × tank_area (convert cm³ to ml)
        volume_ml = level_drop_cm * self.tank_area_cm2
        return max(0, volume_ml)  # Ensure positive volume
        
    def estimate_pump_duration(self, target_volume_ml):
        """Estimate pump duration based on flow rate"""
        # Use historical data or pump specifications
        estimated_flow_rate_ml_per_sec = self.config.pump_flow_rate
        return target_volume_ml / estimated_flow_rate_ml_per_sec

class WateringAnalytics:
    def __init__(self):
        self.events = []
        
    def add_event(self, event):
        self.events.append(event)
        self.save_events()
        
    def get_daily_usage(self, date):
        """Calculate total volume used on specific date"""
        daily_events = [e for e in self.events if self.is_same_date(e['timestamp'], date)]
        return sum(e['actual_volume_ml'] for e in daily_events)
        
    def get_plant_efficiency(self, plant_id, days=7):
        """Calculate watering efficiency for specific plant"""
        recent_events = self.get_recent_events(plant_id, days)
        if not recent_events:
            return None
            
        total_target = sum(e['target_volume_ml'] for e in recent_events)
        total_actual = sum(e['actual_volume_ml'] for e in recent_events)
        
        return (total_actual / total_target) * 100 if total_target > 0 else 0
```

### Testing Strategy
- **Volume Accuracy Test:** Compare calculated vs. actual water delivery
- **Range Test:** Validate 100ml-500ml delivery capability
- **Consistency Test:** Multiple watering events with same target volume
- **Safety Test:** Maximum duration timeout and emergency stop
- **Analytics Test:** Data logging and reporting accuracy

### Definition of Done
✅ Volume control accurate within ±10% for 100-500ml range  
✅ Individual plant volume configuration functional  
✅ Watering events logged with complete data  
✅ Safety timeouts and error handling operational  
✅ Usage analytics providing meaningful insights  

---

## Story E2.3: Safety Systems & Pump Control
**Story Points:** 13 | **Priority:** P0 | **Sprint:** Week 2 | **Owner:** Technical Lead

### User Story
```
As a system user
I want comprehensive safety systems to prevent damage
So that the system operates safely without supervision
```

### Acceptance Criteria
- [ ] **Maximum Duration Limit** - 60-second timeout per watering event
  - Hard timeout enforcement regardless of volume target
  - Automatic pump shutdown after timeout
  - Alert generation for timeout events
  - Timeout value configurable for different scenarios
- [ ] **Dry-Run Protection** - Level check before pump start
  - Minimum water level verification before pumping
  - User alert for low reservoir level
  - Pump disable when water level critically low
  - Graceful degradation with manual override option
- [ ] **Continuous Flow Detection** - Alert for pump malfunctions
  - Monitor for abnormal continuous pumping scenarios
  - Leak detection through unexpected level changes
  - Pump seizure detection (current monitoring if possible)
  - Automatic shutdown and user notification
- [ ] **Emergency Stop** - Manual override capability
  - Touch interface emergency stop button
  - Web dashboard emergency stop button
  - Immediate pump shutdown with status logging
  - Manual reset required after emergency stop
- [ ] **Relay Control** - Fail-safe positioning
  - Normally-open relay configuration (fail-safe off)
  - Relay state monitoring and validation
  - Power-on self-test for relay functionality
  - Backup relay option for critical applications
- [ ] **Error Logging** - Comprehensive safety event recording
  - All safety events logged with timestamps
  - Error categorization (warning, critical, emergency)
  - Automatic log rotation and storage management
  - Export capability for troubleshooting

### Technical Implementation
```python
# Safety and pump control system
class SafetyController:
    def __init__(self, pump, level_sensor, config):
        self.pump = pump
        self.level_sensor = level_sensor
        self.config = config
        self.safety_status = {
            'emergency_stop': False,
            'low_water_lockout': False,
            'pump_malfunction': False
        }
        self.safety_log = []
        
    def check_safety_conditions(self):
        """Comprehensive safety check before any pump operation"""
        safety_issues = []
        
        # Check emergency stop status
        if self.safety_status['emergency_stop']:
            safety_issues.append("Emergency stop active - manual reset required")
            
        # Check water level
        current_level = self.level_sensor.measure_water_level()
        min_level_cm = self.config.minimum_water_level
        
        if current_level < min_level_cm:
            safety_issues.append(f"Water level too low: {current_level}cm < {min_level_cm}cm")
            self.safety_status['low_water_lockout'] = True
            
        # Check pump health
        if self.safety_status['pump_malfunction']:
            safety_issues.append("Pump malfunction detected - service required")
            
        return safety_issues
        
    async def safe_pump_operation(self, plant_id, duration_seconds):
        """Execute pump operation with comprehensive safety monitoring"""
        # Pre-operation safety check
        safety_issues = self.check_safety_conditions()
        if safety_issues:
            raise SafetyException(f"Safety check failed: {safety_issues}")
            
        try:
            # Start pump with monitoring
            self.pump.start(plant_id)
            operation_start = time.time()
            
            # Safety monitoring loop
            while (time.time() - operation_start) < duration_seconds:
                # Check maximum duration (hard limit)
                if (time.time() - operation_start) >= self.config.max_pump_duration:
                    self.log_safety_event("CRITICAL", "Maximum pump duration exceeded")
                    break
                    
                # Check for emergency stop
                if self.safety_status['emergency_stop']:
                    self.log_safety_event("EMERGENCY", "Emergency stop activated during operation")
                    break
                    
                # Monitor water level (detect leaks or blockages)
                current_level = self.level_sensor.measure_water_level()
                if self.detect_abnormal_flow(current_level):
                    self.log_safety_event("WARNING", "Abnormal flow pattern detected")
                    break
                    
                await asyncio.sleep(0.5)  # Monitor every 500ms
                
        finally:
            # Always stop pump and log operation
            self.pump.stop()
            operation_duration = time.time() - operation_start
            
            self.log_safety_event("INFO", f"Pump operation completed - Duration: {operation_duration:.1f}s")
            
    def emergency_stop(self, reason="Manual activation"):
        """Immediate emergency stop with logging"""
        self.pump.emergency_stop()
        self.safety_status['emergency_stop'] = True
        
        self.log_safety_event("EMERGENCY", f"Emergency stop activated: {reason}")
        
        # Send immediate alerts
        self.send_alert("EMERGENCY", f"Plant watering system emergency stop: {reason}")
        
    def reset_emergency_stop(self, authorized_user=None):
        """Reset emergency stop after manual verification"""
        if not authorized_user:
            raise SecurityException("Emergency stop reset requires authorization")
            
        # Verify system safety before reset
        safety_check = self.check_safety_conditions()
        if any("emergency_stop" not in issue for issue in safety_check):
            raise SafetyException("Cannot reset - other safety issues present")
            
        self.safety_status['emergency_stop'] = False
        self.log_safety_event("INFO", f"Emergency stop reset by {authorized_user}")

class PumpController:
    def __init__(self, relay_pins, config):
        self.plant1_relay = Pin(relay_pins['plant1'], Pin.OUT)
        self.plant2_relay = Pin(relay_pins['plant2'], Pin.OUT)
        self.config = config
        self.pump_status = {
            'plant1': {'active': False, 'start_time': None},
            'plant2': {'active': False, 'start_time': None}
        }
        
        # Initialize relays to fail-safe off position
        self.plant1_relay.off()
        self.plant2_relay.off()
        
    def start(self, plant_id):
        """Start pump for specific plant with safety checks"""
        if plant_id not in ['plant1', 'plant2']:
            raise ValueError(f"Invalid plant_id: {plant_id}")
            
        relay = self.plant1_relay if plant_id == 'plant1' else self.plant2_relay
        
        # Verify relay state before activation
        self.test_relay(relay)
        
        # Activate pump
        relay.on()
        self.pump_status[plant_id] = {
            'active': True,
            'start_time': time.time()
        }
        
        print(f"Pump started for {plant_id}")
        
    def stop(self):
        """Stop all pumps immediately"""
        self.plant1_relay.off()
        self.plant2_relay.off()
        
        # Update status
        for plant_id in self.pump_status:
            if self.pump_status[plant_id]['active']:
                duration = time.time() - self.pump_status[plant_id]['start_time']
                print(f"Pump stopped for {plant_id} - Duration: {duration:.1f}s")
                
            self.pump_status[plant_id] = {'active': False, 'start_time': None}
            
    def emergency_stop(self):
        """Immediate emergency stop with logging"""
        self.stop()
        print("EMERGENCY STOP: All pumps shut down immediately")

# Custom exceptions for safety system
class SafetyException(Exception):
    pass

class SecurityException(Exception):
    pass
```

### Testing Strategy
- **Timeout Test:** Verify 60-second hard limit enforcement
- **Dry-Run Test:** Confirm pump disabled when water level low
- **Emergency Stop Test:** Validate immediate shutdown from all interfaces
- **Flow Detection Test:** Simulate leak conditions and verify detection
- **Relay Test:** Verify fail-safe operation and relay health monitoring

### Definition of Done
✅ Maximum duration timeout functional and tested  
✅ Dry-run protection prevents pump damage  
✅ Emergency stop accessible from all interfaces  
✅ Continuous flow detection operational  
✅ All safety events logged comprehensively  

---

# EPIC 3: TOUCH INTERFACE (Week 3)

## Story E3.1: Status Display System
**Story Points:** 8 | **Priority:** P0 | **Sprint:** Week 3 | **Owner:** Frontend Developer

### User Story
```
As a non-technical user
I want clear visual status of system health and plant conditions
So that I can quickly understand if action is needed
```

### Acceptance Criteria
- [ ] **Moisture Level Display** - Real-time percentage bars
  - Visual progress bars for Plant 1 and Plant 2 moisture levels
  - Color coding: Green (>50%), Yellow (30-50%), Red (<30%)
  - Large, clear percentage numbers
  - Threshold indicators showing target moisture levels
- [ ] **Water Reservoir Display** - Visual gauge representation
  - Tank level as percentage and visual gauge
  - Color-coded status: Green (>70%), Yellow (30-70%), Red (<30%)
  - Estimated days remaining based on usage patterns
  - Clear "REFILL NEEDED" alert when low
- [ ] **Watering History** - Last watering timestamps
  - "Last watered: X hours ago" for each plant
  - Next scheduled watering estimation
  - Today's watering summary (volume and frequency)
- [ ] **System Status** - Operational/error/offline indicators
  - Clear status icons: ✓ Operational, ⚠️ Warning, ❌ Error
  - WiFi connection status indicator
  - Sensor health indicators
  - Pump operational status
- [ ] **Display Quality** - Readable fonts and high contrast
  - Font size appropriate for 2.8" display
  - High contrast color scheme for basement environment
  - Anti-aliasing for smooth text rendering
- [ ] **Auto-refresh** - Updates every 30 seconds
  - Automatic data refresh without user interaction
  - Smooth transitions between data updates
  - Loading indicators during data refresh

### Technical Implementation
```python
# Touch display status system using LVGL
import lvgl as lv

class StatusDisplay:
    def __init__(self, sensor_manager, analytics):
        self.sensor_manager = sensor_manager
        self.analytics = analytics
        self.screen = None
        self.widgets = {}
        
        # Initialize display and LVGL
        self.init_display()
        self.create_status_screen()
        
    def create_status_screen(self):
        """Create main status screen layout"""
        self.screen = lv.scr_act()
        
        # Title
        title = lv.label(self.screen)
        title.set_text("Plant Watering System")
        title.set_style_text_font(lv.font_default(), 0)
        title.align(lv.ALIGN.TOP_MID, 0, 10)
        
        # Plant 1 Status Section
        self.create_plant_status(1, 0, 40)
        
        # Plant 2 Status Section  
        self.create_plant_status(2, 0, 120)
        
        # Water Tank Status
        self.create_tank_status(0, 200)
        
        # System Status
        self.create_system_status(0, 250)
        
        # Start auto-refresh timer
        self.start_refresh_timer()
        
    def create_plant_status(self, plant_num, x, y):
        """Create status display for individual plant"""
        # Plant label
        plant_label = lv.label(self.screen)
        plant_label.set_text(f"Plant {plant_num}")
        plant_label.set_pos(x + 10, y)
        
        # Moisture level bar
        moisture_bar = lv.bar(self.screen)
        moisture_bar.set_size(200, 20)
        moisture_bar.set_pos(x + 10, y + 25)
        moisture_bar.set_range(0, 100)
        
        # Moisture percentage label
        moisture_label = lv.label(self.screen)
        moisture_label.set_pos(x + 220, y + 25)
        
        # Last watered label
        last_watered_label = lv.label(self.screen)
        last_watered_label.set_pos(x + 10, y + 50)
        
        # Store widget references
        self.widgets[f'plant{plant_num}_bar'] = moisture_bar
        self.widgets[f'plant{plant_num}_label'] = moisture_label
        self.widgets[f'plant{plant_num}_last'] = last_watered_label
        
    def create_tank_status(self, x, y):
        """Create water tank status display"""
        # Tank label
        tank_label = lv.label(self.screen)
        tank_label.set_text("Water Tank")
        tank_label.set_pos(x + 10, y)
        
        # Tank level bar
        tank_bar = lv.bar(self.screen)
        tank_bar.set_size(200, 20)
        tank_bar.set_pos(x + 10, y + 25)
        tank_bar.set_range(0, 100)
        
        # Tank percentage label
        tank_label = lv.label(self.screen)
        tank_label.set_pos(x + 220, y + 25)
        
        self.widgets['tank_bar'] = tank_bar
        self.widgets['tank_label'] = tank_label
        
    def create_system_status(self, x, y):
        """Create system health status display"""
        # System status label
        status_label = lv.label(self.screen)
        status_label.set_pos(x + 10, y)
        
        # WiFi status icon
        wifi_icon = lv.label(self.screen)
        wifi_icon.set_pos(x + 200, y)
        
        self.widgets['system_status'] = status_label
        self.widgets['wifi_status'] = wifi_icon
        
    def update_display(self):
        """Update all display elements with current data"""
        try:
            # Get current sensor readings
            readings = self.sensor_manager.get_current_readings()
            
            # Update plant moisture levels
            for plant_id in ['plant1', 'plant2']:
                plant_num = plant_id[-1]
                moisture = readings[plant_id]['moisture_percent']
                
                # Update progress bar
                bar = self.widgets[f'{plant_id}_bar']
                bar.set_value(int(moisture))
                
                # Color coding
                if moisture > 50:
                    bar.set_style_bg_color(lv.color_hex(0x00FF00), lv.PART.INDICATOR)  # Green
                elif moisture > 30:
                    bar.set_style_bg_color(lv.color_hex(0xFFFF00), lv.PART.INDICATOR)  # Yellow
                else:
                    bar.set_style_bg_color(lv.color_hex(0xFF0000), lv.PART.INDICATOR)  # Red
                
                # Update percentage label
                label = self.widgets[f'{plant_id}_label']
                label.set_text(f"{moisture:.0f}%")
                
                # Update last watered
                last_watered = self.analytics.get_last_watered(plant_id)
                hours_ago = self.calculate_hours_since(last_watered)
                last_label = self.widgets[f'{plant_id}_last']
                last_label.set_text(f"Last watered: {hours_ago}h ago")
                
            # Update tank level
            tank_level = readings['tank_level_percent']
            tank_bar = self.widgets['tank_bar']
            tank_bar.set_value(int(tank_level))
            
            tank_label = self.widgets['tank_label']
            tank_label.set_text(f"{tank_level:.0f}%")
            
            # Color coding for tank
            if tank_level > 70:
                tank_bar.set_style_bg_color(lv.color_hex(0x00FF00), lv.PART.INDICATOR)
            elif tank_level > 30:
                tank_bar.set_style_bg_color(lv.color_hex(0xFFFF00), lv.PART.INDICATOR)
            else:
                tank_bar.set_style_bg_color(lv.color_hex(0xFF0000), lv.PART.INDICATOR)
                
            # Update system status
            system_status = self.get_system_status()
            status_label = self.widgets['system_status']
            
            if system_status['healthy']:
                status_label.set_text("✓ System Operational")
                status_label.set_style_text_color(lv.color_hex(0x00FF00), 0)
            else:
                status_label.set_text("⚠️ Check Required")
                status_label.set_style_text_color(lv.color_hex(0xFF0000), 0)
                
            # Update WiFi status
            wifi_label = self.widgets['wifi_status']
            if readings['wifi_connected']:
                wifi_label.set_text("📶 WiFi")
            else:
                wifi_label.set_text("❌ Offline")
                
        except Exception as e:
            print(f"Display update error: {e}")
            
    def start_refresh_timer(self):
        """Start 30-second auto-refresh timer"""
        timer = lv.timer_create(lambda timer: self.update_display(), 30000, None)
        timer.set_repeat_count(lv.TIMER.REPEAT_INFINITE)
```

### Testing Strategy
- **Visual Test:** Verify display elements visible and readable
- **Color Test:** Confirm color coding works in various lighting conditions
- **Refresh Test:** Validate 30-second auto-refresh functionality
- **Data Accuracy Test:** Compare displayed values with actual sensor readings
- **Edge Case Test:** Display behavior with sensor failures or missing data

### Definition of Done
✅ All status elements clearly visible and readable  
✅ Color coding functional for different status levels  
✅ Auto-refresh operating every 30 seconds  
✅ Display responsive and smooth transitions  
✅ Non-technical user can interpret status within 10 seconds  

---

## Story E3.2: Manual Watering Controls
**Story Points:** 8 | **Priority:** P0 | **Sprint:** Week 3 | **Owner:** Frontend Developer

### User Story
```
As any user
I want simple manual watering controls for immediate plant care
So that I can supplement automatic care when needed
```

### Acceptance Criteria
- [ ] **Plant Selection Buttons** - Large, clearly labeled buttons
  - "Water Plant 1" and "Water Plant 2" buttons prominently displayed
  - Button size appropriate for touch interaction (minimum 60px height)
  - Clear visual feedback on button press
  - Disabled state when pump operation not safe
- [ ] **Volume Selection** - 100ml, 200ml, 300ml options
  - Radio button or dropdown selection for volume
  - Default to configured plant volume
  - Visual indicator of selected volume
  - Range validation and error prevention
- [ ] **Progress Indication** - During manual watering operation
  - Progress bar showing watering completion percentage
  - Real-time volume delivered display
  - Estimated time remaining
  - Clear indication when watering complete
- [ ] **Confirmation Dialog** - Prevent accidental activation
  - "Confirm watering Plant X with Yml?" dialog
  - Clear YES/NO buttons
  - Timeout for confirmation (auto-cancel after 10 seconds)
- [ ] **Event Logging** - Same as automatic events
  - Manual watering events recorded with timestamp
  - Volume and plant ID logged
  - User identification (manual vs automatic)
  - Integration with analytics system
- [ ] **Emergency Stop** - Accessible during operation
  - Large red "STOP" button visible during pumping
  - Immediate pump shutdown capability
  - Clear feedback that stop was successful
  - Logging of manual stop events

### Technical Implementation
```python
# Manual watering control interface
class ManualWateringUI:
    def __init__(self, pump_controller, volume_controller, safety_controller):
        self.pump_controller = pump_controller
        self.volume_controller = volume_controller
        self.safety_controller = safety_controller
        self.current_operation = None
        
    def create_manual_control_screen(self):
        """Create manual watering control interface"""
        self.screen = lv.obj()
        
        # Title
        title = lv.label(self.screen)
        title.set_text("Manual Watering")
        title.align(lv.ALIGN.TOP_MID, 0, 10)
        
        # Plant 1 Section
        self.create_plant_controls(1, 0, 50)
        
        # Plant 2 Section
        self.create_plant_controls(2, 0, 150)
        
        # Emergency Stop Button (initially hidden)
        self.create_emergency_stop_button()
        
        return self.screen
        
    def create_plant_controls(self, plant_num, x, y):
        """Create manual controls for individual plant"""
        plant_id = f'plant{plant_num}'
        
        # Plant label
        plant_label = lv.label(self.screen)
        plant_label.set_text(f"Plant {plant_num}")
        plant_label.set_pos(x + 10, y)
        
        # Volume selection
        volume_label = lv.label(self.screen)
        volume_label.set_text("Volume:")
        volume_label.set_pos(x + 10, y + 25)
        
        # Volume dropdown
        volume_dropdown = lv.dropdown(self.screen)
        volume_dropdown.set_options("100ml\n200ml\n300ml")
        volume_dropdown.set_selected(1)  # Default to 200ml
        volume_dropdown.set_pos(x + 80, y + 25)
        volume_dropdown.set_size(100, 30)
        
        # Water button
        water_button = lv.btn(self.screen)
        water_button.set_size(150, 40)
        water_button.set_pos(x + 10, y + 60)
        
        button_label = lv.label(water_button)
        button_label.set_text(f"Water Plant {plant_num}")
        button_label.center()
        
        # Set button callback
        water_button.add_event_cb(
            lambda event: self.on_water_button_click(plant_id, volume_dropdown),
            lv.EVENT.CLICKED,
            None
        )
        
        # Store widget references
        self.widgets[f'{plant_id}_button'] = water_button
        self.widgets[f'{plant_id}_volume'] = volume_dropdown
        
    def on_water_button_click(self, plant_id, volume_dropdown):
        """Handle water button click with confirmation"""
        # Get selected volume
        volume_options = [100, 200, 300]
        selected_volume = volume_options[volume_dropdown.get_selected()]
        
        # Show confirmation dialog
        self.show_confirmation_dialog(plant_id, selected_volume)
        
    def show_confirmation_dialog(self, plant_id, volume_ml):
        """Display confirmation dialog for manual watering"""
        # Create modal dialog
        dialog = lv.obj()
        dialog.set_size(250, 150)
        dialog.center()
        dialog.add_style(self.get_dialog_style(), 0)
        
        # Dialog title
        title = lv.label(dialog)
        title.set_text("Confirm Watering")
        title.align(lv.ALIGN.TOP_MID, 0, 10)
        
        # Confirmation message
        message = lv.label(dialog)
        message.set_text(f"Water {plant_id.upper()}\nwith {volume_ml}ml?")
        message.set_style_text_align(lv.TEXT_ALIGN.CENTER, 0)
        message.align(lv.ALIGN.CENTER, 0, -10)
        
        # YES button
        yes_button = lv.btn(dialog)
        yes_button.set_size(80, 30)
        yes_button.align(lv.ALIGN.BOTTOM_LEFT, 20, -10)
        
        yes_label = lv.label(yes_button)
        yes_label.set_text("YES")
        yes_label.center()
        
        yes_button.add_event_cb(
            lambda event: self.confirm_watering(dialog, plant_id, volume_ml),
            lv.EVENT.CLICKED,
            None
        )
        
        # NO button
        no_button = lv.btn(dialog)
        no_button.set_size(80, 30)
        no_button.align(lv.ALIGN.BOTTOM_RIGHT, -20, -10)
        
        no_label = lv.label(no_button)
        no_label.set_text("NO")
        no_label.center()
        
        no_button.add_event_cb(
            lambda event: dialog.del_(),
            lv.EVENT.CLICKED,
            None
        )
        
        # Auto-timeout after 10 seconds
        timeout_timer = lv.timer_create(
            lambda timer: dialog.del_() if dialog.is_valid() else None,
            10000,
            None
        )
        timeout_timer.set_repeat_count(1)
        
    async def confirm_watering(self, dialog, plant_id, volume_ml):
        """Execute confirmed manual watering"""
        # Close dialog
        dialog.del_()
        
        try:
            # Safety check
            safety_issues = self.safety_controller.check_safety_conditions()
            if safety_issues:
                self.show_error_dialog(f"Cannot water: {safety_issues[0]}")
                return
                
            # Show progress interface
            self.show_watering_progress(plant_id, volume_ml)
            
            # Execute watering
            self.current_operation = await self.volume_controller.water_plant(
                plant_id, volume_ml
            )
            
            # Show completion message
            actual_volume = self.current_operation['actual_volume_ml']
            self.show_success_dialog(
                f"Watering complete!\n{actual_volume:.0f}ml delivered"
            )
            
        except Exception as e:
            self.show_error_dialog(f"Watering failed: {str(e)}")
            
        finally:
            self.hide_watering_progress()
            self.current_operation = None
            
    def show_watering_progress(self, plant_id, target_volume):
        """Display watering progress interface"""
        # Create progress screen overlay
        progress_screen = lv.obj()
        progress_screen.set_size(lv.pct(100), lv.pct(100))
        
        # Progress bar
        progress_bar = lv.bar(progress_screen)
        progress_bar.set_size(200, 20)
        progress_bar.center()
        progress_bar.set_range(0, 100)
        
        # Status label
        status_label = lv.label(progress_screen)
        status_label.set_text(f"Watering {plant_id.upper()}...")
        status_label.align(lv.ALIGN.CENTER, 0, -30)
        
        # Volume label
        volume_label = lv.label(progress_screen)
        volume_label.align(lv.ALIGN.CENTER, 0, 30)
        
        # Emergency stop button
        stop_button = lv.btn(progress_screen)
        stop_button.set_size(100, 40)
        stop_button.align(lv.ALIGN.BOTTOM_MID, 0, -20)
        stop_button.set_style_bg_color(lv.color_hex(0xFF0000), 0)
        
        stop_label = lv.label(stop_button)
        stop_label.set_text("STOP")
        stop_label.center()
        
        stop_button.add_event_cb(
            lambda event: self.emergency_stop_manual(),
            lv.EVENT.CLICKED,
            None
        )
        
        # Store progress widgets
        self.progress_widgets = {
            'screen': progress_screen,
            'bar': progress_bar,
            'volume_label': volume_label
        }
        
        # Start progress update timer
        self.progress_timer = lv.timer_create(
            self.update_progress, 500, None
        )
        
    def update_progress(self, timer):
        """Update watering progress display"""
        if not self.current_operation:
            return
            
        try:
            # Calculate progress based on current operation
            if hasattr(self.current_operation, 'get_progress'):
                progress = self.current_operation.get_progress()
                
                # Update progress bar
                self.progress_widgets['bar'].set_value(int(progress['percent']))
                
                # Update volume label
                self.progress_widgets['volume_label'].set_text(
                    f"{progress['delivered']:.0f}ml / {progress['target']:.0f}ml"
                )
                
        except Exception as e:
            print(f"Progress update error: {e}")
```

### Testing Strategy
- **Button Test:** Verify touch responsiveness and visual feedback
- **Volume Selection Test:** Confirm all volume options selectable
- **Confirmation Test:** Validate dialog flow and timeout functionality
- **Progress Test:** Verify real-time progress updates during watering
- **Emergency Stop Test:** Confirm immediate stop capability
- **Logging Test:** Verify manual events logged correctly

### Definition of Done
✅ Manual watering buttons responsive and clearly labeled  
✅ Volume selection functional with visual confirmation  
✅ Confirmation dialog prevents accidental activation  
✅ Progress indication accurate during watering operations  
✅ Emergency stop immediately accessible and functional  
✅ All manual watering events properly logged  

---

## Story E3.3: Basic Settings Configuration
**Story Points:** 13 | **Priority:** P1 | **Sprint:** Week 3 | **Owner:** Frontend Developer

### User Story
```
As a technical user
I want configurable settings accessible via touch interface
So that I can optimize system behavior per plant
```

### Acceptance Criteria
- [ ] **Moisture Threshold Configuration** - Individual plant sliders/numeric input
  - Separate threshold settings for Plant 1 and Plant 2
  - Slider interface with real-time value display
  - Range validation (10% minimum, 80% maximum)
  - Visual indication of current vs. target moisture levels
- [ ] **Volume Configuration** - Default watering amounts
  - Numeric input for default volume per plant
  - Range validation (100ml-500ml)
  - Preview calculation of watering frequency
  - Separate settings for manual vs automatic watering
- [ ] **Time Window Settings** - Watering schedule configuration
  - Start time setting (hour selection)
  - End time setting (hour selection)
  - Visual timeline showing active watering window
  - Validation to prevent invalid time ranges
- [ ] **System Preferences** - Language/units selection
  - Metric/Imperial unit selection
  - Temperature display units (Celsius/Fahrenheit)
  - Time format (12h/24h)
  - Display brightness adjustment
- [ ] **Settings Validation** - Error handling and range checking
  - Real-time validation with error messages
  - Prevention of invalid configurations
  - Confirmation before saving changes
  - Rollback capability if settings cause issues
- [ ] **Persistence** - Settings maintained across restarts
  - Automatic save to JSON configuration file
  - Backup configuration system
  - Factory reset option
  - Export/import settings capability

### Technical Implementation
```python
# Settings configuration interface
class SettingsUI:
    def __init__(self, config_manager):
        self.config = config_manager
        self.current_settings = self.config.load_settings()
        self.widgets = {}
        self.validation_errors = {}
        
    def create_settings_screen(self):
        """Create tabbed settings interface"""
        self.screen = lv.obj()
        
        # Create tab view
        tabview = lv.tabview(self.screen, lv.DIR.TOP, 30)
        
        # Plant Settings Tab
        plant_tab = tabview.add_tab("Plants")
        self.create_plant_settings(plant_tab)
        
        # System Settings Tab
        system_tab = tabview.add_tab("System")
        self.create_system_settings(system_tab)
        
        # Advanced Settings Tab
        advanced_tab = tabview.add_tab("Advanced")
        self.create_advanced_settings(advanced_tab)
        
        # Save/Cancel buttons
        self.create_action_buttons()
        
        return self.screen
        
    def create_plant_settings(self, parent):
        """Create plant-specific settings"""
        y_pos = 10
        
        for plant_num in [1, 2]:
            plant_id = f'plant{plant_num}'
            
            # Plant section label
            plant_label = lv.label(parent)
            plant_label.set_text(f"Plant {plant_num} Settings")
            plant_label.set_pos(10, y_pos)
            
            # Moisture threshold slider
            threshold_label = lv.label(parent)
            threshold_label.set_text("Water when moisture below:")
            threshold_label.set_pos(10, y_pos + 25)
            
            threshold_slider = lv.slider(parent)
            threshold_slider.set_size(200, 20)
            threshold_slider.set_pos(10, y_pos + 45)
            threshold_slider.set_range(10, 80)  # 10%-80% range
            
            current_threshold = self.current_settings['thresholds'][plant_id]
            threshold_slider.set_value(current_threshold)
            
            # Threshold value label
            threshold_value = lv.label(parent)
            threshold_value.set_pos(220, y_pos + 45)
            threshold_value.set_text(f"{current_threshold}%")
            
            # Update callback
            threshold_slider.add_event_cb(
                lambda event, plant=plant_id, label=threshold_value: 
                self.on_threshold_change(event, plant, label),
                lv.EVENT.VALUE_CHANGED,
                None
            )
            
            # Default volume setting
            volume_label = lv.label(parent)
            volume_label.set_text("Default watering volume:")
            volume_label.set_pos(10, y_pos + 75)
            
            volume_spinbox = lv.spinbox(parent)
            volume_spinbox.set_pos(10, y_pos + 95)
            volume_spinbox.set_size(120, 30)
            volume_spinbox.set_range(100, 500)
            volume_spinbox.set_step(50)
            
            current_volume = self.current_settings['volumes'][plant_id]
            volume_spinbox.set_value(current_volume)
            
            # Volume unit label
            volume_unit = lv.label(parent)
            volume_unit.set_text("ml")
            volume_unit.set_pos(140, y_pos + 100)
            
            # Store widget references
            self.widgets[f'{plant_id}_threshold'] = threshold_slider
            self.widgets[f'{plant_id}_threshold_label'] = threshold_value
            self.widgets[f'{plant_id}_volume'] = volume_spinbox
            
            y_pos += 140
            
    def create_system_settings(self, parent):
        """Create system-wide settings"""
        y_pos = 10
        
        # Time window settings
        time_label = lv.label(parent)
        time_label.set_text("Active Watering Hours")
        time_label.set_pos(10, y_pos)
        
        # Start time
        start_label = lv.label(parent)
        start_label.set_text("Start time:")
        start_label.set_pos(10, y_pos + 25)
        
        start_spinbox = lv.spinbox(parent)
        start_spinbox.set_pos(100, y_pos + 25)
        start_spinbox.set_size(80, 30)
        start_spinbox.set_range(0, 23)
        start_spinbox.set_value(self.current_settings['time_window']['start'])
        
        # End time
        end_label = lv.label(parent)
        end_label.set_text("End time:")
        end_label.set_pos(10, y_pos + 65)
        
        end_spinbox = lv.spinbox(parent)
        end_spinbox.set_pos(100, y_pos + 65)
        end_spinbox.set_size(80, 30)
        end_spinbox.set_range(0, 23)
        end_spinbox.set_value(self.current_settings['time_window']['end'])
        
        # Display brightness
        brightness_label = lv.label(parent)
        brightness_label.set_text("Display brightness:")
        brightness_label.set_pos(10, y_pos + 105)
        
        brightness_slider = lv.slider(parent)
        brightness_slider.set_size(150, 20)
        brightness_slider.set_pos(10, y_pos + 125)
        brightness_slider.set_range(20, 100)
        brightness_slider.set_value(self.current_settings['display']['brightness'])
        
        # Store references
        self.widgets['start_time'] = start_spinbox
        self.widgets['end_time'] = end_spinbox
        self.widgets['brightness'] = brightness_slider
        
    def create_advanced_settings(self, parent):
        """Create advanced/debugging settings"""
        y_pos = 10
        
        # Sensor calibration section
        calibration_label = lv.label(parent)
        calibration_label.set_text("Sensor Calibration")
        calibration_label.set_pos(10, y_pos)
        
        # Calibrate moisture sensors button
        calibrate_button = lv.btn(parent)
        calibrate_button.set_size(180, 35)
        calibrate_button.set_pos(10, y_pos + 25)
        
        calibrate_label = lv.label(calibrate_button)
        calibrate_label.set_text("Calibrate Moisture Sensors")
        calibrate_label.center()
        
        calibrate_button.add_event_cb(
            lambda event: self.start_sensor_calibration(),
            lv.EVENT.CLICKED,
            None
        )
        
        # Factory reset section
        y_pos += 80
        reset_label = lv.label(parent)
        reset_label.set_text("Factory Reset")
        reset_label.set_pos(10, y_pos)
        
        reset_button = lv.btn(parent)
        reset_button.set_size(150, 35)
        reset_button.set_pos(10, y_pos + 25)
        reset_button.set_style_bg_color(lv.color_hex(0xFF4444), 0)
        
        reset_button_label = lv.label(reset_button)
        reset_button_label.set_text("Reset to Defaults")
        reset_button_label.center()
        
        reset_button.add_event_cb(
            lambda event: self.show_factory_reset_dialog(),
            lv.EVENT.CLICKED,
            None
        )
        
    def on_threshold_change(self, event, plant_id, label):
        """Handle moisture threshold slider changes"""
        slider = event.get_target()
        new_value = slider.get_value()
        
        # Update label
        label.set_text(f"{new_value}%")
        
        # Validate setting
        if self.validate_threshold(plant_id, new_value):
            # Store temporary setting
            self.current_settings['thresholds'][plant_id] = new_value
            slider.set_style_bg_color(lv.color_hex(0x00FF00), lv.PART.KNOB)
        else:
            # Invalid setting - show error
            slider.set_style_bg_color(lv.color_hex(0xFF0000), lv.PART.KNOB)
            self.validation_errors[f'{plant_id}_threshold'] = "Invalid threshold value"
            
    def validate_threshold(self, plant_id, threshold):
        """Validate moisture threshold setting"""
        # Range check
        if threshold < 10 or threshold > 80:
            return False
            
        # Logic check - threshold should be reasonable
        current_moisture = self.get_current_moisture(plant_id)
        if current_moisture and abs(current_moisture - threshold) < 5:
            # Too close to current reading - might cause oscillation
            return False
            
        return True
        
    def save_settings(self):
        """Save current settings with validation"""
        # Final validation
        if self.validation_errors:
            self.show_validation_errors()
            return False
            
        try:
            # Create backup of current settings
            self.config.backup_settings()
            
            # Save new settings
            self.config.save_settings(self.current_settings)
            
            # Apply settings immediately
            self.apply_settings()
            
            self.show_success_message("Settings saved successfully")
            return True
            
        except Exception as e:
            self.show_error_message(f"Failed to save settings: {e}")
            return False
            
    def show_factory_reset_dialog(self):
        """Show confirmation dialog for factory reset"""
        # Create warning dialog
        dialog = lv.obj()
        dialog.set_size(280, 180)
        dialog.center()
        
        # Warning message
        warning = lv.label(dialog)
        warning.set_text("⚠️ FACTORY RESET\n\nThis will restore all settings\nto default values.\n\nThis cannot be undone!")
        warning.set_style_text_align(lv.TEXT_ALIGN.CENTER, 0)
        warning.align(lv.ALIGN.CENTER, 0, -20)
        
        # Reset button
        reset_btn = lv.btn(dialog)
        reset_btn.set_size(100, 30)
        reset_btn.align(lv.ALIGN.BOTTOM_LEFT, 20, -10)
        reset_btn.set_style_bg_color(lv.color_hex(0xFF0000), 0)
        
        reset_label = lv.label(reset_btn)
        reset_label.set_text("RESET")
        reset_label.center()
        
        # Cancel button
        cancel_btn = lv.btn(dialog)
        cancel_btn.set_size(100, 30)
        cancel_btn.align(lv.ALIGN.BOTTOM_RIGHT, -20, -10)
        
        cancel_label = lv.label(cancel_btn)
        cancel_label.set_text("CANCEL")
        cancel_label.center()
        
        # Set callbacks
        reset_btn.add_event_cb(
            lambda event: self.perform_factory_reset(dialog),
            lv.EVENT.CLICKED,
            None
        )
        
        cancel_btn.add_event_cb(
            lambda event: dialog.del_(),
            lv.EVENT.CLICKED,
            None
        )
```

### Testing Strategy
- **Settings Validation Test:** Verify range checking and error handling
- **Persistence Test:** Confirm settings survive system restart
- **UI Responsiveness Test:** Validate slider and input responsiveness
- **Factory Reset Test:** Verify complete restoration to defaults
- **Calibration Test:** Validate sensor calibration workflow

### Definition of Done
✅ All plant settings configurable via touch interface  
✅ Settings validation prevents invalid configurations  
✅ Configuration persists across system restarts  
✅ Factory reset functionality complete and tested  
✅ Settings interface intuitive for technical users  

---

## Story E3.4: Alert & Notification Display
**Story Points:** 8 | **Priority:** P0 | **Sprint:** Week 3 | **Owner:** Frontend Developer

### User Story
```
As any user
I want clear alerts for system issues and required actions
So that I can respond appropriately to system needs
```

### Acceptance Criteria
- [ ] **Low Water Level Alerts** - Clear refill instructions
  - Prominent visual alert when water level <30%
  - "REFILL NEEDED" message with tank capacity info
  - Estimated time until empty based on usage patterns
  - Clear instructions on refill procedure
- [ ] **Sensor Malfunction Alerts** - Troubleshooting guidance
  - Specific sensor identification (Plant 1/2 moisture, water level)
  - Basic troubleshooting steps displayed
  - Visual indicator of which sensor failed
  - Contact information for technical support
- [ ] **Pump Failure Notifications** - Emergency procedures
  - Immediate notification of pump malfunction
  - Safety status (plants at risk timeline)
  - Emergency manual watering instructions
  - System shutdown/restart procedures
- [ ] **Alert Management** - Dismiss/snooze functionality
  - Individual alert acknowledgment
  - Snooze options (1 hour, 4 hours, 24 hours)
  - Alert history tracking
  - Priority-based alert ordering
- [ ] **Visual Design** - Color coding and clear iconography
  - Red for critical alerts (pump failure, system error)
  - Yellow for warnings (low water, sensor drift)
  - Blue for information (maintenance reminder, updates)
  - Clear, universally understood icons
- [ ] **Alert Persistence** - History and status tracking
  - Alert log with timestamps
  - Resolution tracking (acknowledged vs auto-resolved)
  - Recurring alert detection and handling
  - Export capability for troubleshooting

### Technical Implementation
```python
# Alert and notification system
class AlertSystem:
    def __init__(self, display_manager):
        self.display = display_manager
        self.active_alerts = {}
        self.alert_history = []
        self.alert_widgets = {}
        
        # Alert severity levels
        self.SEVERITY_LEVELS = {
            'CRITICAL': {'color': 0xFF0000, 'icon': '❌', 'priority': 1},
            'WARNING': {'color': 0xFFFF00, 'icon': '⚠️', 'priority': 2},
            'INFO': {'color': 0x0088FF, 'icon': 'ℹ️', 'priority': 3}
        }
        
    def create_alert_overlay(self):
        """Create alert notification overlay"""
        # Alert container (initially hidden)
        self.alert_container = lv.obj(lv.scr_act())
        self.alert_container.set_size(280, 200)
        self.alert_container.set_pos(20, 20)
        self.alert_container.add_flag(lv.obj.FLAG.HIDDEN)
        
        # Alert background with severity color
        self.alert_background = lv.obj(self.alert_container)
        self.alert_background.set_size(lv.pct(100), lv.pct(100))
        
        # Alert icon
        self.alert_icon = lv.label(self.alert_container)
        self.alert_icon.set_pos(10, 10)
        
        # Alert title
        self.alert_title = lv.label(self.alert_container)
        self.alert_title.set_pos(50, 10)
        self.alert_title.set_size(200, 30)
        
        # Alert message
        self.alert_message = lv.label(self.alert_container)
        self.alert_message.set_pos(10, 40)
        self.alert_message.set_size(260, 100)
        self.alert_message.set_long_mode(lv.label.LONG.WRAP)
        
        # Action buttons container
        self.create_alert_buttons()
        
    def create_alert_buttons(self):
        """Create alert action buttons"""
        # Acknowledge button
        self.ack_button = lv.btn(self.alert_container)
        self.ack_button.set_size(80, 30)
        self.ack_button.set_pos(10, 160)
        
        ack_label = lv.label(self.ack_button)
        ack_label.set_text("OK")
        ack_label.center()
        
        # Snooze button
        self.snooze_button = lv.btn(self.alert_container)
        self.snooze_button.set_size(80, 30)
        self.snooze_button.set_pos(100, 160)
        
        snooze_label = lv.label(self.snooze_button)
        snooze_label.set_text("Snooze")
        snooze_label.center()
        
        # Details button
        self.details_button = lv.btn(self.alert_container)
        self.details_button.set_size(80, 30)
        self.details_button.set_pos(190, 160)
        
        details_label = lv.label(self.details_button)
        details_label.set_text("Details")
        details_label.center()
        
        # Set button callbacks
        self.ack_button.add_event_cb(
            lambda event: self.acknowledge_current_alert(),
            lv.EVENT.CLICKED, None
        )
        
        self.snooze_button.add_event_cb(
            lambda event: self.show_snooze_options(),
            lv.EVENT.CLICKED, None
        )
        
        self.details_button.add_event_cb(
            lambda event: self.show_alert_details(),
            lv.EVENT.CLICKED, None
        )
        
    def show_alert(self, alert_id, severity, title, message, actions=None):
        """Display alert with specified severity and content"""
        alert_config = self.SEVERITY_LEVELS[severity]
        
        # Store alert info
        alert_info = {
            'id': alert_id,
            'severity': severity,
            'title': title,
            'message': message,
            'timestamp': time.time(),
            'actions': actions or [],
            'status': 'active'
        }
        
        self.active_alerts[alert_id] = alert_info
        self.alert_history.append(alert_info.copy())
        
        # Update alert display
        self.alert_background.set_style_bg_color(
            lv.color_hex(alert_config['color']), 0
        )
        
        self.alert_icon.set_text(alert_config['icon'])
        self.alert_title.set_text(title)
        self.alert_message.set_text(message)
        
        # Show alert overlay
        self.alert_container.clear_flag(lv.obj.FLAG.HIDDEN)
        
        # Auto-hide info alerts after 10 seconds
        if severity == 'INFO':
            timer = lv.timer_create(
                lambda timer: self.auto_acknowledge_alert(alert_id),
                10000, None
            )
            timer.set_repeat_count(1)
            
    def show_low_water_alert(self, current_level_percent, estimated_days_remaining):
        """Show low water level alert with specific information"""
        if current_level_percent < 10:
            severity = 'CRITICAL'
            title = "WATER TANK EMPTY"
            message = f"Tank level: {current_level_percent:.0f}%\n\nREFILL IMMEDIATELY\n\nPlants at risk!"
        else:
            severity = 'WARNING'
            title = "Low Water Level"
            message = f"Tank level: {current_level_percent:.0f}%\n\nEstimated time remaining:\n{estimated_days_remaining:.1f} days\n\nPlease refill when convenient"
            
        self.show_alert('low_water', severity, title, message)
        
    def show_sensor_malfunction_alert(self, sensor_type, sensor_id, troubleshooting_steps):
        """Show sensor malfunction alert with troubleshooting"""
        title = f"{sensor_type} Sensor Error"
        message = f"Sensor {sensor_id} not responding\n\nTroubleshooting:\n"
        
        for step in troubleshooting_steps[:3]:  # Limit to 3 steps
            message += f"• {step}\n"
            
        message += "\nContact support if issue persists"
        
        self.show_alert(f'sensor_{sensor_id}', 'WARNING', title, message)
        
    def show_pump_failure_alert(self, failure_type, immediate_actions):
        """Show critical pump failure alert"""
        title = "PUMP FAILURE"
        message = f"Pump malfunction detected:\n{failure_type}\n\nImmediate actions:\n"
        
        for action in immediate_actions:
            message += f"• {action}\n"
            
        self.show_alert('pump_failure', 'CRITICAL', title, message)
        
    def acknowledge_current_alert(self):
        """Acknowledge and dismiss current alert"""
        if not self.active_alerts:
            return
            
        # Get current alert (highest priority)
        current_alert_id = self.get_highest_priority_alert()
        alert_info = self.active_alerts[current_alert_id]
        
        # Mark as acknowledged
        alert_info['status'] = 'acknowledged'
        alert_info['acknowledged_time'] = time.time()
        
        # Remove from active alerts
        del self.active_alerts[current_alert_id]
        
        # Hide alert display
        self.hide_current_alert()
        
        # Show next alert if any
        self.show_next_alert()
        
        # Log acknowledgment
        self.log_alert_action(current_alert_id, 'acknowledged')
        
    def show_snooze_options(self):
        """Show snooze duration selection dialog"""
        snooze_dialog = lv.obj()
        snooze_dialog.set_size(200, 180)
        snooze_dialog.center()
        
        # Title
        title = lv.label(snooze_dialog)
        title.set_text("Snooze Alert")
        title.align(lv.ALIGN.TOP_MID, 0, 10)
        
        # Snooze options
        snooze_options = [
            ('1 Hour', 3600),
            ('4 Hours', 14400),
            ('24 Hours', 86400)
        ]
        
        y_pos = 40
        for option_text, duration_seconds in snooze_options:
            option_button = lv.btn(snooze_dialog)
            option_button.set_size(160, 30)
            option_button.set_pos(20, y_pos)
            
            option_label = lv.label(option_button)
            option_label.set_text(option_text)
            option_label.center()
            
            option_button.add_event_cb(
                lambda event, duration=duration_seconds, dialog=snooze_dialog: 
                self.snooze_current_alert(duration, dialog),
                lv.EVENT.CLICKED, None
            )
            
            y_pos += 40
            
        # Cancel button
        cancel_button = lv.btn(snooze_dialog)
        cancel_button.set_size(160, 30)
        cancel_button.set_pos(20, y_pos)
        
        cancel_label = lv.label(cancel_button)
        cancel_label.set_text("Cancel")
        cancel_label.center()
        
        cancel_button.add_event_cb(
            lambda event: snooze_dialog.del_(),
            lv.EVENT.CLICKED, None
        )
        
    def snooze_current_alert(self, duration_seconds, dialog):
        """Snooze current alert for specified duration"""
        # Close snooze dialog
        dialog.del_()
        
        current_alert_id = self.get_highest_priority_alert()
        alert_info = self.active_alerts[current_alert_id]
        
        # Set snooze time
        alert_info['snoozed_until'] = time.time() + duration_seconds
        alert_info['status'] = 'snoozed'
        
        # Hide current alert
        self.hide_current_alert()
        
        # Schedule alert to reappear
        timer = lv.timer_create(
            lambda timer: self.unsnooze_alert(current_alert_id),
            duration_seconds * 1000,  # Convert to milliseconds
            None
        )
        timer.set_repeat_count(1)
        
        # Log snooze action
        self.log_alert_action(current_alert_id, f'snoozed_{duration_seconds}s')
        
        # Show next alert if any
        self.show_next_alert()
```

### Testing Strategy
- **Alert Display Test:** Verify all alert types display correctly
- **Priority Test:** Confirm critical alerts shown before warnings
- **Action Test:** Validate acknowledge, snooze, and details functions
- **Persistence Test:** Verify alert history maintained correctly
- **Visual Test:** Confirm color coding and icons display properly

### Definition of Done
✅ All alert types display with appropriate severity indicators  
✅ Alert management (acknowledge/snooze) functional  
✅ Low water alerts include clear refill instructions  
✅ Sensor alerts provide troubleshooting guidance  
✅ Alert history maintained and accessible  

<function_calls>
<invoke name="TodoWrite">
<parameter name="todos">[{"id": "1", "content": "Identify which epic/story to develop in detail", "status": "completed"}, {"id": "2", "content": "Create detailed user story with acceptance criteria", "status": "completed"}, {"id": "3", "content": "Add technical implementation details", "status": "completed"}, {"id": "4", "content": "Define testing and validation approach", "status": "completed"}]