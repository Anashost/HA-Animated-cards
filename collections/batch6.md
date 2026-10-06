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

# Home Assistant [Batch 6](https://youtu.be/RZncjsCWjTw) Collection.

Other collections? watch these YouTube videos for more cards and instructions:
[Batch 1](https://youtu.be/5vYz37AqSO4) | [Batch 2](https://youtu.be/izx0JMrnhWE) | [Batch 3](https://youtu.be/SrFbC1ae35E) | [Batch 4](https://youtu.be/avAg9CR9TRc) | [Batch 5](https://youtu.be/5k6DfaymBZE)

<hr>

> [!NOTE]
> If you are using the **Sections** view type, you may need to set `rows` to around `1.5` for the card,
> otherwise the card may appear compressed.
>
> ```yaml
> grid_options:
>   rows: 1.5
> ```

<hr>

# Cards:

<img width="494" height="136" alt="665270527-ae6cccdf-0a74-4f4f-b61f-e893fa04d808" src="https://github.com/user-attachments/assets/819826fd-397d-44b5-8444-36d6d14c15dc" />


<details>
<summary><strong>Presence sensor card</summary>

```yaml
type: custom:button-card
entity: binary_sensor.aqara_presence_fp300_presence
name: Living Room
show_state: false
show_label: true
show_icon: false
variables:
  distance: sensor.aqara_presence_fp300_target_distance
  show_distance: true
  range: number.aqara_presence_fp300_detection_range
  show_range: true
  max_supported_limit: 6
  zone_steps: 24
  track_button: button.aqara_presence_fp300_track_target_distance
  show_track_button: true
  temp: sensor.aqara_presence_fp300_temperature
  humidity: sensor.aqara_presence_fp300_humidity
  lux: sensor.aqara_presence_fp300_illuminance
  show_environment: true
  temp_low: 18
  temp_mid: 23
  temp_high: 27
  hum_low: 30
  hum_high: 60
  lux_min: 50
  lux_max: 400
  size_shape: 75px
  size_card_height: 125px
  font_primary: 15px
  font_secondary: 12px
  font_badge: 10px
styles:
  card:
    - --config-shape-size: '[[[ return variables.size_shape ]]]'
    - --config-card-height: >
        [[[ return variables.show_range !== false ? variables.size_card_height :
        '99px'; ]]]
    - --config-font-primary: '[[[ return variables.font_primary ]]]'
    - --config-font-secondary: '[[[ return variables.font_secondary ]]]'
    - --config-font-badge: '[[[ return variables.font_badge ]]]'
    - height: var(--config-card-height) !important
    - padding: 0px !important
    - overflow: hidden
    - position: relative
  grid:
    - padding: 12px 16px
    - height: 100%
    - box-sizing: border-box
    - grid-template-areas: '"radar n" "radar l"'
    - grid-template-columns: var(--config-shape-size) 1fr
    - grid-template-rows: auto auto
    - align-content: start
    - gap: 0px 14px
    - position: relative
    - z-index: 2
  name:
    - justify-self: start
    - font-size: var(--config-font-primary)
    - font-weight: 500
    - align-self: end
    - margin-bottom: 2px
    - position: relative
    - color: var(--primary-text-color)
  label:
    - justify-self: start
    - font-size: var(--config-font-secondary)
    - opacity: 0.7
    - align-self: start
    - margin-top: 2px
    - position: relative
    - color: var(--secondary-text-color)
  custom_fields:
    radar:
      - grid-area: radar
      - justify-self: start
      - width: var(--config-shape-size)
      - height: var(--config-shape-size)
      - border-radius: 50%
      - border: 1px solid rgba(128, 128, 128, 0.15)
      - background: rgba(128, 128, 128, 0.05)
      - position: relative
      - overflow: hidden
      - box-shadow: inset 0 2px 8px rgba(0,0,0,0.1)
    badge1:
      - position: absolute
      - top: 12px
      - right: |
          [[[
            let btn_valid = variables.show_track_button !== false && variables.track_button && states[variables.track_button] && states[variables.track_button].state !== 'unknown' && states[variables.track_button].state !== 'unavailable';
            return btn_valid ? '46px' : '12px';
          ]]]
      - transition: right 0.3s ease-out
      - padding: 4px 10px
      - font-size: var(--config-font-badge)
      - letter-spacing: 0.5px
      - white-space: nowrap
      - font-weight: 600
      - text-transform: uppercase
      - z-index: 5
    badge2:
      - position: absolute
      - top: 45px
      - right: 12px
      - padding: 4px 10px
      - font-size: var(--config-font-badge)
      - letter-spacing: 0.5px
      - white-space: nowrap
      - opacity: 0.9
      - font-weight: 500
      - z-index: 5
    track_button:
      - position: absolute
      - top: 11px
      - right: 12px
      - z-index: 10
      - display: |
          [[[
            let btn_valid = variables.show_track_button !== false && variables.track_button && states[variables.track_button] && states[variables.track_button].state !== 'unknown' && states[variables.track_button].state !== 'unavailable';
            return btn_valid ? 'block' : 'none';
          ]]]
    zone_map:
      - position: absolute
      - bottom: 0
      - left: 0
      - width: 100%
      - height: 42px
      - z-index: 1
tap_action:
  action: more-info
label: |
  [[[ 
    if (!entity) return 'Entity Setup Required';
    
    let range_valid = variables.show_range !== false && variables.range && states[variables.range] && states[variables.range].state !== 'unknown' && states[variables.range].state !== 'unavailable';
    if (!range_valid) return '\u00A0';
    
    let max_l = parseFloat(variables.max_supported_limit) || 6.0;
    let bm = parseInt(states[variables.range].state);
    let highest_zone = -1;
    if (!isNaN(bm)) {
      for(let i=23; i>=0; i--) { if((bm & (1<<i)) !== 0) { highest_zone = i; break; } }
    }
    let limit = highest_zone >= 0 ? (highest_zone + 1) * 0.25 : max_l;
    return `Zone Limit: ${limit.toFixed(1)}m`; 
  ]]]
custom_fields:
  badge1: ' '
  badge2: ' '
  track_button:
    card:
      type: custom:button-card
      entity: '[[[ return variables.track_button ]]]'
      icon: mdi:crosshairs-gps
      show_name: false
      show_state: false
      styles:
        card:
          - width: 26px
          - height: 26px
          - border-radius: 50%
          - background: rgba(128, 128, 128, 0.1)
          - border: 1px solid rgba(128, 128, 128, 0.2)
          - box-shadow: 0 2px 4px rgba(0,0,0,0.1)
          - display: flex
        icon:
          - width: 16px
          - color: var(--primary-text-color)
      tap_action:
        action: call-service
        service: button.press
        service_data:
          entity_id: '[[[ return variables.track_button ]]]'
  radar: |
    [[[
      let is_on = entity && entity.state === 'on';
      
      let dist_valid = variables.show_distance !== false && variables.distance && states[variables.distance] && states[variables.distance].state !== 'unknown' && states[variables.distance].state !== 'unavailable';
      let safe_dist = dist_valid ? parseFloat(states[variables.distance].state) : 0;
      
      let range_valid = variables.show_range !== false && variables.range && states[variables.range] && states[variables.range].state !== 'unknown' && states[variables.range].state !== 'unavailable';
      let bm = range_valid ? parseInt(states[variables.range].state) : 0;
      
      let max_r = parseFloat(variables.max_supported_limit) || 6.0;
      let highest_zone = -1;
      if (range_valid && !isNaN(bm)) {
        for(let i=23; i>=0; i--) { if((bm & (1<<i)) !== 0) { highest_zone = i; break; } }
      }
      let range_val = range_valid ? (highest_zone >= 0 ? (highest_zone + 1) * 0.25 : max_r) : max_r;
      
      if (safe_dist > max_r) safe_dist = max_r;
      
      let raw_zone = Math.floor(safe_dist / 0.25);
      let is_zone_valid = range_valid ? ((bm & (1 << raw_zone)) !== 0) : true;
      
      let max_svg = 47.5;
      let range_pct = (range_val / max_r) * max_svg;
      let dist_pct = dist_valid ? ((safe_dist / max_r) * max_svg) : 0;
      
      let c_rgb = is_on ? '0, 229, 255' : '158, 158, 158'; 
      let t_rgb = is_zone_valid ? c_rgb : '255, 82, 82';   
      let stroke_color = 'rgba(128,128,128,0.2)';
      
      return `
        <svg viewBox="0 0 100 100" style="position: absolute; inset: 0; width: 100%; height: 100%; z-index: 2; pointer-events: none;">
          <circle cx="50" cy="50" r="${max_svg}" fill="none" stroke="${stroke_color}" stroke-width="0.5" />
          <circle cx="50" cy="50" r="${max_svg * 0.75}" fill="none" stroke="${stroke_color}" stroke-width="0.5" />
          <circle cx="50" cy="50" r="${max_svg * 0.50}" fill="none" stroke="${stroke_color}" stroke-width="0.5" />
          <circle cx="50" cy="50" r="${max_svg * 0.25}" fill="none" stroke="${stroke_color}" stroke-width="0.5" />
          <path d="M 50 ${50-max_svg} L 50 ${50+max_svg} M ${50-max_svg} 50 L ${50+max_svg} 50" stroke="${stroke_color}" stroke-width="0.5" />
          
          <circle cx="50" cy="50" r="${range_pct}" fill="rgba(${c_rgb}, 0.05)" stroke="rgba(${c_rgb}, 0.3)" stroke-width="0.75" stroke-dasharray="2 2" style="transition: r 0.5s ease;" />
          
          ${is_on && dist_valid ? `
            <circle cx="50" cy="50" r="${dist_pct}" fill="none" stroke="rgba(${t_rgb}, 0.6)" stroke-width="0.5" style="transition: r 0.3s ease-out, stroke 0.3s ease;" />
            <circle cx="50" cy="${50 - dist_pct}" r="2.5" fill="#FFF" filter="drop-shadow(0 0 3px rgba(${t_rgb}, 1))" style="transition: cy 0.3s ease-out;" />
          ` : ''}
          <circle cx="50" cy="50" r="1.5" fill="var(--primary-text-color)" opacity="0.5" />
        </svg>
        
        ${is_on ? `
          <div style="position: absolute; inset: 0; border-radius: 50%; clip-path: circle(${range_pct}% at 50% 50%); transition: clip-path 0.5s ease; z-index: 1;">
            <div style="width: 100%; height: 100%; background: conic-gradient(from 0deg, transparent 70%, rgba(${c_rgb}, 0.3) 100%); animation: radar-spin 2.5s linear infinite;"></div>
          </div>
        ` : ''}
      `;
    ]]]
  zone_map: |
    [[[
      let range_valid = variables.show_range !== false && variables.range && states[variables.range] && states[variables.range].state !== 'unknown' && states[variables.range].state !== 'unavailable';
      if (!range_valid) return '';
      
      let is_on = entity && entity.state === 'on';
      
      let dist_valid = variables.show_distance !== false && variables.distance && states[variables.distance] && states[variables.distance].state !== 'unknown' && states[variables.distance].state !== 'unavailable';
      let safe_dist = dist_valid ? parseFloat(states[variables.distance].state) : 0;
      
      let bm = parseInt(states[variables.range].state);
      if(isNaN(bm)) bm = 0;
      
      let max_r = parseFloat(variables.max_supported_limit) || 6.0;
      let visual_steps = parseInt(variables.zone_steps) || 12;
      
      safe_dist = Math.max(0, Math.min(safe_dist, max_r - 0.001));
      let step_size = max_r / visual_steps;
      let tracked_visual_step = Math.floor(safe_dist / step_size);
      
      let total_raw_zones = Math.ceil(max_r / 0.25); 
      let raw_per_step = total_raw_zones / visual_steps;
      let visual_array = Array(visual_steps).fill(false);
      
      for(let i=0; i<total_raw_zones; i++) {
        if ((bm & (1 << i)) !== 0) {
          let v_idx = Math.floor(i / raw_per_step);
          if (v_idx >= 0 && v_idx < visual_steps) visual_array[v_idx] = true;
        }
      }
      
      let zone_bars = `<div style="display: flex; gap: 2px; height: 16px; width: 100%; align-items: flex-end;">`;
      
      for(let i=0; i<visual_steps; i++) {
        let is_tracked = is_on && dist_valid && (i === tracked_visual_step);
        let is_active = visual_array[i]; 
        
        let h = '15%'; 
        let c = 'rgba(128, 128, 128, 0.2)'; 
        let s = 'z-index: 1;';

        if (is_tracked) {
          h = '100%';
          let raw_zone = Math.floor(safe_dist / 0.25);
          if ((bm & (1 << raw_zone)) !== 0) {
            c = '#00E5FF';
            s = 'box-shadow: 0 0 8px #00E5FF; z-index: 2;';
          } else {
            c = '#FF5252'; 
            s = 'box-shadow: 0 0 8px #FF5252; z-index: 2;';
          }
        } else if (is_active) {
          h = is_on ? '60%' : '35%'; 
          c = is_on ? 'rgba(0, 229, 255, 0.35)' : 'rgba(128, 128, 128, 0.4)';
        }
        
        zone_bars += `<div style="flex: 1; background: ${c}; height: ${h}; border-radius: 1px 1px 0 0; transition: height 0.3s ease, background 0.3s ease; ${s}"></div>`;
      }
      zone_bars += `</div>`;
      
      let l1 = (max_r * 0.25).toFixed(1) + 'm';
      let l2 = (max_r * 0.50).toFixed(1) + 'm';
      let l3 = (max_r * 0.75).toFixed(1) + 'm';
      let l4 = max_r.toFixed(0) + 'm';
      
      let labels = `<div style="display: flex; justify-content: space-between; font-size: 9px; color: var(--secondary-text-color, rgba(150,150,150,0.8)); font-weight: 600; margin-bottom: 4px; padding: 0 2px; letter-spacing: 0.5px;">
        <span>0m</span><span>${l1}</span><span>${l2}</span><span>${l3}</span><span>${l4}</span>
      </div>`;
      
      return `<div style="display: flex; flex-direction: column; width: 100%; height: 100%; justify-content: flex-end; padding: 0 16px 8px 16px; box-sizing: border-box;">${labels}${zone_bars}</div>`;
    ]]]
extra_styles: |
  [[[
    let is_on = entity && entity.state === 'on';
    
    let dist_valid = variables.show_distance !== false && variables.distance && states[variables.distance] && states[variables.distance].state !== 'unknown' && states[variables.distance].state !== 'unavailable' && !isNaN(parseFloat(states[variables.distance].state));
    let safe_dist = dist_valid ? parseFloat(states[variables.distance].state) : 0;
    if (safe_dist > variables.max_supported_limit) safe_dist = variables.max_supported_limit;
    
    let range_valid = variables.show_range !== false && variables.range && states[variables.range] && states[variables.range].state !== 'unknown' && states[variables.range].state !== 'unavailable' && !isNaN(parseInt(states[variables.range].state));
    let bm = range_valid ? parseInt(states[variables.range].state) : 0;
    
    let raw_zone = Math.floor(safe_dist / 0.25);
    let is_zone_valid = range_valid ? ((bm & (1 << raw_zone)) !== 0) : true;
    
    let status_text = 'CLEAR';
    if (!entity) {
      status_text = 'SETUP REQ';
    } else if (is_on) {
      if (dist_valid) {
        status_text = `PRESENCE • ${safe_dist.toFixed(1)}m`;
      } else {
        status_text = 'PRESENCE';
      }
    }
    
    let color = is_on ? (is_zone_valid ? '0, 229, 255' : '255, 82, 82') : '158, 158, 158'; 
    
    let env_parts = [];
    let c_temp = '128, 128, 128';
    let c_hum  = '128, 128, 128';
    let c_lux  = '128, 128, 128';
    
    if (variables.show_environment !== false && variables.temp && states[variables.temp]) {
      let st = states[variables.temp].state;
      if (st !== 'unknown' && st !== 'unavailable') {
        let v = parseFloat(st);
        if (!isNaN(v)) {
          env_parts.push(`${v.toFixed(1)}°C`);
          if (v < variables.temp_low) c_temp = '66, 165, 245';
          else if (v < variables.temp_mid) c_temp = '255, 235, 59';
          else if (v < variables.temp_high) c_temp = '255, 167, 38';
          else c_temp = '239, 83, 80';
        }
      }
    }
    
    if (variables.show_environment !== false && variables.humidity && states[variables.humidity]) {
      let st = states[variables.humidity].state;
      if (st !== 'unknown' && st !== 'unavailable') {
        let v = parseFloat(st);
        if (!isNaN(v)) {
          env_parts.push(`${v.toFixed(0)}%`);
          if (v < variables.hum_low) c_hum = '255, 167, 38';
          else if (v <= variables.hum_high) c_hum = '66, 165, 245';
          else c_hum = '255, 167, 38';
        }
      }
    }
    
    if (variables.show_environment !== false && variables.lux && states[variables.lux]) {
      let st = states[variables.lux].state;
      if (st !== 'unknown' && st !== 'unavailable') {
        let v = parseFloat(st);
        if (!isNaN(v)) {
          env_parts.push(`${v.toFixed(0)}lx`);
          c_lux = v < variables.lux_min ? '120, 144, 156' : (v > variables.lux_max ? '255, 235, 59' : '212, 225, 87');
        }
      }
    }
    
    let b2_text = env_parts.join(' • ');
    let display_b2 = env_parts.length > 0 ? 'block' : 'none';
    let bg_gradient = `linear-gradient(90deg, rgba(${c_temp}, 0.15) 0%, rgba(${c_hum}, 0.15) 50%, rgba(${c_lux}, 0.2) 100%)`;
    
    return `
      #card {
        --appliance-color: ${color};
      }
      
      #badge1 {
        display: block;
        background: rgba(var(--appliance-color), 0.07);
        color: var(--primary-text-color);
        border-top: 1px solid var(--divider-color, rgba(128,128,128,0.2));
        border-bottom: 1px solid var(--divider-color, rgba(128,128,128,0.2));
        border-left: 2.5px solid rgb(var(--appliance-color));
        border-radius: 6px !important;
      }
      #badge1::before { content: "${status_text}"; }
      
      #badge2 {
        display: ${display_b2};
        background: ${bg_gradient};
        color: var(--primary-text-color);
        border-top: 1px solid var(--divider-color, rgba(128,128,128,0.2));
        border-bottom: 1px solid var(--divider-color, rgba(128,128,128,0.2));
        border-left: 2.5px solid rgb(${c_temp});
        border-right: 2.5px solid rgb(${c_lux});
        border-radius: 6px !important;
      }
      #badge2::before { content: "${b2_text}"; }
      
      @keyframes radar-spin {
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
      }
    `;
  ]]]

```
</details>

<hr>

<img width="491" height="105" alt="665270583-e99d9c97-0201-489e-99b3-9506c5fa2cb7" src="https://github.com/user-attachments/assets/bd2c552f-087e-4f22-8e5a-ee703269c08c" />

<details>
<summary><strong>Smoke detector card </summary>

```yaml
type: custom:button-card
entity: binary_sensor.aqara_smoke_detector_smoke
name: Smoke Detector
show_state: false
show_label: true
variables:
  sensor_density: sensor.aqara_smoke_detector_smoke_density
  sensor_battery: sensor.aqara_smoke_detector_battery
  show_bar: false
  theme_idle_colored: false
  heartbeat_color: '#4caf50'
  heartbeat_interval: 3s
  batt_red: 20
  batt_orange: 40
  batt_yellow: 70
  dens_yellow: 0.1
  dens_orange: 0.3
  dens_red: 0.5
  size_icon: 45px
  size_shape: 65px
  size_card_height: 95px
  font_primary: 15px
  font_secondary: 12px
  font_badge: 10px
styles:
  card:
    - --config-icon-size: '[[[ return variables.size_icon ]]]'
    - --config-shape-size: '[[[ return variables.size_shape ]]]'
    - --config-card-height: '[[[ return variables.size_card_height ]]]'
    - --config-font-primary: '[[[ return variables.font_primary ]]]'
    - --config-font-secondary: '[[[ return variables.font_secondary ]]]'
    - --config-font-badge: '[[[ return variables.font_badge ]]]'
    - height: var(--config-card-height) !important
    - padding: 0px !important
    - overflow: hidden
    - position: relative
    - transition: background 0.5s ease
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
    - z-index: 2
  icon:
    - width: var(--config-icon-size)
    - height: var(--config-icon-size)
    - color: var(--primary-text-color)
    - z-index: 3
    - animation: var(--anim-icon-shake)
    - transform-origin: center center
    - will-change: transform
  img_cell:
    - width: var(--config-shape-size)
    - height: var(--config-shape-size)
    - border-radius: 50%
    - border: 1px solid var(--divider-color, rgba(128,128,128,0.2)) !important
    - background: rgba(var(--appliance-color), 0.1) !important
    - position: relative
    - overflow: visible !important
    - justify-self: start
    - z-index: 2
  name:
    - justify-self: start
    - font-size: var(--config-font-primary)
    - font-weight: 500
    - align-self: end
    - margin-bottom: 2px
    - position: relative
    - z-index: 3
  label:
    - justify-self: start
    - font-size: var(--config-font-secondary)
    - opacity: 0.7
    - align-self: start
    - margin-top: 2px
    - position: relative
    - z-index: 3
  custom_fields:
    bg_smoke:
      - position: absolute
      - inset: 0
      - z-index: 0
      - pointer-events: none
      - display: var(--display-smoke)
    heartbeat:
      - position: absolute
      - top: 10px
      - left: 10px
      - width: 6px
      - height: 6px
      - border-radius: 50%
      - background: var(--hb-color)
      - box-shadow: 0 0 6px var(--hb-color)
      - display: var(--display-heartbeat)
      - animation: hardware-blink var(--hb-interval) infinite
      - z-index: 5
    badge1:
      - position: absolute
      - top: 10px
      - right: 10px
      - background: rgba(var(--appliance-color), 0.15)
      - color: var(--primary-text-color)
      - border-top: 1px solid rgba(128,128,128, 0.2)
      - border-bottom: 1px solid rgba(128,128,128, 0.2)
      - border-left: 2.5px solid rgb(var(--appliance-color))
      - padding: 2px 10px
      - border-radius: 6px
      - font-size: var(--config-font-badge)
      - font-weight: 600
      - text-transform: uppercase
      - letter-spacing: 0.5px
      - white-space: nowrap
      - z-index: 5
    badge2:
      - position: absolute
      - top: 38px
      - right: 10px
      - color: var(--primary-text-color)
      - border-top: 1px solid rgba(128,128,128, 0.2)
      - border-bottom: 1px solid rgba(128,128,128, 0.2)
      - padding: 4px 8px
      - font-size: 10px
      - letter-spacing: 0.5px
      - white-space: nowrap
      - opacity: 0.9
      - text-transform: uppercase
      - font-weight: 500
      - border-radius: 6px
      - display: var(--display-badge2)
      - z-index: 5
    bar:
      - position: absolute
      - bottom: 0
      - left: 0
      - height: 3.5px
      - width: var(--appliance-level)
      - background: rgb(var(--appliance-color))
      - box-shadow: 0 0 8px rgb(var(--appliance-color))
      - transition: width 0.5s ease
      - display: var(--display-bar)
      - z-index: 5
tap_action:
  action: more-info
label: |
  [[[ 
    let ent_smoke = entity ? entity.entity_id : null;
    if (!ent_smoke || !states[ent_smoke]) return 'Entity Setup Required';
    return states[ent_smoke].state === 'on' ? 'Smoke Detected' : 'Monitoring';
  ]]]
icon: mdi:smoke-detector
custom_fields:
  badge1: ' '
  badge2: ' '
  bar: ' '
  heartbeat: ' '
  bg_smoke: |
    [[[
      return `
        <div class="smoke-plume plume-1" style="left: 10%; width: 70px; height: 70px; animation-delay: 0s;"></div>
        <div class="smoke-plume plume-2" style="left: 45%; width: 90px; height: 90px; animation-delay: 1.2s;"></div>
        <div class="smoke-plume plume-3" style="left: 20%; width: 60px; height: 60px; animation-delay: 2.5s;"></div>
        <div class="smoke-plume plume-4" style="left: 35%; width: 85px; height: 85px; animation-delay: 3.8s;"></div>
      `;
    ]]]
extra_styles: |
  [[[
    let ent_smoke = entity ? entity.entity_id : null;
    let ent_bat = variables.sensor_battery;
    let ent_den = variables.sensor_density;
    
    let is_smoke = ent_smoke && states[ent_smoke] && states[ent_smoke].state === 'on';
    let raw_bat = states[ent_bat] ? parseFloat(states[ent_bat].state) : NaN;
    let raw_den = states[ent_den] ? parseFloat(states[ent_den].state) : NaN;
    
    let theme_colored = variables.theme_idle_colored !== undefined ? variables.theme_idle_colored : false;
    let status = 'CLEAR';
    let color = theme_colored ? '0, 229, 255' : '158, 158, 158'; 
    
    let anim_shake = 'none';
    let anim_strobe = 'none';
    let display_smoke = 'none';
    let display_heartbeat = 'block';

    if (is_smoke) {
        status = 'SMOKE ALARM';
        color = '244, 67, 54'; 
        anim_shake = 'buzzer-shake 0.1s linear infinite';
        anim_strobe = 'strobe-fade 0.8s ease-in-out infinite';
        display_smoke = 'block';
        display_heartbeat = 'none'; 
    } 

    let progress = isNaN(raw_bat) ? 100 : Math.max(0, Math.min(100, raw_bat));
    let display_bar = (variables.show_bar !== false && !isNaN(raw_bat)) ? 'block' : 'none';
    
    let c_bat = '76, 175, 80'; 
    if (!isNaN(raw_bat)) {
        if (raw_bat <= (variables.batt_red || 20)) { c_bat = '244, 67, 54'; }
        else if (raw_bat <= (variables.batt_orange || 40)) { c_bat = '255, 152, 0'; }
        else if (raw_bat <= (variables.batt_yellow || 70)) { c_bat = '255, 235, 59'; }
    }

    let c_den = '76, 175, 80'; 
    if (!isNaN(raw_den)) {
        if (raw_den >= (variables.dens_red || 0.5)) { c_den = '244, 67, 54'; }
        else if (raw_den >= (variables.dens_orange || 0.3)) { c_den = '255, 152, 0'; }
        else if (raw_den >= (variables.dens_yellow || 0.1)) { c_den = '255, 235, 59'; }
    }

    let b2_arr = [];
    let b2_text = '';
    if (!isNaN(raw_bat)) b2_arr.push(`Bat ${Math.round(raw_bat)}%`);
    if (!isNaN(raw_den)) b2_arr.push(`Den ${raw_den}`);
    
    let display_badge2 = b2_arr.length > 0 ? 'block' : 'none';
    if (b2_arr.length > 0) {
        b2_text = b2_arr.join(' • ');
    }
    
    let bg_badge2 = 'rgba(128,128,128,0.05)';
    let b2_left = '1px solid rgba(128,128,128,0.2)';
    let b2_right = '1px solid rgba(128,128,128,0.2)';

    if (!isNaN(raw_bat) && !isNaN(raw_den)) {
        bg_badge2 = `linear-gradient(90deg, rgba(${c_bat}, 0.15) 30%, rgba(${c_den}, 0.2) 75%)`;
        b2_left = `2.5px solid rgb(${c_bat})`;
        b2_right = `2.5px solid rgb(${c_den})`;
    } else if (!isNaN(raw_bat)) {
        bg_badge2 = `rgba(${c_bat}, 0.15)`;
        b2_left = `2.5px solid rgb(${c_bat})`;
    } else if (!isNaN(raw_den)) {
        bg_badge2 = `rgba(${c_den}, 0.15)`;
        b2_right = `2.5px solid rgb(${c_den})`;
    }

    return `
      #card {
        --appliance-color: ${color};
        --appliance-level: ${progress}%;
        --anim-icon-shake: ${anim_shake};
        --anim-cell-strobe: ${anim_strobe};
        --display-smoke: ${display_smoke};
        --display-bar: ${display_bar};
        --display-heartbeat: ${display_heartbeat};
        --display-badge2: ${display_badge2};
        --hb-color: ${variables.heartbeat_color || '#4caf50'};
        --hb-interval: ${variables.heartbeat_interval || '5s'};
      }
      
      #badge1::before { content: "${status}"; }
      
      #badge2 {
        background: ${bg_badge2};
        border-left: ${b2_left};
        border-right: ${b2_right};
      }
      
      #badge2::before { content: "${b2_text}"; }
      
      #img-cell::before {
        content: '';
        position: absolute;
        inset: 0;
        border-radius: 50%;
        background-color: rgba(var(--appliance-color), 0.5);
        box-shadow: 0 0 20px rgba(var(--appliance-color), 0.6);
        opacity: 0;
        animation: var(--anim-cell-strobe);
        pointer-events: none;
        will-change: opacity;
      }

      .smoke-plume {
        position: absolute;
        bottom: -40px;
        background: radial-gradient(circle at center, color-mix(in srgb, var(--primary-text-color) 40%, transparent) 0%, transparent 65%);
        border-radius: 50%;
        opacity: 0;
        will-change: transform, opacity;
      }

      .plume-1 { animation: drift-1 4s ease-in infinite; }
      .plume-2 { animation: drift-2 4.5s ease-in infinite; }
      .plume-3 { animation: drift-3 5s ease-in infinite; }
      .plume-4 { animation: drift-1 5.5s ease-in infinite; }

      @keyframes buzzer-shake {
        0%, 100% { transform: translate3d(0, 0, 0); }
        25% { transform: translate3d(-1px, 0.5px, 0) rotate(-1.5deg); }
        75% { transform: translate3d(1px, -0.5px, 0) rotate(1.5deg); }
      }
      
      @keyframes strobe-fade {
        0%, 100% { opacity: 0; }
        50% { opacity: 1; }
      }
      
      @keyframes hardware-blink {
        0%, 8%, 100% { opacity: 0; }
        4% { opacity: 1; }
      }

      @keyframes drift-1 {
        0% { transform: translate3d(0, 10px, 0) scale(0.5); opacity: 0; }
        30% { opacity: 0.7; }
        100% { transform: translate3d(-15px, -110px, 0) scale(2.8); opacity: 0; }
      }
      
      @keyframes drift-2 {
        0% { transform: translate3d(0, 10px, 0) scale(0.5); opacity: 0; }
        30% { opacity: 0.6; }
        100% { transform: translate3d(20px, -100px, 0) scale(3.2); opacity: 0; }
      }
      
      @keyframes drift-3 {
        0% { transform: translate3d(0, 10px, 0) scale(0.5); opacity: 0; }
        30% { opacity: 0.8; }
        100% { transform: translate3d(-5px, -120px, 0) scale(3.0); opacity: 0; }
      }
    `;
  ]]]

```
</details>

<hr>

<img width="492" height="475" alt="665270603-0e21a7c6-cfbb-47fd-8f92-ea5fa3a7038f" src="https://github.com/user-attachments/assets/6c76f0ec-6b9a-42b7-9c3e-78a1b6a9aa53" />

<details>
<summary><strong>Liquid card (Water) </summary>

```yaml
type: custom:button-card
entity: sensor.water_tank_level
name: Water Tank
show_icon: true
show_name: true
show_state: true
icon: mdi:water
variables:
  card_h: 150
  circle_size: 100
styles:
  card:
    - height: '[[[ return variables.card_h + ''px'' ]]]'
    - position: relative
    - overflow: hidden
    - background: transparent
    - box-shadow: var(--ha-card-box-shadow, none)
    - border-radius: var(--ha-card-border-radius, 12px)
    - border: |
        [[[
          let level = entity ? parseFloat(entity.state) || 0 : 0;
          let rgb = level <= 20 ? "150, 29, 29" : "29, 130, 150";
          return `1px solid rgba(${rgb}, 0.3)`;
        ]]]
  grid:
    - grid-template-areas: '"i" "s" "n"'
    - grid-template-columns: 1fr
    - grid-template-rows: min-content min-content min-content
    - height: 100%
    - align-content: center
    - justify-content: center
    - gap: '[[[ return (variables.circle_size * 0.02) + ''px'' ]]]'
  icon:
    - color: white
    - width: '[[[ return (variables.circle_size * 0.35) + ''px'' ]]]'
    - justify-self: center
    - filter: drop-shadow(0px 1px 3px rgba(0,0,0,0.8))
    - position: relative
    - z-index: 3
  state:
    - color: white
    - font-size: '[[[ return (variables.circle_size * 0.15) + ''px'' ]]]'
    - font-weight: bold
    - justify-self: center
    - text-shadow: 0px 1px 3px rgba(0,0,0,0.8)
    - position: relative
    - z-index: 3
  name:
    - color: white
    - font-size: '[[[ return (variables.circle_size * 0.10) + ''px'' ]]]'
    - justify-self: center
    - text-shadow: 0px 1px 3px rgba(0,0,0,0.8)
    - position: relative
    - z-index: 3
  custom_fields:
    glass_circle:
      - position: absolute
      - top: 50%
      - left: 50%
      - transform: translate(-50%, -50%)
      - width: '[[[ return variables.circle_size + ''px'' ]]]'
      - height: '[[[ return variables.circle_size + ''px'' ]]]'
      - border-radius: 50%
      - background: rgba(0, 0, 0, 0.25)
      - backdrop-filter: blur(6px)
      - -webkit-backdrop-filter: blur(6px)
      - border: 1px solid rgba(255, 255, 255, 0.15)
      - box-shadow: 0 4px 15px rgba(0,0,0,0.3)
      - z-index: 2
    back_wave:
      - position: absolute
      - inset: 0
      - z-index: 1
      - pointer-events: none
      - display: |-
          [[[ 
            let level = entity ? parseFloat(entity.state) || 0 : 0;
            return level <= 0 ? "none" : "block"; 
          ]]]
    front_wave:
      - position: absolute
      - inset: 0
      - z-index: 1
      - pointer-events: none
      - display: |-
          [[[ 
            let level = entity ? parseFloat(entity.state) || 0 : 0;
            return level <= 0 ? "none" : "block"; 
          ]]]
custom_fields:
  glass_circle: |
    [[[ return ``; ]]]
  back_wave: |
    [[[
      let level = entity ? parseFloat(entity.state) || 0 : 0;
      let rgb = level <= 20 ? "150, 29, 29" : "29, 130, 150";
      let color = `rgba(${rgb}, 0.6)`;
      
      /* Draw SVG path */
      let path = "M0 7.5 Q30 0 60 7.5 T120 7.5 L120 15 L0 15 Z";
      let svg = `<svg viewBox="0 0 120 15" style="width:120px; height:15px; display:block; flex-shrink:0;"><path d="${path}" fill="${color}"/></svg>`;
      
      /* Repeat the SVG 10 times */
      let wave_row = svg.repeat(10); 

      return `
        <div style="position:absolute; bottom:0; width:100%; height:calc(${level}% + 5px);">
          <div style="position:absolute; top:0; left:0; display:flex; animation:scroll-right 4s linear infinite;">
            ${wave_row}
          </div>
          <div style="position:absolute; top:14px; bottom:0; left:0; width:100%; background:${color};"></div>
        </div>
      `;
    ]]]
  front_wave: |
    [[[
      let level = entity ? parseFloat(entity.state) || 0 : 0;
      let rgb = level <= 20 ? "150, 29, 29" : "29, 130, 150";
      let color = `rgba(${rgb}, 1)`;
      
      /* Draw SVG path */
      let path = "M0 7.5 Q30 0 60 7.5 T120 7.5 L120 15 L0 15 Z";
      let svg = `<svg viewBox="0 0 120 15" style="width:120px; height:15px; display:block; flex-shrink:0;"><path d="${path}" fill="${color}"/></svg>`;

      /* Repeat the SVG 10 times */
      let wave_row = svg.repeat(10); 

      return `
        <div style="position:absolute; bottom:0; width:100%; height:${level}%;">
          <div style="position:absolute; top:0; left:0; display:flex; animation:scroll-left 3s linear infinite;">
            ${wave_row}
          </div>
          <div style="position:absolute; top:14px; bottom:0; left:0; width:100%; background:${color};"></div>
        </div>
      `;
    ]]]
extra_styles: |
  @keyframes scroll-left {
    0% { transform: translateX(0); }
    100% { transform: translateX(-120px); }
  }
  @keyframes scroll-right {
    0% { transform: translateX(-120px); }
    100% { transform: translateX(0); }
  }

```
</details>

<details>
<summary><strong>Liquid card (Fuel) </summary>

```yaml
type: custom:button-card
entity: sensor.fuel_tank_level
name: Fuel Tank
show_icon: true
show_name: true
show_state: true
icon: mdi:barrel
variables:
  card_h: 150
  circle_size: 100
styles:
  card:
    - height: '[[[ return variables.card_h + ''px'' ]]]'
    - position: relative
    - overflow: hidden
    - background: transparent
    - box-shadow: var(--ha-card-box-shadow, none)
    - border-radius: var(--ha-card-border-radius, 12px)
    - border: |
        [[[
          let level = entity ? parseFloat(entity.state) || 0 : 0;
          let rgb = level <= 20 ? "211, 47, 47" : "245, 124, 0";
          return `1px solid rgba(${rgb}, 0.3)`;
        ]]]
  grid:
    - grid-template-areas: '"i" "s" "n"'
    - grid-template-columns: 1fr
    - grid-template-rows: min-content min-content min-content
    - height: 100%
    - align-content: center
    - justify-content: center
    - gap: '[[[ return (variables.circle_size * 0.02) + ''px'' ]]]'
  icon:
    - color: white
    - width: '[[[ return (variables.circle_size * 0.35) + ''px'' ]]]'
    - justify-self: center
    - filter: drop-shadow(0px 1px 3px rgba(0,0,0,0.8))
    - position: relative
    - z-index: 3
  state:
    - color: white
    - font-size: '[[[ return (variables.circle_size * 0.15) + ''px'' ]]]'
    - font-weight: bold
    - justify-self: center
    - text-shadow: 0px 1px 3px rgba(0,0,0,0.8)
    - position: relative
    - z-index: 3
  name:
    - color: white
    - font-size: '[[[ return (variables.circle_size * 0.10) + ''px'' ]]]'
    - justify-self: center
    - text-shadow: 0px 1px 3px rgba(0,0,0,0.8)
    - position: relative
    - z-index: 3
  custom_fields:
    glass_circle:
      - position: absolute
      - top: 50%
      - left: 50%
      - transform: translate(-50%, -50%)
      - width: '[[[ return variables.circle_size + ''px'' ]]]'
      - height: '[[[ return variables.circle_size + ''px'' ]]]'
      - border-radius: 50%
      - background: rgba(0, 0, 0, 0.25)
      - backdrop-filter: blur(6px)
      - -webkit-backdrop-filter: blur(6px)
      - border: 1px solid rgba(255, 255, 255, 0.15)
      - box-shadow: 0 4px 15px rgba(0,0,0,0.3)
      - z-index: 2
    back_wave:
      - position: absolute
      - inset: 0
      - z-index: 1
      - pointer-events: none
      - display: >-
          [[[ return ((entity ? parseFloat(entity.state) || 0 : 0) <= 0) ?
          "none" : "block"; ]]]
    front_wave:
      - position: absolute
      - inset: 0
      - z-index: 1
      - pointer-events: none
      - display: >-
          [[[ return ((entity ? parseFloat(entity.state) || 0 : 0) <= 0) ?
          "none" : "block"; ]]]
custom_fields:
  glass_circle: |
    [[[ return ``; ]]]
  back_wave: |
    [[[
      let level = entity ? parseFloat(entity.state) || 0 : 0;
      let rgb = level <= 20 ? "211, 47, 47" : "245, 124, 0";
      let color = `rgba(${rgb}, 0.6)`;
      
      /* Draw SVG path */
      let path = "M0 7.5 Q30 0 60 7.5 T120 7.5 L120 15 L0 15 Z";
      let svg = `<svg viewBox="0 0 120 15" style="width:120px; height:15px; display:block; flex-shrink:0;"><path d="${path}" fill="${color}"/></svg>`;
      
      /* Repeat the SVG 10 times */
      let wave_row = svg.repeat(10); 

      return `
        <div style="position:absolute; bottom:0; width:100%; height:calc(${level}% + 5px);">
          <div style="position:absolute; top:0; left:0; display:flex; animation:scroll-right 5s linear infinite;">
            ${wave_row}
          </div>
          <div style="position:absolute; top:14px; bottom:0; left:0; width:100%; background:${color};"></div>
        </div>
      `;
    ]]]
  front_wave: |
    [[[
      let level = entity ? parseFloat(entity.state) || 0 : 0;
      let rgb = level <= 20 ? "211, 47, 47" : "245, 124, 0";
      let color = `rgba(${rgb}, 1)`;
      
      /* Draw SVG path */
      let path = "M0 7.5 Q30 0 60 7.5 T120 7.5 L120 15 L0 15 Z";
      let svg = `<svg viewBox="0 0 120 15" style="width:120px; height:15px; display:block; flex-shrink:0;"><path d="${path}" fill="${color}"/></svg>`;

      /* Repeat the SVG 10 times */
      let wave_row = svg.repeat(10); 

      return `
        <div style="position:absolute; bottom:0; width:100%; height:${level}%;">
          <div style="position:absolute; top:0; left:0; display:flex; animation:scroll-left 4s linear infinite;">
            ${wave_row}
          </div>
          <div style="position:absolute; top:14px; bottom:0; left:0; width:100%; background:${color};"></div>
        </div>
      `;
    ]]]
extra_styles: |
  @keyframes scroll-left {
    0% { transform: translateX(0); }
    100% { transform: translateX(-120px); }
  }
  @keyframes scroll-right {
    0% { transform: translateX(-120px); }
    100% { transform: translateX(0); }
  }

```
</details>

<details>
<summary><strong>Liquid card (Battery/percentage) </summary>

```yaml
type: custom:button-card
entity: sensor.anasbox_battery_level
name: Battery
show_icon: true
show_name: true
show_state: true
variables:
  card_h: 150
  circle_size: 110
  threshold_red: 20
  threshold_orange: 50
  threshold_green: 100
  charger_entity: binary_sensor.anasbox_is_charging
icon: |
  [[[
    if (entity && entity.attributes && entity.attributes.icon) return entity.attributes.icon;
    let level = entity && entity.state && !isNaN(entity.state) ? parseFloat(entity.state) : 0;
    let charger = variables.charger_entity && states[variables.charger_entity] ? states[variables.charger_entity] : null;
    let is_charging = charger ? ['on', 'charging', 'plugged'].includes(charger.state.toLowerCase()) : false;
    let rounded = Math.round(level / 10) * 10;
    if (is_charging) {
      if (rounded === 0) return "mdi:battery-charging-outline";
      return `mdi:battery-charging-${rounded}`;
    }
    if (rounded === 100) return "mdi:battery";
    if (rounded === 0) return "mdi:battery-outline";
    return `mdi:battery-${rounded}`;
  ]]]
styles:
  card:
    - height: '[[[ return variables.card_h + ''px'' ]]]'
    - position: relative
    - overflow: hidden
    - background: transparent
    - box-shadow: var(--ha-card-box-shadow, none)
    - border-radius: var(--ha-card-border-radius, 12px)
    - border: |
        [[[
          let level = entity && entity.state && !isNaN(entity.state) ? parseFloat(entity.state) : 0;
          let is_charging = variables.charger_entity && states[variables.charger_entity] ? ['on', 'charging', 'plugged'].includes(states[variables.charger_entity].state.toLowerCase()) : false;
          let rgb = "0, 255, 100";
          if (is_charging) rgb = "0, 255, 255";
          else if (level <= variables.threshold_red) rgb = "244, 67, 54";
          else if (level <= variables.threshold_orange) rgb = "255, 152, 0";
          return `1px solid rgba(${rgb}, 0.3)`;
        ]]]
  grid:
    - grid-template-areas: '"i" "s" "n"'
    - grid-template-columns: 1fr
    - grid-template-rows: min-content min-content min-content
    - height: 100%
    - align-content: center
    - justify-content: center
    - gap: '[[[ return (variables.circle_size * 0.02) + ''px'' ]]]'
  icon:
    - color: white
    - width: '[[[ return (variables.circle_size * 0.35) + ''px'' ]]]'
    - justify-self: center
    - filter: drop-shadow(0px 1px 3px rgba(0,0,0,0.8))
    - position: relative
    - z-index: 3
  state:
    - color: white
    - font-size: '[[[ return (variables.circle_size * 0.15) + ''px'' ]]]'
    - font-weight: bold
    - justify-self: center
    - text-shadow: 0px 1px 3px rgba(0,0,0,0.8)
    - position: relative
    - z-index: 3
  name:
    - color: white
    - font-size: '[[[ return (variables.circle_size * 0.10) + ''px'' ]]]'
    - justify-self: center
    - text-shadow: 0px 1px 3px rgba(0,0,0,0.8)
    - position: relative
    - z-index: 3
  custom_fields:
    glass_circle:
      - position: absolute
      - top: 50%
      - left: 50%
      - transform: translate(-50%, -50%)
      - width: '[[[ return variables.circle_size + ''px'' ]]]'
      - height: '[[[ return variables.circle_size + ''px'' ]]]'
      - border-radius: 50%
      - background: rgba(0, 0, 0, 0.25)
      - backdrop-filter: blur(6px)
      - -webkit-backdrop-filter: blur(6px)
      - border: 1px solid rgba(255, 255, 255, 0.15)
      - box-shadow: 0 4px 15px rgba(0,0,0,0.3)
      - z-index: 2
    back_wave:
      - position: absolute
      - inset: 0
      - z-index: 1
      - pointer-events: none
    front_wave:
      - position: absolute
      - inset: 0
      - z-index: 1
      - pointer-events: none
custom_fields:
  glass_circle: |
    [[[ return ``; ]]]
  back_wave: |
    [[[
      let level = entity && entity.state && !isNaN(entity.state) ? parseFloat(entity.state) : 0;
      let display_level = Math.max(level, 5);
      let is_charging = variables.charger_entity && states[variables.charger_entity] ? ['on', 'charging', 'plugged'].includes(states[variables.charger_entity].state.toLowerCase()) : false;
      let rgb = "46, 204, 113";
      if (is_charging) rgb = "52, 152, 219";
      else if (level <= variables.threshold_red) rgb = "231, 76, 60";
      else if (level <= variables.threshold_orange) rgb = "243, 156, 18";
      let color = `rgba(${rgb}, 0.6)`;
      let speed = is_charging ? "2s" : "4s";
      let path = "M0 7.5 Q30 0 60 7.5 T120 7.5 L120 15 L0 15 Z";
      let svg = `<svg viewBox="0 0 120 15" style="width:120px; height:15px; display:block; flex-shrink:0;"><path d="${path}" fill="${color}"/></svg>`;
      let wave_row = svg.repeat(10); 
      return `
        <div style="position:absolute; bottom:0; width:100%; height:calc(${display_level}% + 5px);">
          <div style="position:absolute; top:0; left:0; display:flex; animation:scroll-right ${speed} linear infinite;">
            ${wave_row}
          </div>
          <div style="position:absolute; top:14px; bottom:0; left:0; width:100%; background:${color};"></div>
        </div>
      `;
    ]]]
  front_wave: |
    [[[
      let level = entity && entity.state && !isNaN(entity.state) ? parseFloat(entity.state) : 0;
      let display_level = Math.max(level, 5);
      let is_charging = variables.charger_entity && states[variables.charger_entity] ? ['on', 'charging', 'plugged'].includes(states[variables.charger_entity].state.toLowerCase()) : false;
      let rgb = "46, 204, 113";
      if (is_charging) rgb = "52, 152, 219";
      else if (level <= variables.threshold_red) rgb = "231, 76, 60";
      else if (level <= variables.threshold_orange) rgb = "243, 156, 18";
      let color = `rgba(${rgb}, 1)`;
      let speed = is_charging ? "1.5s" : "3s";
      let path = "M0 7.5 Q30 0 60 7.5 T120 7.5 L120 15 L0 15 Z";
      let svg = `<svg viewBox="0 0 120 15" style="width:120px; height:15px; display:block; flex-shrink:0;"><path d="${path}" fill="${color}"/></svg>`;
      let wave_row = svg.repeat(10); 
      return `
        <div style="position:absolute; bottom:0; width:100%; height:${display_level}%;">
          <div style="position:absolute; top:0; left:0; display:flex; animation:scroll-left ${speed} linear infinite;">
            ${wave_row}
          </div>
          <div style="position:absolute; top:14px; bottom:0; left:0; width:100%; background:${color};"></div>
        </div>
      `;
    ]]]
extra_styles: |
  @keyframes scroll-left {
    0% { transform: translateX(0); }
    100% { transform: translateX(-120px); }
  }
  @keyframes scroll-right {
    0% { transform: translateX(-120px); }
    100% { transform: translateX(0); }
  }

```
</details>

<hr>

<img width="495" height="136" alt="665270619-e1f31ec9-da72-4c9f-bdfc-ed20abf2d10c" src="https://github.com/user-attachments/assets/2cf9b0b7-00d1-4014-a020-08afa5f2126f" />

<details>
<summary><strong>Mushroom light card with color temps quick toggles</summary>

<br>

>* after pasting this card, use the Find & Replace ALL feature in the card editor (CTRL+F) and Replace `light.CHANGE_ME` with your light entity, to change it everywhere at once.

```yaml
type: custom:vertical-stack-in-card
cards:
  - type: custom:mushroom-light-card
    entity: light.CHANGE_ME
    name: Light Card Name
    icon: mdi:led-strip-variant
    show_brightness_control: true
    show_color_control: true
    show_color_temp_control: true
    use_light_color: true
    card_mod:
      style:
        mushroom-light-brightness-control$:
          mushroom-slider$: |
            .slider {
              background: rgba(255, 255, 255, 0.05) !important;
            }
            .slider-track-active {
              box-shadow: inset 0 2px 4px rgba(0,0,0,0.15) !important;
            }
        .: |
          ha-card {
            background: none !important;
            border: none !important;
            box-shadow: none !important;
            
            padding-top: 10px !important;
            padding-bottom: 10px !important; 
            
            --control-height: 38px;
            --control-border-radius: 19px; 
          }
          mushroom-state-info {
            max-width: calc(100% - 140px) !important; 
          }
  - type: custom:mushroom-chips-card
    alignment: end
    card_mod:
      style: |
        ha-card {
          position: absolute;
          top: 10px;
          right: 10px;
          background: none !important;
          border: none !important;
          box-shadow: none !important;
          
          width: max-content;
          pointer-events: none;
          z-index: 10;
          
          --chip-background: rgba(255, 255, 255, 0.05);
          --chip-box-shadow: none;
          --chip-border-width: 0px;
          --chip-spacing: 6px;
          --chip-padding: 0 10px;
          --chip-height: 38px;
          --chip-icon-size: 20px;
        }
        mushroom-template-chip {
          pointer-events: auto;
        }
    chips:
      - type: template
        entity: light.CHANGE_ME
        icon: mdi:weather-sunset
        icon_color: >-
          {% set temp = state_attr(entity, 'color_temp_kelvin') %}

          {% set mode = state_attr(entity, 'color_mode') %}

          {{ 'orange' if is_state(entity, 'on') and mode == 'color_temp' and
          temp != None and temp <= 3200 else 'disabled' }}
        tap_action:
          action: call-service
          service: light.turn_on
          target:
            entity_id: light.CHANGE_ME
          data:
            color_temp_kelvin: 2702
      - type: template
        entity: light.CHANGE_ME
        icon: mdi:white-balance-sunny
        icon_color: >-
          {% set temp = state_attr(entity, 'color_temp_kelvin') %}

          {% set mode = state_attr(entity, 'color_mode') %}

          {{ 'amber' if is_state(entity, 'on') and mode == 'color_temp' and temp
          != None and 3200 < temp < 5000 else 'disabled' }}
        tap_action:
          action: call-service
          service: light.turn_on
          target:
            entity_id: light.CHANGE_ME
          data:
            color_temp_kelvin: 4000
      - type: template
        entity: light.CHANGE_ME
        icon: mdi:snowflake
        icon_color: >-
          {% set temp = state_attr(entity, 'color_temp_kelvin') %}

          {% set mode = state_attr(entity, 'color_mode') %}

          {{ 'light-blue' if is_state(entity, 'on') and mode == 'color_temp' and
          temp != None and temp >= 5000 else 'disabled' }}
        tap_action:
          action: call-service
          service: light.turn_on
          target:
            entity_id: light.CHANGE_ME
          data:
            color_temp_kelvin: 6535
card_mod:
  style: |
    ha-card {
      position: relative;
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
