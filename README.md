# 24-Hour Digital Clock Using TTL ICs

## Overview
This project is a digital clock that displays time in 24-hour format using TTL logic components.

Display format:

HH:MM

Examples:
- 00:00
- 12:30
- 23:59

---

## Components

- 4x SN74LS90N
- 4x SN74LS47N
- 4x 7-segment displays
- 1x NE555 timer
- 1x SN74LS04
- 1x SN74LS08
- Resistors
- Capacitors
- Breadboard
- Jumper wires

---

## Features

- 24-hour format
- Automatic minute reset
- Automatic hour reset
- Fully hardware-based clock

---

## Clock Flow

555 Timer
→ Minutes
→ Hours

---

## Reset Conditions

59 → 00

23 → 00

---

## Challenges

- Accurate timing
- Large wiring setup
- Logic debugging

---

## Future Improvements

- Add RTC
- Add alarm
- Improve timing precision
