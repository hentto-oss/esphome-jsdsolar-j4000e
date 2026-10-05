# esphome-jsdsolar-j4000e
ESPHome configuration for JSDSolar JSD4000E inverter with Modbus RTU and Home Assistant Lovelace card.
# ESPHome Integration for JSDSolar JSD4000E Inverter (Modbus RTU)

Complete local integration for the **JSDSolar JSD4000E** solar inverter using ESPHome (ESP32 + RS485-to-TTL converter) and Home Assistant. This project replaces the unstable stock cloud application with a reliable, fast, and 100% local Modbus connection.

## Features
- **Real-time Monitoring:** Grid parameters (voltage, current, frequency, power), Load power, PV status, and temperatures.
- **Battery Analytics:** Voltage, current, SOC (%), and battery power.
- **Energy Statistics:** Total PV energy, total load, and battery totals converted to kWh (compatible with Home Assistant Energy Dashboard).
- **Controls (Writable Registers):** Directly change **Output Priority (Menu 03)** and **Charger Priority** options from your Home Assistant Dashboard.
  
---

## 🛠️ Hardware Setup
Connect your ESP32 to the inverter's Modbus/RS485 port using an RS485-to-TTL converter:
- **TX_PIN:** GPIO17
- **RX_PIN:** GPIO16
![Pinout falownika](pinout.png)
---

## 📋 Configuration

1. Add the secure `jsdsolar-j4000e.yaml` configuration to your ESPHome dashboard.
2. Make sure your `secrets.yaml` file includes the following entries:
```yaml
wifi_home_ssid: "YOUR_HOME_WIFI_SSID"
wifi_home_password: "YOUR_HOME_WIFI_PASSWORD"
wifi_ap_password: "YOUR_FALLBACK_AP_PASSWORD"
```

---

## 📊 Home Assistant Dashboard (Lovelace)
![Dashboard Home Assistant](dashboard.png)
To get a beautiful, animated power flow visualization, install `xpower-flow-card` via HACS and use the following YAML configuration for your card:

```yaml
type: custom:xpower-flow-card
preset: custom
inverter_name: Inverter jsd4000e
language: pl
font_size: 28
compact: false
card_style: xpower
energy_frame: true
arrow_style: arrow
power_unit: auto
temp_unit: auto
theme: auto
animations: auto
flow_speed: proportional
solar: sensor.salon_jsdsolar_j4000e_custom_jsd4000e_pv1_power
pv_voltage: sensor.salon_jsdsolar_j4000e_custom_jsd4000e_pv1_voltage
battery: sensor.jsdsolar_j4000e_custom_jsd4000e_battery_power
battery_voltage: sensor.salon_jsdsolar_j4000e_custom_jsd4000e_battery_voltage
soc: sensor.salon_jsdsolar_j4000e_custom_jsd4000e_battery_soc
shutdown_soc: 20
battery_capacity: 2560
bat_polarity: negative
load: sensor.jsdsolar_j4000e_custom_jsd4000e_load_power
grid: sensor.jsdsolar_j4000e_custom_jsd4000e_grid_power
frequency: sensor.jsdsolar_j4000e_custom_jsd4000e_grid_frequency
grid_polarity: positive
grid_threshold: 0
sun_entity: sun.sun
daily_solar: sensor.jsdsolar_j4000e_custom_jsd4000e_pv_energy_total
daily_load: sensor.jsdsolar_j4000e_custom_jsd4000e_load_energy_total
daily_charge: sensor.jsdsolar_j4000e_custom_jsd4000e_battery_energy_total
temperature: sensor.jsdsolar_j4000e_custom_jsd4000e_inverter_temperature
grid_voltage: ''
grid_status: ''
daily_import: ''
daily_export: ''
daily_discharge: ''
battery_temperature: ''
solar2: ''
solar3: ''
pv_voltage2: ''
pv_voltage3: ''
battery_charge: ''
battery_discharge: ''
grid_voltage_l2: ''
grid_voltage_l3: ''
weather_temp: ''
weather_humidity: ''
weather_entity: ''
price_sensor: ''
ev_power: ''
ev_soc: ''
daily_ev: ''
extra1_power: ''
extra1_name: ''
extra1_icon: appliance
extra2_power: ''
extra2_name: ''
extra2_icon: heatpump
extra3_power: ''
extra3_name: ''
extra3_icon: garage
import_cost: ''
export_cost: ''
sparkline_shared_scale: false
mppt_scale: 1

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## ENCJE

type: entities
title: Dane teraz
icon: mdi:solar-power
show_header_toggle: false
entities:
  - entity: sensor.jsdsolar_j4000e_custom_jsd4000e_battery_power
    name: Magazyn (Moc)
    icon: mdi:battery-flash
  - entity: sensor.jsdsolar_j4000e_custom_jsd4000e_battery_current
    name: Magazyn (Prąd)
    icon: mdi:current-dc
  - entity: sensor.salon_jsdsolar_j4000e_custom_jsd4000e_battery_voltage
    name: Magazyn (Napięcie)
    icon: mdi:battery-high
  - entity: sensor.salon_jsdsolar_j4000e_custom_jsd4000e_battery_soc
    name: Stan naładowania (SOC)
    icon: mdi:battery-charging-80
  - entity: sensor.jsdsolar_j4000e_custom_jsd4000e_battery_energy_total
    name: Magazyn (Suma energii)
    icon: mdi:counter
  - type: divider
  - entity: sensor.jsdsolar_j4000e_custom_jsd4000e_load_power
    name: Dom (Obciążenie bieżące)
    icon: mdi:home-lightning-bolt
  - entity: sensor.jsdsolar_j4000e_custom_jsd4000e_load_energy_total
    name: Dom (Suma zużycia)
    icon: mdi:counter
  - type: divider
  - entity: sensor.salon_jsdsolar_j4000e_custom_jsd4000e_pv1_power
    name: PV (Moc ze słońca)
    icon: mdi:solar-panel-large
  - entity: sensor.jsdsolar_j4000e_custom_jsd4000e_pv1_current
    name: PV (Prąd z paneli)
    icon: mdi:current-dc
  - entity: sensor.salon_jsdsolar_j4000e_custom_jsd4000e_pv1_voltage
    name: PV (Napięcie stringu)
    icon: mdi:flash-outline
  - entity: sensor.jsdsolar_j4000e_custom_jsd4000e_pv_energy_total
    name: PV (Suma produkcji)
    icon: mdi:counter
  - type: divider
  - entity: sensor.jsdsolar_j4000e_custom_jsd4000e_inverter_temperature
    name: Temperatura falownika
    icon: mdi:thermometer
