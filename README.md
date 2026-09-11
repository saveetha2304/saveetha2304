<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rootward — grow quiet, bloom loud</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,400;0,9..144,560;1,9..144,500&family=Sora:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --cream:#FBF5EA;
    --charcoal:#241D18;
    --coral:#F2762E;
    --teal:#2C8B98;
    --magenta:#D6407B;
    --leaf:#437A56;
    --leaf-light:#8FC79B;
    --paper:#FFFCF6;
  }

  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background:
      radial-gradient(ellipse 90% 60% at 50% -10%, #FDEBDD 0%, transparent 60%),
      linear-gradient(180deg, var(--cream) 0%, #F6EEE0 100%);
    font-family:'Sora', sans-serif;
    color:var(--charcoal);
    overflow-x:hidden;
    cursor: none;
  }

  @media (prefers-reduced-motion: reduce){
    * { animation: none !important; transition: none !important; }
  }

  /* ---------- custom cursor + bloom trail ---------- */
  #cursor-dot{
    position:fixed; top:0; left:0; width:10px; height:10px;
    border-radius:50%;
    background: var(--coral);
    pointer-events:none;
    z-index:9999;
    transform:translate(-50%,-50%);
    box-shadow:0 0 12px rgba(242,118,46,0.55);
  }
  .petal{
    position:fixed; top:0; left:0;
    pointer-events:none;
    z-index:9998;
    will-change:transform,opacity;
  }

  @media (hover:none){
    body{ cursor:auto; }
    #cursor-dot{ display:none; }
  }

  /* ---------- layout shell ---------- */
  header.top{
    max-width:1180px; margin:0 auto;
    padding:34px 28px 0;
    display:flex; align-items:center; justify-content:space-between;
  }
  .wordmark{
    font-family:'Fraunces', serif;
    font-size:22px; letter-spacing:0.01em;
  }
  .wordmark span{ color:var(--leaf); font-style:italic; }
  nav.top a{
    color:var(--charcoal); text-decoration:none; font-size:14.5px;
    margin-left:28px; opacity:0.72;
  }
  nav.top a:hover{ opacity:1; }

  .hero{
    max-width:1180px; margin:0 auto;
    padding:56px 28px 20px;
    text-align:center;
  }
  .hero h1{
    font-family:'Fraunces', serif;
    font-weight:560;
    font-size:clamp(34px, 5.4vw, 62px);
    line-height:1.06;
    margin:0 auto 20px;
    max-width:820px;
    letter-spacing:-0.01em;
  }
  .hero h1 em{
    font-style:italic;
    font-weight:500;
    color:var(--coral);
  }
  .hero p.lede{
    max-width:480px; margin:0 auto 8px;
    font-size:17px; line-height:1.6;
    color:#5B5148;
  }

  /* ---------- 3D illustration panels ---------- */
  .gallery{
    max-width:1180px; margin:44px auto 0;
    padding:0 28px 80px;
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:28px;
  }
  @media (max-width:820px){
    .gallery{ grid-template-columns:1fr; }
  }

  .panel{
    position:relative;
    border-radius:22px;
    padding:0;
    aspect-ratio:4/3.1;
    perspective:900px;
    background:var(--paper);
    box-shadow:0 1px 0 rgba(0,0,0,0.03) inset, 0 24px 50px -30px rgba(60,40,20,0.35);
    overflow:hidden;
  }
  .panel .caption{
    position:absolute; left:22px; bottom:20px; z-index:5;
    font-family:'Fraunces', serif;
    font-style:italic;
    font-size:18px;
    color:var(--charcoal);
    max-width:70%;
    pointer-events:none;
  }
  .stage{
    position:absolute; inset:0;
    transform-style:preserve-3d;
    transition:transform 0.15s ease-out;
  }
  .layer{
    position:absolute; inset:0;
    display:flex; align-items:center; justify-content:center;
    transform-style:preserve-3d;
  }
  .layer svg{ width:78%; height:78%; overflow:visible; }

  .panel::after{
    content:"";
    position:absolute; left:10%; right:10%; bottom:6%;
    height:22px;
    background:radial-gradient(ellipse, rgba(60,40,20,0.16), transparent 70%);
    filter:blur(3px);
    z-index:1;
  }

  /* ---------- section: practices ---------- */
  .practices{
    max-width:1180px; margin:0 auto;
    padding:10px 28px 100px;
  }
  .practices h2{
    font-family:'Fraunces', serif;
    font-weight:500; font-size:30px;
    max-width:520px;
    margin:0 0 36px;
  }
  .practice-grid{
    display:grid; grid-template-columns:repeat(3,1fr); gap:0;
    border-top:1px solid rgba(36,29,24,0.14);
  }
  @media (max-width:760px){ .practice-grid{ grid-template-columns:1fr; } }
  .practice{
    padding:26px 22px 26px 0;
    border-bottom:1px solid rgba(36,29,24,0.14);
  }
  .practice-grid .practice:not(:last-child){
    border-right:1px solid rgba(36,29,24,0.14);
  }
  @media (max-width:760px){
    .practice-grid .practice{ border-right:none !important; padding-right:0; }
  }
  .practice h3{
    font-size:16.5px; font-weight:600; margin:0 0 10px;
  }
  .practice p{
    font-size:14.5px; line-height:1.6; color:#5B5148; margin:0;
  }
  .practice .mark{
    display:inline-block; width:9px; height:9px; border-radius:50%;
    margin-right:9px; position:relative; top:-1px;
  }

  footer{
    text-align:center; padding:30px 20px 46px;
    font-size:13px; color:#8A7E71;
  }
</style>
</head>
<body>

<div id="cursor-dot"></div>

<header class="top">
  <div class="wordmark">root<span>ward</span></div>
  <nav class="top">
    <a href="#practices">practices</a>
    <a href="#gallery">the work</a>
  </nav>
</header>

<section class="hero">
  <h1>Grow quiet on the inside,<br><em>bloom</em> loud on the outside.</h1>
  <p class="lede">Two ways of looking at the same idea: renewal starts in the mind and shows up everywhere else. Move your cursor over the panels below.</p>
</section>

<section class="gallery" id="gallery">

  <!-- PANEL 1: phoenix / brain / tree -->
  <div class="panel" data-panel>
    <div class="stage" data-stage>

      <div class="layer" data-depth="-40">
        <svg viewBox="0 0 400 320">
          <defs>
            <radialGradient id="glow1" cx="50%" cy="38%" r="60%">
              <stop offset="0%" stop-color="#FFE3B0" stop-opacity="0.9"/>
              <stop offset="100%" stop-color="#FFE3B0" stop-opacity="0"/>
            </radialGradient>
          </defs>
          <ellipse cx="200" cy="120" rx="170" ry="130" fill="url(#glow1)"/>
        </svg>
      </div>

      <div class="layer" data-depth="10">
        <svg viewBox="0 0 400 320">
          <path d="M20 260 C 60 200, 40 150, 90 110 C 120 85, 110 60, 130 40" fill="none" stroke="#4C9A6A" stroke-width="5" stroke-linecap="round"/>
          <circle cx="90" cy="110" r="7" fill="#8FC79B"/>
          <circle cx="130" cy="40" r="6" fill="#8FC79B"/>
          <circle cx="60" cy="180" r="6" fill="#437A56"/>
          <path d="M380 260 C 340 200, 360 150, 310 110 C 280 85, 290 60, 270 40" fill="none" stroke="#4C9A6A" stroke-width="5" stroke-linecap="round"/>
          <circle cx="310" cy="110" r="7" fill="#8FC79B"/>
          <circle cx="270" cy="40" r="6" fill="#8FC79B"/>
          <circle cx="340" cy="180" r="6" fill="#437A56"/>
        </svg>
      </div>

      <div class="layer" data-depth="55">
        <svg viewBox="0 0 400 320">
          <path d="M200 250 C 190 270, 160 275, 140 295 M200 250 C 210 270, 240 275, 260 295 M200 250 L200 275" fill="none" stroke="#5B4636" stroke-width="4" stroke-linecap="round" opacity="0.55"/>
          <path d="M200 250 C 130 250, 95 210, 100 165 C 84 150, 90 115, 118 105 C 116 78, 150 60, 175 72 C 185 55, 200 55, 200 72 Z"
                fill="#F2A66B" stroke="#C9773B" stroke-width="2"/>
          <path d="M200 250 C 270 250, 305 210, 300 165 C 316 150, 310 115, 282 105 C 284 78, 250 60, 225 72 C 215 55, 200 55, 200 72 Z"
                fill="#6FB3C2" stroke="#2C8B98" stroke-width="2"/>
          <path d="M130 110 Q150 95 170 108 M120 140 Q145 128 165 140 M135 175 Q160 165 180 178" fill="none" stroke="#C9773B" stroke-width="1.6" opacity="0.6"/>
          <path d="M270 110 Q250 95 230 108 M280 140 Q255 128 235 140 M265 175 Q240 165 220 178" fill="none" stroke="#2C8B98" stroke-width="1.6" opacity="0.6"/>
          <g transform="translate(200,68)">
            <ellipse rx="9" ry="18" fill="#D6407B" transform="rotate(0)"/>
            <ellipse rx="9" ry="18" fill="#E06B95" transform="rotate(40)"/>
            <ellipse rx="9" ry="18" fill="#E06B95" transform="rotate(-40)"/>
            <ellipse rx="7" ry="14" fill="#F3B4CB" transform="rotate(80)"/>
            <ellipse rx="7" ry="14" fill="#F3B4CB" transform="rotate(-80)"/>
            <circle r="6" fill="#FCE07A"/>
          </g>
        </svg>
      </div>

      <div class="layer" data-depth="90">
        <svg viewBox="0 0 400 320">
          <g transform="translate(200,10)">
            <path d="M0 90 C -22 70, -18 30, 0 0 C 18 30, 22 70, 0 90 Z" fill="#F2762E"/>
            <path d="M0 90 C -12 74, -9 44, 0 18 C 9 44, 12 74, 0 90 Z" fill="#FCC24C"/>
            <path d="M-4 46 C -22 40, -34 18, -28 -2 C -12 2, -2 22, -4 46 Z" fill="#F2762E" opacity="0.9"/>
            <path d="M4 46 C 22 40, 34 18, 28 -2 C 12 2, 2 22, 4 46 Z" fill="#F2762E" opacity="0.9"/>
          </g>
        </svg>
      </div>

    </div>
    <div class="caption">a mind that keeps re-lighting itself</div>
  </div>

  <!-- PANEL 2: meditating figure -->
  <div class="panel" data-panel>
    <div class="stage" data-stage>

      <div class="layer" data-depth="-40">
        <svg viewBox="0 0 400 320">
          <defs>
            <radialGradient id="glow2" cx="50%" cy="30%" r="55%">
              <stop offset="0%" stop-color="#FCE9CF" stop-opacity="0.95"/>
              <stop offset="100%" stop-color="#FCE9CF" stop-opacity="0"/>
            </radialGradient>
          </defs>
          <ellipse cx="200" cy="110" rx="160" ry="120" fill="url(#glow2)"/>
          <g stroke="#E7B77A" stroke-width="2" fill="none" opacity="0.55">
            <path d="M120 40 Q200 10 280 40"/>
            <path d="M110 60 Q200 28 290 60"/>
          </g>
        </svg>
      </div>

      <div class="layer" data-depth="20">
        <svg viewBox="0 0 400 320">
          <path d="M60 300 C 40 230, 70 170, 40 100" stroke="#437A56" stroke-width="5" fill="none" stroke-linecap="round"/>
          <ellipse cx="46" cy="150" rx="26" ry="12" fill="#8FC79B" transform="rotate(-30 46 150)"/>
          <ellipse cx="52" cy="210" rx="30" ry="13" fill="#4C9A6A" transform="rotate(-15 52 210)"/>
          <ellipse cx="40" cy="100" rx="20" ry="10" fill="#8FC79B" transform="rotate(-45 40 100)"/>
          <path d="M340 300 C 360 230, 330 170, 360 100" stroke="#437A56" stroke-width="5" fill="none" stroke-linecap="round"/>
          <ellipse cx="354" cy="150" rx="26" ry="12" fill="#8FC79B" transform="rotate(30 354 150)"/>
          <ellipse cx="348" cy="210" rx="30" ry="13" fill="#4C9A6A" transform="rotate(15 348 210)"/>
          <ellipse cx="360" cy="100" rx="20" ry="10" fill="#8FC79B" transform="rotate(45 360 100)"/>
        </svg>
      </div>

      <div class="layer" data-depth="60">
        <svg viewBox="0 0 400 320">
          <g transform="translate(200,150)">
            <path d="M-70 90 C -40 70, -10 78, 0 60 C 10 78, 40 70, 70 90 C 40 100, 10 92, 0 84 C -10 92, -40 100, -70 90 Z" fill="#E4A48A"/>
            <path d="M-38 60 C -42 20, -30 -10, 0 -16 C 30 -10, 42 20, 38 60 Z" fill="#EBB79A"/>
            <path d="M-38 30 C -55 45, -60 65, -55 82" stroke="#E4A48A" stroke-width="14" fill="none" stroke-linecap="round"/>
            <path d="M38 30 C 55 45, 60 65, 55 82" stroke="#E4A48A" stroke-width="14" fill="none" stroke-linecap="round"/>
            <circle cx="0" cy="-40" r="24" fill="#EFC1A4"/>
            <path d="M-20 -52 C -20 -70, 20 -70, 20 -52 C 20 -60, -20 -60, -20 -52 Z" fill="#3B2A22"/>
            <circle cx="0" cy="-66" r="8" fill="#3B2A22"/>
          </g>
        </svg>
      </div>

      <div class="layer" data-depth="95">
        <svg viewBox="0 0 400 320">
          <g stroke="#D6407B" stroke-width="2" fill="none" opacity="0.75">
            <path d="M150 40 Q200 15 250 40"/>
          </g>
          <circle cx="150" cy="42" r="3" fill="#F2762E"/>
          <circle cx="250" cy="42" r="3" fill="#2C8B98"/>
          <circle cx="200" cy="18" r="3.5" fill="#D6407B"/>
        </svg>
      </div>

    </div>
    <div class="caption">stillness as its own kind of growth</div>
  </div>

</section>

<section class="practices" id="practices">
  <h2>Small, repeatable ways back to both halves of this.</h2>
  <div class="practice-grid">
    <div class="practice">
      <h3><span class="mark" style="background:var(--coral)"></span>Morning reset</h3>
      <p>Five slow breaths before the first notification. The flame gets a chance to catch before the noise starts.</p>
    </div>
    <div class="practice">
      <h3><span class="mark" style="background:var(--teal)"></span>Midday root</h3>
      <p>Feet flat on the floor, shoulders down, one minute of nothing. Roots hold the same tree up through every season.</p>
    </div>
    <div class="practice">
      <h3><span class="mark" style="background:var(--magenta)"></span>Evening bloom</h3>
      <p>Write down one thing that opened today, even slightly. Petals don't unfold all at once — that's not a flaw.</p>
    </div>
  </div>
</section>

<footer>rootward — a small page about starting over, gently.</footer>

<script>
(function(){
  var reduceMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

  /* ---- custom cursor dot ---- */
  var dot = document.getElementById('cursor-dot');
  var mx = window.innerWidth/2, my = window.innerHeight/2;
  var dx = mx, dy = my;

  function raf(){
    dx += (mx-dx)*0.25;
    dy += (my-dy)*0.25;
    dot.style.transform = 'translate('+dx+'px,'+dy+'px) translate(-50%,-50%)';
    requestAnimationFrame(raf);
  }
  raf();

  /* ---- petal bloom trail ---- */
  var petalColors = ['#F2762E','#2C8B98','#D6407B','#8FC79B','#FCC24C'];
  var lastSpawn = 0;
  var spawnGap = 45; // ms between petals

  function makePetal(x,y){
    var el = document.createElement('div');
    el.className = 'petal';
    var size = 10 + Math.random()*10;
    var color = petalColors[Math.floor(Math.random()*petalColors.length)];
    var angle = Math.random()*360;
    var travel = 14 + Math.random()*18;
    var dirAngle = Math.random()*Math.PI*2;
    var tx = Math.cos(dirAngle)*travel;
    var ty = Math.sin(dirAngle)*travel - 10;

    el.innerHTML =
      '<svg width="'+size+'" height="'+size+'" viewBox="0 0 20 20">' +
        '<path d="M10 10 C10 2, 2 2, 2 10 C2 18, 10 18, 10 10 Z" fill="'+color+'" opacity="0.85"/>' +
      '</svg>';

    el.style.left = x+'px';
    el.style.top = y+'px';
    el.style.opacity = '0';
    el.style.transform = 'translate(-50%,-50%) rotate('+angle+'deg) scale(0.2)';
    el.style.transition = 'transform 0.75s cubic-bezier(.2,.8,.3,1), opacity 0.75s ease-out';
    document.body.appendChild(el);

    requestAnimationFrame(function(){
      requestAnimationFrame(function(){
        el.style.opacity = '0.9';
        el.style.transform = 'translate(calc(-50% + '+tx+'px), calc(-50% + '+ty+'px)) rotate('+(angle+70)+'deg) scale(1)';
      });
    });

    setTimeout(function(){
      el.style.opacity = '0';
      el.style.transform += ' scale(0.6)';
    }, 480);

    setTimeout(function(){ el.remove(); }, 900);
  }

  window.addEventListener('mousemove', function(e){
    mx = e.clientX; my = e.clientY;
    if(reduceMotion) return;
    var now = performance.now();
    if(now - lastSpawn > spawnGap){
      lastSpawn = now;
      makePetal(e.clientX, e.clientY);
    }
  });

  window.addEventListener('touchmove', function(e){
    if(reduceMotion) return;
    var t = e.touches[0];
    if(!t) return;
    var now = performance.now();
    if(now - lastSpawn > spawnGap){
      lastSpawn = now;
      makePetal(t.clientX, t.clientY);
    }
  }, {passive:true});

  /* ---- 3D parallax tilt on hero panels ---- */
  if(!reduceMotion){
    document.querySelectorAll('[data-panel]').forEach(function(panel){
      var stage = panel.querySelector('[data-stage]');
      var layers = panel.querySelectorAll('[data-depth]');

      panel.addEventListener('mousemove', function(e){
        var r = panel.getBoundingClientRect();
        var px = (e.clientX - r.left) / r.width - 0.5;
        var py = (e.clientY - r.top) / r.height - 0.5;

        stage.style.transform =
          'rotateY(' + (px*14) + 'deg) rotateX(' + (-py*14) + 'deg)';

        layers.forEach(function(layer){
          var depth = parseFloat(layer.getAttribute('data-depth'));
          var tx = px * depth * 0.6;
          var ty = py * depth * 0.6;
          layer.style.transform = 'translate3d('+tx+'px,'+ty+'px,'+ (depth*0.4) +'px)';
        });
      });

      panel.addEventListener('mouseleave', function(){
        stage.style.transform = 'rotateY(0deg) rotateX(0deg)';
        layers.forEach(function(layer){
          layer.style.transform = 'translate3d(0,0,0)';
        });
      });
    });
  }
})();
</script>

</body>
</html>## Hi there 👋

<!--
**saveetha2304/saveetha2304** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
