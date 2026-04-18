# Sources and Articles

Use these as primary references in your bachelor thesis.

## Official documentation
1. **ESP32 (Espressif)**
   - https://docs.espressif.com/projects/esp-idf/en/latest/esp32/
2. **ESPHome official docs**
   - https://esphome.io/
3. **ESPHome remote transmitter (IR)**
   - https://esphome.io/components/remote_transmitter.html
4. **ESPHome remote receiver (for capturing IR codes)**
   - https://esphome.io/components/remote_receiver.html
5. **ESPHome DHT sensor docs (for DHT22/AM2302 type sensors)**
   - https://esphome.io/components/sensor/dht.html

## IR and protocol references
6. **IRremoteESP8266 library (AC protocols, examples, background)**
   - https://github.com/crankyoldgit/IRremoteESP8266
7. **Ken Shirriff IR tutorial (foundational IR remote theory)**
   - http://www.righto.com/2009/08/multi-protocol-infrared-remote-library.html

## Networking and IoT security
8. **OWASP IoT Top 10**
   - https://owasp.org/www-project-internet-of-things/
9. **NISTIR 8259A (IoT device cybersecurity capability baseline)**
   - https://csrc.nist.gov/publications/detail/nistir/8259a/final

## Academic search suggestions (for peer-reviewed papers)
Search in:
- IEEE Xplore
- ScienceDirect
- SpringerLink
- Google Scholar

Suggested keywords:
- “ESP32 smart home HVAC control”
- “infrared air conditioner control IoT”
- “temperature humidity closed-loop control hysteresis”
- “edge IoT device cybersecurity home automation”
- “ESPHome home assistant integration”

## Note for your hardware uncertainty
If sensor is listed as “M22”, verify if it is actually **DHT22/AM2302** by checking:
- Label on sensor module
- Seller datasheet
- Pinout and timing behavior

Document this verification step in thesis methodology.
