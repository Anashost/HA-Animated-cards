<!-- anashost_support_badges_start -->
[![Revolut.Me][revolut_me_shield]][revolut_me]
[![PayPal.Me][paypal_me_shield]][paypal_me]
[![ko_fi][ko_fi_shield]][ko_fi_me]
[![buymecoffee][buy_me_coffee_shield]][buy_me_coffee_me]
[![patreon][patreon_shield]][patreon_me]
<!-- anashost_support_badges_end -->
<!-- 
```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
-->

<div align="left">
<a href="https://github.com/Anashost/HA-Animated-cards">
  <img src="https://img.shields.io/badge/◀_BACK_TO_HOME_Page-2196F3?style=for-the-badge&logoColor=white" height="60" />
</a>
</div>

# Home Assistant Animated Appliances Cards V2

>* Dishwasher
>
>* Washing Machine
>
>* Dryer
>
>* Combo Washer & Dryer
>
>* Fridge

This [YouTube Video](https://youtu.be/3Njo1-jht5w) explains how to do it.

<img width="1280" height="720" alt="40-high" src="https://github.com/user-attachments/assets/266e4098-7268-4c91-9036-ce5a375aad8a" />


 `Loading image... please wait`

<hr>

> [!NOTE]
> If you are using the **Sections** view type, you may need to set `rows` to around `1.5` for the card,
> otherwise the card may appear compressed.
> (USE THIS ONLY IF YOU HAVE ISSUES).
>
> ```yaml
> grid_options:
>   rows: 1.6
> ```

<hr>

# Cards (Smart)

<details>
<summary><strong>1 - Smart Dishwasher</summary>

```yaml
type: custom:button-card
entity: sensor.smart_dishwasher_status
name: Smart Dishwasher
show_state: false
show_label: true
variables:
  sensor_status: sensor.smart_dishwasher_status
  sensor_progress: sensor.smart_dishwasher_progress
  sensor_time_remaining: sensor.smart_dishwasher_time_remaining
  sensor_power: sensor.smart_dishwasher_power
  sensor_percentage: sensor.smart_dishwasher_percentage
  sensor_door: binary_sensor.smart_dishwasher_door
  max_time: 150
  state_idle: idle, off, standby, unknown, unavailable
  state_running: wash, washing, rinse, rinsing, pre-wash
  state_drying: dry, drying
  state_done: finished, complete, end
  size_icon: 45px
  size_shape: 65px
  size_card_height: 95px
  font_primary: 15px
  font_secondary: 12px
  font_badge: 11px
styles:
  card:
    - "--config-icon-size": "[[[ return variables.size_icon ]]]"
    - "--config-shape-size": "[[[ return variables.size_shape ]]]"
    - "--config-card-height": "[[[ return variables.size_card_height ]]]"
    - "--config-font-primary": "[[[ return variables.font_primary ]]]"
    - "--config-font-secondary": "[[[ return variables.font_secondary ]]]"
    - "--config-font-badge": "[[[ return variables.font_badge ]]]"
    - height: var(--config-card-height) !important
    - padding: 0px !important
    - overflow: hidden
    - position: relative
    - transition: all 0.5s ease
  grid:
    - padding: 12px 16px
    - height: 100%
    - box-sizing: border-box
    - grid-template-areas: "\"i n\" \"i l\""
    - grid-template-columns: var(--config-shape-size) 1fr
    - grid-template-rows: auto auto
    - align-content: center
    - gap: 0px 12px
    - position: relative
  icon:
    - width: var(--config-icon-size)
    - height: var(--config-icon-size)
    - color: var(--primary-text-color)
    - z-index: 1
    - animation: var(--appliance-anim-shake) !important
    - transform-origin: 50% 60%
  img_cell:
    - width: var(--config-shape-size)
    - height: var(--config-shape-size)
    - border-radius: 50%
    - border: 1px solid var(--divider-color) !important
    - background: rgba(128, 128, 128, 0.1) !important
    - position: relative
    - overflow: hidden !important
    - justify-self: start
  name:
    - justify-self: start
    - font-size: var(--config-font-primary)
    - font-weight: 500
    - align-self: end
    - margin-bottom: 2px
    - position: relative
  label:
    - justify-self: start
    - font-size: var(--config-font-secondary)
    - opacity: 0.7
    - align-self: start
    - margin-top: 2px
    - position: relative
  custom_fields:
    badge1:
      - position: absolute
      - top: 10px
      - right: 10px
      - background: rgba(var(--appliance-color), 0.15)
      - color: rgb(var(--appliance-color))
      - border: 1px solid rgba(var(--appliance-color), 0.3)
      - padding: 2px 10px
      - border-radius: 12px
      - font-size: var(--config-font-badge)
      - font-weight: 600
      - text-transform: uppercase
      - letter-spacing: 0.5px
      - white-space: nowrap
      - z-index: 1
      - transition: all 0.5s ease
    badge2:
      - position: absolute
      - top: 38px
      - right: 10px
      - padding: 4px 8px
      - font-size: 10px
      - letter-spacing: 0.5px
      - white-space: nowrap
      - opacity: 0.9
      - text-transform: uppercase
      - font-weight: 500
      - z-index: 5
      - transition: all 0.5s ease
    bar:
      - position: absolute
      - bottom: 0
      - left: 0
      - height: 3.5px
      - width: var(--appliance-level)
      - background: rgb(var(--appliance-color))
      - box-shadow: 0 0 10px rgb(var(--appliance-color))
      - transition: width 0.5s ease
tap_action:
  action: more-info
label: |
  [[[ return entity ? entity.state : 'Entity Setup Required'; ]]]
icon: mdi:dishwasher
custom_fields:
  badge1: " "
  badge2: " "
  bar: " "
extra_styles: |
  [[[
    let ent_progress = variables.sensor_progress;
    let ent_timerem  = variables.sensor_time_remaining;
    let ent_power    = variables.sensor_power; 
    let ent_percent  = variables.sensor_percentage;
    let max_time     = variables.max_time;

    // Safely grab variables. If missing in YAML, falls back to empty strings to prevent crashes.
    let state_idle    = (variables.state_idle || '').split(',').map(s => s.trim().toLowerCase());
    let state_running = (variables.state_running || '').split(',').map(s => s.trim().toLowerCase());
    let state_drying  = (variables.state_drying || '').split(',').map(s => s.trim().toLowerCase());
    let state_done    = (variables.state_done || '').split(',').map(s => s.trim().toLowerCase());

    let status = states[ent_progress] ? String(states[ent_progress].state) : 'unknown';

    let _s = status.trim().toLowerCase();
    if (/^\d+$/.test(_s)) {
        if (state_idle.includes(_s))         status = state_idle.find(s => !/^\d+$/.test(s)) || status;
        else if (state_running.includes(_s)) status = state_running.find(s => !/^\d+$/.test(s)) || status;
        else if (state_drying.includes(_s))  status = state_drying.find(s => !/^\d+$/.test(s)) || status;
        else if (state_done.includes(_s))    status = state_done.find(s => !/^\d+$/.test(s)) || status;
    }

    let status_clean = status.replace(/[-_]/g, ' ').replace(/\b\w/g, c => c.toUpperCase());
    let s_lower = status.toLowerCase();
    
    let is_idle    = state_idle.includes(s_lower);
    let is_running = state_running.includes(s_lower);
    let is_drying  = state_drying.includes(s_lower);
    let is_done    = state_done.includes(s_lower);

    let raw_val = states[ent_timerem] ? states[ent_timerem].state.trim() : '0';
    let uom = states[ent_timerem] && states[ent_timerem].attributes ? states[ent_timerem].attributes.unit_of_measurement : '';
    let time_rem = 0;

    if (raw_val.includes('-') && raw_val.includes(':')) {
        let end_ts = new Date(raw_val);
        let now = new Date();
        time_rem = end_ts > now ? Math.floor((end_ts - now) / 60000) : 0;
    } else if (raw_val.includes(':')) {
        let parts = raw_val.split(':');
        if (parts.length === 3) time_rem = (parseInt(parts[0]) * 60) + parseInt(parts[1]);
        else if (parts.length === 2) time_rem = (parseInt(parts[0]) * 60) + parseInt(parts[1]);
    } else {
        let parsed_val = parseFloat(raw_val) || 0;
        let uom_lower = uom ? uom.toLowerCase() : '';

        if (uom_lower === 'h' || uom_lower === 'hours') {
            time_rem = Math.floor(parsed_val * 60); 
        } else if (uom_lower === 'm' || uom_lower === 'min' || uom_lower === 'minutes') {
            time_rem = Math.floor(parsed_val); 
        } else {
            if (parsed_val > 0 && parsed_val <= 10 && raw_val.includes('.')) {
                time_rem = Math.floor(parsed_val * 60); 
            } else {
                time_rem = Math.floor(parsed_val);
            }
        }
    }
    time_rem = Math.max(0, time_rem);

    let raw_percent_str = states[ent_percent] ? states[ent_percent].state.trim() : '';
    let raw_percent = (raw_percent_str !== '' && raw_percent_str !== 'unknown') ? parseFloat(raw_percent_str) : -1;
    let raw_power = states[ent_power] ? parseFloat(states[ent_power].state) : NaN;
    let power_text = !isNaN(raw_power) ? Math.round(raw_power) + 'W' : '';

    let hours = Math.floor(time_rem / 60);
    let mins = time_rem % 60;
    let time_formatted = (time_rem > 0 && !is_idle) ? `${hours}h ${mins.toString().padStart(2, '0')}m` : '';

    let progress = 0; 
    if (is_idle) {
        progress = 0; 
    } else {
        if (raw_percent >= 0) {
            progress = parseInt(raw_percent);
        } else {
            let safe_max = Math.max(parseFloat(max_time), time_rem);
            progress = Math.max(5, Math.floor(((safe_max - time_rem) / safe_max) * 100));
        }
    }
    progress = Math.max(0, Math.min(100, progress));

    let color = '158, 158, 158'; 
    let anim_type = 'none';
    let icon_shake = 'none';
    let wave_anim = 'none';
    let overlay_img = 'none';

    if (is_drying) {
      color = '255, 152, 0'; 
      anim_type = 'steam-rise 2s ease-in-out infinite'; 
      wave_anim = 'wave 4s linear infinite'; 
      overlay_img = 'linear-gradient(0deg, transparent, rgba(255,255,255,0.5), transparent)';
    } else if (is_done) {
      color = '76, 175, 80'; 
      anim_type = 'sparkle 2s infinite'; 
      wave_anim = 'wave 4s linear infinite'; 
      overlay_img = 'radial-gradient(circle, rgba(255,255,255,0.8) 10%, transparent 60%)';
    } else if (is_running) {
      color = '33, 150, 243'; 
      anim_type = 'bubbles 1s linear infinite'; 
      icon_shake = 'shake 0.8s ease-in-out infinite'; 
      wave_anim = 'wave 4s linear infinite'; 
      overlay_img = 'radial-gradient(2px 2px at 20% 80%, white, transparent), radial-gradient(2px 2px at 50% 70%, white, transparent)';
    }

    let ent_door = variables.sensor_door;
    let door_state = (ent_door && states[ent_door]) ? states[ent_door].state.toLowerCase() : null;
    
    let corner_color = color; 
    let corner_display = 'none'; // Default to hidden

    if (ent_door && door_state && door_state !== 'unknown' && door_state !== 'unavailable') {
        corner_display = 'block';
        let is_open = (door_state === 'on' || door_state === 'open');
        if (is_open) {
            corner_color = '244, 67, 54'; // Red when Open
        }
    }

    let badge1 = [status_clean, power_text].filter(Boolean).join(' • ');

    let badge2 = time_formatted;
    let b2_bg = `rgba(${color}, 0.15)`;
    let b2_border = `1px solid rgba(128,128,128, 0.2)`;
    let b2_br = `2px solid rgb(${color})`;

    return `
      #card {
        --appliance-color: ${color};
        --appliance-level: ${progress}%;
        --appliance-anim-overlay: ${anim_type};
        --appliance-anim-shake: ${icon_shake};
        --appliance-anim-wave: ${wave_anim};
        --appliance-overlay-bg: ${overlay_img};
        --door-corner-color: rgb(${corner_color});
        --door-corner-display: ${corner_display};
      }

      #card::after {
        content: '';
        display: var(--door-corner-display);
        position: absolute;
        top: -0.5px;
        left: -0.5px;
        opacity: 0.7;
        width: 15px;
        height: 15px;
        border-top: 5px solid var(--door-corner-color);
        border-left: 5px solid var(--door-corner-color);
        border-top-left-radius: var(--ha-card-border-radius, 12px);
        pointer-events: none;
        transition: border-color 0.5s ease;
      }

      #badge1::before { content: "${badge1}"; } 

      #badge2 {
        display: ${badge2 ? 'block' : 'none'};
        background: ${b2_bg};
        color: var(--primary-text-color, #fff);
        border-top: ${b2_border};
        border-bottom: ${b2_border};
        border-left: ${b2_border};
        border-left: ${b2_br};
        border-radius: 6px !important;
      }
      #badge2::before { content: "${badge2}"; }

      #img-cell::before {
        content: ''; position: absolute; left: -50%; width: 200%; height: 200%;
        top: calc(100% - var(--appliance-level)); background: rgba(var(--appliance-color), 0.6) !important;
        border-radius: 40%; animation: var(--appliance-anim-wave) !important;
        transition: top 0.5s ease; z-index: 1;
        display: ${wave_anim === 'none' ? 'none' : 'block'};
      }

      #img-cell::after {
        content: ''; position: absolute; inset: 0; background-image: var(--appliance-overlay-bg);
        background-size: 100% 100%; animation: var(--appliance-anim-overlay) !important; z-index: 1;
        display: ${anim_type === 'none' ? 'none' : 'block'};
      }

      @keyframes wave { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
      @keyframes shake { 0%, 100% { transform: rotate(0deg); } 25% { transform: rotate(5deg) translateY(-1px); } 75% { transform: rotate(-5deg) translateY(1px); } }
      @keyframes bubbles { 0% { transform: translateY(10px); opacity: 0; } 50% { opacity: 1; } 100% { transform: translateY(-20px); opacity: 0; } }
      @keyframes steam-rise { 0% { opacity: 0; transform: translateY(5px); } 50% { opacity: 0.8; } 100% { opacity: 0; transform: translateY(-10px); } }
      @keyframes sparkle { 0%, 100% { opacity: 0.3; transform: scale(0.9); } 50% { opacity: 1; transform: scale(1.1); } }
    `;
  ]]]

```
</details>

<details>
<summary><strong>2 - Smart Washing Machine</summary>

```yaml
type: custom:button-card
entity: sensor.smart_washer_status
name: Smart Washer
show_state: false
show_label: true
variables:
  sensor_status: sensor.smart_washer_status
  sensor_progress: sensor.smart_washer_progress
  sensor_time_remaining: sensor.smart_washer_time_remaining
  sensor_power: sensor.smart_washer_power
  sensor_percentage: sensor.smart_washer_percentage
  sensor_door: binary_sensor.smart_washer_door
  max_time: 150
  state_idle: idle, off, standby, unknown, unavailable
  state_running: wash, washing, rinse, rinsing, pre-wash, soak
  state_spinning: spin, spinning
  state_drying: dry, drying
  state_done: finished, complete, end
  size_icon: 45px
  size_shape: 65px
  size_card_height: 95px
  font_primary: 15px
  font_secondary: 12px
  font_badge: 11px
styles:
  icon:
    - width: var(--config-icon-size)
    - height: var(--config-icon-size)
    - color: var(--primary-text-color)
    - z-index: 1
    - animation: var(--appliance-anim-shake) !important
    - transform-origin: 50% 50%
  img_cell:
    - width: var(--config-shape-size)
    - height: var(--config-shape-size)
    - border-radius: 50%
    - border: 1px solid var(--divider-color) !important
    - background: rgba(128, 128, 128, 0.1) !important
    - position: relative
    - overflow: hidden !important
    - justify-self: start
  card:
    - "--config-icon-size": "[[[ return variables.size_icon ]]]"
    - "--config-shape-size": "[[[ return variables.size_shape ]]]"
    - "--config-card-height": "[[[ return variables.size_card_height ]]]"
    - "--config-font-primary": "[[[ return variables.font_primary ]]]"
    - "--config-font-secondary": "[[[ return variables.font_secondary ]]]"
    - "--config-font-badge": "[[[ return variables.font_badge ]]]"
    - height: var(--config-card-height) !important
    - padding: 0px !important
    - overflow: hidden
    - position: relative
    - transition: all 0.5s ease
  grid:
    - padding: 12px 16px
    - height: 100%
    - box-sizing: border-box
    - grid-template-areas: "\"i n\" \"i l\""
    - grid-template-columns: var(--config-shape-size) 1fr
    - grid-template-rows: auto auto
    - align-content: center
    - gap: 0px 12px
    - position: relative
  name:
    - justify-self: start
    - font-size: var(--config-font-primary)
    - font-weight: 500
    - align-self: end
    - margin-bottom: 2px
    - position: relative
  label:
    - justify-self: start
    - font-size: var(--config-font-secondary)
    - opacity: 0.7
    - align-self: start
    - margin-top: 2px
    - position: relative
  custom_fields:
    badge1:
      - position: absolute
      - top: 10px
      - right: 10px
      - background: rgba(var(--appliance-color), 0.15)
      - color: rgb(var(--appliance-color))
      - border: 1px solid rgba(var(--appliance-color), 0.3)
      - padding: 2px 10px
      - border-radius: 12px
      - font-size: var(--config-font-badge)
      - font-weight: 600
      - text-transform: uppercase
      - letter-spacing: 0.5px
      - white-space: nowrap
      - z-index: 1
      - transition: all 0.5s ease
    badge2:
      - position: absolute
      - top: 38px
      - right: 10px
      - padding: 4px 8px
      - font-size: 10px
      - letter-spacing: 0.5px
      - white-space: nowrap
      - opacity: 0.9
      - text-transform: uppercase
      - font-weight: 500
      - z-index: 1
      - transition: all 0.5s ease
    bar:
      - position: absolute
      - bottom: 0
      - left: 0
      - height: 3.5px
      - width: var(--appliance-level)
      - background: rgb(var(--appliance-color))
      - box-shadow: 0 0 10px rgb(var(--appliance-color))
      - transition: width 0.5s ease
tap_action:
  action: more-info
label: |
  [[[ return entity ? entity.state : 'Entity Setup Required'; ]]]
icon: mdi:washing-machine
custom_fields:
  badge1: " "
  badge2: " "
  bar: " "
extra_styles: |
  [[[
    let ent_progress = variables.sensor_progress;
    let ent_timerem  = variables.sensor_time_remaining;
    let ent_power    = variables.sensor_power; 
    let ent_percent  = variables.sensor_percentage;
    let max_time     = variables.max_time;

    let state_idle     = (variables.state_idle || '').split(',').map(s => s.trim().toLowerCase());
    let state_running  = (variables.state_running || '').split(',').map(s => s.trim().toLowerCase());
    let state_spinning = (variables.state_spinning || '').split(',').map(s => s.trim().toLowerCase());
    let state_drying   = (variables.state_drying || '').split(',').map(s => s.trim().toLowerCase());
    let state_done     = (variables.state_done || '').split(',').map(s => s.trim().toLowerCase());

    let status = states[ent_progress] ? String(states[ent_progress].state) : 'unknown';

    let _s = status.trim().toLowerCase();
    if (/^\d+$/.test(_s)) {
        if (state_idle.includes(_s))          status = state_idle.find(s => !/^\d+$/.test(s)) || status;
        else if (state_running.includes(_s))  status = state_running.find(s => !/^\d+$/.test(s)) || status;
        else if (state_spinning.includes(_s)) status = state_spinning.find(s => !/^\d+$/.test(s)) || status;
        else if (state_drying.includes(_s))   status = state_drying.find(s => !/^\d+$/.test(s)) || status;
        else if (state_done.includes(_s))     status = state_done.find(s => !/^\d+$/.test(s)) || status;
    }

    let status_clean = status.replace(/[-_]/g, ' ').replace(/\b\w/g, c => c.toUpperCase());
    let s_lower = status.toLowerCase();

    let raw_val = states[ent_timerem] ? states[ent_timerem].state.trim() : '0';
    let uom = states[ent_timerem] && states[ent_timerem].attributes ? states[ent_timerem].attributes.unit_of_measurement : '';
    let time_rem = 0;

    if (raw_val.includes('-') && raw_val.includes(':')) {
        let end_ts = new Date(raw_val);
        let now = new Date();
        time_rem = end_ts > now ? Math.floor((end_ts - now) / 60000) : 0;
    } else if (raw_val.includes(':')) {
        let parts = raw_val.split(':');
        if (parts.length === 3) time_rem = (parseInt(parts[0]) * 60) + parseInt(parts[1]);
        else if (parts.length === 2) time_rem = (parseInt(parts[0]) * 60) + parseInt(parts[1]);
    } else {
        let parsed_val = parseFloat(raw_val) || 0;
        let uom_lower = uom ? uom.toLowerCase() : '';

        if (uom_lower === 'h' || uom_lower === 'hours') {
            time_rem = Math.floor(parsed_val * 60); 
        } else if (uom_lower === 'm' || uom_lower === 'min' || uom_lower === 'minutes') {
            time_rem = Math.floor(parsed_val); 
        } else {
            if (parsed_val > 0 && parsed_val <= 10 && raw_val.includes('.')) {
                time_rem = Math.floor(parsed_val * 60); 
            } else {
                time_rem = Math.floor(parsed_val);
            }
        }
    }
    time_rem = Math.max(0, time_rem);

    let raw_percent_str = states[ent_percent] ? states[ent_percent].state.trim() : '';
    let raw_percent = (raw_percent_str !== '' && raw_percent_str !== 'unknown') ? parseFloat(raw_percent_str) : -1;
    let raw_power = states[ent_power] ? parseFloat(states[ent_power].state) : NaN;
    let power_text = !isNaN(raw_power) ? Math.round(raw_power) + 'W' : '';
    
    let is_idle = state_idle.includes(s_lower);
    let hours = Math.floor(time_rem / 60);
    let mins = time_rem % 60;
    let time_formatted = (time_rem > 0 && !is_idle) ? `${hours}h ${mins.toString().padStart(2, '0')}m` : '';

    let progress = 0; 
    if (is_idle) {
        progress = 0; 
    } else {
        if (raw_percent >= 0) {
            progress = parseInt(raw_percent);
        } else {
            let safe_max = Math.max(parseFloat(max_time), time_rem);
            progress = Math.max(5, Math.floor(((safe_max - time_rem) / safe_max) * 100));
        }
    }
    progress = Math.max(0, Math.min(100, progress));

    let is_running  = state_running.includes(s_lower);
    let is_spinning = state_spinning.includes(s_lower);
    let is_drying   = state_drying.includes(s_lower);
    let is_done     = state_done.includes(s_lower);

    let color = '158, 158, 158'; 
    let anim_type = 'none';
    let icon_shake = 'none';
    let wave_anim = 'none';
    let overlay_img = 'none';

    if (is_drying) {
      color = '255, 152, 0'; 
      anim_type = 'steam-rise 2s ease-in-out infinite'; 
      wave_anim = 'wave 4s linear infinite'; 
      overlay_img = 'linear-gradient(0deg, transparent, rgba(255,255,255,0.5), transparent)';
    } else if (is_spinning) {
      color = '0, 170, 170';
      anim_type = 'none'; 
      icon_shake = 'washer-spin-smooth 0.8s linear infinite'; 
      wave_anim = 'wave 2s linear infinite'; 
      overlay_img = 'radial-gradient(circle, rgba(255,255,255,0.3) 10%, transparent 60%)';
    } else if (is_done) {
      color = '76, 175, 80'; 
      anim_type = 'sparkle 2s infinite'; 
      wave_anim = 'wave 4s linear infinite'; 
      overlay_img = 'radial-gradient(circle, rgba(255,255,255,0.8) 10%, transparent 60%)';
    } else if (is_running) {
      color = '33, 150, 243'; 
      anim_type = 'bubbles 1s linear infinite'; 
      icon_shake = 'shake 1.5s ease-in-out infinite'; 
      wave_anim = 'wave 4s linear infinite'; 
      overlay_img = 'radial-gradient(2px 2px at 20% 80%, white, transparent), radial-gradient(2px 2px at 50% 70%, white, transparent)';
    }

    // --- SMART ADAPTIVE CORNER LOGIC ---
    let ent_door = variables.sensor_door;
    let door_state = (ent_door && states[ent_door]) ? states[ent_door].state.toLowerCase() : null;
    
    let corner_color = color; 
    let corner_display = 'none'; // Default to hidden

    if (ent_door && door_state && door_state !== 'unknown' && door_state !== 'unavailable') {
        corner_display = 'block';
        let is_open = (door_state === 'on' || door_state === 'open');
        if (is_open) {
            corner_color = '244, 67, 54'; // Red when Open
        }
    }
    // -----------------------------------

    let badge1 = [status_clean, power_text].filter(Boolean).join(' • ');

    let badge2 = time_formatted;
    let b2_bg = `rgba(${color}, 0.15)`;
    let b2_border = `1px solid rgba(128,128,128, 0.2)`;
    let b2_br = `2px solid rgb(${color})`;

    return `
      #card {
        --appliance-color: ${color};
        --appliance-level: ${progress}%;
        --appliance-anim-overlay: ${anim_type};
        --appliance-anim-shake: ${icon_shake};
        --appliance-anim-wave: ${wave_anim};
        --appliance-overlay-bg: ${overlay_img};
        --door-corner-color: rgb(${corner_color});
        --door-corner-display: ${corner_display};
      }
      
      /* Rounded Adaptive Corner Accent */
      #card::after {
        content: '';
        display: var(--door-corner-display);
        position: absolute;
        top: -0.5px;
        left: -0.5px;
        opacity: 0.7;
        width: 15px;
        height: 15px;
        border-top: 5px solid var(--door-corner-color);
        border-left: 5px solid var(--door-corner-color);
        border-top-left-radius: var(--ha-card-border-radius, 12px);
        pointer-events: none;
        transition: border-color 0.5s ease;
      }

      #badge1::before { content: "${badge1}"; } 

      #badge2 {
        display: ${badge2 ? 'block' : 'none'};
        background: ${b2_bg};
        color: var(--primary-text-color, #fff);
        border-top: ${b2_border};
        border-bottom: ${b2_border};
        border-left: ${b2_border};
        border-left: ${b2_br};
        border-radius: 6px !important;
      }
      #badge2::before { content: "${badge2}"; }

      #img-cell::before {
        content: ''; position: absolute; left: -50%; width: 200%; height: 200%;
        top: calc(100% - var(--appliance-level)); background: rgba(var(--appliance-color), 0.6) !important;
        border-radius: 40%; animation: var(--appliance-anim-wave) !important;
        transition: top 0.5s ease; z-index: 1;
        display: ${wave_anim === 'none' ? 'none' : 'block'};
      }

      #img-cell::after {
        content: ''; position: absolute; inset: 0; background-image: var(--appliance-overlay-bg);
        background-size: 100% 100%; animation: var(--appliance-anim-overlay) !important; z-index: 1;
        display: ${anim_type === 'none' ? 'none' : 'block'};
      }

      @keyframes wave { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
      @keyframes shake { 0%, 100% { transform: rotate(0deg); } 25% { transform: rotate(5deg) translateY(-1px); } 75% { transform: rotate(-5deg) translateY(1px); } }
      @keyframes bubbles { 0% { transform: translateY(10px); opacity: 0; } 50% { opacity: 1; } 100% { transform: translateY(-20px); opacity: 0; } }
      @keyframes steam-rise { 0% { opacity: 0; transform: translateY(5px); } 50% { opacity: 0.8; } 100% { opacity: 0; transform: translateY(-10px); } }
      @keyframes sparkle { 0%, 100% { opacity: 0.3; transform: scale(0.9); } 50% { opacity: 1; transform: scale(1.1); } }
      @keyframes washer-spin-smooth {
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
      }
    `;
  ]]]

```
</details>

<details>
<summary><strong>3 - Smart Dryer</summary>

```yaml
type: custom:button-card
entity: sensor.smart_dryer_status
name: Smart Dryer
show_state: false
show_label: true
variables:
  sensor_status: sensor.smart_dryer_status
  sensor_progress: sensor.smart_dryer_progress
  sensor_time_remaining: sensor.smart_dryer_time_remaining
  sensor_power: sensor.smart_dryer_power
  sensor_percentage: sensor.smart_dryer_percentage
  sensor_door: binary_sensor.smart_dryer_door
  max_time: 150
  state_idle: idle, off, standby, unknown, unavailable
  state_drying: drying, tumble, dry, heat, heating, tumbling
  state_cooling: cooling, cool down, anti-crease, air fluff
  state_done: finished, complete, end
  size_icon: 45px
  size_shape: 65px
  size_card_height: 95px
  font_primary: 15px
  font_secondary: 12px
  font_badge: 11px
styles:
  icon:
    - width: var(--config-icon-size)
    - height: var(--config-icon-size)
    - color: var(--primary-text-color)
    - z-index: 1
    - animation: var(--appliance-anim-shake) !important
    - transform-origin: 50% 60%
  img_cell:
    - width: var(--config-shape-size)
    - height: var(--config-shape-size)
    - border-radius: 50%
    - border: 1px solid var(--divider-color) !important
    - background: rgba(128, 128, 128, 0.1) !important
    - position: relative
    - overflow: hidden !important
    - justify-self: start
  card:
    - "--config-icon-size": "[[[ return variables.size_icon ]]]"
    - "--config-shape-size": "[[[ return variables.size_shape ]]]"
    - "--config-card-height": "[[[ return variables.size_card_height ]]]"
    - "--config-font-primary": "[[[ return variables.font_primary ]]]"
    - "--config-font-secondary": "[[[ return variables.font_secondary ]]]"
    - "--config-font-badge": "[[[ return variables.font_badge ]]]"
    - height: var(--config-card-height) !important
    - padding: 0px !important
    - overflow: hidden
    - position: relative
    - transition: all 0.5s ease
  grid:
    - padding: 12px 16px
    - height: 100%
    - box-sizing: border-box
    - grid-template-areas: "\"i n\" \"i l\""
    - grid-template-columns: var(--config-shape-size) 1fr
    - grid-template-rows: auto auto
    - align-content: center
    - gap: 0px 12px
    - position: relative
  name:
    - justify-self: start
    - font-size: var(--config-font-primary)
    - font-weight: 500
    - align-self: end
    - margin-bottom: 2px
    - position: relative
  label:
    - justify-self: start
    - font-size: var(--config-font-secondary)
    - opacity: 0.7
    - align-self: start
    - margin-top: 2px
    - position: relative
  custom_fields:
    badge1:
      - position: absolute
      - top: 10px
      - right: 10px
      - background: rgba(var(--appliance-color), 0.15)
      - color: rgb(var(--appliance-color))
      - border: 1px solid rgba(var(--appliance-color), 0.3)
      - padding: 2px 10px
      - border-radius: 12px
      - font-size: var(--config-font-badge)
      - font-weight: 600
      - text-transform: uppercase
      - letter-spacing: 0.5px
      - white-space: nowrap
      - z-index: 1
      - transition: all 0.5s ease
    badge2:
      - position: absolute
      - top: 38px
      - right: 10px
      - padding: 4px 8px
      - font-size: 10px
      - letter-spacing: 0.5px
      - white-space: nowrap
      - opacity: 0.9
      - text-transform: uppercase
      - font-weight: 500
      - z-index: 1
      - transition: all 0.5s ease
    bar:
      - position: absolute
      - bottom: 0
      - left: 0
      - height: 3.5px
      - width: var(--appliance-level)
      - background: rgb(var(--appliance-color))
      - box-shadow: 0 0 10px rgb(var(--appliance-color))
      - transition: width 0.5s ease
tap_action:
  action: more-info
label: |
  [[[ return entity ? entity.state : 'Entity Setup Required'; ]]]
icon: mdi:tumble-dryer
custom_fields:
  badge1: " "
  badge2: " "
  bar: " "
extra_styles: |
  [[[
    let ent_progress = variables.sensor_progress;
    let ent_timerem  = variables.sensor_time_remaining;
    let ent_power    = variables.sensor_power; 
    let ent_percent  = variables.sensor_percentage;
    let max_time     = variables.max_time;

    let state_idle    = (variables.state_idle || '').split(',').map(s => s.trim().toLowerCase());
    let state_drying  = (variables.state_drying || '').split(',').map(s => s.trim().toLowerCase());
    let state_cooling = (variables.state_cooling || '').split(',').map(s => s.trim().toLowerCase());
    let state_done    = (variables.state_done || '').split(',').map(s => s.trim().toLowerCase());

    let status = states[ent_progress] ? String(states[ent_progress].state) : 'unknown';

    let _s = status.trim().toLowerCase();
    if (/^\d+$/.test(_s)) {
        if (state_idle.includes(_s))         status = state_idle.find(s => !/^\d+$/.test(s)) || status;
        else if (state_drying.includes(_s))  status = state_drying.find(s => !/^\d+$/.test(s)) || status;
        else if (state_cooling.includes(_s)) status = state_cooling.find(s => !/^\d+$/.test(s)) || status;
        else if (state_done.includes(_s))    status = state_done.find(s => !/^\d+$/.test(s)) || status;
    }

    let status_clean = status.replace(/[-_]/g, ' ').replace(/\b\w/g, c => c.toUpperCase());
    let s_lower = status.toLowerCase();

    let raw_val = states[ent_timerem] ? states[ent_timerem].state.trim() : '0';
    let uom = states[ent_timerem] && states[ent_timerem].attributes ? states[ent_timerem].attributes.unit_of_measurement : '';
    let time_rem = 0;

    if (raw_val.includes('-') && raw_val.includes(':')) {
        let end_ts = new Date(raw_val);
        let now = new Date();
        time_rem = end_ts > now ? Math.floor((end_ts - now) / 60000) : 0;
    } else if (raw_val.includes(':')) {
        let parts = raw_val.split(':');
        if (parts.length === 3) time_rem = (parseInt(parts[0]) * 60) + parseInt(parts[1]);
        else if (parts.length === 2) time_rem = (parseInt(parts[0]) * 60) + parseInt(parts[1]);
    } else {
        let parsed_val = parseFloat(raw_val) || 0;
        let uom_lower = uom ? uom.toLowerCase() : '';
        if (uom_lower === 'h' || uom_lower === 'hours') time_rem = Math.floor(parsed_val * 60); 
        else if (uom_lower === 'm' || uom_lower === 'min' || uom_lower === 'minutes') time_rem = Math.floor(parsed_val); 
        else time_rem = (parsed_val > 0 && parsed_val <= 10 && raw_val.includes('.')) ? Math.floor(parsed_val * 60) : Math.floor(parsed_val);
    }
    time_rem = Math.max(0, time_rem);

    let raw_percent_str = states[ent_percent] ? states[ent_percent].state.trim() : '';
    let raw_percent = (raw_percent_str !== '' && raw_percent_str !== 'unknown') ? parseFloat(raw_percent_str) : -1;
    let raw_power = states[ent_power] ? parseFloat(states[ent_power].state) : NaN;
    let power_text = !isNaN(raw_power) ? Math.round(raw_power) + 'W' : '';

    let is_idle = state_idle.includes(s_lower);
    let hours = Math.floor(time_rem / 60);
    let mins = time_rem % 60;
    let time_formatted = (time_rem > 0 && !is_idle) ? `${hours}h ${mins.toString().padStart(2, '0')}m` : '';

    let progress = 0; 
    if (is_idle) {
        progress = 0; 
    } else {
        if (raw_percent >= 0) {
            progress = parseInt(raw_percent);
        } else {
            let safe_max = Math.max(parseFloat(max_time), time_rem);
            progress = Math.max(5, Math.floor(((safe_max - time_rem) / safe_max) * 100));
        }
    }
    progress = Math.max(0, Math.min(100, progress));

    let is_drying  = state_drying.includes(s_lower);
    let is_cooling = state_cooling.includes(s_lower);
    let is_done    = state_done.includes(s_lower);

    let color = '158, 158, 158'; 
    let anim_type = 'none';
    let icon_shake = 'none';
    let wave_anim = 'none';
    let overlay_img = 'none';

    if (is_drying) {
      color = '255, 152, 0'; 
      anim_type = 'steam-rise 2s ease-in-out infinite'; 
      wave_anim = 'wave 4s linear infinite'; 
      overlay_img = 'linear-gradient(0deg, transparent, rgba(255,255,255,0.4), transparent)';
    } else if (is_cooling) {
      color = '33, 150, 243'; 
      anim_type = 'breeze 3s ease-in-out infinite'; 
      icon_shake = 'wobble 2s ease-in-out infinite'; 
      wave_anim = 'wave 6s linear infinite'; 
      overlay_img = 'radial-gradient(circle, rgba(255,255,255,0.5) 0%, transparent 70%)';
    } else if (is_done) {
      color = '76, 175, 80'; 
      anim_type = 'sparkle 2s infinite'; 
      wave_anim = 'wave 4s linear infinite'; 
      overlay_img = 'radial-gradient(circle, rgba(255,255,255,0.8) 10%, transparent 60%)';
    }

    let ent_door = variables.sensor_door;
    let door_state = (ent_door && states[ent_door]) ? states[ent_door].state.toLowerCase() : null;
    
    let corner_color = color; 
    let corner_display = 'none';

    if (ent_door && door_state && door_state !== 'unknown' && door_state !== 'unavailable') {
        corner_display = 'block';
        let is_open = (door_state === 'on' || door_state === 'open');
        if (is_open) {
            corner_color = '244, 67, 54';
        }
    }

    let badge1 = [status_clean, power_text].filter(Boolean).join(' • ');
    let badge2 = time_formatted;

    return `
      #card {
        --appliance-color: ${color};
        --appliance-level: ${progress}%;
        --appliance-anim-overlay: ${anim_type};
        --appliance-anim-shake: ${icon_shake};
        --appliance-anim-wave: ${wave_anim};
        --appliance-overlay-bg: ${overlay_img};
        --door-corner-color: rgb(${corner_color});
        --door-corner-display: ${corner_display};
      }
      #card::after {
        content: '';
        display: var(--door-corner-display);
        position: absolute;
        top: -0.5px;
        left: -0.5px;
        opacity: 0.7;
        width: 15px;
        height: 15px;
        border-top: 5px solid var(--door-corner-color);
        border-left: 5px solid var(--door-corner-color);
        border-top-left-radius: var(--ha-card-border-radius, 12px);
        pointer-events: none;
        transition: border-color 0.5s ease;
      }
      
      #badge1::before { content: "${badge1}"; } 
      #badge2 {
        display: ${badge2 ? 'block' : 'none'};
        background: rgba(${color}, 0.15);
        color: var(--primary-text-color, #fff);
        border-top: 1px solid rgba(128,128,128, 0.2);
        border-bottom: 1px solid rgba(128,128,128, 0.2);
        border-left: 2px solid rgb(${color});
        border-radius: 6px !important;
      }
      #badge2::before { content: "${badge2}"; }
      #img-cell::before {
        content: ''; position: absolute; left: -50%; width: 200%; height: 200%;
        top: calc(100% - var(--appliance-level)); background: rgba(var(--appliance-color), 0.6) !important;
        border-radius: 40%; animation: var(--appliance-anim-wave) !important;
        transition: top 0.5s ease; z-index: 1;
        display: ${wave_anim === 'none' ? 'none' : 'block'};
      }
      #img-cell::after {
        content: ''; position: absolute; inset: 0; background-image: var(--appliance-overlay-bg);
        background-size: 100% 100%; animation: var(--appliance-anim-overlay) !important; z-index: 1;
        display: ${anim_type === 'none' ? 'none' : 'block'};
      }
      @keyframes wave { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
      @keyframes shake { 0%, 100% { transform: rotate(0deg); } 25% { transform: rotate(10deg) translateY(-2px); } 50% { transform: rotate(0deg); } 75% { transform: rotate(-10deg) translateY(2px); } }
      @keyframes wobble { 0%, 100% { transform: rotate(0deg); } 50% { transform: rotate(5deg); } }
      @keyframes steam-rise { 0% { opacity: 0; transform: translateY(10px) scale(0.9); } 50% { opacity: 0.6; } 100% { opacity: 0; transform: translateY(-20px) scale(1.1); } }
      @keyframes breeze { 0% { opacity: 0.2; transform: scale(0.95); } 50% { opacity: 0.5; transform: scale(1.05); } 100% { opacity: 0.2; transform: scale(0.95); } }
      @keyframes sparkle { 0%, 100% { opacity: 0.3; transform: scale(0.9); } 50% { opacity: 1; transform: scale(1.1); } }
    `;
  ]]]

```
</details>

<details>
<summary><strong>4 - Smart Combo Washing machine & Dryer</summary>

```yaml
type: custom:button-card
entity: sensor.smart_combo_status
name: Smart Combo
show_state: false
show_label: true
variables:
  sensor_status: sensor.smart_combo_status
  sensor_progress: sensor.smart_combo_progress
  sensor_time_remaining: sensor.smart_combo_time_remaining
  sensor_power: sensor.smart_combo_power
  sensor_percentage: sensor.smart_combo_percentage
  sensor_door: binary_sensor.smart_combo_door
  max_time: 150
  state_idle: idle, off, standby, unknown, unavailable
  state_washing: wash, washing, rinse, rinsing, pre-wash, soak
  state_spinning: spin, spinning, drain
  state_drying: dry, drying, tumble, tumbling
  state_cooling: cooling, cool down, anti-crease
  state_done: finished, complete, end
  size_icon: 45px
  size_shape: 65px
  size_card_height: 95px
  font_primary: 15px
  font_secondary: 12px
  font_badge: 11px
styles:
  icon:
    - width: var(--config-icon-size)
    - height: var(--config-icon-size)
    - color: var(--primary-text-color)
    - z-index: 1
    - animation: var(--appliance-anim-shake) !important
    - transform-origin: center center
  img_cell:
    - width: var(--config-shape-size)
    - height: var(--config-shape-size)
    - border-radius: 50%
    - border: 1px solid var(--divider-color) !important
    - background: rgba(128, 128, 128, 0.1) !important
    - position: relative
    - overflow: hidden !important
    - justify-self: start
  card:
    - "--config-icon-size": "[[[ return variables.size_icon ]]]"
    - "--config-shape-size": "[[[ return variables.size_shape ]]]"
    - "--config-card-height": "[[[ return variables.size_card_height ]]]"
    - "--config-font-primary": "[[[ return variables.font_primary ]]]"
    - "--config-font-secondary": "[[[ return variables.font_secondary ]]]"
    - "--config-font-badge": "[[[ return variables.font_badge ]]]"
    - height: var(--config-card-height) !important
    - padding: 0px !important
    - overflow: hidden
    - position: relative
    - transition: all 0.5s ease
  grid:
    - padding: 12px 16px
    - height: 100%
    - box-sizing: border-box
    - grid-template-areas: "\"i n\" \"i l\""
    - grid-template-columns: var(--config-shape-size) 1fr
    - grid-template-rows: auto auto
    - align-content: center
    - gap: 0px 12px
    - position: relative
  name:
    - justify-self: start
    - font-size: var(--config-font-primary)
    - font-weight: 500
    - align-self: end
    - margin-bottom: 2px
    - position: relative
  label:
    - justify-self: start
    - font-size: var(--config-font-secondary)
    - opacity: 0.7
    - align-self: start
    - margin-top: 2px
    - position: relative
  custom_fields:
    badge1:
      - position: absolute
      - top: 10px
      - right: 10px
      - background: rgba(var(--appliance-color), 0.15)
      - color: rgb(var(--appliance-color))
      - border: 1px solid rgba(var(--appliance-color), 0.3)
      - padding: 2px 10px
      - border-radius: 12px
      - font-size: var(--config-font-badge)
      - font-weight: 600
      - text-transform: uppercase
      - letter-spacing: 0.5px
      - white-space: nowrap
      - z-index: 1
      - transition: all 0.5s ease
    badge2:
      - position: absolute
      - top: 38px
      - right: 10px
      - padding: 4px 8px
      - font-size: 10px
      - letter-spacing: 0.5px
      - white-space: nowrap
      - opacity: 0.9
      - text-transform: uppercase
      - font-weight: 500
      - z-index: 1
      - transition: all 0.5s ease
    bar:
      - position: absolute
      - bottom: 0
      - left: 0
      - height: 3.5px
      - width: var(--appliance-level)
      - background: rgb(var(--appliance-color))
      - box-shadow: 0 0 10px rgb(var(--appliance-color))
      - transition: width 0.5s ease
tap_action:
  action: more-info
label: |
  [[[ return entity ? entity.state : 'Entity Setup Required'; ]]]
icon: mdi:washing-machine
custom_fields:
  badge1: " "
  badge2: " "
  bar: " "
extra_styles: |
  [[[
    let ent_progress = variables.sensor_progress;
    let ent_timerem  = variables.sensor_time_remaining;
    let ent_power    = variables.sensor_power; 
    let ent_percent  = variables.sensor_percentage;
    let max_time     = variables.max_time;

    let state_idle     = (variables.state_idle || '').split(',').map(s => s.trim().toLowerCase());
    let state_washing  = (variables.state_washing || '').split(',').map(s => s.trim().toLowerCase());
    let state_spinning = (variables.state_spinning || '').split(',').map(s => s.trim().toLowerCase());
    let state_drying   = (variables.state_drying || '').split(',').map(s => s.trim().toLowerCase());
    let state_cooling  = (variables.state_cooling || '').split(',').map(s => s.trim().toLowerCase());
    let state_done     = (variables.state_done || '').split(',').map(s => s.trim().toLowerCase());

    let status = states[ent_progress] ? String(states[ent_progress].state) : 'unknown';

    let _s = status.trim().toLowerCase();
    if (/^\d+$/.test(_s)) {
        if (state_idle.includes(_s))          status = state_idle.find(s => !/^\d+$/.test(s)) || status;
        else if (state_washing.includes(_s))  status = state_washing.find(s => !/^\d+$/.test(s)) || status;
        else if (state_spinning.includes(_s)) status = state_spinning.find(s => !/^\d+$/.test(s)) || status;
        else if (state_drying.includes(_s))   status = state_drying.find(s => !/^\d+$/.test(s)) || status;
        else if (state_cooling.includes(_s))  status = state_cooling.find(s => !/^\d+$/.test(s)) || status;
        else if (state_done.includes(_s))     status = state_done.find(s => !/^\d+$/.test(s)) || status;
    }

    let status_clean = status.replace(/[-_]/g, ' ').replace(/\b\w/g, c => c.toUpperCase());
    let s_lower = status.toLowerCase();

    let raw_val = states[ent_timerem] ? states[ent_timerem].state.trim() : '0';
    let uom = states[ent_timerem] && states[ent_timerem].attributes ? states[ent_timerem].attributes.unit_of_measurement : '';
    let time_rem = 0;

    if (raw_val.includes('-') && raw_val.includes(':')) {
        let end_ts = new Date(raw_val);
        let now = new Date();
        time_rem = end_ts > now ? Math.floor((end_ts - now) / 60000) : 0;
    } else if (raw_val.includes(':')) {
        let parts = raw_val.split(':');
        if (parts.length === 3) time_rem = (parseInt(parts[0]) * 60) + parseInt(parts[1]);
        else if (parts.length === 2) time_rem = (parseInt(parts[0]) * 60) + parseInt(parts[1]);
    } else {
        let parsed_val = parseFloat(raw_val) || 0;
        let uom_lower = uom ? uom.toLowerCase() : '';
        if (uom_lower === 'h' || uom_lower === 'hours') time_rem = Math.floor(parsed_val * 60); 
        else if (uom_lower === 'm' || uom_lower === 'min' || uom_lower === 'minutes') time_rem = Math.floor(parsed_val); 
        else time_rem = (parsed_val > 0 && parsed_val <= 10 && raw_val.includes('.')) ? Math.floor(parsed_val * 60) : Math.floor(parsed_val);
    }
    time_rem = Math.max(0, time_rem);

    let raw_percent_str = states[ent_percent] ? states[ent_percent].state.trim() : '';
    let raw_percent = (raw_percent_str !== '' && raw_percent_str !== 'unknown') ? parseFloat(raw_percent_str) : -1;
    let raw_power = states[ent_power] ? parseFloat(states[ent_power].state) : NaN;
    let power_text = !isNaN(raw_power) ? Math.round(raw_power) + 'W' : '';

    let is_idle = state_idle.includes(s_lower);
    let hours = Math.floor(time_rem / 60);
    let mins = time_rem % 60;
    let time_formatted = (time_rem > 0 && !is_idle) ? `${hours}h ${mins.toString().padStart(2, '0')}m` : '';

    let progress = 0; 
    if (is_idle) {
        progress = 0; 
    } else {
        if (raw_percent >= 0) {
            progress = parseInt(raw_percent);
        } else {
            let safe_max = Math.max(parseFloat(max_time), time_rem);
            progress = Math.max(5, Math.floor(((safe_max - time_rem) / safe_max) * 100));
        }
    }
    progress = Math.max(0, Math.min(100, progress));

    let is_washing  = state_washing.includes(s_lower);
    let is_spinning = state_spinning.includes(s_lower);
    let is_drying   = state_drying.includes(s_lower);
    let is_cooling  = state_cooling.includes(s_lower);
    let is_done     = state_done.includes(s_lower);

    let color = '158, 158, 158'; 
    let anim_type = 'none';
    let icon_shake = 'none';
    let wave_anim = 'none';
    let overlay_img = 'none';

    if (is_drying) {
      color = '255, 152, 0'; 
      anim_type = 'steam-rise 2s ease-in-out infinite'; 
      wave_anim = 'wave 4s linear infinite'; 
      overlay_img = 'linear-gradient(0deg, transparent, rgba(255,255,255,0.4), transparent)';
    } else if (is_cooling) {
      color = '33, 150, 243'; 
      anim_type = 'breeze 3s ease-in-out infinite'; 
      icon_shake = 'wobble 2s ease-in-out infinite'; 
      wave_anim = 'wave 6s linear infinite'; 
      overlay_img = 'radial-gradient(circle, rgba(255,255,255,0.5) 0%, transparent 70%)';
    } else if (is_spinning) {
      color = '0, 170, 170';
      icon_shake = 'washer-spin-smooth 0.8s linear infinite'; 
      wave_anim = 'wave 2s linear infinite'; 
      overlay_img = 'radial-gradient(circle, rgba(255,255,255,0.3) 10%, transparent 60%)';
    } else if (is_washing) {
      color = '33, 150, 243'; 
      anim_type = 'bubbles 1s linear infinite'; 
      icon_shake = 'shake 1.5s ease-in-out infinite'; 
      wave_anim = 'wave 4s linear infinite'; 
      overlay_img = 'radial-gradient(2px 2px at 20% 80%, white, transparent), radial-gradient(2px 2px at 50% 70%, white, transparent)';
    } else if (is_done) {
      color = '76, 175, 80'; 
      anim_type = 'sparkle 2s infinite'; 
      wave_anim = 'wave 4s linear infinite'; 
      overlay_img = 'radial-gradient(circle, rgba(255,255,255,0.8) 10%, transparent 60%)';
    }

    let ent_door = variables.sensor_door;
    let door_state = (ent_door && states[ent_door]) ? states[ent_door].state.toLowerCase() : null;
    
    let corner_color = color; 
    let corner_display = 'none';

    if (ent_door && door_state && door_state !== 'unknown' && door_state !== 'unavailable') {
        corner_display = 'block';
        let is_open = (door_state === 'on' || door_state === 'open');
        if (is_open) {
            corner_color = '244, 67, 54';
        }
    }

    let badge1 = [status_clean, power_text].filter(Boolean).join(' • ');
    let badge2 = time_formatted;

    return `
      #card {
        --appliance-color: ${color};
        --appliance-level: ${progress}%;
        --appliance-anim-overlay: ${anim_type};
        --appliance-anim-shake: ${icon_shake};
        --appliance-anim-wave: ${wave_anim};
        --appliance-overlay-bg: ${overlay_img};
        --door-corner-color: rgb(${corner_color});
        --door-corner-display: ${corner_display};
      }
      #card::after {
        content: '';
        display: var(--door-corner-display);
        position: absolute;
        top: -0.5px;
        left: -0.5px;
        opacity: 0.7;
        width: 15px;
        height: 15px;
        border-top: 5px solid var(--door-corner-color);
        border-left: 5px solid var(--door-corner-color);
        border-top-left-radius: var(--ha-card-border-radius, 12px);
        pointer-events: none;
        transition: border-color 0.5s ease;
      }
      
      #badge1::before { content: "${badge1}"; } 
      #badge2 {
        display: ${badge2 ? 'block' : 'none'};
        background: rgba(${color}, 0.15);
        color: var(--primary-text-color, #fff);
        border-top: 1px solid rgba(128,128,128, 0.2);
        border-bottom: 1px solid rgba(128,128,128, 0.2);
        border-left: 2px solid rgb(${color});
        border-radius: 6px !important;
      }
      #badge2::before { content: "${badge2}"; }
      #img-cell::before {
        content: ''; position: absolute; left: -50%; width: 200%; height: 200%;
        top: calc(100% - var(--appliance-level)); background: rgba(var(--appliance-color), 0.6) !important;
        border-radius: 40%; animation: var(--appliance-anim-wave) !important;
        transition: top 0.5s ease; z-index: 1;
        display: ${wave_anim === 'none' ? 'none' : 'block'};
      }
      #img-cell::after {
        content: ''; position: absolute; inset: 0; background-image: var(--appliance-overlay-bg);
        background-size: 100% 100%; animation: var(--appliance-anim-overlay) !important; z-index: 1;
        display: ${anim_type === 'none' ? 'none' : 'block'};
      }
      @keyframes wave { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
      @keyframes shake { 0%, 100% { transform: rotate(0deg); } 25% { transform: rotate(5deg) translateY(-1px); } 75% { transform: rotate(-5deg) translateY(1px); } }
      @keyframes wobble { 0%, 100% { transform: rotate(0deg); } 50% { transform: rotate(5deg); } }
      @keyframes washer-spin-smooth { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
      @keyframes bubbles { 0% { transform: translateY(10px); opacity: 0; } 50% { opacity: 1; } 100% { transform: translateY(-20px); opacity: 0; } }
      @keyframes steam-rise { 0% { opacity: 0; transform: translateY(10px) scale(0.9); } 50% { opacity: 0.6; } 100% { opacity: 0; transform: translateY(-20px) scale(1.1); } }
      @keyframes breeze { 0% { opacity: 0.2; transform: scale(0.95); } 50% { opacity: 0.5; transform: scale(1.05); } 100% { opacity: 0.2; transform: scale(0.95); } }
      @keyframes sparkle { 0%, 100% { opacity: 0.3; transform: scale(0.9); } 50% { opacity: 1; transform: scale(1.1); } }
    `;
  ]]]

```
</details>

<details>
<summary><strong>5 - Smart Fridge</summary>

```yaml
type: custom:button-card
entity: sensor.smart_fridge_status
name: Smart Refrigerator
show_state: false
show_label: true
variables:
  sensor_status: sensor.smart_fridge_status
  sensor_door: binary_sensor.smart_fridge_door
  sensor_door2: ""
  sensor_temp_fridge: sensor.smart_fridge_temp_fridge
  sensor_temp_freezer: sensor.smart_fridge_temp_freezer
  sensor_power: sensor.smart_fridge_power
  max_power_w: 200
  max_temp_fridge: 6
  max_temp_freezer: -10
  state_cooling: cool, cooling, running, active
  state_super: super_cool, rapid, boost
  state_defrost: defrost, defrosting
tap_action:
  action: more-info
label: |
  [[[ return entity ? entity.state : 'Entity Setup Required'; ]]]
icon: |
  [[[ 
    let d1 = states[variables.sensor_door];
    let d2 = states[variables.sensor_door2];
    let d1_open = d1 && (d1.state === 'on' || d1.state === 'open');
    let d2_open = d2 && (d2.state === 'on' || d2.state === 'open');
    return (d1_open || d2_open) ? 'mdi:fridge-alert' : 'mdi:fridge'; 
  ]]]
custom_fields:
  bg1: " "
  bg2: " "
  badge1: " "
  badge2: " "
  bar: " "
  door_dash: " "
styles:
  card:
    - height: 95px !important
    - padding: 0px !important
    - overflow: hidden
    - position: relative
    - transition: box-shadow 1s ease, background 1s ease
  grid:
    - padding: 12px 16px
    - height: 100%
    - box-sizing: border-box
    - grid-template-areas: "\"i n\" \"i l\""
    - grid-template-columns: 65px 1fr
    - grid-template-rows: auto auto
    - align-content: center
    - gap: 0px 12px
    - position: relative
    - z-index: 2
  icon:
    - width: 45px
    - height: 45px
    - color: rgb(var(--appliance-color))
    - transform-origin: 50% 60%
    - animation: var(--appliance-icon-anim) !important
    - z-index: 3
  img_cell:
    - width: 65px
    - height: 65px
    - border-radius: 50% !important
    - background: rgba(var(--appliance-color), 0.1) !important
    - border: 1px solid rgba(var(--appliance-color), 0.3)
    - position: relative
    - overflow: visible !important
    - justify-self: start
    - z-index: 1
  name:
    - justify-self: start
    - font-size: 15px
    - font-weight: 500
    - align-self: end
    - margin-bottom: 2px
    - position: relative
    - z-index: 2
  label:
    - justify-self: start
    - font-size: 12px
    - opacity: 0.7
    - align-self: start
    - margin-top: 2px
    - position: relative
    - z-index: 2
  custom_fields:
    bg1:
      - position: absolute
      - inset: 0
      - pointer-events: none
      - z-index: 0
      - display: var(--appliance-bg-d1)
      - background-image: var(--appliance-bg-img1)
      - background-size: var(--appliance-bg-sz1)
      - background-repeat: var(--appliance-bg-rep1)
      - animation: var(--appliance-bg-anim1)
      - opacity: var(--appliance-bg-op1)
    bg2:
      - position: absolute
      - inset: 0
      - pointer-events: none
      - z-index: 0
      - display: var(--appliance-bg-d2)
      - background-image: var(--appliance-bg-img2)
      - background-size: var(--appliance-bg-sz2)
      - background-repeat: repeat
      - animation: var(--appliance-bg-anim2)
      - opacity: var(--appliance-bg-op2)
    badge1:
      - position: absolute
      - top: 10px
      - right: 10px
      - white-space: nowrap
      - padding: 3px 8px
      - font-size: 10px
      - letter-spacing: 0.5px
      - text-transform: uppercase
      - font-weight: 700
      - z-index: 1
      - transition: all 0.5s ease
    badge2:
      - position: absolute
      - top: 38px
      - right: 10px
      - white-space: nowrap
      - padding: 4px 8px
      - font-size: 10px
      - letter-spacing: 0.5px
      - text-transform: uppercase
      - font-weight: 500
      - z-index: 1
      - transition: all 0.5s ease
    bar:
      - position: absolute
      - bottom: 0
      - left: 0
      - height: 3px
      - width: var(--appliance-level)
      - background: rgb(var(--appliance-color))
      - box-shadow: 0 0 10px rgba(var(--appliance-color), 0.5)
      - transition: width 0.5s ease, background 0.5s ease
      - z-index: 1
    door_dash:
      - position: absolute
      - top: 50%
      - left: 0
      - transform: translateY(-50%)
      - opacity: 0.8
      - width: 4px
      - height: 26px
      - border-top-right-radius: 4px
      - border-bottom-right-radius: 4px
      - display: var(--door-dash-display)
      - background: rgb(var(--door-dash-color))
      - box-shadow: var(--door-dash-glow)
      - transition: background 0.4s ease, box-shadow 0.4s ease
      - z-index: 2
      - pointer-events: none
extra_styles: |
  [[[
    let ent_door1 = variables.sensor_door;
    let ent_door2 = variables.sensor_door2;
    let ent_temp_f = variables.sensor_temp_fridge;
    let ent_temp_z = variables.sensor_temp_freezer;
    let ent_power = variables.sensor_power; 
    
    let max_power_w = variables.max_power_w;
    let max_temp_f = variables.max_temp_fridge;
    let max_temp_z = variables.max_temp_freezer;

    let state_cooling = variables.state_cooling.split(',').map(s => s.trim().toLowerCase());
    let state_super = variables.state_super.split(',').map(s => s.trim().toLowerCase());
    let state_defrost = variables.state_defrost.split(',').map(s => s.trim().toLowerCase());

    let status = states[variables.sensor_status] ? states[variables.sensor_status].state.toLowerCase() : 'unknown';
    let status_clean = status.replace(/[-_]/g, ' ').replace(/\b\w/g, c => c.toUpperCase());
    
    let door1_val = states[ent_door1] ? states[ent_door1].state.toLowerCase() : 'unknown';
    let door2_val = states[ent_door2] ? states[ent_door2].state.toLowerCase() : 'unknown';
    
    let bad_states = ['unknown', 'unavailable', ''];
    let d1_valid = !bad_states.includes(door1_val);
    let d2_valid = !bad_states.includes(door2_val);
    
    let d1_open = d1_valid && (door1_val === 'on' || door1_val === 'open');
    let d2_open = d2_valid && (door2_val === 'on' || door2_val === 'open');
    let door_open = d1_open || d2_open;

    let raw_temp_f = states[ent_temp_f] ? states[ent_temp_f].state : '';
    let raw_temp_z = states[ent_temp_z] ? states[ent_temp_z].state : '';
    
    let t_f = !bad_states.includes(raw_temp_f) ? raw_temp_f + '°' : '';
    let t_z = !bad_states.includes(raw_temp_z) ? raw_temp_z + '°' : '';

    let val_f = parseFloat(raw_temp_f); if (isNaN(val_f)) val_f = -999;
    let val_z = parseFloat(raw_temp_z); if (isNaN(val_z)) val_z = -999;
    let alert_f = (val_f > max_temp_f) && (val_f !== -999);
    let alert_z = (val_z > max_temp_z) && (val_z !== -999);

    let raw_power = states[ent_power] ? parseFloat(states[ent_power].state) : NaN;
    let power_w = !isNaN(raw_power) ? Math.round(raw_power) : 0;
    let power_text = !isNaN(raw_power) ? power_w + 'W' : '';
    
    let calc_prog = Math.floor((power_w / max_power_w) * 100);
    let progress = Math.max(0, Math.min(calc_prog, 100));

    let has_alert = door_open || alert_f || alert_z;
    let is_cooling = state_cooling.includes(status);
    let is_super = state_super.includes(status);
    let is_defrost = state_defrost.includes(status);

    let color = '158, 158, 158'; let card_shadow = 'var(--ha-card-box-shadow, none)';
    let bg_d1 = 'none'; let bg_img1 = 'none'; let bg_sz1 = 'none'; let bg_anim1 = 'none'; let bg_op1 = '1'; let bg_rep1 = 'repeat';
    let bg_d2 = 'none'; let bg_img2 = 'none'; let bg_sz2 = 'none'; let bg_anim2 = 'none'; let bg_op2 = '1';
    let icon_anim = 'none'; let anim_frost = 'none'; let anim_drip = 'none';
    let frost_shadow = 'none'; let overlay_img = 'none';

    let snow_img_1 = `radial-gradient(circle at 20px 30px, white 2px, transparent 3px), radial-gradient(circle at 50px 160px, white 2px, transparent 3px), radial-gradient(circle at 90px 40px, white 2px, transparent 3px), radial-gradient(circle at 130px 80px, white 2px, transparent 3px), radial-gradient(circle at 160px 120px, white 2px, transparent 3px), radial-gradient(circle at 240px 300px, white 2px, transparent 3px), radial-gradient(circle at 280px 100px, white 2px, transparent 3px)`;
    let snow_img_2 = `radial-gradient(circle at 10px 10px, rgba(255,255,255,0.7) 1px, transparent 2px), radial-gradient(circle at 30px 90px, rgba(255,255,255,0.7) 1px, transparent 2px), radial-gradient(circle at 80px 50px, rgba(255,255,255,0.7) 1px, transparent 2px), radial-gradient(circle at 110px 190px, rgba(255,255,255,0.7) 1px, transparent 2px), radial-gradient(circle at 150px 100px, rgba(255,255,255,0.7) 1px, transparent 2px), radial-gradient(circle at 220px 250px, rgba(255,255,255,0.7) 1px, transparent 2px)`;
    let drop_img   = `radial-gradient(ellipse at center, rgba(255,152,0,0.5) 0%, transparent 60%), radial-gradient(ellipse at center, rgba(255,152,0,0.4) 0%, transparent 60%), radial-gradient(ellipse at center, rgba(255,152,0,0.5) 0%, transparent 60%), radial-gradient(ellipse at center, rgba(255,152,0,0.4) 0%, transparent 60%)`;

    if (door_open) {
        color = '244, 67, 54'; card_shadow = 'inset 0 0 50px rgba(244, 67, 54, 0.15)';
        icon_anim = 'shake-alert 0.5s ease-in-out infinite';
    } else if (is_super) {
        color = '0, 188, 212'; card_shadow = 'inset 0 0 60px rgba(0, 188, 212, 0.15)';
        bg_d1 = 'block'; bg_img1 = snow_img_1; bg_sz1 = '300px 400px'; bg_anim1 = 'snow-fall-1 8s linear infinite'; bg_op1 = '0.15'; bg_rep1 = 'repeat';
        bg_d2 = 'block'; bg_img2 = snow_img_2; bg_sz2 = '300px 300px'; bg_anim2 = 'snow-fall-2 4s linear infinite'; bg_op2 = '0.1';
        icon_anim = 'compressor-rumble 0.1s linear infinite';
        anim_frost = 'pulse-frost 1.5s ease-in-out infinite';
        frost_shadow = 'inset 0 0 25px 5px rgba(0, 188, 212, 0.6)';
    } else if (is_cooling) {
        color = '129, 212, 250'; card_shadow = 'inset 0 0 40px rgba(129, 212, 250, 0.1)';
        bg_d1 = 'block'; bg_img1 = snow_img_1; bg_sz1 = '300px 400px'; bg_anim1 = 'snow-fall-1 16s linear infinite'; bg_op1 = '0.08'; bg_rep1 = 'repeat';
        bg_d2 = 'block'; bg_img2 = snow_img_2; bg_sz2 = '300px 300px'; bg_anim2 = 'snow-fall-2 8s linear infinite'; bg_op2 = '0.05';
        icon_anim = 'compressor-rumble 0.3s linear infinite';
        anim_frost = 'pulse-frost 3s ease-in-out infinite';
        frost_shadow = 'inset 0 0 15px 2px rgba(129, 212, 250, 0.5)';
    } else if (is_defrost) {
        color = '255, 152, 0'; card_shadow = 'inset 0 0 40px rgba(255, 152, 0, 0.08)';
        bg_d1 = 'block'; bg_img1 = drop_img; bg_sz1 = '100% 100%'; bg_anim1 = 'accumulate-drip-card 4s ease-in infinite'; bg_op1 = '1'; bg_rep1 = 'no-repeat';
        anim_drip = 'accumulate-drip-icon 3s ease-in infinite';
        overlay_img = `radial-gradient(ellipse at center, rgba(255,193,7,0.8) 0%, transparent 60%), radial-gradient(ellipse at center, rgba(255,193,7,0.6) 0%, transparent 60%)`;
    }

    let d1_c = color;
    let corner_display = 'none';
    let dash_color = color;
    let dash_glow = 'none';
    let dash_display = 'none';

    if (d1_valid && d2_valid) {
        corner_display = 'block';
        dash_display = 'block';
        d1_c = d1_open ? '244, 67, 54' : color;
        dash_color = d2_open ? '244, 67, 54' : color;
        dash_glow = d2_open ? '2px 0 6px rgba(244, 67, 54, 0.6)' : 'none';
    } else if (d1_valid || d2_valid) {
        corner_display = 'block';
        let open = d1_valid ? d1_open : d2_open;
        d1_c = open ? '244, 67, 54' : color;
    }

    let c_cool = '33, 150, 243';
    let c_alert = '244, 67, 54';

    let badge1_text = '';
    if (d1_open && d2_open) badge1_text = '⚠️ DOORS OPEN';
    else if (d1_open || d2_open) badge1_text = '⚠️ DOOR OPEN';
    else badge1_text = [status_clean, power_text].filter(Boolean).join(' • ');

    let badge1 = badge1_text;
    let b1_c = door_open ? c_alert : color;
    let b1_bg = `rgba(${b1_c}, 0.15)`;
    let b1_border = `1px solid rgba(${b1_c}, 0.3)`;
    let b1_bl = `2px solid rgb(${b1_c})`;
    let b1_br = b1_border;
    let b1_color = `rgb(${b1_c})`;

    let badge2 = '';
    let b2_bg = 'transparent'; let b2_bl = 'none'; let b2_br = 'none'; let b2_border = 'none';
    if (t_f || t_z) {
        let f_str = alert_f ? `⚠️ ${t_f}` : t_f;
        let z_str = alert_z ? `⚠️ ${t_z}` : t_z;
        badge2 = [f_str, z_str].filter(Boolean).join(' | ');

        let c_f = alert_f ? c_alert : c_cool;
        let c_z = alert_z ? c_alert : c_cool;

        b2_border = `1px solid rgba(128,128,128, 0.2)`;
        if (t_f && t_z) {
            b2_bg = `linear-gradient(90deg, rgba(${c_f}, 0.15) 0%, rgba(${c_z}, 0.15) 100%)`;
            b2_bl = `2px solid rgb(${c_f})`;
            b2_br = `2px solid rgb(${c_z})`;
        } else if (t_f) {
            b2_bg = `rgba(${c_f}, 0.15)`;
            b2_bl = `2px solid rgb(${c_f})`;
            b2_br = b2_border;
        } else if (t_z) {
            b2_bg = `rgba(${c_z}, 0.15)`;
            b2_bl = b2_border;
            b2_br = `2px solid rgb(${c_z})`;
        }
    }

    return `
      #card {
        --appliance-color: ${color};
        --appliance-level: ${progress}%; 
        --appliance-bg-d1: ${bg_d1}; --appliance-bg-img1: ${bg_img1}; --appliance-bg-sz1: ${bg_sz1}; --appliance-bg-anim1: ${bg_anim1}; --appliance-bg-op1: ${bg_op1}; --appliance-bg-rep1: ${bg_rep1};
        --appliance-bg-d2: ${bg_d2}; --appliance-bg-img2: ${bg_img2}; --appliance-bg-sz2: ${bg_sz2}; --appliance-bg-anim2: ${bg_anim2}; --appliance-bg-op2: ${bg_op2};
        --appliance-icon-anim: ${icon_anim};
        --appliance-anim-frost: ${anim_frost};
        --appliance-anim-drip: ${anim_drip};
        --appliance-frost-shadow: ${frost_shadow};
        --appliance-overlay-bg: ${overlay_img};
        --door-corner-color: rgb(${d1_c});
        --door-corner-display: ${corner_display};
        --door-dash-color: ${dash_color};
        --door-dash-glow: ${dash_glow};
        --door-dash-display: ${dash_display};
        box-shadow: ${card_shadow} !important;
      }
      #card::after {
        content: '';
        display: var(--door-corner-display);
        position: absolute;
        top: -0.5px;
        left: -0.5px;
        opacity: 0.7;
        width: 15px;
        height: 15px;
        border-top: 5px solid var(--door-corner-color);
        border-left: 5px solid var(--door-corner-color);
        border-top-left-radius: var(--ha-card-border-radius, 12px);
        pointer-events: none;
        transition: border-color 0.5s ease;
        z-index: 1;
      }
      #badge1 {
        background: ${b1_bg};
        color: ${b1_color};
        border-top: ${b1_border};
        border-bottom: ${b1_border};
        border-left: ${b1_bl};
        border-right: ${b1_br};
        border-radius: 6px !important;
      }
      #badge1::before { content: "${badge1}"; }

      #badge2 {
        display: ${badge2 ? 'block' : 'none'};
        background: ${b2_bg};
        color: var(--primary-text-color, #fff);
        border-top: ${b2_border};
        border-bottom: ${b2_border};
        border-left: ${b2_bl};
        border-right: ${b2_br};
        border-radius: 6px !important;
      }
      #badge2::before { content: "${badge2}"; }

      #img-cell::before {
        content: ''; position: absolute; inset: 0; box-shadow: var(--appliance-frost-shadow);
        animation: var(--appliance-anim-frost) !important; z-index: 1; border-radius: 50%; pointer-events: none;
      }
      #img-cell::after {
        content: ''; position: absolute; inset: 0; background-image: var(--appliance-overlay-bg);
        background-repeat: no-repeat; animation: var(--appliance-anim-drip) !important; z-index: 1; 
        border-radius: 50%; pointer-events: none;
      }

      @keyframes snow-fall-1 { from { background-position: 0 0; } to { background-position: 0 400px; } }
      @keyframes snow-fall-2 { from { background-position: 0 0; } to { background-position: 0 300px; } }
      @keyframes accumulate-drip-card {
        0% { background-position: 15% 10%, 45% 20%, 75% 15%, 85% 30%; background-size: 0px 0px, 0px 0px, 0px 0px, 0px 0px; opacity: 0; }
        40% { background-position: 15% 30%, 45% 40%, 75% 35%, 85% 50%; background-size: 15px 25px, 20px 30px, 12px 20px, 25px 35px; opacity: 0.4; }
        80% { background-position: 15% 80%, 45% 85%, 75% 75%, 85% 90%; background-size: 15px 35px, 20px 40px, 12px 30px, 25px 45px; opacity: 0.2; }
        100% { background-position: 15% 100%, 45% 105%, 75% 95%, 85% 110%; background-size: 10px 40px, 15px 45px, 8px 35px, 20px 50px; opacity: 0; }
      }
      @keyframes pulse-frost { 0%, 100% { opacity: 0.4; transform: scale(0.95); } 50% { opacity: 0.8; transform: scale(1); } }
      @keyframes accumulate-drip-icon {
        0% { background-position: 30% 10%, 70% 20%; background-size: 0px 0px, 0px 0px; opacity: 0; }
        40% { background-position: 30% 30%, 70% 40%; background-size: 8px 12px, 12px 16px; opacity: 1; }
        80% { background-position: 30% 80%, 70% 90%; background-size: 8px 18px, 12px 22px; opacity: 0.8; }
        100% { background-position: 30% 100%, 70% 110%; background-size: 6px 20px, 10px 25px; opacity: 0; }
      }
      @keyframes compressor-rumble {
        0% { transform: translate(0, 0); } 25% { transform: translate(-1px, 0.5px); } 50% { transform: translate(1px, -0.5px); } 75% { transform: translate(-0.5px, 0.5px); } 100% { transform: translate(0, 0); }
      }
      @keyframes shake-alert {
        0%, 100% { transform: rotate(0deg); } 25% { transform: rotate(5deg) translateY(-1px); } 75% { transform: rotate(-5deg) translateY(1px); }
      }
    `;
  ]]]

```
</details>

---

# Cards (Dumb)

<details>
<summary><strong>1 - 
 Dishwasher (smart plug)</summary>

```yaml
type: custom:button-card
entity: binary_sensor.dishwasher_active_delay
name: Dumb Dishwasher
show_state: false
show_label: true
variables:
  ent_helper: binary_sensor.dishwasher_active_delay
  ent_switch: switch.smart_plug
  ent_power: sensor.smart_plug_power
  sensor_door: binary_sensor.dishwasher_door_contact
  thresh_heat: 1000
  thresh_active: 5
  size_icon: 45px
  size_shape: 65px
  size_card_height: 95px
  font_primary: 15px
  font_secondary: 13px
  font_badge: 11px
styles:
  card:
    - "--config-icon-size": "[[[ return variables.size_icon ]]]"
    - "--config-shape-size": "[[[ return variables.size_shape ]]]"
    - "--config-card-height": "[[[ return variables.size_card_height ]]]"
    - "--config-font-primary": "[[[ return variables.font_primary ]]]"
    - "--config-font-secondary": "[[[ return variables.font_secondary ]]]"
    - "--config-font-badge": "[[[ return variables.font_badge ]]]"
    - height: var(--config-card-height) !important
    - padding: 0px !important
    - overflow: hidden
    - position: relative
    - transition: all 0.5s ease
  grid:
    - padding: 12px 16px
    - height: 100%
    - box-sizing: border-box
    - grid-template-areas: "\"i n\" \"i l\""
    - grid-template-columns: var(--config-shape-size) 1fr
    - grid-template-rows: auto auto
    - align-content: center
    - gap: 0px 12px
    - position: relative
  icon:
    - width: var(--config-icon-size)
    - height: var(--config-icon-size)
    - color: white
    - z-index: 1
    - animation: var(--appliance-anim-shake) !important
    - transform-origin: 50% 50%
  img_cell:
    - width: var(--config-shape-size)
    - height: var(--config-shape-size)
    - border-radius: 50%
    - border: 1px solid rgba(255, 255, 255, 0.1) !important
    - background: rgba(255, 255, 255, 0.05) !important
    - position: relative
    - overflow: hidden !important
    - justify-self: start
  name:
    - justify-self: start
    - font-size: var(--config-font-primary)
    - font-weight: 500
    - align-self: end
    - margin-bottom: 2px
    - position: relative
  label:
    - justify-self: start
    - font-size: var(--config-font-secondary)
    - opacity: 0.7
    - align-self: start
    - margin-top: 2px
    - position: relative
  custom_fields:
    badge1:
      - position: absolute
      - top: 10px
      - right: 10px
      - background: rgba(var(--appliance-color), 0.15)
      - color: rgb(var(--appliance-color))
      - border: 1px solid rgba(var(--appliance-color), 0.3)
      - padding: 2px 10px
      - border-radius: 12px
      - font-size: var(--config-font-badge)
      - font-weight: 600
      - text-transform: uppercase
      - letter-spacing: 0.5px
      - white-space: nowrap
      - z-index: 1
    badge2:
      - position: absolute
      - top: 38px
      - right: 10px
      - padding: 4px 8px
      - font-size: 10px
      - letter-spacing: 0.5px
      - white-space: nowrap
      - opacity: 0.9
      - text-transform: uppercase
      - font-weight: 500
      - z-index: 1
    bar:
      - position: absolute
      - bottom: 0
      - left: 0
      - height: 3.5px
      - width: var(--appliance-level)
      - background: rgb(var(--appliance-color))
      - box-shadow: 0 0 10px rgb(var(--appliance-color))
      - transition: width 0.5s ease
tap_action:
  action: more-info
label: |
  [[[
    let ent = variables.ent_helper;
    let state = states[ent] ? states[ent].state : 'unknown';
    if (state === 'on') return 'Running';
    if (state === 'off') return 'Not Running';
    return state;
  ]]]
icon: mdi:dishwasher
custom_fields:
  badge1: " "
  badge2: " "
  bar: " "
extra_styles: |
  [[[
    let ent_switch = variables.ent_switch;
    let ent_power = variables.ent_power;
    let ent_helper = variables.ent_helper;
    let thresh_heat = variables.thresh_heat;
    let thresh_active = variables.thresh_active;

    let switch_state = states[ent_switch] ? states[ent_switch].state : 'unknown';
    
    let power_state = states[ent_power];
    let is_power_valid = power_state && !['unknown', 'unavailable', 'none'].includes(power_state.state.toLowerCase());
    let power = is_power_valid ? Math.round(parseFloat(power_state.state)) : 0;
    let power_text = is_power_valid ? ` • ${power}W` : '';

    let helper_obj = states[ent_helper];
    let has_helper = helper_obj && !['unknown', 'unavailable', 'none'].includes(helper_obj.state);
    let status_bin = has_helper ? helper_obj.state : (power > thresh_active ? 'on' : 'off');

    let time_str = '';
    let seconds = 0;

    if (status_bin === 'on' && switch_state === 'on') {
        if (has_helper && helper_obj.last_changed) {
            let start_time = new Date(helper_obj.last_changed);
            let now = new Date();
            seconds = Math.max(0, Math.floor((now - start_time) / 1000));
            let hours = Math.floor(seconds / 3600);
            let mins = Math.floor((seconds % 3600) / 60);
            time_str = seconds > 60 ? `${hours}h ${mins.toString().padStart(2, '0')}m` : 'Started';
        } else {
            time_str = 'Started';
        }
    }

    let status_text = 'Idle';
    let color = '158, 158, 158';
    let anim_type = 'none';
    let icon_shake = 'none';
    let wave_anim = 'none';
    let overlay_img = 'none';
    let level = 0;
    let badge1 = '';

    if (switch_state === 'off') {
        status_text = 'Plug Off';
        color = '244, 67, 54';
        badge1 = status_text;
    } else if (['unavailable', 'unknown'].includes(switch_state)) {
        status_text = 'Offline';
        color = '158, 158, 158';
        badge1 = status_text;
    } else if (status_bin === 'on') {
        if (power > thresh_heat) {
            status_text = 'Heating';
            color = '255, 152, 0';
            anim_type = 'steam-rise 2s ease-in-out infinite';
            overlay_img = 'linear-gradient(0deg, transparent, rgba(255,255,255,0.5), transparent)';
        } else {
            status_text = 'Washing';
            color = '33, 150, 243';
            anim_type = 'bubbles 1s linear infinite';
            overlay_img = 'radial-gradient(2px 2px at 20% 80%, white, transparent), radial-gradient(2px 2px at 50% 70%, white, transparent)';
            icon_shake = 'shake 0.8s ease-in-out infinite';
        }
        wave_anim = 'wave 4s linear infinite';
        
        let mins_elapsed = Math.floor(seconds / 60);
        level = Math.min(80, 10 + (Math.floor(mins_elapsed / 10) * 10));
        
        badge1 = `${status_text}${power_text}`;
    } else {
        status_text = 'Idle';
        color = '158, 158, 158';
        badge1 = `${status_text}${power_text}`;
    }

    let ent_door = variables.sensor_door;
    let door_state = (ent_door && states[ent_door]) ? states[ent_door].state.toLowerCase() : null;
    
    let corner_color = (switch_state === 'off') ? '158, 158, 158' : color; 
    let corner_display = 'none';

    if (ent_door && door_state && door_state !== 'unknown' && door_state !== 'unavailable') {
        corner_display = 'block';
        let is_open = (door_state === 'on' || door_state === 'open');
        if (is_open) {
            corner_color = '244, 67, 54';
        }
    }

    let b2_bg = `rgba(${color}, 0.15)`;
    let b2_border = `1px solid rgba(128,128,128, 0.2)`;
    let b2_br = `2px solid rgb(${color})`;

    return `
      #card {
        --appliance-color: ${color};
        --appliance-level: ${level}%;
        --appliance-anim-overlay: ${anim_type};
        --appliance-anim-shake: ${icon_shake};
        --appliance-anim-wave: ${wave_anim};
        --appliance-overlay-bg: ${overlay_img};
        --door-corner-color: rgb(${corner_color});
        --door-corner-display: ${corner_display};
      }
      #card::after {
        content: '';
        display: var(--door-corner-display);
        position: absolute;
        top: -0.5px;
        left: -0.5px;
        opacity: 0.7;
        width: 15px;
        height: 15px;
        border-top: 5px solid var(--door-corner-color);
        border-left: 5px solid var(--door-corner-color);
        border-top-left-radius: var(--ha-card-border-radius, 12px);
        pointer-events: none;
        transition: border-color 0.5s ease;
      }
      
      #badge1::before { content: "${badge1}"; } 
      #badge2 {
        display: ${time_str ? 'block' : 'none'};
        background: ${b2_bg};
        color: var(--primary-text-color, #fff);
        border-top: ${b2_border}; border-bottom: ${b2_border}; border-right: ${b2_border};
        border-left: ${b2_br}; border-radius: 6px !important;
      }
      #badge2::before { content: "${time_str}"; }
      #img-cell::before {
        content: ''; position: absolute; left: -50%; width: 200%; height: 200%;
        top: calc(100% - var(--appliance-level)); background: rgba(var(--appliance-color), 0.6) !important;
        border-radius: 40%; animation: var(--appliance-anim-wave) !important;
        transition: top 0.5s ease; z-index: 1;
        display: ${wave_anim === 'none' ? 'none' : 'block'};
      }
      #img-cell::after {
        content: ''; position: absolute; inset: 0; background-image: var(--appliance-overlay-bg);
        background-size: 100% 100%; animation: var(--appliance-anim-overlay) !important; z-index: 1;
        display: ${anim_type === 'none' ? 'none' : 'block'};
      }
      @keyframes wave { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
      @keyframes shake { 0%, 100% { transform: rotate(0deg); } 25% { transform: rotate(5deg) translateY(-1px); } 75% { transform: rotate(-5deg) translateY(1px); } }
      @keyframes bubbles { 0% { transform: translateY(10px); opacity: 0; } 50% { opacity: 1; } 100% { transform: translateY(-20px); opacity: 0; } }
      @keyframes steam-rise { 0% { opacity: 0; transform: translateY(5px); } 50% { opacity: 0.8; } 100% { opacity: 0; transform: translateY(-10px); } }
    `;
  ]]]

```
</details>

<details>
<summary><strong>Dumb Dishwasher (Helper/Template)</summary>

```yaml
  - binary_sensor:
      - name: "Dishwasher Active delay"
        unique_id: dishwasher_active_delay
        # Change the entity_id below to match your actual smart plug
        state: >
          {{ states('sensor.smart_plug_power')|float(0) > 5 }}
        delay_off: "00:05:00"
        device_class: running
        icon: mdi:dishwasher
```
</details>

---

<details>
<summary><strong>2 - Dumb Washing Machine (smart plug)</summary>

```yaml
type: custom:button-card
entity: binary_sensor.washing_machine_active_delay
name: Dumb Washer
show_state: false
show_label: true
variables:
  ent_helper: binary_sensor.washing_machine_active_delay
  ent_switch: switch.smart_plug
  ent_power: sensor.smart_plug_power
  sensor_door: binary_sensor.washer_door_contact
  thresh_heat: 1500
  thresh_spin: 150
  thresh_active: 5
  size_icon: 45px
  size_shape: 65px
  size_card_height: 95px
  font_primary: 15px
  font_secondary: 13px
  font_badge: 11px
styles:
  card:
    - "--config-icon-size": "[[[ return variables.size_icon ]]]"
    - "--config-shape-size": "[[[ return variables.size_shape ]]]"
    - "--config-card-height": "[[[ return variables.size_card_height ]]]"
    - "--config-font-primary": "[[[ return variables.font_primary ]]]"
    - "--config-font-secondary": "[[[ return variables.font_secondary ]]]"
    - "--config-font-badge": "[[[ return variables.font_badge ]]]"
    - height: var(--config-card-height) !important
    - padding: 0px !important
    - overflow: hidden
    - position: relative
    - transition: all 0.5s ease
  grid:
    - padding: 12px 16px
    - height: 100%
    - box-sizing: border-box
    - grid-template-areas: "\"i n\" \"i l\""
    - grid-template-columns: var(--config-shape-size) 1fr
    - grid-template-rows: auto auto
    - align-content: center
    - gap: 0px 12px
    - position: relative
  icon:
    - width: var(--config-icon-size)
    - height: var(--config-icon-size)
    - color: white
    - z-index: 1
    - animation: var(--appliance-anim-shake) !important
    - transform-origin: 50% 50%
  img_cell:
    - width: var(--config-shape-size)
    - height: var(--config-shape-size)
    - border-radius: 50%
    - border: 1px solid rgba(255, 255, 255, 0.1) !important
    - background: rgba(255, 255, 255, 0.05) !important
    - position: relative
    - overflow: hidden !important
    - justify-self: start
  name:
    - justify-self: start
    - font-size: var(--config-font-primary)
    - font-weight: 500
    - align-self: end
    - margin-bottom: 2px
    - position: relative
  label:
    - justify-self: start
    - font-size: var(--config-font-secondary)
    - opacity: 0.7
    - align-self: start
    - margin-top: 2px
    - position: relative
  custom_fields:
    badge1:
      - position: absolute
      - top: 10px
      - right: 10px
      - background: rgba(var(--appliance-color), 0.15)
      - color: rgb(var(--appliance-color))
      - border: 1px solid rgba(var(--appliance-color), 0.3)
      - padding: 2px 10px
      - border-radius: 12px
      - font-size: var(--config-font-badge)
      - font-weight: 600
      - text-transform: uppercase
      - letter-spacing: 0.5px
      - white-space: nowrap
      - z-index: 1
      - transition: all 0.5s ease
    badge2:
      - position: absolute
      - top: 38px
      - right: 10px
      - padding: 4px 8px
      - font-size: 10px
      - letter-spacing: 0.5px
      - white-space: nowrap
      - opacity: 0.9
      - text-transform: uppercase
      - font-weight: 500
      - z-index: 1
      - transition: all 0.5s ease
    bar:
      - position: absolute
      - bottom: 0
      - left: 0
      - height: 3.5px
      - width: var(--appliance-level)
      - background: rgb(var(--appliance-color))
      - box-shadow: 0 0 10px rgb(var(--appliance-color))
      - transition: width 0.5s ease
tap_action:
  action: more-info
label: |
  [[[
    let ent = variables.ent_helper;
    let state = states[ent] ? states[ent].state : 'unknown';
    if (state === 'on') return 'Running';
    if (state === 'off') return 'Not Running';
    return state;
  ]]]
icon: mdi:washing-machine
custom_fields:
  badge1: " "
  badge2: " "
  bar: " "
extra_styles: |
  [[[
    let ent_switch = variables.ent_switch;
    let ent_power = variables.ent_power;
    let ent_helper = variables.ent_helper;
    let thresh_heat = variables.thresh_heat;
    let thresh_spin = variables.thresh_spin;
    let thresh_active = variables.thresh_active;

    let switch_state = states[ent_switch] ? states[ent_switch].state : 'unknown';
    
    let power_state = states[ent_power];
    let is_power_valid = power_state && !['unknown', 'unavailable', 'none'].includes(power_state.state.toLowerCase());
    let power = is_power_valid ? Math.round(parseFloat(power_state.state)) : 0;
    let power_text = is_power_valid ? ` • ${power}W` : '';

    let helper_obj = states[ent_helper];
    let has_helper = helper_obj && !['unknown', 'unavailable', 'none'].includes(helper_obj.state);
    let status_bin = has_helper ? helper_obj.state : (power > thresh_active ? 'on' : 'off');

    let time_str = '';
    let seconds = 0;

    if (status_bin === 'on' && switch_state === 'on') {
        if (has_helper && helper_obj.last_changed) {
            let start_time = new Date(helper_obj.last_changed);
            let now = new Date();
            seconds = Math.max(0, Math.floor((now - start_time) / 1000));
            let hours = Math.floor(seconds / 3600);
            let mins = Math.floor((seconds % 3600) / 60);
            if (seconds > 60) {
                time_str = `${hours}h ${mins.toString().padStart(2, '0')}m`;
            } else {
                time_str = 'Started';
            }
        } else {
            time_str = 'Started';
        }
    }

    let status_text = 'Idle';
    let color = '158, 158, 158';
    let anim_type = 'none';
    let icon_shake = 'none';
    let wave_anim = 'none';
    let overlay_img = 'none';
    let level = 0;
    let badge1 = '';

    if (switch_state === 'off') {
        status_text = 'Plug Off';
        color = '244, 67, 54';
        badge1 = status_text;
    } else if (['unavailable', 'unknown'].includes(switch_state)) {
        status_text = 'Offline';
        color = '158, 158, 158';
        badge1 = status_text;
    } else if (status_bin === 'on') {
        
        if (power > thresh_heat) {
            status_text = 'Heating';
            color = '255, 87, 34'; // Orange for heat
            anim_type = 'bubbles 2s linear infinite';
            icon_shake = 'none'; // No intense shaking while heating
            overlay_img = 'radial-gradient(2px 2px at 20% 80%, white, transparent), radial-gradient(2px 2px at 50% 70%, white, transparent)';
        } else if (power > thresh_spin) {
            status_text = 'Spinning';
            color = '0, 170, 170';
            anim_type = 'bubbles 2s linear infinite';
            icon_shake = 'washer-spin-smooth 0.8s linear infinite';
            overlay_img = 'radial-gradient(2px 2px at 20% 80%, white, transparent), radial-gradient(2px 2px at 50% 70%, white, transparent)';
        } else {
            status_text = 'Washing';
            color = '33, 150, 243'; // Blue for washing
            anim_type = 'bubbles 2s linear infinite';
            overlay_img = 'radial-gradient(2px 2px at 20% 80%, white, transparent), radial-gradient(2px 2px at 50% 70%, white, transparent)';
            icon_shake = 'shake 2s ease-in-out infinite';
        }
        
        wave_anim = 'wave 4s linear infinite';
        
        let mins_elapsed = Math.floor(seconds / 60);
        let extra_level = Math.floor(mins_elapsed / 10) * 10;
        level = Math.min(80, 10 + extra_level);
        
        badge1 = `${status_text}${power_text}`;
    } else {
        status_text = 'Idle';
        color = '158, 158, 158';
        badge1 = `${status_text}${power_text}`;
    }

    let ent_door = variables.sensor_door;
    let door_state = (ent_door && states[ent_door]) ? states[ent_door].state.toLowerCase() : null;
    
    let corner_color = (switch_state === 'off') ? '158, 158, 158' : color; 
    let corner_display = 'none';

    if (ent_door && door_state && door_state !== 'unknown' && door_state !== 'unavailable') {
        corner_display = 'block';
        let is_open = (door_state === 'on' || door_state === 'open');
        if (is_open) {
            corner_color = '244, 67, 54';
        }
    }

    let b2_bg = `rgba(${color}, 0.15)`;
    let b2_border = `1px solid rgba(128,128,128, 0.2)`;
    let b2_br = `2px solid rgb(${color})`;

    return `
      #card {
        --appliance-color: ${color};
        --appliance-level: ${level}%;
        --appliance-anim-overlay: ${anim_type};
        --appliance-anim-shake: ${icon_shake};
        --appliance-anim-wave: ${wave_anim};
        --appliance-overlay-bg: ${overlay_img};
        --door-corner-color: rgb(${corner_color});
        --door-corner-display: ${corner_display};
      }
      
      #card::after {
        content: '';
        display: var(--door-corner-display);
        position: absolute;
        top: -0.5px;
        left: -0.5px;
        opacity: 0.7;
        width: 15px;
        height: 15px;
        border-top: 5px solid var(--door-corner-color);
        border-left: 5px solid var(--door-corner-color);
        border-top-left-radius: var(--ha-card-border-radius, 12px);
        pointer-events: none;
        transition: border-color 0.5s ease;
      }
      
      #badge1::before { content: "${badge1}"; } 

      #badge2 {
        display: ${time_str ? 'block' : 'none'};
        background: ${b2_bg};
        color: var(--primary-text-color, #fff);
        border-top: ${b2_border};
        border-bottom: ${b2_border};
        border-right: ${b2_border};
        border-left: ${b2_br};
        border-radius: 6px !important;
      }
      #badge2::before { content: "${time_str}"; }

      #img-cell::before {
        content: ''; position: absolute; left: -50%; width: 200%; height: 200%;
        top: calc(100% - var(--appliance-level)); background: rgba(var(--appliance-color), 0.6) !important;
        border-radius: 40%; animation: var(--appliance-anim-wave) !important;
        transition: top 0.5s ease; z-index: 1;
        display: ${wave_anim === 'none' ? 'none' : 'block'};
      }

      #img-cell::after {
        content: ''; position: absolute; inset: 0; background-image: var(--appliance-overlay-bg);
        background-size: 100% 100%; animation: var(--appliance-anim-overlay) !important; z-index: 1;
        display: ${anim_type === 'none' ? 'none' : 'block'};
      }

      @keyframes wave { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
      @keyframes shake { 0%, 100% { transform: rotate(0deg); } 25% { transform: rotate(5deg) translateY(-1px); } 75% { transform: rotate(-5deg) translateY(1px); } }
      @keyframes bubbles { 0% { transform: translateY(10px); opacity: 0; } 50% { opacity: 1; } 100% { transform: translateY(-20px); opacity: 0; } }
      @keyframes washer-spin-smooth {
        0% { transform: rotate(0deg) translate(0,0); }
        25% { transform: rotate(90deg) translate(0.5px, 0.5px); }
        50% { transform: rotate(180deg) translate(0,0); }
        75% { transform: rotate(270deg) translate(-0.5px, -0.5px); }
        100% { transform: rotate(360deg) translate(0,0); }
      }
    `;
  ]]]

```
</details>

<details>
<summary><strong>Dumb Washing Machine (Helper/Template)</summary>

```yaml
  - binary_sensor:
      - name: "Washing Machine Active delay"
        unique_id: washing_machine_active_delay
        # Change the entity_id below to match your actual smart plug
        state: >
          {{ states('sensor.smart_plug_power')|float(0) > 5 }}
        delay_off: "00:05:00"
        device_class: running
        icon: mdi:washing-machine
```
</details>

---

<details>
<summary><strong>3 - Dumb Dryer (smart plug)</summary>

```yaml
type: custom:button-card
entity: binary_sensor.dryer_active_delay
name: Dumb Dryer
show_state: false
show_label: true
variables:
  ent_helper: binary_sensor.dryer_active_delay
  ent_switch: switch.smart_plug
  ent_power: sensor.smart_plug_power
  sensor_door: binary_sensor.dryer_door_contact
  thresh_heat: 500
  thresh_active: 5
  size_icon: 45px
  size_shape: 65px
  size_card_height: 95px
  font_primary: 15px
  font_secondary: 13px
  font_badge: 11px
styles:
  card:
    - "--config-icon-size": "[[[ return variables.size_icon ]]]"
    - "--config-shape-size": "[[[ return variables.size_shape ]]]"
    - "--config-card-height": "[[[ return variables.size_card_height ]]]"
    - "--config-font-primary": "[[[ return variables.font_primary ]]]"
    - "--config-font-secondary": "[[[ return variables.font_secondary ]]]"
    - "--config-font-badge": "[[[ return variables.font_badge ]]]"
    - height: var(--config-card-height) !important
    - padding: 0px !important
    - overflow: hidden
    - position: relative
    - transition: all 0.5s ease
  grid:
    - padding: 12px 16px
    - height: 100%
    - box-sizing: border-box
    - grid-template-areas: "\"i n\" \"i l\""
    - grid-template-columns: var(--config-shape-size) 1fr
    - grid-template-rows: auto auto
    - align-content: center
    - gap: 0px 12px
    - position: relative
  icon:
    - width: var(--config-icon-size)
    - height: var(--config-icon-size)
    - color: white
    - z-index: 1
    - animation: var(--appliance-anim-shake) !important
    - transform-origin: 50% 50%
  img_cell:
    - width: var(--config-shape-size)
    - height: var(--config-shape-size)
    - border-radius: 50%
    - border: 1px solid rgba(255, 255, 255, 0.1) !important
    - background: rgba(255, 255, 255, 0.05) !important
    - position: relative
    - overflow: hidden !important
    - justify-self: start
  name:
    - justify-self: start
    - font-size: var(--config-font-primary)
    - font-weight: 500
    - align-self: end
    - margin-bottom: 2px
    - position: relative
  label:
    - justify-self: start
    - font-size: var(--config-font-secondary)
    - opacity: 0.7
    - align-self: start
    - margin-top: 2px
    - position: relative
  custom_fields:
    badge1:
      - position: absolute
      - top: 10px
      - right: 10px
      - background: rgba(var(--appliance-color), 0.15)
      - color: rgb(var(--appliance-color))
      - border: 1px solid rgba(var(--appliance-color), 0.3)
      - padding: 2px 10px
      - border-radius: 12px
      - font-size: var(--config-font-badge)
      - font-weight: 600
      - text-transform: uppercase
      - letter-spacing: 0.5px
      - white-space: nowrap
      - z-index: 1
    badge2:
      - position: absolute
      - top: 38px
      - right: 10px
      - padding: 4px 8px
      - font-size: 10px
      - letter-spacing: 0.5px
      - white-space: nowrap
      - opacity: 0.9
      - text-transform: uppercase
      - font-weight: 500
      - z-index: 1
    bar:
      - position: absolute
      - bottom: 0
      - left: 0
      - height: 3.5px
      - width: var(--appliance-level)
      - background: rgb(var(--appliance-color))
      - box-shadow: 0 0 10px rgb(var(--appliance-color))
      - transition: width 0.5s ease
tap_action:
  action: more-info
label: |
  [[[
    let ent = variables.ent_helper;
    let state = states[ent] ? states[ent].state : 'unknown';
    if (state === 'on') return 'Running';
    if (state === 'off') return 'Not Running';
    return state;
  ]]]
icon: mdi:tumble-dryer
custom_fields:
  badge1: " "
  badge2: " "
  bar: " "
extra_styles: |
  [[[
    let ent_switch = variables.ent_switch;
    let ent_power = variables.ent_power;
    let ent_helper = variables.ent_helper;
    let thresh_heat = variables.thresh_heat;
    let thresh_active = variables.thresh_active;

    let switch_state = states[ent_switch] ? states[ent_switch].state : 'unknown';
    
    let power_state = states[ent_power];
    let is_power_valid = power_state && !['unknown', 'unavailable', 'none'].includes(power_state.state.toLowerCase());
    let power = is_power_valid ? Math.round(parseFloat(power_state.state)) : 0;
    let power_text = is_power_valid ? ` • ${power}W` : '';

    let helper_obj = states[ent_helper];
    let has_helper = helper_obj && !['unknown', 'unavailable', 'none'].includes(helper_obj.state);
    let status_bin = has_helper ? helper_obj.state : (power > thresh_active ? 'on' : 'off');

    let time_str = '';
    let seconds = 0;

    if (status_bin === 'on' && switch_state === 'on') {
        if (has_helper && helper_obj.last_changed) {
            let start_time = new Date(helper_obj.last_changed);
            let now = new Date();
            seconds = Math.max(0, Math.floor((now - start_time) / 1000));
            let hours = Math.floor(seconds / 3600);
            let mins = Math.floor((seconds % 3600) / 60);
            time_str = seconds > 60 ? `${hours}h ${mins.toString().padStart(2, '0')}m` : 'Started';
        } else {
            time_str = 'Started';
        }
    }

    let status_text = 'Idle';
    let color = '158, 158, 158';
    let anim_type = 'none';
    let icon_shake = 'none';
    let wave_anim = 'none';
    let overlay_img = 'none';
    let level = 0;
    let badge1 = '';

    if (switch_state === 'off') {
        status_text = 'Plug Off';
        color = '244, 67, 54';
        badge1 = status_text;
    } else if (['unavailable', 'unknown'].includes(switch_state)) {
        status_text = 'Offline';
        color = '158, 158, 158';
        badge1 = status_text;
    } else if (status_bin === 'on') {
        if (power > thresh_heat) {
            status_text = 'Drying';
            color = '255, 152, 0';
            anim_type = 'steam-rise 2s ease-in-out infinite';
            overlay_img = 'linear-gradient(0deg, transparent, rgba(255,255,255,0.4), transparent)';
            icon_shake = 'none';
        } else {
            status_text = 'Tumbling';
            color = '33, 150, 243';
            anim_type = 'breeze 3s ease-in-out infinite';
            overlay_img = 'radial-gradient(circle, rgba(255,255,255,0.5) 0%, transparent 70%)';
            icon_shake = 'wobble 2s ease-in-out infinite';
        }
        wave_anim = 'wave 4s linear infinite';
        
        let mins_elapsed = Math.floor(seconds / 60);
        level = Math.min(80, 10 + (Math.floor(mins_elapsed / 10) * 10));
        
        badge1 = `${status_text}${power_text}`;
    } else {
        status_text = 'Idle';
        color = '158, 158, 158';
        badge1 = `${status_text}${power_text}`;
    }

    let ent_door = variables.sensor_door;
    let door_state = (ent_door && states[ent_door]) ? states[ent_door].state.toLowerCase() : null;
    
    let corner_color = (switch_state === 'off') ? '158, 158, 158' : color; 
    let corner_display = 'none';

    if (ent_door && door_state && door_state !== 'unknown' && door_state !== 'unavailable') {
        corner_display = 'block';
        let is_open = (door_state === 'on' || door_state === 'open');
        if (is_open) {
            corner_color = '244, 67, 54';
        }
    }

    let b2_bg = `rgba(${color}, 0.15)`;
    let b2_border = `1px solid rgba(128,128,128, 0.2)`;
    let b2_br = `2px solid rgb(${color})`;

    return `
      #card {
        --appliance-color: ${color};
        --appliance-level: ${level}%;
        --appliance-anim-overlay: ${anim_type};
        --appliance-anim-shake: ${icon_shake};
        --appliance-anim-wave: ${wave_anim};
        --appliance-overlay-bg: ${overlay_img};
        --door-corner-color: rgb(${corner_color});
        --door-corner-display: ${corner_display};
      }
      
      #card::after {
        content: '';
        display: var(--door-corner-display);
        position: absolute;
        top: -0.5px;
        left: -0.5px;
        opacity: 0.7;
        width: 15px;
        height: 15px;
        border-top: 5px solid var(--door-corner-color);
        border-left: 5px solid var(--door-corner-color);
        border-top-left-radius: var(--ha-card-border-radius, 12px);
        pointer-events: none;
        transition: border-color 0.5s ease;
      }
      
      #badge1::before { content: "${badge1}"; } 
      
      #badge2 {
        display: ${time_str ? 'block' : 'none'};
        background: ${b2_bg};
        color: var(--primary-text-color, #fff);
        border-top: ${b2_border}; border-bottom: ${b2_border}; border-right: ${b2_border};
        border-left: ${b2_br}; border-radius: 6px !important;
      }
      #badge2::before { content: "${time_str}"; }
      
      #img-cell::before {
        content: ''; position: absolute; left: -50%; width: 200%; height: 200%;
        top: calc(100% - var(--appliance-level)); background: rgba(var(--appliance-color), 0.6) !important;
        border-radius: 40%; animation: var(--appliance-anim-wave) !important;
        transition: top 0.5s ease; z-index: 1;
        display: ${wave_anim === 'none' ? 'none' : 'block'};
      }
      
      #img-cell::after {
        content: ''; position: absolute; inset: 0; background-image: var(--appliance-overlay-bg);
        background-size: 100% 100%; animation: var(--appliance-anim-overlay) !important; z-index: 1;
        display: ${anim_type === 'none' ? 'none' : 'block'};
      }
      
      @keyframes wave { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
      @keyframes wobble { 0%, 100% { transform: rotate(0deg); } 50% { transform: rotate(5deg); } }
      @keyframes steam-rise { 0% { opacity: 0; transform: translateY(10px) scale(0.9); } 50% { opacity: 0.6; } 100% { opacity: 0; transform: translateY(-20px) scale(1.1); } }
      @keyframes breeze { 0% { opacity: 0.2; transform: scale(0.95); } 50% { opacity: 0.5; transform: scale(1.05); } 100% { opacity: 0.2; transform: scale(0.95); } }
    `;
  ]]]

```
</details>

<details>
<summary><strong>Dumb Dryer (Helper/Template)</summary>

```yaml
  - binary_sensor:
      - name: "Dryer Active delay"
        unique_id: dryer_active_delay
        # Change the entity_id below to match your actual smart plug
        state: >
          {{ states('sensor.smart_plug_power')|float(0) > 5 }}
        delay_off: "00:05:00"
        device_class: running
        icon: mdi:tumble-dryer
```
</details>

---

<details>
<summary><strong>4 - Dumb Combo Washing machine & Dryer (smart plug)</summary>

```yaml
type: custom:button-card
entity: binary_sensor.combo_machine_active_delay
name: Dumb Combo
show_state: false
show_label: true
variables:
  ent_helper_run: binary_sensor.combo_machine_active_delay
  ent_helper_dry_mode: binary_sensor.combo_machine_drying_detector
  ent_switch: switch.smart_plug
  ent_power: sensor.smart_plug_power
  sensor_door: binary_sensor.combo_door_contact
  thresh_high: 800
  thresh_active: 5
  size_icon: 45px
  size_shape: 65px
  size_card_height: 95px
  font_primary: 15px
  font_secondary: 13px
  font_badge: 11px
styles:
  card:
    - "--config-icon-size": "[[[ return variables.size_icon ]]]"
    - "--config-shape-size": "[[[ return variables.size_shape ]]]"
    - "--config-card-height": "[[[ return variables.size_card_height ]]]"
    - "--config-font-primary": "[[[ return variables.font_primary ]]]"
    - "--config-font-secondary": "[[[ return variables.font_secondary ]]]"
    - "--config-font-badge": "[[[ return variables.font_badge ]]]"
    - height: var(--config-card-height) !important
    - padding: 0px !important
    - overflow: hidden
    - position: relative
    - transition: all 0.5s ease
  grid:
    - padding: 12px 16px
    - height: 100%
    - box-sizing: border-box
    - grid-template-areas: "\"i n\" \"i l\""
    - grid-template-columns: var(--config-shape-size) 1fr
    - grid-template-rows: auto auto
    - align-content: center
    - gap: 0px 12px
    - position: relative
  icon:
    - width: var(--config-icon-size)
    - height: var(--config-icon-size)
    - color: white
    - z-index: 1
    - animation: var(--appliance-anim-shake) !important
    - transform-origin: 50% 50%
  img_cell:
    - width: var(--config-shape-size)
    - height: var(--config-shape-size)
    - border-radius: 50%
    - border: 1px solid rgba(255, 255, 255, 0.1) !important
    - background: rgba(255, 255, 255, 0.05) !important
    - position: relative
    - overflow: hidden !important
    - justify-self: start
  name:
    - justify-self: start
    - font-size: var(--config-font-primary)
    - font-weight: 500
    - align-self: end
    - margin-bottom: 2px
    - position: relative
  label:
    - justify-self: start
    - font-size: var(--config-font-secondary)
    - opacity: 0.7
    - align-self: start
    - margin-top: 2px
    - position: relative
  custom_fields:
    badge1:
      - position: absolute
      - top: 10px
      - right: 10px
      - background: rgba(var(--appliance-color), 0.15)
      - color: rgb(var(--appliance-color))
      - border: 1px solid rgba(var(--appliance-color), 0.3)
      - padding: 2px 10px
      - border-radius: 12px
      - font-size: var(--config-font-badge)
      - font-weight: 600
      - text-transform: uppercase
      - letter-spacing: 0.5px
      - white-space: nowrap
      - z-index: 1
      - transition: all 0.5s ease
    badge2:
      - position: absolute
      - top: 38px
      - right: 10px
      - padding: 4px 8px
      - font-size: 10px
      - letter-spacing: 0.5px
      - white-space: nowrap
      - opacity: 0.9
      - text-transform: uppercase
      - font-weight: 500
      - z-index: 1
      - transition: all 0.5s ease
    bar:
      - position: absolute
      - bottom: 0
      - left: 0
      - height: 3.5px
      - width: var(--appliance-level)
      - background: rgb(var(--appliance-color))
      - box-shadow: 0 0 10px rgb(var(--appliance-color))
      - transition: width 0.5s ease
tap_action:
  action: more-info
label: |
  [[[
    let ent = variables.ent_helper_run;
    let state = states[ent] ? states[ent].state : 'unknown';
    if (state === 'on') return 'Running';
    if (state === 'off') return 'Not Running';
    return state;
  ]]]
icon: mdi:washing-machine
custom_fields:
  badge1: " "
  badge2: " "
  bar: " "
extra_styles: |
  [[[
    let ent_switch = variables.ent_switch;
    let ent_power = variables.ent_power;
    let ent_helper_run = variables.ent_helper_run;
    let ent_dry = variables.ent_helper_dry_mode;
    let thresh_high = variables.thresh_high;
    let thresh_active = variables.thresh_active;

    let switch_state = states[ent_switch] ? states[ent_switch].state : 'unknown';
    
    let power_state = states[ent_power];
    let is_power_valid = power_state && !['unknown', 'unavailable', 'none'].includes(power_state.state.toLowerCase());
    let power = is_power_valid ? Math.round(parseFloat(power_state.state)) : 0;
    let power_text = is_power_valid ? ` • ${power}W` : '';

    let run_obj = states[ent_helper_run];
    let dry_obj = states[ent_dry];
    let has_run_helper = run_obj && !['unknown', 'unavailable', 'none'].includes(run_obj.state);
    let is_running = has_run_helper ? run_obj.state === 'on' : (power > thresh_active);
    let is_drying_mode = dry_obj && dry_obj.state === 'on';

    let time_str = '';
    let seconds = 0;

    if (is_running && switch_state === 'on') {
        if (has_run_helper && run_obj.last_changed) {
            let start_time = new Date(run_obj.last_changed);
            let now = new Date();
            seconds = Math.max(0, Math.floor((now - start_time) / 1000));
            let hours = Math.floor(seconds / 3600);
            let mins = Math.floor((seconds % 3600) / 60);
            time_str = seconds > 60 ? `${hours}h ${mins.toString().padStart(2, '0')}m` : 'Started';
        } else {
            time_str = 'Running';
        }
    }

    let status_text = 'Idle';
    let color = '158, 158, 158';
    let anim_type = 'none';
    let icon_shake = 'none';
    let wave_anim = 'none';
    let overlay_img = 'none';
    let level = 0;
    let badge1 = '';

    if (switch_state === 'off') {
        status_text = 'Plug Off';
        color = '244, 67, 54';
        badge1 = status_text;
    } else if (['unavailable', 'unknown'].includes(switch_state)) {
        status_text = 'Offline';
        color = '158, 158, 158';
        badge1 = status_text;
    } else if (is_running) {
        if (is_drying_mode) {
            status_text = 'Drying';
            color = '255, 152, 0';
            anim_type = 'steam-rise 2s ease-in-out infinite';
            overlay_img = 'linear-gradient(0deg, transparent, rgba(255,255,255,0.4), transparent)';
            icon_shake = 'none';
        } else {
            status_text = 'Washing';
            color = '33, 150, 243';
            anim_type = 'bubbles 2s linear infinite';
            overlay_img = 'radial-gradient(2px 2px at 20% 80%, white, transparent), radial-gradient(2px 2px at 50% 70%, white, transparent)';
            
            if (power > thresh_high) {
                status_text = 'Spinning';
                color = '0, 170, 170';
                icon_shake = 'washer-spin-smooth 0.8s linear infinite';
            } else {
                icon_shake = 'shake 2s ease-in-out infinite';
            }
        }
        wave_anim = 'wave 4s linear infinite';
        let mins_elapsed = Math.floor(seconds / 60);
        level = Math.min(80, 10 + (Math.floor(mins_elapsed / 10) * 10));
        badge1 = `${status_text}${power_text}`;
    } else {
        status_text = 'Idle';
        color = '158, 158, 158';
        badge1 = `${status_text}${power_text}`;
    }

    let ent_door = variables.sensor_door;
    let door_state = (ent_door && states[ent_door]) ? states[ent_door].state.toLowerCase() : null;
    
    let corner_color = (switch_state === 'off') ? '158, 158, 158' : color; 
    let corner_display = 'none';

    if (ent_door && door_state && door_state !== 'unknown' && door_state !== 'unavailable') {
        corner_display = 'block';
        let is_open = (door_state === 'on' || door_state === 'open');
        if (is_open) {
            corner_color = '244, 67, 54';
        }
    }

    let b2_bg = `rgba(${color}, 0.15)`;
    let b2_border = `1px solid rgba(128,128,128, 0.2)`;
    let b2_br = `2px solid rgb(${color})`;

    return `
      #card {
        --appliance-color: ${color};
        --appliance-level: ${level}%;
        --appliance-anim-overlay: ${anim_type};
        --appliance-anim-shake: ${icon_shake};
        --appliance-anim-wave: ${wave_anim};
        --appliance-overlay-bg: ${overlay_img};
        --door-corner-color: rgb(${corner_color});
        --door-corner-display: ${corner_display};
      }
      #card::after {
        content: '';
        display: var(--door-corner-display);
        position: absolute;
        top: -0.5px;
        left: -0.5px;
        opacity: 0.7;
        width: 15px;
        height: 15px;
        border-top: 5px solid var(--door-corner-color);
        border-left: 5px solid var(--door-corner-color);
        border-top-left-radius: var(--ha-card-border-radius, 12px);
        pointer-events: none;
        transition: border-color 0.5s ease;
      }
      
      #badge1::before { content: "${badge1}"; } 
      #badge2 {
        display: ${time_str ? 'block' : 'none'};
        background: ${b2_bg};
        color: var(--primary-text-color, #fff);
        border-top: ${b2_border}; border-bottom: ${b2_border}; border-right: ${b2_border};
        border-left: ${b2_br}; border-radius: 6px !important;
      }
      #badge2::before { content: "${time_str}"; }
      #img-cell::before {
        content: ''; position: absolute; left: -50%; width: 200%; height: 200%;
        top: calc(100% - var(--appliance-level)); background: rgba(var(--appliance-color), 0.6) !important;
        border-radius: 40%; animation: var(--appliance-anim-wave) !important;
        transition: top 0.5s ease; z-index: 1;
        display: ${wave_anim === 'none' ? 'none' : 'block'};
      }
      #img-cell::after {
        content: ''; position: absolute; inset: 0; background-image: var(--appliance-overlay-bg);
        background-size: 100% 100%; animation: var(--appliance-anim-overlay) !important; z-index: 1;
        display: ${anim_type === 'none' ? 'none' : 'block'};
      }
      @keyframes wave { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
      @keyframes shake { 0%, 100% { transform: rotate(0deg); } 25% { transform: rotate(5deg) translateY(-1px); } 75% { transform: rotate(-5deg) translateY(1px); } }
      @keyframes washer-spin-smooth {
        0% { transform: rotate(0deg) translate(0,0); }
        25% { transform: rotate(90deg) translate(0.5px, 0.5px); }
        50% { transform: rotate(180deg) translate(0,0); }
        75% { transform: rotate(270deg) translate(-0.5px, -0.5px); }
        100% { transform: rotate(360deg) translate(0,0); }
      }
      @keyframes bubbles { 0% { transform: translateY(10px); opacity: 0; } 50% { opacity: 1; } 100% { transform: translateY(-20px); opacity: 0; } }
      @keyframes steam-rise { 0% { opacity: 0; transform: translateY(10px) scale(0.9); } 50% { opacity: 0.6; } 100% { opacity: 0; transform: translateY(-20px) scale(1.1); } }
    `;
  ]]]

```
</details>

<details>
<summary><strong>Dumb Combo Washing machine & Dryer (Helper/Template)</summary>

```yaml
  - binary_sensor:
      # 1. Main "Combo Machine Running" Detector
      - name: "Combo Machine Active Delay"
        unique_id: combo_machine_active_delay
        device_class: running
        icon: mdi:washing-machine
        state: >
          {{ states('sensor.smart_plug_power')|float(0) > 5 }}
        delay_off: "00:05:00" # Wait 5 min before saying it's off

      # 2. "Drying Mode" Detector
      # Logic If we see HIGH power for a sustained period, we assume Drying.
      # Note: Washing heaters cycle on/off quickly. Dryers stay on longer.
      - name: "Combo Machine Drying Detector"
        unique_id: combo_machine_drying_detector
        state: >
          {{ states('sensor.smart_plug_power')|float(0) > 800 }}
        # MUST be high for 15 mins to count as drying
        delay_on: "00:15:00"
        # Keeps drying active during cool down
        delay_off: "00:05:00"
```
</details>

---

<details>
<summary><strong>5 - Fridge (smart plug)</summary>

```yaml
type: custom:button-card
entity: sensor.smart_plug_power
name: Dumb Fridge
show_state: false
show_label: true
variables:
  ent_switch: switch.smart_plug
  ent_power: sensor.smart_plug_power
  sensor_door: binary_sensor.fridge_door_contact
  sensor_door2: ""
  sensor_temp_fridge: sensor.fridge_temp
  sensor_temp_freezer: sensor.fridge_temp_freezer
  thresh_cooling: 1
  thresh_super: 180
  thresh_defrost: 300
  max_power_w: 500
  max_temp_fridge: 8
  max_temp_freezer: -10
  show_bar: "off"
  size_icon: 45px
  size_shape: 65px
  size_card_height: 95px
  font_primary: 15px
  font_secondary: 12px
  font_badge: 10px
styles:
  card:
    - "--config-icon-size": "[[[ return variables.size_icon ]]]"
    - "--config-shape-size": "[[[ return variables.size_shape ]]]"
    - "--config-card-height": "[[[ return variables.size_card_height ]]]"
    - "--config-font-primary": "[[[ return variables.font_primary ]]]"
    - "--config-font-secondary": "[[[ return variables.font_secondary ]]]"
    - "--config-font-badge": "[[[ return variables.font_badge ]]]"
    - height: var(--config-card-height) !important
    - padding: 0px !important
    - overflow: hidden
    - position: relative
    - transition: box-shadow 1s ease, background 1s ease
  grid:
    - padding: 12px 16px
    - height: 100%
    - box-sizing: border-box
    - grid-template-areas: "\"i n\" \"i l\""
    - grid-template-columns: var(--config-shape-size) 1fr
    - grid-template-rows: auto auto
    - align-content: center
    - gap: 0px 12px
    - position: relative
    - z-index: 2
  icon:
    - width: var(--config-icon-size)
    - height: var(--config-icon-size)
    - color: rgb(var(--appliance-color))
    - z-index: 3
    - animation: var(--appliance-icon-anim) !important
    - transform-origin: 50% 60%
  img_cell:
    - width: var(--config-shape-size)
    - height: var(--config-shape-size)
    - border-radius: 50%
    - border: 1px solid rgba(var(--appliance-color), 0.3) !important
    - background: rgba(var(--appliance-color), 0.1) !important
    - position: relative
    - overflow: visible !important
    - justify-self: start
    - z-index: 1
  name:
    - justify-self: start
    - font-size: var(--config-font-primary)
    - font-weight: 500
    - align-self: end
    - margin-bottom: 2px
    - position: relative
    - z-index: 2
  label:
    - justify-self: start
    - font-size: var(--config-font-secondary)
    - opacity: 0.7
    - align-self: start
    - margin-top: 2px
    - position: relative
    - z-index: 2
  custom_fields:
    bg1:
      - position: absolute
      - inset: 0
      - pointer-events: none
      - z-index: 0
      - display: var(--appliance-bg-d1)
      - background-image: var(--appliance-bg-img1)
      - background-size: var(--appliance-bg-sz1)
      - background-repeat: var(--appliance-bg-rep1)
      - animation: var(--appliance-bg-anim1)
      - opacity: var(--appliance-bg-op1)
    bg2:
      - position: absolute
      - inset: 0
      - pointer-events: none
      - z-index: 0
      - display: var(--appliance-bg-d2)
      - background-image: var(--appliance-bg-img2)
      - background-size: var(--appliance-bg-sz2)
      - background-repeat: repeat
      - animation: var(--appliance-bg-anim2)
      - opacity: var(--appliance-bg-op2)
    badge1:
      - position: absolute
      - top: 10px
      - right: 10px
      - padding: 3px 8px
      - font-size: var(--config-font-badge)
      - font-weight: 600
      - text-transform: uppercase
      - letter-spacing: 0.5px
      - white-space: nowrap
      - z-index: 5
      - transition: all 0.5s ease
    badge2:
      - position: absolute
      - top: 38px
      - right: 10px
      - padding: 4px 8px
      - font-size: 10px
      - letter-spacing: 0.5px
      - white-space: nowrap
      - opacity: 0.9
      - text-transform: uppercase
      - font-weight: 500
      - z-index: 5
      - transition: all 0.5s ease
    bar:
      - position: absolute
      - bottom: 0
      - left: 0
      - height: 3.5px
      - width: var(--appliance-level)
      - background: rgb(var(--appliance-color))
      - box-shadow: 0 0 10px rgb(var(--appliance-color))
      - transition: width 0.5s ease
      - display: var(--bar-display)
      - z-index: 5
    door_dash:
      - position: absolute
      - top: 50%
      - left: 0
      - transform: translateY(-50%)
      - opacity: 0.8
      - width: 4px
      - height: 26px
      - border-top-right-radius: 4px
      - border-bottom-right-radius: 4px
      - display: var(--door-dash-display)
      - background: rgb(var(--door-dash-color))
      - box-shadow: var(--door-dash-glow)
      - transition: background 0.4s ease, box-shadow 0.4s ease
      - z-index: 2
      - pointer-events: none
tap_action:
  action: more-info
label: |
  [[[ return entity ? entity.state : 'Entity Setup Required'; ]]]
icon: |
  [[[ 
    let d1 = states[variables.sensor_door];
    let d2 = states[variables.sensor_door2];
    let d1_open = d1 && (d1.state === 'on' || d1.state === 'open');
    let d2_open = d2 && (d2.state === 'on' || d2.state === 'open');
    return (d1_open || d2_open) ? 'mdi:fridge-alert' : 'mdi:fridge'; 
  ]]]
custom_fields:
  bg1: " "
  bg2: " "
  badge1: " "
  badge2: " "
  bar: " "
  door_dash: " "
extra_styles: |
  [[[
    let ent_switch = variables.ent_switch;
    let ent_power = variables.ent_power;
    let ent_door1 = variables.sensor_door;
    let ent_door2 = variables.sensor_door2;
    let ent_temp_f = variables.sensor_temp_fridge;
    let ent_temp_z = variables.sensor_temp_freezer;
    
    let thresh_cool = variables.thresh_cooling;
    let thresh_super = variables.thresh_super;
    let thresh_defrost = variables.thresh_defrost;
    let max_power = variables.max_power_w;
    let max_temp_f = variables.max_temp_fridge;
    let max_temp_z = variables.max_temp_freezer;
    let show_bar = variables.show_bar;

    let switch_state = states[ent_switch] ? states[ent_switch].state : 'unknown';
    let power_state = states[ent_power];
    let is_power_valid = power_state && !['unknown', 'unavailable', 'none'].includes(power_state.state.toLowerCase());
    let power = is_power_valid ? Math.round(parseFloat(power_state.state)) : 0;
    let power_text = is_power_valid ? ` • ${power}W` : '';

    let door1_val = (ent_door1 && states[ent_door1]) ? states[ent_door1].state.toLowerCase() : 'unknown';
    let door2_val = (ent_door2 && states[ent_door2]) ? states[ent_door2].state.toLowerCase() : 'unknown';
    
    let bad_states = ['unknown', 'unavailable', ''];
    let d1_valid = !bad_states.includes(door1_val);
    let d2_valid = !bad_states.includes(door2_val);
    
    let d1_open = d1_valid && (door1_val === 'on' || door1_val === 'open');
    let d2_open = d2_valid && (door2_val === 'on' || door2_val === 'open');
    let door_open = d1_open || d2_open;

    let raw_temp_f = states[ent_temp_f] ? states[ent_temp_f].state : '';
    let raw_temp_z = states[ent_temp_z] ? states[ent_temp_z].state : '';
    
    let t_f = !bad_states.includes(raw_temp_f) ? raw_temp_f + '°' : '';
    let t_z = !bad_states.includes(raw_temp_z) ? raw_temp_z + '°' : '';

    let val_f = parseFloat(raw_temp_f); if (isNaN(val_f)) val_f = -999;
    let val_z = parseFloat(raw_temp_z); if (isNaN(val_z)) val_z = -999;
    let alert_f = (val_f > max_temp_f) && (val_f !== -999);
    let alert_z = (val_z > max_temp_z) && (val_z !== -999);

    let status_text = 'Idle';
    let color = '158, 158, 158';
    let card_shadow = 'var(--ha-card-box-shadow, none)';
    let bg_d1 = 'none'; let bg_img1 = 'none'; let bg_sz1 = 'none'; let bg_anim1 = 'none'; let bg_op1 = '1'; let bg_rep1 = 'repeat';
    let bg_d2 = 'none'; let bg_img2 = 'none'; let bg_sz2 = 'none'; let bg_anim2 = 'none'; let bg_op2 = '1';
    let icon_anim = 'none'; let anim_frost = 'none'; let anim_drip = 'none';
    let frost_shadow = 'none'; let overlay_img = 'none';

    let snow_img_1 = `radial-gradient(circle at 20px 30px, white 2px, transparent 3px), radial-gradient(circle at 50px 160px, white 2px, transparent 3px), radial-gradient(circle at 90px 40px, white 2px, transparent 3px), radial-gradient(circle at 130px 80px, white 2px, transparent 3px), radial-gradient(circle at 160px 120px, white 2px, transparent 3px), radial-gradient(circle at 240px 300px, white 2px, transparent 3px), radial-gradient(circle at 280px 100px, white 2px, transparent 3px)`;
    let snow_img_2 = `radial-gradient(circle at 10px 10px, rgba(255,255,255,0.7) 1px, transparent 2px), radial-gradient(circle at 30px 90px, rgba(255,255,255,0.7) 1px, transparent 2px), radial-gradient(circle at 80px 50px, rgba(255,255,255,0.7) 1px, transparent 2px), radial-gradient(circle at 110px 190px, rgba(255,255,255,0.7) 1px, transparent 2px), radial-gradient(circle at 150px 100px, rgba(255,255,255,0.7) 1px, transparent 2px), radial-gradient(circle at 220px 250px, rgba(255,255,255,0.7) 1px, transparent 2px)`;
    let drop_img   = `radial-gradient(ellipse at center, rgba(255,152,0,0.5) 0%, transparent 60%), radial-gradient(ellipse at center, rgba(255,152,0,0.4) 0%, transparent 60%), radial-gradient(ellipse at center, rgba(255,152,0,0.5) 0%, transparent 60%), radial-gradient(ellipse at center, rgba(255,152,0,0.4) 0%, transparent 60%)`;

    if (switch_state === 'off') {
        status_text = 'Plug Off';
        color = '244, 67, 54';
    } else if (['unavailable', 'unknown'].includes(switch_state)) {
        status_text = 'Offline';
    } else {
        if (power > thresh_defrost) {
            status_text = 'Defrost';
            color = '255, 152, 0';
            card_shadow = 'inset 0 0 40px rgba(255, 152, 0, 0.08)';
            bg_d1 = 'block'; bg_img1 = drop_img; bg_sz1 = '100% 100%'; bg_anim1 = 'accumulate-drip-card 4s ease-in infinite'; bg_op1 = '1'; bg_rep1 = 'no-repeat';
            anim_drip = 'accumulate-drip-icon 3s ease-in infinite';
            overlay_img = `radial-gradient(ellipse at center, rgba(255,193,7,0.8) 0%, transparent 60%), radial-gradient(ellipse at center, rgba(255,193,7,0.6) 0%, transparent 60%)`;
        } else if (power > thresh_super) {
            status_text = 'Super Cool';
            color = '0, 188, 212';
            card_shadow = 'inset 0 0 60px rgba(0, 188, 212, 0.15)';
            bg_d1 = 'block'; bg_img1 = snow_img_1; bg_sz1 = '300px 400px'; bg_anim1 = 'snow-fall-1 8s linear infinite'; bg_op1 = '0.15'; bg_rep1 = 'repeat';
            bg_d2 = 'block'; bg_img2 = snow_img_2; bg_sz2 = '300px 300px'; bg_anim2 = 'snow-fall-2 4s linear infinite'; bg_op2 = '0.1';
            icon_anim = 'compressor-rumble 0.1s linear infinite';
            anim_frost = 'pulse-frost 1.5s ease-in-out infinite';
            frost_shadow = 'inset 0 0 25px 5px rgba(0, 188, 212, 0.6)';
        } else if (power > thresh_cool) {
            status_text = 'Cooling';
            color = '129, 212, 250';
            card_shadow = 'inset 0 0 40px rgba(129, 212, 250, 0.1)';
            bg_d1 = 'block'; bg_img1 = snow_img_1; bg_sz1 = '300px 400px'; bg_anim1 = 'snow-fall-1 16s linear infinite'; bg_op1 = '0.08'; bg_rep1 = 'repeat';
            bg_d2 = 'block'; bg_img2 = snow_img_2; bg_sz2 = '300px 300px'; bg_anim2 = 'snow-fall-2 8s linear infinite'; bg_op2 = '0.05';
            icon_anim = 'compressor-rumble 0.3s linear infinite';
            anim_frost = 'pulse-frost 3s ease-in-out infinite';
            frost_shadow = 'inset 0 0 15px 2px rgba(129, 212, 250, 0.5)';
        }
    }

    let d1_c = color;
    let corner_display = 'none';
    let dash_color = color;
    let dash_glow = 'none';
    let dash_display = 'none';

    if (d1_valid && d2_valid) {
        corner_display = 'block';
        dash_display = 'block';
        d1_c = d1_open ? '244, 67, 54' : color;
        dash_color = d2_open ? '244, 67, 54' : color;
        dash_glow = d2_open ? '2px 0 6px rgba(244, 67, 54, 0.6)' : 'none';
    } else if (d1_valid || d2_valid) {
        corner_display = 'block';
        let open = d1_valid ? d1_open : d2_open;
        d1_c = open ? '244, 67, 54' : color;
    }

    if (door_open) {
        color = '244, 67, 54';
        card_shadow = 'inset 0 0 50px rgba(244, 67, 54, 0.15)';
        icon_anim = 'shake-alert 0.5s ease-in-out infinite';
        frost_shadow = 'none';
        anim_frost = 'none';
        anim_drip = 'none';
        overlay_img = 'none';
        bg_d1 = 'none';
        bg_d2 = 'none';
    }

    let badge1_text = '';
    if (d1_open && d2_open) badge1_text = '⚠️ DOORS OPEN';
    else if (d1_open || d2_open) badge1_text = '⚠️ DOOR OPEN';
    else badge1_text = `${status_text}${power_text}`;

    let badge1 = badge1_text;
    let b1_c = door_open ? '244, 67, 54' : color;
    let b1_bg = `rgba(${b1_c}, 0.15)`;
    let b1_border = `1px solid rgba(${b1_c}, 0.3)`;
    let b1_bl = `2px solid rgb(${b1_c})`;

    let badge2 = '';
    let b2_bg = 'transparent'; let b2_bl = 'none'; let b2_br = 'none'; let b2_border = 'none';
    
    let c_cool = '33, 150, 243';
    let c_alert = '244, 67, 54';

    if (t_f || t_z) {
        let f_str = alert_f ? `⚠️ ${t_f}` : t_f;
        let z_str = alert_z ? `⚠️ ${t_z}` : t_z;
        badge2 = [f_str, z_str].filter(Boolean).join(' | ');

        let c_f = alert_f ? c_alert : c_cool;
        let c_z = alert_z ? c_alert : c_cool;

        b2_border = `1px solid rgba(128,128,128, 0.2)`;
        if (t_f && t_z) {
            b2_bg = `linear-gradient(90deg, rgba(${c_f}, 0.15) 0%, rgba(${c_z}, 0.15) 100%)`;
            b2_bl = `2px solid rgb(${c_f})`;
            b2_br = `2px solid rgb(${c_z})`;
        } else if (t_f) {
            b2_bg = `rgba(${c_f}, 0.15)`;
            b2_bl = `2px solid rgb(${c_f})`;
            b2_br = b2_border;
        } else if (t_z) {
            b2_bg = `rgba(${c_z}, 0.15)`;
            b2_bl = b2_border;
            b2_br = `2px solid rgb(${c_z})`;
        }
    }

    let bar_disp = show_bar === 'on' ? 'block' : 'none';
    let progress = Math.min(100, Math.max(0, Math.floor((power / max_power) * 100)));

    return `
      #card {
        --appliance-color: ${color};
        --appliance-level: ${progress}%; 
        --appliance-bg-d1: ${bg_d1}; --appliance-bg-img1: ${bg_img1}; --appliance-bg-sz1: ${bg_sz1}; --appliance-bg-anim1: ${bg_anim1}; --appliance-bg-op1: ${bg_op1}; --appliance-bg-rep1: ${bg_rep1};
        --appliance-bg-d2: ${bg_d2}; --appliance-bg-img2: ${bg_img2}; --appliance-bg-sz2: ${bg_sz2}; --appliance-bg-anim2: ${bg_anim2}; --appliance-bg-op2: ${bg_op2};
        --appliance-icon-anim: ${icon_anim};
        --appliance-anim-frost: ${anim_frost};
        --appliance-anim-drip: ${anim_drip};
        --appliance-frost-shadow: ${frost_shadow};
        --appliance-overlay-bg: ${overlay_img};
        --door-corner-color: rgb(${d1_c});
        --door-corner-display: ${corner_display};
        --door-dash-color: ${dash_color};
        --door-dash-glow: ${dash_glow};
        --door-dash-display: ${dash_display};
        --bar-display: ${bar_disp};
        box-shadow: ${card_shadow} !important;
      }
      #card::after {
        content: '';
        display: var(--door-corner-display);
        position: absolute;
        top: -0.5px;
        left: -0.5px;
        opacity: 0.7;
        width: 15px;
        height: 15px;
        border-top: 5px solid var(--door-corner-color);
        border-left: 5px solid var(--door-corner-color);
        border-top-left-radius: var(--ha-card-border-radius, 12px);
        pointer-events: none;
        transition: border-color 0.5s ease;
        z-index: 1;
      }
      #badge1 {
        background: ${b1_bg};
        color: rgb(${b1_c});
        border-top: ${b1_border};
        border-bottom: ${b1_border};
        border-right: ${b1_border};
        border-left: ${b1_bl};
        border-radius: 6px !important;
      }
      #badge1::before { content: "${badge1}"; }

      #badge2 {
        display: ${badge2 ? 'block' : 'none'};
        background: ${b2_bg};
        color: var(--primary-text-color, #fff);
        border-top: ${b2_border};
        border-bottom: ${b2_border};
        border-left: ${b2_bl};
        border-right: ${b2_br};
        border-radius: 6px !important;
      }
      #badge2::before { content: "${badge2}"; }

      #img-cell::before {
        content: ''; position: absolute; inset: 0; box-shadow: var(--appliance-frost-shadow);
        animation: var(--appliance-anim-frost) !important; z-index: 1; border-radius: 50%; pointer-events: none;
      }
      #img-cell::after {
        content: ''; position: absolute; inset: 0; background-image: var(--appliance-overlay-bg);
        background-repeat: no-repeat; animation: var(--appliance-anim-drip) !important; z-index: 1; 
        border-radius: 50%; pointer-events: none;
      }

      @keyframes snow-fall-1 { from { background-position: 0 0; } to { background-position: 0 400px; } }
      @keyframes snow-fall-2 { from { background-position: 0 0; } to { background-position: 0 300px; } }
      @keyframes accumulate-drip-card {
        0% { background-position: 15% 10%, 45% 20%, 75% 15%, 85% 30%; background-size: 0px 0px, 0px 0px, 0px 0px, 0px 0px; opacity: 0; }
        40% { background-position: 15% 30%, 45% 40%, 75% 35%, 85% 50%; background-size: 15px 25px, 20px 30px, 12px 20px, 25px 35px; opacity: 0.4; }
        80% { background-position: 15% 80%, 45% 85%, 75% 75%, 85% 90%; background-size: 15px 35px, 20px 40px, 12px 30px, 25px 45px; opacity: 0.2; }
        100% { background-position: 15% 100%, 45% 105%, 75% 95%, 85% 110%; background-size: 10px 40px, 15px 45px, 8px 35px, 20px 50px; opacity: 0; }
      }
      @keyframes pulse-frost { 0%, 100% { opacity: 0.4; transform: scale(0.95); } 50% { opacity: 0.8; transform: scale(1); } }
      @keyframes accumulate-drip-icon {
        0% { background-position: 30% 10%, 70% 20%; background-size: 0px 0px, 0px 0px; opacity: 0; }
        40% { background-position: 30% 30%, 70% 40%; background-size: 8px 12px, 12px 16px; opacity: 1; }
        80% { background-position: 30% 80%, 70% 90%; background-size: 8px 18px, 12px 22px; opacity: 0.8; }
        100% { background-position: 30% 100%, 70% 110%; background-size: 6px 20px, 10px 25px; opacity: 0; }
      }
      @keyframes compressor-rumble {
        0% { transform: translate(0, 0); } 25% { transform: translate(-1px, 0.5px); } 50% { transform: translate(1px, -0.5px); } 75% { transform: translate(-0.5px, 0.5px); } 100% { transform: translate(0, 0); }
      }
      @keyframes shake-alert {
        0%, 100% { transform: rotate(0deg); } 25% { transform: rotate(5deg) translateY(-1px); } 75% { transform: rotate(-5deg) translateY(1px); }
      }
    `;
  ]]]

```
</details>

---
<details>
<summary><strong>6 - Dumb Appliance (Generic / Timer)</summary>

```yaml
type: custom:button-card
entity: timer.dishwasher_time_remaining
name: Dumb Dishwasher
show_state: false
show_label: true
variables:
  timer_remaining: timer.dishwasher_time_remaining
  size_icon: 45px
  size_shape: 65px
  size_card_height: 95px
  font_primary: 15px
  font_secondary: 13px
  font_badge: 11px
styles:
  card:
    - "--config-icon-size": "[[[ return variables.size_icon ]]]"
    - "--config-shape-size": "[[[ return variables.size_shape ]]]"
    - "--config-card-height": "[[[ return variables.size_card_height ]]]"
    - "--config-font-primary": "[[[ return variables.font_primary ]]]"
    - "--config-font-secondary": "[[[ return variables.font_secondary ]]]"
    - "--config-font-badge": "[[[ return variables.font_badge ]]]"
    - height: var(--config-card-height) !important
    - padding: 0px !important
    - overflow: hidden
    - position: relative
    - transition: all 0.5s ease
  grid:
    - padding: 12px 16px
    - height: 100%
    - box-sizing: border-box
    - grid-template-areas: '"i n" "i l"'
    - grid-template-columns: var(--config-shape-size) 1fr
    - grid-template-rows: auto auto
    - align-content: center
    - gap: 0px 12px
    - position: relative
  icon:
    - width: var(--config-icon-size)
    - height: var(--config-icon-size)
    - color: white
    - z-index: 1
    - animation: var(--appliance-anim-shake) !important
    - transform-origin: 50% 50%
  img_cell:
    - width: var(--config-shape-size)
    - height: var(--config-shape-size)
    - border-radius: 50%
    - border: 1px solid rgba(255, 255, 255, 0.1) !important
    - background: rgba(255, 255, 255, 0.05) !important
    - position: relative
    - overflow: hidden !important
    - justify-self: start
  name:
    - justify-self: start
    - font-size: var(--config-font-primary)
    - font-weight: 500
    - align-self: end
    - margin-bottom: 2px
    - position: relative
  label:
    - justify-self: start
    - font-size: var(--config-font-secondary)
    - opacity: 0.7
    - align-self: start
    - margin-top: 2px
    - position: relative
  custom_fields:
    badge1:
      - position: absolute
      - top: 10px
      - right: 10px
      - background: rgba(var(--appliance-color), 0.15)
      - color: rgb(var(--appliance-color))
      - border: 1px solid rgba(var(--appliance-color), 0.3)
      - padding: 2px 10px
      - border-radius: 12px
      - font-size: var(--config-font-badge)
      - font-weight: 600
      - text-transform: uppercase
      - letter-spacing: 0.5px
      - white-space: nowrap
      - z-index: 1
    badge2:
      - position: absolute
      - top: 38px
      - right: 10px
      - padding: 4px 8px
      - font-size: 10px
      - letter-spacing: 0.5px
      - white-space: nowrap
      - opacity: 0.9
      - text-transform: uppercase
      - font-weight: 500
      - z-index: 1
    bar:
      - position: absolute
      - bottom: 0
      - left: 0
      - height: 3.5px
      - width: var(--appliance-level)
      - background: rgb(var(--appliance-color))
      - box-shadow: 0 0 10px rgb(var(--appliance-color))
      - transition: width 0.5s ease
tap_action:
  action: more-info
label: |
  [[[
    let ent = variables.timer_remaining;
    let state = states[ent] ? states[ent].state : 'unknown';
    if (state === 'active') return 'Running';
    return 'Not Running';
  ]]]
icon: mdi:dishwasher
custom_fields:
  badge1: " "
  badge2: " "
  bar: " "
extra_styles: |
  [[[
    let ent_timer = variables.timer_remaining;
    let timer_obj = states[ent_timer];
    let is_active = timer_obj && timer_obj.state === 'active';

    let time_str = '';
    let progress_pct = 0;

    // Helper function to parse "HH:MM:SS" into total seconds
    function parseSeconds(timeVal) {
        if (!timeVal) return 0;
        if (typeof timeVal === 'number') return timeVal;
        let parts = timeVal.toString().split(':');
        if (parts.length === 3) {
            return (+parts[0]) * 3600 + (+parts[1]) * 60 + (+parts[2]);
        }
        return 0;
    }

    if (is_active) {
        let remaining_sec = 0;
        let total_duration_sec = 0;

        // Calculate total duration in seconds
        if (timer_obj.attributes && timer_obj.attributes.duration) {
            total_duration_sec = parseSeconds(timer_obj.attributes.duration);
        }

        // Calculate remaining seconds
        if (timer_obj.attributes && timer_obj.attributes.finishes_at) {
            let finish = new Date(timer_obj.attributes.finishes_at);
            let now = new Date();
            remaining_sec = Math.max(0, Math.floor((finish - now) / 1000));
        } else if (timer_obj.attributes && timer_obj.attributes.remaining) {
            remaining_sec = parseSeconds(timer_obj.attributes.remaining);
        }

        // Calculate completion percentage
        if (total_duration_sec > 0) {
            let elapsed_sec = Math.max(0, total_duration_sec - remaining_sec);
            progress_pct = Math.min(100, Math.round((elapsed_sec / total_duration_sec) * 100));
        } else {
            progress_pct = 50; // fallback if duration missing
        }

        if (remaining_sec > 0) {
            let hours = Math.floor(remaining_sec / 3600);
            let mins = Math.floor((remaining_sec % 3600) / 60);
            time_str = hours > 0 ? `${hours}h ${mins.toString().padStart(2, '0')}m left` : `${mins}m left`;
        } else {
            time_str = 'Running';
        }
    }

    let status_text = 'Idle';
    let color = '158, 158, 158';
    let anim_type = 'none';
    let icon_shake = 'none';
    let wave_anim = 'none';
    let overlay_img = 'none';
    let badge1 = '';

    if (is_active) {
        status_text = 'Washing';
        color = '33, 150, 243';
        anim_type = 'bubbles 1s linear infinite';
        overlay_img = 'radial-gradient(2px 2px at 20% 80%, white, transparent), radial-gradient(2px 2px at 50% 70%, white, transparent)';
        icon_shake = 'shake 0.8s ease-in-out infinite';
        wave_anim = 'wave 4s linear infinite';
        badge1 = status_text;
    } else {
        status_text = 'Idle';
        color = '158, 158, 158';
        badge1 = status_text;
    }

    let b2_bg = `rgba(${color}, 0.15)`;
    let b2_border = `1px solid rgba(128,128,128, 0.2)`;
    let b2_br = `2px solid rgb(${color})`;

    return `
      #card {
        --appliance-color: ${color};
        --appliance-level: ${progress_pct}%;
        --appliance-anim-overlay: ${anim_type};
        --appliance-anim-shake: ${icon_shake};
        --appliance-anim-wave: ${wave_anim};
        --appliance-overlay-bg: ${overlay_img};
      }
      
      #badge1::before { content: "${badge1}"; } 
      #badge2 {
        display: ${time_str ? 'block' : 'none'};
        background: ${b2_bg};
        color: var(--primary-text-color, #fff);
        border-top: ${b2_border}; border-bottom: ${b2_border}; border-right: ${b2_br};
        border-left: ${b2_br}; border-radius: 6px !important;
      }
      #badge2::before { content: "${time_str}"; }
      #img-cell::before {
        content: ''; position: absolute; left: -50%; width: 200%; height: 200%;
        top: calc(100% - var(--appliance-level)); background: rgba(var(--appliance-color), 0.6) !important;
        border-radius: 40%; animation: var(--appliance-anim-wave) !important;
        transition: top 0.5s ease; z-index: 1;
        display: ${wave_anim === 'none' ? 'none' : 'block'};
      }
      #img-cell::after {
        content: ''; position: absolute; inset: 0; background-image: var(--appliance-overlay-bg);
        background-size: 100% 100%; animation: var(--appliance-anim-overlay) !important; z-index: 1;
        display: ${anim_type === 'none' ? 'none' : 'block'};
      }
      @keyframes wave { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
      @keyframes shake { 0%, 100% { transform: rotate(0deg); } 25% { transform: rotate(5deg) translateY(-1px); } 75% { transform: rotate(-5deg) translateY(1px); } }
      @keyframes bubbles { 0% { transform: translateY(10px); opacity: 0; } 50% { opacity: 1; } 100% { transform: translateY(-20px); opacity: 0; } }
      @keyframes steam-rise { 0% { opacity: 0; transform: translateY(5px); } 50% { opacity: 0.8; } 100% { opacity: 0; transform: translateY(-10px); } }
    `;
  ]]]

```
</details>

<details>
<summary><strong>Dumb Dishwasher (Helper/Template)</summary>

```
Create a timer helper and an automation that will start the timer based on defined logic. This could be from a vibration sensor being active for a certain amount of time, a contact sensor being open for a specific duration, or a combination of trend / history stats helpers.
```
</details>

---


[paypal_me_shield]: https://img.shields.io/badge/PayPal-00457C?style=for-the-badge&logo=paypal&logoColor=white

[paypal_me]: https://paypal.me/anasboxsupport

[revolut_me_shield]:
https://img.shields.io/badge/revolut-FFFFFF?style=for-the-badge&logo=revolut&logoColor=black

[revolut_me]: https://revolut.me/anas4e

[ko_fi_shield]: https://img.shields.io/badge/Ko--fi-F16061?style=for-the-badge&logo=ko-fi&logoColor=white

[ko_fi_me]: https://ko-fi.com/anasbox

[buy_me_coffee_shield]: 
https://img.shields.io/badge/Buy%20Me%20Coffee-ffdd00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black

[buy_me_coffee_me]: https://www.buymeacoffee.com/anasbox

[patreon_shield]: 
https://img.shields.io/badge/patreon-404040?style=for-the-badge&logo=patreon&logoColor=white

[patreon_me]:  https://patreon.com/AnasBox
