# Brake System Plausibility Device (BSPD)

**Manchester Stinger Motorsports** · Rev V4.0

The BSPD is a **non-programmable safety circuit**, implemented entirely in discrete
logic with **no microcontroller anywhere in the fault-detection or shutdown path**.
It continuously monitors the throttle position sensor (TPS) and brake pressure
sensor (BPS) and cuts power to the vehicle if either reports an implausible
condition.

---

## Fault conditions

### 1. Simultaneous brake and throttle
If the BPS indicates the brakes are applied while the TPS reads **more than 25 %
above idle position**, and both conditions persist continuously for **500 ms**, the
circuit cuts power to the vehicle.

### 2. Sensor signal out of range
If either the TPS or BPS signal falls outside the expected **0.5 V – 4.5 V** range
for **500 ms** — indicating a wiring fault, sensor failure, or an open or short
circuit — the circuit cuts power.

---

## Functional block diagram

![BSPD functional block diagram: the BPS and TPS sensor signals feed an AND stage
(simultaneous brake and throttle); its output is OR'd with the SCS signal, which
flags either sensor leaving the 0.5–4.5 V range. The combined fault passes through
a 500 ms RC delay that latches Power Off, and drives an inverter into a 555-based
10 s timer that restores Power On once the fault has been clear for the full
window.](docs/system-block-diagram.png)
