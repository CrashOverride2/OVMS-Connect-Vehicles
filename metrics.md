### The OVMS Standard Metric List

---

### `m.*` - Module & Network Metrics

| Metric (Topic) | Description from Source | Unit |
| :--- | :--- | :--- |
| `m.version` | OVMS firmware version. | String |
| `m.hardware` | OVMS hardware version. | String |
| `m.serial` | OVMS module serial number. | String |
| `m.tasks` | Number of running tasks. | Integer |
| `m.freeram` | Free RAM on the module. | Bytes |
| `m.monotonic` | Monotonic clock time since boot. | Seconds |
| `m.time.utc` | Current UTC time. | Unix Timestamp |
| `m.net.type` | Network type (e.g., none, wifi, modem). | String |
| `m.net.sq` | Overall network signal quality. | dBm |
| `m.net.provider` | Network provider name. | String |
| `m.net.connected` | True if connected to any network. | Boolean |
| `m.net.ip` | True if the device has an IP address. | Boolean |
| `m.net.good.sq` | True if signal quality is above the configured threshold. | Boolean |
| `m.net.mdm.iccid` | ICCID of the SIM card in the modem. | String |
| `m.net.mdm.model` | Model of the modem. | String |
| `m.net.mdm.netreg`| Modem network registration state. | String |
| `m.net.mdm.network`| Modem network operator name. | String |
| `m.net.mdm.sq` | Modem network signal quality. | dBm |
| `m.net.mdm.mode` | Cellular connection mode and status. | String |
| `m.net.wifi.network`| WiFi network SSID. | String |
| `m.net.wifi.sq` | WiFi network signal quality. | dBm |
| `m.obdc2ecu.on` | True if the OBD2ECU process is running. | Boolean |

### `s.*` - Server Connection Metrics

| Metric (Topic) | Description from Source | Unit |
| :--- | :--- | :--- |
| `s.v2.connected` | True if connected to a V2 server. | Boolean |
| `s.v2.peers` | Number of V2 clients connected. | Integer |
| `s.v3.connected` | True if connected to a V3 (MQTT) server. | Boolean |
| `s.v3.peers` | Number of V3 clients connected. | Integer |

### `v.*` - Vehicle Metrics

#### `v.b.*` - Battery Metrics (Main)

| Metric (Topic) | Description from Source | Unit |
| :--- | :--- | :--- |
| `v.b.soc` | State of charge. | % |
| `v.b.soh` | State of health. | % |
| `v.b.cac` | Calculated Amp-hour Capacity. | Ah |
| `v.b.capacity` | Main battery usable capacity. | kWh |
| `v.b.health` | Textual description of battery health. | String |
| `v.b.voltage` | Main battery momentary voltage. | V |
| `v.b.current` | Main battery momentary current (positive=output). | A |
| `v.b.power` | Main battery momentary power (positive=output). | kW |
| `v.b.consumption` | Main battery momentary consumption. | Wh/km |
| `v.b.coulomb.used`| Coulomb used on trip. | Ah |
| `v.b.coulomb.recd`| Coulomb recovered (regen) on trip. | Ah |
| `v.b.energy.used` | Energy used on trip. | kWh |
| `v.b.energy.recd` | Energy recovered (regen) on trip. | kWh |
| `v.b.coulomb.used.total`| Lifetime coulomb used. | Ah |
| `v.b.coulomb.recd.total`| Lifetime coulomb recovered. | Ah |
| `v.b.energy.used.total` | Lifetime energy used. | kWh |
| `v.b.energy.recd.total` | Lifetime energy recovered. | kWh |
| `v.b.range.full` | Ideal range at 100% SOC. | km |
| `v.b.range.ideal`| Ideal range at current SOC. | km |
| `v.b.range.est` | Estimated range based on recent driving. | km |
| `v.b.temp` | Main battery temperature. | °C |
| `v.b.12v.voltage`| Auxiliary 12V battery voltage. | V |
| `v.b.12v.current`| Auxiliary 12V battery current. | A |
| `v.b.12v.voltage.ref`| Auxiliary 12V battery reference voltage. | V |
| `v.b.12v.voltage.alert` | True if 12V battery voltage is low. | Boolean |

#### `v.b.p.*` - Battery Pack Level Metrics

| Metric (Topic) | Description from Source | Unit |
| :--- | :--- | :--- |
| `v.b.p.level.min` | Cell level - weakest cell in pack (normalized to percent). | % |
| `v.b.p.level.max` | Cell level - strongest cell in pack (normalized to percent). | % |
| `v.b.p.level.avg` | Cell level - pack average (normalized to percent). | % |
| `v.b.p.level.stddev` | Cell level - pack standard deviation (normalized to percent). | % |
| `v.b.p.voltage.min`| Cell voltage - weakest cell in pack. | V |
| `v.b.p.voltage.max`| Cell voltage - strongest cell in pack. | V |
| `v.b.p.voltage.avg`| Cell voltage - pack average. | V |
| `v.b.p.voltage.stddev` | Cell voltage - current standard deviation. | V |
| `v.b.p.voltage.stddev.max` | Cell voltage - maximum standard deviation observed. | V |
| `v.b.p.voltage.grad`| Cell voltage - gradient of current series. | V |
| `v.b.p.temp.min` | Cell temperature - coldest cell in pack. | °C |
| `v.b.p.temp.max` | Cell temperature - warmest cell in pack. | °C |
| `v.b.p.temp.avg` | Cell temperature - pack average. | °C |
| `v.b.p.temp.stddev`| Cell temperature - current standard deviation. | °C |
| `v.b.p.temp.stddev.max`| Cell temperature - maximum standard deviation observed. | °C |

#### `v.b.c.*` - Battery Cell Level Metrics (Vectors/Arrays)

| Metric (Topic) | Description from Source | Unit |
| :--- | :--- | :--- |
| `v.b.c.voltage` | Cell voltages. | V |
| `v.b.c.voltage.min`| Cell minimum voltages. | V |
| `v.b.c.voltage.max`| Cell maximum voltages. | V |
| `v.b.c.voltage.dev.max`| Cell maximum voltage deviation observed. | V |
| `v.b.c.voltage.alert`| Cell voltage deviation alert level (0=normal, 1=warn, 2=alert). | Integer |
| `v.b.c.temp` | Cell temperatures. | °C |
| `v.b.c.temp.min` | Cell minimum temperatures. | °C |
| `v.b.c.temp.max` | Cell maximum temperatures. | °C |
| `v.b.c.temp.dev.max`| Cell maximum temperature deviation observed. | °C |
| `v.b.c.temp.alert`| Cell temperature deviation alert level (0=normal, 1=warn, 2=alert). | Integer |

#### `v.c.*` - Charger Metrics

| Metric (Topic) | Description from Source | Unit |
| :--- | :--- | :--- |
| `v.c.voltage` | Momentary charger supply voltage. | V |
| `v.c.current` | Momentary charger output current to battery. | A |
| `v.c.power` | Momentary charger input power. | kW |
| `v.c.efficiency` | Momentary charger efficiency. | % |
| `v.c.climit` | Maximum charger output current available. | A |
| `v.c.time` | Duration of the current charge session. | Seconds |
| `v.c.kwh` | Energy sum for the running charge session (to battery). | kWh |
| `v.c.kwh.grid` | Energy drawn from grid during the running session. | kWh |
| `v.c.kwh.grid.total` | Lifetime energy drawn from the grid. | kWh |
| `v.c.mode` | Charge mode (e.g., `standard`, `range`, `performance`). | String |
| `v.c.timermode` | True if the charge timer is enabled. | Boolean |
| `v.c.timerstart` | Time the charge timer is scheduled to start. | Unix Timestamp |
| `v.c.state` | Charge state (e.g., `charging`, `topoff`, `done`, `stopped`). | String |
| `v.c.substate` | Detailed charge substate (e.g., `scheduledstop`, `powerwait`). | String |
| `v.c.type` | Charger type (e.g., `type1`, `type2`, `ccs`, `chademo`). | String |
| `v.c.pilot` | True if the charge pilot signal is present. | Boolean |
| `v.c.charging` | True if the vehicle is currently charging. | Boolean |
| `v.c.limit.range`| Sufficient range limit for the current charge. | km |
| `v.c.limit.soc` | Sufficient SOC limit for the current charge. | % |
| `v.c.duration.full`| Estimated time remaining for a full charge. | Minutes |
| `v.c.duration.range`| Estimated time remaining to reach the range limit. | Minutes |
| `v.c.duration.soc` | Estimated time remaining to reach the SOC limit. | Minutes |
| `v.c.temp` | Charger temperature. | °C |
| `v.c.timestamp` | Date & time of last charge end. | DateLocal |
| `v.c.12v.current`| Output current of DC/DC-converter. | A |
| `v.c.12v.power` | Output power of DC/DC-converter. | W |
| `v.c.12v.temp` | Temperature of DC/DC-converter. | °C |
| `v.c.12v.voltage`| Output voltage of DC/DC-converter. | V |

#### `v.d.*` - Door & Port Metrics

| Metric (Topic) | Description from Source | Unit |
| :--- | :--- | :--- |
| `v.d.fl` | Door Front Left is open. | Boolean |
| `v.d.fr` | Door Front Right is open. | Boolean |
| `v.d.rl` | Door Rear Left is open. | Boolean |
| `v.d.rr` | Door Rear Right is open. | Boolean |
| `v.d.cp` | Charge Port is open. | Boolean |
| `v.d.hood` | Hood is open. | Boolean |
| `v.d.trunk` | Trunk is open. | Boolean |

#### `v.e.*` - Environment & State Metrics

| Metric (Topic) | Description from Source | Unit |
| :--- | :--- | :--- |
| `v.e.drivemode` | Active drive profile number. | Integer |
| `v.e.gear` | Current gear/direction (negative=reverse, 0=neutral). | Integer |
| `v.e.throttle` | Accelerator pedal state. | % |
| `v.e.footbrake` | Brake pedal state. | % |
| `v.e.handbrake` | Handbrake state. | Boolean |
| `v.e.regenbrake` | Regenerative braking state. | Boolean |
| `v.e.awake` | Vehicle is fully awake (e.g., switched on by user). | Boolean |
| `v.e.charging12v`| 12V battery is currently charging. | Boolean |
| `v.e.aux12v` | 12V auxiliary system is on (base system awake). | Boolean |
| `v.e.cooling` | Cooling system is active. | Boolean |
| `v.e.heating` | Heating system is active. | Boolean |
| `v.e.hvac` | Climate control system is active. | Boolean |
| `v.e.on` | Vehicle is in "ignition" state (drivable). | Boolean |
| `v.e.locked` | Vehicle is locked. | Boolean |
| `v.e.valet` | Vehicle is in valet mode. | Boolean |
| `v.e.headlights` | Headlights are on. | Boolean |
| `v.e.alarm` | Alarm is sounding. | Boolean |
| `v.e.parktime` | Time since the vehicle was parked. | Seconds |
| `v.e.drivetime` | Duration of the current drive. | Seconds |
| `v.e.temp` | Ambient temperature. | °C |
| `v.e.cabintemp` | Cabin temperature. | °C |
| `v.e.cabinfan` | Cabin FAN speed. | % |
| `v.e.cabinsetpoint`| Cabin setpoint temperature. | °C |
| `v.e.cabinintake`| Cabin intake type (e.g., fresh, recirc). | String |
| `v.e.cabinvent` | Cabin vent type (e.g., feet, face). | String |
| `v.e.serv.range` | Distance to next scheduled service. | km |
| `v.e.serv.time` | Time of scheduled service. | DateLocal |

#### `v.g.*` - Generator (V2G/V2H) Metrics

| Metric (Topic) | Description from Source | Unit |
| :--- | :--- | :--- |
| `v.g.voltage` | Momentary generator output voltage. | V |
| `v.g.current` | Momentary generator input current (from battery). | A |
| `v.g.power` | Momentary generator output power. | kW |
| `v.g.efficiency` | Momentary generator efficiency. | % |
| `v.g.climit` | Maximum generator input current. | A |
| `v.g.time` | Duration of generator running. | Seconds |
| `v.g.kwh` | Energy sum generated in the running session. | kWh |
| `v.g.kwh.grid` | Energy sent to grid during running session. | kWh |
| `v.g.kwh.grid.total` | Lifetime energy sent to grid. | kWh |
| `v.g.mode` | Generator mode. | String |
| `v.g.timermode` | True if generator timer is enabled. | Boolean |
| `v.g.timerstart` | Time generator is due to start. | Unix Timestamp |
| `v.g.state` | Generator state. | String |
| `v.g.substate` | Generator substate. | String |
| `v.g.type` | Connection type (e.g., ccs, chademo). | String |
| `v.g.pilot` | Pilot signal present. | Boolean |
| `v.g.generating` | True if currently delivering power. | Boolean |
| `v.g.limit.range`| Minimum range limit for generator mode. | km |
| `v.g.limit.soc` | Minimum SOC limit for generator mode. | % |
| `v.g.duration.empty`| Estimated time remaining for full discharge. | Minutes |
| `v.g.duration.range`| Estimated time remaining to reach range limit. | Minutes |
| `v.g.duration.soc`| Estimated time remaining to reach SOC limit. | Minutes |
| `v.g.temp` | Generator temperature. | °C |
| `v.g.timestamp` | Date & time of last generation end. | DateLocal |

#### `v.i.*` & `v.m.*` - Inverter & Motor Metrics

| Metric (Topic) | Description from Source | Unit |
| :--- | :--- | :--- |
| `v.i.temp` | Inverter temperature. | °C |
| `v.i.power` | Momentary inverter motor power (positive=output). | kW |
| `v.i.efficiency` | Momentary inverter efficiency. | % |
| `v.m.rpm` | Motor speed. | RPM |
| `v.m.temp` | Motor temperature. | °C |

#### `v.p.*` - Position & Trip Metrics

| Metric (Topic) | Description from Source | Unit |
| :--- | :--- | :--- |
| `v.p.gpslock` | GPS has a valid signal lock. | Boolean |
| `v.p.gpsmode` | GPS mode (e.g., N/A/D/E). | String |
| `v.p.gpshdop` | Horizontal dilution of precision (smaller=better). | Float |
| `v.p.satcount` | Number of GPS satellites in view. | Integer |
| `v.p.gpssq` | GPS signal quality. | % |
| `v.p.gpstime` | UTC Time of GPS coordinates. | Unix Timestamp |
| `v.p.latitude` | Latitude. | Degrees |
| `v.p.longitude` | Longitude. | Degrees |
| `v.p.location` | Name of current location if defined. | String |
| `v.p.direction` | Heading direction. | Degrees |
| `v.p.altitude` | Altitude. | m |
| `v.p.speed` | Vehicle speed from CAN bus. | km/h |
| `v.p.acceleration`| Vehicle acceleration. | m/s² |
| `v.p.gpsspeed` | Speed over ground from GPS. | km/h |
| `v.p.odometer` | Vehicle odometer. | km |
| `v.p.trip` | Current trip distance. | km |
| `v.p.valet.latitude` | Valet mode center latitude. | Degrees |
| `v.p.valet.longitude` | Valet mode center longitude. | Degrees |
| `v.p.valet.distance` | Distance from valet center. | m |

#### `v.t.*` / `v.tp.*` - Tire Pressure Metrics

| Metric (Topic) | Description from Source | Unit |
| :--- | :--- | :--- |
| `v.tp.fl.p` / `v.tp.fr.p`... | Tire Pressure for specific wheel (Front-Left, etc.). | kPa |
| `v.tp.fl.t` / `v.tp.fr.t`... | Tire Temperature for specific wheel (Front-Left, etc.). | °C |
| `v.t.pressure` | Vector/array of all tire pressures. | kPa |
| `v.t.temp` | Vector/array of all tire temperatures. | °C |
| `v.t.health` | Vector/array of all tire health states. | % |
| `v.t.alert` | Vector/array of all tire alert levels (0=normal, 1=warn, 2=alert). | Integer |