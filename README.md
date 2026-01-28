# ha_battery_dynamic_prices

## 🔋 Dynamic Electricity Price Control for Fronius BYD Batteries in Home Assistant

This project provides **Home Assistant template sensors and automations** that optimize charging and discharging of a **Fronius + BYD battery system** based on **dynamic electricity prices** Nordpool .

The goal is simple:  
**Charge the battery when electricity is cheap, avoid charging when it’s expensive, and optionally discharge during high‑price periods.**

This improves self‑consumption, reduces energy costs, and increases the economic efficiency of your battery system.

---

## 📦 Repository Contents

| File | Description |
|------|-------------|
| `configuration.yaml` | Template sensors for evaluating dynamic prices and deriving battery control logic |
| `byd_laden_sperren.yaml` | Automation to charges the battery when prices are low and prevents the battery from discharging until byd_entladen starts |
| `byd_entladen.yaml` | Automation to enable battery discharging during high‑price periods |

---

## ⚙️ Requirements

To use this project, you need:

- **Home Assistant** (latest recommended version)
- **Fronius inverter with BYD battery**
- Integrations:
  - **Fronius** https://github.com/callifo/fronius_modbus
  - **Dynamic electricity price provider**, Nordpool
---

## 🧠 How It Works

### 1. Dynamic Price Sensors  
The template sensors in `configuration.yaml` evaluate:

- current electricity price  
- thresholds for “cheap”, “normal”, and “expensive”  
- whether charging or discharging is economically optimal  

This creates a simple decision model:

- **Low price → Charge battery**
- **High price → Discharge battery**
- **Normal price → Stop discharging**

---

## 🔄 Automations

### 🚫 `byd_laden_sperren.yaml` — Charge and Block Charging/Discharging  
This automation charges the battery when prices are low and prevents the battery from discharging until byd_entladen starts.

---

### ⚡ `byd_entladen.yaml` — Enable Discharging  
This automation forces the battery to discharge when prices are high.

---

## 📥 Installation

### 1. Copy the files  
Place the YAML files into your Home Assistant configuration directory:

/config/
configuration.yaml
byd_laden_sperren.yaml
byd_entladen.yaml


### 2. Include the automations  
In your main `configuration.yaml`:

automation: !include byd_laden_sperren.yaml
automation: !include byd_entladen.yaml

3. Restart Home Assistant
A full restart ensures all sensors and automations load correctly.

📄 License
You may add a license of your choice (MIT recommended).
