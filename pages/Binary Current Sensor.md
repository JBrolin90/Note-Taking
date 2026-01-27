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

- **`template:` vs `binary_sensor:`**: This is the core of the update. The legacy `platform: template` is being removed. Now, all templates (sensors, binary sensors, etc.) live under this one `template:` heading.
    
- **Boolean Logic**: In modern binary sensor templates, you don't need `if/else` statements. The expression `current | float(0) > 1.0` automatically returns `True` if it's over 1 and `False` if it isn't.
    
- **`float(0)`**: Using `| float(0)` is a safety measure. If your Zigbee plug is offline or sending an "unknown" state, the `(0)` provides a default value so the template doesn't crash your logs with errors.
    
- **`unique_id`**: I added this so you can change the icon, name, or area of the boiler directly in the **Settings > Entities** UI without touching the YAML again.
    
- **`device_class: power`**: This is optional, but it tells Home Assistant this sensor is power-related, which helps it choose the right "on/off" icons and behavior automatically.