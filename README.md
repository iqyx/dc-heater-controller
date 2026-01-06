# 48 V heater controller

This aims to be a home-assistant compatible heater controller for off-grid water heating using
surplus electricity from a PV array. It is intended to be used in a 48 V DC system. Some main features:

- turn on the heating element whenever a surplus energy is detected
- cycle multiple heating elements to wear them evenly
- optimized for "3-phase" 48 V heating elements
- multiple redundant protections
- STM32 MCU with a ST's WiFi module for connectivity (no, no ESP32)
- water pump control

Implemented protections:

- high side MOSFET disconnect on UVLO (prevent draining the battery), can be set using a trimpot on the power board
- high side MOSFET disconnect on OV (well, not really important)
- high side MOSFET hardware overtemperature protection (turns them off)
- high side MOSFET software temperature monitoring
- high side current and voltage sense
- high side and low side MOSFETs software control depending on the battery voltage
- 95° water overtemperature hardware protection (a bimetal thermostat turns off high side MOSFETs)
- 90° water overtemperature hardware protection (a NTC with a comparator turns off low side MOSFETs independently of the software control)
- water temperature setpoint control (software controls low side MOSFETs)
- water pump malfunction turns off low side MOSFETs (software)
