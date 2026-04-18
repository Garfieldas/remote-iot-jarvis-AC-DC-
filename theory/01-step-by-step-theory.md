# Step-by-Step Theory for Remote IoT AC System

## 1) Problem definition
Goal: control an AC remotely over internet while monitoring room temperature/humidity.

Core functions:
- Read temperature/humidity
- Send IR commands to AC (power, mode, temp, fan)
- Provide remote UI and automations
- Log values for evaluation

## 2) System architecture (high-level)
1. **ESP32** reads sensor and drives IR LED.
2. **ESPHome** runs on ESP32 and exposes entities to dashboard/home automation.
3. User interacts via phone/web UI.
4. ESP32 sends IR frames that mimic original AC remote.
5. Feedback loop uses sensor readings to trigger rules (e.g., if temp > setpoint, start cooling).

## 3) Hardware theory
### ESP32
- Chosen for Wi-Fi + enough processing + GPIO/PWM/RMT support for IR.

### Temperature/Humidity sensor
- If your “M22” is actually **DHT22/AM2302**, it uses single-wire digital output.
- Sampling is slow (~0.5 Hz typical), so apply filtering and avoid very fast control loops.

### IR transmitter
- AC remotes usually use 38 kHz carrier and protocol-specific payload.
- Use transistor driver for IR LED current stability and better range.

## 4) IR control theory
1. Capture original remote signals (receiver module helps identify protocol/raw code).
2. Map each AC function to known codes:
   - Power on/off
   - Mode (cool/heat/fan/auto)
   - Target temperature
   - Fan speed/swing
3. Validate each code with real AC response.
4. Prefer protocol-based code (if supported) over long raw pulses for reliability.

## 5) Control logic theory
Use hysteresis to avoid rapid ON/OFF toggling:
- Example:
  - If `temp > target + 0.7°C` => send cool command
  - If `temp < target - 0.3°C` => send stop or fan-only command
- Rationale: asymmetric bands can reduce compressor cycling while keeping comfort; tune values experimentally for your room/AC model.

Add:
- Minimum command interval (e.g., 30–60 s)
- Last-command state memory
- Fallback if sensor read fails

## 6) ESPHome implementation flow (theoretical)
1. Configure board + Wi-Fi + OTA + API.
2. Add sensor component (GPIO + update interval).
3. Add `remote_transmitter` (IR output pin).
4. Define template buttons/selects/numbers for AC actions.
5. Connect UI controls to IR send actions.
6. Add automation rules based on sensor thresholds.
7. Expose logs/metrics for evaluation.

## 7) Networking + security theory
- Keep device on trusted network (VLAN if possible).
- Use encrypted remote access path (VPN/Home Assistant secure setup).
- Protect OTA/API credentials.
- Add watchdog/restart strategy for fault recovery.

## 8) Validation methodology (for thesis)
Measure:
1. **IR reliability**: successful commands / sent commands
2. **Control quality**: average temp error vs setpoint
3. **Latency**: UI click to AC reaction
4. **Stability**: no oscillation due to hysteresis design
5. **Availability**: uptime over test period

## 9) Typical risks and mitigations
- Wrong sensor model assumptions → verify exact part number in datasheet.
- IR angle/range issues → tune LED placement and drive current.
- AC vendor protocol mismatch → capture and test full-state commands.
- Network outages → keep local manual control and safe default behavior.
