# Temperature-Controlled Clock Circuit (NE555 + Op-Amps)

An analog version of what a CPU does when it overheats. The clock speeds up under load. When the circuit detects too much stress, it switches on a cooling fan and throttles the clock back down. There is no microcontroller and no code.

This was a team project for Analog Electronics (BAECE203) at VIT Chennai, guided by Dr. Sangeetha R G.

![Breadboard build](breadboard-build.jpg)

## How it works
- **Clock:** an **NE555** timer generates the clock signal. A red LED blinks with every pulse.
- **Speed control:** an **op-amp** drives the 555's control-voltage pin (pin 5). This shifts its thresholds and changes the clock frequency.
- **Fan switch:** a second op-amp works as a **threshold detector**. When the input crosses the set-point, it switches an **NMOS** that turns on a 9 V fan.
- **Throttling:** a **feedback path** pulls the clock frequency back down to a safe range.

![LTspice schematic](ltspice-schematic.png)

## Results
Measured on a Keysight DSOX1202A oscilloscope, with the period read using cursors.

| Setting | Frequency (period) | Scope capture |
|---|---|---|
| Low input | 8.47 Hz (118 ms) | ![](scope-8.47hz.jpg) |
| Normal operating point (designed for 12.0 Hz, within 4%) | 12.5 Hz (80 ms) | ![](scope-12.5hz.jpg) |
| Input pushed higher ("overclocked") | 20.8 Hz (48 ms) | ![](scope-20.8hz.jpg) |
| Maximum, right at the threshold | 25.6 Hz (39 ms) | ![](scope-25.6hz.jpg) |
| Threshold crossed: fan on, clock throttled back | 7.14 Hz (140 ms) | ![](scope-7.14hz-throttled.jpg) |

- **Range:** the clock covers **7.1 Hz to 25.6 Hz**, set entirely by the voltage on one pin.
- **Modelling:** a Python model of the 555's charge/discharge cycle works backwards from each scope reading to the actual control voltage.

## Next improvements
- **Hysteresis,** so the fan doesn't chatter near the threshold.
- **PWM fan speed control** instead of on/off.
- **A real temperature sensor** in place of the potentiometer.
- **A PCB** instead of the breadboard.

## Team
Bharathwaaj Subramanian · Kiran Kumar Sundararaman · Mohit Chandravarman
