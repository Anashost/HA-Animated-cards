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

#  (Updated Recently) Home Assistant Animated Environment cards with graph.

This [YouTube Video](https://youtu.be/avAg9CR9TRc) explains how to do it.

## Preview

<p align="center">
  <img width="1080" alt="gif 42" src="https://github.com/user-attachments/assets/4cd7b5bb-1202-4d36-9aec-2399b405abbf" />
</p>

<hr>

> [!NOTE]
> If you are using the **Sections** view type, you may need to set `rows` to around `1.5` for the card,
> otherwise the card may appear compressed.
> (USE THIS ONLY IF YOU HAVE ISSUES)
>
> ```yaml
> grid_options:
>   rows: 1.5
> ```

<hr>

# Cards:
<details>
<summary><strong>1 - Temperature (C)</strong></summary>

```yaml
type: custom:vertical-stack-in-card
cards:
  - type: custom:mushroom-entity-card
    entity: sensor.livingroom_temperature
    tap_action:
      action: more-info
    icon: mdi:thermometer
    name: Temp
    primary_info: state
    secondary_info: name
    card_mod:
      style:
        mushroom-shape-icon$: |
          .shape {
            {# ======= CONFIG ======= #}
            {% set temp = states(config.entity) | float(0) %}

            {# DEFAULTS #}
            {% set rgb = '0,140,255' %}
            {% set glow_anim = 'temp-cold-glow' %}
            {% set halo_anim = 'temp-cold-halo' %}
            {% set duration = 4.0 %}
            {% set intensity = 0.5 %}

            {# RANGES / COLORS #}
            {# You can change temp numbers below if needed #}

            {% if temp < 18 %}
              {# BLUE #}
              {% set rgb = '0,140,255' %}
              {% set glow_anim = 'temp-cold-glow' %}
              {% set halo_anim = 'temp-cold-halo' %}
              {% set duration = 4.4 %}
              {% set intensity = 0.4 %}
            {% elif temp < 20 %}
              {# YELLOW #}
              {% set rgb = '255,210,40' %}
              {% set glow_anim = 'temp-cool-glow' %}
              {% set halo_anim = 'temp-cool-halo' %}
              {% set duration = 3.4 %}
              {% set intensity = 0.55 %}
            {% elif temp < 22 %}
              {# ORANGE #}
              {% set rgb = '255,150,40' %}
              {% set glow_anim = 'temp-comfy-glow' %}
              {% set halo_anim = 'temp-comfy-halo' %}
              {% set duration = 3.0 %}
              {% set intensity = 0.6 %}
            {% elif temp < 23 %}
              {# DARK ORANGE #}
              {% set rgb = '255,115,20' %}
              {% set glow_anim = 'temp-warm-glow' %}
              {% set halo_anim = 'temp-warm-halo' %}
              {% set duration = 2.4 %}
              {% set intensity = 0.8 %}
            {% else %}
              {# RED #}
              {% set rgb = '255,40,40' %}
              {% set glow_anim = 'temp-hot-glow' %}
              {% set halo_anim = 'temp-hot-halo' %}
              {% set duration = 2.0 %}
              {% set intensity = 1.0 %}
            {% endif %}

            --temp-rgb: {{ rgb }};
            --temp-intensity: {{ intensity }};
            --temp-glow-animation: {{ glow_anim }} {{ duration }}s ease-in-out infinite;
            --temp-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

            opacity: 1;
            --icon-color: rgba({{ rgb }}, 1);
            background-color: rgba(77, 77, 77,0.1) !important;
            box-shadow: none !important;
            border: 1px solid rgba(255,255,255,0.06);
            position: relative;
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
            animation: var(--temp-glow-animation);
          }

          .shape::after {
            inset: -22px;
            animation: var(--temp-halo-animation);
            mix-blend-mode: screen;
          }

          @keyframes temp-cold-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--temp-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--temp-rgb), 0.35); }
          }
          @keyframes temp-cold-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--temp-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--temp-rgb), 0.2); }
          }

          @keyframes temp-cool-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--temp-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--temp-rgb), 0.35); }
          }
          @keyframes temp-cool-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--temp-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--temp-rgb), 0.2); }
          }

          @keyframes temp-comfy-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--temp-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--temp-rgb), 0.35); }
          }
          @keyframes temp-comfy-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--temp-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--temp-rgb), 0.2); }
          }

          @keyframes temp-warm-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--temp-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--temp-rgb), 0.35); }
          }
          @keyframes temp-warm-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--temp-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--temp-rgb), 0.2); }
          }

          @keyframes temp-hot-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--temp-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--temp-rgb), 0.35); }
          }
          @keyframes temp-hot-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--temp-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--temp-rgb), 0.2); }
          }
        .: |
          mushroom-shape-icon {
            --icon-size: 64px;
            --icon-color: rgba(var(--hum-rgb),1) !important;
            display: flex;
            margin: -18px 0 10px -20px !important;
            padding-right: 22px;
            padding-bottom: 25px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            --card-primary-font-size: 1.3rem !important;
            --card-primary-line-height: 1.3 !important;
          }
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
          position: absolute !important;
          inset: 0 !important; 
          margin: 0 !important;
          padding: 0 !important;
          z-index: 1 !important;
          background: transparent !important;
          border: none !important;
          box-shadow: none !important;
          --ha-card-border-width: 0px !important;
          --ha-card-background: transparent !important;
          pointer-events: none;
          opacity: 0.5;
          mask-image: radial-gradient(ellipse at center, rgba(0,0,0,1) 0%, rgba(0,0,0,0) 90%);
        }
        ha-card::before, ha-card::after { display: none !important; }
card_mod:
  style: |
    ha-card {
      overflow: hidden !important; 
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
    primary_info: state
    secondary_info: name
    card_mod:
      style:
        mushroom-shape-icon$: |
          .shape {
            {# ========== CONFIG ========== #}
            {% set hum = states(config.entity) | float(0) %}

            {# DEFAULTS #}
            {% set rgb = '120,210,255' %}
            {% set glow_anim = 'hum-good-glow' %}
            {% set halo_anim = 'hum-good-halo' %}
            {% set duration = 3.4 %}
            {% set intensity = 0.55 %}

            {# RANGES
               < 40   -> BAD (dark blue)
               40-60  -> GOOD (light blue)
               > 60   -> MIDDLE / humid (medium blue)
            #}

            {% if hum < 40 %}
              {# BAD - dry - dark blue #}
              {% set rgb = '0,80,200' %}
              {% set glow_anim = 'hum-bad-glow' %}
              {% set halo_anim = 'hum-bad-halo' %}
              {% set duration = 2.8 %}
              {% set intensity = 0.4 %}
            {% elif hum <= 60 %}
              {# GOOD - light blue #}
              {% set rgb = '120,210,255' %}
              {% set glow_anim = 'hum-good-glow' %}
              {% set halo_anim = 'hum-good-halo' %}
              {% set duration = 3.4 %}
              {% set intensity = 0.55 %}
            {% else %}
              {# MIDDLE / humid - medium blue #}
              {% set rgb = '40,140,255' %}
              {% set glow_anim = 'hum-mid-glow' %}
              {% set halo_anim = 'hum-mid-halo' %}
              {% set duration = 3.0 %}
              {% set intensity = 0.6 %}
            {% endif %}

            --hum-rgb: {{ rgb }};
            --hum-intensity: {{ intensity }};
            --hum-glow-animation: {{ glow_anim }} {{ duration }}s ease-in-out infinite;
            --hum-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

            opacity: 1;
            --icon-color: rgba({{ rgb }}, 1);
            background-color: rgba(77, 77, 77, 0.1) !important;
            box-shadow: none !important;
            border: 1px solid rgba(255,255,255,0.06);
            position: relative;
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
            animation: var(--hum-glow-animation);
          }

          .shape::after {
            inset: -22px;
            animation: var(--hum-halo-animation);
            mix-blend-mode: screen;
          }

          @keyframes hum-bad-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--hum-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--hum-rgb), 0.35); }
          }
          @keyframes hum-bad-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--hum-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--hum-rgb), 0.2); }
          }

          @keyframes hum-good-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--hum-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--hum-rgb), 0.35); }
          }
          @keyframes hum-good-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--hum-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--hum-rgb), 0.2); }
          }

          @keyframes hum-mid-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--hum-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--hum-rgb), 0.35); }
          }
          @keyframes hum-mid-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--hum-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--hum-rgb), 0.2); }
          }
        .: |
          mushroom-shape-icon {
            --icon-size: 64px;
            --icon-color: rgba(var(--hum-rgb), 1) !important;
            display: flex;
            margin: -18px 0 10px -20px !important;
            padding-right: 22px;
            padding-bottom: 25px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            --card-primary-font-size: 1.3rem !important;
            --card-primary-line-height: 1.3 !important;
          }
  - type: custom:mini-graph-card
    entities:
      - sensor.livingroom_humidity
    hours_to_show: 24
    line_width: 5
    line_color: lightblue
    show:
      name: false
      icon: false
      state: false
      labels: false
      legend: false
    card_mod:
      style: |
        ha-card {
          position: absolute !important;
          inset: 0 !important; 
          margin: 0 !important;
          padding: 0 !important;
          z-index: 1 !important;
          background: transparent !important;
          border: none !important;
          box-shadow: none !important;
          --ha-card-border-width: 0px !important;
          --ha-card-background: transparent !important;
          pointer-events: none;
          opacity: 0.5;
          mask-image: radial-gradient(ellipse at center, rgba(0,0,0,1) 0%, rgba(0,0,0,0) 90%);
        }
        ha-card::before, ha-card::after { display: none !important; }
card_mod:
  style: |
    ha-card {
      overflow: hidden !important; 
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
    primary_info: state
    secondary_info: name
    card_mod:
      style:
        mushroom-shape-icon$: |
          .shape {
            {# ========== CONFIG ========== #}
            {% set aqi = states(config.entity) | float(0) %}

            {# DEFAULTS #}
            {% set rgb = '40,190,100' %}
            {% set glow_anim = 'aq-good-glow' %}
            {% set halo_anim = 'aq-good-halo' %}
            {% set duration = 3.4 %}
            {% set intensity = 0.55 %}

            {# RANGES / COLORS #}
            {# You can change numbers below if needed #}
            {% if aqi <= 50 %}
              {# GOOD - GREEN #}
              {% set rgb = '40,190,100' %}
              {% set glow_anim = 'aq-good-glow' %}
              {% set halo_anim = 'aq-good-halo' %}
              {% set duration = 3.4 %}
              {% set intensity = 0.55 %}
            {% elif aqi <= 100 %}
              {# MODERATE - YELLOW #}
              {% set rgb = '255,215,70' %}
              {% set glow_anim = 'aq-moderate-glow' %}
              {% set halo_anim = 'aq-moderate-halo' %}
              {% set duration = 3.0 %}
              {% set intensity = 0.6 %}
            {% elif aqi <= 150 %}
              {# UNHEALTHY FOR SENSITIVE PPL - ORANGE #}
              {% set rgb = '255,170,60' %}
              {% set glow_anim = 'aq-usg-glow' %}
              {% set halo_anim = 'aq-usg-halo' %}
              {% set duration = 2.8 %}
              {% set intensity = 0.7 %}
            {% elif aqi <= 200 %}
              {# UNHEALTHY - RED #}
              {% set rgb = '230,60,60' %}
              {% set glow_anim = 'aq-unhealthy-glow' %}
              {% set halo_anim = 'aq-unhealthy-halo' %}
              {% set duration = 2.4 %}
              {% set intensity = 0.85 %}
            {% elif aqi <= 300 %}
              {# VERY UNHEALTHY - PURPLE #}
              {% set rgb = '170,60,180' %}
              {% set glow_anim = 'aq-veryunhealthy-glow' %}
              {% set halo_anim = 'aq-veryunhealthy-halo' %}
              {% set duration = 2.2 %}
              {% set intensity = 0.95 %}
            {% else %}
              {# HAZARDOUS - DARK MAROON #}
              {% set rgb = '120,0,70' %}
              {% set glow_anim = 'aq-hazard-glow' %}
              {% set halo_anim = 'aq-hazard-halo' %}
              {% set duration = 2.0 %}
              {% set intensity = 1.0 %}
            {% endif %}

            --aq-rgb: {{ rgb }};
            --aq-intensity: {{ intensity }};
            --aq-glow-animation: {{ glow_anim }} {{ duration }}s ease-in-out infinite;
            --aq-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

            opacity: 1;
            --icon-color: rgba({{ rgb }}, 1);
            background-color: rgba(77, 77, 77, 0.1) !important;
            box-shadow: none !important;
            border: 1px solid rgba(255,255,255,0.06);
            position: relative;
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
            animation: var(--aq-glow-animation);
          }

          .shape::after {
            inset: -22px;
            animation: var(--aq-halo-animation);
            mix-blend-mode: screen;
          }

          @keyframes aq-good-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-good-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }

          @keyframes aq-moderate-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-moderate-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }

          @keyframes aq-usg-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-usg-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }

          @keyframes aq-unhealthy-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-unhealthy-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }

          @keyframes aq-veryunhealthy-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-veryunhealthy-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }

          @keyframes aq-hazard-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-hazard-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }
        .: |
          mushroom-shape-icon {
            --icon-size: 64px;
            --icon-color: rgba(var(--aq-rgb), 1) !important;
            display: flex;
            margin: -18px 0 10px -20px !important;
            padding-right: 22px;
            padding-bottom: 25px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            --card-primary-font-size: 1.3rem !important;
            --card-primary-line-height: 1.3 !important;
          }
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
          position: absolute !important;
          inset: 0 !important; 
          margin: 0 !important;
          padding: 0 !important;
          z-index: 1 !important;
          background: transparent !important;
          border: none !important;
          box-shadow: none !important;
          --ha-card-border-width: 0px !important;
          --ha-card-background: transparent !important;
          pointer-events: none;
          opacity: 0.5;
          mask-image: radial-gradient(ellipse at center, rgba(0,0,0,1) 0%, rgba(0,0,0,0) 90%);
        }
        ha-card::before, ha-card::after { display: none !important; }
card_mod:
  style: |
    ha-card {
      overflow: hidden !important; 
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
    primary_info: state
    secondary_info: name
    card_mod:
      style:
        mushroom-shape-icon$: |
          .shape {
            {# ========== CONFIG ========== #}
            {% set temp = states(config.entity) | float(0) %}

            {# DEFAULTS #}
            {% set rgb = '0,140,255' %}
            {% set glow_anim = 'temp-cold-glow' %}
            {% set halo_anim = 'temp-cold-halo' %}
            {% set duration = 4.0 %}
            {% set intensity = 0.5 %}

            {# RANGES / COLORS #}
            {# You can change numbers below if needed #}
            {% if temp < 64 %}
              {# BLUE - COLD #}
              {% set rgb = '0,140,255' %}
              {% set glow_anim = 'temp-cold-glow' %}
              {% set halo_anim = 'temp-cold-halo' %}
              {% set duration = 4.4 %}
              {% set intensity = 0.4 %}
            {% elif temp < 68 %}
              {# YELLOW - COOL #}
              {% set rgb = '255,210,40' %}
              {% set glow_anim = 'temp-cool-glow' %}
              {% set halo_anim = 'temp-cool-halo' %}
              {% set duration = 3.4 %}
              {% set intensity = 0.55 %}
            {% elif temp < 72 %}
              {# ORANGE - COMFY #}
              {% set rgb = '255,150,40' %}
              {% set glow_anim = 'temp-comfy-glow' %}
              {% set halo_anim = 'temp-comfy-halo' %}
              {% set duration = 3.0 %}
              {% set intensity = 0.6 %}
            {% elif temp < 76 %}
              {# DARK ORANGE - WARM #}
              {% set rgb = '255,115,20' %}
              {% set glow_anim = 'temp-warm-glow' %}
              {% set halo_anim = 'temp-warm-halo' %}
              {% set duration = 2.4 %}
              {% set intensity = 0.8 %}
            {% else %}
              {# RED - HOT #}
              {% set rgb = '255,40,40' %}
              {% set glow_anim = 'temp-hot-glow' %}
              {% set halo_anim = 'temp-hot-halo' %}
              {% set duration = 2.0 %}
              {% set intensity = 1.0 %}
            {% endif %}

            --temp-rgb: {{ rgb }};
            --temp-intensity: {{ intensity }};
            --temp-glow-animation: {{ glow_anim }} {{ duration }}s ease-in-out infinite;
            --temp-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

            opacity: 1;
            --icon-color: rgba({{ rgb }}, 1);
            background-color: rgba(77, 77, 77, 0.1) !important;
            box-shadow: none !important;
            border: 1px solid rgba(255,255,255,0.06);
            position: relative;
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
            animation: var(--temp-glow-animation);
          }

          .shape::after {
            inset: -22px;
            animation: var(--temp-halo-animation);
            mix-blend-mode: screen;
          }

          @keyframes temp-cold-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--temp-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--temp-rgb), 0.35); }
          }
          @keyframes temp-cold-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--temp-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--temp-rgb), 0.2); }
          }

          @keyframes temp-cool-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--temp-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--temp-rgb), 0.35); }
          }
          @keyframes temp-cool-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--temp-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--temp-rgb), 0.2); }
          }

          @keyframes temp-comfy-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--temp-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--temp-rgb), 0.35); }
          }
          @keyframes temp-comfy-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--temp-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--temp-rgb), 0.2); }
          }

          @keyframes temp-warm-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--temp-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--temp-rgb), 0.35); }
          }
          @keyframes temp-warm-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--temp-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--temp-rgb), 0.2); }
          }

          @keyframes temp-hot-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--temp-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--temp-rgb), 0.35); }
          }
          @keyframes temp-hot-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--temp-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--temp-rgb), 0.2); }
          }
        .: |
          mushroom-shape-icon {
            --icon-size: 64px;
            --icon-color: rgba(var(--temp-rgb), 1) !important;
            display: flex;
            margin: -18px 0 10px -20px !important;
            padding-right: 22px;
            padding-bottom: 25px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            --card-primary-font-size: 1.3rem !important;
            --card-primary-line-height: 1.3 !important;
          }
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
          position: absolute !important;
          inset: 0 !important; 
          margin: 0 !important;
          padding: 0 !important;
          z-index: 1 !important;
          background: transparent !important;
          border: none !important;
          box-shadow: none !important;
          --ha-card-border-width: 0px !important;
          --ha-card-background: transparent !important;
          pointer-events: none;
          opacity: 0.5;
          mask-image: radial-gradient(ellipse at center, rgba(0,0,0,1) 0%, rgba(0,0,0,0) 90%);
        }
        ha-card::before, ha-card::after { display: none !important; }
card_mod:
  style: |
    ha-card {
      overflow: hidden !important; 
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
    primary_info: state
    secondary_info: name
    card_mod:
      style:
        mushroom-shape-icon$: |
          .shape {
            {# ========== CONFIG ========== #}
            {% set voc = states(config.entity) | float(0) %}

            {# DEFAULTS #}
            {% set rgb = '40,200,120' %}
            {% set glow_anim = 'voc-clean-glow' %}
            {% set halo_anim = 'voc-clean-halo' %}
            {% set duration = 4.0 %}
            {% set intensity = 0.5 %}

            {# RANGES / COLORS #}
            {# You can change numbers below if needed #}

            {% if voc < 100 %}
              {# GREEN #}
              {% set rgb = '40,200,120' %}
              {% set glow_anim = 'voc-clean-glow' %}
              {% set halo_anim = 'voc-clean-halo' %}
              {% set duration = 4.4 %}
              {% set intensity = 0.45 %}
            {% elif voc < 200 %}
              {# YELLOW-GREEN #}
              {% set rgb = '140,220,80' %}
              {% set glow_anim = 'voc-good-glow' %}
              {% set halo_anim = 'voc-good-halo' %}
              {% set duration = 3.6 %}
              {% set intensity = 0.55 %}
            {% elif voc < 300 %}
              {# YELLOW #}
              {% set rgb = '255,210,40' %}
              {% set glow_anim = 'voc-fair-glow' %}
              {% set halo_anim = 'voc-fair-halo' %}
              {% set duration = 3.0 %}
              {% set intensity = 0.7 %}
            {% elif voc < 400 %}
              {# ORANGE #}
              {% set rgb = '255,140,40' %}
              {% set glow_anim = 'voc-poor-glow' %}
              {% set halo_anim = 'voc-poor-halo' %}
              {% set duration = 2.4 %}
              {% set intensity = 0.9 %}
            {% else %}
              {# RED #}
              {% set rgb = '255,50,50' %}
              {% set glow_anim = 'voc-bad-glow' %}
              {% set halo_anim = 'voc-bad-halo' %}
              {% set duration = 2.0 %}
              {% set intensity = 1.0 %}
            {% endif %}

            --voc-rgb: {{ rgb }};
            --voc-intensity: {{ intensity }};
            --voc-glow-animation: {{ glow_anim }} {{ duration }}s ease-in-out infinite;
            --voc-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

            opacity: 1;
            --icon-color: rgba({{ rgb }}, 1);
            background-color: rgba(77, 77, 77, 0.1) !important;
            box-shadow: none !important;
            border: 1px solid rgba(255,255,255,0.06);
            position: relative;
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
            animation: var(--voc-glow-animation);
          }

          .shape::after {
            inset: -22px;
            animation: var(--voc-halo-animation);
            mix-blend-mode: screen;
          }

          @keyframes voc-clean-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--voc-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--voc-rgb), 0.35); }
          }
          @keyframes voc-clean-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--voc-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--voc-rgb), 0.2); }
          }

          @keyframes voc-good-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--voc-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--voc-rgb), 0.35); }
          }
          @keyframes voc-good-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--voc-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--voc-rgb), 0.2); }
          }

          @keyframes voc-fair-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--voc-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--voc-rgb), 0.35); }
          }
          @keyframes voc-fair-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--voc-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--voc-rgb), 0.2); }
          }

          @keyframes voc-poor-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--voc-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--voc-rgb), 0.35); }
          }
          @keyframes voc-poor-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--voc-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--voc-rgb), 0.2); }
          }

          @keyframes voc-bad-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--voc-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--voc-rgb), 0.35); }
          }
          @keyframes voc-bad-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--voc-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--voc-rgb), 0.2); }
          }
        .: |
          mushroom-shape-icon {
            --icon-size: 64px;
            --icon-color: rgba(var(--voc-rgb), 1) !important;
            display: flex;
            margin: -18px 0 10px -20px !important;
            padding-right: 22px;
            padding-bottom: 25px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            --card-primary-font-size: 1.3rem !important;
            --card-primary-line-height: 1.3 !important;
          }
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
          position: absolute !important;
          inset: 0 !important; 
          margin: 0 !important;
          padding: 0 !important;
          z-index: 1 !important;
          background: transparent !important;
          border: none !important;
          box-shadow: none !important;
          --ha-card-border-width: 0px !important;
          --ha-card-background: transparent !important;
          pointer-events: none;
          opacity: 0.5;
          mask-image: radial-gradient(ellipse at center, rgba(0,0,0,1) 0%, rgba(0,0,0,0) 90%);
        }
        ha-card::before, ha-card::after { display: none !important; }
card_mod:
  style: |
    ha-card {
      overflow: hidden !important; 
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
    primary_info: state
    secondary_info: name
    card_mod:
      style:
        mushroom-shape-icon$: |
          .shape {
            {# ========== CONFIG ========== #}
            {% set aqi = states(config.entity) | float(0) %}

            {# DEFAULTS #}
            {% set rgb = '40,190,100' %}
            {% set glow_anim = 'aq-good-glow' %}
            {% set halo_anim = 'aq-good-halo' %}
            {% set duration = 3.4 %}
            {% set intensity = 0.55 %}

            {# RANGES / COLORS #}
            {# You can change numbers below if needed #}

            {% if aqi <= 5 %}
              {# GOOD - GREEN #}
              {% set rgb = '40,190,100' %}
              {% set glow_anim = 'aq-good-glow' %}
              {% set halo_anim = 'aq-good-halo' %}
              {% set duration = 3.4 %}
              {% set intensity = 0.55 %}
            {% elif aqi <= 15 %}
              {# FAIR - LIGHT GREEN #}
              {% set rgb = '140,220,140' %}
              {% set glow_anim = 'aq-fair-glow' %}
              {% set halo_anim = 'aq-fair-halo' %}
              {% set duration = 3.2 %}
              {% set intensity = 0.6 %}
            {% elif aqi <= 50 %}
              {# MODERATE - YELLOW #}
              {% set rgb = '255,215,70' %}
              {% set glow_anim = 'aq-moderate-glow' %}
              {% set halo_anim = 'aq-moderate-halo' %}
              {% set duration = 3.0 %}
              {% set intensity = 0.7 %}
            {% elif aqi <= 90 %}
              {# POOR - ORANGE #}
              {% set rgb = '255,170,60' %}
              {% set glow_anim = 'aq-poor-glow' %}
              {% set halo_anim = 'aq-poor-halo' %}
              {% set duration = 2.8 %}
              {% set intensity = 0.8 %}
            {% elif aqi <= 140 %}
              {# VERY POOR - RED #}
              {% set rgb = '230,60,60' %}
              {% set glow_anim = 'aq-verypoor-glow' %}
              {% set halo_anim = 'aq-verypoor-halo' %}
              {% set duration = 2.4 %}
              {% set intensity = 0.9 %}
            {% else %}
              {# EXTREMELY POOR - DARK MAROON #}
              {% set rgb = '120,0,70' %}
              {% set glow_anim = 'aq-extreme-glow' %}
              {% set halo_anim = 'aq-extreme-halo' %}
              {% set duration = 2.0 %}
              {% set intensity = 1.0 %}
            {% endif %}

            --aq-rgb: {{ rgb }};
            --aq-intensity: {{ intensity }};
            --aq-glow-animation: {{ glow_anim }} {{ duration }}s ease-in-out infinite;
            --aq-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

            opacity: 1;
            --icon-color: rgba({{ rgb }}, 1);
            background-color: rgba(77, 77, 77, 0.1) !important;
            box-shadow: none !important;
            border: 1px solid rgba(255,255,255,0.06);
            position: relative;
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
            animation: var(--aq-glow-animation);
          }

          .shape::after {
            inset: -22px;
            animation: var(--aq-halo-animation);
            mix-blend-mode: screen;
          }

          @keyframes aq-good-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-good-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }

          @keyframes aq-fair-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-fair-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }

          @keyframes aq-moderate-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-moderate-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }

          @keyframes aq-poor-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-poor-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }

          @keyframes aq-verypoor-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-verypoor-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }

          @keyframes aq-extreme-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-extreme-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }
        .: |
          mushroom-shape-icon {
            --icon-size: 64px;
            --icon-color: rgba(var(--aq-rgb), 1) !important;
            display: flex;
            margin: -18px 0 10px -20px !important;
            padding-right: 22px;
            padding-bottom: 25px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            --card-primary-font-size: 1.3rem !important;
            --card-primary-line-height: 1.3 !important;
          }
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
          position: absolute !important;
          inset: 0 !important; 
          margin: 0 !important;
          padding: 0 !important;
          z-index: 1 !important;
          background: transparent !important;
          border: none !important;
          box-shadow: none !important;
          --ha-card-border-width: 0px !important;
          --ha-card-background: transparent !important;
          pointer-events: none;
          opacity: 0.5;
          mask-image: radial-gradient(ellipse at center, rgba(0,0,0,1) 0%, rgba(0,0,0,0) 90%);
        }
        ha-card::before, ha-card::after { display: none !important; }
card_mod:
  style: |
    ha-card {
      overflow: hidden !important; 
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
    primary_info: state
    secondary_info: name
    card_mod:
      style:
        mushroom-shape-icon$: |
          .shape {
            {# ========== CONFIG ========== #}
            {% set aqi = states(config.entity) | float(0) %}

            {# DEFAULTS #}
            {% set rgb = '40,190,100' %}
            {% set glow_anim = 'aq-good-glow' %}
            {% set halo_anim = 'aq-good-halo' %}
            {% set duration = 3.4 %}
            {% set intensity = 0.55 %}

            {# RANGES / COLORS #}
            {# You can change numbers below if needed #}

            {% if aqi <= 5 %}
              {# GOOD - GREEN #}
              {% set rgb = '40,190,100' %}
              {% set glow_anim = 'aq-good-glow' %}
              {% set halo_anim = 'aq-good-halo' %}
              {% set duration = 3.4 %}
              {% set intensity = 0.55 %}
            {% elif aqi <= 15 %}
              {# FAIR - LIGHT GREEN #}
              {% set rgb = '140,220,140' %}
              {% set glow_anim = 'aq-fair-glow' %}
              {% set halo_anim = 'aq-fair-halo' %}
              {% set duration = 3.2 %}
              {% set intensity = 0.6 %}
            {% elif aqi <= 50 %}
              {# MODERATE - YELLOW #}
              {% set rgb = '255,215,70' %}
              {% set glow_anim = 'aq-moderate-glow' %}
              {% set halo_anim = 'aq-moderate-halo' %}
              {% set duration = 3.0 %}
              {% set intensity = 0.7 %}
            {% elif aqi <= 90 %}
              {# POOR - ORANGE #}
              {% set rgb = '255,170,60' %}
              {% set glow_anim = 'aq-poor-glow' %}
              {% set halo_anim = 'aq-poor-halo' %}
              {% set duration = 2.8 %}
              {% set intensity = 0.8 %}
            {% elif aqi <= 140 %}
              {# VERY POOR - RED #}
              {% set rgb = '230,60,60' %}
              {% set glow_anim = 'aq-verypoor-glow' %}
              {% set halo_anim = 'aq-verypoor-halo' %}
              {% set duration = 2.4 %}
              {% set intensity = 0.9 %}
            {% else %}
              {# EXTREMELY POOR - DARK MAROON #}
              {% set rgb = '120,0,70' %}
              {% set glow_anim = 'aq-extreme-glow' %}
              {% set halo_anim = 'aq-extreme-halo' %}
              {% set duration = 2.0 %}
              {% set intensity = 1.0 %}
            {% endif %}

            --aq-rgb: {{ rgb }};
            --aq-intensity: {{ intensity }};
            --aq-glow-animation: {{ glow_anim }} {{ duration }}s ease-in-out infinite;
            --aq-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

            opacity: 1;
            --icon-color: rgba({{ rgb }}, 1);
            background-color: rgba(77, 77, 77, 0.1) !important;
            box-shadow: none !important;
            border: 1px solid rgba(255,255,255,0.06);
            position: relative;
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
            animation: var(--aq-glow-animation);
          }

          .shape::after {
            inset: -22px;
            animation: var(--aq-halo-animation);
            mix-blend-mode: screen;
          }

          @keyframes aq-good-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-good-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }

          @keyframes aq-fair-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-fair-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }

          @keyframes aq-moderate-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-moderate-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }

          @keyframes aq-poor-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-poor-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }

          @keyframes aq-verypoor-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-verypoor-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }

          @keyframes aq-extreme-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--aq-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--aq-rgb), 0.35); }
          }
          @keyframes aq-extreme-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--aq-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--aq-rgb), 0.2); }
          }
        .: |
          mushroom-shape-icon {
            --icon-size: 64px;
            --icon-color: rgba(var(--aq-rgb), 1) !important;
            display: flex;
            margin: -18px 0 10px -20px !important;
            padding-right: 22px;
            padding-bottom: 25px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            --card-primary-font-size: 1.3rem !important;
            --card-primary-line-height: 1.3 !important;
          }
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
          position: absolute !important;
          inset: 0 !important; 
          margin: 0 !important;
          padding: 0 !important;
          z-index: 1 !important;
          background: transparent !important;
          border: none !important;
          box-shadow: none !important;
          --ha-card-border-width: 0px !important;
          --ha-card-background: transparent !important;
          pointer-events: none;
          opacity: 0.5;
          mask-image: radial-gradient(ellipse at center, rgba(0,0,0,1) 0%, rgba(0,0,0,0) 90%);
        }
        ha-card::before, ha-card::after { display: none !important; }
card_mod:
  style: |
    ha-card {
      overflow: hidden !important; 
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
    primary_info: state
    secondary_info: name
    card_mod:
      style:
        mushroom-shape-icon$: |
          .shape {
            {# ========== CONFIG ========== #}
            {% set lux = states(config.entity) | float(0) %}

            {# DEFAULTS #}
            {% set rgb = '40,80,255' %}
            {% set glow_anim = 'lux-dark-glow' %}
            {% set halo_anim = 'lux-dark-halo' %}
            {% set duration = 4.0 %}
            {% set intensity = 0.5 %}

            {# RANGES / COLORS #}
            {# You can change numbers below if needed #}
            {% if lux < 10 %}
              {# DEEP BLUE - VERY DARK #}
              {% set rgb = '40,80,255' %}
              {% set glow_anim = 'lux-dark-glow' %}
              {% set halo_anim = 'lux-dark-halo' %}
              {% set duration = 4.4 %}
              {% set intensity = 0.4 %}
            {% elif lux < 50 %}
              {# PURPLE - DIM #}
              {% set rgb = '140,80,220' %}
              {% set glow_anim = 'lux-dim-glow' %}
              {% set halo_anim = 'lux-dim-halo' %}
              {% set duration = 3.6 %}
              {% set intensity = 0.55 %}
            {% elif lux < 200 %}
              {# SOFT YELLOW - COMFY #}
              {% set rgb = '255,210,80' %}
              {% set glow_anim = 'lux-comfy-glow' %}
              {% set halo_anim = 'lux-comfy-halo' %}
              {% set duration = 3.0 %}
              {% set intensity = 0.6 %}
            {% elif lux < 500 %}
              {# WARM ORANGE - BRIGHT #}
              {% set rgb = '255,160,60' %}
              {% set glow_anim = 'lux-bright-glow' %}
              {% set halo_anim = 'lux-bright-halo' %}
              {% set duration = 2.6 %}
              {% set intensity = 0.8 %}
            {% else %}
              {# NEAR WHITE - VERY BRIGHT #}
              {% set rgb = '255,250,230' %}
              {% set glow_anim = 'lux-sun-glow' %}
              {% set halo_anim = 'lux-sun-halo' %}
              {% set duration = 2.0 %}
              {% set intensity = 1.0 %}
            {% endif %}

            --lux-rgb: {{ rgb }};
            --lux-intensity: {{ intensity }};
            --lux-glow-animation: {{ glow_anim }} {{ duration }}s ease-in-out infinite;
            --lux-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

            opacity: 1;
            --icon-color: rgba({{ rgb }}, 1);
            background-color: rgba(77, 77, 77, 0.1) !important;
            box-shadow: none !important;
            border: 1px solid rgba(255, 255, 255, 0.06);
            position: relative;
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
            animation: var(--lux-glow-animation);
          }

          .shape::after {
            inset: -22px;
            animation: var(--lux-halo-animation);
            mix-blend-mode: screen;
          }

          @keyframes lux-dark-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--lux-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--lux-rgb), 0.35); }
          }
          @keyframes lux-dark-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--lux-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--lux-rgb), 0.2); }
          }

          @keyframes lux-dim-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--lux-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--lux-rgb), 0.35); }
          }
          @keyframes lux-dim-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--lux-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--lux-rgb), 0.2); }
          }

          @keyframes lux-comfy-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--lux-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--lux-rgb), 0.35); }
          }
          @keyframes lux-comfy-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--lux-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--lux-rgb), 0.2); }
          }

          @keyframes lux-bright-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--lux-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--lux-rgb), 0.35); }
          }
          @keyframes lux-bright-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--lux-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--lux-rgb), 0.2); }
          }

          @keyframes lux-sun-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--lux-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--lux-rgb), 0.35); }
          }
          @keyframes lux-sun-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--lux-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--lux-rgb), 0.2); }
          }
        .: |
          mushroom-shape-icon {
            --icon-size: 64px;
            --icon-color: rgba(var(--lux-rgb), 1) !important;
            display: flex;
            margin: -18px 0 10px -20px !important;
            padding-right: 22px;
            padding-bottom: 25px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            --card-primary-font-size: 1.3rem !important;
            --card-primary-line-height: 1.3 !important;
          }
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
          position: absolute !important;
          inset: 0 !important; 
          margin: 0 !important;
          padding: 0 !important;
          z-index: 1 !important;
          background: transparent !important;
          border: none !important;
          box-shadow: none !important;
          --ha-card-border-width: 0px !important;
          --ha-card-background: transparent !important;
          pointer-events: none;
          opacity: 0.5;
          mask-image: radial-gradient(ellipse at center, rgba(0,0,0,1) 0%, rgba(0,0,0,0) 90%);
        }
        ha-card::before, ha-card::after { display: none !important; }
card_mod:
  style: |
    ha-card {
      overflow: hidden !important; 
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
    primary_info: state
    secondary_info: name
    card_mod:
      style:
        mushroom-shape-icon$: |
          .shape {
            {# ========== CONFIG ========== #}
            {% set co2 = states(config.entity) | float(0) %}

            {# DEFAULTS #}
            {% set rgb = '40,200,120' %}
            {% set glow_anim = 'co2-fresh-glow' %}
            {% set halo_anim = 'co2-fresh-halo' %}
            {% set duration = 4.0 %}
            {% set intensity = 0.5 %}

            {# RANGES / COLORS #}
            {# You can change numbers below if needed #}

            {% if co2 < 600 %}
              {# FRESH GREEN #}
              {% set rgb = '40,200,120' %}
              {% set glow_anim = 'co2-fresh-glow' %}
              {% set halo_anim = 'co2-fresh-halo' %}
              {% set duration = 4.4 %}
              {% set intensity = 0.45 %}
            {% elif co2 < 800 %}
              {# SOFT GREEN #}
              {% set rgb = '120,220,120' %}
              {% set glow_anim = 'co2-good-glow' %}
              {% set halo_anim = 'co2-good-halo' %}
              {% set duration = 3.6 %}
              {% set intensity = 0.55 %}
            {% elif co2 < 1000 %}
              {# YELLOW #}
              {% set rgb = '255,210,40' %}
              {% set glow_anim = 'co2-ok-glow' %}
              {% set halo_anim = 'co2-ok-halo' %}
              {% set duration = 3.0 %}
              {% set intensity = 0.65 %}
            {% elif co2 < 1400 %}
              {# ORANGE #}
              {% set rgb = '255,140,40' %}
              {% set glow_anim = 'co2-high-glow' %}
              {% set halo_anim = 'co2-high-halo' %}
              {% set duration = 2.4 %}
              {% set intensity = 0.85 %}
            {% else %}
              {# RED #}
              {% set rgb = '255,50,50' %}
              {% set glow_anim = 'co2-bad-glow' %}
              {% set halo_anim = 'co2-bad-halo' %}
              {% set duration = 2.0 %}
              {% set intensity = 1.0 %}
            {% endif %}

            --co2-rgb: {{ rgb }};
            --co2-intensity: {{ intensity }};
            --co2-glow-animation: {{ glow_anim }} {{ duration }}s ease-in-out infinite;
            --co2-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

            opacity: 1;
            --icon-color: rgba({{ rgb }}, 1);
            background-color: rgba(77, 77, 77, 0.1) !important;
            box-shadow: none !important;
            border: 1px solid rgba(255,255,255,0.06);
            position: relative;
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
            animation: var(--co2-glow-animation);
          }

          .shape::after {
            inset: -22px;
            animation: var(--co2-halo-animation);
            mix-blend-mode: screen;
          }

          @keyframes co2-fresh-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--co2-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--co2-rgb), 0.35); }
          }
          @keyframes co2-fresh-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--co2-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--co2-rgb), 0.2); }
          }

          @keyframes co2-good-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--co2-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--co2-rgb), 0.35); }
          }
          @keyframes co2-good-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--co2-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--co2-rgb), 0.2); }
          }

          @keyframes co2-ok-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--co2-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--co2-rgb), 0.35); }
          }
          @keyframes co2-ok-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--co2-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--co2-rgb), 0.2); }
          }

          @keyframes co2-high-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--co2-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--co2-rgb), 0.35); }
          }
          @keyframes co2-high-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--co2-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--co2-rgb), 0.2); }
          }

          @keyframes co2-bad-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--co2-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--co2-rgb), 0.35); }
          }
          @keyframes co2-bad-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--co2-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--co2-rgb), 0.2); }
          }
        .: |
          mushroom-shape-icon {
            --icon-size: 64px;
            --icon-color: rgba(var(--co2-rgb), 1) !important;
            display: flex;
            margin: -18px 0 10px -20px !important;
            padding-right: 22px;
            padding-bottom: 25px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            --card-primary-font-size: 1.3rem !important;
            --card-primary-line-height: 1.3 !important;
          }
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
          position: absolute !important;
          inset: 0 !important; 
          margin: 0 !important;
          padding: 0 !important;
          z-index: 1 !important;
          background: transparent !important;
          border: none !important;
          box-shadow: none !important;
          --ha-card-border-width: 0px !important;
          --ha-card-background: transparent !important;
          pointer-events: none;
          opacity: 0.5;
          mask-image: radial-gradient(ellipse at center, rgba(0,0,0,1) 0%, rgba(0,0,0,0) 90%);
        }
        ha-card::before, ha-card::after { display: none !important; }
card_mod:
  style: |
    ha-card {
      overflow: hidden !important; 
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
            {% set glow_anim = 'pres-normal-glow' %}
            {% set halo_anim = 'pres-normal-halo' %}
            {% set duration = 3.6 %}
            {% set intensity = 0.55 %}

            {# RANGES / COLORS #}
            {# You can change numbers below if needed #}

            {% if p < 990 %}
              {# BLUE - LOW #}
              {% set rgb = '0,140,255' %}
              {% set glow_anim = 'pres-low-glow' %}
              {% set halo_anim = 'pres-low-halo' %}
              {% set duration = 4.4 %}
              {% set intensity = 0.45 %}
            {% elif p < 1005 %}
              {# TEAL - SOFT #}
              {% set rgb = '60,190,200' %}
              {% set glow_anim = 'pres-soft-glow' %}
              {% set halo_anim = 'pres-soft-halo' %}
              {% set duration = 3.6 %}
              {% set intensity = 0.55 %}
            {% elif p < 1020 %}
              {# GREEN - NORMAL #}
              {% set rgb = '120,220,120' %}
              {% set glow_anim = 'pres-normal-glow' %}
              {% set halo_anim = 'pres-normal-halo' %}
              {% set duration = 3.0 %}
              {% set intensity = 0.6 %}
            {% elif p < 1035 %}
              {# YELLOW - HIGH #}
              {% set rgb = '255,200,60' %}
              {% set glow_anim = 'pres-high-glow' %}
              {% set halo_anim = 'pres-high-halo' %}
              {% set duration = 2.6 %}
              {% set intensity = 0.8 %}
            {% else %}
              {# RED - VERY HIGH #}
              {% set rgb = '255,80,60' %}
              {% set glow_anim = 'pres-veryhigh-glow' %}
              {% set halo_anim = 'pres-veryhigh-halo' %}
              {% set duration = 2.1 %}
              {% set intensity = 1.0 %}
            {% endif %}

            --pres-rgb: {{ rgb }};
            --pres-intensity: {{ intensity }};
            --pres-glow-animation: {{ glow_anim }} {{ duration }}s ease-in-out infinite;
            --pres-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

            opacity: 1;
            --icon-color: rgba({{ rgb }}, 1);
            background-color: rgba(77, 77, 77, 0.1) !important;
            box-shadow: none !important;
            border: 1px solid rgba(255,255,255,0.06);
            position: relative;
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

          @keyframes pres-low-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--pres-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--pres-rgb), 0.35); }
          }
          @keyframes pres-low-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--pres-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--pres-rgb), 0.2); }
          }

          @keyframes pres-soft-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--pres-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--pres-rgb), 0.35); }
          }
          @keyframes pres-soft-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--pres-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--pres-rgb), 0.2); }
          }

          @keyframes pres-normal-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--pres-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--pres-rgb), 0.35); }
          }
          @keyframes pres-normal-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--pres-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--pres-rgb), 0.2); }
          }

          @keyframes pres-high-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--pres-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--pres-rgb), 0.35); }
          }
          @keyframes pres-high-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--pres-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--pres-rgb), 0.2); }
          }

          @keyframes pres-veryhigh-glow {
            0%, 100% { box-shadow: 0 0 15px 0 rgba(var(--pres-rgb), 0.2); }
            50%      { box-shadow: 0 0 20px 2 rgba(var(--pres-rgb), 0.35); }
          }
          @keyframes pres-veryhigh-halo {
            0%, 100% { box-shadow: 0 0 35px 10px rgba(var(--pres-rgb), 0.1); }
            50%      { box-shadow: 0 0 45px 12px rgba(var(--pres-rgb), 0.2); }
          }
        .: |
          mushroom-shape-icon {
            --icon-size: 64px;
            --icon-color: rgba(var(--pres-rgb), 1) !important;
            display: flex;
            margin: -18px 0 10px -20px !important;
            padding-right: 22px;
            padding-bottom: 25px;
          }
          ha-card {
            clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
            --card-primary-font-size: 1.3rem !important;
            --card-primary-line-height: 1.3 !important;
          }
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
          position: absolute !important;
          inset: 0 !important; 
          margin: 0 !important;
          padding: 0 !important;
          z-index: 1 !important;
          background: transparent !important;
          border: none !important;
          box-shadow: none !important;
          --ha-card-border-width: 0px !important;
          --ha-card-background: transparent !important;
          pointer-events: none;
          opacity: 0.5;
          mask-image: radial-gradient(ellipse at center, rgba(0,0,0,1) 0%, rgba(0,0,0,0) 90%);
        }
        ha-card::before, ha-card::after { display: none !important; }
card_mod:
  style: |
    ha-card {
      overflow: hidden !important; 
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
