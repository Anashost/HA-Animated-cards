
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

# Home Assistant Animated Climate Collection

># $${\color{#FF0000}Attention!!}$$
>
>Weather Card V2 available [HERE](https://www.patreon.com/AnasBox/posts/weather-card-v2-164637169)
>
>Whats new:
>- 7 Day forecast
>- hourly forecast
>- many new sensors
>- translation support
>- time and date
>- general improvements

<hr>

## Weather Card

<p align="center">
  <img
    width="500"
    alt="ezgif-5b0eb292c9c97807"
    src="https://github.com/user-attachments/assets/c5346148-d37b-4174-82b1-ba9fcacedef3"
  />
</p>

This [YouTube Video](https://youtu.be/xj5jhU1QD48) explains how to do it.

<hr>

<details>
<summary><strong>Animated Weather Card</summary>

```yaml
type: custom:button-card
variables:
  weather_entity: 
  temp_entity: 
  feels_like_entity: 
  cond_entity: 
  hum_entity: 
  wind_entity: 
  wind_gust_entity: 
  rain_entity: 
  sun_entity: sun.sun
  cond_clear: sunny, sun
  cond_clear_night: clear-night, clear night
  cond_cloudy: cloudy, cloud, mostly cloudy, overcast
  cond_partlycloudy: partlycloudy, partly-cloudy
  cond_rainy: rainy, rain, drizzle, pouring, showers
  cond_snowy: snowy, snow, sleet
  cond_storm: storm, thunderstorm, lightning
  cond_fog: fog, mist, hazy
  temptrend_show: true
  temptrend_entity: sensor.temptrend_24h
tap_action:
  action: none
show_name: false
show_icon: false
show_state: false
styles:
  card:
    - padding: 0
    - border-radius: 20px
    - box-shadow: 0 12px 30px -10px rgba(0,0,0,0.3), inset 0 1px 1px rgba(255,255,255,0.2)
    - border: none
    - color: white
    - font-family: >-
        -apple-system, BlinkMacSystemFont, "SF Pro Display", "Roboto",
        sans-serif
    - overflow: hidden
    - position: relative
    - background: "#1e293b"
    - isolation: isolate
  grid:
    - grid-template-areas: "\"content\""
    - grid-template-columns: 1fr
    - grid-template-rows: 1fr
  custom_fields:
    content:
      - pointer-events: auto !important
      - z-index: 99 !important
extra_styles: >
  .bg-container { position:absolute; inset:0; z-index:0; width:100%;
  height:100%; transition:background 1.2s ease-in-out; }

  .effect-layer { position:absolute; inset:0; width:100%; height:100%;
  pointer-events:none; z-index:1; overflow:hidden; }

  @keyframes rain-fall { from { background-position:0 -200px; } to {
  background-position:0 0; } }

  @keyframes snowflakes-sliding { 0% { background-position:0% 0%; } 100% {
  background-position:0% 100%; } }

  @keyframes celestial-breathe { 0% { transform:scale(0.96); opacity:0.95; }
  100% { transform:scale(1.04); opacity:1; } }

  @keyframes aura-pulse { 0% { transform:scale(1); opacity:0.3; } 100% {
  transform:scale(1.4); opacity:0.6; } }

  @keyframes cloud-drift-1 { 0% { transform:translateX(450px); opacity:0; } 15%
  { opacity:0.9; } 75% { transform:translateX(180px); opacity:0.9; } 100% {
  transform:translateX(110px); opacity:0; } }

  @keyframes cloud-drift-2 { 0% { transform:translateX(400px); opacity:0; } 20%
  { opacity:0.5; } 70% { transform:translateX(200px); opacity:0.5; } 100% {
  transform:translateX(130px); opacity:0; } }

  @keyframes fog-drift { 0% { transform:translateX(-50%) skewX(-15deg); } 100% {
  transform:translateX(0%) skewX(-15deg); } }

  @keyframes storm-strike { 0%,21%,23%,56%,81%,100% { opacity:0; } 20% {
  opacity:1; top:10%; left:10%; transform:scale(1) rotate(-10deg);
  filter:brightness(2); } 22% { opacity:0.5; top:10%; left:10%;
  transform:scale(1); } 55% { opacity:1; top:10%; left:40%; transform:scale(1.5)
  rotate(0deg); } 80% { opacity:1; top:30%; left:70%; transform:scale(0.8)
  rotate(10deg); } }

  @keyframes room-flash { 0%,21%,23%,56%,81%,100% { opacity:0; } 20% {
  opacity:0.4; } 22% { opacity:0.1; } 55% { opacity:0.6; } 80% { opacity:0.3; }
  }

  @keyframes shine { 0%,85%,100% { opacity:0.2; transform:scale(1);
  box-shadow:none; } 92% { opacity:1; transform:scale(1.4); box-shadow:0 0 5px
  1px rgba(255,255,255,0.9); } }

  .celestial-shared { position:absolute; border-radius:50%; }

  .sun-core-day { width:100px; height:100px; top:-20px; right:-20px;
  background:radial-gradient(circle,#fff9c4 0%,#ffca28 60%,#ff8f00 100%);
  box-shadow:0 0 40px rgba(255,193,7,0.8); animation:celestial-breathe 5s
  infinite alternate ease-in-out; }

  .sun-aura-day { width:160px; height:160px; top:-50px; right:-50px;
  background:radial-gradient(circle,rgba(255,213,79,0.6) 0%,transparent 70%);
  filter:blur(10px); animation:aura-pulse 6s infinite alternate ease-in-out; }

  .sun-core-twilight { width:100px; height:100px; top:-10px; right:-10px;
  background:radial-gradient(circle,#fff3e0 0%,#ffcc80 60%,#ffb74d 100%);
  box-shadow:0 0 50px rgba(255,183,77,0.7); animation:celestial-breathe 6s
  infinite alternate ease-in-out; }

  .sun-aura-twilight { width:160px; height:160px; top:-40px; right:-40px;
  background:radial-gradient(circle,rgba(255,183,77,0.5) 0%,transparent 70%);
  filter:blur(12px); animation:aura-pulse 7s infinite alternate ease-in-out; }

  .moon-core-night { width:90px; height:90px; top:-15px; right:-15px;
  background:radial-gradient(circle,#ffffff 0%,#e0e5db 50%,#9ca3af 100%);
  box-shadow:0 0 30px rgba(200,220,255,0.6), inset -10px -10px 20px
  rgba(0,0,0,0.3); animation:celestial-breathe 6s infinite alternate
  ease-in-out; }

  .moon-aura-night { width:150px; height:150px; top:-45px; right:-45px;
  background:radial-gradient(circle,rgba(200,220,255,0.3) 0%,transparent 70%);
  filter:blur(10px); animation:aura-pulse 8s infinite alternate ease-in-out; }

  .stars { position:absolute; inset:0; overflow:hidden; pointer-events:none; }

  .star-layer { position:absolute; width:1.5px; height:1.5px;
  background:transparent; border-radius:50%; box-shadow:12px 45px
  rgba(255,255,255,0.8),88px 12px rgba(255,255,255,0.5),145px 80px #fff,210px
  25px rgba(255,255,255,0.6),280px 95px rgba(255,255,255,0.9),340px 15px
  rgba(255,255,255,0.4),415px 70px #fff,490px 30px rgba(255,255,255,0.7),560px
  110px rgba(255,255,255,0.8),65px 120px rgba(255,255,255,0.5),180px 135px
  #fff,310px 50px rgba(255,255,255,0.6),450px 140px rgba(255,255,255,0.9); }

  .star-layer::after { content:''; position:absolute; width:1px; height:1px;
  background:transparent; border-radius:50%; box-shadow:35px 20px
  rgba(255,255,255,0.7),105px 65px rgba(255,255,255,0.9),160px 15px
  rgba(255,255,255,0.4),235px 115px #fff,295px 35px rgba(255,255,255,0.8),370px
  125px rgba(255,255,255,0.5),425px 45px rgba(255,255,255,0.6),485px 95px
  #fff,530px 15px rgba(255,255,255,0.9),80px 100px rgba(255,255,255,0.4),195px
  60px rgba(255,255,255,0.7),260px 130px #fff,390px 85px
  rgba(255,255,255,0.5),510px 125px rgba(255,255,255,0.8); }

  .t-star { position:absolute; width:1.5px; height:1.5px; background:white;
  border-radius:50%; opacity:0.2; }

  .ts-1 { top:18%; left:22%; animation:shine 4.2s infinite; }

  .ts-2 { top:35%; left:68%; animation:shine 5.5s infinite 1.8s; }

  .ts-3 { top:12%; left:48%; animation:shine 3.6s infinite 2.5s; }

  .css-cloud { position:absolute; background:rgba(255,255,255,0.8);
  border-radius:50px; filter:drop-shadow(0 8px 16px rgba(0,0,0,0.15)); }

  .css-cloud::before, .css-cloud::after { content:''; position:absolute;
  background:inherit; border-radius:50%; }

  .cloud-twilight { background:rgba(255,220,210,0.85); filter:drop-shadow(0 8px
  16px rgba(100,0,0,0.1)); }

  .cloud-night { background:rgba(200,210,225,0.4); filter:drop-shadow(0 5px 10px
  rgba(0,0,0,0.4)); }

  .cloud-shape-1 { width:140px; height:45px; top:40px; animation:cloud-drift-1
  16s linear infinite; z-index:2; }

  .cloud-shape-1::before { width:70px; height:70px; top:-35px; left:25px; }

  .cloud-shape-1::after { width:50px; height:50px; top:-20px; right:20px; }

  .cloud-shape-2 { width:105px; height:34px; top:65px; animation:cloud-drift-2
  22s linear infinite -10s; z-index:1; }

  .cloud-shape-2::before { width:52px; height:52px; top:-26px; left:19px; }

  .cloud-shape-2::after { width:37px; height:37px; top:-15px; right:15px; }

  .rain-1 { background-image:radial-gradient(ellipse at 30px
  20px,rgba(255,255,255,0.6) 1px,transparent 3px),radial-gradient(ellipse at
  80px 100px,rgba(255,255,255,0.6) 1px,transparent 3px),radial-gradient(ellipse
  at 150px 60px,rgba(255,255,255,0.6) 1px,transparent
  3px),radial-gradient(ellipse at 250px 150px,rgba(255,255,255,0.6)
  1px,transparent 3px); background-size:300px 200px; animation:rain-fall 0.6s
  linear infinite; opacity:0.8; }

  .rain-2 { background-image:radial-gradient(ellipse at 10px
  50px,rgba(255,255,255,0.4) 1px,transparent 2px),radial-gradient(ellipse at
  60px 120px,rgba(255,255,255,0.4) 1px,transparent 2px),radial-gradient(ellipse
  at 120px 30px,rgba(255,255,255,0.4) 1px,transparent
  2px),radial-gradient(ellipse at 200px 90px,rgba(255,255,255,0.4)
  1px,transparent 2px); background-size:300px 180px; animation:rain-fall 1.2s
  linear infinite; opacity:0.5; }

  .snow-1 { height:200%; background-image:radial-gradient(circle at 20%
  10%,rgba(255,255,255,0.4) 0%,transparent 6px),radial-gradient(circle at 80%
  30%,rgba(255,255,255,0.4) 0%,transparent 8px),radial-gradient(circle at 40%
  50%,rgba(255,255,255,0.4) 0%,transparent 6px),radial-gradient(circle at 70%
  75%,rgba(255,255,255,0.4) 0%,transparent 7px),radial-gradient(circle at 10%
  90%,rgba(255,255,255,0.4) 0%,transparent 5px),radial-gradient(circle at 60%
  15%,rgba(255,255,255,0.4) 0%,transparent 6px); background-size:100% 50%;
  animation:snowflakes-sliding 2s linear infinite; opacity:0.8; }

  .snow-2 { height:200%; background-image:radial-gradient(circle at 15%
  5%,rgba(255,255,255,0.3) 0%,transparent 4px),radial-gradient(circle at 55%
  25%,rgba(255,255,255,0.3) 0%,transparent 3px),radial-gradient(circle at 85%
  45%,rgba(255,255,255,0.3) 0%,transparent 4px),radial-gradient(circle at 25%
  65%,rgba(255,255,255,0.3) 0%,transparent 3px),radial-gradient(circle at 65%
  85%,rgba(255,255,255,0.3) 0%,transparent 4px); background-size:100% 50%;
  animation:snowflakes-sliding 1s linear infinite; opacity:0.6; }

  .fog-band { position:absolute; width:200%; height:40px;
  background:linear-gradient(to
  right,transparent,rgba(255,255,255,0.7),transparent); filter:blur(10px); }

  .fog-1 { top:40px; animation:fog-drift 18s linear infinite alternate; }

  .fog-2 { top:100px; opacity:0.6; animation:fog-drift 28s linear infinite
  alternate-reverse; width:250%; }

  .storm-flash { background:white; animation:room-flash 7s steps(1) infinite;
  mix-blend-mode:overlay; }

  .storm-bolt { width:80px; height:140px; background:#e0f2fe;
  clip-path:polygon(55% 0%,80% 0%,50% 45%,85% 45%,20% 100%,40% 55%,10% 55%);
  filter:drop-shadow(0 0 15px rgba(255,255,255,0.9)); animation:storm-strike 6s
  steps(1) infinite; }

  .card-content { position:relative; z-index:5; padding:12px 16px; display:flex;
  flex-direction:column; width:100%; box-sizing:border-box; }

  .top-row { display:flex; justify-content:space-between; align-items:center;
  width:100%; }

  .glass-metric { pointer-events:auto; display:flex; align-items:center;
  background:rgba(0,0,0,0.15); backdrop-filter:blur(20px) saturate(180%);
  -webkit-backdrop-filter:blur(20px) saturate(180%); border:1px solid
  rgba(255,255,255,0.2); border-radius:12px; padding:4px 8px; font-size:11px;
  font-weight:600; color:white; text-shadow:0 1px 2px rgba(0,0,0,0.4);
  box-shadow:0 2px 10px rgba(0,0,0,0.05); letter-spacing:0.2px;
  white-space:nowrap; transition:all 0.2s ease; cursor:pointer; }

  .glass-metric:hover, .glass-metric:active { background:rgba(0,0,0,0.25);
  transform:translateY(-1px); }

  .glass-metric ha-icon { opacity:0.9; width:14px; height:14px;
  margin-right:4px; filter:drop-shadow(0 1px 1px rgba(0,0,0,0.3)); }

  .hover-text-block { pointer-events:auto; display:inline-flex;
  align-items:center; cursor:pointer; border-radius:8px; padding:2px 6px;
  margin-left:-6px; transition:background 0.2s ease; }

  .hover-text-block:hover, .hover-text-block:active {
  background:rgba(255,255,255,0.15); }

  .temptrend-container { width:100%; margin-top:2px; padding-top:8px;
  border-top:0px solid rgba(255,255,255,0.1); }

  .temptrend-bar { width:100%; height:6px; border-radius:4px; opacity:0.9;
  box-shadow:inset 0 1px 2px rgba(0,0,0,0.4); }
custom_fields:
  content: |
    [[[
      const wE = variables.weather_entity, tE = variables.temp_entity, cE = variables.cond_entity;
      const wV = wE && states[wE], tV = tE && states[tE], cV = cE && states[cE];

      if (!wV && !tV && !cV) {
        return `
          <div style="display:flex;flex-direction:column;align-items:center;justify-content:center;
          padding:24px;text-align:center;box-sizing:border-box;width:100%;min-height:140px;
          border-radius:20px;background:#1e293b;">
            <ha-icon icon="mdi:cog" style="color:#38bdf8;width:36px;height:36px;
            margin-bottom:12px;filter:drop-shadow(0 2px 4px rgba(0,0,0,0.4));"></ha-icon>
            <span style="font-size:16px;font-weight:600;margin-bottom:6px;color:white;">
              Setup Required
            </span>
            <span style="font-size:12px;color:rgba(255,255,255,0.7);line-height:1.4;">
              Provide a valid <b>weather_entity</b>,<br>or both <b>temp_entity</b> and <b>cond_entity</b>.
            </span>
          </div>`;
      }

      const wS = wV ? states[wE].state : null;
      const tS = tV ? states[tE].state : null;
      const cS = cV ? states[cE].state : null;

      const clk = e => e ? `ontouchstart="this.sX=event.touches[0].clientX;this.sY=event.touches[0].clientY;" 
        ontouchend="if(Math.abs(event.changedTouches[0].clientX-this.sX)<15&&Math.abs(event.changedTouches[0].clientY-this.sY)<15)this.dispatchEvent(new CustomEvent('hass-more-info',{bubbles:true,composed:true,detail:{entityId:'${e}'}}));" 
        onclick="this.dispatchEvent(new CustomEvent('hass-more-info',{bubbles:true,composed:true,detail:{entityId:'${e}'}}));"` : '';

      const wTemp = v => `
        <span style="font-size:38px;font-weight:400;line-height:1;letter-spacing:-1px;
        text-shadow:0 1px 3px rgba(0,0,0,0.3);display:flex;align-items:center;">${v}</span>`;
        
      const wCond = v => `
        <span style="font-size:19px;font-weight:600;color:rgba(255,255,255,0.98);
        text-shadow:0 1px 3px rgba(0,0,0,0.3);letter-spacing:0.3px;">${v}</span>`;

      const tBdg = `
        <div style="display:flex;align-items:center;justify-content:center;
        background:rgba(239,68,68,0.15);padding:4px 12px;border-radius:12px;
        border:1px solid rgba(239,68,68,0.3);height:32px;box-sizing:border-box;">
          <ha-icon icon="mdi:thermometer-off" style="width:20px;height:20px;
          margin-right:6px;color:#fca5a5;display:block;"></ha-icon>
          <span style="font-size:20px;font-weight:600;color:#fca5a5;
          line-height:1;display:block;">-</span>
        </div>`;

      let tH = tBdg;
      if (tV) {
        if (tS === 'unavailable') tH = wTemp('-');
        else if (tS !== 'unknown') tH = wTemp(Math.round(tS) + '°');
      } else if (wV) {
        if (wS === 'unavailable') tH = wTemp('-');
        else if (states[wE].attributes?.temperature !== undefined) 
          tH = wTemp(Math.round(states[wE].attributes.temperature) + '°');
      }

      const cBdg = `
        <div style="display:flex;align-items:center;justify-content:center;
        background:rgba(239,68,68,0.15);padding:4px 10px;border-radius:10px;
        border:1px solid rgba(239,68,68,0.3);height:26px;box-sizing:border-box;">
          <ha-icon icon="mdi:cloud-question" style="width:16px;height:16px;
          margin-right:6px;color:#fca5a5;display:block;"></ha-icon>
          <span style="font-size:16px;font-weight:600;color:#fca5a5;
          line-height:1;display:block;">-</span>
        </div>`;

      let rC = '', cH = cBdg;
      if (cV) {
        if (cS === 'unavailable') cH = wCond('-');
        else if (cS !== 'unknown') rC = cS.toLowerCase();
      } else if (wV) {
        if (wS === 'unavailable') cH = wCond('-');
        else if (wS !== 'unknown') rC = wS.toLowerCase();
      }
      
      if (rC && !isNaN(Number(rC))) {
        rC = '';
        cH = cBdg;
      } else if (rC) {
        const fmtC = rC.replace(/[-_]/g, ' ').replace(/partlycloudy/gi, 'partly cloudy')
          .split(' ').map(s => s.charAt(0).toUpperCase() + s.slice(1)).join(' ');
        cH = wCond(fmtC);
      }

      const fE = variables.feels_like_entity, fV = fE && states[fE];
      const fS = fV ? states[fE].state : null;
      let fH = '';
      
      if (fV) {
        if (fS === 'unavailable') fH = `
          <div class="hover-text-block" style="margin-left:2px;">
            <span style="font-size:14px;font-weight:500;opacity:0.95;">Feels like -</span>
          </div>`;
        else if (fS !== 'unknown') fH = `
          <div class="hover-text-block" style="margin-left:2px;" ${clk(fE)}>
            <span style="font-size:14px;font-weight:500;opacity:0.95;">Feels like ${Math.round(fS)}°</span>
          </div>`;
      } else if (wV) {
        if (wS === 'unavailable') fH = `
          <div class="hover-text-block" style="margin-left:2px;">
            <span style="font-size:14px;font-weight:500;opacity:0.95;">Feels like -</span>
          </div>`;
        else if (states[wE].attributes?.apparent_temperature !== undefined) fH = `
          <div class="hover-text-block" style="margin-left:2px;" ${clk(wE)}>
            <span style="font-size:14px;font-weight:500;opacity:0.95;">
              Feels like ${Math.round(states[wE].attributes.apparent_temperature)}°
            </span>
          </div>`;
      }

      const bM = (e, a, uA, ic, p) => {
        const eV = e && states[e], eS = eV ? states[e].state : null;
        if (eV) {
          if (eS === 'unavailable') return `<div class="glass-metric"><ha-icon icon="${ic}"></ha-icon> -</div>`;
          if (eS !== 'unknown') {
            const u = p ? '%' : ' ' + (states[e].attributes?.unit_of_measurement || '');
            return `<div class="glass-metric" ${clk(e)}><ha-icon icon="${ic}"></ha-icon> ${Math.round(eS)}${u}</div>`;
          }
        } else if (wV) {
          if (wS === 'unavailable') return `<div class="glass-metric"><ha-icon icon="${ic}"></ha-icon> -</div>`;
          const val = states[wE].attributes?.[a];
          if (val !== undefined) {
            const u = p ? '%' : ' ' + (states[wE].attributes?.[uA] || '');
            return `<div class="glass-metric" ${clk(wE)}><ha-icon icon="${ic}"></ha-icon> ${Math.round(val)}${u}</div>`;
          }
        }
        return '';
      };

      const mL = [
        [variables.hum_entity, 'humidity', '', 'mdi:water-percent', true],
        [variables.wind_entity, 'wind_speed', 'wind_speed_unit', 'mdi:weather-windy', false],
        [variables.wind_gust_entity, 'wind_gust', 'wind_speed_unit', 'mdi:weather-windy-variant', false],
        [variables.rain_entity, 'precipitation', 'precipitation_unit', 'mdi:weather-pouring', false]
      ];
      const mH = mL.map(m => bM(...m)).join('');

      let cK = 'unknown';
      const cM = {
        'clear': variables.cond_clear, 'clear-night': variables.cond_clear_night,
        'cloudy': variables.cond_cloudy, 'partlycloudy': variables.cond_partlycloudy,
        'rainy': variables.cond_rainy, 'snowy': variables.cond_snowy,
        'storm': variables.cond_storm, 'fog': variables.cond_fog
      };
      
      if (rC) {
        for (const [k, v] of Object.entries(cM)) {
          if (v?.split(',').map(s => s.trim().toLowerCase()).includes(rC)) { cK = k; break; }
        }
      }

      let tD = 'day';
      const sE = variables.sun_entity, el = sE && states[sE]?.attributes?.elevation;
      if (el !== undefined) {
        tD = el < -4 ? 'night' : (el <= 10 ? (new Date().getHours() < 12 ? 'sunrise' : 'sunset') : 'day');
      } else if (cK.includes('night')) {
        tD = 'night';
      }

      if (tD !== 'night' && cK.includes('night')) cK = cK.replace('-night', '').replace('night', 'clear');
      else if (tD === 'night' && cK === 'sunny') cK = 'clear-night';

      const bG = {
        sunny: { day: ['#29b6f6', '#0288d1'], twilight: ['#7986cb', '#e1bee7', '#ffe0b2'], night: ['#080c16', '#162032'] },
        partly: { day: ['#4fc3f7', '#1976d2'], twilight: ['#5c6bc0', '#ce93d8', '#ffccbc'], night: ['#111827', '#1e293b'] },
        cloudy: { day: ['#607d8b', '#455a64'], twilight: ['#455a64', '#78909c', '#ffebee'], night: ['#1f2937', '#374151'] },
        rain: { day: ['#2c3e50', '#4ca1af'], twilight: ['#3949ab', '#7e57c2', '#ffe0b2'], night: ['#0f172a', '#1e293b'] },
        snow: { day: ['#94a3b8', '#64748b'], twilight: ['#8b5cf6', '#d8b4fe', '#94a3b8'], night: ['#1e293b', '#0f172a'] },
        storm: { day: ['#64748b', '#334155'], twilight: ['#2b285b', '#1e1b4b', '#0f172a'], night: ['#0f172a', '#1e293b'] },
        fog: { day: ['#9ca3af', '#6b7280'], twilight: ['#8b5cf6', '#c084fc', '#9ca3af'], night: ['#1f2937', '#111827'] },
        unknown: { day: ['#475569', '#334155'], twilight: ['#334155', '#1e293b', '#0f172a'], night: ['#0f172a', '#020617'] }
      };

      const sh = {
        rain: { day: 'inset 0 0 20px rgba(0,0,0,0.3)', night: 'inset 0 0 30px rgba(0,0,0,0.6)' },
        snow: { day: 'inset 0 0 50px rgba(200,220,255,0.2)', twilight: 'inset 0 0 30px rgba(200,220,255,0.2)', night: 'inset 0 0 40px rgba(200,220,255,0.1)' },
        storm: { day: 'inset 0 0 50px rgba(0,0,0,0.7)', twilight: 'inset 0 0 50px rgba(0,0,0,0.8)', night: 'inset 0 0 50px rgba(0,0,0,0.9)' }
      };

      let cat = 'sunny', eL = '';
      const sH = tD === 'night' ? `<div class="stars"><div class="star-layer"></div>
        <div class="t-star ts-1"></div><div class="t-star ts-2"></div><div class="t-star ts-3"></div></div>` : '';
      const cC = tD === 'night' ? 'cloud-night' : (tD !== 'day' ? 'cloud-twilight' : '');
      const sC = tD !== 'day' ? 'twilight' : 'day';

      if (cK === 'unknown') {
        cat = 'unknown';
      } else if (cK.includes('storm') || cK.includes('thunder')) {
        cat = 'storm'; 
        eL = `<div class="effect-layer storm-flash"></div><div class="effect-layer storm-bolt"></div>`;
      } else if (cK.includes('snow') || cK.includes('hail')) {
        cat = 'snow'; 
        eL = `<div class="effect-layer snow-1"></div><div class="effect-layer snow-2"></div>`;
      } else if (cK.includes('rain') || cK.includes('pour')) {
        cat = 'rain'; 
        eL = `<div class="effect-layer rain-1"></div><div class="effect-layer rain-2"></div>`;
      } else if (cK.includes('partly')) {
        cat = 'partly'; 
        eL = tD === 'night' 
          ? `${sH}<div class="effect-layer"><div class="moon-aura-night celestial-shared"></div>
             <div class="moon-core-night celestial-shared"></div><div class="css-cloud ${cC} cloud-shape-1"></div></div>` 
          : `<div class="effect-layer"><div class="sun-aura-${sC} celestial-shared"></div>
             <div class="sun-core-${sC} celestial-shared"></div><div class="css-cloud ${cC} cloud-shape-1"></div></div>`;
      } else if (cK.includes('cloud')) {
        cat = 'cloudy'; 
        eL = `${sH}<div class="effect-layer"><div class="css-cloud ${cC} cloud-shape-1"></div>
              <div class="css-cloud ${cC} cloud-shape-2"></div></div>`;
      } else if (cK.includes('fog')) {
        cat = 'fog'; 
        eL = `${sH}<div class="effect-layer"><div class="fog-band fog-1"></div><div class="fog-band fog-2"></div></div>`;
      } else {
        cat = 'sunny'; 
        eL = tD === 'night' 
          ? `${sH}<div class="effect-layer"><div class="moon-aura-night celestial-shared"></div>
             <div class="moon-core-night celestial-shared"></div></div>` 
          : `<div class="effect-layer"><div class="sun-aura-${sC} celestial-shared"></div>
             <div class="sun-core-${sC} celestial-shared"></div></div>`;
      }

      const tK = tD === 'night' ? 'night' : (tD !== 'day' ? 'twilight' : 'day');
      const aC = (bG[cat] || bG.sunny)[tK].join(', ');
      const aS = sh[cat]?.[tK] || 'none';
      const bgS = `background:linear-gradient(to bottom, ${aC});box-shadow:${aS};`;

      let trH = '';
      if (variables.temptrend_show && variables.temptrend_entity) {
        const trE = variables.temptrend_entity;
        const hs = states[trE]?.attributes?.history?.map(Number);
        
        if (hs?.length > 1) {
          const isF = (tV && states[tE].attributes?.unit_of_measurement?.includes('F')) || 
                      (wV && states[wE].attributes?.temperature_unit?.includes('F'));
          const minSp = isF ? 16.2 : 9;
          const mn = Math.min(...hs), mx = Math.max(...hs);
          let sp = mx - mn, bs = mn;
          
          if (sp < minSp) { bs = ((mx + mn) / 2) - (minSp / 2); sp = minSp; }
          
          const st = hs.map((t, i) => {
            const p = Math.max(0, Math.min(1, (t - bs) / (sp || 1)));
            const sg = Math.min(4, Math.floor(p * 5)), lP = (p * 5) - sg;
            let r = 0, g = 0, b = 0;
            
            if (sg === 0) { g = Math.round(50 + lP * 205); b = 255; }
            else if (sg === 1) { g = 255; b = Math.round(255 - lP * 255); }
            else if (sg === 2) { r = Math.round(lP * 255); g = 255; }
            else if (sg === 3) { r = 255; g = Math.round(255 - lP * 127); }
            else { r = 255; g = Math.round(128 - lP * 128); }
            
            return `rgb(${r},${g},${b}) ${(i / (hs.length - 1)) * 100}%`;
          });
          
          trH = `
            <div class="temptrend-container">
              <div class="temptrend-bar" style="background:linear-gradient(to right, ${st.join(', ')});"></div>
            </div>`;
        }
      }

      return `
        <div class="bg-container" style="${bgS}"></div>
        ${eL}
        <div class="card-content">
          <div class="top-row">
            <div style="display:flex;flex-direction:column;align-items:flex-start;width:100%;">
              <div style="display:flex;align-items:center;gap:6px;flex-wrap:wrap;">
                <div class="hover-text-block" style="display:flex;align-items:center;" ${clk(tE || wE)}>
                  ${tH}
                </div>
                ${fH}
              </div>
              <div class="hover-text-block" style="margin-top:4px;" ${clk(cE || wE)}>
                ${cH}
              </div>
              <div style="display:flex;gap:6px;margin-top:8px;flex-wrap:wrap;">
                ${mH}
              </div>
            </div>
          </div>
          ${trH}
        </div>
      `;
    ]]]

```
</details>

<details>
<summary><strong>Template</summary>


- Replace `sensor.openweathermap_temperature` with your own `weather.xx` or `sensor.xx temperature`, in both places.

```yaml
  - trigger:
      - platform: time_pattern
        minutes: "/1"
      - platform: homeassistant
        event: start
    condition: >
      {{ (now().timestamp() - state_attr('sensor.temptrend_24h', 'last_update') | default(0, true) | float(0)) >= 3600 }}
    sensor:
      - name: "Temptrend 24h"
        unique_id: temptrend_24h
        state: >
          {% set target = 'sensor.openweathermap_temperature' %}
          {{ (state_attr(target, 'temperature') if target.startswith('weather.') else states(target)) | float(0) | round(1) }}
        attributes:
          last_update: "{{ now().timestamp() }}"
          history: >
            {% set target = 'sensor.openweathermap_temperature' %}
            {% set current = (state_attr(target, 'temperature') if target.startswith('weather.') else states(target)) | float(0) | round(1) %}
            {% set past = state_attr('sensor.temptrend_24h', 'history') | default([current] * 24, true) %}
            {{ (past + [current])[-24:] }}
```
</details>

<hr>

> [!NOTE]
> More Climate Cards are coming soon. They're currently available to members for Testing, <a href="https://www.patreon.com/c/AnasBox" target="_blank" rel="noopener noreferrer">Patreon</a> and <a href="https://www.youtube.com/@anasbox/membership" target="_blank" rel="noopener noreferrer">YouTube</a>.

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
