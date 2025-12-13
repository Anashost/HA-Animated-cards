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

# Home Assistant Animated Battery / Percentage Cards

This [YouTube Video](https://youtu.be/SrFbC1ae35E) explains how to do it.

![gif-16c233439b5ca922](https://github.com/user-attachments/assets/ed91507c-2dc6-4c35-8825-0df2b2b72f69)
`Loading image... please wait`

<hr>

# Cards:

<details>
<summary><strong>1</summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.anasbox_battery_level
tap_action:
  action: more-info
icon: ""
icon_color: white
primary_info: name
secondary_info: none
name: AnasBox Phone
card_mod:
  style:
    .: |
      ha-card {
        /* ====== USER SETTINGS ===== */
        {% set charging_entity =
          'binary_sensor.anasbox_is_charging' %} 
        /* ========================= */

        /* ======= FONT SETTINGS ======= */
        --card-primary-font-size: 15px !important;
        --card-secondary-font-size: 12px !important;
        --card-primary-font-weight: bold !important;

        /* --- LOGIC --- */
        {% set level = states(config.entity) | float(0) %}
        {% set is_charging = is_state(charging_entity, 'on') %}
        
        /* 1. Determine Color */
        {% if is_charging %}
           {% set color = '0, 255, 255' %} /* Cyan (Charging) */
        {% elif level <= 20 %}
          {% set color = '244, 67, 54' %}  /* Red */
        {% elif level <= 60 %}
          {% set color = '255, 152, 0' %}  /* Orange */
        {% else %}
          {% set color = '0, 255, 100' %}  /* Green */
        {% endif %}

        /* --- PASS VARIABLES TO CSS --- */
        --custom-level: {{ level }}%;
        --custom-color: rgba({{ color }}, 0.8);
        --custom-bubble: {{ 'block' if is_charging else 'none' }};
        
        /* Icon Glow */
        --custom-icon-shadow: {{ '0 0 15px rgba(' ~ color ~ ', 0.6)' if is_charging else 'none' }};
        
        /* Text Color */
        --text-color: {{ 'rgba(' ~ color ~ ', 1)' if level < 100 else 'rgba(255,255,255,0.7)' }};

        /* --- CARD STYLING --- */
        background: #1c1c1c !important;
        border: none !important;
        border-radius: 12px;
        position: relative;
        overflow: hidden;
        transition: all 0.5s ease;
        
        /* Ambient Glow behind the liquid */
        background-image: radial-gradient(circle at 24px 24px, rgba({{ color }}, 0.15) 0%, transparent 60%) !important;
      }

      /* Icon Styling */
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        padding-right: 15px;
        padding-bottom: 5px;
      }

      /* --- PERCENTAGE BADGE (Top Right) --- */
      ha-card::before {
        content: '{{ level | round(0) }}%';
        position: absolute;
        top: 12px; right: 12px;
        font-size: 1rem; font-weight: 700;
        color: var(--text-color);
        background: rgba(0, 0, 0, 0.3);
        border: 1px solid rgba(255, 255, 255, 0.1);
        padding: 2px 6px; border-radius: 4px;
      }

      /* --- PROGRESS BAR TRACK --- */
      ha-card::after {
        content: '';
        position: absolute;
        bottom: 0; left: 0;
        height: 4px;
        width: {{ level }}%;
        background: linear-gradient(90deg, transparent, rgb({{ color }}));
        box-shadow: 0 0 10px rgb({{ color }});
        transition: width 0.5s ease;
      }
    mushroom-shape-icon$: |
      .shape {
        /* --- LOGIC INJECTION --- */
        --liquid-level: var(--custom-level);
        --liquid-color: var(--custom-color);
        --bubble-display: var(--custom-bubble);
        
        /* Container Setup */
        background: rgba(255, 255, 255, 0.05) !important;
        overflow: hidden !important; /* Keeps the liquid inside the circle */
        position: relative;
        border: 1px solid rgba(255,255,255,0.1);
        box-shadow: var(--custom-icon-shadow) !important;
      }

      /* THE LIQUID (Wavy Fill) */
      .shape::before {
        content: '';
        position: absolute;
        left: -50%;
        width: 200%;
        height: 200%;
        
        /* The top is calculated based on battery level (100% - level) */
        top: calc(100% - var(--liquid-level));
        
        background: var(--liquid-color);
        border-radius: 40%; /* Creates the "Wave" shape when rotated */
        
        /* The Wave Animation */
        animation: liquid-wave 6s linear infinite;
        opacity: 0.8;
      }

      /* CHARGING BUBBLES */
      .shape::after {
        content: '';
        display: var(--bubble-display);
        position: absolute;
        inset: 0;
        background-image: 
          radial-gradient(2px 2px at 20% 80%, rgba(255,255,255,0.8), transparent),
          radial-gradient(2px 2px at 50% 70%, rgba(255,255,255,0.8), transparent),
          radial-gradient(3px 3px at 80% 90%, rgba(255,255,255,0.8), transparent);
        background-size: 100% 100%;
        animation: bubbles-rise 0.7s linear infinite;
      }

      /* Ensure the MDI Icon sits on top of the liquid */
      ha-icon {
        position: relative;
        z-index: 2;
        /* Blend the icon slightly so it looks submerged */
        mix-blend-mode: overlay; 
        color: white !important;
      }

      /* --- ANIMATIONS --- */
      @keyframes liquid-wave {
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
      }

      @keyframes bubbles-rise {
        0% { transform: translateY(10px); opacity: 0; }
        50% { opacity: 1; }
        100% { transform: translateY(-20px); opacity: 0; }
      }

```
</details>

<details>
<summary><strong>2</summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.anasbox_battery_level
tap_action:
  action: more-info
name: AnasBox Phone
icon_color: white
primary_info: state
secondary_info: name
card_mod:
  style: |
    ha-card {
      /* ====== USER SETTINGS ===== */
      {% set charging = 
      is_state('binary_sensor.anasbox_is_charging', 'on') %}
      /* ========================= */
      
      /* ======= FONT SETTINGS ======= */
      --card-primary-font-size: 15px !important;
      --card-secondary-font-size: 12px !important;
      --card-primary-font-weight: bold !important;

      {% set level = states(config.entity) | float(0) %}
      
      /* 1. DEFINE COLORS (R, G, B) */
      {% if charging %}
        {% set rgb = '29, 130, 150' %}      /* Blue (Charging) */
      {% elif level <= 20 %}
        {% set rgb = '150, 29, 29' %}       /* Red */
      {% elif level <= 60 %}
        {% set rgb = '150, 109, 29' %}      /* Orange */
      {% else %}
        {% set rgb = '29, 150, 59' %}       /* Green */
      {% endif %}

      /* 2. CSS VARIABLES */
      --liq-color: rgb({{ rgb }});
      --liq-level: {{ level }}%;
      --wave-speed: {{ '3s' if charging else '8s' }};
      
      /* ======= STYLING ====== */
      background-color: #1c1c1c !important;
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

    /* --- LAYER 1: THE LIQUID BODY (Bar) --- */
    ha-card::before {
      content: "";
      position: absolute;
      top: 0; left: 0; bottom: 0;
      z-index: -1;
      
      /* Width: Stop exactly where the wave center begins */
      width: calc(var(--liq-level) - 60px);
      
      /* Override for full battery */
      {% if level >= 100 %}
        width: 100%;
      {% endif %}
      
      /* SOLID COLOR prevents the "Seam" issue */
      background: var(--liq-color);
      
      transition: width 0.5s cubic-bezier(0.25, 0.1, 0.25, 1);
    }

    /* --- LAYER 2: THE SPINNING WAVE (Tip) --- */
    ha-card::after {
      content: "";
      position: absolute;
      z-index: -1;
      
      /* Hide wave if empty or full */
      display: {{ 'none' if level <= 0 or level >= 100 else 'block' }};
      
      width: 120px;
      height: 120px;
      
      /* Must match the Bar color exactly */
      background: var(--liq-color);
      box-shadow: 0 0 25px rgba({{ rgb }}, 0.5);
      border-radius: 40%;
      
      /* Position Logic */
      left: calc(var(--liq-level) - 120px); 
      top: calc(50% - 60px);
      
      animation: spin-wave var(--wave-speed) linear infinite;
      transition: left 0.5s cubic-bezier(0.25, 0.1, 0.25, 1);
    }

    /* --- ENSURE CONTENT IS ON TOP --- */
    .mushroom-state-item {
      z-index: 2;
      position: relative;
      /* Add shadow so text is readable over the bright liquid */
      text-shadow: 0 1px 3px rgba(0,0,0,0.8);
    }

    /* Force Icon White */
    ha-state-icon {
      color: white !important;
      filter: drop-shadow(0 2px 4px rgba(0,0,0,0.5));
    }

    /* --- ANIMATION --- */
    @keyframes spin-wave {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

```
</details>

<details>
<summary><strong>3</summary>

```yaml
type: custom:mushroom-entity-card
entity: sensor.anasbox_battery_level
tap_action:
  action: more-info
name: AnasBox Phone
primary_info: state
secondary_info: name
icon_color: white
card_mod:
  style: >
    ha-card {
      /* ====== USER SETTINGS ===== */
      {% set charging = 
      is_state('binary_sensor.anasbox_is_charging', 'on') %}
      /* ========================= */

      /* ======= FONT SETTINGS ======= */
       --card-primary-font-size: 15px !important;
       --card-secondary-font-size: 12px !important;
       --card-primary-font-weight: bold !important;

      {% set level_raw = states(config.entity) | float(0) %}
      {% set level = 0 if level_raw < 0 else (100 if level_raw > 100 else level_raw) %}

      {% if charging %}
        {% set rgb1 = '90, 185, 255' %}
        {% set rgb2 = '140, 240, 255' %}
      {% elif level <= 20 %}
        {% set rgb1 = '255, 85, 95' %}
        {% set rgb2 = '255, 150, 140' %}
      {% elif level <= 60 %}
        {% set rgb1 = '255, 175, 70' %}
        {% set rgb2 = '255, 220, 130' %}
      {% else %}
        {% set rgb1 = '95, 225, 135' %}
        {% set rgb2 = '170, 255, 210' %}
      {% endif %}

      --lvl: {{ level }};
      --c1: rgb({{ rgb1 }});
      --c2: rgb({{ rgb2 }});
      --accent-soft: rgba({{ rgb1 }}, 0.18);
      --accent-med: rgba({{ rgb1 }}, 0.32);

      --track: rgba(255,255,255,0.08);

      --border-speed: {{ '2.2s' if charging else '14s' }};
      --stripe-speed: {{ '1.1s' if charging else '6.5s' }};
      --breath-speed: {{ '1.4s' if charging else '3.8s' }};

      box-shadow:
        0 10px 26px rgba(0,0,0,0.38),
        inset 0 1px 0 rgba(255,255,255,0.04),
        inset 0 -1px 0 rgba(0,0,0,0.25);

      padding-bottom: 28px !important;
      transition: all 0.3s ease;
      overflow: hidden;
    }

    /* Icon Styling */ mushroom-shape-icon {
      --icon-size: 68px;
      display: flex;
      margin: -18px 0 10px -18px !important;
      padding-right: 10px;
      z-index: 2;
    }

    ha-card::before {
      content: "";
      position: absolute;
      left: 14px;
      right: 14px;
      bottom: 12px;
      height: 12px;
      border-radius: 999px;
      z-index: 0;

      background:
        linear-gradient(180deg,
          rgba(255,255,255,0.05),
          rgba(255,255,255,0.00)
        ),
        var(--track);

      box-shadow:
        inset 0 0 0 1px rgba(255,255,255,0.05),
        inset 0 2px 5px rgba(0,0,0,0.35);
    }

    ha-card::after {
      content: "";
      position: absolute;
      left: 14px;
      bottom: 12px;
      height: 12px;
      border-radius: 999px;
      z-index: 1;

      width: calc((100% - 28px) * {{ level / 100 }});

      background-image:
        linear-gradient(90deg, var(--c1), var(--c2)),
        repeating-linear-gradient(
          135deg,
          rgba(255,255,255,0.18) 0px,
          rgba(255,255,255,0.18) 7px,
          transparent 7px,
          transparent 14px
        ),
        linear-gradient(180deg,
          rgba(255,255,255,0.14),
          rgba(255,255,255,0.00) 55%
        );

      /* KEY FIX: give stripes a real tile size */
      background-size:
        100% 100%,
        28px 28px,
        100% 100%;

      background-position:
        0 0,
        0 0,
        0 0;

      background-repeat: no-repeat;

      box-shadow:
        0 0 10px var(--accent-soft),
        0 0 18px var(--accent-med),
        inset 0 0 0 1px rgba(255,255,255,0.10),
        inset 0 2px 6px rgba(0,0,0,0.25);

      transition: width 0.45s cubic-bezier(0.2, 0.85, 0.2, 1);

      animation:
        stripes-move var(--stripe-speed) linear infinite,
        fill-breathe var(--breath-speed) ease-in-out infinite;
    }

    .mushroom-state-item {
      position: relative;
      z-index: 2;
      text-shadow: 0 1px 2px rgba(0,0,0,0.45);
    }



    ha-state-icon {
      color: white !important;
      opacity: 0.96;
      filter:
        drop-shadow(0 2px 3px rgba(0,0,0,0.45))
        drop-shadow(0 0 8px var(--accent-soft));
    }

    /* KEY FIX: move exactly one tile for seamless loop */ @keyframes
    stripes-move {
      0% {
        background-position:
          0 0,
          0 0,
          0 0;
      }
      100% {
        background-position:
          0 0,
          28px 0,
          0 0;
      }
    }

    @keyframes fill-breathe {
      0%, 100% { filter: brightness(1) saturate(1); }
      50%      { filter: brightness(1.14) saturate(1.08); }
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
