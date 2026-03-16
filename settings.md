# Configuration Settings (`settings.txt`)
This document explains **all** configuration parameters for the Honda OBD1 Dashboard project.  
All settings can be adjusted by inserting the SD card in a computer and editing the `settings.txt` file on the SD card.

## Format
- Uses simple `key=value` lines  
- Lines before `[SETTINGS]` (if present) are ignored  
- Boolean: `1` = true/yes/on, `0` = false/no/off  
- Strings: no quotes needed unless they contain spaces/special chars  
- Integers/floats: just the number  
- Everything after `=` until end-of-line is the value (trimmed)

---

## 🛠 Basic & Program Settings
| Key                  | Type    | Default       | Description |
|----------------------|---------|---------------|-------------|
| `offlineMode`        | bool    | `0`           | Enable demo/offline/bench mode (no ECU needed). `1`=enabled, `0`=disabled |
| `carName`            | String  | `"Civic EF"`  | Friendly name of this dashboard (shown in Bluetooth or logs) |
| `slaveName`          | String  | `"ECTUNE"`    | Bluetooth name of the ECU module to connect to |

---

## 🚗 Transmission & Gear Calculation
| Key           | Type | Default | Description & Values |
|---------------|------|---------|----------------------|
| `trannyType`  | int  | `0`     | Transmission type / gear ratio table:<br>• `0`: Y21 / Y80 / S80<br>• `1`: ITR S80 JDM 98-01<br>• `2`: ITR S80 USDM 97-01<br>• `3`: Z6 / Y8<br>• `4`: GSR<br>• `5`: LS / RS / GS / SE<br>• `6`: H22 JDM<br>• `7`: H22 USDM / H23 JDM<br>• `8`: H23 USDM<br>• `9`: D16Y7 |

---

## 📊 Measurement Units
| Key          | Type | Default | Values & Meaning |
|--------------|------|---------|------------------|
| `speedUnit`  | int  | `0`     | `0`=KMH, `1`=MPH |
| `mapUnit`    | int  | `0`     | Manifold pressure: `0`=mBar, `1`=Bar, `2`=inHgG, `3`=inHg, `4`=psi, `5`=kPa |
| `tempUnit`   | int  | `0`     | Temperature: `0`=°C, `1`=°F |

---

## 🔌 Hardware & Sensors
### O2 / Wideband Input
| Key           | Type | Default | Description & Values |
|---------------|------|---------|----------------------|
| `O2Input`     | byte | `0`     | ECU pin for wideband/analog O2 signal:<br>• `0`: D14 (O2)<br>• `1`: D10 (ELD)<br>• `2`: D12 (EGR)<br>• `3`: B6 |
| `widebandType`| int  | `0`     | Wideband controller/protocol:<br>• `0`: Voltage (0-5V analog)<br>• `1`: Zeitronix<br>• `2`: Stock AFR<br>• `3`: AEM<br>• `4`: FJO<br>• `5`: Motec<br>• `6`: JAW<br>• `7`: PLX M Series<br>• `8`: Innovate MTS<br>• `9`: Techedge<br>• `10`: AEM New |

### Fuel Level Sensor
| Key                        | Type | Default | Description |
|----------------------------|------|---------|-------------|
| `lowFuelLevelResistance`   | int  | `110`   | Resistance (Ω) of fuel sender when tank is empty |
| `fullFuelLevelResistance`  | int  | `3`     | Resistance (Ω) of fuel sender when tank is full |

---

## ⚠️ Warnings & Sounds
| Key                   | Type              | Default              | Description |
|-----------------------|-------------------|----------------------|-------------|
| `batteryCriticalLevel`| float             | `11.0`               | Critical battery voltage: disables WiFi, stops scheduled wake-ups |
| `batteryWarningLevel` | float             | `11.8`               | Warning battery voltage: shows alert, limits WiFi usage |
| `ectWarningLevel`     | float             | `105`                | ECT warning threshold (in °C) |
| `iatWarningLevel`     | float             | `80`                 | IAT warning threshold (in °C) |
| `milSoundType`        | WarningSoundTypes | `SOUND_CONTINUOUS`   | Sound on MIL: `0`=continuous, `1`=3 beeps, `2`=2 quick beeps, `3`=off |
| `warningSoundType`    | WarningSoundTypes | `SOUND_CONTINUOUS`   | Sound on warnings (temp, battery, etc.): `0`=continuous, `1`=3 beeps, `2`=2 quick beeps, `3`=off |
| `notifySoundType`     | WarningSoundTypes | `SOUND_THREE_BEEPS`  | Sound on notifications (e.g. low fuel): `0`=continuous, `1`=3 beeps, `2`=2 quick beeps, `3`=off |

---

## 💾 Logging
| Key                  | Type          | Default     | Description |
|----------------------|---------------|-------------|-------------|
| `logToSD`            | bool          | `1`         | Enable automatic logging to SD when thresholds met |
| `logRpmThreshold`    | RpmThreshold  | `1000`      | Min RPM to start logging: `0`=always, `1`=1000, `2`=2000, `3`=3000, `4`=4000, `5`=5000 |
| `logTpsThreshold`    | TpsThreshold  | `50`        | Min TPS % to start logging: `0`=always, `1`=25, `2`=50, `3`=75, `4`=100 |

---

## 🌐 WiFi & MQTT Connectivity
| Key                                      | Type   | Default                     | Description |
|------------------------------------------|--------|-----------------------------|-------------|
| `syncTimeWithInternet`                   | bool   | `0`                         | Sync RTC with NTP server when WiFi connected |
| `sendBatteryInfoToMqtt`                  | bool   | `0`                         | Send battery voltage to MQTT periodically |
| `sendSDcardDataToMqttWhenConnectedToCharger` | bool | `0`                     | Upload all SD logs to MQTT when charger detected |
| `wifi_ssid`                              | String | `"wifi_ssid"`               | WiFi network name |
| `wifi_password`                          | String | `"wifi_password"`           | WiFi password |
| `mqtt_server`                            | String | `"192.168.0.1"`             | MQTT broker IP/hostname |
| `mqtt_client_name`                       | String | `"Honda_dash"`              | Client ID for MQTT connection |
| `mqtt_server_topic_battery`              | String | `"civic-dash/battery"`      | Topic for battery messages |
| `mqtt_server_topic_logs`                 | String | `"civic-dash/log_data"`     | Topic for log file data upload |

---

## 🖥️ Display & Shutdown
| Key                  | Type   | Default | Description |
|----------------------|--------|---------|-------------|
| `menuMode`           | MenuModes | `SENSORS_1` | Last used menu screen (auto-saved) |
| `shutdownAnimation`  | bool   | `1`     | Show nice shutdown animation when ignition turned off |
| `shutdownImage`      | int    | `0`     | Image during shutdown: `0`=Honda logo, `1`=Civic EF, `3`=Civic EK, `4`=Integra Type R |

---
