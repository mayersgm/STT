# STT
# SiGe Transistor Tester - Integrated Test System Guide

## System Overview
The SiGe Transistor Tester is a precision instrument designed for characterizing SiGe transistors through synchronized voltage control and measurement. The system features dual subsystems working in tandem: voltage generation through Digital-to-Analog Converters (DAC7578) and voltage measurement using Analog-to-Digital Converters (AD799x). This integrated approach enables precise voltage control with real-time measurement verification across eight differential pairs.

## Hardware Architecture

### Dual Reference System
The tester employs independent reference voltages for DACs and ADCs:

1. DAC Reference (0.5V - 5.0V):
   - Controls the output voltage range for all DAC channels
   - Must match the physical DAC potentiometer setting
   - Affects maximum test voltage capability

2. ADC Reference (0.5V - 5.0V):
   - Determines the measurement range for all ADC channels
   - Must match the physical ADC potentiometer setting
   - Influences measurement resolution and accuracy

### Channel Organization
The system utilizes paired DAC and ADC channels organized into eight differential pairs:

First DAC/ADC Set (Pairs 0-3):
- DAC A: Address 0x48
- ADC A: Address 0x20

Second DAC/ADC Set (Pairs 4-7):
- DAC B: Address 0x49
- ADC B: Address 0x21

### Precise Channel Mapping
Each differential pair uses specific DAC outputs and ADC inputs:

```
Differential Pair 0:
  DAC A: CH0(+)/CH2(-) → ADC A: CH1(+)/CH3(-)
Differential Pair 1:
  DAC A: CH4(+)/CH6(-) → ADC A: CH5(+)/CH7(-)
Differential Pair 2:
  DAC A: CH5(+)/CH7(-) → ADC A: CH6(+)/CH8(-)
Differential Pair 3:
  DAC A: CH1(+)/CH3(-) → ADC A: CH2(+)/CH4(-)
Differential Pair 4:
  DAC B: CH0(+)/CH2(-) → ADC B: CH1(+)/CH3(-)
Differential Pair 5:
  DAC B: CH4(+)/CH6(-) → ADC B: CH5(+)/CH7(-)
Differential Pair 6:
  DAC B: CH5(+)/CH7(-) → ADC B: CH6(+)/CH8(-)
Differential Pair 7:
  DAC B: CH1(+)/CH3(-) → ADC B: CH2(+)/CH4(-)
```

## Operation Guide

### Initial Setup
1. Verify and Set Reference Voltages:
   - Adjust DAC potentiometer to desired test range
   - Set matching DAC VREF in GUI
   - Adjust ADC potentiometer for measurement range
   - Set matching ADC VREF in GUI

2. Configuration Management:
   - Load existing configuration or use defaults
   - Verify channel assignments match hardware setup
   - Test connection to all DACs and ADCs

### Basic Testing
1. Setting Test Voltages:
   - Enter desired voltages for each differential pair
   - Values automatically validate against DAC VREF
   - Yellow highlighting indicates adjusted values

2. Measurement Updates:
   - Click UPDATE to apply voltages and read measurements
   - System provides 1ms settling time before readings
   - VIN columns show actual measured voltages
   - Read-only fields prevent accidental modification

### Automated Testing
The SWEEP function provides comprehensive characterization:

1. Configure Sweep Parameters (ALL row):
   - Set starting voltages (VOUT columns)
   - Define voltage increment (SWEEP INC)
   - Set maximum voltage (MAX)

2. During Sweep:
   - System incrementally adjusts all DAC outputs
   - Records ADC measurements at each step
   - Updates display in real-time
   - Generates voltage response curves
   - Saves complete dataset automatically

### Data Management

1. Save Options:
   - Configuration files (.json):
     - Preserve complete test settings
     - Include reference voltages
     - Store channel mappings
   
   - Measurement data (.csv):
     - Record all DAC settings
     - Include corresponding ADC readings
     - Time-stamped for tracking

2. Data Analysis:
   - Automatic plot generation for sweeps
   - CSV format compatible with analysis tools
   - Complete test condition documentation

## Best Practices

### Voltage Management
- Start with lower voltages and gradually increase
- Monitor both positive and negative channels
- Verify measurements match expected values
- Allow settling time between major changes

### System Protection
- Verify all connections before applying voltage
- Use appropriate current limiting
- Monitor for unexpected readings
- Keep voltages within safe operating range

### Configuration Control
- Document reference voltage settings
- Save configurations for repeatability
- Verify hardware matches software settings
- Maintain calibration records

## Troubleshooting

### Common Issues
1. DAC/ADC Initialization Failures:
   - Check I2C connections
   - Verify power supply
   - Confirm address settings

2. Measurement Discrepancies:
   - Verify reference voltage settings
   - Check channel connections
   - Allow adequate settling time
   - Consider noise sources

### Error Messages
The system provides specific warnings for:
- Hardware initialization failures
- Reference voltage mismatches
- Out-of-range values
- Communication errors

## Support and Documentation
For additional assistance:
- Review error messages and logs
- Check connection diagnostics
- Consult hardware documentation
- Contact system support

## Maintenance
Regular system checks:
- Verify reference voltage accuracy
- Check channel calibration
- Update configuration backups
- Clean connections and contacts
