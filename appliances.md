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

# Home Assistant Animated Dishwasher / Washing Machine Cards

This [YouTube Video](https://youtu.be/6NM60DEdScA) explains how to do it.

![531304226-d16dce5f-74d0-4013-8258-ffba7a2a6bfb](https://github.com/user-attachments/assets/3304b727-c65d-4e48-8903-86360ed2e83a)

<hr>

# Cards:

<details>
<summary><strong>1 - Smart Dishwasher</summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.dishwasher_status
name: Smart Dishwasher
icon: mdi:dishwasher
primary_info: name
secondary_info: state
tap_action:
  action: more-info
icon_color: light-grey
fill_container: false
card_mod:
  style:
    .: |
      ha-card {
        /* ======================== */
        /* USER CONFIGURATION       */
        /* ======================== */
        
        /* 1. ENTITIES */
        {% set ent_progress  = 'sensor.dishwasher_progress' %}
        {% set ent_timerem   = 'sensor.dishwasher_time_remaining' %}
        {% set max_time = 120 %}
        {% set ent_power     = 'sensor.smart_plug_power' %} 
        
        /* OPTIONAL Progress Percentage Sensor (if exists) */
        {% set ent_percent   = 'sensor.dishwasher_progress_percantage' %}

        /* 2. SIZES (Px) */
        --config-icon-size:       65px;
        --config-font-primary:    15px;
        --config-font-secondary:  12px;
        --config-font-badge:      12px;
        /* ======================== */

        /* --- SENSORS & TIME --- */
        {% set status = states(ent_progress) %}
        {% set status_clean = status | replace('-', ' ') | title %}
        {% set time_rem = states(ent_timerem) | int(0) %}
        {% set raw_percent = states(ent_percent) | float(-1) %}
        
        /* --- POWER CALCULATION --- */
        {% set power_w = states(ent_power) | float(0) | round %}
        {% set power_text = ' • ' ~ power_w ~ 'W' if power_w > 0 else '' %}

        /* Format Time (min -> Xh Ym) */
        {% set hours = (time_rem / 60) | int %}
        {% set mins = time_rem % 60 %}
        {% set time_formatted = '%dh %02dm' | format(hours, mins) %}

        /* --- PROGRESS CALCULATION --- */
        {% if status | lower in ['idle', 'off', 'standby', 'unknown', 'unavailable'] %}
           {% set progress = 0 %}
           {% set badge_text = status_clean ~ power_text %}
        {% else %}
           
           /* LOGIC: Use Sensor if available, otherwise Calculate */
           {% if raw_percent >= 0 %}
              /* Use the sensor provided percentage */
              {% set progress = raw_percent | int %}
           {% else %}
              /* Fallback: Calculate based on fixed 180min (Adjust as needed) */
              {% set max_cycle_time = max_time %}
              {% set calc_prog = ((max_cycle_time - time_rem) / max_cycle_time * 100) | int %}
              {% set progress = [5, [calc_prog, 100] | min] | max %}
           {% endif %}

           /* Show Status + Time + Power */
           {% set badge_text = status_clean ~ ' • ' ~ time_formatted ~ power_text %}
        {% endif %}

        /* --- STATE DEFINITIONS --- */
        {% set s_lower = status | lower %}
        {% set is_running = s_lower in ['wash', 'washing', 'rinse', 'rinsing', 'pre-wash'] %}
        {% set is_drying  = s_lower in ['dry', 'drying'] %}
        {% set is_done    = s_lower in ['finished', 'complete', 'end'] %}

        /* --- ASSIGN ANIMATIONS --- */
        {% if is_drying %}
          {% set color = '255, 152, 0' %}  /* Orange */
          {% set anim_type = 'steam-rise 2s ease-in-out infinite' %}
          {% set icon_shake = 'none' %}
          {% set wave_anim = 'wave 4s linear infinite' %}
          {% set overlay_img = 'linear-gradient(0deg, transparent, rgba(255,255,255,0.5), transparent)' %}
        {% elif is_done %}
          {% set color = '76, 175, 80' %}   /* Green */
          {% set anim_type = 'sparkle 2s infinite' %}
          {% set icon_shake = 'none' %}
          {% set wave_anim = 'wave 4s linear infinite' %}
          {% set overlay_img = 'radial-gradient(circle, rgba(255,255,255,0.8) 10%, transparent 60%)' %}
        {% elif is_running %}
          {% set color = '33, 150, 243' %}  /* Blue */
          {% set anim_type = 'bubbles 1s linear infinite' %}
          {% set icon_shake = 'shake 0.8s ease-in-out infinite' %}
          {% set wave_anim = 'wave 4s linear infinite' %}
          {% set overlay_img = 'radial-gradient(2px 2px at 20% 80%, white, transparent), radial-gradient(2px 2px at 50% 70%, white, transparent)' %}
        {% else %}
          {% set color = '158, 158, 158' %}  /* Grey */
          {% set anim_type = 'none' %}
          {% set icon_shake = 'none' %}
          {% set wave_anim = 'none' %}
          {% set overlay_img = 'none' %}
        {% endif %}

        /* --- OUTPUT VARIABLES --- */
        --dw-color: {{ color }};
        --dw-level: {{ progress }}%;
        --dw-anim-overlay: {{ anim_type }};
        --dw-anim-shake: {{ icon_shake }};
        --dw-anim-wave: {{ wave_anim }};
        --dw-overlay-bg: {{ overlay_img }};
        --dw-badge-content: "{{ badge_text }}";
        
        transition: all 0.5s ease;
        overflow: hidden;
      }

      /* BADGE */
      ha-card::before {
        content: var(--dw-badge-content);
        position: absolute;
        top: 10px; right: 10px;
        background: rgba(var(--dw-color), 0.15);
        color: rgb(var(--dw-color));
        border: 1px solid rgba(var(--dw-color), 0.3);
        padding: 2px 10px;
        border-radius: 12px;
        text-transform: uppercase;
        font-weight: 600;
        letter-spacing: 0.5px;
        font-size: var(--config-font-badge);
      }

      /* BAR */
      ha-card::after {
        content: '';
        position: absolute;
        bottom: 0; left: 0;
        height: 4px;
        width: var(--dw-level);
        background: rgb(var(--dw-color));
        box-shadow: 0 0 10px rgb(var(--dw-color));
        transition: width 0.5s ease;
      }
    mushroom-shape-icon$: |
      .shape {
        --icon-size: var(--config-icon-size) !important;
        background: rgba(255, 255, 255, 0.05) !important;
        overflow: hidden;
        position: relative;
        border: 1px solid rgba(255,255,255,0.1);
        
        /* Apply the animation determined by the Logic below */
        animation: var(--dw-anim-shake) !important;
        transform-origin: 50% 60%; 
      }

      /* Wave Layer */
      .shape::before {
        content: '';
        position: absolute;
        left: -50%;
        width: 200%; height: 200%;
        top: calc(100% - var(--dw-level));
        background: rgba(var(--dw-color), 0.6);
        border-radius: 40%;
        animation: var(--dw-anim-wave);
      }

      /* Overlay Layer (Bubbles/Steam) */
      .shape::after {
        content: '';
        position: absolute;
        inset: 0;
        background-image: var(--dw-overlay-bg);
        background-size: 100% 100%;
        animation: var(--dw-anim-overlay);
        z-index: 2;
      }

      /* The Icon Itself */
      ha-icon {
        z-index: 3;
        mix-blend-mode: overlay;
        color: white !important;
      }

      /* --- KEYFRAMES --- */
      @keyframes wave {
        from { transform: rotate(0deg); }
        to   { transform: rotate(360deg); }
      }
      @keyframes shake {
        0%, 100% { transform: rotate(0deg); }
        25% { transform: rotate(5deg) translateY(-1px); }
        75% { transform: rotate(-5deg) translateY(1px); }
      }
      @keyframes bubbles {
        0% { transform: translateY(10px); opacity: 0; }
        50% { opacity: 1; }
        100% { transform: translateY(-20px); opacity: 0; }
      }
      @keyframes steam-rise {
        0% { opacity: 0; transform: translateY(5px); }
        50% { opacity: 0.8; }
        100% { opacity: 0; transform: translateY(-10px); }
      }
      @keyframes sparkle {
        0%, 100% { opacity: 0.3; transform: scale(0.9); }
        50% { opacity: 1; transform: scale(1.1); }
      }
    mushroom-state-info$: |
      .container .primary {
        font-size: var(--config-font-primary) !important;
      }
      .container .secondary {
        font-size: var(--config-font-secondary) !important;
      }

```
</details>

<details>
<summary><strong>2 - Smart Washing Machine</summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.washing_machine_status
name: Smart Washing Machine
icon: mdi:washing-machine
primary_info: name
secondary_info: state
tap_action:
  action: more-info
icon_color: light-grey
fill_container: false
card_mod:
  style:
    .: |
      ha-card {
        /* ======================== */
        /* USER CONFIGURATION       */
        /* ======================== */
        
        /* 1. ENTITIES (Update these!) */
        {% set ent_status  = 'sensor.washing_machine_progress' %}
        {% set ent_timerem = 'sensor.washing_machine_time_remaining' %}
        {% set max_time = 120 %}
        {% set ent_power   = 'sensor.smart_plug_power' %}

        /* OPTIONAL Progress Percentage Sensor (if exists) */
        {% set ent_percent   = 'sensor.washing_machine_progress_percantage' %}

        /* 2. SIZES (Px) */
        --config-icon-size:       65px;
        --config-font-primary:    15px;
        --config-font-secondary:  12px;
        --config-font-badge:      12px;
        /* ======================== */

        /* --- SENSORS & TIME --- */
        {% set status = states(ent_status) %}
        {% set status_clean = status | replace('-', ' ') | title %}
        {% set time_rem = states(ent_timerem) | int(0) %}
        {% set raw_percent = states(ent_percent) | float(-1) %}

        /* --- POWER CALCULATION --- */
        {% set power_w = states(ent_power) | float(0) | round %}
        {% set power_text = ' • ' ~ power_w ~ 'W' if power_w > 0 else '' %}
        
        /* Format Time (min -> Xh Ym) */
        {% set hours = (time_rem / 60) | int %}
        {% set mins = time_rem % 60 %}
        {% set time_formatted = '%dh %02dm' | format(hours, mins) %}

        /* --- PROGRESS CALCULATION --- */
        
        {% if status | lower in ['idle', 'off', 'standby', 'unknown', 'unavailable'] %}
           {% set progress = 0 %}
           {% set badge_text = status_clean ~ power_text %}
        {% else %}
           
           /* LOGIC: Use Sensor if available, otherwise Calculate */
           {% if raw_percent >= 0 %}
              /* Use the sensor provided percentage */
              {% set progress = raw_percent | int %}
           {% else %}
              /* Fallback: Calculate based on fixed avg cycle (90m) */
              {% set max_cycle_time = max_time %}
              {% set calc_prog = ((max_cycle_time - time_rem) / max_cycle_time * 100) | int %}
              {% set progress = [5, [calc_prog, 100] | min] | max %}
           {% endif %}

           {% set badge_text = status_clean ~ ' • ' ~ time_formatted ~ power_text %}
        {% endif %}

        /* --- STATE DEFINITIONS --- */
        {% set s_lower = status | lower %}
        {% set is_running  = s_lower in ['wash', 'washing', 'rinse', 'rinsing', 'pre-wash', 'soak'] %}
        {% set is_spinning = s_lower in ['spin', 'spinning'] %}
        {% set is_drying   = s_lower in ['dry', 'drying'] %}
        {% set is_done     = s_lower in ['finished', 'complete', 'end'] %}

        /* --- ASSIGN ANIMATIONS --- */
        {% if is_drying %}
          {% set color = '255, 152, 0' %}   /* Orange */
          {% set anim_type = 'steam-rise 2s ease-in-out infinite' %}
          {% set icon_shake = 'none' %}
          {% set wave_anim = 'wave 4s linear infinite' %}
          {% set overlay_img = 'linear-gradient(0deg, transparent, rgba(255,255,255,0.5), transparent)' %}
        
        {% elif is_spinning %}
          {% set color = '0, 255, 255' %}   /* cyan */
          {% set anim_type = 'none' %}
          {% set icon_shake = 'washer-spin-smooth 0.8s linear infinite' %}
          {% set wave_anim = 'wave 2s linear infinite' %}          /* Fast Wave */
          {% set overlay_img = 'radial-gradient(circle, rgba(255,255,255,0.3) 10%, transparent 60%)' %}

        {% elif is_done %}
          {% set color = '76, 175, 80' %}   /* Green */
          {% set anim_type = 'sparkle 2s infinite' %}
          {% set icon_shake = 'none' %}
          {% set wave_anim = 'wave 4s linear infinite' %}
          {% set overlay_img = 'radial-gradient(circle, rgba(255,255,255,0.8) 10%, transparent 60%)' %}

        {% elif is_running %}
          {% set color = '33, 150, 243' %}   /* Blue */
          {% set anim_type = 'bubbles 1s linear infinite' %}
          {% set icon_shake = 'shake 1.5s ease-in-out infinite' %} /* Slow Shake */
          {% set wave_anim = 'wave 4s linear infinite' %}
          {% set overlay_img = 'radial-gradient(2px 2px at 20% 80%, white, transparent), radial-gradient(2px 2px at 50% 70%, white, transparent)' %}
        
        {% else %}
          {% set color = '158, 158, 158' %}  /* Grey */
          {% set anim_type = 'none' %}
          {% set icon_shake = 'none' %}
          {% set wave_anim = 'none' %}
          {% set overlay_img = 'none' %}
        {% endif %}

        /* --- OUTPUT VARIABLES --- */
        --wm-color: {{ color }};
        --wm-level: {{ progress }}%;
        --wm-anim-overlay: {{ anim_type }};
        --wm-anim-shake: {{ icon_shake }};
        --wm-anim-wave: {{ wave_anim }};
        --wm-overlay-bg: {{ overlay_img }};
        --wm-badge-content: "{{ badge_text }}";
        
        transition: all 0.5s ease;
        overflow: hidden;
      }

      /* BADGE */
      ha-card::before {
        content: var(--wm-badge-content);
        position: absolute;
        top: 10px; right: 10px;
        background: rgba(var(--wm-color), 0.15);
        color: rgb(var(--wm-color));
        border: 1px solid rgba(var(--wm-color), 0.3);
        padding: 2px 10px;
        border-radius: 12px;
        font-weight: 600;
        text-transform: uppercase;
        letter-spacing: 0.5px;
        font-size: var(--config-font-badge);
      }

      /* BAR */
      ha-card::after {
        content: '';
        position: absolute;
        bottom: 0; left: 0;
        height: 4px;
        width: var(--wm-level);
        background: rgb(var(--wm-color));
        box-shadow: 0 0 10px rgb(var(--wm-color));
        transition: width 0.5s ease;
      }
    mushroom-shape-icon$: |
      .shape {
        --icon-size: var(--config-icon-size) !important;
        background: rgba(255, 255, 255, 0.05) !important;
        overflow: hidden;
        position: relative;
        border: 1px solid rgba(255,255,255,0.1);
        
        /* Apply the animation determined by the Logic below */
        animation: var(--wm-anim-shake) !important;
        transform-origin: center center; 
      }

      /* Wave Layer */
      .shape::before {
        content: '';
        position: absolute;
        left: -50%;
        width: 200%; height: 200%;
        top: calc(100% - var(--wm-level));
        background: rgba(var(--wm-color), 0.6);
        border-radius: 40%;
        animation: var(--wm-anim-wave);
      }

      /* Overlay Layer (Bubbles/Steam) */
      .shape::after {
        content: '';
        position: absolute;
        inset: 0;
        background-image: var(--wm-overlay-bg);
        background-size: 100% 100%;
        animation: var(--wm-anim-overlay);
        z-index: 2;
      }

      /* The Icon Itself */
      ha-icon {
        z-index: 3;
        mix-blend-mode: overlay;
        color: white !important;
      }

      /* --- KEYFRAMES --- */
      @keyframes wave {
        from { transform: rotate(0deg); }
        to   { transform: rotate(360deg); }
      }
      @keyframes shake {
        0%, 100% { transform: rotate(0deg); }
        25% { transform: rotate(5deg) translateY(-1px); }
        75% { transform: rotate(-5deg) translateY(1px); }
      }
      @keyframes bubbles {
        0% { transform: translateY(10px); opacity: 0; }
        50% { opacity: 1; }
        100% { transform: translateY(-20px); opacity: 0; }
      }
      @keyframes steam-rise {
        0% { opacity: 0; transform: translateY(5px); }
        50% { opacity: 0.8; }
        100% { opacity: 0; transform: translateY(-10px); }
      }
      @keyframes sparkle {
        0%, 100% { opacity: 0.3; transform: scale(0.9); }
        50% { opacity: 1; transform: scale(1.1); }
      }

      @keyframes washer-spin-smooth {
        0% {
          transform: rotate(0deg) translate(0,0);
          box-shadow: inset 0 0 0 2px rgba(var(--wm-color), 0.7);
        }
        25% { transform: rotate(90deg) translate(0.5px, 0.5px); }
        50% { transform: rotate(180deg) translate(0,0); }
        75% { transform: rotate(270deg) translate(-0.5px, -0.5px); }
        100% {
          transform: rotate(360deg) translate(0,0);
          box-shadow: inset 0 0 0 2px rgba(var(--wm-color), 0.7);
        }
      }
    mushroom-state-info$: |
      .container .primary {
        font-size: var(--config-font-primary) !important;
      }
      .container .secondary {
        font-size: var(--config-font-secondary) !important;
      }

```
</details>

---

<details>
<summary><strong>3 - Dumb Dishwasher (smart plug)</summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.smart_plug_power
name: Dishwasher
icon: mdi:dishwasher
primary_info: name
secondary_info: state
tap_action:
  action: more-info
fill_container: false
icon_color: light-grey
card_mod:
  style:
    .: |
      ha-card {
        /* ======================== */
        /* USER CONFIGURATION       */
        /* ======================== */
        
        {% set ent_switch = 'switch.smart_plug' %} 
        {% set ent_power = 'sensor.smart_plug_power' %}
        
        /* Optional Helper (Leave as is if you don't have one) */
        {% set ent_helper = 'binary_sensor.dishwasher_active_delay' %}

        /* Thresholds */
        {% set thresh_heat = 1000 %}
        {% set thresh_active = 5 %}

        /* Sizes */
        --config-icon-size:      65px;
        --config-font-primary:   15px;
        --config-font-secondary: 12px;
        --config-font-badge:     11px;
        /* ======================== */

        /* --- DEFAULTS --- */
        {% set icon_shake = 'none' %}
        {% set anim_type = 'none' %}
        {% set wave_anim = 'none' %}
        {% set overlay_img = 'none' %}
        {% set level = 0 %}
        {% set badge_content = '' %}
        {% set time_str = '' %}
        {% set color = '158, 158, 158' %}

        /* --- DATA FETCHING --- */
        {% set power = states(ent_power) | float(0) | int %}
        {% set switch_state = states(ent_switch) %}
        {% set has_helper = states(ent_helper) not in ['unknown', 'unavailable', 'none'] %}
        
        /* --- SMART LOGIC --- */
        {% if has_helper %}
          /* Scenario A: Helper Exists */
          {% set status_bin = states(ent_helper) %}
        {% else %}
          /* Scenario B: Helper Missing (Fallback to Power) */
          {% set status_bin = 'on' if power > thresh_active else 'off' %}
        {% endif %}

        /* --- DURATION TIMER --- */
        {% if status_bin == 'on' and switch_state == 'on' %}
          {% if has_helper %}
             /* Precise Timer via Helper */
             {% set start_time = states[ent_helper].last_changed %}
             {% set seconds = as_timestamp(now()) - as_timestamp(start_time) %}
             {% set hours = (seconds / 3600) | int %}
             {% set mins = ((seconds % 3600) / 60) | int %}
             {% if seconds > 60 %}
                {% set time_str = '%dh %02dm' | format(hours, mins) %}
             {% else %}
                {% set time_str = 'Started' %}
             {% endif %}
          {% else %}
             /* No Helper - Just say Started */
             {% set time_str = 'Started' %}
          {% endif %}
        {% else %}
          {% set time_str = '' %}
        {% endif %}

        /* --- VISUAL STATE LOGIC --- */
        {% if switch_state == 'off' %}
           {% set status_text = 'Plug Off' %}
           {% set color = '244, 67, 54' %}       
           {% set badge_content = status_text %}

        {% elif switch_state in ['unavailable', 'unknown'] %}
           {% set status_text = 'Offline' %}
           {% set color = '158, 158, 158' %}    
           {% set badge_content = status_text %}

        {% elif status_bin == 'on' %}
           /* Machine is Active */
           {% if power > thresh_heat %}
             {% set status_text = 'Heating' %}
             {% set color = '255, 152, 0' %}       
             {% set anim_type = 'steam-rise 2s ease-in-out infinite' %}
             {% set overlay_img = 'linear-gradient(0deg, transparent, rgba(255,255,255,0.5), transparent)' %}
           {% else %}
             {% set status_text = 'Washing' %}
             {% set color = '33, 150, 243' %}      
             {% set anim_type = 'bubbles 1s linear infinite' %}
             {% set overlay_img = 'radial-gradient(2px 2px at 20% 80%, white, transparent), radial-gradient(2px 2px at 50% 70%, white, transparent)' %}
             {% set icon_shake = 'shake 0.8s ease-in-out infinite' %}
           {% endif %}
           
           {% set wave_anim = 'wave 4s linear infinite' %}
           {% set level = 60 %}
           {% set badge_content = status_text ~ " • " ~ power ~ " W" %}

        {% else %}
           /* --- IDLE STATE --- */
           {% set status_text = 'Idle' %}
           {% set color = '158, 158, 158' %}       
           {% set badge_content = status_text ~ " • " ~ power ~ " W" %}
        {% endif %}

        /* --- APPLY CSS VARIABLES --- */
        --dw-color: {{ color }};
        --dw-level: {{ level }}%;
        --dw-anim-overlay: {{ anim_type }};
        --dw-anim-shake: {{ icon_shake }};
        --dw-anim-wave: {{ wave_anim }};
        --dw-overlay-bg: {{ overlay_img }};
        --dw-badge-status: "{{ badge_content }}";
        
        /* Pass text AND display mode logic */
        --dw-time-text: "{{ time_str }}";
        --dw-time-display: {{ 'block' if time_str | length > 0 else 'none' }};
        
        transition: all 0.5s ease;
        overflow: hidden;
      }

      /* 1. STATUS BADGE (Top Right) */
      ha-card::before {
        content: var(--dw-badge-status);
        position: absolute;
        top: 8px; right: 10px;
        background: rgba(var(--dw-color), 0.15);
        color: rgb(var(--dw-color));
        border: 1px solid rgba(var(--dw-color), 0.3);
        padding: 2px 8px;
        border-radius: 10px;
        font-weight: 700;
        text-transform: uppercase;
        font-size: var(--config-font-badge);
        letter-spacing: 0.5px;
        z-index: 5;
      }

      /* 2. PROGRESS BAR */
      ha-card::after {
        content: '';
        position: absolute;
        bottom: 0; left: 0;
        height: 4px;
        width: var(--dw-level);
        background: rgb(var(--dw-color));
        box-shadow: 0 0 10px rgb(var(--dw-color));
        transition: width 0.5s ease;
        z-index: 1;
      }
    mushroom-state-info$: >
      .container .primary { font-size: var(--config-font-primary) !important; }
      .container .secondary { font-size: var(--config-font-secondary)
      !important; }

      .container::after {
        content: var(--dw-time-text);
        position: absolute;
        top: 40px; 
        right: 10px;
        color: var(--primary-text-color);
        background: rgba(var(--rgb-primary-text-color), 0.05);
        border: 1px solid rgba(var(--rgb-primary-text-color), 0.1);
        padding: 2px 8px;
        border-radius: 10px;
        font-weight: 700;
        font-size: var(--config-font-badge);
        letter-spacing: 0.5px;
        display: var(--dw-time-display);
      }
    mushroom-shape-icon$: >
      .shape {
        --icon-size: var(--config-icon-size) !important;
        background: rgba(255, 255, 255, 0.05) !important;
        overflow: hidden;
        position: relative;
        border: 1px solid rgba(255,255,255,0.1);
        animation: var(--dw-anim-shake) !important;
        transform-origin: 50% 60%; 
      } 

      .shape::before {
        content: '';
        position: absolute;
        left: -50%;
        width: 200%; height: 200%;
        top: calc(100% - var(--dw-level));
        background: rgba(var(--dw-color), 0.6);
        border-radius: 40%;
        animation: var(--dw-anim-wave);
      } 

      .shape::after {
        content: '';
        position: absolute;
        inset: 0;
        background-image: var(--dw-overlay-bg);
        background-size: 100% 100%;
        animation: var(--dw-anim-overlay);
        z-index: 2;
      } 

      ha-icon {
        z-index: 3;
        mix-blend-mode: overlay;
        color: white !important;
      }

      @keyframes wave { from { transform: rotate(0deg); } to { transform:
      rotate(360deg); } } @keyframes shake {
        0%, 100% { transform: rotate(0deg); }
        25% { transform: rotate(5deg) translateY(-1px); }
        75% { transform: rotate(-5deg) translateY(1px); }
      } @keyframes bubbles {
        0% { transform: translateY(10px); opacity: 0; }
        50% { opacity: 1; }
        100% { transform: translateY(-20px); opacity: 0; }
      } @keyframes steam-rise {
        0% { opacity: 0; transform: translateY(5px); }
        50% { opacity: 0.8; }
        100% { opacity: 0; transform: translateY(-10px); }
      }

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
          {{ states('sensor.smart_plug')|float(0) > 5 }}
        delay_off: "00:05:00"
        device_class: running
        icon: mdi:dishwasher
```
</details>

---

<details>
<summary><strong>4 - Dumb Washing Machine (smart plug)</summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.smart_plug_power
name: Washing Machine
icon: mdi:washing-machine
primary_info: name
secondary_info: state
tap_action:
  action: more-info
fill_container: false
icon_color: white
card_mod:
  style:
    .: |
      ha-card {
        /* ======================== */
        /* USER CONFIGURATION       */
        /* ======================== */
        
        {% set ent_switch = 'switch.smart_plug' %} 
        {% set ent_power = 'sensor.smart_plug_power' %}
        
        /* Optional Helper */
        {% set ent_helper = 'binary_sensor.washing_machine_active_delay' %}

        /* Thresholds */
        {% set thresh_spin = 300 %}
        {% set thresh_active = 5 %}

        /* Sizes */
        --config-icon-size:       65px;
        --config-font-primary:    15px;
        --config-font-secondary:  12px;
        --config-font-badge:      11px;
        /* ======================== */

        /* --- DEFAULTS --- */
        {% set icon_shake = 'none' %}
        {% set anim_type = 'none' %}
        {% set wave_anim = 'none' %}
        {% set overlay_img = 'none' %}
        {% set level = 0 %}
        {% set badge_content = '' %}
        {% set time_str = '' %}
        {% set color = '158, 158, 158' %}

        /* --- DATA FETCHING --- */
        {% set power = states(ent_power) | float(0) | int %}
        {% set switch_state = states(ent_switch) %}
        {% set has_helper = states(ent_helper) not in ['unknown', 'unavailable', 'none'] %}
        
        /* --- SMART LOGIC --- */
        {% if has_helper %}
          {% set status_bin = states(ent_helper) %}
        {% else %}
          /* Fallback: Active if power > 5W */
          {% set status_bin = 'on' if power > thresh_active else 'off' %}
        {% endif %}
        
        /* --- DURATION TIMER --- */
        {% if status_bin == 'on' and switch_state == 'on' %}
          {% if has_helper %}
             /* Scenario A: Precise Timer via Helper */
             {% set start_time = states[ent_helper].last_changed %}
             {% set seconds = as_timestamp(now()) - as_timestamp(start_time) %}
             {% set hours = (seconds / 3600) | int %}
             {% set mins = ((seconds % 3600) / 60) | int %}
             {% if seconds > 60 %}
                {% set time_str = '%dh %02dm' | format(hours, mins) %}
             {% else %}
                {% set time_str = 'Started' %}
             {% endif %}
          {% else %}
             /* Scenario B: No Helper - Just say Started */
             {% set time_str = 'Started' %}
          {% endif %}
        {% else %}
          {% set time_str = '' %}
        {% endif %}

        /* --- STATE LOGIC --- */
        {% if switch_state == 'off' %}
           {% set status_text = 'Plug Off' %}
           {% set color = '244, 67, 54' %}       
           {% set badge_content = status_text %}

        {% elif switch_state in ['unavailable', 'unknown'] %}
           {% set status_text = 'Offline' %}
           {% set color = '158, 158, 158' %}    
           {% set badge_content = status_text %}

        {% elif status_bin == 'on' %}
           /* --- HIGH POWER (SPINNING) --- */
           {% if power > thresh_spin %}
             {% set status_text = 'Spinning' %}
             {% set color = '0, 255, 255' %} 
             {% set anim_type = 'none' %}
             {% set overlay_img = 'none' %}
             {% set icon_shake = 'washer-spin-smooth 0.8s linear infinite' %} 
           
           /* --- NORMAL POWER (WASHING) --- */
           {% else %}
             {% set status_text = 'Washing' %}
             {% set color = '33, 150, 243' %}
             {% set anim_type = 'bubbles 2s linear infinite' %}
             {% set overlay_img = 'radial-gradient(2px 2px at 20% 80%, white, transparent), radial-gradient(2px 2px at 50% 70%, white, transparent)' %}
             {% set icon_shake = 'shake 2s ease-in-out infinite' %} 
           {% endif %}
           
           {% set wave_anim = 'wave 4s linear infinite' %}
           {% set level = 60 %}
           {% set badge_content = status_text ~ " • " ~ power ~ " W" %}

        {% else %}
           /* --- IDLE STATE --- */
           {% set status_text = 'Idle' %}
           {% set color = '158, 158, 158' %}       
           {% set badge_content = status_text ~ " • " ~ power ~ " W" %}
        {% endif %}

        /* --- OUTPUT VARIABLES --- */
        --wm-color: {{ color }};
        --wm-level: {{ level }}%;
        --wm-anim-overlay: {{ anim_type }};
        --wm-anim-shake: {{ icon_shake }};
        --wm-anim-wave: {{ wave_anim }};
        --wm-overlay-bg: {{ overlay_img }};
        --wm-badge-status: "{{ badge_content }}";
        
        --wm-time-text: "{{ time_str }}";
        --wm-time-display: {{ 'block' if time_str | length > 0 else 'none' }};
        
        transition: all 0.5s ease;
        overflow: hidden;
      }

      /* 1. STATUS BADGE */
      ha-card::before {
        content: var(--wm-badge-status);
        position: absolute;
        top: 8px; right: 10px;
        background: rgba(var(--wm-color), 0.15);
        color: rgb(var(--wm-color));
        border: 1px solid rgba(var(--wm-color), 0.3);
        padding: 2px 8px;
        border-radius: 10px;
        font-weight: 700;
        text-transform: uppercase;
        font-size: var(--config-font-badge);
        letter-spacing: 0.5px;
        z-index: 5;
      }

      /* 2. PROGRESS BAR */
      ha-card::after {
        content: '';
        position: absolute;
        bottom: 0; left: 0;
        height: 4px;
        width: var(--wm-level);
        background: rgb(var(--wm-color));
        box-shadow: 0 0 10px rgb(var(--wm-color));
        transition: width 0.5s ease;
        z-index: 1;
      }
    mushroom-state-info$: >
      .container .primary { font-size: var(--config-font-primary) !important; }
      .container .secondary { font-size: var(--config-font-secondary)
      !important; }

      .container::after {
        content: var(--wm-time-text);
        position: absolute;
        top: 40px; 
        right: 10px;
        color: var(--primary-text-color);
        background: rgba(var(--rgb-primary-text-color), 0.05);
        border: 1px solid rgba(var(--rgb-primary-text-color), 0.1);
        padding: 2px 8px;
        border-radius: 10px;
        font-weight: 700;
        font-size: var(--config-font-badge);
        letter-spacing: 0.5px;
        display: var(--wm-time-display);
      }
    mushroom-shape-icon$: >
      .shape {
        --icon-size: var(--config-icon-size) !important;
        background: rgba(255, 255, 255, 0.05) !important;
        overflow: hidden !important; 
        position: relative;
        border: 1px solid rgba(255,255,255,0.1);
        animation: var(--wm-anim-shake) !important;
        transform-origin: 50% 50%; 
      } 

      .shape::before {
        content: '';
        position: absolute;
        left: -50%;
        width: 200%; height: 200%;
        top: calc(100% - var(--wm-level));
        background: rgba(var(--wm-color), 0.6);
        border-radius: 40%;
        animation: var(--wm-anim-wave);
      } 

      .shape::after {
        content: '';
        position: absolute;
        inset: 0;
        background-image: var(--wm-overlay-bg);
        background-size: 100% 100%;
        animation: var(--wm-anim-overlay);
        z-index: 2;
      } 

      ha-icon {
        z-index: 3;
        mix-blend-mode: overlay;
        color: white !important;
      } 

      @keyframes wave { from { transform: rotate(0deg); } to { transform:
      rotate(360deg); } } @keyframes shake {
        0%, 100% { transform: rotate(0deg); }
        25% { transform: rotate(5deg) translateY(-1px); }
        75% { transform: rotate(-5deg) translateY(1px); }
      } 

      @keyframes bubbles {
        0% { transform: translateY(10px); opacity: 0; }
        50% { opacity: 1; }
        100% { transform: translateY(-20px); opacity: 0; }
      } 

      @keyframes washer-spin-smooth {
        0% {
          transform: rotate(0deg) translate(0,0);
          box-shadow: inset 0 0 0 2px rgba(var(--wm-color), 0.7);
        }
        25% { transform: rotate(90deg) translate(0.5px, 0.5px); }
        50% { transform: rotate(180deg) translate(0,0); }
        75% { transform: rotate(270deg) translate(-0.5px, -0.5px); }
        100% {
          transform: rotate(360deg) translate(0,0);
          box-shadow: inset 0 0 0 2px rgba(var(--wm-color), 0.7);
        }
      }

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
          {{ states('sensor.smart_plug')|float(0) > 5 }}
        delay_off: "00:05:00"
        device_class: running
        icon: mdi:washing-machine
```
</details>

---

<details>
<summary><strong>Smart and dumb Dryer cards (coming soon)</summary>

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
