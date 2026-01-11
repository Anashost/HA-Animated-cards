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

# 🏠 Home Assistant Animated Cards

> Take your Home Assistant dashboard to the next level with dynamic, customizable animated cards that bring your smart home dashboard to life.

| 📂 Category | 📝 Description | 🔗 Link |
| :--- | :--- | :---: |
| **🏠Home** | main collection| [**You are here**](./) |
| **🧺 Appliances** | washer, dryer, dishwasher, etc | [**View Page**](./appliances.md) |
| **🔋 Battery** | Battery level, charging animations | [**View Page**](./battery.md) |
| **📈 Graph Cards** | Temp, humidity, etc | [**View Page**](./env_with_graph.md) |

---

Those YouTube Videos
[Batch 1](https://youtu.be/5vYz37AqSO4) | [Batch 2](https://youtu.be/izx0JMrnhWE) | [Batch 3](https://youtu.be/SrFbC1ae35E) | [Batch 4](https://youtu.be/avAg9CR9TRc)
explains how to do it.

<hr>

## Batch 1:
![ezgif-8e9c11636a22c613](https://github.com/user-attachments/assets/4f5a1af0-d89b-4ed9-9c8c-36e678045580)
`Loading images... please wait`

## Batch 2:
![522590522-55a39df8-b28b-427b-8ec2-73221f6d154b](https://github.com/user-attachments/assets/65ba4a4e-bed4-4ee1-8735-03e2bfd67db6)

## Batch 3:
![gif-16c233439b5ca922-2](https://github.com/user-attachments/assets/8acdc17a-abc0-41dc-80c3-929c5b1fa2b6)

## Batch 4:
![gif-2](https://github.com/user-attachments/assets/a7c3671a-11bd-4725-9765-536dbc835220)


# Cards:

<details>
  <summary><strong>1 - smartplug</summary>

  ```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
   action: toggle
icon: mdi:power-plug
icon_color: green
name: Smart Plug
grid_options:
  rows: 1.4
card_mod:
	  style:
	    mushroom-shape-icon$: |
	      .shape {
	        {# ========== USER CONFIG ========== #}
	        {# true = number mode, false = state mode #}
	        {% set use_number      = false %}
	
	        {# STATE MODE SETTINGS #}
	        {% set state_entity    = 'switch.plug_6_local' %}
	        {% set active_value    = 'on' %}
	
	        {# OPTIONAL: NUMBER MODE SETTINGS #}
	        {% set number_entity   = 'sensor.plug_power' %}
	        
	        {# '>' '<' '=' '>=' '<=' #}
	        {% set number_operator = '>' %}
	        
	        {% set threshold       = 0.0 %}
	        {# ========== END USER CONFIG ====== #}
	
	        {# ======== TRIGGER DECISION LOGIC ======== #}
	        {% if use_number %}
	          {% set num = states(number_entity) | float(0) %}
	          
	          {# Evaluate numeric rule #}
	          {% if number_operator == '>' %}
	            {% set trigger_active = (num > threshold) %}
	          {% elif number_operator == '<' %}
	            {% set trigger_active = (num < threshold) %}
	          {% elif number_operator == '=' %}
	            {% set trigger_active = (num == threshold) %}
	          {% elif number_operator == '>=' %}
	            {% set trigger_active = (num >= threshold) %}
	          {% elif number_operator == '<=' %}
	            {% set trigger_active = (num <= threshold) %}
	          {% else %}
	            {% set trigger_active = false %}
	          {% endif %}
	
	        {% else %}
	          {# State mode #}
	          {% if states(state_entity) == active_value %}
	            {% set trigger_active = true %}
	          {% else %}
	            {% set trigger_active = false %}
	          {% endif %}
	        {% endif %}
	        {# =========== END TRIGGER LOGIC =========== #}
	
	        {% if trigger_active %}
	          --shape-animation: ring-breathe 1.8s ease-out infinite;
	          opacity: 1;
	        {% else %}
	          --shape-animation: none;
	          opacity: 0.7;
	        {% endif %}
	      }
	
	      @keyframes ring-breathe {
	        0%   { box-shadow: 0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9); }
	        70%  { box-shadow: 0 0 0 14px rgba(var(--rgb-{{ config.icon_color }}), 0.0); }
	        100% { box-shadow: 0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.0); }
	      }
	    .: |
	      mushroom-shape-icon {
	        --icon-size: 65px;
	        display: flex;
	        margin: -18px 0 10px -20px !important;
	        padding-right: 10px;
	      }
	      ha-card {
	        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
	      }

  ```
</details>

<details>
  <summary><strong>2 - Charger</summary>

  ```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
   action: toggle
icon: mdi:power-socket-au
icon_color: green
name: Charger
grid_options:
  rows: 1.4
card_mod:
	  style:
	    mushroom-shape-icon$: |
	      .shape {
	        {# ========== USER CONFIG ========== #}
	        {# true = number mode, false = state mode #}
	        {% set use_number      = false %}
	
	        {# STATE MODE SETTINGS #}
	        {% set state_entity    = 'switch.plug_6_local' %}
	        {% set active_value    = 'on' %}
	
	        {# OPTIONAL: NUMBER MODE SETTINGS #}
	        {% set number_entity   = 'sensor.plug_power' %}
	        
	        {# '>' '<' '=' '>=' '<=' #}
	        {% set number_operator = '>' %}
	        
	        {% set threshold       = 0.0 %}
	        {# ========== END USER CONFIG ====== #}
	
	        {# ======== TRIGGER DECISION LOGIC ======== #}
	        {% if use_number %}
	          {% set num = states(number_entity) | float(0) %}
	
	          {% if number_operator == '>' %}
	            {% set trigger_active = (num > threshold) %}
	          {% elif number_operator == '<' %}
	            {% set trigger_active = (num < threshold) %}
	          {% elif number_operator == '=' %}
	            {% set trigger_active = (num == threshold) %}
	          {% elif number_operator == '>=' %}
	            {% set trigger_active = (num >= threshold) %}
	          {% elif number_operator == '<=' %}
	            {% set trigger_active = (num <= threshold) %}
	          {% else %}
	            {% set trigger_active = false %}
	          {% endif %}
	        {% else %}
	          {% set trigger_active = (states(state_entity) == active_value) %}
	        {% endif %}
	        {# =========== END TRIGGER LOGIC =========== #}
	
	        {% if trigger_active %}
	          {# adjust speed based on this plug's own power attribute #}
	          {% set p = state_attr(config.entity, 'current_power_w') | float(0) %}
	          {% set dur = 1.6 - (p / 800) %}
	          --shape-animation: ultra-plug-on {{ [0.4, dur] | max | round(2) }}s ease-in-out infinite;
	          --plug-glow-animation: ultra-plug-glow 1.8s ease-in-out infinite;
	          --plug-arcs-animation: ultra-plug-arcs 1.2s linear infinite;
	          opacity: 1;
	        {% else %}
	          --shape-animation: none;
	          --plug-glow-animation: none;
	          --plug-arcs-animation: none;
	          opacity: 0.7;
	        {% endif %}
	
	        transform-origin: 50% 50%;
	        position: relative;
	      }
	
	      .shape::before,
	      .shape::after {
	        content: '';
	        position: absolute;
	        inset: -4px;
	        border-radius: inherit;
	        pointer-events: none;
	      }
	
	      .shape::before {
	        animation: var(--plug-glow-animation);
	      }
	
	      .shape::after {
	        animation: var(--plug-arcs-animation);
	      }
	
	      @keyframes ultra-plug-on {
	        0%   { transform: scale(1); }
	        25%  { transform: scale(1.05) translateY(-1px); }
	        50%  { transform: scale(1.08) translateY(-2px); }
	        75%  { transform: scale(1.04) translateY(-1px); }
	        100% { transform: scale(1); }
	      }
	
	      @keyframes ultra-plug-glow {
	        0% {
	          box-shadow:
	            0 0 10px 3px rgba(var(--rgb-{{ config.icon_color }}), 0.6),
	            0 0 20px 8px rgba(var(--rgb-{{ config.icon_color }}), 0.3);
	        }
	        50% {
	          box-shadow:
	            0 0 18px 6px rgba(var(--rgb-{{ config.icon_color }}), 0.9),
	            0 0 32px 12px rgba(var(--rgb-{{ config.icon_color }}), 0.4);
	        }
	        100% {
	          box-shadow:
	            0 0 10px 3px rgba(var(--rgb-{{ config.icon_color }}), 0.6),
	            0 0 20px 8px rgba(var(--rgb-{{ config.icon_color }}), 0.3);
	        }
	      }
	
	      @keyframes ultra-plug-arcs {
	        0% {
	          box-shadow:
	            -10px -6px 0 -4px rgba(var(--rgb-{{ config.icon_color }}), 0.0),
	            12px 4px 0 -4px rgba(var(--rgb-{{ config.icon_color }}), 0.0);
	        }
	        25% {
	          box-shadow:
	            -10px -6px 0 -4px rgba(var(--rgb-{{ config.icon_color }}), 0.7),
	            12px 4px 0 -4px rgba(var(--rgb-{{ config.icon_color }}), 0.4);
	        }
	        50% {
	          box-shadow:
	            -6px 2px 0 -4px rgba(var(--rgb-{{ config.icon_color }}), 0.3),
	            10px -8px 0 -4px rgba(var(--rgb-{{ config.icon_color }}), 0.7);
	        }
	        75% {
	          box-shadow:
	            -12px 4px 0 -4px rgba(var(--rgb-{{ config.icon_color }}), 0.5),
	            8px 0 0 -4px rgba(var(--rgb-{{ config.icon_color }}), 0.2);
	        }
	        100% {
	          box-shadow:
	            -10px -6px 0 -4px rgba(var(--rgb-{{ config.icon_color }}), 0.0),
	            12px 4px 0 -4px rgba(var(--rgb-{{ config.icon_color }}), 0.0);
	        }
	      }
	    .: |
	      mushroom-shape-icon {
	        --icon-size: 65px;
	        display: flex;
	        margin: -18px 0 10px -20px !important;
	        padding-right: 10px;
	      }
	      ha-card {
	        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
	      }

  ```
</details>

<details>
  <summary><strong>3 - Fan</summary>

  ```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
   action: toggle
icon: mdi:fan
icon_color: blue
name: Fan
grid_options:
  rows: 1.4
card_mod:
	  style:
	    mushroom-shape-icon$: |
	      .shape {
	        {# ========== USER CONFIG ========== #}
	        {# true = number mode, false = state mode #}
	        {% set use_number      = false %}
	
	        {# STATE MODE SETTINGS #}
	        {% set state_entity    = 'switch.plug_6_local' %}
	        {% set active_value    = 'on' %}
	
	        {# OPTIONAL: NUMBER MODE SETTINGS #}
	        {% set number_entity   = 'sensor.plug_power' %}
	        
	        {# '>' '<' '=' '>=' '<=' #}
	        {% set number_operator = '>' %}
	        
	        {% set threshold       = 0.0 %}
	        {# ========== END USER CONFIG ====== #}
	
	        {# ======== TRIGGER DECISION LOGIC ======== #}
	        {% if use_number %}
	          {% set num = states(number_entity) | float(0) %}
	          {% if number_operator == '>' %}
	            {% set trigger_active = (num > threshold) %}
	          {% elif number_operator == '<' %}
	            {% set trigger_active = (num < threshold) %}
	          {% elif number_operator == '=' %}
	            {% set trigger_active = (num == threshold) %}
	          {% elif number_operator == '>=' %}
	            {% set trigger_active = (num >= threshold) %}
	          {% elif number_operator == '<=' %}
	            {% set trigger_active = (num <= threshold) %}
	          {% else %}
	            {% set trigger_active = false %}
	          {% endif %}
	        {% else %}
	          {% set trigger_active = (states(state_entity) == active_value) %}
	        {% endif %}
	        {# =========== END TRIGGER LOGIC =========== #}
	
	        {% if trigger_active %}
	          {# Fan speed logic based on THIS card's entity #}
	          {% if is_state(config.entity, 'on') %}
	            --shape-animation: fan-turbine 0.5s linear infinite;
	            opacity: 1;
	          {% elif is_state(config.entity, 'medium') %}
	            --shape-animation: fan-turbine 0.8s linear infinite;
	            opacity: 1;
	          {% elif is_state(config.entity, 'low') %}
	            --shape-animation: fan-turbine 1.2s linear infinite;
	            opacity: 1;
	          {% else %}
	            --shape-animation: fan-rock 2.4s ease-in-out infinite;
	            opacity: 0.7;
	          {% endif %}
	        {% else %}
	          --shape-animation: none;
	          opacity: 0.7;
	        {% endif %}
	
	        transform-origin: 50% 50%;
	        position: relative;
	        box-shadow:
	          0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.6),
	          0 0 0 6px rgba(var(--rgb-{{ config.icon_color }}), 0.08),
	          0 0 18px 0 rgba(var(--rgb-{{ config.icon_color }}), 0.7);
	      }
	
	      @keyframes fan-turbine {
	        0% {
	          transform: rotate(0deg) scale(1);
	          filter: drop-shadow(0 0 3px rgba(var(--rgb-{{ config.icon_color }}), 0.9));
	        }
	        25% {
	          transform: rotate(90deg) scale(1.02);
	        }
	        50% {
	          transform: rotate(180deg) scale(1.04);
	          filter: drop-shadow(0 0 8px rgba(var(--rgb-{{ config.icon_color }}), 1));
	        }
	        75% {
	          transform: rotate(270deg) scale(1.02);
	        }
	        100% {
	          transform: rotate(360deg) scale(1);
	          filter: drop-shadow(0 0 3px rgba(var(--rgb-{{ config.icon_color }}), 0.9));
	        }
	      }
	
	      @keyframes fan-rock {
	        0%   { transform: rotate(-4deg); }
	        50%  { transform: rotate(4deg); }
	        100% { transform: rotate(-4deg); }
	      }
	    .: |
	      mushroom-shape-icon {
	        --icon-size: 65px;
	        display: flex;
	        margin: -18px 0 10px -20px !important;
	        padding-right: 10px;
	      }
	      ha-card {
	        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
	      }

  ```
</details>

<details>
  <summary><strong>4 - Fan</summary>

  ```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
   action: toggle
icon: mdi:fan
icon_color: cyan
name: Fan
grid_options:
  rows: 1.4
card_mod:
	  style:
	    mushroom-shape-icon$: |
	      .shape {
	        {# ========== USER CONFIG ========== #}
	        {# true = number mode, false = state mode #}
	        {% set use_number      = false %}
	
	        {# STATE MODE SETTINGS #}
	        {% set state_entity    = 'switch.plug_6_local' %}
	        {% set active_value    = 'on' %}
	
	        {# OPTIONAL: NUMBER MODE SETTINGS #}
	        {% set number_entity   = 'sensor.plug_power' %}
	        
	        {# '>' '<' '=' '>=' '<=' #}
	        {% set number_operator = '>' %}
	        
	        {% set threshold       = 0.0 %}
	        {# ========== END USER CONFIG ====== #}
	
	        {# -------- TRIGGER DECISION LOGIC -------- #}
	        {% if use_number %}
	          {% set num = states(number_entity) | float(0) %}
	          {% if number_operator == '>' %}
	            {% set trigger_active = (num > threshold) %}
	          {% elif number_operator == '<' %}
	            {% set trigger_active = (num < threshold) %}
	          {% elif number_operator == '=' %}
	            {% set trigger_active = (num == threshold) %}
	          {% elif number_operator == '>=' %}
	            {% set trigger_active = (num >= threshold) %}
	          {% elif number_operator == '<=' %}
	            {% set trigger_active = (num <= threshold) %}
	          {% else %}
	            {% set trigger_active = false %}
	          {% endif %}
	        {% else %}
	          {% set sensor_entity = state_entity %}
	          {% if states(sensor_entity) == active_value %}
	            {% set trigger_active = true %}
	          {% else %}
	            {% set trigger_active = false %}
	          {% endif %}
	        {% endif %}
	        {# ------ END TRIGGER DECISION LOGIC ------ #}
	
	        {# Fan speed still based on THIS card's entity percentage #}
	        {% set speed = state_attr(config.entity, 'percentage') | int(0) %}
	
	        {% if trigger_active %}
	          {% if speed == 0 and is_state(config.entity, 'off') %}
	            --shape-animation: fan-ultra-idle 3s ease-in-out infinite;
	          {% else %}
	            {% set dur = 1.2 - (speed / 120) %}
	            --shape-animation: fan-ultra-spin {{ [0.25, dur] | max | round(2) }}s linear infinite;
	          {% endif %}
	          --fan-warp-animation: fan-warp 1.4s ease-in-out infinite;
	          --fan-stream-animation: fan-stream 1.6s ease-in-out infinite;
	          opacity: 1;
	        {% else %}
	          --shape-animation: none;
	          --fan-warp-animation: none;
	          --fan-stream-animation: none;
	          opacity: 0.7;
	        {% endif %}
	
	        transform-origin: 50% 50%;
	        position: relative;
	      }
	
	      .shape::before,
	      .shape::after {
	        content: '';
	        position: absolute;
	        inset: 0;
	        border-radius: inherit;
	        pointer-events: none;
	      }
	
	      .shape::before {
	        animation: var(--fan-warp-animation);
	      }
	
	      .shape::after {
	        mix-blend-mode: screen;
	        animation: var(--fan-stream-animation);
	      }
	
	      @keyframes fan-ultra-spin {
	        0% {
	          transform: rotate(0deg) scale(1);
	          filter: drop-shadow(0 0 3px rgba(var(--rgb-{{ config.icon_color }}), 0.8));
	        }
	        20% { transform: rotate(72deg) scale(1.03); }
	        40% { transform: rotate(144deg) scale(1.05); }
	        60% { transform: rotate(216deg) scale(1.03); }
	        80% { transform: rotate(288deg) scale(1.02); }
	        100% {
	          transform: rotate(360deg) scale(1);
	          filter: drop-shadow(0 0 5px rgba(var(--rgb-{{ config.icon_color }}), 1));
	        }
	      }
	
	      @keyframes fan-ultra-idle {
	        0%   { transform: rotate(-6deg); }
	        50%  { transform: rotate(6deg); }
	        100% { transform: rotate(-6deg); }
	      }
	
	      @keyframes fan-warp {
	        0% {
	          box-shadow:
	            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.7),
	            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.25);
	        }
	        40% {
	          box-shadow:
	            0 0 0 8px rgba(var(--rgb-{{ config.icon_color }}), 0.4),
	            0 0 24px 6px rgba(var(--rgb-{{ config.icon_color }}), 0.25);
	        }
	        100% {
	          box-shadow:
	            0 0 0 18px rgba(var(--rgb-{{ config.icon_color }}), 0.0),
	            0 0 40px 12px rgba(var(--rgb-{{ config.icon_color }}), 0.0);
	        }
	      }
	
	      @keyframes fan-stream {
	        0% {
	          box-shadow:
	            20px 0 16px -12px rgba(var(--rgb-{{ config.icon_color }}), 0),
	            -20px 0 16px -12px rgba(var(--rgb-{{ config.icon_color }}), 0);
	        }
	        50% {
	          box-shadow:
	            24px 0 20px -10px rgba(var(--rgb-{{ config.icon_color }}), 0.6),
	            -24px 0 20px -10px rgba(var(--rgb-{{ config.icon_color }}), 0.4);
	        }
	        100% {
	          box-shadow:
	            20px 0 16px -12px rgba(var(--rgb-{{ config.icon_color }}), 0),
	            -20px 0 16px -12px rgba(var(--rgb-{{ config.icon_color }}), 0);
	        }
	      }
	    .: |
	      mushroom-shape-icon {
	        --icon-size: 65px;
	        display: flex;
	        margin: -18px 0 10px -20px !important;
	        padding-right: 10px;
	      }
	      ha-card {
	        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
	      }

  ```
</details>

<details>
  <summary><strong>5 - Fan</summary>

  ```yaml
type: custom:mushroom-fan-card
entity: fan.living_room_fan
show_percentage_control: true
show_oscillate_control: true
show_direction_control: true
collapsible_controls: false
fill_container: false
icon_animation: false
icon_type: icon
card_mod:
	  style:
	    mushroom-shape-icon$: |
	      .shape {
	        {# ========= COLOR CONFIG ========= #}
	        {# change to 'blue', 'red', 'purple', etc. #}
	        {% set fan_color = 'green' %}
	        --fan-color-rgb: var(--rgb-{{ fan_color }});
	        {# ================================ #}
	
	        {# ========== USER CONFIG ========== #}
	        {% set use_number      = false %}
	
	        {# STATE MODE SETTINGS #}
	        {% set state_entity    = 'fan.living_room_fan' %}
	        {% set active_value    = 'on' %}
	
	        {# OPTIONAL: NUMBER MODE SETTINGS #}
	        {% set number_entity   = 'sensor.plug_power' %}
	        {% set number_operator = '>' %}
	        {% set threshold       = 0.0 %}
	        {# ========== END USER CONFIG ====== #}
	
	        {# -------- TRIGGER DECISION LOGIC -------- #}
	        {% if use_number %}
	          {% set num = states(number_entity) | float(0) %}
	          {% if number_operator == '>' %}
	            {% set trigger_active = (num > threshold) %}
	          {% elif number_operator == '<' %}
	            {% set trigger_active = (num < threshold) %}
	          {% elif number_operator == '=' %}
	            {% set trigger_active = (num == threshold) %}
	          {% elif number_operator == '>=' %}
	            {% set trigger_active = (num >= threshold) %}
	          {% elif number_operator == '<=' %}
	            {% set trigger_active = (num <= threshold) %}
	          {% else %}
	            {% set trigger_active = false %}
	          {% endif %}
	        {% else %}
	          {% set sensor_entity = state_entity %}
	          {% if states(sensor_entity) == active_value %}
	            {% set trigger_active = true %}
	          {% else %}
	            {% set trigger_active = false %}
	          {% endif %}
	        {% endif %}
	        {# ------ END TRIGGER DECISION LOGIC ------ #}
	
	        {# Fan speed still based on THIS card's entity percentage #}
	        {% set speed = state_attr(config.entity, 'percentage') | int(0) %}
	
	        {% if trigger_active %}
	          {% if speed == 0 and is_state(config.entity, 'off') %}
	            --shape-animation: fan-ultra-idle 3s ease-in-out infinite;
	          {% else %}
	            {% set dur = 1.2 - (speed / 120) %}
	            --shape-animation: fan-ultra-spin {{ [0.25, dur] | max | round(2) }}s linear infinite;
	          {% endif %}
	          --fan-warp-animation: fan-warp 1.4s ease-in-out infinite;
	          --fan-stream-animation: fan-stream 1.6s ease-in-out infinite;
	          opacity: 1;
	        {% else %}
	          --shape-animation: none;
	          --fan-warp-animation: none;
	          --fan-stream-animation: none;
	          opacity: 0.7;
	        {% endif %}
	
	        transform-origin: 50% 50%;
	        position: relative;
	      }
	
	      .shape::before,
	      .shape::after {
	        content: '';
	        position: absolute;
	        inset: 0;
	        border-radius: inherit;
	        pointer-events: none;
	      }
	
	      .shape::before {
	        animation: var(--fan-warp-animation);
	      }
	
	      .shape::after {
	        mix-blend-mode: screen;
	        animation: var(--fan-stream-animation);
	      }
	
	      @keyframes fan-ultra-spin {
	        0% {
	          transform: rotate(0deg) scale(1);
	          filter: drop-shadow(0 0 3px rgba(var(--fan-color-rgb), 0.8));
	        }
	        20% { transform: rotate(72deg) scale(1.03); }
	        40% { transform: rotate(144deg) scale(1.05); }
	        60% { transform: rotate(216deg) scale(1.03); }
	        80% { transform: rotate(288deg) scale(1.02); }
	        100% {
	          transform: rotate(360deg) scale(1);
	          filter: drop-shadow(0 0 5px rgba(var(--fan-color-rgb), 1));
	        }
	      }
	
	      @keyframes fan-ultra-idle {
	        0%   { transform: rotate(-6deg); }
	        50%  { transform: rotate(6deg); }
	        100% { transform: rotate(-6deg); }
	      }
	
	      @keyframes fan-warp {
	        0% {
	          box-shadow:
	            0 0 0 0 rgba(var(--fan-color-rgb), 0.7),
	            0 0 0 0 rgba(var(--fan-color-rgb), 0.25);
	        }
	        40% {
	          box-shadow:
	            0 0 0 8px rgba(var(--fan-color-rgb), 0.4),
	            0 0 24px 6px rgba(var(--fan-color-rgb), 0.25);
	        }
	        100% {
	          box-shadow:
	            0 0 0 18px rgba(var(--fan-color-rgb), 0.0),
	            0 0 40px 12px rgba(var(--fan-color-rgb), 0.0);
	        }
	      }
	
	      @keyframes fan-stream {
	        0% {
	          box-shadow:
	            20px 0 16px -12px rgba(var(--fan-color-rgb), 0),
	           -20px 0 16px -12px rgba(var(--fan-color-rgb), 0);
	        }
	        50% {
	          box-shadow:
	            24px 0 20px -10px rgba(var(--fan-color-rgb), 0.6),
	           -24px 0 20px -10px rgba(var(--fan-color-rgb), 0.4);
	        }
	        100% {
	          box-shadow:
	            20px 0 16px -12px rgba(var(--fan-color-rgb), 0),
	           -20px 0 16px -12px rgba(var(--fan-color-rgb), 0);
	        }
	      }
	    .: |
	      mushroom-shape-icon {
	        --icon-size: 65px;
	        display: flex;
	        margin: -18px 0 10px -20px !important;
	        padding-right: 10px;
	      }
	      ha-card {
	        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
	      }

  ```
</details>

<details>
  <summary><strong>6 - Lock</summary>

  ```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
   action: toggle
icon: mdi:lock
icon_color: red
name: Lock
grid_options:
  rows: 1.4
card_mod:
	  style:
	    mushroom-shape-icon$: |
	      .shape {
	        {# ========== USER CONFIG ========== #}
	        {# true = number mode, false = state mode #}
	        {% set use_number      = false %}
	
	        {# STATE MODE SETTINGS #}
	        {% set state_entity    = 'switch.plug_6_local' %}
	        {% set active_value    = 'on' %}
	
	        {# OPTIONAL: NUMBER MODE SETTINGS #}
	        {% set number_entity   = 'sensor.plug_power' %}
	        
	        {# '>' '<' '=' '>=' '<=' #}
	        {% set number_operator = '>' %}
	        
	        {% set threshold       = 0.0 %}
	        {# ========== END USER CONFIG ====== #}
	
	        {# ---------- TRIGGER DECISION LOGIC ---------- #}
	        {% if use_number %}
	          {% set num = states(number_entity) | float(0) %}
	          {% if number_operator == '>' %}
	            {% set trigger_active = (num > threshold) %}
	          {% elif number_operator == '<' %}
	            {% set trigger_active = (num < threshold) %}
	          {% elif number_operator == '=' %}
	            {% set trigger_active = (num == threshold) %}
	          {% elif number_operator == '>=' %}
	            {% set trigger_active = (num >= threshold) %}
	          {% elif number_operator == '<=' %}
	            {% set trigger_active = (num <= threshold) %}
	          {% else %}
	            {% set trigger_active = false %}
	          {% endif %}
	        {% else %}
	          {% set trigger_active = (states(state_entity) == active_value) %}
	        {% endif %}
	        {# ---------- END TRIGGER LOGIC ---------- #}
	
	
	        {% if trigger_active %}
	          {% if is_state(config.entity, 'locked') %}
	            --shape-animation: lock-secure 2.3s ease-in-out infinite;
	          {% elif is_state(config.entity, 'unlocking') or is_state(config.entity, 'locking') %}
	            --shape-animation: lock-action 0.7s ease-in-out infinite;
	          {% else %}
	            --shape-animation: lock-open 1.6s ease-in-out infinite;
	          {% endif %}
	
	          opacity: 1;
	
	          /* HUGE glow system */
	          --glow-1: 0 0 25px 8px rgba(var(--rgb-{{ config.icon_color }}), 1);
	          --glow-2: 0 0 55px 18px rgba(var(--rgb-{{ config.icon_color }}), 0.7);
	          --glow-3: 0 0 95px 35px rgba(var(--rgb-{{ config.icon_color }}), 0.45);
	          --glow-anim: lock-ultraglow 2.2s ease-in-out infinite;
	
	        {% else %}
	          --shape-animation: none;
	          --glow-1: none;
	          --glow-2: none;
	          --glow-3: none;
	          --glow-anim: none;
	          opacity: 0.6;
	        {% endif %}
	
	        transform-origin: 50% 50%;
	        position: relative;
	      }
	
	      /* Glow layers */
	      .shape::before,
	      .shape::after {
	        content: '';
	        position: absolute;
	        inset: -8px;
	        border-radius: inherit;
	        pointer-events: none;
	      }
	
	      .shape::before {
	        box-shadow: var(--glow-1), var(--glow-2), var(--glow-3);
	        animation: var(--glow-anim);
	      }
	
	      .shape::after {
	        inset: -18px;
	        box-shadow: 0 0 120px 40px rgba(var(--rgb-{{ config.icon_color }}), 0.25);
	        opacity: 0.9;
	        animation: var(--glow-anim);
	      }
	
	      @keyframes lock-ultraglow {
	        0% {
	          opacity: 0.9;
	          filter: brightness(1);
	        }
	        50% {
	          opacity: 1;
	          filter: brightness(1.4);
	        }
	        100% {
	          opacity: 0.9;
	          filter: brightness(1);
	        }
	      }
	
	      @keyframes lock-secure {
	        0%   { transform: rotate(0deg) scale(1); }
	        15%  { transform: rotate(-12deg) scale(1.02); }
	        30%  { transform: rotate(2deg) scale(1.03); }
	        40%  { transform: rotate(0deg) scale(1); }
	        100% { transform: rotate(0deg) scale(1); }
	      }
	
	      @keyframes lock-action {
	        0%   { transform: rotate(-25deg) scale(0.96); }
	        50%  { transform: rotate(25deg) scale(1.04); }
	        100% { transform: rotate(-25deg) scale(0.96); }
	      }
	
	      @keyframes lock-open {
	        0%   { transform: rotate(10deg); }
	        50%  { transform: rotate(18deg); }
	        100% { transform: rotate(10deg); }
	      }
	    .: |
	      mushroom-shape-icon {
	        --icon-size: 65px;
	        display: flex;
	        margin: -18px 0 10px -20px !important;
	        padding-right: 20px;
	      }
	      ha-card {
	        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
	      }

  ```
</details>

<details>
<summary><strong>7 - Projector</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:projector
icon_color: accent
name: Projector
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: proj-ultra 1.7s ease-in-out infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.65;
        {% endif %}

        transform-origin: 30% 50%;
        position: relative;
      }

      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        inset: -6px;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        background:
          radial-gradient(circle at 20% 50%, rgba(255,255,255,0.6), transparent 55%);
        transform-origin: 20% 50%;
        {% if trigger_active %}
          opacity: 0.8;
          animation: proj-beam 1.7s ease-in-out infinite;
          filter: blur(1px);
        {% else %}
          opacity: 0;           /* hide beam completely */
          animation: none;
          filter: none;
        {% endif %}
      }

      .shape::after {
        {% if trigger_active %}
          animation: proj-focus 1.2s ease-in-out infinite;
        {% else %}
          animation: none;
          box-shadow: none;     /* kill leftover glow */
        {% endif %}
      }

      @keyframes proj-ultra {
        0%   { transform: translateX(0) scale(1); }
        25%  { transform: translateX(1px) scale(1.02); }
        50%  { transform: translateX(0) scale(1.03); }
        75%  { transform: translateX(-1px) scale(1.02); }
        100% { transform: translateX(0) scale(1); }
      }

      @keyframes proj-standby {
        0%   { transform: scale(1); }
        50%  { transform: scale(1.02); }
        100% { transform: scale(1); }
      }

      @keyframes proj-beam {
        0% {
          opacity: 0.7;
          filter: blur(1px);
          transform: scaleX(1) scaleY(1);
        }
        50% {
          opacity: 1;
          filter: blur(0.5px);
          transform: scaleX(1.15) scaleY(1.05);
        }
        100% {
          opacity: 0.7;
          filter: blur(1px);
          transform: scaleX(1) scaleY(1);
        }
      }

      @keyframes proj-focus {
        0% {
          box-shadow:
            0 0 10px 3px rgba(var(--rgb-{{ config.icon_color }}), 0.7);
        }
        50% {
          box-shadow:
            0 0 20px 8px rgba(var(--rgb-{{ config.icon_color }}), 1);
        }
        100% {
          box-shadow:
            0 0 10px 3px rgba(var(--rgb-{{ config.icon_color }}), 0.7);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }


```
</details>

<details>
<summary><strong>8 - Doorbell</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:bell
icon_color: red
name: Doorbell
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}


        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {# default: simple equality state trigger #}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}


        {% if trigger_active %}
          --shape-animation: doorbell-ring 0.9s ease-out infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.8;
        {% endif %}

        transform-origin: 50% 50%;
      }

      @keyframes doorbell-ring {
        0% {
          transform: scale(1.05);
          box-shadow:
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 1),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.8),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.4);
        }
        30% {
          transform: scale(0.95);
          box-shadow:
            0 0 0 4px  rgba(var(--rgb-{{ config.icon_color }}), 0.9),
            0 0 0 10px rgba(var(--rgb-{{ config.icon_color }}), 0.7),
            0 0 0 18px rgba(var(--rgb-{{ config.icon_color }}), 0.4);
        }
        60% {
          transform: scale(1.02);
          box-shadow:
            0 0 0 10px rgba(var(--rgb-{{ config.icon_color }}), 0.0),
            0 0 0 18px rgba(var(--rgb-{{ config.icon_color }}), 0.2),
            0 0 0 26px rgba(var(--rgb-{{ config.icon_color }}), 0.0);
        }
        100% {
          transform: scale(1);
          box-shadow:
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.0),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.0),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.0);
        }
      }

      @keyframes doorbell-idle {
        0%   { transform: scale(1); }
        50%  { transform: scale(1.03); }
        100% { transform: scale(1); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>9 - Sprinkler</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:sprinkler-variant
icon_color: blue
name: Sprinkler
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: irrig-ultra 2s ease-in-out infinite;
          --irrig-heads-animation: irrig-heads 1.6s ease-out infinite;
          --irrig-fog-animation: irrig-fog 2s ease-in-out infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          --irrig-heads-animation: none;
          --irrig-fog-animation: none;
          opacity: 0.75;
        {% endif %}

        position: relative;
      }

      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        border-radius: inherit;
        inset: 0;
        pointer-events: none;
      }

      .shape::before {
        animation: var(--irrig-heads-animation);
      }

      .shape::after {
        animation: var(--irrig-fog-animation);
      }

      @keyframes irrig-ultra {
        0%   { transform: translateY(0) scale(1); }
        25%  { transform: translateY(-2px) scale(1.02); }
        50%  { transform: translateY(-4px) scale(1.03); }
        75%  { transform: translateY(-2px) scale(1.02); }
        100% { transform: translateY(0) scale(1); }
      }

      @keyframes irrig-idle {
        0%   { transform: translateY(1px); }
        50%  { transform: translateY(-1px); }
        100% { transform: translateY(1px); }
      }

      @keyframes irrig-heads {
        0% {
          box-shadow:
            -10px 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0),
            0 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0),
            10px 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0);
        }
        20% {
          box-shadow:
            -10px 4px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9),
            0 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0),
            10px 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0);
        }
        40% {
          box-shadow:
            -10px -2px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.4),
            0 4px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9),
            10px 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0);
        }
        60% {
          box-shadow:
            -10px -8px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.1),
            0 -2px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.4),
            10px 4px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9);
        }
        80% {
          box-shadow:
            -10px -12px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.0),
            0 -8px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.1),
            10px -2px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.4);
        }
        100% {
          box-shadow:
            -10px 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0),
            0 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0),
            10px 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0);
        }
      }

      @keyframes irrig-fog {
        0% {
          filter: blur(0);
        }
        50% {
          filter: blur(0.7px);
          box-shadow: 0 -14px 18px -8px rgba(var(--rgb-{{ config.icon_color }}), 0.45);
        }
        100% {
          filter: blur(0);
          box-shadow: 0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 20pxx 0px -18px !important;
        padding-right: 20px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>9 - Sprinkler (icon in corner version)</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:sprinkler-variant
icon_color: blue
name: Sprinkler
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: irrig-ultra 2s ease-in-out infinite;
          --irrig-heads-animation: irrig-heads 1.6s ease-out infinite;
          --irrig-fog-animation: irrig-fog 2s ease-in-out infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          --irrig-heads-animation: none;
          --irrig-fog-animation: none;
          opacity: 0.75;
        {% endif %}

        position: relative;
      }

      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        border-radius: inherit;
        inset: 0;
        pointer-events: none;
      }

      .shape::before {
        animation: var(--irrig-heads-animation);
      }

      .shape::after {
        animation: var(--irrig-fog-animation);
      }

      @keyframes irrig-ultra {
        0%   { transform: translateY(0) scale(1); }
        25%  { transform: translateY(-2px) scale(1.02); }
        50%  { transform: translateY(-4px) scale(1.03); }
        75%  { transform: translateY(-2px) scale(1.02); }
        100% { transform: translateY(0) scale(1); }
      }

      @keyframes irrig-idle {
        0%   { transform: translateY(1px); }
        50%  { transform: translateY(-1px); }
        100% { transform: translateY(1px); }
      }

      @keyframes irrig-heads {
        0% {
          box-shadow:
            -10px 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0),
            0 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0),
            10px 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0);
        }
        20% {
          box-shadow:
            -10px 4px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9),
            0 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0),
            10px 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0);
        }
        40% {
          box-shadow:
            -10px -2px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.4),
            0 4px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9),
            10px 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0);
        }
        60% {
          box-shadow:
            -10px -8px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.1),
            0 -2px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.4),
            10px 4px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9);
        }
        80% {
          box-shadow:
            -10px -12px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.0),
            0 -8px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.1),
            10px -2px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.4);
        }
        100% {
          box-shadow:
            -10px 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0),
            0 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0),
            10px 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0);
        }
      }

      @keyframes irrig-fog {
        0% {
          filter: blur(0);
        }
        50% {
          filter: blur(0.7px);
          box-shadow: 0 -14px 18px -8px rgba(var(--rgb-{{ config.icon_color }}), 0.45);
        }
        100% {
          filter: blur(0);
          box-shadow: 0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -17px 0 10px -17px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>10 - Heater</strong></summary>

```yaml
type: custom:mushroom-climate-card
entity: climate.heatpump
collapsible_controls: false
show_temperature_control: true
fill_container: false
hvac_modes:
  - auto
  - heat_cool
  - cool
  - heat
  - dry
  - fan_only
  - "off"
name: Heater
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========= FLAME COLOR CONFIG ========= #}
        {% set flame_color = 'deep-orange' %}   {# 'red', 'amber', 'orange', etc. #}
        --flame-color-rgb: var(--rgb-{{ flame_color }});
        {# ===================================== #}

        {# ========== USER CONFIG ========== #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'climate.heatpump' %}
        {% set active_value    = 'heat' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        {% set number_operator = '>' %}
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ----------- TRIGGER LOGIC ----------- #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# --------- END TRIGGER LOGIC --------- #}

        {% if trigger_active %}
          # --shape-animation: flame-core 1.4s infinite;
          --flame-layer1: flame-layers 1.8s infinite;
          --flame-layer2: ember-pulse 2.4s infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          --flame-layer1: none;
          --flame-layer2: none;
          opacity: 0.6;
        {% endif %}

        position: relative;
        transform-origin: 50% 75%;
      }

      /* Flame layers */
      .shape::before,
      .shape::after {
        content: "";
        position: absolute;
        inset: -8px;
        border-radius: inherit;
        pointer-events: none;
        filter: blur(3px);
      }

      .shape::before {
        animation: var(--flame-layer1);
      }

      .shape::after {
        animation: var(--flame-layer2);
      }

      /* Core flame motion: chaotic vertical flicker + heat ripple */
      @keyframes flame-core {
        0%   { transform: translateY(0)    scale(1);     filter: brightness(1.1) hue-rotate(0deg); }
        12%  { transform: translateY(-2px) scale(1.05);  filter: brightness(1.4) hue-rotate(-10deg); }
        25%  { transform: translateY(1px)  scale(0.98);  filter: brightness(0.9) hue-rotate(8deg); }
        40%  { transform: translateY(-3px) scale(1.07);  filter: brightness(1.5) hue-rotate(-18deg); }
        55%  { transform: translateY(0)    scale(1.02);  filter: brightness(1.2) hue-rotate(10deg); }
        70%  { transform: translateY(-1px) scale(1.04);  filter: brightness(1.35) hue-rotate(-6deg); }
        85%  { transform: translateY(2px)  scale(0.97);  filter: brightness(0.95) hue-rotate(6deg); }
        100% { transform: translateY(0)    scale(1);     filter: brightness(1.1) hue-rotate(0deg); }
      }

      /* Outer flame shape: shifting blurred glow */
      @keyframes flame-layers {
        0% {
          box-shadow:
            0 0 14px 8px rgba(var(--flame-color-rgb), 0.8),
            0 -12px 24px -6px rgba(255, 200, 0, 0.4);
        }
        33% {
          box-shadow:
            0 0 20px 10px rgba(var(--flame-color-rgb), 1),
            0 -16px 30px -8px rgba(255, 160, 0, 0.5);
        }
        66% {
          box-shadow:
            0 0 18px 9px rgba(var(--flame-color-rgb), 0.9),
            0 -8px 20px -6px rgba(255, 220, 0, 0.35);
        }
        100% {
          box-shadow:
            0 0 14px 8px rgba(var(--flame-color-rgb), 0.8),
            0 -12px 24px -6px rgba(255, 200, 0, 0.4);
        }
      }

      /* Ember pulse: slow breathing glow */
      @keyframes ember-pulse {
        0% {
          box-shadow:
            0 0 30px 10px rgba(var(--flame-color-rgb), 0.25),
            0 0 60px 20px rgba(255, 120, 0, 0.15);
        }
        50% {
          box-shadow:
            0 0 50px 18px rgba(var(--flame-color-rgb), 0.5),
            0 0 90px 35px rgba(255, 150, 0, 0.25);
        }
        100% {
          box-shadow:
            0 0 30px 10px rgba(var(--flame-color-rgb), 0.25),
            0 0 60px 20px rgba(255, 120, 0, 0.15);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -17px 0 20px -17px !important;
        padding-right: 20px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>11 - LED Strip</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:led-strip-variant
icon_color: blue
name: LED Strip
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}

          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}

        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: rgb-wave 2.2s linear infinite;
          opacity: 1;
        {% else %}
          --shape-animation: rgb-off 3s ease-in-out infinite;
          opacity: 0.5;
        {% endif %}

        transform-origin: 50% 50%;
      }

      @keyframes rgb-wave {
        0% {
          filter: hue-rotate(0deg) brightness(1.1);
          box-shadow:
            0 0 12px 3px rgba(var(--rgb-{{ config.icon_color }}), 0.9);
          transform: scale(1);
        }
        25% {
          filter: hue-rotate(90deg) brightness(1.3);
          box-shadow:
            0 0 16px 6px rgba(var(--rgb-{{ config.icon_color }}), 1);
          transform: scale(1.04);
        }
        50% {
          filter: hue-rotate(180deg) brightness(1.15);
          box-shadow:
            0 0 20px 8px rgba(var(--rgb-{{ config.icon_color }}), 0.9);
          transform: scale(1.02);
        }
        75% {
          filter: hue-rotate(270deg) brightness(1.3);
          box-shadow:
            0 0 16px 6px rgba(var(--rgb-{{ config.icon_color }}), 1);
          transform: scale(1.04);
        }
        100% {
          filter: hue-rotate(360deg) brightness(1.1);
          box-shadow:
            0 0 12px 3px rgba(var(--rgb-{{ config.icon_color }}), 0.9);
          transform: scale(1);
        }
      }

      @keyframes rgb-off {
        0%   { filter: brightness(0.7); }
        50%  { filter: brightness(0.9); }
        100% { filter: brightness(0.7); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>12 - Washing Machine</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:washing-machine
icon_color: blue
name: Washing Machine
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: wash-cycle 1s cubic-bezier(0.45, 0.05, 0.55, 0.95) infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.8;
        {% endif %}

        transform-origin: 50% 55%;
      }

      @keyframes wash-cycle {
        0%   { transform: translateY(0) rotate(-8deg) scale(1); box-shadow: 0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.5); }
        20%  { transform: translateY(-3px) rotate(8deg) scale(1.02); box-shadow: 0 0 8px 4px rgba(var(--rgb-{{ config.icon_color }}), 0.3); }
        40%  { transform: translateY(2px) rotate(-6deg) scale(1.01); }
        60%  { transform: translateY(-2px) rotate(6deg) scale(1.02); }
        80%  { transform: translateY(1px) rotate(-4deg) scale(1.01); }
        100% { transform: translateY(0) rotate(-8deg) scale(1); box-shadow: 0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.2); }
      }

      @keyframes wash-idle {
        0%   { transform: rotate(0deg); }
        50%  { transform: rotate(2deg); }
        100% { transform: rotate(0deg); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -22px 0 10px -22px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>13 - Washing Machine</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:washing-machine
icon_color: blue
name: Washing Machine
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: washer-chaos 1.1s cubic-bezier(0.25, 0.1, 0.25, 1) infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.85;
        {% endif %}

        transform-origin: 50% 55%;
        box-shadow:
          inset 0 0 0 2px rgba(var(--rgb-{{ config.icon_color }}), 0.5),
          0 0 10px 0 rgba(var(--rgb-{{ config.icon_color }}), 0.6);
        position: relative;
      }

      @keyframes washer-chaos {
        0% {
          transform: rotate(0deg) scale(1);
          box-shadow:
            inset 0 0 0 2px rgba(var(--rgb-{{ config.icon_color }}), 0.7),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.6);
        }
        15%  { transform: rotate(18deg) translate(1px, -1px) scale(1.02); }
        30%  { transform: rotate(60deg) translate(-2px, 2px) scale(0.98); }
        45%  { transform: rotate(120deg) translate(3px, -2px) scale(1.03); }
        60%  { transform: rotate(190deg) translate(-1px, 3px) scale(0.97); }
        75%  { transform: rotate(260deg) translate(1px, -3px) scale(1.04); }
        90%  { transform: rotate(330deg) translate(-2px, 1px) scale(1.01); }
        100% {
          transform: rotate(360deg) translate(0, 0) scale(1);
          box-shadow:
            inset 0 0 0 2px rgba(var(--rgb-{{ config.icon_color }}), 0.7),
            0 0 10px 6px rgba(var(--rgb-{{ config.icon_color }}), 0.0);
        }
      }

      @keyframes washer-idle {
        0%   { transform: rotate(-2deg); }
        50%  { transform: rotate(2deg); }
        100% { transform: rotate(-2deg); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -22px 0 10px -22px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>14 - Dishwasher</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:dishwasher
icon_color: blue
name: Dishwasher
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: dishwasher-swash 1.5s ease-in-out infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.8;
        {% endif %}

        transform-origin: 50% 55%;
      }

      @keyframes dishwasher-swash {
        0% {
          transform: scale(1) rotate(0deg);
          box-shadow:
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.8),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.3);
          filter: blur(0);
        }
        25% {
          transform: scale(1.03) rotate(10deg);
          box-shadow:
            0 0 10px 3px rgba(var(--rgb-{{ config.icon_color }}), 0.9),
            0 0 18px 8px rgba(var(--rgb-{{ config.icon_color }}), 0.3);
          filter: blur(0.4px);
        }
        50% {
          transform: scale(0.98) rotate(-15deg);
          box-shadow:
            0 0 14px 6px rgba(var(--rgb-{{ config.icon_color }}), 0.7),
            0 0 26px 12px rgba(var(--rgb-{{ config.icon_color }}), 0.2);
          filter: blur(0.6px);
        }
        75% {
          transform: scale(1.04) rotate(15deg);
          box-shadow:
            0 0 10px 3px rgba(var(--rgb-{{ config.icon_color }}), 0.9),
            0 0 18px 8px rgba(var(--rgb-{{ config.icon_color }}), 0.3);
          filter: blur(0.4px);
        }
        100% {
          transform: scale(1) rotate(0deg);
          box-shadow:
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.0),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.0);
          filter: blur(0);
        }
      }

      @keyframes dishwasher-idle {
        0%   { transform: scale(1); }
        50%  { transform: scale(1.02); }
        100% { transform: scale(1); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>15 - Fireplace</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:fire
icon_color: deep-orange
name: Fireplace
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ----------- TRIGGER LOGIC ----------- #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# --------- END TRIGGER LOGIC --------- #}

        {% if trigger_active %}
          --shape-animation: flame-core 1.4s infinite;
          --flame-layer1: flame-layers 1.8s infinite;
          --flame-layer2: ember-pulse 2.4s infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          --flame-layer1: none;
          --flame-layer2: none;
          opacity: 0.6;
        {% endif %}

        position: relative;
        transform-origin: 50% 75%;
      }

      /* Flame layers */
      .shape::before,
      .shape::after {
        content: "";
        position: absolute;
        inset: -8px;
        border-radius: inherit;
        pointer-events: none;
        filter: blur(3px);
      }

      .shape::before {
        animation: var(--flame-layer1);
      }

      .shape::after {
        animation: var(--flame-layer2);
      }


      /* Core flame motion: chaotic vertical flicker + heat ripple */
      @keyframes flame-core {
        0%   { transform: translateY(0)    scale(1);     filter: brightness(1.1) hue-rotate(0deg); }
        12%  { transform: translateY(-2px) scale(1.05);  filter: brightness(1.4) hue-rotate(-10deg); }
        25%  { transform: translateY(1px)  scale(0.98);  filter: brightness(0.9) hue-rotate(8deg); }
        40%  { transform: translateY(-3px) scale(1.07);  filter: brightness(1.5) hue-rotate(-18deg); }
        55%  { transform: translateY(0)    scale(1.02);  filter: brightness(1.2) hue-rotate(10deg); }
        70%  { transform: translateY(-1px) scale(1.04);  filter: brightness(1.35) hue-rotate(-6deg); }
        85%  { transform: translateY(2px)  scale(0.97);  filter: brightness(0.95) hue-rotate(6deg); }
        100% { transform: translateY(0)    scale(1);     filter: brightness(1.1) hue-rotate(0deg); }
      }


      /* Outer flame shape: shifting blurred glow */
      @keyframes flame-layers {
        0% {
          box-shadow:
            0 0 14px 8px rgba(var(--rgb-{{ config.icon_color }}), 0.8),
            0 -12px 24px -6px rgba(255, 200, 0, 0.4);
        }
        33% {
          box-shadow:
            0 0 20px 10px rgba(var(--rgb-{{ config.icon_color }}), 1),
            0 -16px 30px -8px rgba(255, 160, 0, 0.5);
        }
        66% {
          box-shadow:
            0 0 18px 9px rgba(var(--rgb-{{ config.icon_color }}), 0.9),
            0 -8px 20px -6px rgba(255, 220, 0, 0.35);
        }
        100% {
          box-shadow:
            0 0 14px 8px rgba(var(--rgb-{{ config.icon_color }}), 0.8),
            0 -12px 24px -6px rgba(255, 200, 0, 0.4);
        }
      }


      /* Ember pulse: slow breathing glow */
      @keyframes ember-pulse {
        0% {
          box-shadow:
            0 0 30px 10px rgba(var(--rgb-{{ config.icon_color }}), 0.25),
            0 0 60px 20px rgba(255, 120, 0, 0.15);
        }
        50% {
          box-shadow:
            0 0 50px 18px rgba(var(--rgb-{{ config.icon_color }}), 0.5),
            0 0 90px 35px rgba(255, 150, 0, 0.25);
        }
        100% {
          box-shadow:
            0 0 30px 10px rgba(var(--rgb-{{ config.icon_color }}), 0.25),
            0 0 60px 20px rgba(255, 120, 0, 0.15);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0 20px -20px !important;
        padding-right: 20px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>16 - Vacuum</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:robot-vacuum
icon_color: blue
name: Vacuum
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}

          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}

        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: robo-path 3.4s linear infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.7;
        {% endif %}

        transform-origin: 50% 50%;
      }

      @keyframes robo-path {
        0%   { transform: translate(0, 0) scale(1); }
        10%  { transform: translate(6px, -2px) rotate(8deg) scale(0.98); }
        20%  { transform: translate(10px, 4px) rotate(-6deg) scale(1); }
        30%  { transform: translate(4px, 8px) rotate(-14deg) scale(1.02); }
        40%  { transform: translate(-6px, 10px) rotate(4deg) scale(0.98); }
        50%  { transform: translate(-10px, 2px) rotate(16deg) scale(1.03); }
        60%  { transform: translate(-6px, -6px) rotate(-8deg) scale(1); }
        70%  { transform: translate(2px, -10px) rotate(10deg) scale(0.97); }
        80%  { transform: translate(8px, -6px) rotate(-6deg) scale(1.02); }
        90%  { transform: translate(4px, -2px) rotate(4deg) scale(1.01); }
        100% { transform: translate(0, 0) rotate(0deg) scale(1); }
      }

      @keyframes robo-dock {
        0%   { transform: translateY(0); }
        50%  { transform: translateY(-2px); }
        100% { transform: translateY(0); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 20pxx 0px -18px !important;
        padding-right: 20px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>17 - 3d Printer</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:printer-3d-nozzle
icon_color: purple
name: 3d Printer
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}

          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}

        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: printer-sequence 2.3s linear infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.8;
        {% endif %}

        transform-origin: 50% 80%;
        box-shadow:
          0 8px 0 -4px rgba(var(--rgb-{{ config.icon_color }}), 0.5),
          0 0 12px 0 rgba(var(--rgb-{{ config.icon_color }}), 0.8);
      }

      @keyframes printer-sequence {
        0%   { transform: translate(-5px, 4px) scale(0.96); }
        15%  { transform: translate(5px, 4px) scale(0.96); }
        16%  { transform: translate(5px, 2px) scale(0.98); }
        30%  { transform: translate(-5px, 2px) scale(0.98); }
        31%  { transform: translate(-5px, 0px) scale(1); }
        45%  { transform: translate(5px, 0px) scale(1); }
        46%  { transform: translate(5px, -2px) scale(1.02); }
        60%  { transform: translate(-5px, -2px) scale(1.02); }
        61%  { transform: translate(-5px, -4px) scale(1.04); }
        80%  { transform: translate(5px, -4px) scale(1.04); }
        100% { transform: translate(-5px, 4px) scale(0.96); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -22px 0 10px -22px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>18 - PIR Sensor</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:motion-sensor
icon_color: red
name: PIR Sensor
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}

          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: motion-active 1.4s linear infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.7;
        {% endif %}

        transform-origin: 50% 50%;
      }

      @keyframes motion-active {
        0% {
          transform: scale(1);
          box-shadow:
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.4);
        }
        40% {
          transform: scale(1.06);
          box-shadow:
            0 0 0 6px rgba(var(--rgb-{{ config.icon_color }}), 0.5),
            0 0 0 12px rgba(var(--rgb-{{ config.icon_color }}), 0.2);
        }
        100% {
          transform: scale(1);
          box-shadow:
            0 0 0 16px rgba(var(--rgb-{{ config.icon_color }}), 0.0),
            0 0 0 24px rgba(var(--rgb-{{ config.icon_color }}), 0.0);
        }
      }

      @keyframes motion-scan {
        0% {
          transform: rotate(0deg);
          box-shadow:
            0 -10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9);
        }
        50% {
          transform: rotate(180deg);
          box-shadow:
            0 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.6);
        }
        100% {
          transform: rotate(360deg);
          box-shadow:
            0 -10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -15px 0 10px -18px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>19 - Alarm</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:alarm
icon_color: pink
name: Alarm
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}

          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: siren-alert 0.6s linear infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.7;
        {% endif %}

        transform-origin: 50% 50%;
      }

      @keyframes siren-alert {
        0% {
          transform: translate(0, 0) scale(1);
          box-shadow: 0 0 10px 4px rgba(var(--rgb-{{ config.icon_color }}), 1);
        }
        10%  { transform: translate(-2px, -1px) rotate(-3deg) scale(1.02); }
        20%  { transform: translate(3px, 1px) rotate(2deg) scale(1.03); }
        30%  { transform: translate(-4px, 0) rotate(-4deg) scale(1.04); }
        40%  { transform: translate(4px, 2px) rotate(3deg) scale(1.05); }
        50%  { transform: translate(-2px, -2px) rotate(-2deg) scale(1.02); }
        60%  { transform: translate(2px, 1px) rotate(1deg) scale(1.03); }
        70%  { transform: translate(-3px, 0) rotate(-3deg) scale(1.04); }
        80%  { transform: translate(3px, -1px) rotate(2deg) scale(1.03); }
        100% {
          transform: translate(0, 0) rotate(0deg) scale(1);
          box-shadow: 0 0 20px 8px rgba(var(--rgb-{{ config.icon_color }}), 0);
        }
      }

      @keyframes siren-armed {
        0%   { box-shadow: 0 0 4px 1px rgba(var(--rgb-{{ config.icon_color }}), 0.4); }
        50%  { box-shadow: 0 0 10px 4px rgba(var(--rgb-{{ config.icon_color }}), 0.9); }
        100% { box-shadow: 0 0 4px 1px rgba(var(--rgb-{{ config.icon_color }}), 0.4); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>20 - Heater</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
icon: mdi:radiator
icon_color: amber
name: Heater
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {% set power_val = states(number_entity) | float(0) %}
        {% set norm = (power_val / 1500) | float %}
        {% set norm_c = [0, [norm, 1.3] | min] | max %}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% if number_operator == '>' %}
            {% set trigger_active = (power_val > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (power_val < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (power_val == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (power_val >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (power_val <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: heater-waves 1.7s ease-in-out infinite;
          --heater-glow-animation: heater-glow 2.1s ease-in-out infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          --heater-glow-animation: none;
          opacity: 0.6;
        {% endif %}

        --heater-scale: {{ (1 + norm_c * 0.15) | round(3) }};
        transform-origin: 50% 60%;
        position: relative;
      }

      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        inset: -8px;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        animation: var(--heater-glow-animation);
      }

      .shape::after {
        inset: -18px;
        animation: var(--heater-glow-animation);
        opacity: 0.9;
      }

      @keyframes heater-waves {
        0%   { transform: translateY(0) scale(1); }
        25%  { transform: translateY(-1px) scale(var(--heater-scale)); }
        50%  { transform: translateY(-2px) scale(1.02); }
        75%  { transform: translateY(-1px) scale(var(--heater-scale)); }
        100% { transform: translateY(0) scale(1); }
      }

      @keyframes heater-glow {
        0% {
          box-shadow:
            0 -10px 18px -6px rgba(var(--rgb-{{ config.icon_color }}), 0.6),
            0 -20px 40px -10px rgba(255, 120, 0, 0.35);
        }
        50% {
          box-shadow:
            0 -14px 26px -4px rgba(var(--rgb-{{ config.icon_color }}), 1),
            0 -26px 60px -10px rgba(255, 90, 0, 0.55);
        }
        100% {
          box-shadow:
            0 -10px 18px -6px rgba(var(--rgb-{{ config.icon_color }}), 0.6),
            0 -20px 40px -10px rgba(255, 120, 0, 0.35);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -15px 0 10px -15px !important;
        padding-right: 20px;

      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>21 - RGB</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:led-on
icon_color: blue
name: RGB
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}

          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% if states(state_entity) == active_value %}
            {% set trigger_active = true %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: rainbow 3s linear infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.7;
        {% endif %}
      }

      @keyframes rainbow {
        0%   { filter: hue-rotate(0deg) brightness(1.1); }
        50%  { filter: hue-rotate(180deg) brightness(1.3); }
        100% { filter: hue-rotate(360deg) brightness(1.1); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>22 - Kettle</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:kettle-steam
icon_color: brown
name: Kettle
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: tv-glitch 1.2s linear infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.6;
        {% endif %}

        transform-origin: 50% 50%;
      }

      @keyframes tv-glitch {
        0%   { transform: scale(1) translate(0, 0); filter: brightness(1.05); box-shadow: 0 0 8px 2px rgba(var(--rgb-{{ config.icon_color }}), 0.7); }
        10%  { transform: scaleX(1.02) translate(-1px, 0); }
        20%  { transform: scaleX(0.98) translate(1px, -1px); filter: brightness(1.3); }
        25%  { transform: scale(1.01) translate(0, 1px); }
        40%  { transform: scale(1) translate(0, 0); filter: brightness(1.1); }
        55%  { transform: scaleX(1.03) translate(0, -1px); }
        70%  { transform: scale(1) translate(0, 0); box-shadow: 0 0 14px 5px rgba(var(--rgb-{{ config.icon_color }}), 0.9); }
        100% { transform: scale(1) translate(0, 0); filter: brightness(1.05); box-shadow: 0 0 8px 2px rgba(var(--rgb-{{ config.icon_color }}), 0.7); }
      }

      @keyframes tv-standby {
        0%   { box-shadow: 0 0 2px 0 rgba(var(--rgb-{{ config.icon_color }}), 0.3); }
        50%  { box-shadow: 0 0 6px 2px rgba(var(--rgb-{{ config.icon_color }}), 0.6); }
        100% { box-shadow: 0 0 2px 0 rgba(var(--rgb-{{ config.icon_color }}), 0.3); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0 10px -15px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>23 - Android TV</strong></summary>

```yaml
type: custom:mushroom-media-player-card
entity: media_player.android_tv
volume_controls:
  - volume_mute
  - volume_set
  - volume_buttons
media_controls:
  - on_off
  - shuffle
  - previous
  - play_pause_stop
  - next
  - repeat
show_volume_level: true
use_media_info: false
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ======= COLOR CONFIG ======= #}
        {% set icon_on_color      = 'red' %}
        {% set circle_on_rgb      = '255, 30, 30' %}     {# dark red #}
        {% set circle_on_opacity  = 0.1 %}

        {% set icon_off_color     = 'grey' %}
        {% set circle_off_rgb     = '80, 80, 80' %}      {# dark grey #}
        {% set circle_off_opacity = 0.25 %}
        {# ============================ #}

        {% set s = states('media_player.android_tv') %}

        {% if s != 'off' %}
          {% set trigger = true %}
        {% else %}
          {% set trigger = false %}
        {% endif %}

        {% if trigger %}
          /* icon color */
          --icon-color: rgb(var(--rgb-{{ icon_on_color }}));
          --icon-color-rgb: var(--rgb-{{ icon_on_color }});

          /* circle color */
          --shape-color: rgba({{ circle_on_rgb }}, {{ circle_on_opacity }});
          --shape-color-rgb: {{ circle_on_rgb }};

          --shape-animation: tv-rgb 1.4s linear infinite;
          --glow-enabled: 1;
          opacity: 1;
        {% else %}
          /* icon color */
          --icon-color: rgb(var(--rgb-{{ icon_off_color }}));
          --icon-color-rgb: var(--rgb-{{ icon_off_color }});

          /* circle color */
          --shape-color: rgba({{ circle_off_rgb }}, {{ circle_off_opacity }});
          --shape-color-rgb: {{ circle_off_rgb }};

          --shape-animation: none;
          --glow-enabled: 0;
          opacity: 0.7;
        {% endif %}

        transform-origin: 50% 50%;
      }

      /* Remove glow when off */
      .shape[style*="--glow-enabled: 0"] {
        filter: none !important;
        box-shadow: none !important;
      }
      .shape[style*="--glow-enabled: 0"]::before,
      .shape[style*="--glow-enabled: 0"]::after {
        animation: none !important;
        filter: none !important;
        box-shadow: none !important;
      }

      @keyframes tv-rgb {
        0% {
          transform: scale(1); /* no movement */
          filter: brightness(1.0);
          box-shadow:
            0 0 6px 2px rgba(var(--icon-color-rgb), 0.4),
            -4px 0 8px -4px rgba(255, 0, 0, 0.4),
             4px 0 8px -4px rgba(0, 128, 255, 0.4);
        }
        40% {
          transform: scale(1); /* still */
          filter: brightness(1.25);
          box-shadow:
            0 0 16px 6px rgba(var(--icon-color-rgb), 0.9),
            -6px 0 12px -4px rgba(255, 0, 0, 0.7),
             6px 0 12px -4px rgba(0, 128, 255, 0.7);
        }
        100% {
          transform: scale(1); /* still */
          filter: brightness(1.0);
          box-shadow:
            0 0 6px 2px rgba(var(--icon-color-rgb), 0.4),
            -4px 0 8px -4px rgba(255, 0, 0, 0.4),
             4px 0 8px -4px rgba(0, 128, 255, 0.4);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0px 0px -15px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius,12px));
      }

```
</details>

<details>
<summary><strong>24 - Living Room Speaker</strong></summary>

```yaml
type: custom:mushroom-media-player-card
entity: media_player.living_room_speaker
volume_controls:
  - volume_mute
  - volume_set
  - volume_buttons
media_controls:
  - on_off
  - shuffle
  - previous
  - play_pause_stop
  - next
  - repeat
show_volume_level: true
use_media_info: false
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ====== COLOR CONFIG ====== #}
        {% set icon_on_color      = 'red' %}
        {% set circle_on_rgb      = '255, 30, 30' %}
        {% set circle_on_opacity  = 0.1 %}

        {% set icon_off_color     = 'grey' %}
        {% set circle_off_rgb     = '80, 80, 80' %}
        {% set circle_off_opacity = 0.25 %}
        {# ========================== #}

        {# ========== USER CONFIG ========== #}
        {# STATE ENTITY #}
        {% set state_entity    = 'media_player.living_room_speaker' %}
        {% set off_value       = 'off' %}
        {% set play_value      = 'playing' %}
        {% set idle_value      = 'idle' %}
        {# ========== END CONFIG ========== #}

        {% set st = states(state_entity) %}

        {# LIGHT ACTIVE = any state except off #}
        {% set light_active = (st != off_value) %}

        {# ANIMATION TRIGGER: default = only when playing #}
          {# animation ONLY when playing #}
          {% set trigger_active = (st == play_value) %}

        {% set vol = state_attr(config.entity, 'volume_level') | float(0) %}

        {% if light_active %}
          {# ---- COLORS WHEN NOT OFF ---- #}
          --icon-color: rgb(var(--rgb-{{ icon_on_color }}));
          --icon-color-rgb: var(--rgb-{{ icon_on_color }});
          --shape-color: rgba({{ circle_on_rgb }}, {{ circle_on_opacity }});
          --shape-color-rgb: {{ circle_on_rgb }};

          opacity: 1;

          {# ---- ANIMATION ONLY WHEN trigger_active ---- #}
          {% if trigger_active %}
            --shape-animation: ultra-speaker-main 0.9s ease-in-out infinite;
            --speaker-bars-animation: ultra-speaker-bars 0.55s linear infinite;
            --speaker-bass-animation: ultra-speaker-bass 1s ease-out infinite;
          {% else %}
            --shape-animation: none;
            --speaker-bars-animation: none;
            --speaker-bass-animation: none;
            --no-glow: 0 0 0 0 rgba(0,0,0,0);
          {% endif %}

        {% else %}
          {# ---- OFF: DIM + NO ANIMATION ---- #}
          --icon-color: rgb(var(--rgb-{{ icon_off_color }}));
          --icon-color-rgb: var(--rgb-{{ icon_off_color }});
          --shape-color: rgba({{ circle_off_rgb }}, {{ circle_off_opacity }});
          --shape-color-rgb: {{ circle_off_rgb }};

          --shape-animation: none;
          --speaker-bars-animation: none;
          --speaker-bass-animation: none;
          --no-glow: 0 0 0 0 rgba(0,0,0,0);

          opacity: 0.6;
        {% endif %}

        transform-origin: 50% 50%;
        position: relative;
      }

      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        inset: 0;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        animation: var(--speaker-bars-animation);
        box-shadow: var(--no-glow, none);
      }

      .shape::after {
        animation: var(--speaker-bass-animation);
        box-shadow: var(--no-glow, none);
      }

      @keyframes ultra-speaker-main {
        0%   { transform: scale(1); }
        50%  { transform: scale(1.06); }
        100% { transform: scale(1); }
      }

      @keyframes ultra-speaker-bars {
        0% {
          box-shadow:
            -10px 6px 0 -5px rgba(var(--icon-color-rgb), 0.4),
            0 2px 0 -5px rgba(var(--icon-color-rgb), 0.6),
            10px -4px 0 -5px rgba(var(--icon-color-rgb), 0.3);
        }
        33% {
          box-shadow:
            -10px -2px 0 -5px rgba(var(--icon-color-rgb), 0.7),
            0 8px 0 -5px rgba(var(--icon-color-rgb), 0.3),
            10px -8px 0 -5px rgba(var(--icon-color-rgb), 0.6);
        }
        66% {
          box-shadow:
            -10px -8px 0 -5px rgba(var(--icon-color-rgb), 0.3),
            0 -4px 0 -5px rgba(var(--icon-color-rgb), 0.7),
            10px 6px 0 -5px rgba(var(--icon-color-rgb), 0.5);
        }
        100% {
          box-shadow:
            -10px 6px 0 -5px rgba(var(--icon-color-rgb), 0.4),
            0 2px 0 -5px rgba(var(--icon-color-rgb), 0.6),
            10px -4px 0 -5px rgba(var(--icon-color-rgb), 0.3);
        }
      }

      @keyframes ultra-speaker-bass {
        0% {
          {% set s0 = 1 + (vol * 0.09) %}
          transform: scale({{ s0 | round(2) }});
          box-shadow:
            0 0 0 0 rgba(var(--icon-color-rgb), 0.9),
            0 0 0 0 rgba(var(--icon-color-rgb), 0.5);
        }
        40% {
          {% set s1 = 1.08 + vol * 0.1 %}
          transform: scale({{ s1 | round(2) }});
          box-shadow:
            0 0 0 8px rgba(var(--icon-color-rgb), 0.6),
            0 0 0 14px rgba(var(--icon-color-rgb), 0.3);
        }
        100% {
          transform: scale(1);
          box-shadow:
            0 0 0 20px rgba(var(--icon-color-rgb), 0),
            0 0 0 30px rgba(var(--icon-color-rgb), 0);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0px 0px -18px !important;
        padding-right: 20px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>25 - Router</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:router-wireless
icon_color: blue
name: Router
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: wifi-waves 1.7s ease-out infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.6;
        {% endif %}

        position: relative;
      }

      @keyframes wifi-waves {
        0% {
          box-shadow:
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.5),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.2);
        }
        30% {
          box-shadow:
            0 0 0 4px rgba(var(--rgb-{{ config.icon_color }}), 0.6),
            0 0 0 10px rgba(var(--rgb-{{ config.icon_color }}), 0.35),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.2);
        }
        60% {
          box-shadow:
            0 0 0 8px rgba(var(--rgb-{{ config.icon_color }}), 0.0),
            0 0 0 18px rgba(var(--rgb-{{ config.icon_color }}), 0.25),
            0 0 0 28px rgba(var(--rgb-{{ config.icon_color }}), 0.1);
        }
        100% {
          box-shadow:
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.0),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.0),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.0);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>26 - Android TV</strong></summary>

```yaml
type: custom:mushroom-media-player-card
entity: media_player.android_tv
volume_controls:
  - volume_mute
  - volume_set
  - volume_buttons
media_controls:
  - on_off
  - shuffle
  - previous
  - play_pause_stop
  - next
  - repeat
show_volume_level: true
use_media_info: false
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ======= COLOR CONFIG ======= #}
        {% set icon_on_color      = 'red' %}
        {% set circle_on_rgb      = '255, 30, 30' %}     {# dark red-ish #}
        {% set circle_on_opacity  = 0.15 %}

        {% set icon_off_color     = 'grey' %}
        {% set circle_off_rgb     = '80, 80, 80' %}      {# dark grey #}
        {% set circle_off_opacity = 0.25 %}
        {# ============================ #}

        {# ========== USER CONFIG ========== #}

        {# STATE MODE SETTINGS: any state except 'off' will trigger #}
        {% set state_entity    = 'media_player.android_tv' %}
        {% set off_value       = 'off' %}

        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER LOGIC ======== #}
          {# any state except 'off' #}
          {% set trigger_active = (states(state_entity) != off_value) %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          {# ON / ACTIVE COLORS #}
          --icon-color: rgb(var(--rgb-{{ icon_on_color }}));
          --icon-color-rgb: var(--rgb-{{ icon_on_color }});

          --shape-color: rgba({{ circle_on_rgb }}, {{ circle_on_opacity }});
          --shape-color-rgb: {{ circle_on_rgb }};

          --shape-animation: bass-pulse 0.8s ease-out infinite;
          opacity: 1;
        {% else %}
          {# OFF / IDLE COLORS #}
          --icon-color: rgb(var(--rgb-{{ icon_off_color }}));
          --icon-color-rgb: var(--rgb-{{ icon_off_color }});

          --shape-color: rgba({{ circle_off_rgb }}, {{ circle_off_opacity }});
          --shape-color-rgb: {{ circle_off_rgb }};

          --shape-animation: none;
          opacity: 0.7;
        {% endif %}

        transform-origin: 50% 50%;
      }

      @keyframes bass-pulse {
        0% {
          transform: scale(1);
          box-shadow:
            0 0 0 0 rgba(var(--icon-color-rgb), 0.8);
        }
        10% {
          transform: scale(1.08);
          box-shadow:
            0 0 10px 4px rgba(var(--icon-color-rgb), 0.8);
        }
        25% {
          transform: scale(1.03);
          box-shadow:
            0 0 6px 2px rgba(var(--icon-color-rgb), 0.5);
        }
        50% {
          transform: scale(1.06);
          box-shadow:
            0 0 12px 5px rgba(var(--icon-color-rgb), 0.6);
        }
        100% {
          transform: scale(1);
          box-shadow:
            0 0 0 0 rgba(var(--icon-color-rgb), 0.0);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0px 0px -15px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>27 - PIR Sensor</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:motion-sensor
icon_color: red
name: PIR Sensor
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: ultra-motion-active 1.3s linear infinite;
          --motion-cone-animation: ultra-motion-cone 1.6s linear infinite;
          --motion-pulse-animation: ultra-motion-pulse 1.3s ease-out infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          --motion-cone-animation: none;
          --motion-pulse-animation: none;
          opacity: 0.75;
        {% endif %}

        transform-origin: 50% 50%;
        position: relative;
      }

      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        inset: -6px;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        animation: var(--motion-cone-animation);
      }

      .shape::after {
        animation: var(--motion-pulse-animation);
      }

      @keyframes ultra-motion-active {
        0%   { transform: scale(1); }
        50%  { transform: scale(1.06); }
        100% { transform: scale(1); }
      }

      @keyframes ultra-motion-scan {
        0%   { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
      }

      @keyframes ultra-motion-cone {
        0% {
          box-shadow:
            0 -20px 14px -16px rgba(var(--rgb-{{ config.icon_color }}), 0.0);
        }
        25% {
          box-shadow:
            8px -16px 14px -16px rgba(var(--rgb-{{ config.icon_color }}), 0.5);
        }
        50% {
          box-shadow:
            0 -20px 14px -12px rgba(var(--rgb-{{ config.icon_color }}), 0.8);
        }
        75% {
          box-shadow:
            -8px -16px 14px -16px rgba(var(--rgb-{{ config.icon_color }}), 0.5);
        }
        100% {
          box-shadow:
            0 -20px 14px -16px rgba(var(--rgb-{{ config.icon_color }}), 0.0);
        }
      }

      @keyframes ultra-motion-pulse {
        0% {
          box-shadow:
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.4);
        }
        40% {
          box-shadow:
            0 0 0 8px rgba(var(--rgb-{{ config.icon_color }}), 0.5),
            0 0 0 14px rgba(var(--rgb-{{ config.icon_color }}), 0.2);
        }
        100% {
          box-shadow:
            0 0 0 22px rgba(var(--rgb-{{ config.icon_color }}), 0.0),
            0 0 0 30px rgba(var(--rgb-{{ config.icon_color }}), 0.0);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -15px 0 10px -18px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>28 - Lamp</strong></summary>

```yaml
type: custom:mushroom-light-card
entity: light.bedroom_lamp_local
use_light_color: true
show_color_temp_control: true
show_brightness_control: true
collapsible_controls: false
show_color_control: true
name: Lamp
grid_options:
  rows: 1.4
icon_color: auto
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {% set state_entity    = 'light.bedroom_lamp_local' %}
        {% set active_value    = 'on' %}

        {# ====== TRIGGER ====== #}
          {% set trigger_active = (states(state_entity) == active_value) %}

        {# ====== COLOR FROM ENTITY (rgb_color) ====== #}
        {% set rgb = state_attr(config.entity, 'rgb_color') %}
        {% if rgb is not none %}
          {% set r = (rgb[0] | int) %}
          {% set g = (rgb[1] | int) %}
          {% set b = (rgb[2] | int) %}
        {% else %}
          {# fallback if lamp has no rgb_color (ct-only, etc) #}
          {% set r = 255 %}
          {% set g = 240 %}
          {% set b = 200 %}
        {% endif %}

        {% if trigger_active %}
          --shape-animation: lamp-glow 1.4s ease-in-out infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.5;
        {% endif %}
      }

      @keyframes lamp-glow {
        0% {
          filter: brightness(1);
          box-shadow: 0 0 6px 2px rgba({{ r }}, {{ g }}, {{ b }}, 0.6);
        }
        20% {
          filter: brightness(1.25);
          box-shadow: 0 0 14px 6px rgba({{ r }}, {{ g }}, {{ b }}, 0.9);
        }
        30% {
          filter: brightness(0.9);
          box-shadow: 0 0 3px 1px rgba({{ r }}, {{ g }}, {{ b }}, 0.4);
        }
        50% {
          filter: brightness(1.3);
          box-shadow: 0 0 16px 8px rgba({{ r }}, {{ g }}, {{ b }}, 1);
        }
        80% {
          filter: brightness(1.05);
          box-shadow: 0 0 8px 3px rgba({{ r }}, {{ g }}, {{ b }}, 0.7);
        }
        100% {
          filter: brightness(1);
          box-shadow: 0 0 6px 2px rgba({{ r }}, {{ g }}, {{ b }}, 0.6);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -22px 0px 0px -22px !important;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>29 - Garage Door</strong></summary>

```yaml
type: custom:mushroom-cover-card
entity: cover.garage_door
show_buttons_control: true
show_position_control: true
show_tilt_position_control: true
fill_container: false
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========= COLOR CONFIG ========= #}
        {% set cover_color = 'blue' %}   {# change to 'red', 'blue', etc. #}
        --cover-color-rgb: var(--rgb-{{ cover_color }});
        {# ================================= #}

        {# ========== USER CONFIG ========== #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'cover.garage_door' %}
        {% set active_value    = 'open' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.cover_position' %}
        {% set number_operator = '>' %}
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}

          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: motion-active 1.4s linear infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.7;
        {% endif %}

        transform-origin: 50% 50%;
      }

      @keyframes motion-active {
        0% {
          transform: scale(1);
          box-shadow:
            0 0 0 0 rgba(var(--cover-color-rgb), 0.9),
            0 0 0 0 rgba(var(--cover-color-rgb), 0.4);
        }
        40% {
          transform: scale(1.06);
          box-shadow:
            0 0 0 6px rgba(var(--cover-color-rgb), 0.5),
            0 0 0 12px rgba(var(--cover-color-rgb), 0.2);
        }
        100% {
          transform: scale(1);
          box-shadow:
            0 0 0 16px rgba(var(--cover-color-rgb), 0.0),
            0 0 0 24px rgba(var(--cover-color-rgb), 0.0);
        }
      }

      @keyframes motion-scan {
        0% {
          transform: rotate(0deg);
          box-shadow:
            0 -10px 0 0 rgba(var(--cover-color-rgb), 0.9);
        }
        50% {
          transform: rotate(180deg);
          box-shadow:
            0 10px 0 0 rgba(var(--cover-color-rgb), 0.6);
        }
        100% {
          transform: rotate(360deg);
          box-shadow:
            0 -10px 0 0 rgba(var(--cover-color-rgb), 0.9);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -15px 0 10px -18px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>30 - Lamp</strong></summary>

```yaml
type: custom:mushroom-light-card
entity: light.livingroom_lamp_local
use_light_color: true
show_color_temp_control: true
show_brightness_control: true
collapsible_controls: false
show_color_control: true
name: Lamp
grid_options:
  rows: 1.4
icon_color: auto
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {% set state_entity    = 'light.livingroom_lamp_local' %}
        {% set active_value    = 'on' %}

        {# ======== TRIGGER ======== #}
          {% set trigger_active = (states(state_entity) == active_value) %}

        {# ======== COLOR FROM ENTITY (rgb_color) ======== #}
        {% set rgb = state_attr(config.entity, 'rgb_color') %}
        {% if rgb is not none %}
          {% set r = (rgb[0] | int) %}
          {% set g = (rgb[1] | int) %}
          {% set b = (rgb[2] | int) %}
        {% else %}
          {# fallback for CT-only lights #}
          {% set r = 255 %}
          {% set g = 240 %}
          {% set b = 200 %}
        {% endif %}

        {% if trigger_active %}
          --shape-animation: lamp-sweep 1.8s ease-in-out infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.5;
        {% endif %}

        position: relative;
        transform-origin: 50% 60%;
      }

      @keyframes lamp-sweep {
        0% {
          filter: brightness(1.1);
          box-shadow:
            0 0 12px 4px rgba({{ r }}, {{ g }}, {{ b }}, 0.9),
            0 30px 40px -10px rgba({{ r }}, {{ g }}, {{ b }}, 0.0);
          transform: rotate(-4deg) scale(1);
        }
        25% {
          filter: brightness(1.4);
          box-shadow:
            0 0 18px 8px rgba({{ r }}, {{ g }}, {{ b }}, 1),
            -8px 35px 45px -12px rgba({{ r }}, {{ g }}, {{ b }}, 0.5);
          transform: rotate(3deg) scale(1.02);
        }
        50% {
          filter: brightness(1.2);
          box-shadow:
            0 0 24px 10px rgba({{ r }}, {{ g }}, {{ b }}, 0.9),
            8px 35px 45px -12px rgba({{ r }}, {{ g }}, {{ b }}, 0.5);
          transform: rotate(-2deg) scale(1.03);
        }
        75% {
          filter: brightness(1.5);
          box-shadow:
            0 0 18px 8px rgba({{ r }}, {{ g }}, {{ b }}, 1),
            -6px 30px 40px -12px rgba({{ r }}, {{ g }}, {{ b }}, 0.4);
          transform: rotate(2deg) scale(1.01);
        }
        100% {
          filter: brightness(1.1);
          box-shadow:
            0 0 12px 4px rgba({{ r }}, {{ g }}, {{ b }}, 0.8),
            0 30px 40px -10px rgba({{ r }}, {{ g }}, {{ b }}, 0.0);
          transform: rotate(-4deg) scale(1);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0px 0px -18px !important;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>31 - Console</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:controller
icon_color: purple
name: Console
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS (for "intensity") #}
        {% set number_entity   = 'sensor.plug_power' %}
        {% set number_operator = '>' %}
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ---------- TRIGGER DECISION LOGIC ---------- #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# ---------- END TRIGGER LOGIC ---------- #}

        {# Optional intensity from power, just for shaping motion #}
        {% set power     = states(number_entity) | float(0) %}
        {% set intensity = (power / 10) | float(0) %}
        {% if intensity < 0.3 %}{% set intensity = 0.3 %}{% endif %}
        {% if intensity > 1.6 %}{% set intensity = 1.6 %}{% endif %}

        {% set px  = (1.5 * intensity) | round(2) %}
        {% set deg = (5.0 * intensity) | round(2) %}

        {% if trigger_active %}
          {# If use_number is off, it will just use this "active" path always when switch is on #}
          --shape-animation: controller-rumble 0.5s ease-in-out infinite;
          --controller-led-animation: controller-led 1.5s ease-in-out infinite;
          --controller-trail-animation: controller-trail 1.2s ease-out infinite;

          /* Huge RGB glow like your lock example */
          --glow-1: 0 0 30px 10px rgba(var(--rgb-{{ config.icon_color }}), 1);
          --glow-2: 0 0 70px 22px rgba(var(--rgb-{{ config.icon_color }}), 0.7);
          --glow-3: 0 0 120px 42px rgba(var(--rgb-{{ config.icon_color }}), 0.5);
          --glow-anim: controller-ultraglow 2.0s ease-in-out infinite;

          opacity: 1;
        {% else %}
          --shape-animation: none;
          --controller-led-animation: none;
          --controller-trail-animation: none;

          --glow-1: none;
          --glow-2: none;
          --glow-3: none;
          --glow-anim: none;
          opacity: 0.6;
        {% endif %}

        transform-origin: 50% 50%;
        position: relative;
        animation: var(--shape-animation);
      }

      /* Glow layers like the lock card */
      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        inset: -10px;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        box-shadow: var(--glow-1), var(--glow-2), var(--glow-3);
        animation: var(--glow-anim);
      }

      .shape::after {
        inset: -22px;
        box-shadow:
          0 0 130px 40px rgba(var(--rgb-{{ config.icon_color }}), 0.23),
          0 0 190px 70px rgba(var(--rgb-{{ config.icon_color }}), 0.15);
        opacity: 0.9;
        animation: var(--glow-anim);
        mix-blend-mode: screen;
      }

      @keyframes controller-ultraglow {
        0% {
          opacity: 0.9;
          filter: brightness(1);
        }
        40% {
          opacity: 1;
          filter: brightness(1.4);
        }
        70% {
          opacity: 1;
          filter: brightness(1.2);
        }
        100% {
          opacity: 0.9;
          filter: brightness(1);
        }
      }

      @keyframes controller-rumble {
        0% { transform: translate(0, 0) rotate(0deg); }
        25% { transform: translate(-2px, 1px) rotate(-3deg); }
        50% { transform: translate(2px, -1px) rotate(3deg); }
        75% { transform: translate(-1px, 2px) rotate(-1deg); }
        100% { transform: translate(0, 0) rotate(0deg); }
      }

      @keyframes controller-led {
        0% {
          box-shadow:
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.8),
            0 0 16px 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9);
          filter: drop-shadow(0 0 3px rgba(var(--rgb-{{ config.icon_color }}), 0.8));
        }
        33% {
          box-shadow:
            0 0 0 6px rgba(0, 210, 255, 0.5),
            0 0 26px 6px rgba(0, 210, 255, 0.95);
          filter: drop-shadow(0 0 5px rgba(0, 210, 255, 1));
        }
        66% {
          box-shadow:
            0 0 0 10px rgba(200, 110, 255, 0.5),
            0 0 34px 10px rgba(200, 110, 255, 1);
          filter: drop-shadow(0 0 6px rgba(200, 110, 255, 1));
        }
        100% {
          box-shadow:
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.8),
            0 0 16px 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9);
          filter: drop-shadow(0 0 3px rgba(var(--rgb-{{ config.icon_color }}), 0.8));
        }
      }

      @keyframes controller-trail {
        0% {
          box-shadow:
            22px 0 22px -16px rgba(0, 255, 255, 0),
            -22px 0 22px -16px rgba(255, 0, 200, 0);
        }
        25% {
          box-shadow:
            26px -4px 26px -14px rgba(0, 255, 255, 0.8),
            -26px 4px 26px -14px rgba(255, 0, 200, 0.7);
        }
        55% {
          box-shadow:
            20px 4px 24px -14px rgba(0, 255, 160, 0.5),
            -20px -4px 24px -14px rgba(255, 210, 0, 0.4);
        }
        100% {
          box-shadow:
            22px 0 22px -16px rgba(0, 255, 255, 0),
            -22px 0 22px -16px rgba(255, 0, 200, 0);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 25px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>32 - Gaming Rig</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:desktop-tower
icon_color: white
name: Gaming Rig
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        {% set number_operator = '>' %}
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# 1. STATE CHECK #}
        {% set is_on = states(state_entity) == active_value %}

        {# 2. ANIMATION CHECK #}
        {% set should_animate = false %}
        {% if is_on %}
          {% if use_number %}
            {% set num = states(number_entity) | float(0) %}
            {% if number_operator == '>' %}
              {% set should_animate = (num > threshold) %}
            {% elif number_operator == '<' %}
              {% set should_animate = (num < threshold) %}
            {% elif number_operator == '=' %}
              {% set should_animate = (num == threshold) %}
            {% elif number_operator == '>=' %}
              {% set should_animate = (num >= threshold) %}
            {% elif number_operator == '<=' %}
              {% set should_animate = (num <= threshold) %}
            {% endif %}
          {% else %}
            {% set should_animate = true %}
          {% endif %}
        {% endif %}

        /* --- STYLING --- */

        {% if is_on %}
          /* DEVICE IS ON */
          
          {% if should_animate %}
            /* High Power / Gaming Mode */
            --fan-spin: rgb-fan 2s linear infinite;
            --case-glow: neon-breathe 2s ease-in-out infinite alternate;
            --shadow-layer: 
              0 0 15px 2px rgba(0, 255, 255, 0.6), 
              0 0 30px 10px rgba(255, 0, 255, 0.4);
            --fan-display: block;
          {% else %}
            /* Idle / Low Power Mode */
            --fan-spin: none;
            --case-glow: none;
            /* Subtle static glow indicating it is ON but idle */
            --shadow-layer: 0 0 5px 0 rgba(var(--rgb-{{ config.icon_color }}), 0.4);
            --fan-display: none;
          {% endif %}

        {% else %}
          /* DEVICE IS OFF - RESET TO DEFAULTS */
          --fan-spin: none;
          --case-glow: none;
          --shadow-layer: none;
          --fan-display: none;
        {% endif %}

        /* Boxy PC Case Shape */
        border-radius: 10px !important;
        position: relative;
        overflow: hidden; 
        transform: translateZ(0);
        
        /* Apply the shadow/glow only when ON */
        box-shadow: var(--shadow-layer);
        animation: var(--case-glow);
      }

      /* THE RGB FAN (Spinning Gradient Background) */
      .shape::before {
        content: '';
        display: var(--fan-display); /* Hidden when OFF or Idle */
        position: absolute;
        top: -50%;
        left: -50%;
        width: 200%;
        height: 200%;
        background: conic-gradient(
          from 0deg, 
          #ff0000, 
          #ff8000, 
          #ffff00, 
          #00ff00, 
          #00ffff, 
          #0000ff, 
          #ff00ff, 
          #ff0000
        );
        opacity: 0.5; 
        animation: var(--fan-spin);
        mix-blend-mode: screen; 
      }

      /* THE GLASS PANEL REFLECTION (Static Shine) */
      .shape::after {
        content: '';
        display: var(--fan-display); /* Hidden when OFF */
        position: absolute;
        inset: 0;
        background: linear-gradient(135deg, rgba(255,255,255,0.4) 0%, transparent 40%, transparent 100%);
        pointer-events: none;
      }

      /* --- ANIMATIONS --- */

      @keyframes rgb-fan {
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
      }

      @keyframes neon-breathe {
        0% { box-shadow: 0 0 15px 2px rgba(0, 255, 255, 0.6), 0 0 30px 10px rgba(255, 0, 255, 0.4); }
        100% { box-shadow: 0 0 25px 5px rgba(0, 255, 255, 0.8), 0 0 50px 20px rgba(255, 0, 255, 0.6); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -15px 0 10px -15px !important;
        padding-right: 10px;
        z-index: 1; 
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>33 - PC</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:desktop-tower
icon_color: white
name: PC
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# -------- TRIGGER DECISION LOGIC -------- #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set sensor_entity = state_entity %}
          {% if states(sensor_entity) == active_value %}
            {% set trigger_active = true %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% endif %}
        {# ------ END TRIGGER DECISION LOGIC ------ #}

        {% if trigger_active %}
          /* 1. THE RGB CYCLE: Outer glow */
          --gamer-glow: rgb-cycle 5s linear infinite;
          
          /* 2. THE POWER LED: Blinking Yellow Light */
          --power-led-anim: yellow-blink 0.5s steps(2, start) infinite;
          --led-opacity: 1;
          
          /* Show colors */
          filter: grayscale(0%);
          opacity: 1;
        {% else %}
          /* Stop Animations */
          --gamer-glow: none;
          --power-led-anim: none;
          --led-opacity: 0;

          /* Turn Gray/Monochrome */
          filter: grayscale(100%);
          opacity: 0.4;
        {% endif %}

        /* FORCE SQUARE SHAPE for PC Case look */
        border-radius: 12px !important;
        
        position: relative;
        transform: translateZ(0); 
      }

      /* The RGB LED Strip Effect (Outer Glow) */
      .shape::before {
        content: '';
        position: absolute;
        inset: 0;
        border-radius: inherit;
        z-index: -1;
        animation: var(--gamer-glow);
      }

      /* The Yellow Power Button LED */
      .shape::after {
        content: '';
        position: absolute;
        
        /* Positioning the dot to match mdi:desktop-tower power button location */
        top: 75%;
        right: 15%; 
        width: 5px;
        height: 5px;
        
        border-radius: 50%;
        background-color: #ffff; /* Bright Yellow */
        box-shadow: 0 0 5px #ffeb3b; /* Yellow Glow */
        
        opacity: var(--led-opacity);
        animation: var(--power-led-anim);
      }

      /* --- ANIMATIONS --- */

      /* RGB RAINBOW CYCLE */
      @keyframes rgb-cycle {
        0% {
          box-shadow: 
            0 0 10px 2px rgba(255, 0, 0, 0.6),    /* Red */
            inset 0 0 15px rgba(255, 0, 0, 0.2); 
        }
        25% {
          box-shadow: 
            0 0 10px 2px rgba(255, 0, 255, 0.6),  /* Purple */
            inset 0 0 15px rgba(255, 0, 255, 0.2);
        }
        50% {
          box-shadow: 
            0 0 10px 2px rgba(0, 0, 255, 0.6),    /* Blue */
            inset 0 0 15px rgba(0, 0, 255, 0.2);
        }
        75% {
          box-shadow: 
            0 0 10px 2px rgba(0, 255, 255, 0.6),  /* Cyan */
            inset 0 0 15px rgba(0, 255, 255, 0.2);
        }
        100% {
          box-shadow: 
            0 0 10px 2px rgba(255, 0, 0, 0.6),    /* Back to Red */
            inset 0 0 15px rgba(255, 0, 0, 0.2);
        }
      }

      /* YELLOW LED BLINK */
      @keyframes yellow-blink {
        0% { opacity: 1; transform: scale(1); }
        50% { opacity: 0.3; transform: scale(0.9); }
        100% { opacity: 1; transform: scale(1); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -15px 0 10px -15px !important;
        padding-right: 10px;
        z-index: 1; 
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>34 - Home Server</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:server-network
icon_color: blue
name: Home Server
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# 1. CHECK STATE (For Color) #}
        {% set is_on = states(state_entity) == active_value %}

        {# 2. CHECK ANIMATION LOGIC #}
        {% set should_animate = false %}

        {% if is_on %}
          {% if use_number %}
            {% set num = states(number_entity) | float(0) %}
            {% if number_operator == '>' %}
              {% set should_animate = (num > threshold) %}
            {% elif number_operator == '<' %}
              {% set should_animate = (num < threshold) %}
            {% elif number_operator == '=' %}
              {% set should_animate = (num == threshold) %}
            {% elif number_operator == '>=' %}
              {% set should_animate = (num >= threshold) %}
            {% elif number_operator == '<=' %}
              {% set should_animate = (num <= threshold) %}
            {% endif %}
          {% else %}
            {% set should_animate = true %}
          {% endif %}
        {% endif %}

        /* --- APPLY STYLES --- */

        /* ANIMATION TOGGLE */
        {% if should_animate %}
          /* 1. DISK I/O: Chaotic blinking lights */
          --disk-activity: hdd-blink 0.5s steps(2, start) infinite;
          
          /* 2. NETWORK LOAD: Heartbeat pulsing */
          --server-throb: network-pulse 1.5s ease-in-out infinite;
        {% else %}
          --disk-activity: none;
          --server-throb: none;
        {% endif %}

        /* STATE COLOR TOGGLE */
        {% if is_on %}
          filter: grayscale(0%);
          opacity: 1;
        {% else %}
          filter: grayscale(100%);
          opacity: 0.4;
        {% endif %}

        /* SQUARE SHAPE: Servers are boxes, not circles */
        border-radius: 12px !important;
        
        transform-origin: 50% 50%;
        position: relative;
        animation: var(--server-throb);
      }

      /* Activity LEDs (The blinking lights) */
      .shape::before {
        content: '';
        position: absolute;
        bottom: 25%;
        right: 25%;
        width: 6px;
        height: 6px;
        border-radius: 50%;
        /* Create 3 "LEDs" using box-shadows to avoid multiple elements */
        box-shadow: 
          10px 0 0 0 #00ff00, 
          0 10px 0 0 #ffaa00, 
          10px 10px 0 0 #00ff00;
        opacity: 0;
        animation: var(--disk-activity);
        z-index: 2;
      }

      /* Network/Heat Glow (Background) */
      .shape::after {
        content: '';
        position: absolute;
        inset: 0;
        border-radius: inherit;
        background: radial-gradient(circle, rgba(var(--rgb-{{ config.icon_color }}), 0.5) 0%, transparent 70%);
        opacity: 0;
        animation: var(--server-throb);
        z-index: 1;
      }

      /* --- ANIMATIONS --- */

      /* Simulates HDD Activity LEDs flickering rapidly */
      @keyframes hdd-blink {
        0%   { opacity: 0; }
        25%  { opacity: 1; }
        50%  { opacity: 0; }
        75%  { opacity: 1; }
        90%  { opacity: 0; }
        100% { opacity: 1; }
      }

      /* Simulates Network Load / "Heartbeat" */
      @keyframes network-pulse {
        0% { transform: scale(1); opacity: 0.3; }
        50% { transform: scale(1.03); opacity: 0.6; }
        100% { transform: scale(1); opacity: 0.3; }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>35 - Nintendo Switch</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:nintendo-switch
icon_color: white
name: Nintendo Switch
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %} 
        {# ========== END USER CONFIG ====== #}

        {# 1. CHECK STATE (For Color) #}
        {% set is_on = states(state_entity) == active_value %}

        {# 2. CHECK ANIMATION LOGIC #}
        {% set should_animate = false %}

        {% if is_on %}
          {% if use_number %}
            {% set num = states(number_entity) | float(0) %}
            {% if number_operator == '>' %}
              {% set should_animate = (num > threshold) %}
            {% elif number_operator == '<' %}
              {% set should_animate = (num < threshold) %}
            {% elif number_operator == '=' %}
              {% set should_animate = (num == threshold) %}
            {% elif number_operator == '>=' %}
              {% set should_animate = (num >= threshold) %}
            {% elif number_operator == '<=' %}
              {% set should_animate = (num <= threshold) %}
            {% endif %}
          {% else %}
            {% set should_animate = true %}
          {% endif %}
        {% endif %}

        {% if should_animate %}
          --joycon-glow: neon-split-big 0.5s ease-in-out infinite alternate;
          --switch-rumble: haptic-shake 0.4s linear infinite;
        {% else %}
          --joycon-glow: none;
          --switch-rumble: none;
        {% endif %}

        {% if is_on %}
          filter: grayscale(0%);
          opacity: 1;
        {% else %}
          filter: grayscale(100%);
          opacity: 0.4;
        {% endif %}

        transform-origin: 50% 50%;
        position: relative;
        overflow: visible !important;

        animation: var(--switch-rumble);
      }

      /* HUGE expanded glow */
      .shape::before {
        content: "";
        position: absolute;
        inset: -10px;
        border-radius: inherit;
        z-index: -1;
        animation: var(--joycon-glow);
      }

      /* MASSIVE dual-color neon */
      @keyframes neon-split-big {
        0% {
          box-shadow:
            /* Left red side (3-layer bloom) */
            -6px 0 12px rgba(255, 20, 20, 0.5),
            -12px 0 24px rgba(255, 20, 20, 0.35),
            -18px 0 36px rgba(255, 20, 20, 0.20),

            /* Right blue side (3-layer bloom) */
             6px 0 12px rgba(0, 200, 255, 0.5),
            12px 0 24px rgba(0, 200, 255, 0.35),
            18px 0 36px rgba(0, 200, 255, 0.20);
        }

        100% {
          box-shadow:
            /* Left — super intense bloom */
            -12px 0 24px rgba(255, 20, 20, 0.9),
            -24px 0 40px rgba(255, 20, 20, 0.65),
            -32px 0 60px rgba(255, 20, 20, 0.40),

            /* Right — super intense bloom */
             12px 0 24px rgba(0, 200, 255, 0.9),
             24px 0 40px rgba(0, 200, 255, 0.65),
             32px 0 60px rgba(0, 200, 255, 0.40);
        }
      }

      /* Rumble effect stays unchanged */
      @keyframes haptic-shake {
        0%   { transform: translate(0, 0) rotate(0deg); }
        25%  { transform: translate(-1px, 1px) rotate(-1deg); }
        50%  { transform: translate(1px, -1px) rotate(1deg); }
        75%  { transform: translate(-1px, -1px) rotate(0deg); }
        100% { transform: translate(0, 0) rotate(0deg); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display:flex;
        margin: -17px 0 10px -15px !important;
        padding-right: 15px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius,12px));
      }

```
</details>

<details>
<summary><strong>36 - Printer</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:printer
icon_color: amber
name: Printer
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# 1. CHECK STATE (For Color) #}
        {% set is_on = states(state_entity) == active_value %}

        {# 2. CHECK ANIMATION LOGIC #}
        {% set should_animate = false %}

        {% if is_on %}
          {% if use_number %}
            {% set num = states(number_entity) | float(0) %}
            {% if number_operator == '>' %}
              {% set should_animate = (num > threshold) %}
            {% elif number_operator == '<' %}
              {% set should_animate = (num < threshold) %}
            {% elif number_operator == '=' %}
              {% set should_animate = (num == threshold) %}
            {% elif number_operator == '>=' %}
              {% set should_animate = (num >= threshold) %}
            {% elif number_operator == '<=' %}
              {% set should_animate = (num <= threshold) %}
            {% endif %}
          {% else %}
            {% set should_animate = true %}
          {% endif %}
        {% endif %}

        /* --- APPLY STYLES --- */

        /* ANIMATION TOGGLE */
        {% if should_animate %}
          /* 1. SHAKE: Simulates mechanical printing vibration */
          --printer-shake: printer-vibrate 0.2s linear infinite;
          
          /* 2. SCAN: A laser/copier light bar moving down */
          --scan-beam: scanner-light 1.5s ease-in-out infinite;
          
          /* 3. LED: Status light pulsing */
          --status-led: led-blink 1s infinite alternate;
        {% else %}
          --printer-shake: none;
          --scan-beam: none;
          --status-led: none;
        {% endif %}

        /* STATE COLOR TOGGLE */
        {% if is_on %}
          filter: grayscale(0%);
          opacity: 1;
        {% else %}
          filter: grayscale(100%);
          opacity: 0.4;
        {% endif %}

        transform-origin: 50% 50%;
        position: relative;
        overflow: hidden; /* Keeps the scan beam inside the circle shape */
        
        /* Apply the mechanical shake to the whole icon */
        animation: var(--printer-shake);
      }

      /* The Scanning Light Beam */
      .shape::before {
        content: '';
        position: absolute;
        left: 0;
        right: 0;
        height: 30%; /* Height of the beam */
        background: linear-gradient(to bottom, 
          transparent 0%, 
          rgba(255, 255, 255, 0.8) 50%, 
          transparent 100%);
        top: -50%;
        animation: var(--scan-beam);
        pointer-events: none;
        mix-blend-mode: overlay;
      }

      /* The Status LED (Green/Yellow dot) */
      .shape::after {
        content: '';
        position: absolute;
        bottom: 15%;
        right: 15%;
        width: 8px;
        height: 8px;
        border-radius: 50%;
        background-color: #00ff00; /* Green LED */
        box-shadow: 0 0 5px #00ff00;
        opacity: 0; /* Hidden by default unless animating */
        animation: var(--status-led);
      }

      /* --- ANIMATIONS --- */

      /* Mechanical Shake */
      @keyframes printer-vibrate {
        0% { transform: translate(0, 0); }
        25% { transform: translate(-1px, 1px); }
        50% { transform: translate(1px, -1px); }
        75% { transform: translate(-1px, -1px); }
        100% { transform: translate(0, 0); }
      }

      /* Scanner Bar Movement */
      @keyframes scanner-light {
        0% { top: -40%; opacity: 0; }
        10% { opacity: 1; }
        90% { opacity: 1; }
        100% { top: 120%; opacity: 0; }
      }

      /* Status LED Blinking */
      @keyframes led-blink {
        0% { opacity: 0; transform: scale(0.8); }
        100% { opacity: 1; transform: scale(1.2); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>37 - Air Purifier</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:air-purifier
icon_color: light-blue
name: Air Purifier
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# 1. CHECK STATE (For Color) #}
        {% set is_on = states(state_entity) == active_value %}

        {# 2. CHECK ANIMATION LOGIC #}
        {% set should_animate = false %}

        {% if is_on %}
          {% if use_number %}
            {% set num = states(number_entity) | float(0) %}
            {% if number_operator == '>' %}
              {% set should_animate = (num > threshold) %}
            {% elif number_operator == '<' %}
              {% set should_animate = (num < threshold) %}
            {% elif number_operator == '=' %}
              {% set should_animate = (num == threshold) %}
            {% elif number_operator == '>=' %}
              {% set should_animate = (num >= threshold) %}
            {% elif number_operator == '<=' %}
              {% set should_animate = (num <= threshold) %}
            {% endif %}
          {% else %}
            {# If not using number, animate whenever ON #}
            {% set should_animate = true %}
          {% endif %}
        {% endif %}

        /* --- APPLY STYLES --- */

        /* ANIMATION TOGGLE */
        {% if should_animate %}
          /* 1. RIPPLE: Represents clean air spreading out */
          --air-flow: clean-air-ripple 2s infinite ease-out;
          /* 2. BREATH: Represents the intake motor humming */
          --core-breath: motor-breath 3s ease-in-out infinite;
        {% else %}
          --air-flow: none;
          --core-breath: none;
        {% endif %}

        /* STATE COLOR TOGGLE */
        {% if is_on %}
          filter: grayscale(0%);
          opacity: 1;
        {% else %}
          filter: grayscale(100%);
          opacity: 0.4;
        {% endif %}

        transform-origin: 50% 50%;
        position: relative;
        /* Ensure the ripple is visible outside the shape */
        overflow: visible !important;
        
        /* Apply the breathing animation to the main shape */
        animation: var(--core-breath);
      }

      /* Inner Ripple (Fast) */
      .shape::before {
        content: '';
        position: absolute;
        inset: 0;
        border-radius: inherit;
        
        animation: var(--air-flow);
        z-index: -1;
      }

      /* Outer Ripple (Delayed, Slower) */
      .shape::after {
        content: '';
        position: absolute;
        inset: 0;
        border-radius: inherit;
        background: rgba(var(--rgb-{{ config.icon_color }}), 0.1);
        animation: var(--air-flow);
        animation-duration: 3s; /* Slower expansion */
        animation-delay: 0.5s;
        z-index: -2;
      }

      /* --- ANIMATIONS --- */

      /* Expanding Rings representing Airflow */
      @keyframes clean-air-ripple {
        0% {
          transform: scale(1);
          opacity: 0.8;
          box-shadow: 0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.4);
        }
        100% {
          transform: scale(2.5);
          opacity: 0;
          box-shadow: 0 0 20px 20px rgba(var(--rgb-{{ config.icon_color }}), 0);
        }
      }

      /* Gentle "Humming" motion of the device */
      @keyframes motor-breath {
        0%   { transform: scale(1); }
        50%  { transform: scale(0.95); opacity: 0.9; }
        100% { transform: scale(1); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>38 - Awtrix Clock</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:clock-digital
icon_color: cyan
name: Awtrix Clock
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# 1. CHECK STATE (For Color) #}
        {% set is_on = states(state_entity) == active_value %}

        {# 2. CHECK ANIMATION LOGIC #}
        {% set should_animate = false %}

        {% if is_on %}
          {% if use_number %}
            {% set num = states(number_entity) | float(0) %}
            {% if number_operator == '>' %}
              {% set should_animate = (num > threshold) %}
            {% elif number_operator == '<' %}
              {% set should_animate = (num < threshold) %}
            {% elif number_operator == '=' %}
              {% set should_animate = (num == threshold) %}
            {% elif number_operator == '>=' %}
              {% set should_animate = (num >= threshold) %}
            {% elif number_operator == '<=' %}
              {% set should_animate = (num <= threshold) %}
            {% endif %}
          {% else %}
            {% set should_animate = true %}
          {% endif %}
        {% endif %}

        /* --- APPLY STYLES --- */

        /* ANIMATION TOGGLE */
        {% if should_animate %}
          /* 1. SCROLLER: Simulates text/rainbows scrolling across */
          --matrix-scroll: pixel-scroll 1.5s linear infinite;
          
          /* 2. REFRESH RATE: Subtle 60hz flicker simulation */
          --matrix-flicker: refresh-flicker 0.1s steps(2) infinite;
        {% else %}
          --matrix-scroll: none;
          
          /* Idle breathing when ON but not active */
          --matrix-flicker: idle-breathe 4s ease-in-out infinite;
        {% endif %}

        /* STATE COLOR TOGGLE */
        {% if is_on %}
          filter: grayscale(0%);
          opacity: 1;
        {% else %}
          filter: grayscale(100%);
          opacity: 0.4;
          --matrix-flicker: none; /* No breathing when off */
        {% endif %}

        /* THE MATRIX SHAPE */
        border-radius: 8px !important; /* Slightly rounded corners like Ulanzi case */
        transform-origin: 50% 50%;
        position: relative;
        overflow: hidden;
        
        /* Apply the grid pattern directly to the shape background */
        background-image: 
          linear-gradient(rgba(0,0,0,0.2) 1px, transparent 1px),
          linear-gradient(90deg, rgba(0,0,0,0.2) 1px, transparent 1px) !important;
        background-size: 4px 4px !important; /* Creates the "Pixel" look */
        
        animation: var(--matrix-flicker);
      }

      /* The Scrolling Marquee / Notification Light */
      .shape::before {
        content: '';
        position: absolute;
        top: 0;
        left: -100%; /* Start off screen */
        width: 100%;
        height: 100%;
        
        /* Rainbow Gradient Bar */
        background: linear-gradient(90deg, 
          transparent 0%, 
          rgba(255, 0, 0, 0.6) 20%, 
          rgba(255, 255, 0, 0.6) 40%, 
          rgba(0, 255, 0, 0.6) 60%, 
          rgba(0, 255, 255, 0.6) 80%, 
          transparent 100%
        );
        mix-blend-mode: color-dodge;
        animation: var(--matrix-scroll);
      }

      /* CRT/LED Scanline Glare */
      .shape::after {
        content: '';
        position: absolute;
        inset: 0;
        border-radius: inherit;
        background: linear-gradient(rgba(255,255,255,0.1) 50%, rgba(0,0,0,0.1) 50%);
        background-size: 100% 4px;
        pointer-events: none;
        z-index: 2;
      }

      /* --- ANIMATIONS --- */

      /* Simulates text/colors scrolling left to right */
      @keyframes pixel-scroll {
        0% { left: -100%; }
        100% { left: 100%; }
      }

      /* Simulates the subtle refresh rate of LED matrices */
      @keyframes refresh-flicker {
        0% { opacity: 1; }
        100% { opacity: 0.95; }
      }

      /* Standby breathing */
      @keyframes idle-breathe {
        0% { filter: brightness(1); }
        50% { filter: brightness(1.2); }
        100% { filter: brightness(1); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -15px 0 10px -15px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>39 - Freezer / Refrigerator</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:fridge-industrial
icon_color: white
name: Freezer / Refrigerator
grid_options:
  rows: 1.4
card_mod:
  style:
    .: |
      ha-card {
        /* ================= USER CONFIGURATION ================= */
        
        {% set use_number      = false %}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}
        {% set number_entity   = 'sensor.plug_power' %}

        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        {% set threshold       = 0.0 %}
        
        /* ====================================================== */

        /* --- LOGIC ENGINE (Do not edit) --- */
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %} {% set active = (num > threshold) %}
          {% elif number_operator == '<' %} {% set active = (num < threshold) %}
          {% elif number_operator == '=' %} {% set active = (num == threshold) %}
          {% elif number_operator == '>=' %} {% set active = (num >= threshold) %}
          {% elif number_operator == '<=' %} {% set active = (num <= threshold) %}
          {% else %} {% set active = false %} {% endif %}
        {% else %}
          {% set active = states(state_entity) == active_value %}
        {% endif %}

        /* --- DEFINE VARIABLES BASED ON STATE --- */
        /* These variables are passed down to the icon and used here */
        
        /* Card Styles */
        --card-bg: {{ 'linear-gradient(to bottom, #2C5364, #203A43, #0F2027)' if active else 'var(--ha-card-background, var(--card-background-color, white))' }};
       
        --card-shadow: {{ 'inset 0 0 30px rgba(200, 255, 255, 0.6)' if active else 'var(--ha-card-box-shadow, none)' }};
        
        /* Snow Visibility */
        --snow-display: {{ 'block' if active else 'none' }};
        
        /* Text Colors */
        --primary-text-color: {{ '#e0f7fa' if active else 'var(--primary-text-color)' }};
        --secondary-text-color: {{ '#b2ebf2' if active else 'var(--secondary-text-color)' }};
        
        /* Icon Animations (Passed to Shadow DOM) */
        --custom-icon-anim: {{ 'compressor-rumble 0.2s linear infinite' if active else 'none' }};
        --custom-icon-shadow: {{ '0 0 25px 5px rgba(255, 255, 255, 0.6)' if active else 'none' }};

        /* --- APPLY STYLES --- */

        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius,12px));
        background: var(--card-bg) !important;
        
        box-shadow: var(--card-shadow) !important;
        
        border-radius: 12px;
        position: relative;
        overflow: hidden;
        transition: all 0.5s ease;
      }

      /* --- LAYER 1: HEAVY FLAKES (Slow) --- */
      ha-card::before {
        content: '';
        display: var(--snow-display);
        position: absolute;
        inset: 0;
        background-image: 
          radial-gradient(circle at 20px 30px, white 2px, transparent 3px),
          radial-gradient(circle at 50px 160px, white 2px, transparent 3px),
          radial-gradient(circle at 90px 40px, white 2px, transparent 3px),
          radial-gradient(circle at 130px 80px, white 2px, transparent 3px),
          radial-gradient(circle at 160px 120px, white 2px, transparent 3px),
          radial-gradient(circle at 240px 300px, white 2px, transparent 3px),
          radial-gradient(circle at 280px 100px, white 2px, transparent 3px);
        background-size: 300px 400px; 
        background-repeat: repeat;
        animation: snow-fall-layer1 10s linear infinite;
        opacity: 0.9;
        pointer-events: none;
        z-index: 0;
      }

      /* --- LAYER 2: FINE BLIZZARD (Fast) --- */
      ha-card::after {
        content: '';
        display: var(--snow-display);
        position: absolute;
        inset: 0;
        background-image: 
          radial-gradient(circle at 10px 10px, rgba(255,255,255,0.7) 1px, transparent 2px),
          radial-gradient(circle at 30px 90px, rgba(255,255,255,0.7) 1px, transparent 2px),
          radial-gradient(circle at 80px 50px, rgba(255,255,255,0.7) 1px, transparent 2px),
          radial-gradient(circle at 110px 190px, rgba(255,255,255,0.7) 1px, transparent 2px),
          radial-gradient(circle at 150px 100px, rgba(255,255,255,0.7) 1px, transparent 2px),
          radial-gradient(circle at 220px 250px, rgba(255,255,255,0.7) 1px, transparent 2px);
        background-size: 300px 300px;
        animation: snow-fall-layer2 5s linear infinite;
        opacity: 0.6;
        pointer-events: none;
        z-index: 0;
        
      }

      /* Fix icon z-index */
      mushroom-shape-icon {
        --icon-size: 65px;
        display:flex;
        margin: -18px 0 10px -18px !important;
        padding-right: 15px;

      }
      .mushroom-state-info {
        position: relative;
        z-index: 1;
      }

      /* --- SEAMLESS FALLING ANIMATIONS --- */
      @keyframes snow-fall-layer1 {
        from { background-position: 0 0; }
        to   { background-position: 0 400px; }
      }
      @keyframes snow-fall-layer2 {
        from { background-position: 0 0; }
        to   { background-position: 0 300px; }
      }
    mushroom-shape-icon$: |
      .shape {
        --shape-animation: var(--custom-icon-anim) !important;
        ##box-shadow: var(--custom-icon-shadow) !important;
        opacity: 1;
        overflow: visible !important;
      }

      /* Define the Keyframe for the icon here */
      @keyframes compressor-rumble {
        0% { transform: translate(0, 0); }
        25% { transform: translate(-1px, 0.5px); }
        50% { transform: translate(1px, -0.5px); }
        75% { transform: translate(-0.5px, 0.5px); }
        100% { transform: translate(0, 0); }
      }

```
</details>

<details>
<summary><strong>40 - Vibration</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:vibrate
icon_color: red
name: Vibration
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# -------- TRIGGER DECISION LOGIC -------- #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set sensor_entity = state_entity %}
          {% if states(sensor_entity) == active_value %}
            {% set trigger_active = true %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% endif %}
        {# ------ END TRIGGER DECISION LOGIC ------ #}

        {% if trigger_active %}
          --shape-animation: disposal-shake 0.5s linear infinite;
          --warp-animation: disposal-shockwave 0.8s ease-out infinite;
          --stream-animation: disposal-pulse 1.5s ease-in-out infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          --warp-animation: none;
          --stream-animation: none;
          opacity: 1;
        {% endif %}

        transform-origin: 50% 50%;
        position: relative;
      }

      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        inset: 0;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        animation: var(--warp-animation);
      }

      .shape::after {
        mix-blend-mode: overlay;
        animation: var(--stream-animation);
      }

      /* THE SHAKE: Rapid movement to simulate heavy grinding motor */
      @keyframes disposal-shake {
        0% { transform: translate(1px, 1px) rotate(0deg); }
        10% { transform: translate(-1px, -2px) rotate(-1deg); }
        20% { transform: translate(-3px, 0px) rotate(1deg); }
        30% { transform: translate(3px, 2px) rotate(0deg); }
        40% { transform: translate(1px, -1px) rotate(1deg); }
        50% { transform: translate(-1px, 2px) rotate(-1deg); }
        60% { transform: translate(-3px, 1px) rotate(0deg); }
        70% { transform: translate(3px, 1px) rotate(-1deg); }
        80% { transform: translate(-1px, -1px) rotate(1deg); }
        90% { transform: translate(1px, 2px) rotate(0deg); }
        100% { transform: translate(1px, -2px) rotate(-1deg); }
      }

      /* THE SHOCKWAVE: Fast, aggressive expansion */
      @keyframes disposal-shockwave {
        0% {
          box-shadow: 0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.8);
        }
        70% {
          box-shadow: 0 0 0 15px rgba(var(--rgb-{{ config.icon_color }}), 0);
        }
        100% {
          box-shadow: 0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0);
        }
      }

      /* THE PULSE: Secondary glow to add "heat" to the look */
      @keyframes disposal-pulse {
        0% {
          box-shadow: inset 0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.4);
        }
        50% {
           box-shadow: inset 0 0 10px 4px rgba(var(--rgb-{{ config.icon_color }}), 0.1);
        }
        100% {
          box-shadow: inset 0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.4);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0 10px -18px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>41 - Water Pump</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:pump
icon_color: blue
name: Water Pump
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# 1. STATE CHECK #}
        {% set is_on = states(state_entity) == active_value %}

        {# 2. ANIMATION CHECK #}
        {% set should_animate = false %}
        {% if is_on %}
          {% if use_number %}
            {% set num = states(number_entity) | float(0) %}
            {% if number_operator == '>' %}
              {% set should_animate = (num > threshold) %}
            {% elif number_operator == '<' %}
              {% set should_animate = (num < threshold) %}
            {% elif number_operator == '=' %}
              {% set should_animate = (num == threshold) %}
            {% elif number_operator == '>=' %}
              {% set should_animate = (num >= threshold) %}
            {% elif number_operator == '<=' %}
              {% set should_animate = (num <= threshold) %}
            {% endif %}
          {% else %}
            {% set should_animate = true %}
          {% endif %}
        {% endif %}

        /* --- STYLING --- */

        {% if is_on %}
          /* DEVICE IS ON */
          
          {% if should_animate %}
            /* ACTIVELY PUMPING */
            /* 1. Internal Impeller Spin */
            --impeller-spin: hydro-spin 0.8s linear infinite;
            /* 2. Motor Vibration */
            --pump-rumble: motor-shake 0.1s ease-in-out infinite alternate;
            /* 3. Water Pressure Waves */
            --pressure-flow: flow-ripple 1.5s ease-out infinite;
            --effect-display: block;
          {% else %}
            /* IDLE (Water present but not moving) */
            --impeller-spin: none;
            --pump-rumble: none;
            --pressure-flow: none;
            --effect-display: none;
          {% endif %}

        {% else %}
          /* DEVICE IS OFF */
          --impeller-spin: none;
          --pump-rumble: none;
          --pressure-flow: none;
          --effect-display: none;
        {% endif %}

        border-radius: 50%;
        position: relative;
        overflow: visible !important;
        transform: translateZ(0);
        
        /* Shake the housing */
        animation: var(--pump-rumble);
      }

      /* THE INTERNAL IMPELLER (Spinning Gradient) */
      .shape::before {
        content: '';
        display: var(--effect-display);
        position: absolute;
        inset: 0;
        border-radius: 50%;
        /* Creates a spinning "fan blade" look inside the color */
        background: conic-gradient(
          from 0deg,
          rgba(255, 255, 255, 0) 0%,
          rgba(255, 255, 255, 0.4) 25%,
          rgba(255, 255, 255, 0) 50%,
          rgba(255, 255, 255, 0.4) 75%,
          rgba(255, 255, 255, 0) 100%
        );
        animation: var(--impeller-spin);
        mix-blend-mode: overlay;
        z-index: 1; /* Inside the shape */
      }

      /* THE PRESSURE WAVES (Outer flow) */
      .shape::after {
        content: '';
        display: var(--effect-display);
        position: absolute;
        inset: 0;
        border-radius: 50%;
        border: 2px solid rgba(var(--rgb-{{ config.icon_color }}), 0.6);
        opacity: 0;
        animation: var(--pressure-flow);
        z-index: -1; /* Outside the shape */
      }

      /* --- ANIMATIONS --- */

      /* Rapid Impeller Rotation */
      @keyframes hydro-spin {
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
      }

      /* High-frequency mechanical vibration */
      @keyframes motor-shake {
        0% { transform: translate(0.5px, 0.5px); }
        100% { transform: translate(-0.5px, -0.5px); }
      }

      /* Expanding Water Ripples */
      @keyframes flow-ripple {
        0% {
          transform: scale(1);
          opacity: 0.8;
          border-width: 4px;
        }
        100% {
          transform: scale(1.6);
          opacity: 0;
          border-width: 0px;
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -17px 0 10px -17px !important;
        padding-right: 10px;
        z-index: 1;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>42 - Washing Machine</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:washing-machine
icon_color: blue
name: Washing Machine
grid_options:
  rows: 1.4
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {% set use_number      = false %}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}
        {% set number_entity   = 'sensor.plug_power' %}
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}
          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}

        {# Logic for Animations #}
        {% if trigger_active %}
           opacity: 1;
           --wash-glow: ultra-wash-glow 1.8s ease-in-out infinite;
           --wash-drum: spin-laundry 0.6s cubic-bezier(0.4, 0.0, 0.2, 1) infinite;
           /* Added the 'thump' to match the intense style of the plug example */
           animation: ultra-wash-thump 1.8s ease-in-out infinite;
        {% else %}
           opacity: 0.8;
           --wash-glow: none;
           --wash-drum: none;
           animation: none;
        {% endif %}
        
        isolation: isolate; 
        position: relative;
      }

      /* LAYER 3 (Top): The Icon Frame */
      .shape ha-icon {
        z-index: 10;
        position: relative;
        display: block;
      }

      /* LAYER 2 (Middle): The Spinning Drum Illusion */
      .shape::after {
        content: "";
        position: absolute;
        top: 58%; 
        left: 50%;
        width: 24px; 
        height: 24px;
        border-radius: 50%;
        z-index: 2; 
        
        /* The "Wet Clothes" Texture */
        background: conic-gradient(
          from 0deg,
          transparent 0deg,
          var(--icon-color) 40deg,
          transparent 100deg,
          var(--icon-color) 160deg, 
          var(--icon-color) 200deg,
          transparent 280deg,
          var(--icon-color) 320deg
        );
        filter: blur(0.8px); 
        opacity: 0.7;

        /* Apply Animation */
        animation: var(--wash-drum);
        
        /* Hide if not active */
        {% if not trigger_active %}
          display: none;
        {% endif %}
      }

      /* LAYER 1 (Bottom): The ULTRA Glow */
      .shape::before {
        content: '';
        position: absolute;
        inset: -4px; /* Expand glow slightly outside */
        border-radius: 50%;
        z-index: 1; 
        animation: var(--wash-glow);
      }

      /* === ANIMATIONS === */

      @keyframes spin-laundry {
        0%   { transform: translate(-50%, -50%) rotate(0deg); }
        100% { transform: translate(-50%, -50%) rotate(360deg); }
      }

      /* THE REQUESTED ULTRA GLOW (Double Shadow Layer) */
      @keyframes ultra-wash-glow {
        0% {
          box-shadow:
            0 0 10px 3px rgba(var(--rgb-blue), 0.6),
            0 0 20px 8px rgba(var(--rgb-blue), 0.3);
        }
        50% {
          box-shadow:
            0 0 18px 6px rgba(var(--rgb-blue), 0.9),
            0 0 32px 12px rgba(var(--rgb-blue), 0.4);
        }
        100% {
          box-shadow:
            0 0 10px 3px rgba(var(--rgb-blue), 0.6),
            0 0 20px 8px rgba(var(--rgb-blue), 0.3);
        }
      }

      /* THUMP ANIMATION (Matches the plug scale effect) */
      @keyframes ultra-wash-thump {
        0%   { transform: scale(1); }
        50%  { transform: scale(1.05); } 
        100% { transform: scale(1); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -16px 0 10px -16px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>43 - 3D Printer</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.3d_printer_progress
tap_action:
  action: more-info
icon: mdi:printer-3d-nozzle
icon_color: purple
name: 3D Printer
grid_options:
  rows: 1.4
hold_action:
  action: none
double_tap_action:
  action: none
card_mod:
  style:
    .: |
      ha-card {
        /* ================= USER SETTINGS ================= */
        
        {% set max_val = 100 %} 
        
        /* ================================================= */

        /* --- LOGIC --- */
        {% set val = states(config.entity) | float(0) %}
        {% set active = val > 0 and val < max_val %}
        {% set is_done = val >= max_val %}
        
        /* Calculate Percentage Width */
        {% set width_pct = (val / max_val * 100) | round(2) %}
        {% if width_pct > 100 %}{% set width_pct = 100 %}{% endif %}
        
        /* --- CSS VARIABLES --- */
        --bar-width: {{ width_pct }}%;
        --bar-opacity: {{ 1 if active else 0 }};
        --done-opacity: {{ 1 if is_done else 0 }};
        
        /* Icon Variables */
        --custom-icon-anim: {{ 'printer-sequence 2.3s linear infinite' if active else 'none' }};
        --custom-icon-shadow: {{ '0 0 10px 5px rgba(var(--rgb-' ~ config.icon_color ~ '), 0.6)' if active else 'none' }};
        --custom-icon-opacity: {{ '1' if active else '1' }};
        
        /* --- CARD STYLING LOGIC --- */
        /* Only apply the dark custom background if ACTIVE. Otherwise, use default theme. */
        {% if active %}
          background-color: #1c1c1c !important;
          border: none !important;
          /* Ambient Glow */
          background-image: radial-gradient(circle at 24px 24px, rgba(var(--rgb-{{ config.icon_color }}), 0.35) 0%, rgba(var(--rgb-{{ config.icon_color }}), 0.1) 40%, transparent 80%),
                            linear-gradient(to right, rgba(255,255,255,0.1), rgba(255,255,255,0.1)) !important;
        {% else %}
          /* When Done/Idle: Reset to defaults (no custom BG color, standard border behavior if any) */
          background-image: none !important;
          box-shadow: none !important;
          /* We don't set background-color here, letting the theme take over */
        {% endif %}

        border-radius: 12px;
        position: relative;
        overflow: hidden;
        transition: all 0.5s ease;
        background-size: 100% 100%, 100% 6px !important;
        background-position: top left, bottom left !important;
        background-repeat: no-repeat !important;
      }

      /* --- THE "DONE" BADGE --- */
      ha-card::before {
        content: 'DONE';
        position: absolute;
        top: 12px;
        right: 12px;
        font-size: 10px;
        font-weight: 900;
        letter-spacing: 1px;
        color: #00ff00;
        background: rgba(0, 255, 0, 0.15);
        border: 1px solid rgba(0, 255, 0, 0.5);
        padding: 2px 6px;
        border-radius: 4px;
        box-shadow: 0 0 10px rgba(0, 255, 0, 0.2);
        
        opacity: var(--done-opacity);
        transform: scale(var(--done-opacity));
        transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        pointer-events: none; /* Let clicks pass through */
      }

      /* --- ACTIVE PROGRESS BAR (BEAM) --- */
      ha-card::after {
        content: '';
        position: absolute;
        bottom: 0; left: 0;
        height: 6px;
        width: var(--bar-width);
        
        background: linear-gradient(90deg, 
          rgba(var(--rgb-{{ config.icon_color }}), 0.4) 0%, 
          rgba(var(--rgb-{{ config.icon_color }}), 1) 100%
        );
        
        box-shadow: 0 -2px 10px rgba(var(--rgb-{{ config.icon_color }}), 0.8);
        opacity: var(--bar-opacity);
        transition: width 0.5s ease-out, opacity 0.5s ease;
        animation: bar-flow 2s infinite linear;
        pointer-events: none;
      }

      @keyframes bar-flow {
        0% { filter: brightness(1); }
        50% { filter: brightness(1.3); }
        100% { filter: brightness(1); }
      }

      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -20px 0 10px -20px !important;
        padding-right: 15px;
        padding-bottom: 15px;
      }
    mushroom-shape-icon$: |
      .shape {
        --shape-animation: var(--custom-icon-anim) !important;
        box-shadow: var(--custom-icon-shadow) !important;
        opacity: var(--custom-icon-opacity) !important;
        transform-origin: 50% 80%;
      }
      @keyframes printer-sequence {
        0%   { transform: translate(-5px, 4px) scale(0.96); }
        15%  { transform: translate(5px, 4px) scale(0.96); }
        16%  { transform: translate(5px, 2px) scale(0.98); }
        30%  { transform: translate(-5px, 2px) scale(0.98); }
        31%  { transform: translate(-5px, 0px) scale(1); }
        45%  { transform: translate(5px, 0px) scale(1); }
        46%  { transform: translate(5px, -2px) scale(1.02); }
        60%  { transform: translate(-5px, -2px) scale(1.02); }
        61%  { transform: translate(-5px, -4px) scale(1.04); }
        80%  { transform: translate(5px, -4px) scale(1.04); }
        100% { transform: translate(-5px, 4px) scale(0.96); }
      }

```
</details>

<details>
<summary><strong>44 - Open Contact (Door)</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: binary_sensor.contact_front_door_contact
tap_action:
  action: more-info
icon: mdi:door
name: Contact (Door)
grid_options:
  rows: 1.4
icon_color: red
primary_info: state
secondary_info: name
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {% set is_open = is_state(config.entity, 'on') %}

        /* LOGIC: Define colors and animations based on state */
        {% if is_open %}
           /* OPEN: Red, Dark Red Shape, Animated */
           --icon-color-set: rgb(244, 67, 54);
           --shape-color-set: rgba(160, 0, 0, 0.15); 
           --shape-animation: door-soft-open 1.7s ease-in-out infinite;
           /* Increased duration slightly for smoother persistent glow */
           --glow-animation: door-soft-glow 2.5s ease-in-out infinite;
           --beam-animation: door-soft-beam 2.5s ease-in-out infinite;
           --icon-filter: drop-shadow(0 0 6px rgba(160, 0, 0, 0.95));
        {% else %}
           /* CLOSED: Green, Dark Green Shape, Static */
           --icon-color-set: rgb(76, 175, 80);
           --shape-color-set: rgba(0, 80, 0, 0.4);
           --shape-animation: none;
           --glow-animation: none;
           --beam-animation: none;
           --icon-filter: none;
        {% endif %}

        /* Apply the variable colors defined above */
        background-color: var(--shape-color-set) !important;
        
        /* Standard positioning */
        position: relative;
        transform-origin: 25% 50%;
        animation: var(--shape-animation);
      }

      /* Color and Filter for the Icon itself */
      .shape ha-icon {
        color: var(--icon-color-set) !important;
        filter: var(--icon-filter);
      }

      /* --- ANIMATION LAYERS --- */
      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        border-radius: inherit;
        pointer-events: none;
      }

      /* Inner Glow */
      .shape::before {
        inset: -10px;
        animation: var(--glow-animation);
      }

      /* Outer Beam */
      .shape::after {
        inset: -15px;
        animation: var(--beam-animation);
        mix-blend-mode: screen;
      }

      /* --- KEYFRAMES --- */
      @keyframes door-soft-open {
        0%   { transform: rotate(0deg); }
        40%  { transform: rotate(-9deg); }
        70%  { transform: rotate(-6deg); }
        100% { transform: rotate(0deg); }
      }

      @keyframes door-soft-glow {
        0% {
          box-shadow:
            0 0 20px 0 rgba(160, 0, 0, 0.7),
            0 0 40px 6 rgba(160, 0, 0, 0.6),
            0 0 80px 14px rgba(160, 0, 0, 0.4);
        }
        50% {
          box-shadow:
            0 0 30px 4 rgba(200, 0, 0, 1),
            0 0 70px 16px rgba(200, 0, 0, 0.95),
            0 0 120px 28px rgba(200, 0, 0, 0.7);
        }
        100% {
          box-shadow:
            0 0 20px 0 rgba(160, 0, 0, 0.7),
            0 0 40px 6 rgba(160, 0, 0, 0.6),
            0 0 80px 14px rgba(160, 0, 0, 0.4);
        }
      }

      /* UPDATED: Huge halo now never fully disappears */
      @keyframes door-soft-beam {
        0% {
          /* Small, persistent base glow */
          box-shadow:
            0 0 40px 10px rgba(160, 0, 0, 0.3),
            0 0 60px 20px rgba(100, 0, 0, 0.2);
          opacity: 0.4; 
        }
        50% {
          /* Maximum Intense Glow */
          box-shadow:
            0 0 160px 60px rgba(230, 20, 20, 0.8),
            0 0 230px 100px rgba(160, 0, 0, 0.7);
          opacity: 1;
        }
        100% {
           /* Return to base glow */
          box-shadow:
            0 0 40px 10px rgba(160, 0, 0, 0.3),
            0 0 60px 20px rgba(100, 0, 0, 0.2);
          opacity: 0.4;
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 64px;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 25px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
      }

```
</details>

<details>
<summary><strong>45 - Garage Door</strong></summary>

```yaml
type: custom:mushroom-cover-card
entity: cover.garage_door
show_buttons_control: true
show_position_control: true
show_tilt_position_control: true
fill_container: false
icon: ""
card_mod:
  style:
    mushroom-shape-icon$: >
      .shape {
        /* --- LOGIC BLOCK --- */
        {% set status = states(config.entity) %}
        
        {% if status == 'closed' %}
          /* SECURE: Green */
          --main-color: var(--rgb-green);
          --effect-anim: liquid-sheen 6s ease-in-out infinite;
          --ring-display: none;
          --icon-anim: none;
          
        {% elif status == 'open' %}
          /* OPEN: Red */
          --main-color: var(--rgb-red);
          --effect-anim: soft-heartbeat 3s ease-in-out infinite;
          --ring-display: block;
          /* NEW: Icon breathes when open */
          --icon-anim: icon-alert-pulse 3s ease-in-out infinite;

        {% else %}
          /* MOVING: Orange */
          --main-color: var(--rgb-orange);
          --effect-anim: smooth-flow 2s linear infinite;
          --ring-display: none;
          /* Icon moves up/down */
          --icon-anim: nudge-icon 1s ease-in-out infinite;
        {% endif %}

        /* --- BASE STYLING --- */
        background-color: rgba(var(--main-color), 0.20) !important;
        
        --icon-color: var(--main-color) !important;
        --icon-color-disabled: var(--main-color) !important;
        --shape-color: transparent !important;
        color: rgb(var(--main-color)) !important;

        box-shadow: 0 0 20px rgba(var(--main-color), 0.2);
        
        border-radius: 16px !important;
        position: relative;
        overflow: visible !important;
        transition: background-color 0.5s ease, box-shadow 0.5s ease;
        
        /* Apply the background shape animation */
        animation: var(--effect-anim);
      }


      /* --- INNER EFFECT (Sheen / Stripes) --- */

      .shape::before {
        content: '';
        position: absolute;
        inset: 0;
        border-radius: inherit;
        background: linear-gradient(120deg, transparent 20%, rgba(255,255,255,0.2) 50%, transparent 80%);
        background-size: 200% 100%;
        opacity: 0; 
        animation: inherit; 
      }


      /* --- OUTER EFFECT (Soft Ripple for Open) --- */

      .shape::after {
        content: '';
        display: var(--ring-display);
        position: absolute;
        inset: 0;
        border-radius: inherit;
        background: rgba(var(--main-color), 0.8);
        z-index: -1;
        animation: soft-ripple 1s infinite ease-out;
      }


      /* --- ANIMATIONS --- */


      /* CLOSED: Liquid Sheen */

      @keyframes liquid-sheen {
        0%, 100% { background-position: 150% 0; box-shadow: 0 0 15px rgba(var(--main-color), 0.1); opacity: 1; }
        50% { background-position: -50% 0; box-shadow: 0 0 25px rgba(var(--main-color), 0.3); opacity: 1; }
      }

      .shape[style*="liquid-sheen"]::before { opacity: 1; animation:
      liquid-sheen 6s ease-in-out infinite; }


      /* OPEN: Background Heartbeat */

      @keyframes soft-heartbeat {
        0% { transform: scale(1); box-shadow: 0 0 10px rgba(var(--main-color), 0.2); }
        50% { transform: scale(1.03); box-shadow: 0 0 25px rgba(var(--main-color), 0.5); }
        100% { transform: scale(1); box-shadow: 0 0 10px rgba(var(--main-color), 0.2); }
      }


      /* OPEN: Icon Alert Pulse (The Icon itself scales) */

      @keyframes icon-alert-pulse {
        0% { transform: scale(1); filter: drop-shadow(0 0 0 rgba(var(--main-color), 0)); }
        50% { transform: scale(1.2); filter: drop-shadow(0 0 8px rgba(var(--main-color), 0.6)); }
        100% { transform: scale(1); filter: drop-shadow(0 0 0 rgba(var(--main-color), 0)); }
      }


      /* OPEN: Fading Ripple */

      @keyframes soft-ripple {
        0% { transform: scale(1); opacity: 0.6; }
        100% { transform: scale(1.8); opacity: 0; }
      }


      /* MOVING: Smooth Flow Background */

      @keyframes smooth-flow {
        0% { background: repeating-linear-gradient(45deg, transparent, transparent 10px, rgba(255,255,255,0.1) 10px, rgba(255,255,255,0.1) 20px); background-position: 0 0; opacity: 1; }
        100% { background: repeating-linear-gradient(45deg, transparent, transparent 10px, rgba(255,255,255,0.1) 10px, rgba(255,255,255,0.1) 20px); background-position: 28px 0; opacity: 1; }
      }


      /* MOVING: Gentle Icon Nudge */

      @keyframes nudge-icon {
        0%, 100% { transform: translateY(0); }
        50% { transform: translateY(-3px); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0 10px -15px !important;
        padding-right: 10px;
        z-index: 1;
        
        /* APPLY ICON ANIMATION HERE */
        animation: var(--icon-anim);
        transform-origin: center;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }

```
</details>

<details>
<summary><strong>46 - Living room temp (C)</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.livingroom_temperature
tap_action:
  action: more-info
icon: mdi:thermometer
name: Living room temp (C)
grid_options:
  rows: 1.4
primary_info: state
secondary_info: name
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== CONFIG ========== #}
        {% set temp = states('sensor.livingroom_temperature') | float(0) %}

        {# ------------------------------------------- #}
        {# TEMPERATURE → COLOR + EFFECT PRESETS        #}
        {# ------------------------------------------- #}

        {# DEFAULTS (will be overridden by ranges) #}
        {% set rgb = '0,140,255' %}
        {% set anim = 'temp-cold-breathe' %}
        {% set glow_anim = 'temp-cold-glow' %}
        {% set halo_anim = 'temp-cold-halo' %}
        {% set duration = 4.0 %}
        {% set intensity = 0.5 %}

        {# RANGES / COLORS #}
        {# You can change temp numbers below if needed #}

        {% if temp < 16 %}
          {# BLUE #}
          {% set rgb = '0,140,255' %}
          {% set anim = 'temp-cold-breathe' %}
          {% set glow_anim = 'temp-cold-glow' %}
          {% set halo_anim = 'temp-cold-halo' %}
          {% set duration = 4.4 %}
          {% set intensity = 0.4 %}

        {% elif temp < 18 %}
          {# YELLOW #}
          {% set rgb = '255,210,40' %}
          {% set anim = 'temp-cool-wave' %}
          {% set glow_anim = 'temp-cool-glow' %}
          {% set halo_anim = 'temp-cool-halo' %}
          {% set duration = 3.4 %}
          {% set intensity = 0.55 %}

        {% elif temp < 20 %}
          {# ORANGE #}
          {% set rgb = '255,150,40' %}
          {% set anim = 'temp-comfy-breathe' %}
          {% set glow_anim = 'temp-comfy-glow' %}
          {% set halo_anim = 'temp-comfy-halo' %}
          {% set duration = 3.0 %}
          {% set intensity = 0.6 %}

        {% elif temp < 22 %}
          {# DARK ORANGE #}
          {% set rgb = '255,115,20' %}
          {% set anim = 'temp-warm-pulse' %}
          {% set glow_anim = 'temp-warm-glow' %}
          {% set halo_anim = 'temp-warm-halo' %}
          {% set duration = 2.4 %}
          {% set intensity = 0.8 %}

        {% else %}
          {# RED #}
          {% set rgb = '255,40,40' %}
          {% set anim = 'temp-hot-shimmer' %}
          {% set glow_anim = 'temp-hot-glow' %}
          {% set halo_anim = 'temp-hot-halo' %}
          {% set duration = 2.0 %}
          {% set intensity = 1.0 %}
        {% endif %}

        {# Apply variables #}
        --temp-rgb: {{ rgb }};
        --temp-intensity: {{ intensity }};
        --shape-animation: {{ anim }} {{ duration }}s ease-in-out infinite;
        --temp-glow-animation: {{ glow_anim }} {{ (duration * 0.9) | round(2) }}s ease-in-out infinite;
        --temp-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

        opacity: 1;

        /* Icon color follows the temperature */
        --icon-color: rgba({{ rgb }}, 1);

        /* 🔧 KILL THE THEME BLUE & MAKE SHAPE NEUTRAL */
        background-color: rgba(77, 77, 77,0.1) !important;
        box-shadow: none !important;
        border: 1px solid rgba(255,255,255,0.06);

        position: relative;
        transform-origin: 50% 60%;
        animation: var(--shape-animation);
      }

      /* Glow layers */
      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        inset: -8px;
        animation: var(--temp-glow-animation);
      }

      .shape::after {
        inset: -22px;
        animation: var(--temp-halo-animation);
        mix-blend-mode: screen;
      }

      /* ========== COLD ========== */
      @keyframes temp-cold-breathe {
        0%   { transform: scale(0.96); }
        50%  { transform: scale(1.03); }
        100% { transform: scale(0.96); }
      }

      @keyframes temp-cold-glow {
        0% {
          box-shadow:
            0 0 20px 0 rgba(var(--temp-rgb), 0.6),
            0 0 34px 6 rgba(var(--temp-rgb), 0.55);
        }
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--temp-rgb), 0.95),
            0 0 50px 10px rgba(var(--temp-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 20px 0 rgba(var(--temp-rgb), 0.6),
            0 0 34px 6 rgba(var(--temp-rgb), 0.55);
        }
      }

      @keyframes temp-cold-halo {
        0% {
          box-shadow:
            0 0 80px 20px rgba(var(--temp-rgb), 0.35),
            0 -20px 80px -14px rgba(220, 240, 255, 0.55);
        }
        50% {
          box-shadow:
            0 0 130px 36px rgba(var(--temp-rgb), 0.5),
            0 -34px 100px -8px rgba(240, 250, 255, 0.8);
        }
        100% {
          box-shadow:
            0 0 80px 20px rgba(var(--temp-rgb), 0.35),
            0 -20px 80px -14px rgba(220, 240, 255, 0.55);
        }
      }

      /* ========== COOL ========== */
      @keyframes temp-cool-wave {
        0%   { transform: translateX(0); }
        25%  { transform: translateX(-1px); }
        50%  { transform: translateX(1px) translateY(-1px); }
        75%  { transform: translateX(-1px); }
        100% { transform: translateX(0); }
      }

      @keyframes temp-cool-glow {
        0% {
          box-shadow:
            0 0 22px 0 rgba(var(--temp-rgb), 0.6),
            0 0 34px 4 rgba(var(--temp-rgb), 0.7);
        }
        50% {
          box-shadow:
            0 0 28px 2 rgba(var(--temp-rgb), 0.95),
            0 0 48px 12px rgba(var(--temp-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 22px 0 rgba(var(--temp-rgb), 0.6),
            0 0 34px 4 rgba(var(--temp-rgb), 0.7);
        }
      }

      @keyframes temp-cool-halo {
        0% {
          box-shadow:
            0 0 90px 26px rgba(var(--temp-rgb), 0.35),
            0 18px 80px -12px rgba(0, 220, 255, 0.35);
        }
        50% {
          box-shadow:
            0 0 140px 42px rgba(var(--temp-rgb), 0.45),
            0 30px 110px -10px rgba(0, 255, 255, 0.5);
        }
        100% {
          box-shadow:
            0 0 90px 26px rgba(var(--temp-rgb), 0.35),
            0 18px 80px -12px rgba(0, 220, 255, 0.35);
        }
      }

      /* ========== COMFY ========== */
      @keyframes temp-comfy-breathe {
        0%   { transform: scale(0.98); }
        50%  { transform: scale(1.05); }
        100% { transform: scale(0.98); }
      }

      @keyframes temp-comfy-glow {
        50% {
          box-shadow:
            0 0 26px 4 rgba(var(--temp-rgb), 0.9),
            0 0 42px 10px rgba(var(--temp-rgb), 0.85);
        }
      }

      @keyframes temp-comfy-halo {
        50% {
          box-shadow:
            0 0 120px 40px rgba(var(--temp-rgb), 0.45),
            0 26px 80px -10px rgba(180,255,200,0.5);
        }
      }

      /* ========== WARM ========== */
      @keyframes temp-warm-pulse {
        0%   { transform: scale(1); }
        50%  { transform: scale(1.07); }
        100% { transform: scale(1); }
      }

      @keyframes temp-warm-glow {
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--temp-rgb), 0.95),
            0 0 54px 14px rgba(var(--temp-rgb), 0.9);
        }
      }

      @keyframes temp-warm-halo {
        50% {
          box-shadow:
            0 0 140px 48px rgba(var(--temp-rgb), 0.55),
            0 26px 100px -10px rgba(255,210,150,0.5);
        }
      }

      /* ========== HOT ========== */
      @keyframes temp-hot-shimmer {
        0%   { transform: scale(1); filter: blur(0); }
        50%  { transform: scale(1.08); filter: blur(0.6px); }
        100% { transform: scale(1); filter: blur(0); }
      }

      @keyframes temp-hot-glow {
        50% {
          box-shadow:
            0 0 34px 6 rgba(var(--temp-rgb), 1),
            0 0 62px 14px rgba(var(--temp-rgb), 0.95);
        }
      }

      @keyframes temp-hot-halo {
        50% {
          box-shadow:
            0 0 160px 60px rgba(var(--temp-rgb), 0.6),
            0 34px 120px -12px rgba(255,150,100,0.6);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 64px;
        --icon-color: rgba(var(--hum-rgb),1) !important;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 22px;
        padding-bottom: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
        
        /* FONT SIZE & SPACING SETTINGS */
        --card-primary-font-size: 1.5rem !important;
        
        /* Increases vertical space between primary and secondary */
        --card-primary-line-height: 1.3 !important;
      }

```
</details>

<details>
<summary><strong>47 - Living room temp (F)</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.livingroom_temperature_fah
tap_action:
  action: more-info
icon: mdi:thermometer
name: Living room temp (F)
grid_options:
  rows: 1.4
primary_info: state
secondary_info: name
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== CONFIG (FAHRENHEIT) ========== #}
        {% set temp = states('sensor.livingroom_temperature_fah') | float(0) %}

        {# DEFAULTS (overridden by ranges) #}
        {% set rgb = '0,140,255' %}
        {% set anim = 'temp-cold-breathe' %}
        {% set glow_anim = 'temp-cold-glow' %}
        {% set halo_anim = 'temp-cold-halo' %}
        {% set duration = 4.0 %}
        {% set intensity = 0.5 %}

        {# RANGES / COLORS #}
        {# You can change temp numbers below if needed #}

        {% if temp < 64 %}
          {# BLUE - COLD #}
          {% set rgb = '0,140,255' %}
          {% set anim = 'temp-cold-breathe' %}
          {% set glow_anim = 'temp-cold-glow' %}
          {% set halo_anim = 'temp-cold-halo' %}
          {% set duration = 4.4 %}
          {% set intensity = 0.4 %}

        {% elif temp < 68 %}
          {# YELLOW - COOL #}
          {% set rgb = '255,210,40' %}
          {% set anim = 'temp-cool-wave' %}
          {% set glow_anim = 'temp-cool-glow' %}
          {% set halo_anim = 'temp-cool-halo' %}
          {% set duration = 3.4 %}
          {% set intensity = 0.55 %}

        {% elif temp < 72 %}
          {# ORANGE - COMFY #}
          {% set rgb = '255,150,40' %}
          {% set anim = 'temp-comfy-breathe' %}
          {% set glow_anim = 'temp-comfy-glow' %}
          {% set halo_anim = 'temp-comfy-halo' %}
          {% set duration = 3.0 %}
          {% set intensity = 0.6 %}

        {% elif temp < 76 %}
          {# DARK ORANGE - WARM #}
          {% set rgb = '255,115,20' %}
          {% set anim = 'temp-warm-pulse' %}
          {% set glow_anim = 'temp-warm-glow' %}
          {% set halo_anim = 'temp-warm-halo' %}
          {% set duration = 2.4 %}
          {% set intensity = 0.8 %}

        {% else %}
          {# RED - HOT #}
          {% set rgb = '255,40,40' %}
          {% set anim = 'temp-hot-shimmer' %}
          {% set glow_anim = 'temp-hot-glow' %}
          {% set halo_anim = 'temp-hot-halo' %}
          {% set duration = 2.0 %}
          {% set intensity = 1.0 %}
        {% endif %}

        {# Apply variables #}
        --temp-rgb: {{ rgb }};
        --temp-intensity: {{ intensity }};
        --shape-animation: {{ anim }} {{ duration }}s ease-in-out infinite;
        --temp-glow-animation: {{ glow_anim }} {{ (duration * 0.9) | round(2) }}s ease-in-out infinite;
        --temp-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

        opacity: 1;

        /* Icon color follows the temperature */
        --icon-color: rgba({{ rgb }}, 1);

        /* Neutral pill, no theme blue */
        background-color: rgba(77,77,77,0.2) !important;
        box-shadow: none !important;
        border: 1px solid rgba(255,255,255,0.06);

        position: relative;
        transform-origin: 50% 60%;
        animation: var(--shape-animation);
      }

      /* Glow layers */
      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        inset: -8px;
        animation: var(--temp-glow-animation);
      }

      .shape::after {
        inset: -22px;
        animation: var(--temp-halo-animation);
        mix-blend-mode: screen;
      }

      /* ========== COLD (blue) ========== */
      @keyframes temp-cold-breathe {
        0%   { transform: scale(0.96); }
        50%  { transform: scale(1.03); }
        100% { transform: scale(0.96); }
      }

      @keyframes temp-cold-glow {
        0% {
          box-shadow:
            0 0 20px 0 rgba(var(--temp-rgb), 0.6),
            0 0 34px 6 rgba(var(--temp-rgb), 0.55);
        }
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--temp-rgb), 0.95),
            0 0 50px 10px rgba(var(--temp-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 20px 0 rgba(var(--temp-rgb), 0.6),
            0 0 34px 6 rgba(var(--temp-rgb), 0.55);
        }
      }

      @keyframes temp-cold-halo {
        0% {
          box-shadow:
            0 0 80px 20px rgba(var(--temp-rgb), 0.35),
            0 -20px 80px -14px rgba(220, 240, 255, 0.55);
        }
        50% {
          box-shadow:
            0 0 130px 36px rgba(var(--temp-rgb), 0.5),
            0 -34px 100px -8px rgba(240, 250, 255, 0.8);
        }
        100% {
          box-shadow:
            0 0 80px 20px rgba(var(--temp-rgb), 0.35),
            0 -20px 80px -14px rgba(220, 240, 255, 0.55);
        }
      }

      /* ========== COOL / YELLOW ========== */
      @keyframes temp-cool-wave {
        0%   { transform: translateX(0); }
        25%  { transform: translateX(-1px); }
        50%  { transform: translateX(1px) translateY(-1px); }
        75%  { transform: translateX(-1px); }
        100% { transform: translateX(0); }
      }

      @keyframes temp-cool-glow {
        0% {
          box-shadow:
            0 0 22px 0 rgba(var(--temp-rgb), 0.6),
            0 0 34px 4 rgba(var(--temp-rgb), 0.7);
        }
        50% {
          box-shadow:
            0 0 28px 2 rgba(var(--temp-rgb), 0.95),
            0 0 48px 12px rgba(var(--temp-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 22px 0 rgba(var(--temp-rgb), 0.6),
            0 0 34px 4 rgba(var(--temp-rgb), 0.7);
        }
      }

      @keyframes temp-cool-halo {
        0% {
          box-shadow:
            0 0 90px 26px rgba(var(--temp-rgb), 0.35),
            0 18px 80px -12px rgba(0, 220, 255, 0.35);
        }
        50% {
          box-shadow:
            0 0 140px 42px rgba(var(--temp-rgb), 0.45),
            0 30px 110px -10px rgba(0, 255, 255, 0.5);
        }
        100% {
          box-shadow:
            0 0 90px 26px rgba(var(--temp-rgb), 0.35),
            0 18px 80px -12px rgba(0, 220, 255, 0.35);
        }
      }

      /* ========== COMFY / ORANGE ========== */
      @keyframes temp-comfy-breathe {
        0%   { transform: scale(0.98); }
        50%  { transform: scale(1.05); }
        100% { transform: scale(0.98); }
      }

      @keyframes temp-comfy-glow {
        50% {
          box-shadow:
            0 0 26px 4 rgba(var(--temp-rgb), 0.9),
            0 0 42px 10px rgba(var(--temp-rgb), 0.85);
        }
      }

      @keyframes temp-comfy-halo {
        50% {
          box-shadow:
            0 0 120px 40px rgba(var(--temp-rgb), 0.45),
            0 26px 80px -10px rgba(180,255,200,0.5);
        }
      }

      /* ========== WARM / DARK ORANGE ========== */
      @keyframes temp-warm-pulse {
        0%   { transform: scale(1); }
        50%  { transform: scale(1.07); }
        100% { transform: scale(1); }
      }

      @keyframes temp-warm-glow {
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--temp-rgb), 0.95),
            0 0 54px 14px rgba(var(--temp-rgb), 0.9);
        }
      }

      @keyframes temp-warm-halo {
        50% {
          box-shadow:
            0 0 140px 48px rgba(var(--temp-rgb), 0.55),
            0 26px 100px -10px rgba(255,210,150,0.5);
        }
      }

      /* ========== HOT / RED ========== */
      @keyframes temp-hot-shimmer {
        0%   { transform: scale(1); filter: blur(0); }
        50%  { transform: scale(1.08); filter: blur(0.6px); }
        100% { transform: scale(1); filter: blur(0); }
      }

      @keyframes temp-hot-glow {
        50% {
          box-shadow:
            0 0 34px 6 rgba(var(--temp-rgb), 1),
            0 0 62px 14px rgba(var(--temp-rgb), 0.95);
        }
      }

      @keyframes temp-hot-halo {
        50% {
          box-shadow:
            0 0 160px 60px rgba(var(--temp-rgb), 0.6),
            0 34px 120px -12px rgba(255,150,100,0.6);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 64px;
        --icon-color: rgba(var(--hum-rgb),1) !important;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 22px;
        padding-bottom: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
        
        /* FONT SIZE & SPACING SETTINGS */
        --card-primary-font-size: 1.5rem !important;
        
        /* Increases vertical space between primary and secondary */
        --card-primary-line-height: 1.3 !important;
      }

```
</details>

<details>
<summary><strong>48 - Living room humidity</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.livingroom_humidity
tap_action:
  action: more-info
icon: mdi:water-percent
name: Living room humidity
grid_options:
  rows: 1.4
primary_info: state
secondary_info: name
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== CONFIG ========== #}
        {% set hum = states('sensor.livingroom_humidity') | float(0) %}

        {# DEFAULTS #}
        {% set rgb = '120,210,255' %}
        {% set anim = 'hum-good-breathe' %}
        {% set glow_anim = 'hum-good-glow' %}
        {% set halo_anim = 'hum-good-halo' %}
        {% set duration = 3.2 %}

        {# RANGES / COLORS #}
        {# You can change number below if needed #}

        {% if hum < 40 %}
          {# BAD - dry - dark blue #}
          {% set rgb = '0,80,200' %}
          {% set anim = 'hum-bad-pulse' %}
          {% set glow_anim = 'hum-bad-glow' %}
          {% set halo_anim = 'hum-bad-halo' %}
          {% set duration = 2.8 %}
        {% elif hum <= 60 %}
          {# GOOD - light blue #}
          {% set rgb = '120,210,255' %}
          {% set anim = 'hum-good-breathe' %}
          {% set glow_anim = 'hum-good-glow' %}
          {% set halo_anim = 'hum-good-halo' %}
          {% set duration = 3.4 %}
        {% else %}
          {# MIDDLE / humid - medium blue #}
          {% set rgb = '40,140,255' %}
          {% set anim = 'hum-mid-wave' %}
          {% set glow_anim = 'hum-mid-glow' %}
          {% set halo_anim = 'hum-mid-halo' %}
          {% set duration = 3.0 %}
        {% endif %}

        --hum-rgb: {{ rgb }};
        --shape-animation: {{ anim }} {{ duration }}s ease-in-out infinite;
        --hum-glow-animation: {{ glow_anim }} {{ (duration * 0.9) | round(2) }}s ease-in-out infinite;
        --hum-halo-animation: {{ halo_anim }} {{ (duration * 1.1) | round(2) }}s ease-in-out infinite;

        /* Icon color follows humidity color */
        --icon-color: rgba({{ rgb }}, 1);

        /* Neutral pill so theme blue does not leak through */
        background-color: rgba(77,77,77,0.2) !important;
        box-shadow: none !important;
        border: 1px solid rgba(255,255,255,0.06);

        opacity: 1;
        position: relative;
        transform-origin: 50% 60%;
        animation: var(--shape-animation);
      }

      /* Glow layers */
      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        inset: -8px;
        animation: var(--hum-glow-animation);
      }

      .shape::after {
        inset: -22px;
        animation: var(--hum-halo-animation);
        mix-blend-mode: screen;
      }

      /* ========== GOOD - light blue ========== */
      @keyframes hum-good-breathe {
        0%   { transform: scale(0.98); }
        50%  { transform: scale(1.04); }
        100% { transform: scale(0.98); }
      }

      @keyframes hum-good-glow {
        0% {
          box-shadow:
            0 0 18px 0 rgba(var(--hum-rgb), 0.55),
            0 0 30px 4 rgba(var(--hum-rgb), 0.6);
        }
        50% {
          box-shadow:
            0 0 24px 4 rgba(var(--hum-rgb), 0.9),
            0 0 44px 10px rgba(var(--hum-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 18px 0 rgba(var(--hum-rgb), 0.55),
            0 0 30px 4 rgba(var(--hum-rgb), 0.6);
        }
      }

      @keyframes hum-good-halo {
        0% {
          box-shadow:
            0 0 80px 24px rgba(var(--hum-rgb), 0.35),
            0 18px 70px -12px rgba(180,230,255,0.3);
        }
        50% {
          box-shadow:
            0 0 120px 40px rgba(var(--hum-rgb), 0.45),
            0 26px 90px -10px rgba(200,240,255,0.45);
        }
        100% {
          box-shadow:
            0 0 80px 24px rgba(var(--hum-rgb), 0.35),
            0 18px 70px -12px rgba(180,230,255,0.3);
        }
      }

      /* ========== MIDDLE / humid - medium blue ========== */
      @keyframes hum-mid-wave {
        0%   { transform: translateX(0); }
        25%  { transform: translateX(-1px); }
        50%  { transform: translateX(1px) translateY(-1px); }
        75%  { transform: translateX(-1px); }
        100% { transform: translateX(0); }
      }

      @keyframes hum-mid-glow {
        0% {
          box-shadow:
            0 0 20px 0 rgba(var(--hum-rgb), 0.6),
            0 0 32px 4 rgba(var(--hum-rgb), 0.7);
        }
        50% {
          box-shadow:
            0 0 28px 3 rgba(var(--hum-rgb), 0.95),
            0 0 48px 10px rgba(var(--hum-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 20px 0 rgba(var(--hum-rgb), 0.6),
            0 0 32px 4 rgba(var(--hum-rgb), 0.7);
        }
      }

      @keyframes hum-mid-halo {
        0% {
          box-shadow:
            0 0 90px 26px rgba(var(--hum-rgb), 0.4),
            0 18px 80px -12px rgba(80,190,255,0.35);
        }
        50% {
          box-shadow:
            0 0 135px 42px rgba(var(--hum-rgb), 0.5),
            0 28px 105px -10px rgba(100,210,255,0.5);
        }
        100% {
          box-shadow:
            0 0 90px 26px rgba(var(--hum-rgb), 0.4),
            0 18px 80px -12px rgba(80,190,255,0.35);
        }
      }

      /* ========== BAD - dry - dark blue ========== */
      @keyframes hum-bad-pulse {
        0%   { transform: scale(0.97); }
        40%  { transform: scale(1.03); }
        100% { transform: scale(0.97); }
      }

      @keyframes hum-bad-glow {
        0% {
          box-shadow:
            0 0 18px 0 rgba(var(--hum-rgb), 0.6),
            0 0 28px 4 rgba(var(--hum-rgb), 0.7);
        }
        50% {
          box-shadow:
            0 0 26px 4 rgba(var(--hum-rgb), 0.95),
            0 0 44px 12px rgba(var(--hum-rgb), 0.9);
        }
        100% {
          box-shadow:
            0 0 18px 0 rgba(var(--hum-rgb), 0.6),
            0 0 28px 4 rgba(var(--hum-rgb), 0.7);
        }
      }

      @keyframes hum-bad-halo {
        0% {
          box-shadow:
            0 0 80px 22px rgba(var(--hum-rgb), 0.45),
            0 18px 75px -10px rgba(0,70,160,0.5);
        }
        50% {
          box-shadow:
            0 0 130px 40px rgba(var(--hum-rgb), 0.6),
            0 26px 100px -8px rgba(0,90,190,0.65);
        }
        100% {
          box-shadow:
            0 0 80px 22px rgba(var(--hum-rgb), 0.45),
            0 18px 75px -10px rgba(0,70,160,0.5);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 64px;
        --icon-color: rgba(var(--hum-rgb),1) !important;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 22px;
        padding-bottom: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
        
        /* FONT SIZE & SPACING SETTINGS */
        --card-primary-font-size: 1.5rem !important;
        
        /* Increases vertical space between primary and secondary */
        --card-primary-line-height: 1.3 !important;
      }

```
</details>

<details>
<summary><strong>49 - Air quality Home</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: air_quality.air_quality_home
tap_action:
  action: more-info
icon: mdi:air-filter
name: Air quality Home
grid_options:
  rows: 1.4
primary_info: state
secondary_info: name
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== CONFIG (EUROPEAN AQI STYLE, PM2.5) ========== #}
        {% set aqi = states('air_quality.air_quality_home') | float(0) %}

        {# DEFAULTS (overridden by ranges) #}
        {% set rgb = '40,190,100' %}
        {% set anim = 'aq-good-breathe' %}
        {% set glow_anim = 'aq-good-glow' %}
        {% set halo_anim = 'aq-good-halo' %}
        {% set duration = 3.2 %}

        {# EAQI PM2.5 BANDS (µg/m3, 1 hour)
           0   - 5    -> Good (dark green)
           6   - 15   -> Fair (light green)
           16  - 50   -> Moderate (yellow)
           51  - 90   -> Poor (orange)
           91  - 140  -> Very poor (red)
           > 140      -> Extremely poor (dark maroon)
        #}

        {# RANGES / COLORS #}
        {# You can change aqi number below if needed #}


        {% if aqi <= 5 %}
          {# GOOD #}
          {% set rgb = '40,190,100' %}
          {% set anim = 'aq-good-breathe' %}
          {% set glow_anim = 'aq-good-glow' %}
          {% set halo_anim = 'aq-good-halo' %}
          {% set duration = 3.4 %}

        {% elif aqi <= 15 %}
          {# FAIR #}
          {% set rgb = '140,220,140' %}
          {% set anim = 'aq-fair-wave' %}
          {% set glow_anim = 'aq-fair-glow' %}
          {% set halo_anim = 'aq-fair-halo' %}
          {% set duration = 3.2 %}

        {% elif aqi <= 50 %}
          {# MODERATE #}
          {% set rgb = '255,215,70' %}
          {% set anim = 'aq-moderate-wave' %}
          {% set glow_anim = 'aq-moderate-glow' %}
          {% set halo_anim = 'aq-moderate-halo' %}
          {% set duration = 3.0 %}

        {% elif aqi <= 90 %}
          {# POOR #}
          {% set rgb = '255,170,60' %}
          {% set anim = 'aq-poor-pulse' %}
          {% set glow_anim = 'aq-poor-glow' %}
          {% set halo_anim = 'aq-poor-halo' %}
          {% set duration = 2.8 %}

        {% elif aqi <= 140 %}
          {# VERY POOR #}
          {% set rgb = '230,60,60' %}
          {% set anim = 'aq-verypoor-throb' %}
          {% set glow_anim = 'aq-verypoor-glow' %}
          {% set halo_anim = 'aq-verypoor-halo' %}
          {% set duration = 2.4 %}

        {% else %}
          {# EXTREMELY POOR #}
          {% set rgb = '120,0,70' %}
          {% set anim = 'aq-extreme-smog' %}
          {% set glow_anim = 'aq-extreme-glow' %}
          {% set halo_anim = 'aq-extreme-halo' %}
          {% set duration = 2.0 %}
        {% endif %}

        --aq-rgb: {{ rgb }};
        --shape-animation: {{ anim }} {{ duration }}s ease-in-out infinite;
        --aq-glow-animation: {{ glow_anim }} {{ (duration * 0.9) | round(2) }}s ease-in-out infinite;
        --aq-halo-animation: {{ halo_anim }} {{ (duration * 1.1) | round(2) }}s ease-in-out infinite;

        /* icon color follows AQ color */
        --icon-color: rgba({{ rgb }}, 1);

        /* neutral pill so theme color does not bleed */
        background-color: rgba(77,77,77,0.12) !important;
        box-shadow: none !important;
        border: 1px solid rgba(255,255,255,0.06);

        opacity: 1;
        position: relative;
        transform-origin: 50% 60%;
        animation: var(--shape-animation);
      }

      /* glow layers */
      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        inset: -8px;
        animation: var(--aq-glow-animation);
      }

      .shape::after {
        inset: -22px;
        animation: var(--aq-halo-animation);
        mix-blend-mode: screen;
      }

      /* ========== GOOD (green) ========== */
      @keyframes aq-good-breathe {
        0%   { transform: scale(0.98); }
        50%  { transform: scale(1.04); }
        100% { transform: scale(0.98); }
      }

      @keyframes aq-good-glow {
        0% {
          box-shadow:
            0 0 18px 0 rgba(var(--aq-rgb), 0.55),
            0 0 30px 4 rgba(var(--aq-rgb), 0.6);
        }
        50% {
          box-shadow:
            0 0 24px 4 rgba(var(--aq-rgb), 0.9),
            0 0 40px 10px rgba(var(--aq-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 18px 0 rgba(var(--aq-rgb), 0.55),
            0 0 30px 4 rgba(var(--aq-rgb), 0.6);
        }
      }

      @keyframes aq-good-halo {
        0% {
          box-shadow:
            0 0 80px 24px rgba(var(--aq-rgb), 0.35),
            0 18px 70px -12px rgba(180,255,210,0.3);
        }
        50% {
          box-shadow:
            0 0 120px 40px rgba(var(--aq-rgb), 0.45),
            0 26px 90px -10px rgba(200,255,220,0.45);
        }
        100% {
          box-shadow:
            0 0 80px 24px rgba(var(--aq-rgb), 0.35),
            0 18px 70px -12px rgba(180,255,210,0.3);
        }
      }

      /* ========== FAIR (light green) ========== */
      @keyframes aq-fair-wave {
        0%   { transform: translateX(0); }
        25%  { transform: translateX(-1px); }
        50%  { transform: translateX(1px) translateY(-1px); }
        75%  { transform: translateX(-1px); }
        100% { transform: translateX(0); }
      }

      @keyframes aq-fair-glow {
        0% {
          box-shadow:
            0 0 18px 0 rgba(var(--aq-rgb), 0.55),
            0 0 30px 4 rgba(var(--aq-rgb), 0.6);
        }
        50% {
          box-shadow:
            0 0 24px 3 rgba(var(--aq-rgb), 0.9),
            0 0 40px 9px rgba(var(--aq-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 18px 0 rgba(var(--aq-rgb), 0.55),
            0 0 30px 4 rgba(var(--aq-rgb), 0.6);
        }
      }

      @keyframes aq-fair-halo {
        0% {
          box-shadow:
            0 0 85px 26px rgba(var(--aq-rgb), 0.35),
            0 18px 75px -12px rgba(200,255,210,0.3);
        }
        50% {
          box-shadow:
            0 0 125px 42px rgba(var(--aq-rgb), 0.45),
            0 26px 95px -10px rgba(215,255,225,0.45);
        }
        100% {
          box-shadow:
            0 0 85px 26px rgba(var(--aq-rgb), 0.35),
            0 18px 75px -12px rgba(200,255,210,0.3);
        }
      }

      /* ========== MODERATE (yellow) ========== */
      @keyframes aq-moderate-wave {
        0%   { transform: translateX(0); }
        25%  { transform: translateX(-1px); }
        50%  { transform: translateX(1px) translateY(-1px); }
        75%  { transform: translateX(-1px); }
        100% { transform: translateX(0); }
      }

      @keyframes aq-moderate-glow {
        0% {
          box-shadow:
            0 0 20px 0 rgba(var(--aq-rgb), 0.6),
            0 0 32px 4 rgba(var(--aq-rgb), 0.7);
        }
        50% {
          box-shadow:
            0 0 26px 3 rgba(var(--aq-rgb), 0.95),
            0 0 44px 10px rgba(var(--aq-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 20px 0 rgba(var(--aq-rgb), 0.6),
            0 0 32px 4 rgba(var(--aq-rgb), 0.7);
        }
      }

      @keyframes aq-moderate-halo {
        0% {
          box-shadow:
            0 0 90px 28px rgba(var(--aq-rgb), 0.4),
            0 20px 80px -10px rgba(255,240,170,0.3);
        }
        50% {
          box-shadow:
            0 0 135px 44px rgba(var(--aq-rgb), 0.5),
            0 30px 105px -8px rgba(255,250,190,0.45);
        }
        100% {
          box-shadow:
            0 0 90px 28px rgba(var(--aq-rgb), 0.4),
            0 20px 80px -10px rgba(255,240,170,0.3);
        }
      }

      /* ========== POOR (orange) ========== */
      @keyframes aq-poor-pulse {
        0%   { transform: scale(0.99); }
        50%  { transform: scale(1.06); }
        100% { transform: scale(0.99); }
      }

      @keyframes aq-poor-glow {
        0% {
          box-shadow:
            0 0 22px 0 rgba(var(--aq-rgb), 0.65),
            0 0 34px 4 rgba(var(--aq-rgb), 0.75);
        }
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--aq-rgb), 1),
            0 0 50px 12px rgba(var(--aq-rgb), 0.9);
        }
        100% {
          box-shadow:
            0 0 22px 0 rgba(var(--aq-rgb), 0.65),
            0 0 34px 4 rgba(var(--aq-rgb), 0.75);
        }
      }

      @keyframes aq-poor-halo {
        0% {
          box-shadow:
            0 0 100px 34px rgba(var(--aq-rgb), 0.5),
            0 24px 90px -10px rgba(255,210,150,0.45);
        }
        50% {
          box-shadow:
            0 0 145px 50px rgba(var(--aq-rgb), 0.6),
            0 32px 115px -8px rgba(255,220,170,0.55);
        }
        100% {
          box-shadow:
            0 0 100px 34px rgba(var(--aq-rgb), 0.5),
            0 24px 90px -10px rgba(255,210,150,0.45);
        }
      }

      /* ========== VERY POOR (red) ========== */
      @keyframes aq-verypoor-throb {
        0%   { transform: scale(1); }
        40%  { transform: scale(1.07); }
        100% { transform: scale(1); }
      }

      @keyframes aq-verypoor-glow {
        0% {
          box-shadow:
            0 0 24px 0 rgba(var(--aq-rgb), 0.75),
            0 0 38px 6 rgba(var(--aq-rgb), 0.8);
        }
        50% {
          box-shadow:
            0 0 34px 4 rgba(var(--aq-rgb), 1),
            0 0 60px 14px rgba(var(--aq-rgb), 0.95);
        }
        100% {
          box-shadow:
            0 0 24px 0 rgba(var(--aq-rgb), 0.75),
            0 0 38px 6 rgba(var(--aq-rgb), 0.8);
        }
      }

      @keyframes aq-verypoor-halo {
        0% {
          box-shadow:
            0 0 120px 40px rgba(var(--aq-rgb), 0.55),
            0 30px 110px -10px rgba(150,60,60,0.55);
        }
        50% {
          box-shadow:
            0 0 170px 64px rgba(var(--aq-rgb), 0.7),
            0 40px 140px -8px rgba(180,80,80,0.7);
        }
        100% {
          box-shadow:
            0 0 120px 40px rgba(var(--aq-rgb), 0.55),
            0 30px 110px -10px rgba(150,60,60,0.55);
        }
      }

      /* ========== EXTREMELY POOR (dark maroon) ========== */
      @keyframes aq-extreme-smog {
        0%   { transform: scale(1); filter: blur(0); }
        35%  { transform: scale(1.1) translateY(-1px); filter: blur(0.6px); }
        100% { transform: scale(1); filter: blur(0); }
      }

      @keyframes aq-extreme-glow {
        0% {
          box-shadow:
            0 0 26px 0 rgba(var(--aq-rgb), 0.85),
            0 0 44px 8 rgba(var(--aq-rgb), 0.9);
        }
        50% {
          box-shadow:
            0 0 38px 6 rgba(var(--aq-rgb), 1),
            0 0 70px 18px rgba(var(--aq-rgb), 0.98);
        }
        100% {
          box-shadow:
            0 0 26px 0 rgba(var(--aq-rgb), 0.85),
            0 0 44px 8 rgba(var(--aq-rgb), 0.9);
        }
      }

      @keyframes aq-extreme-halo {
        0% {
          box-shadow:
            0 0 180px 60px rgba(var(--aq-rgb), 0.7),
            0 40px 150px -10px rgba(60,0,30,0.7);
        }
        50% {
          box-shadow:
            0 0 230px 90px rgba(var(--aq-rgb), 0.85),
            0 52px 180px -8px rgba(90,0,45,0.85);
        }
        100% {
          box-shadow:
            0 0 180px 60px rgba(var(--aq-rgb), 0.7),
            0 40px 150px -10px rgba(60,0,30,0.7);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 64px;
        --icon-color: rgba(var(--hum-rgb),1) !important;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 22px;
        padding-bottom: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
        
        /* FONT SIZE & SPACING SETTINGS */
        --card-primary-font-size: 1.5rem !important;
        
        /* Increases vertical space between primary and secondary */
        --card-primary-line-height: 1.3 !important;
      }

```
</details>

<details>
<summary><strong>50 - Air quality Amsterdam</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.livingroom_air_quality_eu
tap_action:
  action: more-info
icon: mdi:air-filter
name: Air quality Amsterdam
grid_options:
  rows: 1.4
primary_info: state
secondary_info: name
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== CONFIG (EUROPEAN AQI STYLE, PM2.5) ========== #}
        {% set aqi = states('sensor.livingroom_air_quality_eu') | float(0) %}

        {# DEFAULTS (overridden by ranges) #}
        {% set rgb = '40,190,100' %}
        {% set anim = 'aq-good-breathe' %}
        {% set glow_anim = 'aq-good-glow' %}
        {% set halo_anim = 'aq-good-halo' %}
        {% set duration = 3.2 %}

        {# EAQI PM2.5 BANDS (µg/m3, 1 hour)
           0   - 5    -> Good (dark green)
           6   - 15   -> Fair (light green)
           16  - 50   -> Moderate (yellow)
           51  - 90   -> Poor (orange)
           91  - 140  -> Very poor (red)
           > 140      -> Extremely poor (dark maroon)
        #}

        {# RANGES / COLORS #}
        {# You can change aqi number below if needed #}

        {% if aqi <= 5 %}
          {# GOOD #}
          {% set rgb = '40,190,100' %}
          {% set anim = 'aq-good-breathe' %}
          {% set glow_anim = 'aq-good-glow' %}
          {% set halo_anim = 'aq-good-halo' %}
          {% set duration = 3.4 %}

        {% elif aqi <= 15 %}
          {# FAIR #}
          {% set rgb = '140,220,140' %}
          {% set anim = 'aq-fair-wave' %}
          {% set glow_anim = 'aq-fair-glow' %}
          {% set halo_anim = 'aq-fair-halo' %}
          {% set duration = 3.2 %}

        {% elif aqi <= 50 %}
          {# MODERATE #}
          {% set rgb = '255,215,70' %}
          {% set anim = 'aq-moderate-wave' %}
          {% set glow_anim = 'aq-moderate-glow' %}
          {% set halo_anim = 'aq-moderate-halo' %}
          {% set duration = 3.0 %}

        {% elif aqi <= 90 %}
          {# POOR #}
          {% set rgb = '255,170,60' %}
          {% set anim = 'aq-poor-pulse' %}
          {% set glow_anim = 'aq-poor-glow' %}
          {% set halo_anim = 'aq-poor-halo' %}
          {% set duration = 2.8 %}

        {% elif aqi <= 140 %}
          {# VERY POOR #}
          {% set rgb = '230,60,60' %}
          {% set anim = 'aq-verypoor-throb' %}
          {% set glow_anim = 'aq-verypoor-glow' %}
          {% set halo_anim = 'aq-verypoor-halo' %}
          {% set duration = 2.4 %}

        {% else %}
          {# EXTREMELY POOR #}
          {% set rgb = '120,0,70' %}
          {% set anim = 'aq-extreme-smog' %}
          {% set glow_anim = 'aq-extreme-glow' %}
          {% set halo_anim = 'aq-extreme-halo' %}
          {% set duration = 2.0 %}
        {% endif %}

        --aq-rgb: {{ rgb }};
        --shape-animation: {{ anim }} {{ duration }}s ease-in-out infinite;
        --aq-glow-animation: {{ glow_anim }} {{ (duration * 0.9) | round(2) }}s ease-in-out infinite;
        --aq-halo-animation: {{ halo_anim }} {{ (duration * 1.1) | round(2) }}s ease-in-out infinite;

        /* icon color follows AQ color */
        --icon-color: rgba({{ rgb }}, 1);

        /* neutral pill so theme color does not bleed */
        background-color: rgba(77,77,77,0.12) !important;
        box-shadow: none !important;
        border: 1px solid rgba(255,255,255,0.06);

        opacity: 1;
        position: relative;
        transform-origin: 50% 60%;
        animation: var(--shape-animation);
      }

      /* glow layers */
      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        inset: -8px;
        animation: var(--aq-glow-animation);
      }

      .shape::after {
        inset: -22px;
        animation: var(--aq-halo-animation);
        mix-blend-mode: screen;
      }

      /* ========== GOOD (green) ========== */
      @keyframes aq-good-breathe {
        0%   { transform: scale(0.98); }
        50%  { transform: scale(1.04); }
        100% { transform: scale(0.98); }
      }

      @keyframes aq-good-glow {
        0% {
          box-shadow:
            0 0 18px 0 rgba(var(--aq-rgb), 0.55),
            0 0 30px 4 rgba(var(--aq-rgb), 0.6);
        }
        50% {
          box-shadow:
            0 0 24px 4 rgba(var(--aq-rgb), 0.9),
            0 0 40px 10px rgba(var(--aq-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 18px 0 rgba(var(--aq-rgb), 0.55),
            0 0 30px 4 rgba(var(--aq-rgb), 0.6);
        }
      }

      @keyframes aq-good-halo {
        0% {
          box-shadow:
            0 0 80px 24px rgba(var(--aq-rgb), 0.35),
            0 18px 70px -12px rgba(180,255,210,0.3);
        }
        50% {
          box-shadow:
            0 0 120px 40px rgba(var(--aq-rgb), 0.45),
            0 26px 90px -10px rgba(200,255,220,0.45);
        }
        100% {
          box-shadow:
            0 0 80px 24px rgba(var(--aq-rgb), 0.35),
            0 18px 70px -12px rgba(180,255,210,0.3);
        }
      }

      /* ========== FAIR (light green) ========== */
      @keyframes aq-fair-wave {
        0%   { transform: translateX(0); }
        25%  { transform: translateX(-1px); }
        50%  { transform: translateX(1px) translateY(-1px); }
        75%  { transform: translateX(-1px); }
        100% { transform: translateX(0); }
      }

      @keyframes aq-fair-glow {
        0% {
          box-shadow:
            0 0 18px 0 rgba(var(--aq-rgb), 0.55),
            0 0 30px 4 rgba(var(--aq-rgb), 0.6);
        }
        50% {
          box-shadow:
            0 0 24px 3 rgba(var(--aq-rgb), 0.9),
            0 0 40px 9px rgba(var(--aq-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 18px 0 rgba(var(--aq-rgb), 0.55),
            0 0 30px 4 rgba(var(--aq-rgb), 0.6);
        }
      }

      @keyframes aq-fair-halo {
        0% {
          box-shadow:
            0 0 85px 26px rgba(var(--aq-rgb), 0.35),
            0 18px 75px -12px rgba(200,255,210,0.3);
        }
        50% {
          box-shadow:
            0 0 125px 42px rgba(var(--aq-rgb), 0.45),
            0 26px 95px -10px rgba(215,255,225,0.45);
        }
        100% {
          box-shadow:
            0 0 85px 26px rgba(var(--aq-rgb), 0.35),
            0 18px 75px -12px rgba(200,255,210,0.3);
        }
      }

      /* ========== MODERATE (yellow) ========== */
      @keyframes aq-moderate-wave {
        0%   { transform: translateX(0); }
        25%  { transform: translateX(-1px); }
        50%  { transform: translateX(1px) translateY(-1px); }
        75%  { transform: translateX(-1px); }
        100% { transform: translateX(0); }
      }

      @keyframes aq-moderate-glow {
        0% {
          box-shadow:
            0 0 20px 0 rgba(var(--aq-rgb), 0.6),
            0 0 32px 4 rgba(var(--aq-rgb), 0.7);
        }
        50% {
          box-shadow:
            0 0 26px 3 rgba(var(--aq-rgb), 0.95),
            0 0 44px 10px rgba(var(--aq-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 20px 0 rgba(var(--aq-rgb), 0.6),
            0 0 32px 4 rgba(var(--aq-rgb), 0.7);
        }
      }

      @keyframes aq-moderate-halo {
        0% {
          box-shadow:
            0 0 90px 28px rgba(var(--aq-rgb), 0.4),
            0 20px 80px -10px rgba(255,240,170,0.3);
        }
        50% {
          box-shadow:
            0 0 135px 44px rgba(var(--aq-rgb), 0.5),
            0 30px 105px -8px rgba(255,250,190,0.45);
        }
        100% {
          box-shadow:
            0 0 90px 28px rgba(var(--aq-rgb), 0.4),
            0 20px 80px -10px rgba(255,240,170,0.3);
        }
      }

      /* ========== POOR (orange) ========== */
      @keyframes aq-poor-pulse {
        0%   { transform: scale(0.99); }
        50%  { transform: scale(1.06); }
        100% { transform: scale(0.99); }
      }

      @keyframes aq-poor-glow {
        0% {
          box-shadow:
            0 0 22px 0 rgba(var(--aq-rgb), 0.65),
            0 0 34px 4 rgba(var(--aq-rgb), 0.75);
        }
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--aq-rgb), 1),
            0 0 50px 12px rgba(var(--aq-rgb), 0.9);
        }
        100% {
          box-shadow:
            0 0 22px 0 rgba(var(--aq-rgb), 0.65),
            0 0 34px 4 rgba(var(--aq-rgb), 0.75);
        }
      }

      @keyframes aq-poor-halo {
        0% {
          box-shadow:
            0 0 100px 34px rgba(var(--aq-rgb), 0.5),
            0 24px 90px -10px rgba(255,210,150,0.45);
        }
        50% {
          box-shadow:
            0 0 145px 50px rgba(var(--aq-rgb), 0.6),
            0 32px 115px -8px rgba(255,220,170,0.55);
        }
        100% {
          box-shadow:
            0 0 100px 34px rgba(var(--aq-rgb), 0.5),
            0 24px 90px -10px rgba(255,210,150,0.45);
        }
      }

      /* ========== VERY POOR (red) ========== */
      @keyframes aq-verypoor-throb {
        0%   { transform: scale(1); }
        40%  { transform: scale(1.07); }
        100% { transform: scale(1); }
      }

      @keyframes aq-verypoor-glow {
        0% {
          box-shadow:
            0 0 24px 0 rgba(var(--aq-rgb), 0.75),
            0 0 38px 6 rgba(var(--aq-rgb), 0.8);
        }
        50% {
          box-shadow:
            0 0 34px 4 rgba(var(--aq-rgb), 1),
            0 0 60px 14px rgba(var(--aq-rgb), 0.95);
        }
        100% {
          box-shadow:
            0 0 24px 0 rgba(var(--aq-rgb), 0.75),
            0 0 38px 6 rgba(var(--aq-rgb), 0.8);
        }
      }

      @keyframes aq-verypoor-halo {
        0% {
          box-shadow:
            0 0 120px 40px rgba(var(--aq-rgb), 0.55),
            0 30px 110px -10px rgba(150,60,60,0.55);
        }
        50% {
          box-shadow:
            0 0 170px 64px rgba(var(--aq-rgb), 0.7),
            0 40px 140px -8px rgba(180,80,80,0.7);
        }
        100% {
          box-shadow:
            0 0 120px 40px rgba(var(--aq-rgb), 0.55),
            0 30px 110px -10px rgba(150,60,60,0.55);
        }
      }

      /* ========== EXTREMELY POOR (dark maroon) ========== */
      @keyframes aq-extreme-smog {
        0%   { transform: scale(1); filter: blur(0); }
        35%  { transform: scale(1.1) translateY(-1px); filter: blur(0.6px); }
        100% { transform: scale(1); filter: blur(0); }
      }

      @keyframes aq-extreme-glow {
        0% {
          box-shadow:
            0 0 26px 0 rgba(var(--aq-rgb), 0.85),
            0 0 44px 8 rgba(var(--aq-rgb), 0.9);
        }
        50% {
          box-shadow:
            0 0 38px 6 rgba(var(--aq-rgb), 1),
            0 0 70px 18px rgba(var(--aq-rgb), 0.98);
        }
        100% {
          box-shadow:
            0 0 26px 0 rgba(var(--aq-rgb), 0.85),
            0 0 44px 8 rgba(var(--aq-rgb), 0.9);
        }
      }

      @keyframes aq-extreme-halo {
        0% {
          box-shadow:
            0 0 180px 60px rgba(var(--aq-rgb), 0.7),
            0 40px 150px -10px rgba(60,0,30,0.7);
        }
        50% {
          box-shadow:
            0 0 230px 90px rgba(var(--aq-rgb), 0.85),
            0 52px 180px -8px rgba(90,0,45,0.85);
        }
        100% {
          box-shadow:
            0 0 180px 60px rgba(var(--aq-rgb), 0.7),
            0 40px 150px -10px rgba(60,0,30,0.7);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 64px;
        --icon-color: rgba(var(--hum-rgb),1) !important;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 22px;
        padding-bottom: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
        
        /* FONT SIZE & SPACING SETTINGS */
        --card-primary-font-size: 1.5rem !important;
        
        /* Increases vertical space between primary and secondary */
        --card-primary-line-height: 1.3 !important;
      }

```
</details>

<details>
<summary><strong>51 - Air quality (US)</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.livingroom_air_quality
tap_action:
  action: more-info
icon: mdi:air-filter
name: Air quality (US)
grid_options:
  rows: 1.4
primary_info: state
secondary_info: name
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== CONFIG ========== #}
        {% set aqi = states('sensor.livingroom_air_quality') | float(0) %}

        {# DEFAULTS (overridden by ranges) #}
        {% set rgb = '40,190,100' %}
        {% set anim = 'aq-good-breathe' %}
        {% set glow_anim = 'aq-good-glow' %}
        {% set halo_anim = 'aq-good-halo' %}
        {% set duration = 3.2 %}

        {# STANDARD AQI RANGES
           0   - 50   -> Good (green)
           51  - 100  -> Moderate (yellow)
           101 - 150  -> Unhealthy for sensitive groups (orange)
           151 - 200  -> Unhealthy (red)
           201 - 300  -> Very unhealthy (purple)
           301+       -> Hazardous (dark maroon)
        #}

        {# RANGES / COLORS #}
        {# You can change aqi number below if needed #}

        {% if aqi <= 50 %}
          {# GOOD #}
          {% set rgb = '40,190,100' %}
          {% set anim = 'aq-good-breathe' %}
          {% set glow_anim = 'aq-good-glow' %}
          {% set halo_anim = 'aq-good-halo' %}
          {% set duration = 3.4 %}

        {% elif aqi <= 100 %}
          {# MODERATE #}
          {% set rgb = '255,215,70' %}
          {% set anim = 'aq-moderate-wave' %}
          {% set glow_anim = 'aq-moderate-glow' %}
          {% set halo_anim = 'aq-moderate-halo' %}
          {% set duration = 3.0 %}

        {% elif aqi <= 150 %}
          {# UNHEALTHY FOR SENSITIVE GROUPS #}
          {% set rgb = '255,170,60' %}
          {% set anim = 'aq-usg-pulse' %}
          {% set glow_anim = 'aq-usg-glow' %}
          {% set halo_anim = 'aq-usg-halo' %}
          {% set duration = 2.8 %}

        {% elif aqi <= 200 %}
          {# UNHEALTHY #}
          {% set rgb = '230,60,60' %}
          {% set anim = 'aq-unhealthy-throb' %}
          {% set glow_anim = 'aq-unhealthy-glow' %}
          {% set halo_anim = 'aq-unhealthy-halo' %}
          {% set duration = 2.4 %}

        {% elif aqi <= 300 %}
          {# VERY UNHEALTHY #}
          {% set rgb = '170,60,180' %}
          {% set anim = 'aq-veryunhealthy-smog' %}
          {% set glow_anim = 'aq-veryunhealthy-glow' %}
          {% set halo_anim = 'aq-veryunhealthy-halo' %}
          {% set duration = 2.2 %}

        {% else %}
          {# HAZARDOUS #}
          {% set rgb = '120,0,70' %}
          {% set anim = 'aq-hazard-smog' %}
          {% set glow_anim = 'aq-hazard-glow' %}
          {% set halo_anim = 'aq-hazard-halo' %}
          {% set duration = 2.0 %}
        {% endif %}

        --aq-rgb: {{ rgb }};
        --shape-animation: {{ anim }} {{ duration }}s ease-in-out infinite;
        --aq-glow-animation: {{ glow_anim }} {{ (duration * 0.9) | round(2) }}s ease-in-out infinite;
        --aq-halo-animation: {{ halo_anim }} {{ (duration * 1.1) | round(2) }}s ease-in-out infinite;

        /* icon color follows AQ color */
        --icon-color: rgba({{ rgb }}, 1);

        /* neutral pill so theme color does not bleed */
        background-color: rgba(77,77,77,0.12) !important;
        box-shadow: none !important;
        border: 1px solid rgba(255,255,255,0.06);

        opacity: 1;
        position: relative;
        transform-origin: 50% 60%;
        animation: var(--shape-animation);
      }

      /* glow layers */
      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        inset: -8px;
        animation: var(--aq-glow-animation);
      }

      .shape::after {
        inset: -22px;
        animation: var(--aq-halo-animation);
        mix-blend-mode: screen;
      }

      /* ========== GOOD (green) ========== */
      @keyframes aq-good-breathe {
        0%   { transform: scale(0.98); }
        50%  { transform: scale(1.04); }
        100% { transform: scale(0.98); }
      }

      @keyframes aq-good-glow {
        0% {
          box-shadow:
            0 0 18px 0 rgba(var(--aq-rgb), 0.55),
            0 0 30px 4 rgba(var(--aq-rgb), 0.6);
        }
        50% {
          box-shadow:
            0 0 24px 4 rgba(var(--aq-rgb), 0.9),
            0 0 40px 10px rgba(var(--aq-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 18px 0 rgba(var(--aq-rgb), 0.55),
            0 0 30px 4 rgba(var(--aq-rgb), 0.6);
        }
      }

      @keyframes aq-good-halo {
        0% {
          box-shadow:
            0 0 80px 24px rgba(var(--aq-rgb), 0.35),
            0 18px 70px -12px rgba(180,255,210,0.3);
        }
        50% {
          box-shadow:
            0 0 120px 40px rgba(var(--aq-rgb), 0.45),
            0 26px 90px -10px rgba(200,255,220,0.45);
        }
        100% {
          box-shadow:
            0 0 80px 24px rgba(var(--aq-rgb), 0.35),
            0 18px 70px -12px rgba(180,255,210,0.3);
        }
      }

      /* ========== MODERATE (yellow) ========== */
      @keyframes aq-moderate-wave {
        0%   { transform: translateX(0); }
        25%  { transform: translateX(-1px); }
        50%  { transform: translateX(1px) translateY(-1px); }
        75%  { transform: translateX(-1px); }
        100% { transform: translateX(0); }
      }

      @keyframes aq-moderate-glow {
        0% {
          box-shadow:
            0 0 20px 0 rgba(var(--aq-rgb), 0.6),
            0 0 32px 4 rgba(var(--aq-rgb), 0.7);
        }
        50% {
          box-shadow:
            0 0 26px 3 rgba(var(--aq-rgb), 0.95),
            0 0 44px 10px rgba(var(--aq-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 20px 0 rgba(var(--aq-rgb), 0.6),
            0 0 32px 4 rgba(var(--aq-rgb), 0.7);
        }
      }

      @keyframes aq-moderate-halo {
        0% {
          box-shadow:
            0 0 90px 28px rgba(var(--aq-rgb), 0.4),
            0 20px 80px -10px rgba(255,240,170,0.3);
        }
        50% {
          box-shadow:
            0 0 135px 44px rgba(var(--aq-rgb), 0.5),
            0 30px 105px -8px rgba(255,250,190,0.45);
        }
        100% {
          box-shadow:
            0 0 90px 28px rgba(var(--aq-rgb), 0.4),
            0 20px 80px -10px rgba(255,240,170,0.3);
        }
      }

      /* ========== UNHEALTHY FOR SENSITIVE GROUPS (orange) ========== */
      @keyframes aq-usg-pulse {
        0%   { transform: scale(0.99); }
        50%  { transform: scale(1.06); }
        100% { transform: scale(0.99); }
      }

      @keyframes aq-usg-glow {
        0% {
          box-shadow:
            0 0 22px 0 rgba(var(--aq-rgb), 0.65),
            0 0 34px 4 rgba(var(--aq-rgb), 0.75);
        }
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--aq-rgb), 1),
            0 0 50px 12px rgba(var(--aq-rgb), 0.9);
        }
        100% {
          box-shadow:
            0 0 22px 0 rgba(var(--aq-rgb), 0.65),
            0 0 34px 4 rgba(var(--aq-rgb), 0.75);
        }
      }

      @keyframes aq-usg-halo {
        0% {
          box-shadow:
            0 0 100px 34px rgba(var(--aq-rgb), 0.5),
            0 24px 90px -10px rgba(255,210,150,0.45);
        }
        50% {
          box-shadow:
            0 0 145px 50px rgba(var(--aq-rgb), 0.6),
            0 32px 115px -8px rgba(255,220,170,0.55);
        }
        100% {
          box-shadow:
            0 0 100px 34px rgba(var(--aq-rgb), 0.5),
            0 24px 90px -10px rgba(255,210,150,0.45);
        }
      }

      /* ========== UNHEALTHY (red) ========== */
      @keyframes aq-unhealthy-throb {
        0%   { transform: scale(1); }
        40%  { transform: scale(1.07); }
        100% { transform: scale(1); }
      }

      @keyframes aq-unhealthy-glow {
        0% {
          box-shadow:
            0 0 24px 0 rgba(var(--aq-rgb), 0.75),
            0 0 38px 6 rgba(var(--aq-rgb), 0.8);
        }
        50% {
          box-shadow:
            0 0 34px 4 rgba(var(--aq-rgb), 1),
            0 0 60px 14px rgba(var(--aq-rgb), 0.95);
        }
        100% {
          box-shadow:
            0 0 24px 0 rgba(var(--aq-rgb), 0.75),
            0 0 38px 6 rgba(var(--aq-rgb), 0.8);
        }
      }

      @keyframes aq-unhealthy-halo {
        0% {
          box-shadow:
            0 0 120px 40px rgba(var(--aq-rgb), 0.55),
            0 30px 110px -10px rgba(150,60,60,0.55);
        }
        50% {
          box-shadow:
            0 0 170px 64px rgba(var(--aq-rgb), 0.7),
            0 40px 140px -8px rgba(180,80,80,0.7);
        }
        100% {
          box-shadow:
            0 0 120px 40px rgba(var(--aq-rgb), 0.55),
            0 30px 110px -10px rgba(150,60,60,0.55);
        }
      }

      /* ========== VERY UNHEALTHY (purple) ========== */
      @keyframes aq-veryunhealthy-smog {
        0%   { transform: scale(1); filter: blur(0); }
        40%  { transform: scale(1.08) translateY(-1px); filter: blur(0.4px); }
        100% { transform: scale(1); filter: blur(0); }
      }

      @keyframes aq-veryunhealthy-glow {
        0% {
          box-shadow:
            0 0 24px 0 rgba(var(--aq-rgb), 0.8),
            0 0 40px 6 rgba(var(--aq-rgb), 0.85);
        }
        50% {
          box-shadow:
            0 0 34px 4 rgba(var(--aq-rgb), 1),
            0 0 64px 14px rgba(var(--aq-rgb), 0.95);
        }
        100% {
          box-shadow:
            0 0 24px 0 rgba(var(--aq-rgb), 0.8),
            0 0 40px 6 rgba(var(--aq-rgb), 0.85);
        }
      }

      @keyframes aq-veryunhealthy-halo {
        0% {
          box-shadow:
            0 0 140px 46px rgba(var(--aq-rgb), 0.6),
            0 32px 120px -10px rgba(90,40,110,0.6);
        }
        50% {
          box-shadow:
            0 0 190px 72px rgba(var(--aq-rgb), 0.75),
            0 42px 150px -8px rgba(120,60,140,0.75);
        }
        100% {
          box-shadow:
            0 0 140px 46px rgba(var(--aq-rgb), 0.6),
            0 32px 120px -10px rgba(90,40,110,0.6);
        }
      }

      /* ========== HAZARDOUS (dark maroon) ========== */
      @keyframes aq-hazard-smog {
        0%   { transform: scale(1); filter: blur(0); }
        35%  { transform: scale(1.1) translateY(-1px); filter: blur(0.6px); }
        100% { transform: scale(1); filter: blur(0); }
      }

      @keyframes aq-hazard-glow {
        0% {
          box-shadow:
            0 0 26px 0 rgba(var(--aq-rgb), 0.85),
            0 0 44px 8 rgba(var(--aq-rgb), 0.9);
        }
        50% {
          box-shadow:
            0 0 38px 6 rgba(var(--aq-rgb), 1),
            0 0 70px 18px rgba(var(--aq-rgb), 0.98);
        }
        100% {
          box-shadow:
            0 0 26px 0 rgba(var(--aq-rgb), 0.85),
            0 0 44px 8 rgba(var(--aq-rgb), 0.9);
        }
      }

      @keyframes aq-hazard-halo {
        0% {
          box-shadow:
            0 0 180px 60px rgba(var(--aq-rgb), 0.7),
            0 40px 150px -10px rgba(60,0,30,0.7);
        }
        50% {
          box-shadow:
            0 0 230px 90px rgba(var(--aq-rgb), 0.85),
            0 52px 180px -8px rgba(90,0,45,0.85);
        }
        100% {
          box-shadow:
            0 0 180px 60px rgba(var(--aq-rgb), 0.7),
            0 40px 150px -10px rgba(60,0,30,0.7);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 64px;
        --icon-color: rgba(var(--hum-rgb),1) !important;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 22px;
        padding-bottom: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
        
        /* FONT SIZE & SPACING SETTINGS */
        --card-primary-font-size: 1.5rem !important;
        
        /* Increases vertical space between primary and secondary */
        --card-primary-line-height: 1.3 !important;
      }

```
</details>

<details>
<summary><strong>52 - Living room light (lux)</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.livingroom_illuminance
tap_action:
  action: more-info
icon: mdi:brightness-5
name: Living room light (lux)
grid_options:
  rows: 1.4
primary_info: state
secondary_info: name
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== CONFIG ========== #}
        {% set lux = states('sensor.livingroom_illuminance') | float(0) %}

        {# ------------------------------------------- #}
        {# LIGHT LEVEL → COLOR + EFFECT PRESETS        #}
        {# ------------------------------------------- #}

        {# DEFAULTS (will be overridden by ranges) #}
        {% set rgb = '40,80,255' %}
        {% set anim = 'lux-dark-breathe' %}
        {% set glow_anim = 'lux-dark-glow' %}
        {% set halo_anim = 'lux-dark-halo' %}
        {% set duration = 4.0 %}
        {% set intensity = 0.5 %}

        {# YOUR RANGES / COLORS #####
           < 10      -> deep blue (very dark)
           10 - <50  -> purple (dim)
           50 - <200 -> soft yellow (normal)
           200 - <500 -> warm orange (bright)
           >= 500    -> near white (very bright)
        ########################## #}

        {# RANGES / COLORS #}
        {# You can change aqi number below if needed #}

        {% if lux < 10 %}
          {# DEEP BLUE - VERY DARK #}
          {% set rgb = '40,80,255' %}
          {% set anim = 'lux-dark-breathe' %}
          {% set glow_anim = 'lux-dark-glow' %}
          {% set halo_anim = 'lux-dark-halo' %}
          {% set duration = 4.4 %}
          {% set intensity = 0.4 %}

        {% elif lux < 50 %}
          {# PURPLE - DIM #}
          {% set rgb = '140,80,220' %}
          {% set anim = 'lux-dim-wave' %}
          {% set glow_anim = 'lux-dim-glow' %}
          {% set halo_anim = 'lux-dim-halo' %}
          {% set duration = 3.6 %}
          {% set intensity = 0.55 %}

        {% elif lux < 200 %}
          {# SOFT YELLOW - COMFY #}
          {% set rgb = '255,210,80' %}
          {% set anim = 'lux-comfy-breathe' %}
          {% set glow_anim = 'lux-comfy-glow' %}
          {% set halo_anim = 'lux-comfy-halo' %}
          {% set duration = 3.0 %}
          {% set intensity = 0.6 %}

        {% elif lux < 500 %}
          {# WARM ORANGE - BRIGHT #}
          {% set rgb = '255,160,60' %}
          {% set anim = 'lux-bright-pulse' %}
          {% set glow_anim = 'lux-bright-glow' %}
          {% set halo_anim = 'lux-bright-halo' %}
          {% set duration = 2.6 %}
          {% set intensity = 0.8 %}

        {% else %}
          {# NEAR WHITE - VERY BRIGHT #}
          {% set rgb = '255,250,230' %}
          {% set anim = 'lux-sun-shimmer' %}
          {% set glow_anim = 'lux-sun-glow' %}
          {% set halo_anim = 'lux-sun-halo' %}
          {% set duration = 2.0 %}
          {% set intensity = 1.0 %}
        {% endif %}

        {# Apply variables #}
        --lux-rgb: {{ rgb }};
        --lux-intensity: {{ intensity }};
        --shape-animation: {{ anim }} {{ duration }}s ease-in-out infinite;
        --lux-glow-animation: {{ glow_anim }} {{ (duration * 0.9) | round(2) }}s ease-in-out infinite;
        --lux-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

        opacity: 1;

        /* Icon color follows the light level */
        --icon-color: rgba({{ rgb }}, 1);

        /* Neutral base for the shape */
        background-color: rgba(77, 77, 77, 0.1) !important;
        box-shadow: none !important;
        border: 1px solid rgba(255, 255, 255, 0.06);

        position: relative;
        transform-origin: 50% 60%;
        animation: var(--shape-animation);
      }

      /* Glow layers */
      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        inset: -8px;
        animation: var(--lux-glow-animation);
      }

      .shape::after {
        inset: -22px;
        animation: var(--lux-halo-animation);
        mix-blend-mode: screen;
      }

      /* ========== DARK ========== */
      @keyframes lux-dark-breathe {
        0%   { transform: scale(0.96); }
        50%  { transform: scale(1.03); }
        100% { transform: scale(0.96); }
      }

      @keyframes lux-dark-glow {
        0% {
          box-shadow:
            0 0 20px 0 rgba(var(--lux-rgb), 0.6),
            0 0 34px 6 rgba(var(--lux-rgb), 0.55);
        }
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--lux-rgb), 0.95),
            0 0 50px 10px rgba(var(--lux-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 20px 0 rgba(var(--lux-rgb), 0.6),
            0 0 34px 6 rgba(var(--lux-rgb), 0.55);
        }
      }

      @keyframes lux-dark-halo {
        0% {
          box-shadow:
            0 0 80px 20px rgba(var(--lux-rgb), 0.35),
            0 -20px 80px -14px rgba(220, 240, 255, 0.55);
        }
        50% {
          box-shadow:
            0 0 130px 36px rgba(var(--lux-rgb), 0.5),
            0 -34px 100px -8px rgba(240, 250, 255, 0.8);
        }
        100% {
          box-shadow:
            0 0 80px 20px rgba(var(--lux-rgb), 0.35),
            0 -20px 80px -14px rgba(220, 240, 255, 0.55);
        }
      }

      /* ========== DIM ========== */
      @keyframes lux-dim-wave {
        0%   { transform: translateX(0); }
        25%  { transform: translateX(-1px); }
        50%  { transform: translateX(1px) translateY(-1px); }
        75%  { transform: translateX(-1px); }
        100% { transform: translateX(0); }
      }

      @keyframes lux-dim-glow {
        0% {
          box-shadow:
            0 0 22px 0 rgba(var(--lux-rgb), 0.6),
            0 0 34px 4 rgba(var(--lux-rgb), 0.7);
        }
        50% {
          box-shadow:
            0 0 28px 2 rgba(var(--lux-rgb), 0.95),
            0 0 48px 12px rgba(var(--lux-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 22px 0 rgba(var(--lux-rgb), 0.6),
            0 0 34px 4 rgba(var(--lux-rgb), 0.7);
        }
      }

      @keyframes lux-dim-halo {
        0% {
          box-shadow:
            0 0 90px 26px rgba(var(--lux-rgb), 0.35),
            0 18px 80px -12px rgba(0, 220, 255, 0.35);
        }
        50% {
          box-shadow:
            0 0 140px 42px rgba(var(--lux-rgb), 0.45),
            0 30px 110px -10px rgba(0, 255, 255, 0.5);
        }
        100% {
          box-shadow:
            0 0 90px 26px rgba(var(--lux-rgb), 0.35),
            0 18px 80px -12px rgba(0, 220, 255, 0.35);
        }
      }

      /* ========== COMFY ========== */
      @keyframes lux-comfy-breathe {
        0%   { transform: scale(0.98); }
        50%  { transform: scale(1.05); }
        100% { transform: scale(0.98); }
      }

      @keyframes lux-comfy-glow {
        50% {
          box-shadow:
            0 0 26px 4 rgba(var(--lux-rgb), 0.9),
            0 0 42px 10px rgba(var(--lux-rgb), 0.85);
        }
      }

      @keyframes lux-comfy-halo {
        50% {
          box-shadow:
            0 0 120px 40px rgba(var(--lux-rgb), 0.45),
            0 26px 80px -10px rgba(180, 255, 200, 0.5);
        }
      }

      /* ========== BRIGHT ========== */
      @keyframes lux-bright-pulse {
        0%   { transform: scale(1); }
        50%  { transform: scale(1.07); }
        100% { transform: scale(1); }
      }

      @keyframes lux-bright-glow {
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--lux-rgb), 0.95),
            0 0 54px 14px rgba(var(--lux-rgb), 0.9);
        }
      }

      @keyframes lux-bright-halo {
        50% {
          box-shadow:
            0 0 140px 48px rgba(var(--lux-rgb), 0.55),
            0 26px 100px -10px rgba(255, 210, 150, 0.5);
        }
      }

      /* ========== VERY BRIGHT / SUN ========== */
      @keyframes lux-sun-shimmer {
        0%   { transform: scale(1); filter: blur(0); }
        50%  { transform: scale(1.08); filter: blur(0.6px); }
        100% { transform: scale(1); filter: blur(0); }
      }

      @keyframes lux-sun-glow {
        50% {
          box-shadow:
            0 0 34px 6 rgba(var(--lux-rgb), 1),
            0 0 62px 14px rgba(var(--lux-rgb), 0.95);
        }
      }

      @keyframes lux-sun-halo {
        50% {
          box-shadow:
            0 0 160px 60px rgba(var(--lux-rgb), 0.6),
            0 34px 120px -12px rgba(255, 230, 180, 0.6);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 64px;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 22px;
        padding-bottom: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
        
        /* FONT SIZE & SPACING SETTINGS */
        --card-primary-font-size: 1.5rem !important;
        
        /* Increases vertical space between primary and secondary */
        --card-primary-line-height: 1.3 !important;
      }

```
</details>

<details>
<summary><strong>53 - Alarmo (Requires card-mode v3.4.6)</strong></summary>

```yaml
type: custom:alarmo-card
entity: alarm_control_panel.alarmo
keep_keypad_visible: true
card_mod:
  style: |
    {% set state = states(config.entity) %}

    {% if state == 'disarmed' %}
      {% set color = '0, 255, 100' %}  /* Green */
      {% set glow_anim = 'glow-breathe 4s infinite' %}
      
    {% elif state == 'triggered' %}
      {% set color = '255, 0, 0' %}    /* Red */
      {% set glow_anim = 'glow-strobe 0.5s infinite' %}

    /* ARMED HOME */
    {% elif state == 'armed_home' %}
      {% set color = '0, 191, 255' %}  /* Blue */
      {% set glow_anim = 'glow-pulse 3s infinite' %}
      
    /* ARMED AWAY */
    {% elif 'armed' in state %}
      {% set color = '244, 67, 54' %}   /* Red */
      {% set glow_anim = 'glow-pulse 3s infinite' %}

    /* pending */
    {% elif state == 'pending' %}
      {% set color = '255, 152, 0' %}  /* Orange */
      {% set glow_anim = 'glow-pulse 1s infinite' %}

    /* loading and other */
    {% else %}
      {% set color = '158, 158, 158' %}  /* Grey */
      {% set glow_anim = 'none' %}
    {% endif %}

    /* --- THE CARD Inner Glow --- */
    ha-card {
      background: #1c1c1c !important;

      ## optional
      ## border: 1px solid rgba({{ color }}, 0.5) !important;
      border-radius: 25px !important;
      color: white !important;
      
      /* The Inner Glow Logic */
      box-shadow: inset 0 0 20px rgba({{ color }}, 0.2);
      animation: {{ glow_anim }};
      transition: all 1s ease;
    }

    /* --- ANIMATIONS (Card Glow Only) --- */

    @keyframes glow-breathe {
      0%   { box-shadow: inset 0 0 10px rgba({{ color }}, 0.1); }
      50%  { box-shadow: inset 0 0 60px rgba({{ color }}, 0.4); border-color: rgba({{ color }}, 0.8); }
      100% { box-shadow: inset 0 0 10px rgba({{ color }}, 0.1); }
    }

    @keyframes glow-pulse {
      0%   { box-shadow: inset 0 0 20px rgba({{ color }}, 0.2); }
      50%  { box-shadow: inset 0 0 50px rgba({{ color }}, 0.6); }
      100% { box-shadow: inset 0 0 20px rgba({{ color }}, 0.2); }
    }

    @keyframes glow-strobe {
      0%   { box-shadow: inset 0 0 10px rgba({{ color }}, 0.1); }
      50%  { box-shadow: inset 0 0 100px rgba({{ color }}, 0.9); background: rgba({{ color }}, 0.1); }
      100% { box-shadow: inset 0 0 10px rgba({{ color }}, 0.1); }
    }

```
</details>

<details>
<summary><strong>54 - Smart Plug</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: switch.plug_6_local
tap_action:
  action: toggle
icon: mdi:power-socket-eu
icon_color: green
hold_action:
  action: more-info
double_tap_action:
  action: none
name: Smart Plug
grid_options:
  rows: 1.4
card_mod:
  style:
    .: |
      ha-card {
        /* ================= USER SETTINGS ================= */
        {% set power_entity = 'sensor.plug_power' %}
        {% set max_w = 50 %} 
        /* ================================================= */

        /* --- LOGIC --- */
        {% set current_w = states(power_entity) | float(0) %}
        
        /* ACTIVE determines if animations/glows are ON (depends only on power) */
        {% set active = current_w > 0 %}
        
        /* Calculate Load Percentage */
        {% set width_pct = (current_w / max_w * 100) | round(2) %}
        {% if width_pct > 100 %}{% set width_pct = 100 %}{% endif %}
        
        /* --- PASS VARIABLES TO CSS --- */
        /* Define the color we want the effects to use (from config) */
        --active-color: var(--rgb-{{ config.icon_color }});
        
        --bar-width: {{ width_pct }}%;
        --bar-opacity: {{ 1 if active else 0 }};
        
        /* Text color: If power > 0, show colored text. Else dim. */
        --text-color: {{ 'rgba(var(--active-color), 1)' if active else 'rgba(255,255,255,0.5)' }};
        
        /* PASS ANIMATION VARIABLES DOWN TO SHADOW DOM */
        --shape-animation: {{ 'ultra-plug-on 3s ease-in-out infinite' if active else 'none' }};
        --plug-glow-animation: {{ 'ultra-plug-glow 3s ease-in-out infinite' if active else 'none' }};
        --plug-arcs-animation: {{ 'ultra-plug-arcs 3s linear infinite' if active else 'none' }};
        --effect-opacity: {{ 1 if active else 0 }};
        
        /* --- CARD STYLING --- */
        {% if active %}
          background-color: #1c1c1c !important;
          border: none !important;
          background-image: 
            radial-gradient(circle at 24px 24px, rgba(var(--active-color), 0.35) 0%, rgba(var(--active-color), 0.1) 40%, transparent 80%),
            linear-gradient(to right, rgba(255,255,255,0.1), rgba(255,255,255,0.1)) !important;
          background-size: 100% 100%, 100% 6px !important;
          background-position: top left, bottom left !important;
          background-repeat: no-repeat !important;
        {% else %}
          /* When Power is 0: Clean slate */
          background-image: none !important;
          box-shadow: none !important;
        {% endif %}

        border-radius: 12px;
        position: relative;
        overflow: hidden;
        transition: all 0.5s ease;
      }

      /* --- WATTAGE BADGE (Top Right) --- */
      ha-card::before {
        content: '{{ current_w | round(1) }} W';
        position: absolute;
        top: 12px;
        right: 12px;
        font-size: 11px;
        font-weight: 700;
        letter-spacing: 0.5px;
        color: var(--text-color);
        
        /* Only show badge background if active */
        background: {{ 'rgba(0, 0, 0, 0.2)' if active else 'transparent' }};
        border: {{ '1px solid rgba(255, 255, 255, 0.1)' if active else 'none' }};
        
        padding: 4px 8px;
        border-radius: 6px;
        backdrop-filter: blur(2px);
        transition: all 0.5s ease;
        z-index: 2;
      }

      /* --- ACTIVE PROGRESS BAR (BEAM) --- */
      ha-card::after {
        content: '';
        position: absolute;
        bottom: 0; left: 0;
        height: 6px;
        width: var(--bar-width);
        
        background: linear-gradient(90deg, 
          rgba(var(--active-color), 0.4) 0%, 
          rgba(var(--active-color), 1) 100%
        );
        
        box-shadow: 0 -2px 15px rgba(var(--active-color), 0.9);
        opacity: var(--bar-opacity);
        transition: width 0.5s ease-out, opacity 0.5s ease;
        animation: current-flow 1.5s infinite linear;
      }

      @keyframes current-flow {
        0% { filter: brightness(1); opacity: 0.8; }
        50% { filter: brightness(1.5); opacity: 1; }
        100% { filter: brightness(1); opacity: 0.8; }
      }

      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -20px 0 10px -20px !important;
        padding-right: 15px;
        padding-bottom: 15px;
      }
    mushroom-shape-icon$: >
      .shape {
        /* Receive animation variables from Main Card logic */
        animation: var(--shape-animation) !important;
        overflow: visible !important;
        position: relative;
      }


      /* Create the Pseudo-Elements for Glow and Arcs */

      .shape::before,

      .shape::after {
        content: '';
        position: absolute;
        inset: -4px;
        border-radius: inherit;
        pointer-events: none;
        opacity: var(--effect-opacity); 
      }


      /* Glow Layer */

      .shape::before {
        animation: var(--plug-glow-animation);
      }


      /* Electric Arcs Layer */

      .shape::after {
        animation: var(--plug-arcs-animation);
      }


      /* --- ANIMATION KEYFRAMES --- */

      /* Note: We use var(--active-color) so the glow stays green even if icon
      is gray */


      @keyframes ultra-plug-on {
        0%   { transform: scale(1); }
        25%  { transform: scale(1.05) translateY(-1px); }
        50%  { transform: scale(1.08) translateY(-2px); }
        75%  { transform: scale(1.04) translateY(-1px); }
        100% { transform: scale(1); }
      }


      @keyframes ultra-plug-glow {
        0% {
          box-shadow:
            0 0 10px 3px rgba(var(--active-color), 0.6),
            0 0 20px 8px rgba(var(--active-color), 0.3);
        }
        50% {
          box-shadow:
            0 0 18px 6px rgba(var(--active-color), 0.9),
            0 0 32px 12px rgba(var(--active-color), 0.4);
        }
        100% {
          box-shadow:
            0 0 10px 3px rgba(var(--active-color), 0.6),
            0 0 20px 8px rgba(var(--active-color), 0.3);
        }
      }


      @keyframes ultra-plug-arcs {
        0% {
          box-shadow:
            -10px -6px 0 -4px rgba(var(--active-color), 0.0),
            12px 4px 0 -4px rgba(var(--active-color), 0.0);
        }
        25% {
          box-shadow:
            -10px -6px 0 -4px rgba(var(--active-color), 0.7),
            12px 4px 0 -4px rgba(var(--active-color), 0.4);
        }
        50% {
          box-shadow:
            -6px 2px 0 -4px rgba(var(--active-color), 0.3),
            10px -8px 0 -4px rgba(var(--active-color), 0.7);
        }
        75% {
          box-shadow:
            -12px 4px 0 -4px rgba(var(--active-color), 0.5),
            8px 0 0 -4px rgba(var(--active-color), 0.2);
        }
        100% {
          box-shadow:
            -10px -6px 0 -4px rgba(var(--active-color), 0.0),
            12px 4px 0 -4px rgba(var(--active-color), 0.0);
        }
      }

```
</details>


<details>
<summary><strong>55 - Mushroom Alarm</strong></summary>

```yaml
type: custom:mushroom-alarm-control-panel-card
entity: alarm_control_panel.home_alarm
states:
  - armed_home
  - armed_away
layout: vertical
fill_container: true
primary_info: state
secondary_info: none
tap_action:
  action: none
hold_action:
  action: none
double_tap_action:
  action: none
card_mod:
  style:
    mushroom-shape-icon$: >
      .shape {
        /* --- LOGIC BLOCK --- */
        {% set status = states(config.entity) %}
        
        {% if status == 'disarmed' %}
          /* --- DISARMED --- */
          --main-color: var(--rgb-green);
          /* Shape: Floating effect */
          --bg-anim: shield-float 3s ease-in-out infinite;
          /* Inner: Light sheen scan */
          --inner-style: linear-gradient(to bottom, transparent, rgba(255,255,255,0.4), transparent);
          --inner-anim: sheen-scan 3s ease-in-out infinite;
          /* Outer: None */
          --outer-display: none;
          /* ICON: Slow, calm breathing */
          --icon-anim: breathe-slow 3s ease-in-out infinite;

        {% elif status == 'triggered' %}
          /* --- TRIGGERED --- */
          --main-color: var(--rgb-deep-orange);
          /* Shape: Strobe */
          --bg-anim: panic-strobe 0.5s steps(2) infinite;
          /* Inner: None */
          --inner-style: none;
          --inner-anim: none;
          /* Outer: Shockwave */
          --outer-display: block;
          --outer-anim: shockwave 0.5s linear infinite;
          /* ICON: Violent shake */
          --icon-anim: violent-shake 0.1s linear infinite;

        {% elif 'armed' in status %}
          /* --- ARMED --- */
          --main-color: var(--rgb-red);
          /* Shape: Static */
          --bg-anim: none;
          /* Inner: Radar sweep gradient */
          --inner-style: conic-gradient(from 0deg, transparent 0%, rgba(var(--main-color), 0.6) 20%, transparent 40%);
          --inner-anim: radar-spin 2s linear infinite;
          /* Outer: Sonar expansion */
          --outer-display: block;
          --outer-anim: sonar-expand 2s ease-out infinite;
          /* ICON: Alert pulse */
          --icon-anim: breathe-fast 2s ease-in-out infinite;

        {% elif status == 'pending' %}
          /* --- PENDING --- */
          --main-color: var(--rgb-orange);
          /* Shape: Breathing */
          --bg-anim: arming-breathe 1s ease-in-out infinite;
          /* Inner/Outer: None */
          --inner-style: none;
          --inner-anim: none;
          --outer-display: none;
          /* ICON: Medium pulse */
          --icon-anim: breathe-medium 2s ease-in-out infinite;

        {% else %}
          /* UNKNOWN */
          --main-color: var(--rgb-grey);
          --bg-anim: none; --inner-style: none; --inner-anim: none; --outer-display: none; --icon-anim: none;
        {% endif %}

        /* --- SHAPE CONTAINER STYLING --- */
        background-color: rgba(var(--main-color), 0.15) !important;
        --icon-color: var(--main-color) !important;
        color: rgb(var(--main-color)) !important;
        
        box-shadow: 0 0 25px rgba(var(--main-color), 0.3), inset 0 0 10px rgba(var(--main-color), 0.1);
        border: 1px solid rgba(var(--main-color), 0.3);
        
        border-radius: 50% !important;
        position: relative;
        overflow: visible !important;
        transition: all 0.5s ease;
        animation: var(--bg-anim);
      }


      /* INNER EFFECT (Sheen or Radar Sweep) */

      .shape::before {
        content: ''; position: absolute; inset: 0; border-radius: 50%;
        background: var(--inner-style); background-size: 100% 200%;
        animation: var(--inner-anim); z-index: 1;
      }


      /* OUTER EFFECT (Sonar Ring or Shockwave) */

      .shape::after {
        content: ''; display: var(--outer-display); position: absolute; inset: -2px; border-radius: 50%;
        border: 2px solid rgba(var(--main-color), 0.6);
        animation: var(--outer-anim); z-index: -1;
      }


      /* ICON ANIMATION (Applied directly to the icon) */

      ha-icon {
        position: relative; z-index: 2;
        animation: var(--icon-anim); transform-origin: center;
      }


      /* --- SHAPE & ICON ANIMATIONS --- */

      @keyframes shield-float { 0%, 100% { transform: translateY(0); } 50% {
      transform: translateY(-3px); } }

      @keyframes sheen-scan { 0% { background-position: 0% 150%; opacity: 0; }
      20%, 80% { opacity: 1; } 100% { background-position: 0% -50%; opacity: 0;
      } }

      @keyframes radar-spin { 0% { transform: rotate(0deg); } 100% { transform:
      rotate(360deg); } }

      @keyframes sonar-expand { 0% { transform: scale(1); opacity: 0.8;
      border-width: 2px; } 100% { transform: scale(2.5); opacity: 0;
      border-width: 0px; } }

      @keyframes panic-strobe { 0% { background-color: rgba(var(--main-color),
      0.2); box-shadow: 0 0 10px rgba(var(--main-color), 1); } 100% {
      background-color: rgba(var(--main-color), 0.6); box-shadow: 0 0 50px
      rgba(var(--main-color), 1); } }

      @keyframes violent-shake { 0% { transform: translate(0, 0) rotate(0deg); }
      25% { transform: translate(-3px, 3px) rotate(-5deg); } 50% { transform:
      translate(3px, -3px) rotate(5deg); } 75% { transform: translate(-3px,
      -3px) rotate(-5deg); } 100% { transform: translate(0, 0) rotate(0deg); } }

      @keyframes shockwave { 0% { transform: scale(1); opacity: 1; } 100% {
      transform: scale(1.5); opacity: 0; } }

      @keyframes arming-breathe { 0%, 100% { box-shadow: 0 0 10px
      rgba(var(--main-color), 0.5); } 50% { box-shadow: 0 0 30px
      rgba(var(--main-color), 1); } }


      /* Icon Breathing Animations */

      @keyframes breathe-slow { 0%, 100% { transform: scale(1); opacity: 0.8; }
      50% { transform: scale(1.05); opacity: 1; } }

      @keyframes breathe-medium { 0%, 100% { transform: scale(1); } 50% {
      transform: scale(1.1); } }

      @keyframes breathe-fast { 0%, 100% { transform: scale(1); } 50% {
      transform: scale(1.15); } }
    mushroom-alarm-control-panel-buttons-control$: |
      mushroom-button {
        --bg-color: rgba(var(--rgb-primary-text-color), 0.05) !important;
        --button-color: rgb(var(--rgb-primary-text-color)) !important;
        transition: all 0.2s ease;
      }
      mushroom-button:active {
        background-color: rgba(var(--rgb-primary-color), 0.2) !important;
      }
    .: |
      ha-card {
        /* --- LOGIC FOR CARD GLOW --- */
        {% set status = states(config.entity) %}
        
        {% if status == 'disarmed' %}
          /* DISARMED: Green Glow */
          --card-glow-color: var(--rgb-green);
          --card-anim-speed: 2s; /* Slow & Calm */
          
        {% elif status == 'triggered' %}
          /* TRIGGERED: Deep Orange/Red Strobe */
          --card-glow-color: var(--rgb-deep-orange);
          --card-anim-speed: 0.5s;
          
        {% elif status == 'pending' %}
          /* PENDING: Orange */
          --card-glow-color: var(--rgb-orange);
          --card-anim-speed: 2s;
          
        {% else %}
          /* ARMED (Any mode): Red Glow */
          --card-glow-color: var(--rgb-red);
          --card-anim-speed: 2s;
        {% endif %}
        
        --card-fill-anim: card-fill-pulse var(--card-anim-speed) ease-in-out infinite alternate;

        /* Base Card Styling */
        border: 1px solid rgba(255, 255, 255, 0.1);
        background: linear-gradient(145deg, rgba(30,30,30,0.9) 0%, rgba(20,20,20,1) 100%);
        box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
        position: relative;
        overflow: hidden; /* Important to contain the glow */
      }

      /* THE CARD-FILLING GLOW LAYER */
      ha-card::before {
        content: '';
        position: absolute;
        inset: 0;
        /* A large radial gradient that expands to fill the card */
        background: radial-gradient(circle at center, rgba(var(--card-glow-color), 0.4) 0%, transparent 70%);
        opacity: 0;
        pointer-events: none;
        mix-blend-mode: screen;
        animation: var(--card-fill-anim);
        z-index: 0; /* Behind content but in front of background */
      }

      /* Animation for the card glow */
      @keyframes card-fill-pulse {
        0% { opacity: 0.1; transform: scale(0.8); }
        100% { opacity: 0.6; transform: scale(1.5); }
      }

      /* Center the main icon */
      mushroom-shape-icon {
        --icon-size: 80px !important;
        display: flex; justify-content: center; align-items: center;
        margin: 20px 0 30px 0 !important;
        position: relative; z-index: 1; /* Keep icon above the card glow */
      }

```
</details>

<details>
<summary><strong>56 - Pollen grass (kleenex)</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.kleenex_pollen_radar_home_grass_level
tap_action:
  action: more-info
name: Grass
grid_options:
  rows: 1.4
icon: mdi:grass
primary_info: state
secondary_info: name
icon_color: light-grey
card_mod:
  style: |
    ha-card {
      /* ===== LOGIC & SETTINGS ===== */
      {% set state = states(config.entity) %}
      /* 1. Get the Grass Sensor Data */
      {% set grass = states('sensor.kleenex_pollen_radar_home_grass') %}
      
      /* 2. Define Colors based on state */
      {% if state in ['high', 'very-high', 'red'] %}
        {% set c1 = '255, 65, 108' %}  /* Red RGB */
        {% set c2 = '255, 75, 43' %}   /* Orange RGB */
        {% set speed = '4s' %}
      {% elif state in ['moderate', 'medium', 'orange'] %}
        {% set c1 = '247, 151, 30' %}  /* Orange RGB */
        {% set c2 = '255, 210, 0' %}   /* Yellow RGB */
        {% set speed = '7s' %}
      {% else %}
        {% set c1 = '0, 242, 96' %}    /* Green RGB */
        {% set c2 = '5, 117, 230' %}   /* Blue RGB */
        {% set speed = '12s' %}
      {% endif %}

      /* 3. Pass variables to CSS */
      --aura-color-1: rgba({{ c1 }}, 0.6);
      --aura-color-2: rgba({{ c2 }}, 0.6);
      --speed: {{ speed }};
      
      /* 4. Card Body Styling */
      background: #101010 !important;
      border-radius: 25px;
      border: 1px solid rgba(255,255,255,0.08);
      position: relative;
      overflow: hidden;
      box-shadow: inset 0 0 20px rgba(0,0,0,0.5);
    }

    ha-card::before {
      content: "";
      position: absolute;
      top: -50%; left: -50%;
      width: 200%; height: 200%;
      z-index: 0;
      
      /* Two radial gradients in one element */
      background-image: 
        radial-gradient(circle at 50% 50%, var(--aura-color-1) 0%, transparent 50%),
        radial-gradient(circle at 80% 80%, var(--aura-color-2) 0%, transparent 50%);
      
      filter: blur(60px);
      opacity: 0.8;
      animation: rotate-aura var(--speed) linear infinite;
    }

    ha-card::after {
      /* INJECT THE DATA HERE */
      content: '{{ grass }}';
      
      position: absolute;
      top: 50%; 
      right: 16px;
      transform: translateY(-50%);
      z-index: 10;
      
      /* Badge Styling (Like the battery example) */
      color: white;
      font-weight: 700;
      font-size: 14px;
      background: rgba(0, 0, 0, 0.4);
      border: 1px solid rgba(255, 255, 255, 0.15);
      backdrop-filter: blur(4px);
      padding: 4px 10px;
      border-radius: 12px;
      text-shadow: 0 1px 2px black;
    }

    /* --- GLASS SURFACE OVERLAY --- */
    mushroom-shape-icon {
       --icon-size: 68px;
       --icon-color: rgba(var(--voc-rgb),1) !important;
      display: flex;
      margin: -18px 0 10px -15px !important;
      padding-right: 22px;
      padding-bottom: 10px;
    }
    ha-card {
      clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));

      --card-primary-font-size: 1.2rem !important;
      --card-primary-line-height: 1.3 !important;
    }

    /* Typography */
    .mushroom-state-info span.primary {
      color: white !important;
      font-weight: 600 !important;
      font-size: 16px !important;
      text-shadow: 0 2px 4px rgba(0,0,0,0.5);
    }
    .mushroom-state-info span.secondary {
      color: rgba(255,255,255,0.8) !important;
    }

    /* Icon Styling */
    mushroom-shape-icon {
      --icon-size: 60px;
      --icon-color: white !important;
    }
    ha-state-icon {
      color: white !important;
    }

    /* Animation */
    @keyframes rotate-aura {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

```
</details>

<details>
<summary><strong>57 - Pollen trees (kleenex)</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.kleenex_pollen_radar_home_trees_level
tap_action:
  action: more-info
name: Trees
grid_options:
  rows: 1.4
icon: mdi:forest
primary_info: state
secondary_info: name
icon_color: light-grey
card_mod:
  style: |
    ha-card {
      /* ===== LOGIC & SETTINGS ===== */
      {% set state = states(config.entity) %}
      /* 1. Get the Grass Sensor Data */
      {% set grass = states('sensor.kleenex_pollen_radar_home_trees') %}
      
      /* 2. Define Colors based on state */
      {% if state in ['high', 'very-high', 'red'] %}
        {% set c1 = '255, 65, 108' %}  /* Red RGB */
        {% set c2 = '255, 75, 43' %}   /* Orange RGB */
        {% set speed = '4s' %}
      {% elif state in ['moderate', 'medium', 'orange'] %}
        {% set c1 = '247, 151, 30' %}  /* Orange RGB */
        {% set c2 = '255, 210, 0' %}   /* Yellow RGB */
        {% set speed = '7s' %}
      {% else %}
        {% set c1 = '0, 242, 96' %}    /* Green RGB */
        {% set c2 = '5, 117, 230' %}   /* Blue RGB */
        {% set speed = '12s' %}
      {% endif %}

      /* 3. Pass variables to CSS */
      --aura-color-1: rgba({{ c1 }}, 0.6);
      --aura-color-2: rgba({{ c2 }}, 0.6);
      --speed: {{ speed }};
      
      /* 4. Card Body Styling */
      background: #101010 !important;
      border-radius: 25px;
      border: 1px solid rgba(255,255,255,0.08);
      position: relative;
      overflow: hidden;
      box-shadow: inset 0 0 20px rgba(0,0,0,0.5);
    }

    ha-card::before {
      content: "";
      position: absolute;
      top: -50%; left: -50%;
      width: 200%; height: 200%;
      z-index: 0;
      
      /* Two radial gradients in one element */
      background-image: 
        radial-gradient(circle at 50% 50%, var(--aura-color-1) 0%, transparent 50%),
        radial-gradient(circle at 80% 80%, var(--aura-color-2) 0%, transparent 50%);
      
      filter: blur(60px);
      opacity: 0.8;
      animation: rotate-aura var(--speed) linear infinite;
    }

    ha-card::after {
      /* INJECT THE DATA HERE */
      content: '{{ grass }}';
      
      position: absolute;
      top: 50%; 
      right: 16px;
      transform: translateY(-50%);
      z-index: 10;
      
      /* Badge Styling (Like the battery example) */
      color: white;
      font-weight: 700;
      font-size: 14px;
      background: rgba(0, 0, 0, 0.4);
      border: 1px solid rgba(255, 255, 255, 0.15);
      backdrop-filter: blur(4px);
      padding: 4px 10px;
      border-radius: 12px;
      text-shadow: 0 1px 2px black;
    }

    /* --- GLASS SURFACE OVERLAY --- */
    mushroom-shape-icon {
       --icon-size: 68px;
       --icon-color: rgba(var(--voc-rgb),1) !important;
      display: flex;
      margin: -18px 0 10px -15px !important;
      padding-right: 22px;
      padding-bottom: 10px;
    }
    ha-card {
      clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));

      --card-primary-font-size: 1.2rem !important;
      --card-primary-line-height: 1.3 !important;
    }

    /* Typography */
    .mushroom-state-info span.primary {
      color: white !important;
      font-weight: 600 !important;
      font-size: 16px !important;
      text-shadow: 0 2px 4px rgba(0,0,0,0.5);
    }
    .mushroom-state-info span.secondary {
      color: rgba(255,255,255,0.8) !important;
    }

    /* Icon Styling */
    mushroom-shape-icon {
      --icon-size: 60px;
      --icon-color: white !important;
    }
    ha-state-icon {
      color: white !important;
    }

    /* Animation */
    @keyframes rotate-aura {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

```
</details>

<details>
<summary><strong>58 - Pollen weeds (kleenex)</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.kleenex_pollen_radar_home_weeds_level
tap_action:
  action: more-info
name: Weeds
grid_options:
  rows: 1.4
icon: mdi:cannabis
primary_info: state
secondary_info: name
icon_color: light-grey
card_mod:
  style: |
    ha-card {
      /* ===== LOGIC & SETTINGS ===== */
      {% set state = states(config.entity) %}
      /* 1. Get the Grass Sensor Data */
      {% set grass = states('sensor.kleenex_pollen_radar_home_weeds') %}
      
      /* 2. Define Colors based on state */
      {% if state in ['high', 'very-high', 'red'] %}
        {% set c1 = '255, 65, 108' %}  /* Red RGB */
        {% set c2 = '255, 75, 43' %}   /* Orange RGB */
        {% set speed = '4s' %}
      {% elif state in ['moderate', 'medium', 'orange'] %}
        {% set c1 = '247, 151, 30' %}  /* Orange RGB */
        {% set c2 = '255, 210, 0' %}   /* Yellow RGB */
        {% set speed = '7s' %}
      {% else %}
        {% set c1 = '0, 242, 96' %}    /* Green RGB */
        {% set c2 = '5, 117, 230' %}   /* Blue RGB */
        {% set speed = '12s' %}
      {% endif %}

      /* 3. Pass variables to CSS */
      --aura-color-1: rgba({{ c1 }}, 0.6);
      --aura-color-2: rgba({{ c2 }}, 0.6);
      --speed: {{ speed }};
      
      /* 4. Card Body Styling */
      background: #101010 !important;
      border-radius: 25px;
      border: 1px solid rgba(255,255,255,0.08);
      position: relative;
      overflow: hidden;
      box-shadow: inset 0 0 20px rgba(0,0,0,0.5);
    }

    ha-card::before {
      content: "";
      position: absolute;
      top: -50%; left: -50%;
      width: 200%; height: 200%;
      z-index: 0;
      
      /* Two radial gradients in one element */
      background-image: 
        radial-gradient(circle at 50% 50%, var(--aura-color-1) 0%, transparent 50%),
        radial-gradient(circle at 80% 80%, var(--aura-color-2) 0%, transparent 50%);
      
      filter: blur(60px);
      opacity: 0.8;
      animation: rotate-aura var(--speed) linear infinite;
    }

    ha-card::after {
      /* INJECT THE DATA HERE */
      content: '{{ grass }}';
      
      position: absolute;
      top: 50%; 
      right: 16px;
      transform: translateY(-50%);
      z-index: 10;
      
      /* Badge Styling (Like the battery example) */
      color: white;
      font-weight: 700;
      font-size: 14px;
      background: rgba(0, 0, 0, 0.4);
      border: 1px solid rgba(255, 255, 255, 0.15);
      backdrop-filter: blur(4px);
      padding: 4px 10px;
      border-radius: 12px;
      text-shadow: 0 1px 2px black;
    }

    /* --- GLASS SURFACE OVERLAY --- */
    mushroom-shape-icon {
       --icon-size: 68px;
       --icon-color: rgba(var(--voc-rgb),1) !important;
      display: flex;
      margin: -18px 0 10px -15px !important;
      padding-right: 22px;
      padding-bottom: 10px;
    }
    ha-card {
      clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));

      --card-primary-font-size: 1.2rem !important;
      --card-primary-line-height: 1.3 !important;
    }

    /* Typography */
    .mushroom-state-info span.primary {
      color: white !important;
      font-weight: 600 !important;
      font-size: 16px !important;
      text-shadow: 0 2px 4px rgba(0,0,0,0.5);
    }
    .mushroom-state-info span.secondary {
      color: rgba(255,255,255,0.8) !important;
    }

    /* Icon Styling */
    mushroom-shape-icon {
      --icon-size: 60px;
      --icon-color: white !important;
    }
    ha-state-icon {
      color: white !important;
    }

    /* Animation */
    @keyframes rotate-aura {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

```
</details>

<details>
<summary><strong>59 - water leak</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: binary_sensor.flood_kitchen_water_leak
tap_action:
  action: more-info
name: Leak sensor
grid_options:
  rows: 1.4
icon: mdi:pipe-leak
primary_info: name
secondary_info: none
icon_color: white
card_mod:
  style: |
    ha-card {
      /* ===== LOGIC & SETTINGS ===== */
      {% set level = 70 %}
      {% set rgb = '29, 130, 150' %}
      {% set sensor_on = is_state(config.entity, 'on') %}

      /* ===== VARIABLE ==== */
      --liq-color: rgb({{ rgb }});
      --liq-level: {{ level }}%;
      --wave-speed: 1.5s;

      /* ===== FONT SETTINGS ==== */
      --card-primary-font-size: 16px !important;
      --card-secondary-font-size: 12px !important;
      --card-primary-font-weight: bold !important;

      background-color: #1c1c1c !important;

      {% if sensor_on %}
      background-image:
        linear-gradient(
          90deg,
          rgba({{ rgb }}, 1) 0%,
          rgba({{ rgb }}, 1) {{ level -10 }}%,
          transparent {{ level }}%,
          transparent 100%
        ) !important;
      {% else %}
      background-image: none !important;
      {% endif %}

      border-radius: 12px;
      position: relative;
      overflow: hidden;
      z-index: 0;
      transition: all 0.5s ease;
    }

    /* ===== WET/DRY BADGE  ===== */
    ha-card::before {
      {% set label = 'Wet' if sensor_on else 'Dry' %}
      content: '{{ label }}';
      position: absolute;
      top: 30%;
      right: 10px;

      font-size: 1.1rem;
      font-weight: 700;

      color: {{ 'rgb(50,151,200)' if sensor_on else 'white' }};
      background: rgba(0, 0, 0, 0.3);
      border: 1px solid rgba(255, 255, 255, 0.1);
      padding: 2px 8px;
      border-radius: 6px;
      z-index: 3;
      pointer-events: none;
    }

    /* ===== LAYER: THE SPINNING WAVE ===== */
    ha-card::after {
      content: "";
      position: absolute;
      z-index: -1;

      /* Show wave only when sensor is ON and level is between 0 and 100 */
      display: {{
        'block'
        if sensor_on and level > 0 and level < 100
        else 'none'
      }};

      width: 120px;
      height: 120px;

      background: var(--liq-color);
      box-shadow: 0 0 25px rgba({{ rgb }}, 0.5);
      border-radius: 40%;

      left: calc(var(--liq-level) - 120px);
      top: calc(50% - 60px);

      animation: spin-wave var(--wave-speed) linear infinite;
      transition: left 0.5s cubic-bezier(0.25, 0.1, 0.25, 1);
    }

    /* ===== ENSURE CONTENT IS ON TOP ===== */
    .mushroom-state-item {
      z-index: 2;
      position: relative;
      text-shadow: 0 1px 3px rgba(0,0,0,0.8);
    }

    /* ===== ICON + SHAPE STATE COLORS ===== */
    mushroom-shape-icon {
      --icon-size: 68px;
      display: flex;
      margin: -18px 0 10px -18px !important;
      padding-right: 15px;
      z-index: 2;

      /* Shape blue tinted when OFF */
      {% if not sensor_on %}
        --shape-color: rgba({{ rgb }}, 0.25);
      {% endif %}
    }

    /* Icon color changes with state */
    ha-state-icon {
      color: {{
        'white'
        if sensor_on
        else 'rgb(50,151,200)'
      }} !important;

      filter: drop-shadow(0 2px 4px rgba(0,0,0,0.5));
    }

    /* ===== NIMATION ===== */
    @keyframes spin-wave {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

```
</details>

<details>
<summary><strong>60 - water leak</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: binary_sensor.flood_kitchen_water_leak
tap_action:
  action: more-info
name: Leak sensor
grid_options:
  rows: 1.4
icon: mdi:pipe-leak
icon_color: white
primary_info: name
secondary_info: none
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        /* --- LOGIC INJECTION --- */
        --liquid-level: var(--custom-level);
        --liquid-color: var(--custom-color);

        /* Container Setup */
        background: rgba(255, 255, 255, 0.05) !important;
        overflow: hidden !important;
        position: relative;
        box-shadow: var(--custom-icon-shadow) !important;
      }

      /* THE LIQUID (Wavy Fill) */
      .shape::before {
        content: '';
        position: absolute;
        left: -50%;
        width: 200%;
        height: 200%;

        /* 50% fill when ON, 0% when OFF */
        top: calc(100% - var(--liquid-level));

        background: var(--liquid-color);
        border-radius: 40%;

        /* Animate only when ON */
        animation: var(--custom-wave-anim);
        opacity: 0.85;
      }

      /* Ensure the MDI Icon sits on top of the liquid */
      ha-icon {
        position: relative;
        z-index: 2;
        mix-blend-mode: overlay;
        color: white !important;
      }

      /* --- ANIMATION --- */
      @keyframes liquid-wave {
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
      }
    .: |
      ha-card {
        /* ================= USER SETTINGS ================= */
        {% set rgb = '29, 130, 150' %}

        /* Font sizes you can change */
        {% set primary_font_size = 16 %}
        {% set secondary_font_size = 12 %}
        /* ================================================= */

        /* Apply Mushroom font vars */
        --card-primary-font-size: {{ primary_font_size }}px !important;
        --card-secondary-font-size: {{ secondary_font_size }}px !important;
        --card-primary-font-weight: 700 !important;

        /* --- LOGIC --- */
        {% set sensor_on = is_state(config.entity, 'on') %}
        {% set level = 50 if sensor_on else 0 %}

        /* --- PASS VARIABLES TO CSS --- */
        --custom-level: {{ level }}%;
        --custom-color: rgba({{ rgb }}, {{ 0.8 if sensor_on else 0 }});
        --custom-icon-shadow: {{ '0 0 12px rgba(' ~ rgb ~ ', 0.45)' if sensor_on else 'none' }};
        --custom-wave-anim: {{ 'liquid-wave 6s linear infinite' if sensor_on else 'none' }};

        /* --- CARD STYLING --- */
        background: #1c1c1c !important;
        border: none !important;
        border-radius: 12px;
        position: relative;
        overflow: hidden;
        transition: all 0.5s ease;

        /* Subtle ambient glow only when ON */
        {% if sensor_on %}
        background-image:
          radial-gradient(circle at 24px 24px, rgba({{ rgb }}, 0.15) 0%, transparent 60%) !important;
        {% else %}
        background-image: none !important;
        {% endif %}
      }

      /* Optional: if you ever enable primary_info later,
         this ensures the text respects the vars robustly */
      .primary {
        font-size: var(--card-primary-font-size) !important;
        font-weight: var(--card-primary-font-weight) !important;
      }
      .secondary {
        font-size: var(--card-secondary-font-size) !important;
      }

      /* --- WET/DRY BADGE (Right side) --- */
      ha-card::before {
        content: '{{ "Wet" if sensor_on else "Dry" }}';
        position: absolute;
        top: 30%;
        right: 10px;
        font-size: 1.1rem;
        font-weight: 700;

        color: {{ 'rgb(50,151,200)' if sensor_on else 'white' }};
        background: rgba(0, 0, 0, 0.3);
        border: 1px solid rgba(255, 255, 255, 0.1);
        padding: 2px 8px;
        border-radius: 6px;
        pointer-events: none;
      }
      /* Icon color changes with state */
      ha-state-icon {
        color: {{
          'white'
          if sensor_on
          else 'rgb(50,151,200)'
        }} !important;
        filter: drop-shadow(0 2px 4px rgba(0,0,0,0.5));
      }

      mushroom-shape-icon {
        --icon-size: 60px;
        display: flex;
        padding-right: 15px;
      }

```
</details>

<details>
<summary><strong>61 - CO2 PPM</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.livingroom_co2_ppm
tap_action:
  action: more-info
icon: mdi:molecule-co2
name: Living room CO2 (ppm)
grid_options:
  rows: 1.4
primary_info: state
secondary_info: name
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== CONFIG ========== #}
        {% set co2 = states('sensor.livingroom_co2_ppm') | float(0) %}

        {# ------------------------------------------- #}
        {# CO2 → COLOR + EFFECT PRESETS                #}
        {# ------------------------------------------- #}

        {# DEFAULTS (will be overridden by ranges) #}
        {% set rgb = '40,200,120' %}
        {% set anim = 'co2-fresh-breathe' %}
        {% set glow_anim = 'co2-fresh-glow' %}
        {% set halo_anim = 'co2-fresh-halo' %}
        {% set duration = 4.0 %}
        {% set intensity = 0.5 %}

        {# RANGES / COLORS #}
        {# You can change numbers below if needed #}

        {% if co2 < 600 %}
          {# FRESH GREEN #}
          {% set rgb = '40,200,120' %}
          {% set anim = 'co2-fresh-breathe' %}
          {% set glow_anim = 'co2-fresh-glow' %}
          {% set halo_anim = 'co2-fresh-halo' %}
          {% set duration = 4.4 %}
          {% set intensity = 0.45 %}

        {% elif co2 < 800 %}
          {# SOFT GREEN #}
          {% set rgb = '120,220,120' %}
          {% set anim = 'co2-good-wave' %}
          {% set glow_anim = 'co2-good-glow' %}
          {% set halo_anim = 'co2-good-halo' %}
          {% set duration = 3.6 %}
          {% set intensity = 0.55 %}

        {% elif co2 < 1000 %}
          {# YELLOW #}
          {% set rgb = '255,210,40' %}
          {% set anim = 'co2-ok-breathe' %}
          {% set glow_anim = 'co2-ok-glow' %}
          {% set halo_anim = 'co2-ok-halo' %}
          {% set duration = 3.0 %}
          {% set intensity = 0.65 %}

        {% elif co2 < 1400 %}
          {# ORANGE #}
          {% set rgb = '255,140,40' %}
          {% set anim = 'co2-high-pulse' %}
          {% set glow_anim = 'co2-high-glow' %}
          {% set halo_anim = 'co2-high-halo' %}
          {% set duration = 2.4 %}
          {% set intensity = 0.85 %}

        {% else %}
          {# RED #}
          {% set rgb = '255,50,50' %}
          {% set anim = 'co2-bad-shimmer' %}
          {% set glow_anim = 'co2-bad-glow' %}
          {% set halo_anim = 'co2-bad-halo' %}
          {% set duration = 2.0 %}
          {% set intensity = 1.0 %}
        {% endif %}

        {# Apply variables #}
        --co2-rgb: {{ rgb }};
        --co2-intensity: {{ intensity }};
        --shape-animation: {{ anim }} {{ duration }}s ease-in-out infinite;
        --co2-glow-animation: {{ glow_anim }} {{ (duration * 0.9) | round(2) }}s ease-in-out infinite;
        --co2-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

        opacity: 1;

        /* Icon color follows CO2 level */
        --icon-color: rgba({{ rgb }}, 1);

        /* Shape neutral base */
        background-color: rgba(77, 77, 77,0.1) !important;
        box-shadow: none !important;
        border: 1px solid rgba(255,255,255,0.06);

        position: relative;
        transform-origin: 50% 60%;
        animation: var(--shape-animation);
      }

      /* Glow layers */
      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        inset: -8px;
        animation: var(--co2-glow-animation);
      }

      .shape::after {
        inset: -22px;
        animation: var(--co2-halo-animation);
        mix-blend-mode: screen;
      }

      /* ========== FRESH ========== */
      @keyframes co2-fresh-breathe {
        0%   { transform: scale(0.96); }
        50%  { transform: scale(1.03); }
        100% { transform: scale(0.96); }
      }

      @keyframes co2-fresh-glow {
        0% {
          box-shadow:
            0 0 20px 0 rgba(var(--co2-rgb), 0.55),
            0 0 34px 6 rgba(var(--co2-rgb), 0.5);
        }
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--co2-rgb), 0.9),
            0 0 50px 10px rgba(var(--co2-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 20px 0 rgba(var(--co2-rgb), 0.55),
            0 0 34px 6 rgba(var(--co2-rgb), 0.5);
        }
      }

      @keyframes co2-fresh-halo {
        0% {
          box-shadow:
            0 0 80px 20px rgba(var(--co2-rgb), 0.28),
            0 -20px 80px -14px rgba(200, 255, 230, 0.45);
        }
        50% {
          box-shadow:
            0 0 130px 36px rgba(var(--co2-rgb), 0.42),
            0 -34px 100px -8px rgba(220, 255, 240, 0.65);
        }
        100% {
          box-shadow:
            0 0 80px 20px rgba(var(--co2-rgb), 0.28),
            0 -20px 80px -14px rgba(200, 255, 230, 0.45);
        }
      }

      /* ========== GOOD ========== */
      @keyframes co2-good-wave {
        0%   { transform: translateX(0); }
        25%  { transform: translateX(-1px); }
        50%  { transform: translateX(1px) translateY(-1px); }
        75%  { transform: translateX(-1px); }
        100% { transform: translateX(0); }
      }

      @keyframes co2-good-glow {
        0% {
          box-shadow:
            0 0 22px 0 rgba(var(--co2-rgb), 0.55),
            0 0 34px 4 rgba(var(--co2-rgb), 0.6);
        }
        50% {
          box-shadow:
            0 0 28px 2 rgba(var(--co2-rgb), 0.9),
            0 0 48px 12px rgba(var(--co2-rgb), 0.8);
        }
        100% {
          box-shadow:
            0 0 22px 0 rgba(var(--co2-rgb), 0.55),
            0 0 34px 4 rgba(var(--co2-rgb), 0.6);
        }
      }

      @keyframes co2-good-halo {
        0% {
          box-shadow:
            0 0 90px 26px rgba(var(--co2-rgb), 0.3),
            0 18px 80px -12px rgba(120, 255, 160, 0.3);
        }
        50% {
          box-shadow:
            0 0 140px 42px rgba(var(--co2-rgb), 0.4),
            0 30px 110px -10px rgba(140, 255, 180, 0.45);
        }
        100% {
          box-shadow:
            0 0 90px 26px rgba(var(--co2-rgb), 0.3),
            0 18px 80px -12px rgba(120, 255, 160, 0.3);
        }
      }

      /* ========== OK ========== */
      @keyframes co2-ok-breathe {
        0%   { transform: scale(0.98); }
        50%  { transform: scale(1.05); }
        100% { transform: scale(0.98); }
      }

      @keyframes co2-ok-glow {
        50% {
          box-shadow:
            0 0 26px 4 rgba(var(--co2-rgb), 0.85),
            0 0 42px 10px rgba(var(--co2-rgb), 0.8);
        }
      }

      @keyframes co2-ok-halo {
        50% {
          box-shadow:
            0 0 120px 40px rgba(var(--co2-rgb), 0.42),
            0 26px 80px -10px rgba(255, 245, 180, 0.5);
        }
      }

      /* ========== HIGH ========== */
      @keyframes co2-high-pulse {
        0%   { transform: scale(1); }
        50%  { transform: scale(1.07); }
        100% { transform: scale(1); }
      }

      @keyframes co2-high-glow {
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--co2-rgb), 0.95),
            0 0 54px 14px rgba(var(--co2-rgb), 0.9);
        }
      }

      @keyframes co2-high-halo {
        50% {
          box-shadow:
            0 0 140px 48px rgba(var(--co2-rgb), 0.52),
            0 26px 100px -10px rgba(255, 210, 150, 0.5);
        }
      }

      /* ========== BAD ========== */
      @keyframes co2-bad-shimmer {
        0%   { transform: scale(1); filter: blur(0); }
        50%  { transform: scale(1.08); filter: blur(0.6px); }
        100% { transform: scale(1); filter: blur(0); }
      }

      @keyframes co2-bad-glow {
        50% {
          box-shadow:
            0 0 34px 6 rgba(var(--co2-rgb), 1),
            0 0 62px 14px rgba(var(--co2-rgb), 0.95);
        }
      }

      @keyframes co2-bad-halo {
        50% {
          box-shadow:
            0 0 160px 60px rgba(var(--co2-rgb), 0.6),
            0 34px 120px -12px rgba(255, 140, 120, 0.6);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 64px;
        --icon-color: rgba(var(--co2-rgb),1) !important;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 22px;
        padding-bottom: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));

        /* FONT SIZE & SPACING SETTINGS */
        --card-primary-font-size: 1.5rem !important;

        /* Increases vertical space between primary and secondary */
        --card-primary-line-height: 1.3 !important;
      }

```
</details>

<details>
<summary><strong>62 - Air Quality VOC</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.livingroom_air_quality_voc
tap_action:
  action: more-info
icon: mdi:air-filter
name: Living room VOC
grid_options:
  rows: 1.4
primary_info: state
secondary_info: name
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== CONFIG ========== #}
        {% set voc = states('sensor.livingroom_air_quality_voc') | float(0) %}

        {# DEFAULTS (will be overridden by ranges) #}
        {% set rgb = '40,200,120' %}
        {% set anim = 'voc-clean-breathe' %}
        {% set glow_anim = 'voc-clean-glow' %}
        {% set halo_anim = 'voc-clean-halo' %}
        {% set duration = 4.0 %}
        {% set intensity = 0.5 %}

        {# RANGES / COLORS #}
        {# You can change numbers below if needed #}

        {% if voc < 100 %}
          {# GREEN #}
          {% set rgb = '40,200,120' %}
          {% set anim = 'voc-clean-breathe' %}
          {% set glow_anim = 'voc-clean-glow' %}
          {% set halo_anim = 'voc-clean-halo' %}
          {% set duration = 4.4 %}
          {% set intensity = 0.45 %}

        {% elif voc < 200 %}
          {# YELLOW-GREEN #}
          {% set rgb = '140,220,80' %}
          {% set anim = 'voc-good-wave' %}
          {% set glow_anim = 'voc-good-glow' %}
          {% set halo_anim = 'voc-good-halo' %}
          {% set duration = 3.6 %}
          {% set intensity = 0.55 %}

        {% elif voc < 300 %}
          {# YELLOW #}
          {% set rgb = '255,210,40' %}
          {% set anim = 'voc-fair-breathe' %}
          {% set glow_anim = 'voc-fair-glow' %}
          {% set halo_anim = 'voc-fair-halo' %}
          {% set duration = 3.0 %}
          {% set intensity = 0.7 %}

        {% elif voc < 400 %}
          {# ORANGE #}
          {% set rgb = '255,140,40' %}
          {% set anim = 'voc-poor-pulse' %}
          {% set glow_anim = 'voc-poor-glow' %}
          {% set halo_anim = 'voc-poor-halo' %}
          {% set duration = 2.4 %}
          {% set intensity = 0.9 %}

        {% else %}
          {# RED #}
          {% set rgb = '255,50,50' %}
          {% set anim = 'voc-bad-shimmer' %}
          {% set glow_anim = 'voc-bad-glow' %}
          {% set halo_anim = 'voc-bad-halo' %}
          {% set duration = 2.0 %}
          {% set intensity = 1.0 %}
        {% endif %}

        {# Apply variables #}
        --voc-rgb: {{ rgb }};
        --voc-intensity: {{ intensity }};
        --shape-animation: {{ anim }} {{ duration }}s ease-in-out infinite;
        --voc-glow-animation: {{ glow_anim }} {{ (duration * 0.9) | round(2) }}s ease-in-out infinite;
        --voc-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

        opacity: 1;

        /* Icon color follows VOC level */
        --icon-color: rgba({{ rgb }}, 1);

        /* Shape neutral base */
        background-color: rgba(77, 77, 77,0.1) !important;
        box-shadow: none !important;
        border: 1px solid rgba(255,255,255,0.06);

        position: relative;
        transform-origin: 50% 60%;
        animation: var(--shape-animation);
      }

      /* Glow layers */
      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        inset: -8px;
        animation: var(--voc-glow-animation);
      }

      .shape::after {
        inset: -22px;
        animation: var(--voc-halo-animation);
        mix-blend-mode: screen;
      }

      /* ========== CLEAN ========== */
      @keyframes voc-clean-breathe {
        0%   { transform: scale(0.96); }
        50%  { transform: scale(1.03); }
        100% { transform: scale(0.96); }
      }

      @keyframes voc-clean-glow {
        0% {
          box-shadow:
            0 0 20px 0 rgba(var(--voc-rgb), 0.55),
            0 0 34px 6 rgba(var(--voc-rgb), 0.5);
        }
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--voc-rgb), 0.9),
            0 0 50px 10px rgba(var(--voc-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 20px 0 rgba(var(--voc-rgb), 0.55),
            0 0 34px 6 rgba(var(--voc-rgb), 0.5);
        }
      }

      @keyframes voc-clean-halo {
        0% {
          box-shadow:
            0 0 80px 20px rgba(var(--voc-rgb), 0.28),
            0 -20px 80px -14px rgba(200, 255, 230, 0.45);
        }
        50% {
          box-shadow:
            0 0 130px 36px rgba(var(--voc-rgb), 0.42),
            0 -34px 100px -8px rgba(220, 255, 240, 0.65);
        }
        100% {
          box-shadow:
            0 0 80px 20px rgba(var(--voc-rgb), 0.28),
            0 -20px 80px -14px rgba(200, 255, 230, 0.45);
        }
      }

      /* ========== GOOD ========== */
      @keyframes voc-good-wave {
        0%   { transform: translateX(0); }
        25%  { transform: translateX(-1px); }
        50%  { transform: translateX(1px) translateY(-1px); }
        75%  { transform: translateX(-1px); }
        100% { transform: translateX(0); }
      }

      @keyframes voc-good-glow {
        0% {
          box-shadow:
            0 0 22px 0 rgba(var(--voc-rgb), 0.55),
            0 0 34px 4 rgba(var(--voc-rgb), 0.6);
        }
        50% {
          box-shadow:
            0 0 28px 2 rgba(var(--voc-rgb), 0.9),
            0 0 48px 12px rgba(var(--voc-rgb), 0.8);
        }
        100% {
          box-shadow:
            0 0 22px 0 rgba(var(--voc-rgb), 0.55),
            0 0 34px 4 rgba(var(--voc-rgb), 0.6);
        }
      }

      @keyframes voc-good-halo {
        0% {
          box-shadow:
            0 0 90px 26px rgba(var(--voc-rgb), 0.3),
            0 18px 80px -12px rgba(140, 255, 120, 0.25);
        }
        50% {
          box-shadow:
            0 0 140px 42px rgba(var(--voc-rgb), 0.4),
            0 30px 110px -10px rgba(160, 255, 140, 0.4);
        }
        100% {
          box-shadow:
            0 0 90px 26px rgba(var(--voc-rgb), 0.3),
            0 18px 80px -12px rgba(140, 255, 120, 0.25);
        }
      }

      /* ========== FAIR ========== */
      @keyframes voc-fair-breathe {
        0%   { transform: scale(0.98); }
        50%  { transform: scale(1.05); }
        100% { transform: scale(0.98); }
      }

      @keyframes voc-fair-glow {
        50% {
          box-shadow:
            0 0 26px 4 rgba(var(--voc-rgb), 0.85),
            0 0 42px 10px rgba(var(--voc-rgb), 0.8);
        }
      }

      @keyframes voc-fair-halo {
        50% {
          box-shadow:
            0 0 120px 40px rgba(var(--voc-rgb), 0.42),
            0 26px 80px -10px rgba(255, 245, 180, 0.5);
        }
      }

      /* ========== POOR ========== */
      @keyframes voc-poor-pulse {
        0%   { transform: scale(1); }
        50%  { transform: scale(1.07); }
        100% { transform: scale(1); }
      }

      @keyframes voc-poor-glow {
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--voc-rgb), 0.95),
            0 0 54px 14px rgba(var(--voc-rgb), 0.9);
        }
      }

      @keyframes voc-poor-halo {
        50% {
          box-shadow:
            0 0 140px 48px rgba(var(--voc-rgb), 0.52),
            0 26px 100px -10px rgba(255, 210, 150, 0.5);
        }
      }

      /* ========== BAD ========== */
      @keyframes voc-bad-shimmer {
        0%   { transform: scale(1); filter: blur(0); }
        50%  { transform: scale(1.08); filter: blur(0.6px); }
        100% { transform: scale(1); filter: blur(0); }
      }

      @keyframes voc-bad-glow {
        50% {
          box-shadow:
            0 0 34px 6 rgba(var(--voc-rgb), 1),
            0 0 62px 14px rgba(var(--voc-rgb), 0.95);
        }
      }

      @keyframes voc-bad-halo {
        50% {
          box-shadow:
            0 0 160px 60px rgba(var(--voc-rgb), 0.6),
            0 34px 120px -12px rgba(255, 140, 120, 0.6);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 64px;
        --icon-color: rgba(var(--voc-rgb),1) !important;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 22px;
        padding-bottom: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));

        --card-primary-font-size: 1.5rem !important;
        --card-primary-line-height: 1.3 !important;
      }

```
</details>

<details>
<summary><strong>63 - Pressure mbar</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.livingroom_pressure_mbar
tap_action:
  action: more-info
icon: mdi:gauge
name: Living room pressure (mbar)
grid_options:
  rows: 1.4
primary_info: state
secondary_info: name
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== CONFIG ========== #}
        {% set p = states('sensor.livingroom_pressure_mbar') | float(0) %}

        {# DEFAULTS #}
        {% set rgb = '120,220,120' %}
        {% set anim = 'pres-normal-breathe' %}
        {% set glow_anim = 'pres-normal-glow' %}
        {% set halo_anim = 'pres-normal-halo' %}
        {% set duration = 3.6 %}
        {% set intensity = 0.55 %}

        {# RANGES / COLORS #}
        {# You can change numbers below if needed #}

        {% if p < 990 %}
          {% set rgb = '0,140,255' %}
          {% set anim = 'pres-low-breathe' %}
          {% set glow_anim = 'pres-low-glow' %}
          {% set halo_anim = 'pres-low-halo' %}
          {% set duration = 4.4 %}
          {% set intensity = 0.45 %}

        {% elif p < 1005 %}
          {% set rgb = '60,190,200' %}
          {% set anim = 'pres-soft-wave' %}
          {% set glow_anim = 'pres-soft-glow' %}
          {% set halo_anim = 'pres-soft-halo' %}
          {% set duration = 3.6 %}
          {% set intensity = 0.55 %}

        {% elif p < 1020 %}
          {% set rgb = '120,220,120' %}
          {% set anim = 'pres-normal-breathe' %}
          {% set glow_anim = 'pres-normal-glow' %}
          {% set halo_anim = 'pres-normal-halo' %}
          {% set duration = 3.0 %}
          {% set intensity = 0.6 %}

        {% elif p < 1035 %}
          {% set rgb = '255,200,60' %}
          {% set anim = 'pres-high-pulse' %}
          {% set glow_anim = 'pres-high-glow' %}
          {% set halo_anim = 'pres-high-halo' %}
          {% set duration = 2.6 %}
          {% set intensity = 0.8 %}

        {% else %}
          {% set rgb = '255,80,60' %}
          {% set anim = 'pres-veryhigh-shimmer' %}
          {% set glow_anim = 'pres-veryhigh-glow' %}
          {% set halo_anim = 'pres-veryhigh-halo' %}
          {% set duration = 2.1 %}
          {% set intensity = 1.0 %}
        {% endif %}

        --pres-rgb: {{ rgb }};
        --pres-intensity: {{ intensity }};
        --shape-animation: {{ anim }} {{ duration }}s ease-in-out infinite;
        --pres-glow-animation: {{ glow_anim }} {{ (duration * 0.9) | round(2) }}s ease-in-out infinite;
        --pres-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

        opacity: 1;

        --icon-color: rgba({{ rgb }}, 1);

        background-color: rgba(77, 77, 77,0.1) !important;
        box-shadow: none !important;
        border: 1px solid rgba(255,255,255,0.06);

        position: relative;
        transform-origin: 50% 60%;
        animation: var(--shape-animation);
      }

      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        inset: -8px;
        animation: var(--pres-glow-animation);
      }

      .shape::after {
        inset: -22px;
        animation: var(--pres-halo-animation);
        mix-blend-mode: screen;
      }

      /* LOW */
      @keyframes pres-low-breathe {
        0%   { transform: scale(0.96); }
        50%  { transform: scale(1.03); }
        100% { transform: scale(0.96); }
      }
      @keyframes pres-low-glow {
        0%, 100% {
          box-shadow:
            0 0 20px 0 rgba(var(--pres-rgb), 0.6),
            0 0 34px 6 rgba(var(--pres-rgb), 0.55);
        }
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--pres-rgb), 0.95),
            0 0 50px 10px rgba(var(--pres-rgb), 0.85);
        }
      }
      @keyframes pres-low-halo {
        0%, 100% {
          box-shadow:
            0 0 80px 20px rgba(var(--pres-rgb), 0.35),
            0 -20px 80px -14px rgba(220, 240, 255, 0.55);
        }
        50% {
          box-shadow:
            0 0 130px 36px rgba(var(--pres-rgb), 0.5),
            0 -34px 100px -8px rgba(240, 250, 255, 0.8);
        }
      }

      /* SOFT */
      @keyframes pres-soft-wave {
        0%   { transform: translateX(0); }
        25%  { transform: translateX(-1px); }
        50%  { transform: translateX(1px) translateY(-1px); }
        75%  { transform: translateX(-1px); }
        100% { transform: translateX(0); }
      }
      @keyframes pres-soft-glow {
        0%, 100% {
          box-shadow:
            0 0 22px 0 rgba(var(--pres-rgb), 0.6),
            0 0 34px 4 rgba(var(--pres-rgb), 0.7);
        }
        50% {
          box-shadow:
            0 0 28px 2 rgba(var(--pres-rgb), 0.95),
            0 0 48px 12px rgba(var(--pres-rgb), 0.85);
        }
      }
      @keyframes pres-soft-halo {
        0%, 100% {
          box-shadow:
            0 0 90px 26px rgba(var(--pres-rgb), 0.35),
            0 18px 80px -12px rgba(0, 220, 255, 0.35);
        }
        50% {
          box-shadow:
            0 0 140px 42px rgba(var(--pres-rgb), 0.45),
            0 30px 110px -10px rgba(0, 255, 255, 0.5);
        }
      }

      /* NORMAL */
      @keyframes pres-normal-breathe {
        0%   { transform: scale(0.98); }
        50%  { transform: scale(1.05); }
        100% { transform: scale(0.98); }
      }
      @keyframes pres-normal-glow {
        50% {
          box-shadow:
            0 0 26px 4 rgba(var(--pres-rgb), 0.9),
            0 0 42px 10px rgba(var(--pres-rgb), 0.85);
        }
      }
      @keyframes pres-normal-halo {
        50% {
          box-shadow:
            0 0 120px 40px rgba(var(--pres-rgb), 0.45),
            0 26px 80px -10px rgba(180,255,200,0.5);
        }
      }

      /* HIGH */
      @keyframes pres-high-pulse {
        0%   { transform: scale(1); }
        50%  { transform: scale(1.07); }
        100% { transform: scale(1); }
      }
      @keyframes pres-high-glow {
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--pres-rgb), 0.95),
            0 0 54px 14px rgba(var(--pres-rgb), 0.9);
        }
      }
      @keyframes pres-high-halo {
        50% {
          box-shadow:
            0 0 140px 48px rgba(var(--pres-rgb), 0.55),
            0 26px 100px -10px rgba(255,210,150,0.5);
        }
      }

      /* VERY HIGH */
      @keyframes pres-veryhigh-shimmer {
        0%   { transform: scale(1); filter: blur(0); }
        50%  { transform: scale(1.08); filter: blur(0.6px); }
        100% { transform: scale(1); filter: blur(0); }
      }
      @keyframes pres-veryhigh-glow {
        50% {
          box-shadow:
            0 0 34px 6 rgba(var(--pres-rgb), 1),
            0 0 62px 14px rgba(var(--pres-rgb), 0.95);
        }
      }
      @keyframes pres-veryhigh-halo {
        50% {
          box-shadow:
            0 0 160px 60px rgba(var(--pres-rgb), 0.6),
            0 34px 120px -12px rgba(255,150,100,0.6);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 64px;
        --icon-color: rgba(var(--pres-rgb),1) !important;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 22px;
        padding-bottom: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
        --card-primary-font-size: 1.5rem !important;
        --card-primary-line-height: 1.3 !important;
      }

```
</details>

<details>
<summary><strong>64 - Water Boiler (C)</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.water_boiler
name: Water Boiler
grid_options:
  rows: 1.4
icon: mdi:water-boiler
primary_info: state
secondary_info: name
tap_action:
  action: more-info
icon_color: white
card_mod:
  style: |
    ha-card {
      /* ====== CONFIG ====== */
      {% set temp = states(config.entity) | float(0) %}
      
      {% if temp < 30 %}
        {% set level_pct = (temp / 29) * 39 %}
        {% set rgb = '29, 130, 150' %}  /* Blue */
        {% set speed = '6s' %}
        
      {% elif temp < 35 %}
        {% set level_pct = 40 + ((temp - 30) / 5) * 39 %}
        {% set rgb = '150, 109, 29' %}  /* Orange */
        {% set speed = '4s' %}

      {% else %}
        {% set raw_red = 80 + ((temp - 35) / 10) * 12 %}
        /* Hard Cap at 96% temp exceeds 45C */
        {% set level_pct = 96 if raw_red > 96 else raw_red %}
        {% set rgb = '150, 29, 29' %}  /* Red */
        {% set speed = '2s' %}     
      {% endif %}
        
      /* ===== VARIABLES ===== */
      --liq-color: rgb({{ rgb }});
      --liq-level: {{ level_pct }}%;
      --wave-speed: {{ speed }};
      
      /* ===== STYLING ===== */
      # background-color: #1c1c1c !important;
      border-radius: 12px;
      position: relative;
      overflow: hidden;
      z-index: 0;
      transition: all 0.5s ease;
    }

    /* Icon Styling */
    mushroom-shape-icon {
      --icon-size: 68px;
      display: flex;
      margin: -18px 0 10px -18px !important;
      padding-right: 15px;
      z-index: 2;
    }

    /* --- LIQUID Bar --- */
    ha-card::before {
      content: "";
      position: absolute;
      top: 0; left: 0; bottom: 0;
      z-index: -1;
      
      /* Width based on our calculated level */
      width: calc(var(--liq-level) - 60px);
      
      /* SOLID COLOR prevents the "Seam" issue */
      background: var(--liq-color);
      
      transition: width 0.5s cubic-bezier(0.25, 0.1, 0.25, 1);
    }

    /* --- SPINNING WAVE --- */
    ha-card::after {
      content: "";
      position: absolute;
      z-index: -1;
      
      /* Only hide wave if empty (<= 0C) */
      /* Removed the upper limit check so wave stays at high temp */
      display: {{ 'none' if temp <= 0 else 'block' }};
      
      width: 120px;
      height: 120px;
      
      background: var(--liq-color);
      box-shadow: 0 0 25px rgba({{ rgb }}, 0.5);
      border-radius: 40%;
      
      /* Position Logic */
      left: calc(var(--liq-level) - 120px); 
      top: calc(50% - 60px);
      
      animation: spin-wave var(--wave-speed) linear infinite;
      transition: left 0.5s cubic-bezier(0.25, 0.1, 0.25, 1);
    }

    /* --- CONTENT ON TOP --- */
    .mushroom-state-item {
      z-index: 2;
      position: relative;
      text-shadow: 0 1px 3px rgba(0,0,0,0.8);
    }

    /* Force Icon White */
    ha-state-icon {
      color: white !important;
      filter: drop-shadow(0 2px 4px rgba(0,0,0,0.5));
    }

    /* --- ANIMATIONZZ --- */
    @keyframes spin-wave {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

```
</details>

<details>
<summary><strong>65 - Water Boiler (F)</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.water_boiler
name: Water Boiler (F)
grid_options:
  rows: 1.4
icon: mdi:water-boiler
primary_info: state
secondary_info: name
tap_action:
  action: more-info
icon_color: white
card_mod:
  style: |
    ha-card {
      /* ====== CONFIG ====== */
      {% set temp = states(config.entity) | float(0) %}
      
      {% if temp < 100 %}
        {% set level_pct = (temp / 99) * 35 %}
        {% set rgb = '29, 130, 150' %} /* Blue */
        {% set speed = '6s' %}
        
      {% elif temp < 150 %}
        {% set level_pct = 36 + ((temp - 100) / 50) * 35 %}
        {% set rgb = '150, 109, 29' %} /* Orange */
        {% set speed = '4s' %}
        
      {% else %}
        {% set raw = 72 + ((temp - 150) / 40) * 24 %}
        {% set level_pct = 96 if raw > 96 else raw %}
        {% set rgb = '150, 29, 29' %} /* Red */
        {% set speed = '2s' %}
      {% endif %}

      /* ===== VARIABLES ===== */
      --liq-color: rgb({{ rgb }});
      --liq-level: {{ level_pct }}%;
      --wave-speed: {{ speed }};
      
      /* ===== STYLING ===== */
      border-radius: 12px;
      position: relative;
      overflow: hidden;
      z-index: 0;
      transition: all 0.5s ease;
    }

    mushroom-shape-icon {
      --icon-size: 68px;
      display: flex;
      margin: -18px 0 10px -18px !important;
      padding-right: 15px;
      z-index: 2;
    }

    ha-card::before {
      content: "";
      position: absolute;
      top: 0; left: 0; bottom: 0;
      z-index: -1;
      width: calc(var(--liq-level) - 60px);
      background: var(--liq-color);
      transition: width 0.5s cubic-bezier(0.25, 0.1, 0.25, 1);
    }

    ha-card::after {
      content: "";
      position: absolute;
      z-index: -1;
      display: {{ 'none' if temp <= 40 else 'block' }};
      width: 120px;
      height: 120px;
      background: var(--liq-color);
      box-shadow: 0 0 25px rgba({{ rgb }}, 0.5);
      border-radius: 40%;
      left: calc(var(--liq-level) - 120px);
      top: calc(50% - 60px);
      animation: spin-wave var(--wave-speed) linear infinite;
      transition: left 0.5s cubic-bezier(0.25, 0.1, 0.25, 1);
    }

    .mushroom-state-item {
      z-index: 2;
      position: relative;
      text-shadow: 0 1px 3px rgba(0,0,0,0.8);
    }

    ha-state-icon {
      color: white !important;
      filter: drop-shadow(0 2px 4px rgba(0,0,0,0.5));
    }

    @keyframes spin-wave {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

```
</details>

<details>
<summary><strong>66 - Water Tank</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.water_tank_level
name: Water Tank
grid_options:
  rows: 1.4
tap_action:
  action: more-info
primary_info: state
secondary_info: name
icon: mdi:water
layout: vertical
icon_color: white
card_mod:
  style: |
    ha-card {
      /* ====== DIMENSIONS ====== */
      height: 200px !important;
      --custom-icon-size: 60px;
      --custom-state-font-size: 20px;   /* Size of the % number */
      --custom-name-font-size: 14px; 
      
      /* ====== LOGIC ====== */
      {% set level = states(config.entity) | float(0) %}

      /* Colors */
      {% if level <= 20 %}
        {% set rgb = '150, 29, 29' %} /* Red */
      {% else %}
        {% set rgb = '29, 130, 150' %}  /* Blue */
      {% endif %}

      --liq-color: rgb({{ rgb }});
      --liq-color-light: rgba({{ rgb }}, 0.7);
      --liq-level: {{ level }}%;

      --card-primary-font-size: var(--custom-state-font-size) !important;
      --card-secondary-font-size: var(--custom-name-font-size) !important;
      
      /* Size of the small shapes */
      --wave-size: 40px; 
      
      /* Gradient Body (Solid) */
      background: linear-gradient(to top, 
        var(--liq-color) 0%, 
        var(--liq-color) var(--liq-level), 
        transparent var(--liq-level), 
        transparent 100%
      ) !important;

      position: relative;
      overflow: hidden;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      z-index: 0;

      border: 1px solid rgba({{ rgb }}, 1);
    }

    /* --- Animation Layers --- */
    ha-card::before, ha-card::after {
      content: "";
      position: absolute;
      z-index: 1; /* Low Z-Index so content sits on top */

      height: 30px; 
      width: 200%; 
      bottom: var(--liq-level);
      left: 0;

      background-image: radial-gradient(
        circle at 50% 100%, 
        var(--liq-color) 65%, 
        transparent 66%
      );
      
      background-size: var(--wave-size) 40px;
      background-repeat: repeat-x;
      display: {{ 'none' if level <= 0 or level >= 100 else 'block' }};
      pointer-events: none;
    }

    /* Front Wave */
    ha-card::after {
      background-image: radial-gradient(
        circle at 50% 100%, 
        var(--liq-color) 65%, 
        transparent 66%
      );
      animation: scroll-left 10s linear infinite;
    }

    /* Back Wave */
     ha-card::before {
          background-image: radial-gradient(
            circle at 50% 100%, 
            var(--liq-color-light) 65%, 
            transparent 66%
          );
          animation: scroll-right 3s linear infinite;
          bottom: calc(var(--liq-level) + 5px);
        }

    /* content wrapper */
    mushroom-card-content {
      position: relative !important;
      z-index: 10 !important;
    }

    /* Icon  */
    mushroom-shape-icon {
      position: relative !important;
      z-index: 11 !important; /* Higher than content wrapper */
      --icon-size: var(--custom-icon-size) !important;
    }

    /* Text (Name ,, State) */
    mushroom-state-info {
      position: relative !important;
      z-index: 11 !important;
      text-shadow: 0px 1px 3px rgba(0,0,0,0.9); 
    }

    /* icon color */
    ha-state-icon {
      color: white !important;
    }

    /* --- ANIMATIONS --- */
    @keyframes scroll-left {
      0% { transform: translateX(0); }
      100% { transform: translateX(calc(var(--wave-size) * -1)); }
    }

    @keyframes scroll-right {
      0% { transform: translateX(calc(var(--wave-size) * -1)); }
      100% { transform: translateX(0); }
    }

```
</details>

<details>
<summary><strong>67 - Fuel Tank</strong></summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.fuel_tank_level
name: Fuel Tank
grid_options:
  rows: 1.4
tap_action:
  action: more-info
primary_info: state
secondary_info: name
icon: mdi:barrel
layout: vertical
icon_color: white
card_mod:
  style: |
    ha-card {
      /* ====== DIMENSIONS ====== */
      height: 200px !important;
      --custom-icon-size: 60px;
      --custom-state-font-size: 20px;   /* Size of the % number */
      --custom-name-font-size: 14px; 
      
      /* ====== LOGIC ====== */
      {% set level = states(config.entity) | float(0) %}

      /* Colors */
      {% if level <= 20 %}
        {% set rgb = '150, 29, 29' %} /* Red */
      {% else %}
        {% set rgb = '150, 109, 29' %}  /* Orange..ish */
      {% endif %}

      --liq-color: rgb({{ rgb }});
      --liq-color-light: rgba({{ rgb }}, 0.7);
      --liq-level: {{ level }}%;

      --card-primary-font-size: var(--custom-state-font-size) !important;
      --card-secondary-font-size: var(--custom-name-font-size) !important;
      
      /* Size of the small shapes */
      --wave-size: 40px; 
      
      /* Gradient Body (Solid) */
      background: linear-gradient(to top, 
        var(--liq-color) 0%, 
        var(--liq-color) var(--liq-level), 
        transparent var(--liq-level), 
        transparent 100%
      ) !important;

      position: relative;
      overflow: hidden;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      z-index: 0;

      border: 1px solid rgba({{ rgb }}, 1);
    }

    /* --- Animation Layers --- */
    ha-card::before, ha-card::after {
      content: "";
      position: absolute;
      z-index: 1; /* Low Z-Index so content sits on top */

      height: 30px; 
      width: 200%; 
      bottom: var(--liq-level);
      left: 0;

      background-image: radial-gradient(
        circle at 50% 100%, 
        var(--liq-color) 65%, 
        transparent 66%
      );
      
      background-size: var(--wave-size) 40px;
      background-repeat: repeat-x;
      display: {{ 'none' if level <= 0 or level >= 100 else 'block' }};
      pointer-events: none;
    }

    /* Front Wave */
    ha-card::after {
      background-image: radial-gradient(
        circle at 50% 100%, 
        var(--liq-color) 65%, 
        transparent 66%
      );
      animation: scroll-left 10s linear infinite;
    }

    /* Back Wave */
     ha-card::before {
          background-image: radial-gradient(
            circle at 50% 100%, 
            var(--liq-color-light) 65%, 
            transparent 66%
          );
          animation: scroll-right 3s linear infinite;
          bottom: calc(var(--liq-level) + 5px);
        }

    /* content wrapper */
    mushroom-card-content {
      position: relative !important;
      z-index: 10 !important;
    }

    /* Icon  */
    mushroom-shape-icon {
      position: relative !important;
      z-index: 11 !important; /* Higher than content wrapper */
      --icon-size: var(--custom-icon-size) !important;
    }

    /* Text (Name ,, State) */
    mushroom-state-info {
      position: relative !important;
      z-index: 11 !important;
      text-shadow: 0px 1px 3px rgba(0,0,0,0.9); 
    }

    /* icon color */
    ha-state-icon {
      color: white !important;
    }

    /* --- ANIMATIONS --- */
    @keyframes scroll-left {
      0% { transform: translateX(0); }
      100% { transform: translateX(calc(var(--wave-size) * -1)); }
    }

    @keyframes scroll-right {
      0% { transform: translateX(calc(var(--wave-size) * -1)); }
      100% { transform: translateX(0); }
    }

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
