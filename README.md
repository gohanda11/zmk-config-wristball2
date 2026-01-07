# ZMK Config for wristBall2

Standalone macro pad with integrated trackball, based on Seeeduino XIAO BLE.

## Features
- 6 keys macro pad
- PMW3610 trackball sensor
- Battery voltage monitoring (Ni-MH AAA battery support)
- ZMK Studio support
- ZMK firmware support
- Bluetooth connectivity

## Battery Voltage Monitoring

This configuration supports Ni-MH AAA battery voltage monitoring using a voltage divider circuit.

### Hardware Requirements

**Voltage Divider Circuit:**
- R2 = 1MΩ (connected to battery positive)
- R3 = 470kΩ (connected to ground)
- Divider ratio = 470k / (1000k + 470k) = 0.32
- ADC input connected to the junction between R2 and R3

### Voltage Ranges

**Actual Battery Voltage:**
- MIN: 1100mV (0% charge)
- MAX: 1400mV (100% charge)
- LOW: 1050mV (shutdown threshold)

**ADC Input Voltage (after divider):**
- MIN: 352mV (1100mV × 0.32)
- MAX: 448mV (1400mV × 0.32)
- LOW: 336mV (1050mV × 0.32)

These values are configured in `wristball2.conf` using the `zmk-feature-non-lipo-battery-management` module.

## Dependencies

This configuration requires the following external modules (defined in `config/west.yml`):

- **[zmk-feature-non-lipo-battery-management](https://github.com/sekigon-gonnoc/zmk-feature-non-lipo-battery-management)** - Non-LiPo battery voltage monitoring
- **[zmk-pmw3610-driver-wristball2](https://github.com/gohanda11/zmk-pmw3610-driver-wristball2)** - PMW3610 trackball sensor driver
- **[zmk-rgbled-widget](https://github.com/gohanda11/zmk-rgbled-widget)** - RGB LED status indicator

## Building
This configuration uses GitHub Actions to build the firmware automatically.