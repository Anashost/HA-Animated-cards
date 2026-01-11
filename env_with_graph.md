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

# Home Assistant Animated Environment cards with graph.


## Preview

![528866814-fa15fbcc-b3e8-4db3-8d69-e9368dc49a2a](https://github.com/user-attachments/assets/a57463d6-40b5-45b4-bb4d-6e0fd3bf0b78)

`Loading images... please wait`

# Cards:
<details>
<summary><strong>1 - Temperature</strong></summary>

```yaml
type: custom:vertical-stack-in-card
cards:
  - type: custom:mushroom-entity-card
    entity: sensor.livingroom_temperature
    tap_action:
      action: more-info
    icon: mdi:thermometer
    name: Temperature
    grid_options:
      rows: 1.4
    primary_info: state
    secondary_info: name
    card_mod:
      style:
        mushroom-shape-icon$: |
          .shape {
            {# ========== CONFIG ========== #}
            {# == Updated: entity auto generated == #}
            {% set temp = states(config.entity) | float(0) %}

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

            /* KILL THE THEME BLUE & MAKE SHAPE NEUTRAL */
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
            padding-bottom: 50px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            
            /* FONT SIZE & SPACING SETTINGS */
            --card-primary-font-size: 1.4rem !important;
            
            /* Increases vertical space between primary and secondary */
            --card-primary-line-height: 1.3 !important;
          }
  - type: custom:vertical-stack-in-card
    cards:
      - type: custom:mini-graph-card
        entities:
          - sensor.livingroom_temperature
        hours_to_show: 24
        line_width: 5
        show:
          name: false
          icon: false
          state: false
          labels: false
          legend: false
        color_thresholds:
          - value: 0
            color: blue
          - value: 16
            color: lightblue
          - value: 18
            color: orange
          - value: 21
            color: red
        card_mod:
          style: |
            ha-card {
              background: none;
              box-shadow: none;
              opacity: 50%;
              border: none;
              width: 400px;
              mask-image: radial-gradient(
                ellipse at center,
                rgba(0,0,0,1) 0%,
                rgba(0,0,0,0) 90%
              );
            }
    card_mod:
      style:
        .: |
          ha-card {
              background: none;
              box-shadow: none;
              border: none;
              margin: 8px 12px; 
              position: absolute;
              bottom: -10px;
              right: -10px;
              }

```
</details>

<details>
<summary><strong>2 - Humidity</strong></summary>

```yaml
type: custom:vertical-stack-in-card
cards:
  - type: custom:mushroom-entity-card
    entity: sensor.livingroom_humidity
    tap_action:
      action: more-info
    icon: mdi:water-percent
    name: Humidity
    grid_options:
      rows: 1.4
    primary_info: state
    secondary_info: name
    card_mod:
      style:
        mushroom-shape-icon$: |
          .shape {
            {# ========== CONFIG ========== #}
            {# == Updated: entity auto generated == #}
            {% set hum = states(config.entity) | float(0) %}

            {# DEFAULTS #}
            {% set rgb = '120,210,255' %}
            {% set anim = 'hum-good-breathe' %}
            {% set glow_anim = 'hum-good-glow' %}
            {% set halo_anim = 'hum-good-halo' %}
            {% set duration = 3.2 %}

            {# RANGES
               < 40   -> BAD (dark blue)
               40-60  -> GOOD (light blue)
               > 60   -> MIDDLE / humid (medium blue)
            #}

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
            padding-bottom: 50px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            
            /* FONT SIZE & SPACING SETTINGS */
            --card-primary-font-size: 1.4rem !important;
            
            /* Increases vertical space between primary and secondary */
            --card-primary-line-height: 1.3 !important;
          }
  - type: custom:vertical-stack-in-card
    cards:
      - type: custom:mini-graph-card
        entities:
          - sensor.livingroom_humidity
        line_color: lightblue
        line_width: 5
        hours_to_show: 24
        show:
          name: false
          icon: false
          state: false
          labels: false
          legend: false
        card_mod:
          style: |
            ha-card {
              background: none;
              box-shadow: none;
              opacity: 50%;
              border: none;
              width: 400px;
              mask-image: radial-gradient(
                ellipse at center,
                rgba(0,0,0,1) 0%,
                rgba(0,0,0,0) 90%
              );
            }
    card_mod:
      style:
        .: |
          ha-card {
              background: none;
              box-shadow: none;
              border: none;
              margin: 8px 12px; 
              position: absolute;
              bottom: -10px;
              right: -10px;
              }

```
</details>

<details>
<summary><strong>3 - Airquility (US)</strong></summary>

```yaml
type: custom:vertical-stack-in-card
cards:
  - type: custom:mushroom-entity-card
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
            {% set aqi = states(config.entity) | float(0) %}

            {# DEFAULTS (overridden by ranges) #}
            {% set rgb = '40,190,100' %}
            {% set anim = 'aq-good-breathe' %}
            {% set glow_anim = 'aq-good-glow' %}
            {% set halo_anim = 'aq-good-halo' %}
            {% set duration = 3.2 %}

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
            padding-bottom: 50px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            
            /* FONT SIZE & SPACING SETTINGS */
            --card-primary-font-size: 1.5rem !important;
            
            /* Increases vertical space between primary and secondary */
            --card-primary-line-height: 1.3 !important;
          }
  - type: custom:vertical-stack-in-card
    cards:
      - type: custom:mini-graph-card
        entities:
          - sensor.livingroom_air_quality
        hours_to_show: 24
        line_width: 5
        show:
          name: false
          icon: false
          state: false
          labels: false
          legend: false
        color_thresholds:
          - value: 0
            color: rgb(40,190,100)
          - value: 51
            color: rgb(255,215,70)
          - value: 101
            color: rgb(255,170,60)
          - value: 151
            color: rgb(230,60,60)
          - value: 201
            color: rgb(170,60,180)
          - value: 301
            color: rgb(120,0,70)
        card_mod:
          style: |
            ha-card {
              background: none;
              box-shadow: none;
              opacity: 0.5;
              border: none;
              width: 400px;
              mask-image: radial-gradient(
                ellipse at center,
                rgba(0,0,0,1) 0%,
                rgba(0,0,0,0) 90%
              );
            }
    card_mod:
      style:
        .: |
          ha-card {
              background: none;
              box-shadow: none;
              border: none;
              margin: 8px 12px; 
              position: absolute;
              bottom: -10px;
              right: -10px;
              }

```
</details>

<details>
<summary><strong>4 - Temperature (F)</strong></summary>

```yaml
type: custom:vertical-stack-in-card
cards:
  - type: custom:mushroom-entity-card
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
            {% set temp = states(config.entity) | float(0) %}

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
            padding-bottom: 50px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            
            /* FONT SIZE & SPACING SETTINGS */
            --card-primary-font-size: 1.5rem !important;
            
            /* Increases vertical space between primary and secondary */
            --card-primary-line-height: 1.3 !important;
          }
  - type: custom:vertical-stack-in-card
    cards:
      - type: custom:mini-graph-card
        entities:
          - sensor.livingroom_temperature_fah
        hours_to_show: 24
        line_width: 5
        show:
          name: false
          icon: false
          state: false
          labels: false
          legend: false
        color_thresholds:
          - value: 0
            color: rgb(0,140,255)
          - value: 64
            color: rgb(255,210,40)
          - value: 68
            color: rgb(255,150,40)
          - value: 72
            color: rgb(255,115,20)
          - value: 76
            color: rgb(255,40,40)
        card_mod:
          style: |
            ha-card {
              background: none;
              box-shadow: none;
              opacity: 50%;
              border: none;
              width: 400px;
              mask-image: radial-gradient(
                ellipse at center,
                rgba(0,0,0,1) 0%,
                rgba(0,0,0,0) 90%
              );
            }
    card_mod:
      style:
        .: |
          ha-card {
              background: none;
              box-shadow: none;
              border: none;
              margin: 8px 12px; 
              position: absolute;
              bottom: -10px;
              right: -10px;
              }

```
</details>

<details>
<summary><strong>5 - Air quality (VOC)</strong></summary>

```yaml
type: custom:vertical-stack-in-card
cards:
  - type: custom:mushroom-entity-card
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
            {% set voc = states(config.entity) | float(0) %}

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
            padding-bottom: 50px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));

            --card-primary-font-size: 1.5rem !important;
            --card-primary-line-height: 1.3 !important;
          }
  - type: custom:vertical-stack-in-card
    cards:
      - type: custom:mini-graph-card
        entities:
          - sensor.livingroom_air_quality_voc
        hours_to_show: 24
        line_width: 5
        show:
          name: false
          icon: false
          state: false
          labels: false
          legend: false
        color_thresholds:
          - value: 0
            color: rgb(40,200,120)
          - value: 100
            color: rgb(140,220,80)
          - value: 200
            color: rgb(255,210,40)
          - value: 300
            color: rgb(255,140,40)
          - value: 400
            color: rgb(255,50,50)
        card_mod:
          style: |
            ha-card {
              background: none;
              box-shadow: none;
              opacity: 50%;
              border: none;
              width: 400px;
              mask-image: radial-gradient(
                ellipse at center,
                rgba(0,0,0,1) 0%,
                rgba(0,0,0,0) 90%
              );
            }
    card_mod:
      style:
        .: |
          ha-card {
              background: none;
              box-shadow: none;
              border: none;
              margin: 8px 12px; 
              position: absolute;
              bottom: -10px;
              right: -10px;
              }

```
</details>

<details>
<summary><strong>6 - Air quality (PM2.5)</strong></summary>

```yaml
type: custom:vertical-stack-in-card
cards:
  - type: custom:mushroom-entity-card
    entity: air_quality.demo_air_quality_home
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
            {% set aqi = states(config.entity) | float(0) %}

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
            padding-bottom: 50px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            
            /* FONT SIZE & SPACING SETTINGS */
            --card-primary-font-size: 1.5rem !important;
            
            /* Increases vertical space between primary and secondary */
            --card-primary-line-height: 1.3 !important;
          }
  - type: custom:vertical-stack-in-card
    cards:
      - type: custom:mini-graph-card
        entities:
          - air_quality.demo_air_quality_home
        hours_to_show: 24
        line_width: 5
        show:
          name: false
          icon: false
          state: false
          labels: false
          legend: false
        color_thresholds:
          - value: 0
            color: rgb(40,190,100)
          - value: 6
            color: rgb(140,220,140)
          - value: 16
            color: rgb(255,215,70)
          - value: 51
            color: rgb(255,170,60)
          - value: 91
            color: rgb(230,60,60)
          - value: 141
            color: rgb(120,0,70)
        card_mod:
          style: |
            ha-card {
              background: none;
              box-shadow: none;
              opacity: 50%;
              border: none;
              width: 400px;
              mask-image: radial-gradient(
                ellipse at center,
                rgba(0,0,0,1) 0%,
                rgba(0,0,0,0) 90%
              );
            }
    card_mod:
      style:
        .: |
          ha-card {
              background: none;
              box-shadow: none;
              border: none;
              margin: 8px 12px; 
              position: absolute;
              bottom: -10px;
              right: -10px;
              }

```
</details>

<details>
<summary><strong>7 - Air quality (EU)</strong></summary>

```yaml
type: custom:vertical-stack-in-card
cards:
  - type: custom:mushroom-entity-card
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
            {% set aqi = states(config.entity) | float(0) %}

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
            padding-bottom: 50px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            
            /* FONT SIZE & SPACING SETTINGS */
            --card-primary-font-size: 1.5rem !important;
            
            /* Increases vertical space between primary and secondary */
            --card-primary-line-height: 1.3 !important;
          }
  - type: custom:vertical-stack-in-card
    cards:
      - type: custom:mini-graph-card
        entities:
          - sensor.livingroom_air_quality_eu
        hours_to_show: 24
        line_width: 5
        show:
          name: false
          icon: false
          state: false
          labels: false
          legend: false
        color_thresholds:
          - value: 0
            color: rgb(40,190,100)
          - value: 6
            color: rgb(140,220,140)
          - value: 16
            color: rgb(255,215,70)
          - value: 51
            color: rgb(255,170,60)
          - value: 91
            color: rgb(230,60,60)
          - value: 141
            color: rgb(120,0,70)
        card_mod:
          style: |
            ha-card {
              background: none;
              box-shadow: none;
              opacity: 0.5;
              border: none;
              width: 400px;
              mask-image: radial-gradient(
                ellipse at center,
                rgba(0,0,0,1) 0%,
                rgba(0,0,0,0) 90%
              );
            }
    card_mod:
      style:
        .: |
          ha-card {
              background: none;
              box-shadow: none;
              border: none;
              margin: 8px 12px; 
              position: absolute;
              bottom: -10px;
              right: -10px;
              }

```
</details>

<details>
<summary><strong>8 - illuminance (LUX)</strong></summary>

```yaml
type: custom:vertical-stack-in-card
cards:
  - type: custom:mushroom-entity-card
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
            {% set lux = states(config.entity) | float(0) %}

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
            padding-bottom: 50px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            
            /* FONT SIZE & SPACING SETTINGS */
            --card-primary-font-size: 1.5rem !important;
            
            /* Increases vertical space between primary and secondary */
            --card-primary-line-height: 1.3 !important;
          }
  - type: custom:vertical-stack-in-card
    cards:
      - type: custom:mini-graph-card
        entities:
          - sensor.livingroom_illuminance
        hours_to_show: 24
        line_width: 5
        show:
          name: false
          icon: false
          state: false
          labels: false
          legend: false
        color_thresholds:
          - value: 0
            color: rgb(40,80,255)
          - value: 10
            color: rgb(140,80,220)
          - value: 50
            color: rgb(255,210,80)
          - value: 200
            color: rgb(255,160,60)
          - value: 500
            color: rgb(255,250,230)
        card_mod:
          style: |
            ha-card {
              background: none;
              box-shadow: none;
              opacity: 50%;
              border: none;
              width: 400px;
              mask-image: radial-gradient(
                ellipse at center,
                rgba(0,0,0,1) 0%,
                rgba(0,0,0,0) 90%
              );
            }
    card_mod:
      style:
        .: |
          ha-card {
              background: none;
              box-shadow: none;
              border: none;
              margin: 8px 12px; 
              position: absolute;
              bottom: -10px;
              right: -10px;
              }

```
</details>

<details>
<summary><strong>9 - CO2</strong></summary>

```yaml
type: custom:vertical-stack-in-card
cards:
  - type: custom:mushroom-entity-card
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
            {% set co2 = states(config.entity) | float(0) %}

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
            padding-bottom: 50px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));

            /* FONT SIZE & SPACING SETTINGS */
            --card-primary-font-size: 1.5rem !important;

            /* Increases vertical space between primary and secondary */
            --card-primary-line-height: 1.3 !important;
          }
  - type: custom:vertical-stack-in-card
    cards:
      - type: custom:mini-graph-card
        entities:
          - sensor.livingroom_co2_ppm
        hours_to_show: 24
        line_width: 5
        show:
          name: false
          icon: false
          state: false
          labels: false
          legend: false
        color_thresholds:
          - value: 0
            color: rgb(40,200,120)
          - value: 600
            color: rgb(120,220,120)
          - value: 800
            color: rgb(255,210,40)
          - value: 1000
            color: rgb(255,140,40)
          - value: 1400
            color: rgb(255,50,50)
        card_mod:
          style: |
            ha-card {
              background: none;
              box-shadow: none;
              opacity: 50%;
              border: none;
              width: 400px;
              mask-image: radial-gradient(
                ellipse at center,
                rgba(0,0,0,1) 0%,
                rgba(0,0,0,0) 90%
              );
            }
    card_mod:
      style:
        .: |
          ha-card {
              background: none;
              box-shadow: none;
              border: none;
              margin: 8px 12px; 
              position: absolute;
              bottom: -10px;
              right: -10px;
              }

```
</details>

<details>
<summary><strong>10 - Pressure (mbar)</strong></summary>

```yaml
type: custom:vertical-stack-in-card
cards:
  - type: custom:mushroom-entity-card
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
            {% set p = states(config.entity) | float(0) %}

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
            padding-bottom: 50px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            --card-primary-font-size: 1.5rem !important;
            --card-primary-line-height: 1.3 !important;
          }
  - type: custom:vertical-stack-in-card
    cards:
      - type: custom:mini-graph-card
        entities:
          - sensor.livingroom_pressure_mbar
        hours_to_show: 24
        line_width: 5
        show:
          name: false
          icon: false
          state: false
          labels: false
          legend: false
        color_thresholds:
          - value: 0
            color: rgb(0,140,255)
          - value: 990
            color: rgb(60,190,200)
          - value: 1005
            color: rgb(120,220,120)
          - value: 1020
            color: rgb(255,200,60)
          - value: 1035
            color: rgb(255,80,60)
        card_mod:
          style: |
            ha-card {
              background: none;
              box-shadow: none;
              opacity: 50%;
              border: none;
              width: 400px;
              mask-image: radial-gradient(
                ellipse at center,
                rgba(0,0,0,1) 0%,
                rgba(0,0,0,0) 90%
              );
            }
    card_mod:
      style:
        .: |
          ha-card {
              background: none;
              box-shadow: none;
              border: none;
              margin: 8px 12px; 
              position: absolute;
              bottom: -10px;
              right: -10px;
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
