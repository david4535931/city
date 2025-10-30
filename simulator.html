<!DOCTYPE html>
<html lang="uk">
<head>
<meta charset="utf-8" />
<title>2D Симулятор — міні-гра</title>
<style>
  :root{
    --bg:#0f1724;
    --hud-bg: rgba(255,255,255,0.06);
    --work:#d97706;
    --home:#059669;
    --shop:#2563eb;
    --text:#e6eef8;
  }
  html,body{height:100%;margin:0;font-family:Inter,Arial,Helvetica,sans-serif;background:var(--bg);color:var(--text);}
  #container{display:flex;flex-direction:column;align-items:center;padding:14px;height:100%;}
  #hud{
    width:900px; max-width:95%; background:var(--hud-bg); padding:10px 16px; border-radius:10px; 
    display:flex;justify-content:space-between;align-items:center;box-shadow:0 6px 18px rgba(2,6,23,0.6);
    margin-bottom:10px;
  }
  #hud .stat{font-size:18px}
  #gamewrap{width:900px; max-width:95%; flex:1; display:flex; justify-content:center; align-items:center;}
  canvas{background: linear-gradient(180deg,#071129 0%, #071129 40%, #071631 100%); border-radius:10px; box-shadow:0 10px 40px rgba(2,6,23,0.8);}
  #controls{margin-top:8px;color:#cfd8e6;font-size:13px;}
  /* overlay (mini-game) */
  #overlay{
    position:fixed;left:0;top:0;right:0;bottom:0;display:none;align-items:center;justify-content:center;
    background:rgba(0,0,0,0.6); z-index:30;
  }
  .panel{
    background:#0b1220; padding:18px;border-radius:12px;border:1px solid rgba(255,255,255,0.06); width:520px; text-align:center;
  }
  .bar{height:18px;background:rgba(255,255,255,0.06);border-radius:8px;overflow:hidden;margin:10px 0}
  .bar > div{height:100%;width:0%;background:linear-gradient(90deg,#10b981,#06b6d4);}
  button.btn{
    background:#111827;color:var(--text);border:1px solid rgba(255,255,255,0.06);padding:8px 14px;border-radius:8px;font-size:15px;cursor:pointer;
  }
  .zone-label{font-size:12px;color:rgba(255,255,255,0.9);text-shadow:0 1px 0 rgba(0,0,0,0.6)}
  footer{font-size:12px;color:#9fb0d8;margin-top:8px}
</style>
</head>
<body>
<div id="container">
  <div id="hud">
    <div class="stat">День: <span id="day">1</span></div>
    <div class="stat">Гроші: <span id="money">100</span></div>
    <div class="stat">Енергія: <span id="energy">50</span></div>
    <div class="stat zone-label">Зайди в зони: <span style="color:var(--work)">Робота</span>, <span style="color:var(--home)">Дім</span>, <span style="color:var(--shop)">Магазин</span></div>
  </div>

  <div id="gamewrap">
    <canvas id="game" width="900" height="520"></canvas>
  </div>

  <div id="controls">Керування: ← → ↑ ↓ або WASD — рух. Коли в зоні роботи — натисни пробіл або кнопку в міні-грі для виконання роботи.</div>
  <footer>Злови енергетики (сині краплі) щоб поповнити енергію. Пропущені дропи віднімають енергію.</footer>
</div>

<!-- Overlay для міні-ігри -->
<div id="overlay">
  <div class="panel">
    <h2 id="mini-title">Робота</h2>
    <p id="mini-desc">Натискай <strong>ПРОБІЛ</strong> або кнопку як можна швидше, щоб заробити гроші. Енергія витрачається.</p>
    <div class="bar"><div id="mini-progress"></div></div>
    <div style="margin-top:8px">
      <button class="btn" id="mini-press">Натисни!</button>
      <button class="btn" id="mini-exit" style="margin-left:10px">Завершити</button>
    </div>
    <p style="margin-top:10px;font-size:13px;color:#9fb0d8">Прогрес дає винагороду; чим більше заповниш — тим більше грошей.</p>
  </div>
</div>

<script>
/* ========== Налаштування гри ========== */
const canvas = document.getElementById('game');
const ctx = canvas.getContext('2d');

let W = canvas.width, H = canvas.height;

/* Статус гравця */
const state = {
  x: W/2-12, y: H/2-12, radius:14, speed:3.6,
  energy: 50, money: 100, day: 1,
  keys: {}, inZone: null
};

/* Зони на мапі (прямокутники) */
const zones = {
  work: {x: 640, y: 60, w: 200, h: 130, color: getComputedStyle(document.documentElement).getPropertyValue('--work').trim()},
  home: {x: 60, y: 340, w: 220, h: 140, color: getComputedStyle(document.documentElement).getPropertyValue('--home').trim()},
  shop: {x: 320, y: 60, w: 200, h: 130, color: getComputedStyle(document.documentElement).getPropertyValue('--shop').trim()}
};

/* енергодропи (предмети) */
let drops = []; // {x,y,vy, w,h, picked:false}

/* HUD елементи */
const elEnergy = document.getElementById('energy');
const elMoney = document.getElementById('money');
const elDay = document.getElementById('day');

/* Overlay mini-game */
const overlay = document.getElementById('overlay');
const miniProgress = document.getElementById('mini-progress');
const miniPressBtn = document.getElementById('mini-press');
const miniExitBtn = document.getElementById('mini-exit');
let mini = {active:false, progress:0, presses:0, startTime:0};

/* ========== Події клавіш ========== */
window.addEventListener('keydown', (e)=>{
  state.keys[e.key] = true;
  // пробіл у міні-грі
  if(mini.active && (e.code === 'Space')) handleMiniPress();
});
window.addEventListener('keyup', (e)=>{
  state.keys[e.key] = false;
});

/* Кнопки у міні-грі */
miniPressBtn.addEventListener('click', handleMiniPress);
miniExitBtn.addEventListener('click', endMiniGame);

/* ========== Функції міні-ігри (робота) ========== */
function startMiniGame(){
  if(mini.active) return;
  mini.active = true;
  mini.progress = 0;
  mini.presses = 0;
  mini.startTime = performance.now();
  overlay.style.display = 'flex';
  miniProgress.style.width = '0%';
}

function handleMiniPress(){
  if(!mini.active) return;
  // кожен прес додає прогрес (залежить від часу між пресами)
  mini.presses++;
  mini.progress += 1.6; // базове додавання
  // витрати енергії при натиску
  state.energy = Math.max(0, state.energy - 0.7);
  if(mini.progress >= 100) {
    mini.progress = 100;
    finalizeMiniSuccess();
  }
  miniProgress.style.width = mini.progress + '%';
  updateHUD();
}

function finalizeMiniSuccess(){
  // винагорода залежить від presses
  const reward = Math.floor(10 + mini.presses * 2 + Math.random()*8);
  const energyCost = Math.floor(6 + mini.presses * 0.8);
  state.money += reward;
  state.energy = Math.max(0, state.energy - energyCost);
  alert(`Гарно працював! Отримано ${reward} грн. Енергія -${energyCost}.`);
  endMiniGame();
}

function endMiniGame(){
  mini.active = false;
  overlay.style.display = 'none';
  mini.progress = 0;
  mini.presses = 0;
  mini.startTime = 0;
  miniProgress.style.width = '0%';
  updateHUD();
}

/* ========== Генерація дропів ========== */
function spawnDrop(){
  const x = Math.random() * (W - 30) + 15;
  drops.push({x:x, y:-20, vy: 2 + Math.random()*2, w:18, h:26});
}

/* Перевірка колізій */
function rectCircleCollides(rx, ry, rw, rh, cx, cy, cr){
  // перевірка близькості
  let testX = cx;
  let testY = cy;
  if (cx < rx) testX = rx;
  else if (cx > rx+rw) testX = rx+rw;
  if (cy < ry) testY = ry;
  else if (cy > ry+rh) testY = ry+rh;
  const dx = cx - testX;
  const dy = cy - testY;
  return (dx*dx + dy*dy) <= cr*cr;
}

/* ========== Оновлення HUD ========== */
function updateHUD(){
  elEnergy.textContent = Math.max(0, Math.floor(state.energy));
  elMoney.textContent = state.money;
  elDay.textContent = state.day;
}

/* ========== Головна петля гри ========== */
let lastDropAt = 0;
function gameLoop(ts){
  // переміщення гравця
  if(state.keys['ArrowLeft'] || state.keys['a'] || state.keys['A']) state.x -= state.speed;
  if(state.keys['ArrowRight'] || state.keys['d'] || state.keys['D']) state.x += state.speed;
  if(state.keys['ArrowUp'] || state.keys['w'] || state.keys['W']) state.y -= state.speed;
  if(state.keys['ArrowDown'] || state.keys['s'] || state.keys['S']) state.y += state.speed;

  // межі
  state.x = Math.max(0, Math.min(W - state.radius*2, state.x));
  state.y = Math.max(0, Math.min(H - state.radius*2, state.y));

  // оновлення падіння дропів
  for(let i=drops.length-1;i>=0;i--){
    const d = drops[i];
    d.y += d.vy;
    // перевірка на збір
    const cx = state.x + state.radius;
    const cy = state.y + state.radius;
    const collided = rectCircleCollides(d.x, d.y, d.w, d.h, cx, cy, state.radius);
    if(collided){
      // зібрав
      state.energy = Math.min(100, state.energy + 12);
      drops.splice(i,1);
      continue;
    }
    if(d.y > H + 30){
      // пропущений дроп — штраф
      drops.splice(i,1);
      state.energy = Math.max(0, state.energy - 8);
    }
  }

  // періодичне появлення дропів
  if(ts - lastDropAt > 1500 + Math.random()*1200){
    spawnDrop();
    lastDropAt = ts;
  }

  // перевірка зон
  const cx = state.x + state.radius;
  const cy = state.y + state.radius;
  let currentZone = null;
  for(const k of Object.keys(zones)){
    const z = zones[k];
    if(cx > z.x && cx < z.x + z.w && cy > z.y && cy < z.y + z.h){
      currentZone = k;
      break;
    }
  }
  if(currentZone !== state.inZone){
    // вхід або вихід з зони
    state.inZone = currentZone;
    if(currentZone === 'work'){
      // автоматичне підказування: натисни пробіл щоб почати
      // відкриємо міні-ігру автоматично
      startMiniGame();
    }
    if(currentZone === 'home'){
      // автоматичне відновлення (ліжко)
      state.energy = Math.min(100, state.energy + 30);
      alert('Ти відпочив вдома. Енергія +30.');
    }
    if(currentZone === 'shop'){
      // показати просте вікно покупки
      const buy = confirm('Магазин: купити енергетик +25 енергії за 40 грн?\nНатисни OK, щоб купити.');
      if(buy){
        if(state.money >= 40){
          state.money -= 40;
          state.energy = Math.min(100, state.energy + 25);
          alert('Куплено! Енергія +25');
        } else {
          alert('Недостатньо грошей.');
        }
      }
    }
  }

  // якщо енергія впала до 0 — новий день, відновлення
  if(state.energy <= 0){
    state.day += 1;
    state.energy = 45;
    // невеликий штраф грошей за енергетичні збитки
    state.money = Math.max(0, state.money - 8);
    alert('Ти втратив усю енергію. Новий день починається. День +1.');
  }

  // малюй сцену
  drawScene();

  updateHUD();

  requestAnimationFrame(gameLoop);
}

/* ========== Малювання ========== */
function drawScene(){
  // фон
  ctx.clearRect(0,0,W,H);
  // легка сітка / підлога
  ctx.fillStyle = "#071428";
  ctx.fillRect(0,0,W,H);

  // зони
  for(const key of Object.keys(zones)){
    const z = zones[key];
    ctx.fillStyle = hexToRGBA(z.color, 0.18);
    ctx.fillRect(z.x, z.y, z.w, z.h);
    ctx.strokeStyle = hexToRGBA(z.color, 0.6);
    ctx.lineWidth = 2;
    ctx.strokeRect(z.x+1, z.y+1, z.w-2, z.h-2);
    // текст
    ctx.fillStyle = "#e6eef8";
    ctx.font = '14px Inter, Arial';
    ctx.fillText(key === 'work' ? 'РОБОТА' : key === 'home' ? 'ДІМ' : 'МАГАЗИН',
                 z.x + 10, z.y + 20);
  }

  // дропи
  for(const d of drops){
    // малюнок краплі
    ctx.beginPath();
    const centerX = d.x + d.w/2, centerY = d.y + d.h/2;
    ctx.fillStyle = '#06b6d4';
    ctx.ellipse(centerX, centerY, d.w/2, d.h/2, 0, 0, Math.PI*2);
    ctx.fill();
    ctx.closePath();
    // блиск
    ctx.fillStyle = '#9ee3f2';
    ctx.fillRect(d.x + d.w/2 - 3, d.y + 4, 5, 3);
  }

  // гравець
  ctx.beginPath();
  const px = state.x + state.radius, py = state.y + state.radius;
  // тінь
  ctx.fillStyle = 'rgba(0,0,0,0.35)';
  ctx.ellipse(px, py + state.radius*0.6, state.radius*1.1, state.radius*0.45, 0, 0, Math.PI*2);
  ctx.fill();
  // тіло
  ctx.beginPath();
  ctx.fillStyle = '#10b981';
  ctx.ellipse(px, py, state.radius, state.radius, 0, 0, Math.PI*2);
  ctx.fill();
  // око / орієнтир
  ctx.fillStyle = '#04202b';
  ctx.fillRect(px-4, py-3, 6, 6);

  // маленька підказка якщо в зоні
  if(state.inZone){
    ctx.fillStyle = 'rgba(255,255,255,0.06)';
    ctx.fillRect(8, H - 46, 320, 36);
    ctx.fillStyle = '#cfe7ff';
    ctx.font = '13px Inter, Arial';
    let msg = state.inZone === 'work' ? 'В зоні РОБОТА — міні-гра запущена.' :
              state.inZone === 'home' ? 'В зоні ДІМ — енергія відновлюється.' :
              'В зоні МАГАЗИН — купівля доступна.';
    ctx.fillText(msg, 16, H - 22);
  }
}

/* ========== Утиліти ========== */
function hexToRGBA(hex, alpha){
  // hex у форматі #rrggbb або #rrggbbaa
  hex = hex.replace('#','').trim();
  let r = parseInt(hex.slice(0,2),16);
  let g = parseInt(hex.slice(2,4),16);
  let b = parseInt(hex.slice(4,6),16);
  return `rgba(${r},${g},${b},${alpha})`;
}

/* ========== Старт гри ========== */
updateHUD();
requestAnimationFrame(gameLoop);

/* ========== Додаткові підказки / швидке тестування ========== */
// Додатково: клік по canvas — дає невелику імпульсну енергію
canvas.addEventListener('click', ()=> {
  state.energy = Math.min(100, state.energy + 3);
});
</script>
</body>
</html>
