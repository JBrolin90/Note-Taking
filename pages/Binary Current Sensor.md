---
Note-Type: Permanent
tags:
  - Permanent
Date: 2026-01-27
Topic:
  - "[[HA]]"
  - "[[Home Assistant]]"
  - "[[Water Boiler]]"
  - "[[Sensor]]"
  - "[[Template]]"
---
```YAML
template:
  - binary_sensor:
      - name: "Water boiler"
        unique_id: water_boiler_sensor_01  # Highly recommended for UI editing
        state: >
          {% set current = states('sensor.tz3000_ww6drja5_ts011f_plug_current') | float(0) %}
          {{ current > 1.0 }}
```
