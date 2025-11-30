Those Animations also works with:

`mushroom legacy template card`

Needs some tweakes tho:

### example

<details>
<summary><strong>template card</summary>

```yaml
type: custom:mushroom-legacy-template-card
primary: Fan
secondary: "{{states('switch.plug_6_local')}}"
icon: mdi:fan
layout: horizontal
entity: switch.plug_6_local
tap_action:
  action: toggle
hold_action:
  action: none
double_tap_action:
  action: none
badge_color: ""
badge_icon: ""
fill_container: true
icon_color: cyan
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

      ## Add those only to 
      ## mushroom legacy template card

      ha-state-icon {
        {% if is_state(config.entity, 'on') %}
          filter: none;
        {% else %}
          filter: grayscale(1);
        {% endif %}
      }
      mushroom-shape-icon {
        {% if is_state(config.entity, 'on') %}
          filter: none;
        {% else %}
          filter: grayscale(1);
        {% endif %}
      }

```
</details>

So, simply add the card mode style you want, then add this at the bottom to fix the icon.

<details>
<summary><strong>the fix</summary>

```yaml
      ## Add those only to 
      ## mushroom legacy template card

      ha-state-icon {
        {% if is_state(config.entity, 'on') %}
          filter: none;
        {% else %}
          filter: grayscale(1);
        {% endif %}
      }
      mushroom-shape-icon {
        {% if is_state(config.entity, 'on') %}
          filter: none;
        {% else %}
          filter: grayscale(1);
        {% endif %}
      }
```
</details>
