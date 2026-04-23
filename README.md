# Digital Clock Using SN74LS90N and SN74LS47N

## Project Overview
This project is a **12-hour digital clock (HH:MM:SS with AM/PM indicator)** built using TTL logic ICs, a 555 timer, and 7-segment displays.

The clock counts:

- Seconds: `00–59`
- Minutes: `00–59`
- Hours: `01–12`
- AM/PM toggles every 12-hour cycle

The system uses cascading decade counters and BCD-to-7-segment decoders to display time.

---

## Components Used

| Component | Quantity | Purpose |
|------------|------------|----------|
| SN74LS90N Decade Counter | 7 | Time counting (seconds, minutes, hours, AM/PM) |
| SN74LS47N BCD to 7-Segment Decoder | 6 | Drives displays |
| NE555 Timer | 1 | Generates 1Hz clock pulse |
| SN74LS04 Hex Inverter | 1 | Reset logic |
| SN74LS08 Quad AND Gate | 1 | Reset logic |
| 5161AS 7-Segment Display | 7 | Displays time + AM/PM |
| 330Ω Resistors | 49 | Current limiting |
| 4.7kΩ Resistors | 2 | 555 timer timing |
| 100µF Capacitor | 1 | 555 timer timing |
| 0.01µF Capacitor | 1 | 555 timer stability |
| Breadboard | 1 | Circuit assembly |
| Jumper Wires | Multiple | Connections |

---

# System Flow

```plaintext
555 Timer
   ↓
Seconds Ones
   ↓
Seconds Tens
   ↓
Minutes Ones
   ↓
Minutes Tens
   ↓
Hours Ones
   ↓
Hours Tens
   ↓
AM/PM Toggle
```

---

## Circuit Operation

### 1. 555 Timer Clock Generator
The NE555 timer is configured in astable mode to generate approximately **1 pulse per second (1Hz)**.

### Timer Formula

f = 1.44 / ((R1 + 2R2) × C)

Using:

- R1 = 4.7kΩ
- R2 = 4.7kΩ
- C = 100µF

:contentReference[oaicite:0]{index=0}

This pulse acts as the clock signal for the seconds counter.

---

## Counter Breakdown

### Seconds Ones (U1)
Counts:

```plaintext
0 → 9
```

After reaching 9:
- resets to 0
- sends carry pulse to seconds tens

---

### Seconds Tens (U2)
Counts:

```plaintext
0 → 5
```

After reaching 5:
- resets
- sends carry pulse to minute ones

---

### Minutes Ones (U3)
Counts:

```plaintext
0 → 9
```

---

### Minutes Tens (U4)
Counts:

```plaintext
0 → 5
```

---

### Hours Ones (U5)
Counts:

```plaintext
0 → 9
```

---

### Hours Tens (U6)
Counts:

```plaintext
0 → 1
```

System resets after:

```plaintext
12 → 01
```

---

### AM/PM Counter (U7)
Toggles after every 12-hour cycle:

- LOW = AM
- HIGH = PM

---

# Reset Logic

The following ICs handle reset conditions:

- SN74LS08 (AND Gate)
- SN74LS04 (NOT Gate)

### Reset Conditions

| Time Value | Action |
|------------|----------|
| 60 seconds | Reset seconds |
| 60 minutes | Reset minutes |
| 12 hours | Reset hours |
| 12-hour rollover | Toggle AM/PM |

---

# Display System

Each SN74LS47N converts BCD outputs from the counters into signals for the 7-segment displays.

### Segment Mapping

| 7447 Pin | Segment |
|----------|----------|
| 13 | a |
| 12 | b |
| 11 | c |
| 10 | d |
| 9 | e |
| 15 | f |
| 14 | g |

Each segment uses:

```plaintext
Decoder → 330Ω resistor → Display segment
```

---

# Breadboard Layout

Recommended physical arrangement:

```plaintext
[555 TIMER] → [SECONDS] → [MINUTES] → [HOURS] → [AM/PM] → [DISPLAYS]
```

This minimizes wiring complexity.

---

# Simulation Platforms

Recommended simulators:

- :contentReference[oaicite:1]{index=1} (best for exact IC simulation)
- :contentReference[oaicite:2]{index=2}
- :contentReference[oaicite:3]{index=3}
- :contentReference[oaicite:4]{index=4}

---

# Challenges Encountered

- Large number of jumper wires
- Complex reset logic
- Multiple IC synchronization
- Accurate 1Hz pulse generation
- Breadboard space limitations

---

# Future Improvements

- Use a microcontroller such as Arduino Uno
- Add RTC module
- Add alarm functionality
- Improve power efficiency
- Reduce hardware complexity

---

# Authors

Group Members:
- Arindaeng, Paul Daniel
- Desucatan, Miho Jae Person
- Dueñas, Beatrice Gillian
- Mondragon, Christian Paul
- Palomares, Charles Yexel
- Seda, George Albin
---

# License

This project is for educational purposes.
