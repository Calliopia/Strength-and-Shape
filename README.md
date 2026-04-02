# Strength-and-Shape
Progressive overload, macro and progress tracker for the gym in a simplistic set up. 
[index (1).html](https://github.com/user-attachments/files/26450126/index.1.html)
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover" />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
  <meta name="apple-mobile-web-app-title" content="Strength & Shape" />
  <meta name="theme-color" content="#0e0c0a" />
  <title>Strength & Shape</title>
  <link rel="manifest" href="data:application/json,{
    &quot;name&quot;:&quot;Strength %26 Shape&quot;,
    &quot;short_name&quot;:&quot;S%26S&quot;,
    &quot;start_url&quot;:&quot;.&quot;,
    &quot;display&quot;:&quot;standalone&quot;,
    &quot;background_color&quot;:&quot;%230e0c0a&quot;,
    &quot;theme_color&quot;:&quot;%230e0c0a&quot;,
    &quot;icons&quot;:[{&quot;src&quot;:&quot;data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 192 192'%3E%3Crect width='192' height='192' fill='%230e0c0a'/%3E%3Ccircle cx='96' cy='96' r='70' fill='none' stroke='%23c8a882' stroke-width='8'/%3E%3Ctext x='96' y='112' text-anchor='middle' font-size='64' fill='%23c8a882'%3E💪%3C/text%3E%3C/svg%3E&quot;,&quot;sizes&quot;:&quot;192x192&quot;,&quot;type&quot;:&quot;image/svg+xml&quot;}]
  }" />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;500;600&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet" />
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
    body { background: #0e0c0a; color: #f0e8de; font-family: 'Cormorant Garamond', Georgia, serif; overscroll-behavior: none; }
    input[type=number]::-webkit-inner-spin-button, input[type=number]::-webkit-outer-spin-button { -webkit-appearance: none; }
    input { -webkit-appearance: none; appearance: none; }
    ::-webkit-scrollbar { display: none; }
    .app { max-width: 480px; margin: 0 auto; min-height: 100vh; min-height: 100dvh; }
    .header { padding: calc(env(safe-area-inset-top) + 24px) 24px 16px; border-bottom: 1px solid #1e1c1a; background: linear-gradient(180deg, #141210 0%, #0e0c0a 100%); }
    .header-label { font-size: 10px; letter-spacing: 0.2em; color: #c8a882; font-family: 'DM Mono', monospace; margin-bottom: 4px; }
    .header-title { font-size: 26px; font-weight: 600; letter-spacing: -0.02em; line-height: 1.1; }
    .header-sub { font-size: 12px; color: #888; margin-top: 4px; font-family: 'DM Mono', monospace; }
    .stat-row { margin-top: 10px; display: flex; gap: 12px; }
    .stat-box { background: rgba(200,168,130,0.1); border: 1px solid rgba(200,168,130,0.2); border-radius: 8px; padding: 6px 12px; }
    .stat-box.blue { background: rgba(139,168,200,0.1); border-color: rgba(139,168,200,0.2); }
    .stat-label { font-size: 10px; color: #888; font-family: 'DM Mono', monospace; }
    .stat-val { font-size: 18px; color: #c8a882; font-weight: 600; }
    .stat-box.blue .stat-val { color: #8ba8c8; }
    .stat-val span { font-size: 11px; }
    .tab-bar { display: flex; border-bottom: 1px solid #1e1c1a; background: #0e0c0a; position: sticky; top: 0; z-index: 10; }
    .tab-btn { flex: 1; padding: 12px 4px; font-size: 11px; font-family: 'DM Mono', monospace; letter-spacing: 0.05em; background: transparent; border: none; border-bottom: 2px solid transparent; color: #666; cursor: pointer; transition: all 0.2s; }
    .tab-btn.active { border-bottom-color: #c8a882; color: #c8a882; }
    .content { padding: 20px 20px calc(env(safe-area-inset-bottom) + 80px); }
    .day-selector { display: flex; gap: 8px; margin-bottom: 20px; flex-wrap: wrap; }
    .day-btn { padding: 8px 14px; border-radius: 8px; font-size: 12px; font-family: 'DM Mono', monospace; border: 1px solid #2a2826; background: transparent; color: #666; cursor: pointer; transition: all 0.2s; }
    .day-btn.active-gold { border-color: #c8a882; background: rgba(200,168,130,0.13); color: #c8a882; }
    .day-btn.active-blue { border-color: #8ba8c8; background: rgba(139,168,200,0.13); color: #8ba8c8; }
    .day-header { margin-bottom: 20px; }
    .day-header-label { font-size: 11px; letter-spacing: 0.1em; font-family: 'DM Mono', monospace; margin-bottom: 4px; }
    .day-header-title { font-size: 24px; font-weight: 600; }
    .day-header-sub { font-size: 14px; color: #888; margin-top: 2px; }
    .ex-card { border: 1px solid #1e1c1a; border-radius: 12px; margin-bottom: 10px; overflow: hidden; transition: all 0.2s; background: rgba(255,255,255,0.03); }
    .ex-card.done { background: rgba(200,168,130,0.06); border-color: rgba(200,168,130,0.3); }
    .ex-header { padding: 14px 16px; cursor: pointer; display: flex; align-items: center; justify-content: space-between; }
    .ex-name { font-size: 15px; font-weight: 500; display: flex; align-items: center; gap: 8px; }
    .ex-done-badge { font-size: 11px; color: #c8a882; }
    .ex-meta { font-size: 12px; color: #666; font-family: 'DM Mono', monospace; margin-top: 2px; }
    .ex-arrow { color: #555; font-size: 14px; }
    .ex-body { padding: 0 16px 16px; border-top: 1px solid #1e1c1a; }
    .cue-box { margin: 12px 0 14px; padding: 10px 12px; background: rgba(200,168,130,0.08); border-left: 2px solid #c8a882; border-radius: 0 6px 6px 0; }
    .cue-label { font-size: 10px; color: #c8a882; font-family: 'DM Mono', monospace; margin-bottom: 4px; }
    .cue-text { font-size: 13px; color: #d4c4b0; line-height: 1.5; }
    .sets-label { font-size: 11px; color: #666; font-family: 'DM Mono', monospace; margin-bottom: 10px; }
    .set-row { display: flex; align-items: center; gap: 8px; margin-bottom: 6px; }
    .set-num { width: 20px; font-size: 11px; color: #888; font-family: 'DM Mono', monospace; }
    .set-input { width: 60px; padding: 5px 8px; background: rgba(255,255,255,0.05); border: 1px solid #333; border-radius: 6px; color: #f0e8de; font-size: 12px; font-family: 'DM Mono', monospace; outline: none; text-align: center; }
    .set-check { width: 28px; height: 28px; border-radius: 50%; border: 2px solid #444; background: transparent; cursor: pointer; display: flex; align-items: center; justify-content: center; font-size: 12px; transition: all 0.2s; flex-shrink: 0; color: #0e0c0a; }
    .set-check.checked { border-color: #c8a882; background: #c8a882; }
    .card { background: rgba(255,255,255,0.03); border: 1px solid #1e1c1a; border-radius: 12px; padding: 16px; margin-bottom: 16px; }
    .card-label { font-size: 11px; color: #888; font-family: 'DM Mono', monospace; margin-bottom: 12px; }
    .card-note { font-size: 12px; color: #666; margin-bottom: 12px; line-height: 1.5; }
    .two-col { display: flex; gap: 10px; margin-bottom: 16px; }
    .two-col .stat-box { flex: 1; }
    .wide-input { width: 100%; padding: 8px 12px; background: rgba(255,255,255,0.05); border: 1px solid #333; border-radius: 8px; color: #f0e8de; font-size: 14px; font-family: 'Cormorant Garamond', Georgia, serif; outline: none; margin-bottom: 8px; }
    .row-input { display: flex; gap: 8px; margin-bottom: 8px; }
    .row-input .set-input { flex: 1; width: auto; text-align: left; padding: 8px 12px; }
    .primary-btn { width: 100%; padding: 12px; background: rgba(200,168,130,0.15); border: 1px solid rgba(200,168,130,0.4); border-radius: 8px; color: #c8a882; font-size: 13px; font-family: 'DM Mono', monospace; letter-spacing: 0.1em; cursor: pointer; transition: all 0.2s; }
    .primary-btn:active { background: rgba(200,168,130,0.25); }
    .section-label { font-size: 11px; color: #888; font-family: 'DM Mono', monospace; margin-bottom: 10px; }
    .food-entry { background: rgba(255,255,255,0.02); border: 1px solid #1e1c1a; border-radius: 8px; padding: 10px 14px; margin-bottom: 8px; display: flex; justify-content: space-between; align-items: center; }
    .food-name { font-size: 14px; }
    .food-note { font-size: 11px; color: #666; }
    .food-cal { font-size: 13px; color: #c8a882; font-family: 'DM Mono', monospace; text-align: right; }
    .food-prot { font-size: 11px; color: #8ba8c8; font-family: 'DM Mono', monospace; text-align: right; }
    .weight-row { display: flex; justify-content: space-between; align-items: center; padding: 10px 14px; background: rgba(255,255,255,0.02); border: 1px solid #1e1c1a; border-radius: 8px; margin-bottom: 8px; }
    .weight-val { font-size: 18px; font-weight: 500; }
    .weight-val span { font-size: 12px; color: #888; }
    .weight-date { font-size: 11px; color: #666; font-family: 'DM Mono', monospace; }
    .weight-diff { font-size: 13px; font-family: 'DM Mono', monospace; text-align: right; }
    .weight-diff.down { color: #8bc8a0; }
    .weight-diff.up { color: #c88a8a; }
    .weight-goal { font-size: 11px; color: #555; text-align: right; }
    .empty { text-align: center; padding: 40px 20px; color: #444; }
    .empty-icon { font-size: 32px; margin-bottom: 10px; }
    .progress-card { background: rgba(255,255,255,0.03); border: 1px solid #1e1c1a; border-radius: 12px; padding: 14px 16px; margin-bottom: 10px; }
    .progress-top { display: flex; justify-content: space-between; margin-bottom: 8px; align-items: center; }
    .progress-title { font-size: 14px; font-weight: 500; }
    .progress-day { font-size: 11px; color: #666; font-family: 'DM Mono', monospace; }
    .progress-pct { font-size: 20px; font-weight: 600; font-family: 'DM Mono', monospace; }
    .progress-bar-bg { height: 4px; background: #1e1c1a; border-radius: 2px; }
    .progress-bar-fill { height: 100%; border-radius: 2px; transition: width 0.3s; }
    .progress-sets { font-size: 11px; color: #555; margin-top: 6px; font-family: 'DM Mono', monospace; }
    .info-card { border-radius: 12px; padding: 16px; margin-top: 12px; }
    .info-card.gold { background: rgba(200,168,130,0.06); border: 1px solid rgba(200,168,130,0.2); }
    .info-card.blue { background: rgba(139,168,200,0.06); border: 1px solid rgba(139,168,200,0.2); }
    .info-label { font-size: 10px; font-family: 'DM Mono', monospace; margin-bottom: 8px; }
    .info-card.gold .info-label { color: #c8a882; }
    .info-card.blue .info-label { color: #8ba8c8; }
    .info-text { font-size: 13px; line-height: 1.6; }
    .info-card.gold .info-text { color: #d4c4b0; }
    .info-card.blue .info-text { color: #b0c4d8; }
    .diet-card { background: rgba(139,168,200,0.06); border: 1px solid rgba(139,168,200,0.2); border-radius: 12px; padding: 14px 16px; margin-bottom: 20px; }
    .diet-label { font-size: 10px; color: #8ba8c8; font-family: 'DM Mono', monospace; margin-bottom: 10px; }
    .diet-item { font-size: 13px; color: #b0c4d8; margin-bottom: 4px; display: flex; gap: 8px; }
    .diet-dash { color: #8ba8c8; }
    .flex-row { display: flex; gap: 10px; }
    .flex-row .set-input { flex: 1; width: auto; text-align: left; padding: 10px 14px; }
    .flex-row .primary-btn { width: auto; margin: 0; padding: 10px 20px; }
  </style>
</head>
<body>
<div class="app">
  <div class="header">
    <div class="header-label">YOUR PROGRAM</div>
    <h1 class="header-title">Strength & Shape</h1>
    <div class="header-sub">Goal: 145 lbs · Glutes · Core</div>
    <div class="stat-row" id="stat-row" style="display:none">
      <div class="stat-box">
        <div class="stat-label">CURRENT</div>
        <div class="stat-val" id="stat-current">— <span>lbs</span></div>
      </div>
      <div class="stat-box blue">
        <div class="stat-label">TO GOAL</div>
        <div class="stat-val" id="stat-goal">— <span>lbs</span></div>
      </div>
    </div>
  </div>

  <div class="tab-bar">
    <button class="tab-btn active" onclick="switchTab('workout')">WORKOUT</button>
    <button class="tab-btn" onclick="switchTab('food')">LOG FOOD</button>
    <button class="tab-btn" onclick="switchTab('weight')">WEIGHT</button>
    <button class="tab-btn" onclick="switchTab('progress')">PROGRESS</button>
  </div>

  <div class="content">
    <!-- WORKOUT TAB -->
    <div id="tab-workout">
      <div class="day-selector" id="day-selector"></div>
      <div id="day-header"></div>
      <div id="exercises"></div>
    </div>

    <!-- FOOD TAB -->
    <div id="tab-food" style="display:none">
      <div class="diet-card">
        <div class="diet-label">YOUR DIETARY RULES</div>
        <div class="diet-item"><span class="diet-dash">—</span>No chicken · No salmon</div>
        <div class="diet-item"><span class="diet-dash">—</span>Low sodium · Avoid soy</div>
        <div class="diet-item"><span class="diet-dash">—</span>Low sugar · Migraine-aware</div>
        <div class="diet-item"><span class="diet-dash">—</span>~1,600–1,750 cal target</div>
        <div class="diet-item"><span class="diet-dash">—</span>Protein anchor every meal</div>
        <div class="diet-item"><span class="diet-dash">—</span>Evening: savory over sweet to close cravings loop</div>
      </div>
      <div class="two-col">
        <div class="stat-box" style="flex:1">
          <div class="stat-label">TODAY CAL</div>
          <div class="stat-val" id="today-cal" style="color:#c8a882">0</div>
          <div style="font-size:10px;color:#555">target: 1600–1750</div>
        </div>
        <div class="stat-box blue" style="flex:1">
          <div class="stat-label">PROTEIN</div>
          <div class="stat-val" id="today-prot" style="color:#8ba8c8">0g</div>
          <div style="font-size:10px;color:#555">aim: 110–130g</div>
        </div>
      </div>
      <div class="card">
        <div class="card-label">ADD ENTRY</div>
        <input class="wide-input" id="food-name" placeholder="Food name" />
        <div class="row-input">
          <input class="set-input" id="food-cal" type="number" placeholder="Calories" />
          <input class="set-input" id="food-prot" type="number" placeholder="Protein (g)" />
        </div>
        <input class="wide-input" id="food-notes" placeholder="Notes (optional)" />
        <button class="primary-btn" onclick="addFood()">Add Entry</button>
      </div>
      <div id="food-list"></div>
    </div>

    <!-- WEIGHT TAB -->
    <div id="tab-weight" style="display:none">
      <div class="card">
        <div class="card-label">LOG THIS WEEK'S WEIGHT</div>
        <div class="card-note">Weigh once weekly · Same morning · Same conditions. The trend matters, not the number.</div>
        <div class="flex-row">
          <input class="set-input" id="weight-input" type="number" placeholder="lbs" step="0.1" />
          <button class="primary-btn" onclick="addWeight()">Log</button>
        </div>
      </div>
      <div id="weight-list"></div>
    </div>

    <!-- PROGRESS TAB -->
    <div id="tab-progress" style="display:none">
      <div class="section-label">WEEKLY OVERVIEW</div>
      <div id="progress-list"></div>
      <div class="info-card gold">
        <div class="info-label">PROGRESSIVE OVERLOAD RULE</div>
        <div class="info-text">When you complete all sets and reps with good form and the last rep feels like you had 2–3 more in you — increase weight by the smallest increment available next session.</div>
      </div>
      <div class="info-card blue">
        <div class="info-label">REMEMBER</div>
        <div class="info-text">The mirror and how your clothes fit will tell a more accurate story than the scale. You are building something real this time.</div>
      </div>
    </div>
  </div>
</div>

<script>
const PROGRAM = {
  days: [
    { id:"day1", label:"Day 1 — Monday", title:"Lower Body A", subtitle:"Glute Focus · Hip Dominant", color:"#c8a882",
      exercises:[
        {id:"e1",name:"Hip Thrust / Barbell",sets:4,reps:"10–12",cue:"Drive through heel. Crack a walnut at the top. Lower back stays neutral."},
        {id:"e2",name:"Romanian Deadlift",sets:3,reps:"10–12",cue:"Hinge hips back like closing a car door. Feel hamstring stretch. Squeeze glutes to drive up."},
        {id:"e3",name:"Cable Kickback",sets:3,reps:"15 each side",cue:"2 sec up, 2 sec back. Feel it in glute only. If you feel lower back — drop the weight."},
        {id:"e4",name:"Abductor Machine",sets:3,reps:"15",cue:"Slow and controlled. Pause at full extension. This is glute med — critical for shape."},
        {id:"e5",name:"Plank",sets:3,reps:"30–45 sec",cue:"Squeeze glutes AND abs. Don't let hips sag."},
      ]},
    { id:"day2", label:"Day 2 — Tuesday", title:"Upper Body A", subtitle:"Push Focus", color:"#8ba8c8",
      exercises:[
        {id:"e6",name:"Chest Press Machine",sets:3,reps:"12",cue:"Retract shoulder blades before pressing. Don't let shoulders shrug up."},
        {id:"e7",name:"Shoulder Press Machine",sets:3,reps:"12",cue:"Core tight throughout. Don't arch lower back to get the weight up."},
        {id:"e8",name:"Lateral Raises",sets:3,reps:"15",cue:"Lead with your elbow, not your hand. Slight forward lean helps."},
        {id:"e9",name:"Tricep Cable Pushdown",sets:3,reps:"12–15",cue:"Elbows pinned to sides. Full extension at bottom. Squeeze."},
        {id:"e10",name:"Dead Bug",sets:3,reps:"10 each side",cue:"Lower back pressed INTO the floor the entire time. Go slow."},
      ]},
    { id:"day3", label:"Day 3 — Thursday", title:"Lower Body B", subtitle:"Glute Focus · Quad/Glute Mix", color:"#c8a882",
      exercises:[
        {id:"e11",name:"Barbell / Goblet Squat",sets:4,reps:"10–12",cue:"Knees out over pinky toes. Spread the floor. Hard glute squeeze at top."},
        {id:"e12",name:"Bulgarian Split Squat",sets:3,reps:"10 each side",cue:"Front foot far enough forward that knee stays behind toes. Sink straight down."},
        {id:"e13",name:"Leg Press — High Wide Foot",sets:3,reps:"12",cue:"Feet high and wide shifts load to glutes. Don't let lower back round at bottom."},
        {id:"e14",name:"Cable Pull-Through",sets:3,reps:"15",cue:"This IS a glute exercise. Hinge. Drive hips forward. Squeeze hard at top."},
        {id:"e15",name:"Clamshell with Band",sets:3,reps:"15 each side",cue:"Keep hips stacked. Rotation comes from hip only, not your whole body."},
      ]},
    { id:"day4", label:"Day 4 — Friday", title:"Upper Body B", subtitle:"Pull Focus", color:"#8ba8c8",
      exercises:[
        {id:"e16",name:"Seated Cable Row",sets:3,reps:"12",cue:"Pull to lower chest. Squeeze shoulder blades together at end. Don't lean back excessively."},
        {id:"e17",name:"Lat Pulldown",sets:3,reps:"12",cue:"Pull bar to upper chest. Think 'elbows to back pockets.' Chest tall."},
        {id:"e18",name:"Face Pulls",sets:3,reps:"15",cue:"Pull to your face, elbows high. Critical for shoulder health and posture."},
        {id:"e19",name:"Dumbbell Curl",sets:3,reps:"12",cue:"Elbows stationary at sides. Full range. Supinate (rotate) at top."},
        {id:"e20",name:"Hollow Body Hold",sets:3,reps:"20–30 sec",cue:"Lower back FLAT. Arms overhead or by sides. This is harder than it looks."},
      ]},
  ]
};

const GOAL = 145;
let currentDay = 0;
let expandedEx = null;
let logs = {};
let foodLog = [];
let weights = [];

function save(key, val) { try { localStorage.setItem(key, JSON.stringify(val)); } catch(e){} }
function load(key) { try { const v = localStorage.getItem(key); return v ? JSON.parse(v) : null; } catch(e){ return null; } }

function init() {
  logs = load('ss-logs') || {};
  foodLog = load('ss-food') || [];
  weights = load('ss-weights') || [];
  renderDaySelector();
  renderWorkout();
  renderHeader();
}

function renderHeader() {
  if (weights.length > 0) {
    const latest = weights[weights.length-1].weight;
    document.getElementById('stat-row').style.display = 'flex';
    document.getElementById('stat-current').innerHTML = latest + ' <span>lbs</span>';
    document.getElementById('stat-goal').innerHTML = Math.max(0,(latest-GOAL).toFixed(1)) + ' <span>lbs</span>';
  }
}

function renderDaySelector() {
  const el = document.getElementById('day-selector');
  el.innerHTML = PROGRAM.days.map((d,i) => {
    const isActive = i === currentDay;
    const cls = isActive ? (d.color === '#c8a882' ? 'day-btn active-gold' : 'day-btn active-blue') : 'day-btn';
    return `<button class="${cls}" onclick="selectDay(${i})">D${i+1}</button>`;
  }).join('');
}

function selectDay(i) {
  currentDay = i;
  expandedEx = null;
  renderDaySelector();
  renderWorkout();
}

function renderWorkout() {
  const d = PROGRAM.days[currentDay];
  document.getElementById('day-header').innerHTML = `
    <div class="day-header">
      <div class="day-header-label" style="color:${d.color}">${d.label.toUpperCase()}</div>
      <div class="day-header-title">${d.title}</div>
      <div class="day-header-sub">${d.subtitle}</div>
    </div>`;
  document.getElementById('exercises').innerHTML = d.exercises.map(ex => renderExercise(d, ex)).join('');
}

function allSetsDone(d, ex) {
  return Array.from({length:ex.sets},(_,i)=>i+1).every(s => logs[`${d.id}-${ex.id}-${s}`]?.done);
}

function renderExercise(d, ex) {
  const done = allSetsDone(d, ex);
  const isOpen = expandedEx === ex.id;
  let body = '';
  if (isOpen) {
    const setRows = Array.from({length:ex.sets},(_,i)=>i+1).map(s => {
      const key = `${d.id}-${ex.id}-${s}`;
      const log = logs[key] || {};
      const checked = log.done ? 'checked' : '';
      return `<div class="set-row">
        <span class="set-num">S${s}</span>
        <input class="set-input" type="number" placeholder="lbs" value="${log.weight||''}" oninput="updateLog('${key}','weight',this.value)" />
        <input class="set-input" type="number" placeholder="reps" value="${log.reps||''}" oninput="updateLog('${key}','reps',this.value)" />
        <button class="set-check ${checked}" onclick="toggleDone('${key}',this)">${log.done?'✓':''}</button>
      </div>`;
    }).join('');
    body = `<div class="ex-body">
      <div class="cue-box"><div class="cue-label">MIND-MUSCLE CUE</div><div class="cue-text">${ex.cue}</div></div>
      <div class="sets-label">LOG YOUR SETS</div>
      ${setRows}
    </div>`;
  }
  return `<div class="ex-card ${done?'done':''}" id="excard-${ex.id}">
    <div class="ex-header" onclick="toggleEx('${ex.id}')">
      <div>
        <div class="ex-name">${ex.name}${done?'<span class="ex-done-badge">✓</span>':''}</div>
        <div class="ex-meta">${ex.sets} sets · ${ex.reps} reps</div>
      </div>
      <span class="ex-arrow">${isOpen?'▲':'▼'}</span>
    </div>
    ${body}
  </div>`;
}

function toggleEx(id) {
  expandedEx = expandedEx === id ? null : id;
  renderWorkout();
}

function updateLog(key, field, val) {
  if (!logs[key]) logs[key] = {};
  logs[key][field] = val;
  save('ss-logs', logs);
}

function toggleDone(key, btn) {
  if (!logs[key]) logs[key] = {};
  logs[key].done = !logs[key].done;
  save('ss-logs', logs);
  btn.className = 'set-check ' + (logs[key].done ? 'checked' : '');
  btn.textContent = logs[key].done ? '✓' : '';
  const d = PROGRAM.days[currentDay];
  const card = btn.closest('.ex-card');
  const exId = card.id.replace('excard-','');
  const ex = d.exercises.find(e=>e.id===exId);
  if (ex && allSetsDone(d,ex)) card.classList.add('done');
  else card.classList.remove('done');
}

// FOOD
function addFood() {
  const name = document.getElementById('food-name').value.trim();
  if (!name) return;
  const entry = {
    id: Date.now(), name,
    cal: parseInt(document.getElementById('food-cal').value)||0,
    protein: parseInt(document.getElementById('food-prot').value)||0,
    notes: document.getElementById('food-notes').value.trim(),
    date: new Date().toDateString()
  };
  foodLog.push(entry);
  save('ss-food', foodLog);
  document.getElementById('food-name').value='';
  document.getElementById('food-cal').value='';
  document.getElementById('food-prot').value='';
  document.getElementById('food-notes').value='';
  renderFood();
}

function renderFood() {
  const today = new Date().toDateString();
  const todayEntries = foodLog.filter(e=>e.date===today);
  const totalCal = todayEntries.reduce((s,e)=>s+e.cal,0);
  const totalProt = todayEntries.reduce((s,e)=>s+e.protein,0);
  document.getElementById('today-cal').textContent = totalCal;
  document.getElementById('today-cal').style.color = totalCal > 1750 ? '#e88' : '#c8a882';
  document.getElementById('today-prot').textContent = totalProt + 'g';
  const list = document.getElementById('food-list');
  if (todayEntries.length === 0) { list.innerHTML=''; return; }
  list.innerHTML = `<div class="section-label">TODAY'S LOG</div>` +
    [...todayEntries].reverse().map(e=>`
      <div class="food-entry">
        <div><div class="food-name">${e.name}</div>${e.notes?`<div class="food-note">${e.notes}</div>`:''}</div>
        <div><div class="food-cal">${e.cal} cal</div><div class="food-prot">${e.protein}g prot</div></div>
      </div>`).join('');
}

// WEIGHT
function addWeight() {
  const val = parseFloat(document.getElementById('weight-input').value);
  if (!val) return;
  weights.push({ id:Date.now(), weight:val, date:new Date().toDateString() });
  save('ss-weights', weights);
  document.getElementById('weight-input').value='';
  renderWeight();
  renderHeader();
}

function renderWeight() {
  const list = document.getElementById('weight-list');
  if (weights.length===0) {
    list.innerHTML=`<div class="empty"><div class="empty-icon">⚖</div><div>No weigh-ins yet. Log your first one above.</div></div>`;
    return;
  }
  list.innerHTML = `<div class="section-label">HISTORY</div>` +
    [...weights].reverse().map((w,i,arr)=>{
      const prev = arr[i+1];
      const diff = prev ? (w.weight - prev.weight).toFixed(1) : null;
      const diffHtml = diff!==null ? `<div class="weight-diff ${parseFloat(diff)<=0?'down':'up'}">${parseFloat(diff)>0?'+':''}${diff} lbs</div>` : '';
      return `<div class="weight-row">
        <div><div class="weight-val">${w.weight} <span>lbs</span></div><div class="weight-date">${w.date}</div></div>
        <div>${diffHtml}<div class="weight-goal">${Math.max(0,(w.weight-GOAL).toFixed(1))} to goal</div></div>
      </div>`;
    }).join('');
}

// PROGRESS
function renderProgress() {
  const list = document.getElementById('progress-list');
  list.innerHTML = PROGRAM.days.map(d=>{
    const totalSets = d.exercises.reduce((s,ex)=>s+ex.sets,0);
    const doneSets = d.exercises.reduce((s,ex)=>{
      return s + Array.from({length:ex.sets},(_,i)=>i+1).filter(n=>logs[`${d.id}-${ex.id}-${n}`]?.done).length;
    },0);
    const pct = Math.round((doneSets/totalSets)*100);
    return `<div class="progress-card">
      <div class="progress-top">
        <div><div class="progress-title">${d.title}</div><div class="progress-day">${d.label}</div></div>
        <div class="progress-pct" style="color:${d.color}">${pct}%</div>
      </div>
      <div class="progress-bar-bg"><div class="progress-bar-fill" style="width:${pct}%;background:${d.color}"></div></div>
      <div class="progress-sets">${doneSets} / ${totalSets} sets logged</div>
    </div>`;
  }).join('');
}

// TABS
function switchTab(tab) {
  ['workout','food','weight','progress'].forEach(t=>{
    document.getElementById(`tab-${t}`).style.display = t===tab?'block':'none';
  });
  document.querySelectorAll('.tab-btn').forEach((btn,i)=>{
    btn.classList.toggle('active', ['workout','food','weight','progress'][i]===tab);
  });
  if (tab==='food') renderFood();
  if (tab==='weight') renderWeight();
  if (tab==='progress') renderProgress();
}

init();

// PWA install prompt
let deferredPrompt;
window.addEventListener('beforeinstallprompt', (e) => {
  e.preventDefault();
  deferredPrompt = e;
  const banner = document.createElement('div');
  banner.id = 'install-banner';
  banner.style.cssText = 'position:fixed;bottom:20px;left:50%;transform:translateX(-50%);background:#c8a882;color:#0e0c0a;padding:12px 24px;border-radius:24px;font-family:DM Mono,monospace;font-size:13px;cursor:pointer;z-index:999;white-space:nowrap;box-shadow:0 4px 20px rgba(0,0,0,0.4)';
  banner.textContent = '＋ Add to Home Screen';
  banner.onclick = async () => {
    deferredPrompt.prompt();
    const { outcome } = await deferredPrompt.userChoice;
    banner.remove();
    deferredPrompt = null;
  };
  document.body.appendChild(banner);
});
</script>
</body>
</html>
