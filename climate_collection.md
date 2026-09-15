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
YouTube [Video](https://youtu.be/B0pU4OLGWRQ)

<p align="center">
  <img width="420" alt="ezgif-5b0eb292c9c97807" src="https://github.com/user-attachments/assets/0624cc44-395a-4ffa-9edd-18fdf70f5aae" />
  <img width="820" alt="ezgif-735c7b50daf994d9" src="https://github.com/user-attachments/assets/18c3fc83-df9e-4e9b-943e-8791e18428f0" />
</p>


<hr>

<details>
<summary><strong>Animated Weather Card (V3)</summary>
  
<br>

- For instructions watch the V1 [video](https://youtu.be/xj5jhU1QD48) and the instructions [here](https://www.patreon.com/AnasBox/posts/weather-card-v3-164637169?utm_medium=clipboard_copy&utm_source=copyLink&utm_campaign=postshare_creator&utm_content=join_link) too.

<br>

```yaml
type: custom:button-card
variables:
  weather_entity: weather.openweathermap
  temp_entity: sensor.openweathermap_temperature
  feels_like_entity: sensor.openweathermap_feels_like_temperature
  cond_entity: sensor.openweathermap_condition
  hum_entity: sensor.openweathermap_humidity
  wind_entity: sensor.openweathermap_wind_speed
  wind_gust_entity: sensor.openweathermap_wind_gust
  rain_entity: sensor.openweathermap_rain_intensity
  pressure_entity: sensor.openweathermap_pressure
  sun_entity: sun.sun
  aqi_entity: sensor.amsterdam_aqi
  uv_entity: sensor.openweathermap_uv_index
  pollen_entity: sensor.pollen_grass_level
  fire_entity: sensor.fire_index
  time_show: true
  date_show: true
  time_format: 24
  time_entity: sensor.time
  cond_clear: sunny, sun
  cond_clear_night: clear-night, clear night
  cond_cloudy: cloudy, cloud, mostly cloudy, overcast
  cond_partlycloudy: partlycloudy, partly-cloudy, partly cloudy
  cond_rainy: rainy, rain, drizzle, pouring, showers
  cond_snowy: snowy, snow, sleet
  cond_storm: storm, thunderstorm, lightning
  cond_fog: fog, mist, hazy
  cond_windy: windy, breeze, windy-variant
  temptrend_show: true
  temptrend_entity: sensor.temptrend_24h
  forecast_hourly_show: true
  forecast_hourly_count: 6
  forecast_daily_show: true
  forecast_daily_count: 7
  forecast_hourly_entity: sensor.custom_weather_forecast_hourly
  forecast_daily_entity: sensor.custom_weather_forecast_daily
  translate_feels_like: ''
  translate_conditions:
    clear: ''
    clear-night: ''
    cloudy: ''
    partlycloudy: ''
    rainy: ''
    snowy: ''
    storm: ''
    fog: ''
    windy: ''
  translate_days:
    - SUN
    - MON
    - TUE
    - WED
    - THU
    - FRI
    - SAT
  size_temp: '40'
  size_cond: '30'
  size_badges: '10'
  size_date_time: '15'
  size_forecast: '12'
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
    - background: '#1e293b'
    - isolation: isolate
  grid:
    - grid-template-areas: '"content"'
    - grid-template-columns: 1fr
    - grid-template-rows: 1fr
  custom_fields:
    content:
      - pointer-events: auto !important
      - z-index: 99 !important
extra_styles: >
  .bg-container { position:absolute; inset:0; z-index:0; width:100%;
  height:100%; transition:background 1.2s ease-in-out; } .effect-layer {
  position:absolute; inset:0; width:100%; height:100%; pointer-events:none;
  z-index:1; overflow:hidden; }  @keyframes rain-fall-1 { 0% {
  background-position:0 -160px; } 100% { background-position:0 0; } } @keyframes
  rain-fall-2 { 0% { background-position:0 -120px; } 100% {
  background-position:0 0; } } @keyframes snowflakes-sliding { 0% {
  background-position:0% 0%; } 100% { background-position:0% 100%; } }
  @keyframes celestial-breathe { 0% { transform:scale(0.96); opacity:0.95; }
  100% { transform:scale(1.04); opacity:1; } } @keyframes aura-pulse { 0% {
  transform:scale(1); opacity:0.3; } 100% { transform:scale(1.4); opacity:0.6; }
  } @keyframes cloud-drift-1 { 0% { transform:translateX(450px); opacity:0; }
  15% { opacity:0.9; } 75% { transform:translateX(180px); opacity:0.9; } 100% {
  transform:translateX(110px); opacity:0; } } @keyframes cloud-drift-2 { 0% {
  transform:translateX(400px); opacity:0; } 20% { opacity:0.5; } 70% {
  transform:translateX(200px); opacity:0.5; } 100% {
  transform:translateX(130px); opacity:0; } } @keyframes fog-drift { 0% {
  transform:translateX(-50%) skewX(-15deg); } 100% { transform:translateX(0%)
  skewX(-15deg); } } @keyframes storm-strike { 0%,21%,23%,56%,81%,100% {
  opacity:0; } 20% { opacity:1; top:10%; left:10%; transform:scale(1)
  rotate(-10deg); filter:brightness(2); } 22% { opacity:0.5; top:10%; left:10%;
  transform:scale(1); } 55% { opacity:1; top:10%; left:40%; transform:scale(1.5)
  rotate(0deg); } 80% { opacity:1; top:30%; left:70%; transform:scale(0.8)
  rotate(10deg); } } @keyframes room-flash { 0%,21%,23%,56%,81%,100% {
  opacity:0; } 20% { opacity:0.4; } 22% { opacity:0.1; } 55% { opacity:0.6; }
  80% { opacity:0.3; } } @keyframes shine { 0%,85%,100% { opacity:0.2;
  transform:scale(1); box-shadow:none; } 92% { opacity:1; transform:scale(1.4);
  box-shadow:0 0 5px 1px rgba(255,255,255,0.9); } } @keyframes wind-rush { 0% { 
  transform:translateX(450px); opacity:0; } 10% { opacity:1; } 90% { opacity:1;
  } 100% {  transform:translateX(-250px); opacity:0; } } .celestial-shared {
  position:absolute; border-radius:50%; } .sun-core-day { width:100px;
  height:100px; top:-20px; right:-20px;
  background:radial-gradient(circle,#fff9c4 0%,#ffca28 60%,#ff8f00 100%);
  box-shadow:0 0 40px rgba(255,193,7,0.8); animation:celestial-breathe 5s
  infinite alternate ease-in-out; } .sun-aura-day { width:160px; height:160px;
  top:-50px; right:-50px; background:radial-gradient(circle,rgba(255,213,79,0.6)
  0%,transparent 70%); filter:blur(10px); animation:aura-pulse 6s infinite
  alternate ease-in-out; } .sun-core-twilight { width:100px; height:100px;
  top:-10px; right:-10px; background:radial-gradient(circle,#fff3e0 0%,#ffcc80
  60%,#ffb74d 100%); box-shadow:0 0 50px rgba(255,183,77,0.7);
  animation:celestial-breathe 6s infinite alternate ease-in-out; }
  .sun-aura-twilight { width:160px; height:160px; top:-40px; right:-40px;
  background:radial-gradient(circle,rgba(255,183,77,0.5) 0%,transparent 70%);
  filter:blur(12px); animation:aura-pulse 7s infinite alternate ease-in-out; }
  .moon-core-night { width:90px; height:90px; top:-15px; right:-15px;
  background:radial-gradient(circle,#ffffff 0%,#e0e5db 50%,#9ca3af 100%);
  box-shadow:0 0 30px rgba(200,220,255,0.6), inset -10px -10px 20px
  rgba(0,0,0,0.3); animation:celestial-breathe 6s infinite alternate
  ease-in-out; } .moon-aura-night { width:150px; height:150px; top:-45px;
  right:-45px; background:radial-gradient(circle,rgba(200,220,255,0.3)
  0%,transparent 70%); filter:blur(10px); animation:aura-pulse 8s infinite
  alternate ease-in-out; } .stars { position:absolute; inset:0; overflow:hidden;
  pointer-events:none; } .star-layer { position:absolute; width:1.5px;
  height:1.5px; background:transparent; border-radius:50%; box-shadow:12px 45px
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
  rgba(255,255,255,0.5),510px 125px rgba(255,255,255,0.8); } .t-star {
  position:absolute; width:1.5px; height:1.5px; background:white;
  border-radius:50%; opacity:0.2; } .ts-1 { top:18%; left:22%; animation:shine
  4.2s infinite; } .ts-2 { top:35%; left:68%; animation:shine 5.5s infinite
  1.8s; } .ts-3 { top:12%; left:48%; animation:shine 3.6s infinite 2.5s; }
  .css-cloud { position:absolute; background:rgba(255,255,255,0.8);
  border-radius:50px; filter:drop-shadow(0 8px 16px rgba(0,0,0,0.15)); }
  .css-cloud::before, .css-cloud::after { content:''; position:absolute;
  background:inherit; border-radius:50%; } .cloud-twilight {
  background:rgba(255,220,210,0.85); filter:drop-shadow(0 8px 16px
  rgba(100,0,0,0.1)); } .cloud-night { background:rgba(200,210,225,0.4);
  filter:drop-shadow(0 5px 10px rgba(0,0,0,0.4)); } .cloud-shape-1 {
  width:140px; height:45px; top:40px; animation:cloud-drift-1 16s linear
  infinite; z-index:2; } .cloud-shape-1::before { width:70px; height:70px;
  top:-35px; left:25px; } .cloud-shape-1::after { width:50px; height:50px;
  top:-20px; right:20px; } .cloud-shape-2 { width:105px; height:34px; top:65px;
  animation:cloud-drift-2 22s linear infinite -10s; z-index:1; }
  .cloud-shape-2::before { width:52px; height:52px; top:-26px; left:19px; }
  .cloud-shape-2::after { width:37px; height:37px; top:-15px; right:15px; }
  .rain-1 { background-image: radial-gradient(ellipse 1px 12px at 30%
  10px,rgba(255,255,255,0.3) 0%,transparent 100%), radial-gradient(ellipse 1px
  16px at 80% 60px,rgba(255,255,255,0.2) 0%,transparent 100%);
  background-size:140px 160px; animation:rain-fall-1 0.7s linear infinite; }
  .rain-2 { background-image: radial-gradient(ellipse 1px 10px at 15%
  20px,rgba(255,255,255,0.2) 0%,transparent 100%), radial-gradient(ellipse 1px
  14px at 65% 80px,rgba(255,255,255,0.15) 0%,transparent 100%);
  background-size:100px 120px; animation:rain-fall-2 0.9s linear infinite; }
  .snow-1 { height:200%; background-image:radial-gradient(circle at 20%
  10%,rgba(255,255,255,0.4) 0%,transparent 6px),radial-gradient(circle at 80%
  30%,rgba(255,255,255,0.4) 0%,transparent 8px),radial-gradient(circle at 40%
  50%,rgba(255,255,255,0.4) 0%,transparent 6px),radial-gradient(circle at 70%
  75%,rgba(255,255,255,0.4) 0%,transparent 7px),radial-gradient(circle at 10%
  90%,rgba(255,255,255,0.4) 0%,transparent 5px),radial-gradient(circle at 60%
  15%,rgba(255,255,255,0.4) 0%,transparent 6px); background-size:100% 50%;
  animation:snowflakes-sliding 2s linear infinite; opacity:0.8; } .snow-2 {
  height:200%; background-image:radial-gradient(circle at 15%
  5%,rgba(255,255,255,0.3) 0%,transparent 4px),radial-gradient(circle at 55%
  25%,rgba(255,255,255,0.3) 0%,transparent 3px),radial-gradient(circle at 85%
  45%,rgba(255,255,255,0.3) 0%,transparent 4px),radial-gradient(circle at 25%
  65%,rgba(255,255,255,0.3) 0%,transparent 3px),radial-gradient(circle at 65%
  85%,rgba(255,255,255,0.3) 0%,transparent 4px); background-size:100% 50%;
  animation:snowflakes-sliding 1s linear infinite; opacity:0.6; } .fog-band {
  position:absolute; width:200%; height:40px; background:linear-gradient(to
  right,transparent,rgba(255,255,255,0.7),transparent); filter:blur(10px); }
  .fog-1 { top:40px; animation:fog-drift 18s linear infinite alternate; } .fog-2
  { top:100px; opacity:0.6; animation:fog-drift 28s linear infinite
  alternate-reverse; width:250%; } .storm-flash { background:white;
  animation:room-flash 7s steps(1) infinite; mix-blend-mode:overlay; }
  .storm-bolt { width:80px; height:140px; background:#e0f2fe;
  clip-path:polygon(55% 0%,80% 0%,50% 45%,85% 45%,20% 100%,40% 55%,10% 55%);
  filter:drop-shadow(0 0 15px rgba(255,255,255,0.9)); animation:storm-strike 6s
  steps(1) infinite; } .wind-stream { position:absolute; 
  background:linear-gradient(90deg,transparent,rgba(255,255,255,0.4),transparent); 
  height:2px; border-radius:50%; filter:blur(1px); } .ws-1 { top:25%;
  width:200px;  animation:wind-rush 1.4s linear infinite; } .ws-2 { top:55%;
  width:150px;  animation:wind-rush 1.8s linear infinite 0.7s; } .ws-3 {
  top:75%; width:250px;  animation:wind-rush 1.2s linear infinite 0.3s; }
  .card-content { position:relative; z-index:5; padding:12px 16px; display:flex;
  flex-direction:column; width:100%; box-sizing:border-box; } .top-row {
  display:flex; justify-content:space-between; align-items:flex-start;
  width:100%; } .glass-metric { pointer-events:auto; display:flex;
  align-items:center; background:rgba(0,0,0,0.15); backdrop-filter:blur(20px)
  saturate(180%); -webkit-backdrop-filter:blur(20px) saturate(180%); border:1px
  solid rgba(255,255,255,0.2); border-radius:calc(12px * var(--s-bdg, 1));
  padding:calc(4px * var(--s-bdg, 1)) calc(8px * var(--s-bdg, 1));
  font-size:calc(11px * var(--s-bdg, 1)); font-weight:600; color:white;
  text-shadow:0 1px 2px rgba(0,0,0,0.4); box-shadow:0 2px 10px rgba(0,0,0,0.05);
  letter-spacing:0.2px; white-space:nowrap; transition:all 0.2s ease;
  cursor:pointer; } .glass-metric:hover, .glass-metric:active {
  background:rgba(0,0,0,0.25); transform:translateY(-1px); } .glass-metric
  ha-icon { opacity:0.9; width:calc(14px * var(--s-bdg, 1)); height:calc(14px *
  var(--s-bdg, 1)); margin-right:calc(4px * var(--s-bdg, 1));
  filter:drop-shadow(0 1px 1px rgba(0,0,0,0.3)); } .hover-text-block {
  pointer-events:auto; display:inline-flex; align-items:center; cursor:pointer;
  border-radius:calc(8px * var(--s-txt, 1)); padding:calc(2px * var(--s-txt, 1))
  calc(6px * var(--s-txt, 1)); margin-left:calc(-6px * var(--s-txt, 1));
  transition:background 0.2s ease; } .hover-text-block:hover,
  .hover-text-block:active { background:rgba(255,255,255,0.15); }
  .forecast-container { display:flex; gap:calc(4px * var(--s-fc, 1));
  margin-top:calc(6px * var(--s-fc, 1)); width:100%; box-sizing:border-box;
  justify-content:space-between; } .forecast-item { display:flex;
  flex-direction:column; align-items:center; background:rgba(0,0,0,0.15);
  border:1px solid rgba(255,255,255,0.15); border-radius:calc(10px * var(--s-fc,
  1)); padding:calc(6px * var(--s-fc, 1)) 0; flex:1 1 0; min-width:0;
  overflow:hidden; } .fc-time { font-size:calc(10px * var(--s-fc, 1));
  font-weight:600; opacity:0.9; margin-bottom:calc(4px * var(--s-fc, 1));
  text-transform:uppercase; white-space:nowrap; } .fc-icon { width:calc(20px *
  var(--s-fc, 1)); height:calc(20px * var(--s-fc, 1)); margin-bottom:calc(4px *
  var(--s-fc, 1)); filter:drop-shadow(0 2px 2px rgba(0,0,0,0.3)); } .fc-temp {
  font-size:calc(13px * var(--s-fc, 1)); font-weight:700; line-height:1; }
  .fc-low { font-size:calc(10px * var(--s-fc, 1)); opacity:0.6;
  margin-top:calc(2px * var(--s-fc, 1)); font-weight:500; } .temptrend-container
  { width:100%; margin-top:calc(8px * var(--s-fc, 1)); padding-top:calc(8px *
  var(--s-fc, 1)); border-top:0px solid rgba(255,255,255,0.1); } .temptrend-bar
  { width:100%; height:calc(6px * var(--s-fc, 1)); border-radius:calc(4px *
  var(--s-fc, 1)); opacity:0.9; box-shadow:inset 0 1px 2px rgba(0,0,0,0.4); }
custom_fields:
  content: |
    [[[
      const clk = e => e ? `ontouchstart="this.sX=event.touches[0].clientX;this.sY=event.touches[0].clientY;" 
        ontouchend="if(Math.abs(event.changedTouches[0].clientX-this.sX)<15&&Math.abs(event.changedTouches[0].clientY-this.sY)<15)this.dispatchEvent(new CustomEvent('hass-more-info',{bubbles:true,composed:true,detail:{entityId:'${e}'}}));" 
        onclick="this.dispatchEvent(new CustomEvent('hass-more-info',{bubbles:true,composed:true,detail:{entityId:'${e}'}}));"` : '';

      const v = variables;
      const getObj = eid => eid && states[eid] ? states[eid] : null;

      const w = getObj(v.weather_entity);
      const t = getObj(v.temp_entity);
      const c = getObj(v.cond_entity);
      const dF = getObj(v.forecast_daily_entity);
      const hF = getObj(v.forecast_hourly_entity);
      
      const sT = v.size_temp && !isNaN(v.size_temp) ? parseFloat(v.size_temp) / 38 : 1;
      const sC = v.size_cond && !isNaN(v.size_cond) ? parseFloat(v.size_cond) / 19 : 1;
      const sB = v.size_badges && !isNaN(v.size_badges) ? parseFloat(v.size_badges) / 11 : 1;
      const sdT = v.size_date_time && !isNaN(v.size_date_time) ? parseFloat(v.size_date_time) / 14 : 1;
      const sF = v.size_forecast && !isNaN(v.size_forecast) ? parseFloat(v.size_forecast) / 13 : 1;

      if (!w && !t && !c && !dF && !hF) {
        return `
          <div style="--s-err: ${sT};display:flex;flex-direction:column;align-items:center;justify-content:center;
            padding:24px;text-align:center;box-sizing:border-box;width:100%;min-height:140px;
            border-radius:20px;background:#1e293b;">
            <ha-icon icon="mdi:cog" style="color:#38bdf8;width:calc(36px * var(--s-err, 1));height:calc(36px * var(--s-err, 1));margin-bottom:calc(12px * var(--s-err, 1));"></ha-icon>
            <span style="font-size:calc(16px * var(--s-err, 1));font-weight:600;margin-bottom:calc(6px * var(--s-err, 1));color:white;">Setup Required</span>
            <span style="font-size:calc(12px * var(--s-err, 1));color:rgba(255,255,255,0.7);line-height:1.4;">
              Provide a valid <b>weather_entity</b>,<br>or both <b>temp_entity</b> and <b>cond_entity</b>.
            </span>
          </div>`;
      }

      const getAttr = (ent, attr) => ent ? ent.attributes?.[attr] : null;

      const wTemp = val => `
        <span style="font-size:${38 * sT}px;font-weight:400;line-height:1;letter-spacing:-1px;
        text-shadow:0 1px 3px rgba(0,0,0,0.3);display:flex;align-items:center;">${val}</span>`;
      
      const wCond = val => `
        <span style="font-size:${19 * sC}px;font-weight:600;color:rgba(255,255,255,0.98);
        text-shadow:0 1px 3px rgba(0,0,0,0.3);letter-spacing:0.3px;">${val}</span>`;
      
      const bdg = (ic, col, h, s, scale) => `
        <div style="display:flex;align-items:center;justify-content:center;background:rgba(239,68,68,0.15);
        padding:${4 * scale}px ${s * scale}px;border-radius:${s * scale}px;border:1px solid rgba(239,68,68,0.3);height:${h * scale}px;box-sizing:border-box;">
          <ha-icon icon="${ic}" style="width:${(s+6) * scale}px;height:${(s+6) * scale}px;margin-right:${6 * scale}px;color:${col};display:block;"></ha-icon>
          <span style="font-size:${(s+6) * scale}px;font-weight:600;color:${col};line-height:1;display:block;">-</span>
        </div>`;

      let tS = t ? t.state : getAttr(w, 'temperature');
      let tH = bdg('mdi:thermometer-off', '#fca5a5', 32, 12, sT);
      if (tS === 'unavailable') tH = wTemp('-');
      else if (tS != null && !isNaN(tS)) tH = wTemp(Math.round(tS) + '°');

      let timeHtml = '';
      if (v.time_show !== false || v.date_show !== false) {
        const dt = new Date();
        const ts = v.time_show !== false ? dt.toLocaleTimeString(undefined, { hour: 'numeric', minute: '2-digit', hour12: v.time_format === 12 }) : '';
        const ds = v.date_show !== false ? dt.toLocaleDateString(undefined, { weekday: 'short', month: 'short', day: 'numeric' }) : '';
        timeHtml = `
          <div class="hover-text-block" style="margin-left:${2 * sdT}px;opacity:0.65;display:flex;align-items:center;gap:${4 * sdT}px;" ${v.time_entity ? clk(v.time_entity) : ''}>
            <span style="font-size:${14 * sdT}px;font-weight:500;">${[ts, ds].filter(Boolean).join(' • ')}</span>
          </div>`;
      }

      let rC = c ? c.state : (w ? w.state : null);
      rC = ['unknown', 'unavailable'].includes(rC) ? null : (rC ? String(rC).toLowerCase() : null);

      let cK = 'unknown';
      let cH = bdg('mdi:cloud-question', '#fca5a5', 26, 10, sC);

      if (rC && isNaN(Number(rC))) {
        const cM = {
          clear: v.cond_clear, 'clear-night': v.cond_clear_night, cloudy: v.cond_cloudy,
          partlycloudy: v.cond_partlycloudy, rainy: v.cond_rainy, snowy: v.cond_snowy,
          storm: v.cond_storm, fog: v.cond_fog, windy: v.cond_windy
        };
        cK = Object.keys(cM).find(k => cM[k]?.split(',').map(x => x.trim().toLowerCase()).includes(rC)) || 'unknown';
        if (cK === 'unknown' && (rC.includes('wind') || rC.includes('breez'))) cK = 'windy';
        const rawTxt = rC.replace(/[-_]/g, ' ').replace(/partlycloudy/gi, 'partly cloudy').split(' ').map(x => x.charAt(0).toUpperCase() + x.slice(1)).join(' ');
        cH = wCond(v.translate_conditions?.[cK] || rawTxt);
      } else if (rC !== null) {
        cH = wCond('-');
      }

      const fE = getObj(v.feels_like_entity);
      let fS = fE ? fE.state : getAttr(w, 'apparent_temperature');
      let fH = '';
      if (fS != null) {
        const fVal = fS === 'unavailable' ? '-' : Math.round(fS) + '°';
        fH = `
          <div class="hover-text-block" style="margin-left:${2 * sdT}px;" ${clk(v.feels_like_entity || v.weather_entity)}>
            <span style="font-size:${14 * sdT}px;font-weight:500;opacity:0.95;">${v.translate_feels_like || 'Feels like'} ${fVal}</span>
          </div>`;
      }

      const buildMetric = (eid, attr, uAttr, ic, isPct, custU) => {
        const ent = getObj(eid);
        const val = ent ? ent.state : (w && attr ? getAttr(w, attr) : null);
        if (val == null || val === 'unknown') return '';
        if (val === 'unavailable') return `<div class="glass-metric"><ha-icon icon="${ic}"></ha-icon> -</div>`;

        const unit = custU ? ` ${custU}` : (isPct ? '%' : ` ${(ent ? getAttr(ent, 'unit_of_measurement') : getAttr(w, uAttr)) || ''}`);
        const fmtVal = isNaN(val) ? String(val).replace(/ uv(?: index)?/gi, '').trim() : Math.round(val);
        const finalVal = typeof fmtVal === 'string' ? fmtVal.charAt(0).toUpperCase() + fmtVal.slice(1) : fmtVal;

        return `
          <div class="glass-metric" ${clk(eid || v.weather_entity)}>
            <ha-icon icon="${ic}"></ha-icon> ${finalVal}${unit}
          </div>`;
      };

      const mH = [
        [v.hum_entity, 'humidity', '', 'mdi:water-percent', true],
        [v.wind_entity, 'wind_speed', 'wind_speed_unit', 'mdi:weather-windy', false],
        [v.wind_gust_entity, 'wind_gust', 'wind_speed_unit', 'mdi:weather-windy-variant', false],
        [v.rain_entity, 'precipitation', 'precipitation_unit', 'mdi:weather-pouring', false],
        [v.pressure_entity, 'pressure', 'pressure_unit', 'mdi:gauge', false],
        [v.aqi_entity, null, null, 'mdi:air-filter', false],
        [v.uv_entity, null, null, 'mdi:weather-sunny-alert', false, 'uv'],
        [v.pollen_entity, null, null, 'mdi:flower-pollen', false],
        [v.fire_entity, null, null, 'mdi:fire-alert', false]
      ].map(m => buildMetric(...m)).join('');

      const getIc = cond => ({
        'clear-night': 'mdi:weather-night', cloudy: 'mdi:weather-cloudy', fog: 'mdi:weather-fog',
        hail: 'mdi:weather-hail', lightning: 'mdi:weather-lightning', 'lightning-rainy': 'mdi:weather-lightning-rainy',
        partlycloudy: 'mdi:weather-partly-cloudy', pouring: 'mdi:weather-pouring', rainy: 'mdi:weather-rainy',
        snowy: 'mdi:weather-snowy', 'snowy-rainy': 'mdi:weather-snowy-rainy', sunny: 'mdi:weather-sunny',
        windy: 'mdi:weather-windy', 'windy-variant': 'mdi:weather-windy-variant', clear: 'mdi:weather-sunny'
      }[cond] || 'mdi:cloud-question');

      const buildFc = (data, count, isHourly) => {
        if (!data || !Array.isArray(data)) return '';
        const items = data.slice(0, count || 7).map(f => {
          const dtObj = new Date(f.datetime);
          let timeStr;
          if (isHourly) {
            timeStr = dtObj.toLocaleTimeString(undefined, { hour: 'numeric', minute: '2-digit', hour12: v.time_format === 12 });
          } else {
            timeStr = v.translate_days?.[dtObj.getDay()] || dtObj.toLocaleDateString(undefined, { weekday: 'short' });
          }
          const lowHtml = !isHourly && f.templow !== undefined ? `<div class="fc-low">${Math.round(f.templow)}°</div>` : '';
          
          return `
            <div class="forecast-item">
              <div class="fc-time">${timeStr}</div>
              <ha-icon class="fc-icon" icon="${getIc(f.condition)}"></ha-icon>
              <div class="fc-temp">${Math.round(f.temperature)}°</div>
              ${lowHtml}
            </div>`;
        }).join('');
        return `<div class="forecast-container">${items}</div>`;
      };

      const hrData = hF ? getAttr(hF, 'forecast') : (w ? getAttr(w, 'forecast_hourly') || (!getAttr(w, 'forecast_daily') ? getAttr(w, 'forecast') : null) : null);
      const dyData = dF ? getAttr(dF, 'forecast') : (w ? getAttr(w, 'forecast_daily') || getAttr(w, 'forecast') : null);

      const hourlyH = v.forecast_hourly_show ? buildFc(hrData, v.forecast_hourly_count, true) : '';
      const dailyH = v.forecast_daily_show ? buildFc(dyData, v.forecast_daily_count, false) : '';

      const el = getAttr(getObj(v.sun_entity), 'elevation');
      let tD = el !== undefined ? (el < -4 ? 'night' : (el <= 10 ? (new Date().getHours() < 12 ? 'sunrise' : 'sunset') : 'day')) : (cK.includes('night') ? 'night' : 'day');

      if (tD !== 'night' && cK.includes('night')) cK = cK.replace('-night', '').replace('night', 'clear');
      else if (tD === 'night' && cK === 'sunny') cK = 'clear-night';

      const sH = tD === 'night' ? `<div class="stars"><div class="star-layer"></div><div class="t-star ts-1"></div><div class="t-star ts-2"></div><div class="t-star ts-3"></div></div>` : '';
      const cC = tD === 'night' ? 'cloud-night' : (tD !== 'day' ? 'cloud-twilight' : '');
      const sC_theme = tD !== 'day' ? 'twilight' : 'day';
      const css = `
        ${sH}
        <div class="effect-layer">
          <div class="${tD === 'night' ? 'moon' : 'sun'}-aura-${tD === 'night' ? 'night' : sC_theme} celestial-shared"></div>
          <div class="${tD === 'night' ? 'moon' : 'sun'}-core-${tD === 'night' ? 'night' : sC_theme} celestial-shared"></div>`;

      let cat = 'sunny', eL = css + `</div>`;
      if (cK === 'unknown') {
        cat = 'unknown';
      } else if (cK.includes('storm') || cK.includes('thunder')) {
        cat = 'storm'; eL = `<div class="effect-layer storm-flash"></div><div class="effect-layer storm-bolt"></div>`;
      } else if (cK.includes('snow') || cK.includes('hail')) {
        cat = 'snow'; eL = `<div class="effect-layer snow-1"></div><div class="effect-layer snow-2"></div>`;
      } else if (cK.includes('rain') || cK.includes('pour')) {
        cat = 'rain'; eL = `<div class="effect-layer rain-1"></div><div class="effect-layer rain-2"></div>`;
      } else if (cK.includes('partly')) {
        cat = 'partly'; eL = css + `<div class="css-cloud ${cC} cloud-shape-1"></div></div>`;
      } else if (cK.includes('cloud')) {
        cat = 'cloudy'; eL = `${sH}<div class="effect-layer"><div class="css-cloud ${cC} cloud-shape-1"></div><div class="css-cloud ${cC} cloud-shape-2"></div></div>`;
      } else if (cK.includes('fog')) {
        cat = 'fog'; eL = `${sH}<div class="effect-layer"><div class="fog-band fog-1"></div><div class="fog-band fog-2"></div></div>`;
      } else if (cK.includes('wind')) {
        cat = 'cloudy'; eL = `${sH}<div class="effect-layer"><div class="css-cloud ${cC} cloud-shape-1" style="animation-duration:5s;"></div><div class="css-cloud ${cC} cloud-shape-2" style="animation-duration:7s;"></div><div class="wind-stream ws-1"></div><div class="wind-stream ws-2"></div><div class="wind-stream ws-3"></div></div>`;
      }

      const tK = tD === 'night' ? 'night' : (tD !== 'day' ? 'twilight' : 'day');
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
      const bgS = `background:linear-gradient(to bottom, ${(bG[cat] || bG.sunny)[tK].join(', ')});box-shadow:${sh[cat]?.[tK] || 'none'};`;

      let trH = '';
      if (v.temptrend_show && v.temptrend_entity) {
        const trend = getObj(v.temptrend_entity);
        const hs = getAttr(trend, 'history')?.map(Number);
        if (hs?.length > 1) {
          const isF = getAttr(t, 'unit_of_measurement')?.includes('F') || getAttr(w, 'temperature_unit')?.includes('F');
          const minSp = isF ? 16.2 : 9;
          const mn = Math.min(...hs), mx = Math.max(...hs);
          let sp = mx - mn, bs = mn;
          if (sp < minSp) { bs = ((mx + mn) / 2) - (minSp / 2); sp = minSp; }
          const st = hs.map((temp, i) => {
            const p = Math.max(0, Math.min(1, (temp - bs) / (sp || 1)));
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
        <div class="card-content" style="--s-bdg: ${sB}; --s-txt: ${sdT}; --s-fc: ${sF};">
          <div class="top-row">
            <div style="display:flex;flex-direction:column;align-items:flex-start;flex:1;min-width:0;">
              <div style="display:flex;align-items:center;gap:${6 * sT}px;flex-wrap:wrap;">
                <div class="hover-text-block" style="display:flex;align-items:center;" ${clk(v.temp_entity || v.weather_entity)}>
                  ${tH}
                </div>
                ${fH}
                ${timeHtml}
              </div>
              <div class="hover-text-block" style="margin-top:${4 * sC}px;" ${clk(v.cond_entity || v.weather_entity)}>
                ${cH}
              </div>
              <div style="display:flex;gap:${6 * sB}px;margin-top:${8 * sB}px;flex-wrap:wrap;">
                ${mH}
              </div>
            </div>
          </div>
          ${hourlyH}
          ${dailyH}
          ${trH}
        </div>`;
    ]]]

```
</details>

<details>
<summary><strong>Template (Temperature Trend)</summary>

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

<details>
<summary><strong>Template (Forecast)</summary>
  
<br>
  
>Note: Replace weather.REPLACE_ME in all 5 places with your weather entity ID.

```yaml
  - trigger:
      - trigger: state
        entity_id: weather.REPLACE_ME
      - trigger: homeassistant
        event: start
    action:
      - action: weather.get_forecasts
        data:
          type: daily
        target:
          entity_id: weather.REPLACE_ME
        response_variable: daily
      - action: weather.get_forecasts
        data:
          type: hourly
        target:
          entity_id: weather.REPLACE_ME
        response_variable: hourly
    sensor:
      - name: Custom Weather Forecast Daily
        unique_id: custom_weather_forecast_daily
        state: "{{ now().isoformat() }}"
        attributes:
          forecast: "{{ daily['weather.REPLACE_ME'].forecast }}"
      - name: Custom Weather Forecast Hourly
        unique_id: custom_weather_forecast_hourly
        state: "{{ now().isoformat() }}"
        attributes:
          forecast: "{{ hourly['weather.REPLACE_ME'].forecast }}"
```
</details>


<hr>

<details>
<summary><strong>Universal Climate Card</summary>

```yaml
type: custom:button-card
entity: 
name: Climate Universal
show_state: false
show_label: true
variables:
  sensor_status: ''
  sensor_temp: ''
  round_temp: 1
  sensor_hum: ''
  round_hum: 0
  temp_color_yellow: 24
  temp_color_orange: 27
  temp_color_red: 30
  state_error: unavailable, unknown
  state_idle: idle, off, standby
  state_auto: auto
  state_heat: heat, heating
  state_cool: cool, cooling
  state_heat_cool: heat_cool
  state_dry: dry, drying, dehumidify
  state_fan: fan, fan_only, ventilation
  sensor_presence: ''
  sensor_power: ''
  sensor_cost: ''
  show_cost: false
  bar_mode: temp
  max_cost: 10
  max_power_w: 100
tap_action:
  action: more-info
label: |
  [[[
    if (!entity || !entity.state) return 'Entity Setup Required';
    let st = entity.state;
    let err = (variables.state_error || 'unavailable, unknown').split(',').map(s => s.trim().toLowerCase());
    if (err.includes(st.toLowerCase())) return 'Check Configuration';
    return st.replace(/_/g, ' ').replace(/-/g, ' ').replace(/\b\w/g, c => c.toUpperCase());
  ]]]
icon: |
  [[[
    if (!entity || !entity.state) return 'mdi:alert-circle-outline';
    let st = entity.state.toLowerCase();
    let err = variables.state_error.split(',').map(s => s.trim().toLowerCase());
    let cool = variables.state_cool.split(',').map(s => s.trim().toLowerCase());
    let heat = variables.state_heat.split(',').map(s => s.trim().toLowerCase());
    let dry = variables.state_dry.split(',').map(s => s.trim().toLowerCase());
    let fan = variables.state_fan.split(',').map(s => s.trim().toLowerCase());
    let auto = variables.state_auto.split(',').map(s => s.trim().toLowerCase());
    let hc = variables.state_heat_cool.split(',').map(s => s.trim().toLowerCase());
    
    if (err.includes(st)) return 'mdi:alert-circle-outline';
    if (cool.includes(st)) return 'mdi:snowflake';
    if (heat.includes(st)) return 'mdi:fire';
    if (dry.includes(st)) return 'mdi:water-percent';
    if (fan.includes(st)) return 'mdi:fan';
    if (auto.includes(st) || hc.includes(st)) return 'mdi:thermostat-auto';
    return 'mdi:thermostat';
  ]]]
custom_fields:
  badge1: ' '
  badge2: ' '
  t1: ' '
  t2: ' '
  bar: ' '
  presence_dot: ' '
styles:
  card:
    - height: 95px !important
    - padding: 0px !important
    - overflow: hidden
    - position: relative
  grid:
    - padding: 12px 16px
    - height: 100%
    - box-sizing: border-box
    - grid-template-areas: '"i n" "i l"'
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
    - transform-origin: center center
    - animation: var(--appliance-icon-anim) !important
    - z-index: 3
  img_cell:
    - width: 65px
    - height: 65px
    - border-radius: 50%
    - background: rgba(var(--appliance-color), 0.05) !important
    - border: 1px solid rgba(var(--appliance-color), 0.15)
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
    presence_dot:
      - position: absolute
      - top: 12px
      - left: 12px
      - width: 6px
      - height: 6px
      - border-radius: 50%
      - z-index: 5
      - transition: background-color 0.4s ease
    badge1:
      - position: absolute
      - top: 10px
      - right: 10px
      - padding: 3px 8px
      - font-size: 10px
      - letter-spacing: 0.5px
      - white-space: nowrap
      - text-transform: uppercase
      - font-weight: 700
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
      - color: var(--primary-text-color)
      - opacity: 0.9
      - text-transform: uppercase
      - font-weight: 500
      - z-index: 5
      - transition: all 0.5s ease
    t1:
      - position: absolute
      - bottom: 14px
      - font-size: 11px
      - font-weight: 700
      - letter-spacing: 0.5px
      - line-height: 1
      - z-index: 5
      - transition: all 0.5s ease
    t2:
      - position: absolute
      - bottom: 14px
      - right: 10px
      - font-size: 11px
      - font-weight: 700
      - letter-spacing: 0.5px
      - line-height: 1
      - z-index: 5
      - transition: all 0.5s ease
    bar:
      - position: absolute
      - bottom: 0
      - left: 0
      - height: 3px
      - width: var(--appliance-level)
      - background: var(--appliance-bar-bg)
      - box-shadow: var(--appliance-bar-shadow)
      - transition: width 0.8s cubic-bezier(0.4, 0, 0.2, 1)
      - z-index: 5
extra_styles: |
  [[[
    let ent_power = variables.sensor_power;
    let bar_mode = variables.bar_mode;
    let max_power_w = variables.max_power_w;
    
    let raw_status = states[variables.sensor_status] ? states[variables.sensor_status].state : '';
    let status = raw_status.toLowerCase();
    
    let state_err = variables.state_error.split(',').map(s => s.trim().toLowerCase());
    let state_idle = variables.state_idle.split(',').map(s => s.trim().toLowerCase());
    let state_cool = variables.state_cool.split(',').map(s => s.trim().toLowerCase());
    let state_heat = variables.state_heat.split(',').map(s => s.trim().toLowerCase());
    let state_dry = variables.state_dry.split(',').map(s => s.trim().toLowerCase());
    let state_fan = variables.state_fan.split(',').map(s => s.trim().toLowerCase());
    let state_auto = variables.state_auto.split(',').map(s => s.trim().toLowerCase());
    let state_hc = variables.state_heat_cool.split(',').map(s => s.trim().toLowerCase());
    
    let is_error = state_err.includes(status);
    let is_idle = state_idle.includes(status);
    let is_cool = state_cool.includes(status);
    let is_heat = state_heat.includes(status);
    let is_dry = state_dry.includes(status);
    let is_fan = state_fan.includes(status);
    let is_auto = state_auto.includes(status);
    let is_heat_cool = state_hc.includes(status);
    
    let attr = states[variables.sensor_status] ? states[variables.sensor_status].attributes : {};
    
    let ext_temp = (variables.sensor_temp && states[variables.sensor_temp]) ? parseFloat(states[variables.sensor_temp].state) : undefined;
    let ext_hum = (variables.sensor_hum && states[variables.sensor_hum]) ? parseFloat(states[variables.sensor_hum].state) : undefined;
    
    let raw_temp_attr = !isNaN(parseFloat(attr.current_temperature)) ? parseFloat(attr.current_temperature) : NaN;
    let raw_hum_attr = !isNaN(parseFloat(attr.current_humidity)) ? parseFloat(attr.current_humidity) : NaN;
    
    let c_t = !isNaN(ext_temp) ? ext_temp : (!isNaN(raw_temp_attr) ? raw_temp_attr : NaN);
    let c_h = !isNaN(ext_hum) ? ext_hum : (!isNaN(raw_hum_attr) ? raw_hum_attr : NaN);
    
    let rt = variables.round_temp !== undefined ? variables.round_temp : 1;
    let rh = variables.round_hum !== undefined ? variables.round_hum : 0;
    
    let temp_str = !isNaN(c_t) ? c_t.toFixed(rt) + '°' : '';
    let hum_str = !isNaN(c_h) ? c_h.toFixed(rh) + '%' : '';

    let temp_color_rgb = '33, 150, 243'; 
    if (variables.temp_color_red !== undefined && c_t >= variables.temp_color_red) temp_color_rgb = '244, 67, 54';
    else if (variables.temp_color_orange !== undefined && c_t >= variables.temp_color_orange) temp_color_rgb = '255, 152, 0';
    else if (variables.temp_color_yellow !== undefined && c_t >= variables.temp_color_yellow) temp_color_rgb = '255, 193, 7';
    
    let hum_color_rgb = '33, 150, 243'; 
    
    let raw_fan = attr.fan_mode ? String(attr.fan_mode) : '';
    let power_state = states[ent_power];
    let raw_power = power_state ? parseFloat(power_state.state) : NaN;
    
    let t_single = attr.temperature;
    let t_low = attr.target_temp_low;
    let t_high = attr.target_temp_high;
    let action = attr.hvac_action ? String(attr.hvac_action).toLowerCase() : '';
    
    let t1_text = ''; let t1_color = 'transparent'; 
    let t2_text = ''; let t2_color = 'transparent';
    let raw_targ = 0; let t1_right = '10px';
    
    if (!isNaN(parseFloat(t_low)) && !isNaN(parseFloat(t_high)) && t_low !== null) {
        t1_text = '➔ ' + t_low + '°';
        t1_color = 'orangered';
        t2_text = '| ' + t_high + '°';
        t2_color = '#2196F3';
        raw_targ = (parseFloat(t_low) + parseFloat(t_high)) / 2;
        t1_right = `calc(5px + ${t2_text.length}ch)`;
    } else if (!isNaN(parseFloat(t_single)) && t_single !== null) {
        t1_text = '➔ ' + t_single + '°';
        let t_t = parseFloat(t_single);
        if (c_t > 0) {
            if (t_t > c_t) t1_color = 'orangered';
            else if (t_t < c_t) t1_color = '#2196F3';
            else t1_color = 'var(--primary-text-color)';
        } else {
            if (is_heat || action === 'heating') t1_color = 'orangered';
            else if (is_cool || action === 'cooling') t1_color = '#2196F3';
            else t1_color = 'var(--primary-text-color)';
        }
        raw_targ = t_single;
    } else {
        raw_targ = c_t;
    }
    
    let fan_text = '';
    if (!['unknown', 'unavailable', 'none', ''].includes(raw_fan.toLowerCase())) {
        let f = raw_fan.toLowerCase().replace(/_/g, ' ').replace(/-/g, ' ');
        let clean_fan = '';
        if (f === 'on') clean_fan = 'On';
        else {
            f = f.replace('on low', 'low').replace('low on', 'low');
            f = f.replace('on medium', 'medium').replace('medium on', 'medium');
            f = f.replace('on high', 'high').replace('high on', 'high');
            f = f.replace('on med', 'med').replace('med on', 'med');
            clean_fan = f.replace(/\b\w/g, c => c.toUpperCase());
        }
        fan_text = 'Fan: ' + clean_fan;
    }
    
    let pwr_pct = 0;
    let power_text = '';
    
    if (variables.show_cost && variables.sensor_cost && states[variables.sensor_cost]) {
        let c_state = states[variables.sensor_cost];
        let c_val = parseFloat(c_state.state);
        let uom = c_state.attributes.unit_of_measurement || '';
        if (!isNaN(c_val)) {
            power_text = c_val.toFixed(2) + uom;
            pwr_pct = variables.max_cost > 0 ? (c_val / variables.max_cost) * 100 : 50; 
        }
    } else if (!isNaN(raw_power)) {
        let power_w = Math.round(raw_power);
        power_text = power_w + 'W';
        pwr_pct = max_power_w > 0 ? (power_w / max_power_w) * 100 : 0;
    }
    
    let f_pct = 50;
    if (!['unknown', 'unavailable', 'none', ''].includes(raw_fan.toLowerCase())) {
        let f_val = raw_fan.toLowerCase().replace(/ /g, '_');
        if (f_val === 'off') f_pct = 0;
        else if (!isNaN(parseFloat(f_val)) && parseFloat(f_val) > 5) f_pct = parseFloat(f_val);
        else if (['on_low', 'low', 'quiet', 'min', '1', 'auto_low'].includes(f_val)) f_pct = 33;
        else if (['on_medium', 'medium', 'med', '2', '3', 'auto_medium'].includes(f_val)) f_pct = 66;
        else if (['on_high', 'high', 'max', 'turbo', '4', '5', 'auto', 'on', 'auto_high'].includes(f_val)) f_pct = 100;
    } else {
        f_pct = -1; 
    }
    
    let anim_speed = 2.5;
    if (f_pct >= 80) anim_speed = 0.8;
    else if (f_pct >= 50) anim_speed = 1.5;
    
    let fan_color = '76, 175, 80';
    if (f_pct === -1) fan_color = 'transparent';
    else if (f_pct === 0) fan_color = '158, 158, 158'; 
    else if (f_pct >= 80) fan_color = '244, 67, 54'; 
    else if (f_pct >= 50) fan_color = '33, 150, 243';
    
    let pwr_color = '76, 175, 80';
    if (pwr_pct >= 75) pwr_color = '244, 67, 54'; 
    else if (pwr_pct >= 40) pwr_color = '255, 193, 7'; 
    
    let progress = 0;
    if (!is_idle && !is_error) {
        if (bar_mode === 'power') {
            progress = Math.max(3, Math.min(pwr_pct, 100));
        } else if (bar_mode === 'fan' && f_pct >= 0) {
            progress = f_pct;
        } else if (bar_mode === 'temp' && c_t > 0) {
            if (!isNaN(parseFloat(t_low)) && !isNaN(parseFloat(t_high)) && t_low !== null) {
                let tl = parseFloat(t_low); let th = parseFloat(t_high);
                if (c_t < tl) {
                    let p = tl > 0 ? (c_t / tl) * 100 : 100;
                    progress = Math.max(3, Math.min(p, 100));
                } else if (c_t > th) {
                    let p = c_t > 0 ? (th / c_t) * 100 : 100;
                    progress = Math.max(3, Math.min(p, 100));
                } else progress = 100;
            } else if (!isNaN(parseFloat(raw_targ)) && raw_targ !== null) {
                let t_t = parseFloat(raw_targ);
                if (is_cool || action === 'cooling') {
                    let p = c_t > 0 ? (t_t / c_t) * 100 : 100;
                    progress = Math.max(3, Math.min(p, 100));
                } else if (is_heat || action === 'heating') {
                    let p = t_t > 0 ? (c_t / t_t) * 100 : 100;
                    progress = Math.max(3, Math.min(p, 100));
                } else {
                    let p = c_t > t_t ? (c_t > 0 ? (t_t / c_t)*100 : 100) : (t_t > 0 ? (c_t / t_t)*100 : 100);
                    progress = Math.max(3, Math.min(p, 100));
                }
            }
        }
    }
    
    let pres_state = (variables.sensor_presence && states[variables.sensor_presence]) ? states[variables.sensor_presence].state.toLowerCase() : 'none';
    let pres_display = 'none';
    let pres_bg = 'transparent';
    let pres_shadow = 'none';
    
    if (pres_state !== 'none' && pres_state !== 'unavailable' && pres_state !== 'unknown') {
        pres_display = 'block';
        if (pres_state === 'on' || pres_state === 'home' || pres_state === 'active') {
            pres_bg = '#F44336';
            pres_shadow = '0 0 4px rgba(244, 67, 54, 0.8)';
        } else {
            pres_bg = '#9E9E9E';
        }
    }
    
    let badge1 = ''; let badge2 = ''; 
    let color = '158, 158, 158'; let icon_anim = 'none';
    let b1_bg = 'transparent'; let b1_border = 'none'; let b1_bl = 'none'; let b1_br = 'none'; let b1_text = 'inherit';
    let b1_shadow = 'none';
    let b2_bg = 'transparent'; let b2_bl = 'none'; let b2_br = 'none';
    let bar_bg = 'rgb(158, 158, 158)';
    let bar_shadow = 'none';
    
    if (is_error) {
        badge1 = '⚠️ ERROR';
        color = '244, 67, 54';
        b1_bg = `rgba(${color}, 0.15)`; b1_border = `1px solid rgba(${color}, 0.3)`; b1_bl = `2px solid rgb(${color})`; b1_br = b1_border; b1_text = `rgb(${color})`;
    } else {
        if (is_cool) { color = '33, 150, 243'; icon_anim = 'none'; }
        else if (is_heat) { color = '255, 87, 34'; icon_anim = 'gentle-fire 3s ease-in-out infinite alternate'; }
        else if (is_dry) { color = '255, 213, 79'; icon_anim = 'none'; }
        else if (is_fan) { color = '0, 150, 136'; icon_anim = 'gentle-spin var(--appliance-speed) linear infinite'; }
        else if (is_auto || is_heat_cool) { color = '158, 158, 158'; icon_anim = 'none'; }
        
        let s_fmt = status.replace(/_/g, ' ').replace(/-/g, ' ').replace(/\b\w/g, c => c.toUpperCase());
        let b1_parts = [s_fmt];
        if (hum_str) b1_parts.push(hum_str);
        if (temp_str) b1_parts.push(temp_str);
        badge1 = b1_parts.join(' • ');
        
        b1_text = 'var(--primary-text-color)';
        b1_border = '1px solid rgba(128,128,128, 0.2)';
        let has_hum = !!hum_str;
        let has_temp = !!temp_str;
        
        if (has_hum && has_temp) {
            b1_bg = `linear-gradient(90deg, rgba(${color}, 0.15) 0%, rgba(${hum_color_rgb}, 0.15) 50%, rgba(${temp_color_rgb}, 0.15) 100%)`;
            b1_bl = `2.5px solid rgb(${color})`;
            b1_br = `2.5px solid rgb(${temp_color_rgb})`;
        } else if (has_temp) {
            b1_bg = `linear-gradient(90deg, rgba(${color}, 0.15) 0%, rgba(${temp_color_rgb}, 0.15) 100%)`;
            b1_bl = `2.5px solid rgb(${color})`;
            b1_br = `2.5px solid rgb(${temp_color_rgb})`;
        } else if (has_hum) {
            b1_bg = `linear-gradient(90deg, rgba(${color}, 0.15) 0%, rgba(${hum_color_rgb}, 0.15) 100%)`;
            b1_bl = `2.5px solid rgb(${color})`;
            b1_br = `2.5px solid rgb(${hum_color_rgb})`;
        } else {
            b1_bg = `linear-gradient(0deg, rgba(${color}, 0.15), rgba(${color}, 0.15))`;
            b1_bl = `2.5px solid rgb(${color})`;
            b1_br = `2.5px solid rgb(${color})`;
        }
        
        if (is_heat_cool || is_auto) {
            b1_bl = '2.5px solid transparent';
            b1_shadow = 'none';
            let border_bg = `linear-gradient(to bottom, rgb(255, 87, 34) 50%, rgb(33, 150, 243) 50%) 0 0 / 2.5px 100% no-repeat border-box border-box`;
            let inner_bg = `${b1_bg} 0 0 / 100% 100% no-repeat padding-box padding-box`;
            b1_bg = `${border_bg}, ${inner_bg}`;
        }
        
        let b2_parts = [fan_text, power_text].filter(Boolean);
        badge2 = b2_parts.join(' • ');
        let has_fan = fan_text !== ''; let has_pwr = power_text !== '';
        
        if (has_fan && has_pwr) {
            b2_bg = `linear-gradient(90deg, rgba(${fan_color}, 0.15) 0%, rgba(${pwr_color}, 0.15) 100%)`;
            b2_bl = `2.5px solid rgb(${fan_color})`;
            b2_br = `2.5px solid rgb(${pwr_color})`;
        } else if (has_fan) {
            b2_bg = `rgba(${fan_color}, 0.15)`;
            b2_bl = `2px solid rgb(${fan_color})`;
            b2_br = `1px solid rgba(128,128,128, 0.2)`;
        } else if (has_pwr) {
            b2_bg = `rgba(${pwr_color}, 0.15)`;
            b2_bl = `1px solid rgba(128,128,128, 0.2)`;
            b2_br = `2px solid rgb(${pwr_color})`;
        }
        
        if (is_heat_cool || is_auto) {
            bar_bg = 'linear-gradient(90deg, rgb(33, 150, 243) 0%, rgb(255, 87, 34) 100%)';
            bar_shadow = '0 -1px 8px rgba(158, 158, 158, 0.4)';
        } else {
            bar_bg = `rgb(${color})`;
            bar_shadow = `0 -1px 8px rgba(${color}, 0.5)`;
        }
    }
    
    return `
      #card {
        --appliance-color: ${color};
        --appliance-level: ${progress}%;
        --appliance-speed: ${anim_speed}s;
        --appliance-bar-bg: ${bar_bg};
        --appliance-bar-shadow: ${bar_shadow};
        --appliance-icon-anim: ${icon_anim};
      }
      
      #presence_dot {
        display: ${pres_display};
        background: ${pres_bg};
        box-shadow: ${pres_shadow};
      }
      
      #badge1 {
        background: ${b1_bg};
        color: ${b1_text};
        border-top: ${b1_border};
        border-bottom: ${b1_border};
        border-left: ${b1_bl};
        border-right: ${b1_br};
        border-radius: 6px !important;
        box-shadow: ${b1_shadow};
      }
      #badge1::before { content: "${badge1}"; }
      
      #badge2 {
        display: ${badge2 ? 'block' : 'none'};
        background: ${b2_bg};
        border-top: 1px solid rgba(128,128,128, 0.2);
        border-bottom: 1px solid rgba(128,128,128, 0.2);
        border-left: ${b2_bl};
        border-right: ${b2_br};
        border-radius: 6px !important;
      }
      #badge2::before { content: "${badge2}"; }
      
      #t1 { color: ${t1_color}; right: ${t1_right}; }
      #t1::before { content: "${t1_text}"; }
      
      #t2 { color: ${t2_color}; }
      #t2::before { content: "${t2_text}"; }
      
      ${is_cool ? `
        #img-cell::before {
          content: ''; position: absolute; pointer-events: none; z-index: 0;
          inset: -15px; border-radius: 50%;
          box-shadow: inset 8px 0 15px -5px rgba(var(--appliance-color), 0.7), 0 -8px 15px -5px rgba(var(--appliance-color), 0.5);
          animation: frost-orbit 2.5s cubic-bezier(0.4, 0, 0.2, 1) infinite;
        }
        #img-cell::after {
          content: ''; position: absolute; pointer-events: none; z-index: 0;
          inset: -10px; border-radius: 50%;
          box-shadow: inset -5px 0 15px -5px rgba(var(--appliance-color), 0.9);
          animation: frost-orbit 3.5s linear infinite reverse;
        }
      ` : ''}
      ${is_heat ? `
        #img-cell::before {
          content: ''; position: absolute; pointer-events: none; z-index: 0;
          width: 150%; height: 150%; bottom: -20%; left: -25%; border-radius: 50%;
          background: radial-gradient(circle at 50% 100%, rgba(var(--appliance-color), 0.45) 0%, transparent 65%);
          filter: blur(4px);
          animation: intense-updraft 3s ease-in-out infinite alternate;
        }
        #img-cell::after {
          content: ''; position: absolute; pointer-events: none; z-index: 0;
          width: 3px; height: 3px; border-radius: 50%; bottom: -5px; left: 50%;
          background: rgba(var(--appliance-color), 0.9);
          box-shadow: 
            15px 10px 0 1px rgba(var(--appliance-color), 0.8),
            -20px 25px 0 0px rgba(var(--appliance-color), 0.7),
            5px 35px 0 2px rgba(var(--appliance-color), 0.9),
            -10px 15px 0 -1px rgba(var(--appliance-color), 0.6);
          animation: intense-embers 2s ease-in infinite;
        }
      ` : ''}
      ${is_dry ? `
        #img-cell::before {
          content: ''; position: absolute; pointer-events: none; z-index: 0;
          width: 3px; height: 3px; border-radius: 50%; bottom: 10px; left: 50%;
          background: rgba(var(--appliance-color), 0.7);
          box-shadow: -12px 15px 0 1px rgba(var(--appliance-color), 0.4), 10px 25px 0 0.5px rgba(var(--appliance-color), 0.5);
          animation: evaporate-up 3s cubic-bezier(0.2, 0.8, 0.2, 1) infinite;
        }
      ` : ''}
      ${is_fan ? `
        #img-cell::before {
          content: ''; position: absolute; pointer-events: none; z-index: 0;
          inset: 0; border-radius: 50%; border: 2px solid rgba(var(--appliance-color), 0.5);
          animation: air-ripple var(--appliance-speed) cubic-bezier(0.1, 0.5, 0.5, 1) infinite;
        }
        #img-cell::after {
          content: ''; position: absolute; pointer-events: none; z-index: 0;
          inset: 0; border-radius: 50%; border: 2px solid rgba(var(--appliance-color), 0.3);
          animation: air-ripple var(--appliance-speed) cubic-bezier(0.1, 0.5, 0.5, 1) infinite;
          animation-delay: calc(var(--appliance-speed) / 2);
        }
      ` : ''}
      ${(is_heat_cool || is_auto) ? `
        #img-cell {
          background: linear-gradient(135deg, rgba(33, 150, 243, 0.15) 0%, rgba(255, 87, 34, 0.15) 100%) !important;
          border: 1px solid rgba(158, 158, 158, 0.2) !important;
        }
        #img-cell::before {
          content: ''; position: absolute; pointer-events: none; z-index: 0;
          inset: -5px; border-radius: 50%;
          background: 
            radial-gradient(circle at 25% 25%, rgba(33, 150, 243, 0.25) 0%, transparent 60%),
            radial-gradient(circle at 75% 75%, rgba(255, 87, 34, 0.25) 0%, transparent 60%);
          animation: auto-breathe 3s ease-in-out infinite alternate;
        }
        #img-cell::after {
          content: ''; position: absolute; pointer-events: none; z-index: 0;
          inset: -15px; border-radius: 50%;
          border: 2px solid transparent;
          border-top-color: rgba(33, 150, 243, 0.4);
          border-left-color: rgba(33, 150, 243, 0.2);
          border-bottom-color: rgba(255, 87, 34, 0.4);
          border-right-color: rgba(255, 87, 34, 0.2);
          animation: auto-ripple 3s cubic-bezier(0.4, 0, 0.2, 1) infinite;
        }
      ` : ''}
      
      @keyframes gentle-fire {
        0%   { transform: scaleY(0.95) skewX(-1deg); color: #ff9800; filter: drop-shadow(0 0 2px rgba(255,152,0,0.4)); }
        100% { transform: scaleY(1.05) skewX(1deg); color: #ff5722; filter: drop-shadow(0 0 5px rgba(255,87,34,0.6)); }
      }
      @keyframes gentle-spin {
        0%   { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
      }
      @keyframes frost-orbit {
        0%   { transform: rotate(0deg) scale(1); }
        50%  { transform: rotate(180deg) scale(1.05); }
        100% { transform: rotate(360deg) scale(1); }
      }
      @keyframes intense-updraft {
        0%   { transform: translateY(10px) scale(0.9); opacity: 0.5; }
        100% { transform: translateY(-15px) scale(1.1); opacity: 1; filter: blur(6px); }
      }
      @keyframes intense-embers {
        0%   { transform: translateY(0) scale(1); opacity: 0; }
        15%  { opacity: 1; }
        100% { transform: translateY(-55px) scale(0.3); opacity: 0; }
      }
      @keyframes air-ripple {
        0%   { transform: scale(1); opacity: 0.8; }
        100% { transform: scale(1.5); opacity: 0; }
      }
      @keyframes evaporate-up {
        0%   { transform: translateY(0); opacity: 0; }
        30%  { opacity: 1; }
        100% { transform: translateY(-30px); opacity: 0; }
      }
      @keyframes auto-breathe {
        0%   { transform: scale(0.9); opacity: 0.4; }
        100% { transform: scale(1.1); opacity: 1; }
      }
      @keyframes auto-ripple {
        0%   { transform: scale(0.7); opacity: 0.8; }
        100% { transform: scale(1.2); opacity: 0; }
      }
    `;
  ]]]

```
</details>

<details>
<summary><strong>Air Purifier Card</summary>

```yaml
type: custom:button-card
entity: ""
name: Air Purifier
show_state: false
show_label: true
variables:
  entity_main: ""
  sensor_filter_life: ""
  sensor_air_quality: ""
  max_time: 120
  aqi_low: 25
  aqi_mid: 50
  aqi_high: 100
  state_idle: idle, off, standby, unknown, unavailable
  state_running: on, manual, medium, low, high
  state_auto: auto
  state_sleep: sleep, silent, night, quiet
  state_turbo: turbo, max
  sensor_session_timer: ""
  sensor_power: ""
  size_icon: 45px
  size_card_height: 95px
  font_primary: 15px
  font_secondary: 12px
  font_badge: 11px
styles:
  card:
    - --config-icon-size: '[[[ return variables.size_icon ]]]'
    - --config-shape-size: 65px
    - --config-card-height: '[[[ return variables.size_card_height ]]]'
    - --config-font-primary: '[[[ return variables.font_primary ]]]'
    - --config-font-secondary: '[[[ return variables.font_secondary ]]]'
    - --config-font-badge: '[[[ return variables.font_badge ]]]'
    - height: var(--config-card-height) !important
    - padding: 0px !important
    - overflow: hidden
    - position: relative
    - transition: all 0.8s ease
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
    - color: rgb(var(--appliance-color))
    - z-index: 3
  img_cell:
    - width: var(--config-shape-size)
    - height: var(--config-shape-size)
    - border-radius: 50%
    - border: 1px solid rgba(var(--appliance-color), 0.3) !important
    - background: rgba(var(--appliance-color), 0.05) !important
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
    filter_ring:
      - position: absolute
      - left: 11px
      - top: 50%
      - transform: translateY(-50%)
      - width: 75px
      - height: 75px
      - z-index: 4
      - pointer-events: none
    badge1:
      - position: absolute
      - top: 10px
      - right: 10px
      - padding: 4px 10px
      - font-size: var(--config-font-badge)
      - letter-spacing: 0.5px
      - white-space: nowrap
      - opacity: 0.9
      - text-transform: uppercase
      - font-weight: 600
      - z-index: 5
      - transition: all 0.5s ease
    badge2:
      - position: absolute
      - top: 38px
      - right: 10px
      - padding: 4px 10px
      - font-size: var(--config-font-badge)
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
      - height: 3px
      - width: var(--appliance-level)
      - background: rgb(var(--appliance-color))
      - box-shadow: 0 -1px 6px rgba(var(--appliance-color), 0.5)
      - transition: width 1s cubic-bezier(0.4, 0, 0.2, 1)
      - z-index: 5
tap_action:
  action: more-info
label: |
  [[[ 
    if (!entity) return 'Entity Setup Required';
    if (entity.state === 'off') return 'Off';
    return entity.attributes && entity.attributes.preset_mode 
      ? entity.attributes.preset_mode.replace(/-/g, ' ').replace(/\b\w/g, c => c.toUpperCase())
      : 'On';
  ]]]
icon: mdi:air-purifier
custom_fields:
  filter_ring: |
    [[[
      if (!variables.sensor_filter_life || !states[variables.sensor_filter_life]) return '';
      let pct = parseInt(states[variables.sensor_filter_life].state);
      if (isNaN(pct)) pct = 0;
      let r = 35; 
      let c = 2 * Math.PI * r;
      let offset = c - (pct / 100) * c;
      return `<svg viewBox="0 0 75 75" style="transform: rotate(-90deg); width: 100%; height: 100%;">
        <circle cx="37.5" cy="37.5" r="${r}" fill="none" stroke="rgb(var(--appliance-color))" stroke-width="3"
                stroke-dasharray="${c}" stroke-dashoffset="${offset}" stroke-linecap="round" 
                style="transition: stroke-dashoffset 1s ease-in-out, stroke 0.5s ease;"/>
      </svg>`;
    ]]]
  badge1: ' '
  badge2: ' '
  bar: ' '
extra_styles: |
  [[[
    let ent_status   = variables.entity_main || (entity ? entity.entity_id : null);
    let ent_timerem  = variables.sensor_session_timer;
    let ent_power    = variables.sensor_power; 
    let ent_aqi      = variables.sensor_air_quality;
    let ent_percent  = variables.sensor_filter_life;
    let max_time     = variables.max_time;

    let a_low = variables.aqi_low;
    let a_mid = variables.aqi_mid;
    let a_high = variables.aqi_high;

    let state_idle    = variables.state_idle.split(',').map(s => s.trim().toLowerCase());
    let state_running = variables.state_running.split(',').map(s => s.trim().toLowerCase());
    let state_auto    = variables.state_auto.split(',').map(s => s.trim().toLowerCase());
    let state_sleep   = variables.state_sleep.split(',').map(s => s.trim().toLowerCase());
    let state_turbo   = variables.state_turbo.split(',').map(s => s.trim().toLowerCase());

    let state_obj = ent_status && states[ent_status] ? states[ent_status] : null;
    let base_state = state_obj ? state_obj.state.toLowerCase() : 'unknown';
    
    let active_mode = base_state;
    if (base_state === 'on' && state_obj && state_obj.attributes && state_obj.attributes.preset_mode) {
        active_mode = state_obj.attributes.preset_mode.toLowerCase();
    }
    
    let status_clean = active_mode.replace(/-/g, ' ').replace(/\b\w/g, c => c.toUpperCase());
    let s_lower = active_mode;

    let raw_val = states[ent_timerem];
    let time_rem = NaN;
    
    if (raw_val && raw_val.state !== 'unavailable' && raw_val.state !== 'unknown') {
        let state_str = raw_val.state.trim();
        let attrs = raw_val.attributes || {};
        let uom = attrs.unit_of_measurement ? attrs.unit_of_measurement.toLowerCase() : '';

        if (state_str === 'active' && attrs.finishes_at) {
            let finish_time = new Date(attrs.finishes_at).getTime();
            let now = new Date().getTime();
            time_rem = finish_time > now ? (finish_time - now) / 60000 : 0;
        }
        else if (state_str.includes('-') && state_str.includes('T')) {
            let finish_time = new Date(state_str).getTime();
            let now = new Date().getTime();
            time_rem = finish_time > now ? (finish_time - now) / 60000 : 0;
        }
        else if (state_str.includes(':')) {
            let parts = state_str.split(':');
            time_rem = (parseInt(parts[0]) * 60) + parseInt(parts[1]); 
        }

        else {
            let parsed_val = parseFloat(state_str) || 0;
            if (uom === 'h' || uom === 'hours' || uom === 'hour') {
                time_rem = parsed_val * 60;
            } else if (uom === 's' || uom === 'seconds' || uom === 'second') {
                time_rem = parsed_val / 60;
            } else {
                time_rem = parsed_val; 
            }
        }
    }

    let raw_power = states[ent_power] ? parseFloat(states[ent_power].state) : NaN;
    let raw_aqi = states[ent_aqi] ? parseFloat(states[ent_aqi].state) : NaN;
    let raw_pct = states[ent_percent] ? parseFloat(states[ent_percent].state) : NaN;

    let progress = 0; 
    if (!state_idle.includes(s_lower) && !isNaN(time_rem)) {
        let safe_max = Math.max(parseFloat(max_time), time_rem);
        progress = time_rem > 0 ? Math.max(5, Math.floor(((safe_max - time_rem) / safe_max) * 100)) : 100;
    }
    progress = Math.max(0, Math.min(100, progress));

    let color = '41, 182, 246'; let duration = '6s';
    if (state_idle.includes(s_lower)) { color = '158, 158, 158'; duration = '0s'; }
    else if (state_turbo.includes(s_lower)) { color = '255, 112, 67'; duration = '4s'; }
    else if (state_auto.includes(s_lower)) { color = '38, 166, 154'; duration = '6s'; }
    else if (state_sleep.includes(s_lower)) { color = '233, 30, 99'; duration = '6s'; }

    let aqi_color = '76, 175, 80'; 
    if (!isNaN(raw_aqi)) {
        if (raw_aqi > a_high) aqi_color = '244, 67, 54'; 
        else if (raw_aqi > a_mid) aqi_color = '255, 152, 0'; 
        else if (raw_aqi > a_low) aqi_color = '255, 235, 59';
    }

    let b1_arr = [status_clean];
    if (!isNaN(raw_aqi)) b1_arr.push(`AQI ${Math.round(raw_aqi)}`);
    let badge1_text = b1_arr.join(' • ');

    let b2_arr = [];
    if (!state_idle.includes(s_lower) && !isNaN(time_rem) && time_rem > 0) {
        b2_arr.push(`${Math.floor(time_rem/60)}h ${(Math.floor(time_rem)%60).toString().padStart(2,'0')}m`);
    }
    if (!isNaN(raw_power)) b2_arr.push(`${Math.round(raw_power)}W`);
    let badge2_text = b2_arr.join(' • ');

    return `
      #card { 
        --appliance-color: ${color}; 
        --appliance-level: ${progress}%; 
        --appliance-duration: ${duration}; 
      }
      
      #bar {
        display: ${isNaN(time_rem) ? 'none' : 'block'};
      }
      
      #badge1 {
        display: block;
        background: linear-gradient(90deg, rgba(${color}, 0.15) 30%, rgba(${aqi_color}, 0.2) 75%);
        color: var(--primary-text-color, #fff);
        border-top: 1px solid rgba(128,128,128, 0.2);
        border-bottom: 1px solid rgba(128,128,128, 0.2);
        border-left: 2.5px solid rgb(${color});
        border-right: 2.5px solid rgb(${aqi_color});
        border-radius: 6px !important;
      }
      #badge1::before { content: "${badge1_text}"; } 

      #badge2 {
        display: ${badge2_text !== '' ? 'block' : 'none'};
        background: rgba(${color}, 0.07);
        color: var(--primary-text-color, #fff);
        border-top: 1px solid rgba(128,128,128, 0.2);
        border-bottom: 1px solid rgba(128,128,128, 0.2);
        border-left: 2.5px solid rgb(${color});
        border-radius: 6px !important;
      }
      #badge2::before { content: "${badge2_text}"; } 

      #img-cell::before {
        content: ''; position: absolute; top: 50%; left: 50%; width: 6px; height: 6px; border-radius: 50%;
        transform: translate(-50%, -50%); animation: bad-air-suck var(--appliance-duration) ease-in infinite;
        pointer-events: none; z-index: 0; display: ${duration === '0s' ? 'none' : 'block'};
      }

      #img-cell::after {
        content: ''; position: absolute; inset: 0; border-radius: 50%;
        animation: good-air-push var(--appliance-duration) ease-out infinite;
        pointer-events: none; z-index: 0; display: ${duration === '0s' ? 'none' : 'block'};
      }

      @keyframes bad-air-suck {
        0% { box-shadow: -45px -35px 0 -1px rgba(150,150,150,0.8), 55px -20px 0 -2px rgba(130,130,130,0.6), 35px 45px 0 0px rgba(160,160,160,0.7), -40px 50px 0 -1px rgba(140,140,140,0.5), 10px -60px 0 -2px rgba(150,150,150,0.8), -55px 10px 0 -1px rgba(120,120,120,0.6), 65px 20px 0 -1px rgba(145,145,145,0.7), -25px -55px 0 -2px rgba(135,135,135,0.5), 45px -45px 0 0px rgba(155,155,155,0.6), -15px 65px 0 -1px rgba(160,160,160,0.8), 70px -10px 0 -2px rgba(125,125,125,0.5), -65px -15px 0 0px rgba(150,150,150,0.7), 0px -80px 0 -1px rgba(140,140,140,0.6), -80px 0px 0 -2px rgba(155,155,155,0.7), 80px 40px 0 -1px rgba(130,130,130,0.5), 30px 80px 0 0px rgba(160,160,160,0.8), -60px -50px 0 -2px rgba(145,145,145,0.6), 60px 60px 0 -1px rgba(150,150,150,0.7), -75px 40px 0 0px rgba(125,125,125,0.8), 45px -75px 0 -2px rgba(140,140,140,0.5), -25px -85px 0 -1px rgba(135,135,135,0.6), 85px 10px 0 0px rgba(155,155,155,0.7), 10px 85px 0 -2px rgba(160,160,160,0.6), -85px -30px 0 -1px rgba(145,145,145,0.8); opacity: 0; }
        5% { opacity: 1; }
        60% { box-shadow: 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent, 0 0 0 -3px transparent; opacity: 0; }
        100% { box-shadow: 0 0 0 -3px transparent; opacity: 0; }
      }

      @keyframes good-air-push {
        0%, 55% { box-shadow: 0 0 0 0 rgba(var(--appliance-color), 0.6), 0 0 0 0 rgba(var(--appliance-color), 0.4), 0 0 0 0 rgba(var(--appliance-color), 0.2); opacity: 0; }
        60% { box-shadow: 0 0 0 0 rgba(var(--appliance-color), 0.7), 0 0 0 0 rgba(var(--appliance-color), 0.5), 0 0 0 0 rgba(var(--appliance-color), 0.3); opacity: 1; }
        95%, 100% { box-shadow: 0 0 0 400px rgba(var(--appliance-color), 0), 0 0 0 300px rgba(var(--appliance-color), 0), 0 0 0 200px rgba(var(--appliance-color), 0); opacity: 0; }
      }
    `;
  ]]]

```
</details>

<details>
<summary><strong>Smart Humidifier Card</summary>

```yaml
type: custom:button-card
entity: 
name: Smart Humidifier
show_state: false
show_label: true
variables:
  entity_humidifier: ''
  sensor_humidity: ''
  hum_low: 35
  hum_high: 60
  state_idle: idle, off, standby, unknown, unavailable
  state_running: on, humidifying, manual, medium, low, high
  state_auto: auto, eco
  state_sleep: sleep, silent, night, quiet
  state_turbo: turbo, max
  sensor_water_level: ''
  sensor_session_timer: ''
  sensor_power: ''
  bar_source: timer
  max_time: 120
  size_icon: 45px
  size_shape: 65px
  size_card_height: 95px
  font_primary: 15px
  font_secondary: 12px
  font_badge: 11px
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
    - transition: all 0.8s ease
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
    - color: rgb(var(--appliance-color))
    - z-index: 3
  img_cell:
    - width: var(--config-shape-size)
    - height: var(--config-shape-size)
    - border-radius: 50%
    - border: 1px solid rgba(var(--appliance-color), 0.3) !important
    - background: rgba(var(--appliance-color), 0.05) !important
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
    badge1:
      - position: absolute
      - top: 10px
      - right: 10px
      - padding: 4px 10px
      - font-size: var(--config-font-badge)
      - letter-spacing: 0.5px
      - white-space: nowrap
      - opacity: 0.9
      - text-transform: uppercase
      - font-weight: 600
      - z-index: 5
      - transition: all 0.5s ease
    badge2:
      - position: absolute
      - top: 38px
      - right: 10px
      - padding: 4px 10px
      - font-size: var(--config-font-badge)
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
      - height: 3px
      - width: var(--appliance-level)
      - background: rgb(var(--appliance-color))
      - box-shadow: 0 -1px 6px rgba(var(--appliance-color), 0.5)
      - transition: width 1s cubic-bezier(0.4, 0, 0.2, 1)
      - z-index: 5
tap_action:
  action: more-info
label: |
  [[[ 
    if (!entity) return 'Entity Setup Required';
    if (entity.state === 'off') return 'Off';
    
    let attrs = entity.attributes;
    if (attrs && attrs.action && attrs.action !== 'idle') {
       return attrs.action.charAt(0).toUpperCase() + attrs.action.slice(1);
    }
    
    return attrs && attrs.mode 
      ? attrs.mode.replace(/-/g, ' ').replace(/\b\w/g, c => c.toUpperCase())
      : 'On';
  ]]]
icon: mdi:air-humidifier
custom_fields:
  badge1: ' '
  badge2: ' '
  bar: ' '
extra_styles: |
  [[[
    let ent_status = variables.entity_humidifier || (entity ? entity.entity_id : null);
    let ent_water = variables.sensor_water_level;
    let ent_timerem = variables.sensor_session_timer;
    let ent_power = variables.sensor_power;

    let h_low = variables.hum_low;
    let h_high = variables.hum_high;

    let state_idle = variables.state_idle.split(',').map(s => s.trim().toLowerCase());
    let state_running = variables.state_running.split(',').map(s => s.trim().toLowerCase());
    let state_auto = variables.state_auto.split(',').map(s => s.trim().toLowerCase());
    let state_sleep = variables.state_sleep.split(',').map(s => s.trim().toLowerCase());
    let state_turbo = variables.state_turbo.split(',').map(s => s.trim().toLowerCase());

    let state_obj = ent_status && states[ent_status] ? states[ent_status] : null;
    let base_state = state_obj ? state_obj.state.toLowerCase() : 'unknown';
    
    let active_mode = base_state;
    if (base_state === 'on' && state_obj && state_obj.attributes) {
        if (state_obj.attributes.action && state_obj.attributes.action !== 'idle') {
            active_mode = state_obj.attributes.action.toLowerCase();
        } else if (state_obj.attributes.mode) {
            active_mode = state_obj.attributes.mode.toLowerCase();
        }
    }

    let status_clean = active_mode.replace(/-/g, ' ').replace(/\b\w/g, c => c.toUpperCase());
    let s_lower = active_mode;

    let raw_hum = NaN;
    if (variables.sensor_humidity && states[variables.sensor_humidity]) {
        raw_hum = parseFloat(states[variables.sensor_humidity].state);
    } else if (state_obj && state_obj.attributes && state_obj.attributes.current_humidity !== undefined) {
        raw_hum = parseFloat(state_obj.attributes.current_humidity);
    }

    let raw_power = states[ent_power] ? parseFloat(states[ent_power].state) : NaN;
    let raw_water = states[ent_water] ? parseFloat(states[ent_water].state) : NaN;

    let raw_val = states[ent_timerem];
    let time_rem = NaN;
    
    if (raw_val && raw_val.state !== 'unavailable' && raw_val.state !== 'unknown') {
        let state_str = raw_val.state.trim();
        let attrs = raw_val.attributes || {};
        let uom = attrs.unit_of_measurement ? attrs.unit_of_measurement.toLowerCase() : '';

        if (state_str === 'active' && attrs.finishes_at) {
            let finish_time = new Date(attrs.finishes_at).getTime();
            let now = new Date().getTime();
            time_rem = finish_time > now ? (finish_time - now) / 60000 : 0;
        }
        else if (state_str.includes('-') && state_str.includes('T')) {
            let finish_time = new Date(state_str).getTime();
            let now = new Date().getTime();
            time_rem = finish_time > now ? (finish_time - now) / 60000 : 0;
        }
        else if (state_str.includes(':')) {
            let parts = state_str.split(':');
            time_rem = (parseInt(parts[0]) * 60) + parseInt(parts[1]); 
        }
        else {
            let parsed_val = parseFloat(state_str) || 0;
            if (uom === 'h' || uom === 'hours' || uom === 'hour') {
                time_rem = parsed_val * 60;
            } else if (uom === 's' || uom === 'seconds' || uom === 'second') {
                time_rem = parsed_val / 60;
            } else {
                time_rem = parsed_val; 
            }
        }
    }

    let progress = 0;
    let bar_display = 'none';

    if (variables.bar_source === 'timer') {
        if (!state_idle.includes(s_lower) && !isNaN(time_rem) && time_rem > 0) {
            let max_t = parseFloat(variables.max_time) || 120;
            let safe_max = Math.max(max_t, time_rem);
            progress = Math.max(5, Math.floor(((safe_max - time_rem) / safe_max) * 100));
            bar_display = 'block';
        }
    } else {
        if (!isNaN(raw_water)) {
            progress = Math.max(0, Math.min(100, raw_water));
            bar_display = 'block';
        }
    }

    let color = '41, 182, 246';
    let duration = '3s';

    if (state_idle.includes(s_lower)) {
      color = '158, 158, 158';
      duration = '0s';
    } else if (state_turbo.includes(s_lower)) {
      color = '33, 150, 243';
      duration = '2s';
    } else if (state_auto.includes(s_lower)) {
      color = '38, 166, 154';
      duration = '3s';
    } else if (state_sleep.includes(s_lower)) {
      color = '179, 136, 255';
      duration = '5s';
    }

    let hum_color = '76, 175, 80';

    if (!isNaN(raw_hum)) {
      if (raw_hum < h_low) {
        hum_color = '255, 152, 0';
      } else if (raw_hum > h_high) {
        hum_color = '33, 150, 243';
      }
    }

    let b1_arr = [status_clean];
    if (!isNaN(raw_hum)) {
      b1_arr.push(`Hum ${Math.round(raw_hum)}%`);
    }
    let badge1_text = b1_arr.join(' • ');

    let b2_arr = [];
    
    if (!state_idle.includes(s_lower) && !isNaN(time_rem) && time_rem > 0) {
        b2_arr.push(`${Math.floor(time_rem/60)}h ${(Math.floor(time_rem)%60).toString().padStart(2,'0')}m`);
    }
    
    if (!isNaN(raw_water)) {
      b2_arr.push(`Tank ${Math.round(raw_water)}%`);
    }

    if (!isNaN(raw_power)) {
      b2_arr.push(`${Math.round(raw_power)}W`);
    }

    let badge2_text = b2_arr.join(' • ');

    return `
      #card {
        --appliance-color: ${color};
        --appliance-level: ${progress}%;
        --appliance-duration: ${duration};
      }

      #bar {
        display: ${bar_display};
      }

      #badge1 {
        display: block;
        background: linear-gradient(
          90deg,
          rgba(${color}, 0.15) 30%,
          rgba(${hum_color}, 0.2) 75%
        );
        color: var(--primary-text-color, #fff);
        border-top: 1px solid rgba(128,128,128, 0.2);
        border-bottom: 1px solid rgba(128,128,128, 0.2);
        border-left: 2.5px solid rgb(${color});
        border-right: 2.5px solid rgb(${hum_color});
        border-radius: 6px !important;
      }

      #badge1::before {
        content: "${badge1_text}";
      }

      #badge2 {
        display: ${badge2_text !== '' ? 'block' : 'none'};
        background: rgba(${color}, 0.07);
        color: var(--primary-text-color, #fff);
        border-top: 1px solid rgba(128,128,128, 0.2);
        border-bottom: 1px solid rgba(128,128,128, 0.2);
        border-left: 2.5px solid rgb(${color});
        border-radius: 6px !important;
      }

      #badge2::before {
        content: "${badge2_text}";
      }

      #img-cell::before,
      #img-cell::after {
        content: '';
        position: absolute;
        top: 50%;
        left: 50%;
        width: 18px;
        height: 18px;
        border-radius: 50%;
        pointer-events: none;
        z-index: 0;
        display: ${duration === '0s' ? 'none' : 'block'};
        animation: realistic-steam var(--appliance-duration) linear infinite;
        background: rgba(var(--appliance-color), 0.75);
        filter: blur(8px);
        box-shadow: 0 0 12px 6px rgba(var(--appliance-color), 0.8);
      }

      #img-cell::after {
        animation-delay: calc(var(--appliance-duration) / -2);
      }

      @keyframes realistic-steam {
        0% {
          top: 60%;
          transform: translate(-50%, 0) scale(0.6) rotate(0deg);
          opacity: 0;
        }

        20% {
          opacity: 1;
        }

        50% {
          transform: translate(-50%, -20px) scale(1.6) rotate(-5deg);
          opacity: 0.9;
        }

        100% {
          top: -15px;
          transform: translate(-50%, -45px) scale(3.2) rotate(15deg);
          opacity: 0;
        }
      }
    `;
  ]]]

```
</details>

<details>
<summary><strong>Smart Dehumidifier Card</summary>

```yaml
type: custom:button-card
entity: 
name: Smart Dehumidifier
show_state: false
show_label: true
variables:
  entity_dehumidifier: ''
  sensor_humidity: ''
  hum_low: 40
  hum_high: 60
  state_idle: idle, off, standby, unknown, unavailable
  state_running: on, drying, manual, medium, low, high
  state_auto: auto, eco
  state_sleep: sleep, silent, night, quiet
  state_turbo: turbo, max
  sensor_water_level: ''
  sensor_session_timer: ''
  sensor_power: ''
  bar_source: timer
  max_time: 120
  size_icon: 45px
  size_shape: 65px
  size_card_height: 95px
  font_primary: 15px
  font_secondary: 12px
  font_badge: 11px
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
    - transition: all 0.8s ease
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
    - color: rgb(var(--appliance-color))
    - z-index: 3
  img_cell:
    - width: var(--config-shape-size)
    - height: var(--config-shape-size)
    - border-radius: 50%
    - border: 1px solid rgba(var(--appliance-color), 0.3) !important
    - background: rgba(var(--appliance-color), 0.05) !important
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
    badge1:
      - position: absolute
      - top: 10px
      - right: 10px
      - padding: 4px 10px
      - font-size: var(--config-font-badge)
      - letter-spacing: 0.5px
      - white-space: nowrap
      - opacity: 0.9
      - text-transform: uppercase
      - font-weight: 600
      - z-index: 5
      - transition: all 0.5s ease
    badge2:
      - position: absolute
      - top: 38px
      - right: 10px
      - padding: 4px 10px
      - font-size: var(--config-font-badge)
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
      - height: 3px
      - width: var(--appliance-level)
      - background: rgb(var(--appliance-color))
      - box-shadow: 0 -1px 6px rgba(var(--appliance-color), 0.5)
      - transition: width 1s cubic-bezier(0.4, 0, 0.2, 1)
      - z-index: 5
    drip1:
      - position: absolute
      - left: 22%
      - top: -15px
      - width: 5px
      - height: 11px
      - z-index: 0
    drip2:
      - position: absolute
      - left: 45%
      - top: -15px
      - width: 6px
      - height: 14px
      - z-index: 0
    drip3:
      - position: absolute
      - left: 82%
      - top: -15px
      - width: 4px
      - height: 10px
      - z-index: 0
tap_action:
  action: more-info
label: |
  [[[ 
    if (!entity) return 'Entity Setup Required';
    if (entity.state === 'off') return 'Off';
    
    let attrs = entity.attributes;
    if (attrs && attrs.action && attrs.action !== 'idle') {
       return attrs.action.charAt(0).toUpperCase() + attrs.action.slice(1);
    }
    
    return attrs && attrs.mode 
      ? attrs.mode.replace(/-/g, ' ').replace(/\b\w/g, c => c.toUpperCase())
      : 'On';
  ]]]
icon: mdi:water-minus
custom_fields:
  badge1: ' '
  badge2: ' '
  bar: ' '
  drip1: ' '
  drip2: ' '
  drip3: ' '
extra_styles: |
  [[[
    let ent_status = variables.entity_dehumidifier || (entity ? entity.entity_id : null);
    let ent_water = variables.sensor_water_level;
    let ent_timerem = variables.sensor_session_timer;
    let ent_power = variables.sensor_power;

    let h_low = variables.hum_low;
    let h_high = variables.hum_high;

    let state_idle = variables.state_idle.split(',').map(s => s.trim().toLowerCase());
    let state_running = variables.state_running.split(',').map(s => s.trim().toLowerCase());
    let state_auto = variables.state_auto.split(',').map(s => s.trim().toLowerCase());
    let state_sleep = variables.state_sleep.split(',').map(s => s.trim().toLowerCase());
    let state_turbo = variables.state_turbo.split(',').map(s => s.trim().toLowerCase());

    let state_obj = ent_status && states[ent_status] ? states[ent_status] : null;
    let base_state = state_obj ? state_obj.state.toLowerCase() : 'unknown';
    
    let active_mode = base_state;
    if (base_state === 'on' && state_obj && state_obj.attributes) {
        if (state_obj.attributes.action && state_obj.attributes.action !== 'idle') {
            active_mode = state_obj.attributes.action.toLowerCase();
        } else if (state_obj.attributes.mode) {
            active_mode = state_obj.attributes.mode.toLowerCase();
        }
    }

    let status_clean = active_mode.replace(/-/g, ' ').replace(/\b\w/g, c => c.toUpperCase());
    let s_lower = active_mode;

    let raw_hum = NaN;
    if (variables.sensor_humidity && states[variables.sensor_humidity]) {
        raw_hum = parseFloat(states[variables.sensor_humidity].state);
    } else if (state_obj && state_obj.attributes && state_obj.attributes.current_humidity !== undefined) {
        raw_hum = parseFloat(state_obj.attributes.current_humidity);
    }

    let raw_power = states[ent_power] ? parseFloat(states[ent_power].state) : NaN;
    let raw_water = states[ent_water] ? parseFloat(states[ent_water].state) : NaN;

    let raw_val = states[ent_timerem];
    let time_rem = NaN;
    
    if (raw_val && raw_val.state !== 'unavailable' && raw_val.state !== 'unknown') {
        let state_str = raw_val.state.trim();
        let attrs = raw_val.attributes || {};
        let uom = attrs.unit_of_measurement ? attrs.unit_of_measurement.toLowerCase() : '';

        if (state_str === 'active' && attrs.finishes_at) {
            let finish_time = new Date(attrs.finishes_at).getTime();
            let now = new Date().getTime();
            time_rem = finish_time > now ? (finish_time - now) / 60000 : 0;
        }
        else if (state_str.includes('-') && state_str.includes('T')) {
            let finish_time = new Date(state_str).getTime();
            let now = new Date().getTime();
            time_rem = finish_time > now ? (finish_time - now) / 60000 : 0;
        }
        else if (state_str.includes(':')) {
            let parts = state_str.split(':');
            time_rem = (parseInt(parts[0]) * 60) + parseInt(parts[1]); 
        }
        else {
            let parsed_val = parseFloat(state_str) || 0;
            if (uom === 'h' || uom === 'hours' || uom === 'hour') {
                time_rem = parsed_val * 60;
            } else if (uom === 's' || uom === 'seconds' || uom === 'second') {
                time_rem = parsed_val / 60;
            } else {
                time_rem = parsed_val; 
            }
        }
    }

    let progress = 0;
    let bar_display = 'none';

    if (variables.bar_source === 'timer') {
        if (!state_idle.includes(s_lower) && !isNaN(time_rem) && time_rem > 0) {
            let max_t = parseFloat(variables.max_time) || 120;
            let safe_max = Math.max(max_t, time_rem);
            progress = Math.max(5, Math.floor(((safe_max - time_rem) / safe_max) * 100));
            bar_display = 'block';
        }
    } else {
        if (!isNaN(raw_water)) {
            progress = Math.max(0, Math.min(100, raw_water));
            bar_display = 'block';
        }
    }

    let is_on = !state_idle.includes(s_lower);
    let color = '41, 182, 246';
    let duration = '2s';

    if (!is_on) {
      color = '158, 158, 158';
      duration = '0s';
    } else if (s_lower === 'full' || raw_water >= 100) {
      color = '244, 67, 54';
      duration = '0s';
      status_clean = 'Tank Full';
    } else if (state_turbo.includes(s_lower)) {
      duration = '1.2s';
    } else if (state_auto.includes(s_lower)) {
      duration = '2s';
    } else if (state_sleep.includes(s_lower)) {
      duration = '3.5s';
    }

    let hum_color = '76, 175, 80';

    if (!isNaN(raw_hum)) {
      if (raw_hum > h_high) {
        hum_color = '255, 152, 0';
      } else if (raw_hum < h_low) {
        hum_color = '3, 169, 244';
      }
    }

    let b1_arr = [status_clean];
    if (!isNaN(raw_hum)) {
      b1_arr.push(`Hum ${Math.round(raw_hum)}%`);
    }
    let badge1_text = b1_arr.join(' • ');

    let b2_arr = [];

    if (!state_idle.includes(s_lower) && !isNaN(time_rem) && time_rem > 0) {
        b2_arr.push(`${Math.floor(time_rem/60)}h ${(Math.floor(time_rem)%60).toString().padStart(2,'0')}m`);
    }

    if (!isNaN(raw_water)) {
      b2_arr.push(`Tank ${Math.round(raw_water)}%`);
    }

    if (!isNaN(raw_power)) {
      b2_arr.push(`${Math.round(raw_power)}W`);
    }

    let badge2_text = b2_arr.join(' • ');

    return `
      #card {
        --appliance-color: ${color};
        --appliance-level: ${progress}%;
        --appliance-duration: ${duration};
      }

      #bar {
        display: ${bar_display};
      }

      #badge1 {
        display: block;
        background: linear-gradient(
          90deg,
          rgba(${color}, 0.15) 30%,
          rgba(${hum_color}, 0.2) 75%
        );
        color: var(--primary-text-color, #fff);
        border-top: 1px solid rgba(128,128,128, 0.2);
        border-bottom: 1px solid rgba(128,128,128, 0.2);
        border-left: 2.5px solid rgb(${color});
        border-right: 2.5px solid rgb(${hum_color});
        border-radius: 6px !important;
      }

      #badge1::before {
        content: "${badge1_text}";
      }

      #badge2 {
        display: ${badge2_text !== '' ? 'block' : 'none'};
        background: rgba(${color}, 0.07);
        color: var(--primary-text-color, #fff);
        border-top: 1px solid rgba(128,128,128, 0.2);
        border-bottom: 1px solid rgba(128,128,128, 0.2);
        border-left: 2.5px solid rgb(${color});
        border-radius: 6px !important;
      }

      #badge2::before {
        content: "${badge2_text}";
      }

      #drip1,
      #drip2,
      #drip3,
      #img-cell::after {
        border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
        background: rgba(255, 255, 255, 0.3);
        box-shadow:
          inset 0px 2px 3px rgba(255, 255, 255, 0.8),
          inset 0px -2px 3px rgba(41, 182, 246, 0.4),
          0px 2px 4px rgba(0, 0, 0, 0.2);
        filter: blur(0.8px);
        pointer-events: none;
        display: ${duration === '0s' ? 'none' : 'block'};
        opacity: 0;
      }

      #img-cell::after {
        content: '';
        position: absolute;
        left: 50%;
        top: -15px;
        width: 7px;
        height: 14px;
        animation: window-drip var(--appliance-duration) ease-in infinite;
      }

      #drip1 {
        animation: window-drip calc(var(--appliance-duration) * 1.3) ease-in infinite 0.4s;
      }

      #drip2 {
        animation: window-drip calc(var(--appliance-duration) * 0.9) ease-in infinite 1.1s;
      }

      #drip3 {
        animation: window-drip calc(var(--appliance-duration) * 1.5) ease-in infinite 0.7s;
      }

      @keyframes window-drip {
        0% {
          transform: translateY(0px) scaleY(0.8);
          opacity: 0;
        }

        15% {
          transform: translateY(15px) scaleY(1);
          opacity: 0.9;
        }

        70% {
          transform: translateY(70px) scaleY(1.2);
          opacity: 0.9;
        }

        100% {
          transform: translateY(95px) scaleY(1.5);
          opacity: 0;
        }
      }
    `;
  ]]]

```
</details>

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
