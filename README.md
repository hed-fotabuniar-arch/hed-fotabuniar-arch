<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Buchi-dev | Full-Stack Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;700;800&display=swap" rel="stylesheet"/>
<style>
  :root {
    --bg: #0a0a0f;
    --surface: #10101a;
    --card: #13131f;
    --border: #1e1e30;
    --accent1: #7c5cfc;
    --accent2: #00f0ff;
    --accent3: #ff6b6b;
    --text: #e8e8ff;
    --muted: #6b6b8a;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'Syne', sans-serif;
    background: var(--bg);
    color: var(--text);
    overflow-x: hidden;
    min-height: 100vh;
  }

  /* Starfield BG */
  #stars {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    pointer-events: none;
    z-index: 0;
    overflow: hidden;
  }
  .star {
    position: absolute;
    border-radius: 50%;
    background: #fff;
    animation: twinkle var(--d, 3s) ease-in-out infinite;
    opacity: 0;
  }
  @keyframes twinkle {
    0%, 100% { opacity: 0; transform: scale(0.5); }
    50% { opacity: var(--o, 0.6); transform: scale(1); }
  }

  /* Gradient Orbs */
  .orb {
    position: fixed;
    border-radius: 50%;
    filter: blur(80px);
    pointer-events: none;
    z-index: 0;
    animation: floatOrb var(--fd, 12s) ease-in-out infinite alternate;
  }
  .orb1 { width: 500px; height: 500px; background: rgba(124,92,252,0.12); top: -100px; left: -100px; --fd: 10s; }
  .orb2 { width: 400px; height: 400px; background: rgba(0,240,255,0.08); bottom: -100px; right: -100px; --fd: 14s; }
  .orb3 { width: 300px; height: 300px; background: rgba(255,107,107,0.07); top: 40%; left: 40%; --fd: 9s; }
  @keyframes floatOrb {
    from { transform: translate(0, 0) scale(1); }
    to { transform: translate(40px, 40px) scale(1.1); }
  }

  .wrapper { position: relative; z-index: 1; max-width: 900px; margin: 0 auto; padding: 60px 24px 100px; }

  /* ===== HEADER ===== */
  .header {
    text-align: center;
    margin-bottom: 64px;
    animation: slideDown 0.9s cubic-bezier(.22,1,.36,1) both;
  }
  @keyframes slideDown {
    from { opacity: 0; transform: translateY(-40px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .header-badge {
    display: inline-block;
    padding: 6px 18px;
    border: 1px solid var(--accent1);
    border-radius: 100px;
    font-size: 12px;
    font-family: 'Space Mono', monospace;
    color: var(--accent1);
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-bottom: 20px;
    animation: pulseBorder 2.5s ease-in-out infinite;
  }
  @keyframes pulseBorder {
    0%, 100% { box-shadow: 0 0 0 0 rgba(124,92,252,0.4); }
    50% { box-shadow: 0 0 0 8px rgba(124,92,252,0); }
  }

  .header h1 {
    font-size: clamp(2.5rem, 8vw, 5rem);
    font-weight: 800;
    line-height: 1.05;
    background: linear-gradient(135deg, var(--accent1) 0%, var(--accent2) 50%, var(--accent3) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    background-size: 200% 200%;
    animation: gradientShift 4s ease infinite;
    margin-bottom: 16px;
  }
  @keyframes gradientShift {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }

  /* Typewriter */
  .typewriter {
    font-family: 'Space Mono', monospace;
    font-size: 1.1rem;
    color: var(--accent2);
    min-height: 1.6em;
    margin-bottom: 28px;
  }
  .cursor {
    display: inline-block;
    width: 2px;
    height: 1.1em;
    background: var(--accent2);
    margin-left: 2px;
    vertical-align: middle;
    animation: blink 0.7s step-end infinite;
  }
  @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }

  /* Badges */
  .badges {
    display: flex;
    gap: 12px;
    justify-content: center;
    flex-wrap: wrap;
    margin-bottom: 0;
  }
  .badge-link {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 10px 22px;
    border-radius: 12px;
    font-weight: 700;
    font-size: 14px;
    text-decoration: none;
    color: #fff;
    border: 1px solid transparent;
    transition: transform 0.2s, box-shadow 0.2s;
    position: relative;
    overflow: hidden;
  }
  .badge-link::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba(255,255,255,0.12), transparent);
    opacity: 0;
    transition: opacity 0.2s;
  }
  .badge-link:hover::before { opacity: 1; }
  .badge-link:hover { transform: translateY(-3px); box-shadow: 0 12px 30px rgba(0,0,0,0.4); }
  .badge-link.linkedin { background: #0A66C2; border-color: #1e77d0; }
  .badge-link.portfolio { background: #181717; border-color: #333; }

  /* ===== DIVIDER ===== */
  .divider {
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--border), var(--accent1), var(--border), transparent);
    margin: 48px 0;
    animation: shimmer 3s ease-in-out infinite;
    background-size: 200%;
  }
  @keyframes shimmer {
    0% { background-position: -100%; }
    100% { background-position: 200%; }
  }

  /* ===== SECTIONS ===== */
  .section {
    margin-bottom: 52px;
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .section.visible { opacity: 1; transform: translateY(0); }

  .section-title {
    font-size: 1.3rem;
    font-weight: 800;
    letter-spacing: 1px;
    color: var(--text);
    margin-bottom: 24px;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .section-title span.emoji {
    font-size: 1.2rem;
    animation: bounce 2s ease-in-out infinite;
  }
  @keyframes bounce {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-5px); }
  }
  .section-title::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, var(--border), transparent);
    margin-left: 10px;
  }

  /* ===== ICON GRID ===== */
  .icon-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
    justify-content: center;
  }

  .tech-chip {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px 18px;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 12px;
    font-size: 14px;
    font-weight: 700;
    color: var(--text);
    cursor: default;
    transition: transform 0.25s cubic-bezier(.34,1.56,.64,1), border-color 0.25s, box-shadow 0.25s, background 0.25s;
    position: relative;
    overflow: hidden;
    animation: chipEntrance 0.5s cubic-bezier(.22,1,.36,1) both;
  }
  .tech-chip::after {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(circle at var(--mx,50%) var(--my,50%), rgba(255,255,255,0.08), transparent 60%);
    opacity: 0;
    transition: opacity 0.3s;
  }
  .tech-chip:hover::after { opacity: 1; }
  .tech-chip:hover {
    transform: translateY(-5px) scale(1.04);
    border-color: var(--chip-color, var(--accent1));
    box-shadow: 0 8px 30px rgba(0,0,0,0.4), 0 0 20px var(--chip-glow, rgba(124,92,252,0.3));
    background: var(--surface);
  }
  .tech-chip img {
    width: 26px;
    height: 26px;
    object-fit: contain;
    transition: transform 0.3s;
  }
  .tech-chip:hover img { transform: rotate(10deg) scale(1.15); }

  @keyframes chipEntrance {
    from { opacity: 0; transform: scale(0.7) translateY(10px); }
    to { opacity: 1; transform: scale(1) translateY(0); }
  }

  /* ===== STATS ===== */
  .stats-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }
  .stat-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    overflow: hidden;
    transition: transform 0.3s, border-color 0.3s;
  }
  .stat-card:hover { transform: scale(1.02); border-color: var(--accent1); }
  .stat-card img { width: 100%; display: block; }

  /* ===== STREAK ===== */
  .streak-wrap {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    overflow: hidden;
    transition: transform 0.3s;
  }
  .streak-wrap:hover { transform: scale(1.01); }
  .streak-wrap img { width: 100%; display: block; }

  /* ===== PACMAN ===== */
  .pacman-wrap {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    overflow: hidden;
    padding: 8px;
  }
  .pacman-wrap img { width: 100%; display: block; border-radius: 8px; }

  /* ===== FOOTER ===== */
  .footer {
    text-align: center;
    padding-top: 32px;
    font-family: 'Space Mono', monospace;
    font-size: 13px;
    color: var(--muted);
    animation: fadeIn 1s ease both;
    animation-delay: 1.5s;
    opacity: 0;
  }
  .footer.visible { opacity: 1; }
  .footer a {
    color: var(--accent1);
    text-decoration: none;
    font-weight: 700;
  }
  .footer a:hover { color: var(--accent2); }
  .made-badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 10px 24px;
    background: linear-gradient(135deg, var(--accent1), var(--accent2));
    border-radius: 100px;
    color: #fff;
    font-weight: 700;
    font-size: 14px;
    text-decoration: none;
    transition: transform 0.3s, box-shadow 0.3s;
    margin-bottom: 16px;
    animation: heartbeat 2s ease-in-out infinite;
  }
  .made-badge:hover { transform: scale(1.05); box-shadow: 0 0 30px rgba(124,92,252,0.5); }
  @keyframes heartbeat {
    0%, 100% { box-shadow: 0 0 0 0 rgba(124,92,252,0.5); }
    50% { box-shadow: 0 0 0 10px rgba(124,92,252,0); }
  }
  .heart {
    display: inline-block;
    animation: heartPulse 1.2s ease-in-out infinite;
    color: #ff6b6b;
  }
  @keyframes heartPulse {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.3); }
  }

  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }
</style>
</head>
<body>

<!-- Starfield -->
<div id="stars"></div>
<!-- Orbs -->
<div class="orb orb1"></div>
<div class="orb orb2"></div>
<div class="orb orb3"></div>

<div class="wrapper">

  <!-- HEADER -->
  <div class="header">
    <div class="header-badge">🚀 Open to Work</div>
    <h1>Full-Stack Developer</h1>
    <div class="typewriter"><span id="type-text"></span><span class="cursor"></span></div>
    <div class="badges">
      <a href="#" class="badge-link linkedin">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="white"><path d="M16 8a6 6 0 016 6v7h-4v-7a2 2 0 00-2-2 2 2 0 00-2 2v7h-4v-7a6 6 0 016-6zM2 9h4v12H2z"/><circle cx="4" cy="4" r="2"/></svg>
        LinkedIn — Connect
      </a>
      <a href="https://github.com/Buchi-dev" class="badge-link portfolio">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="white"><path d="M12 2C6.48 2 2 6.48 2 12c0 4.42 2.87 8.17 6.84 9.49.5.09.68-.22.68-.48v-1.7c-2.78.6-3.37-1.34-3.37-1.34-.45-1.15-1.1-1.46-1.1-1.46-.9-.62.07-.6.07-.6 1 .07 1.53 1.02 1.53 1.02.89 1.52 2.34 1.08 2.91.83.09-.65.35-1.08.63-1.33-2.22-.25-4.56-1.11-4.56-4.95 0-1.09.39-1.99 1.02-2.69-.1-.25-.44-1.27.1-2.65 0 0 .84-.27 2.75 1.02A9.56 9.56 0 0112 6.8c.85.004 1.71.11 2.51.33 1.91-1.29 2.75-1.02 2.75-1.02.54 1.38.2 2.4.1 2.65.63.7 1.02 1.6 1.02 2.69 0 3.85-2.34 4.7-4.57 4.94.36.31.68.92.68 1.85v2.74c0 .27.18.58.69.48A10.01 10.01 0 0022 12c0-5.52-4.48-10-10-10z"/></svg>
        Portfolio — Visit
      </a>
    </div>
  </div>

  <div class="divider"></div>

  <!-- PROGRAMMING LANGUAGES -->
  <div class="section" id="s1">
    <div class="section-title"><span class="emoji">🔥</span> Programming Languages</div>
    <div class="icon-grid" id="lang-grid"></div>
  </div>

  <div class="divider"></div>

  <!-- FRONTEND -->
  <div class="section" id="s2">
    <div class="section-title"><span class="emoji">⚡</span> Frontend Development</div>
    <div class="icon-grid" id="frontend-grid"></div>
  </div>

  <div class="divider"></div>

  <!-- UI FRAMEWORKS -->
  <div class="section" id="s3">
    <div class="section-title"><span class="emoji">🎨</span> UI Frameworks & Design</div>
    <div class="icon-grid" id="ui-grid"></div>
  </div>

  <div class="divider"></div>

  <!-- DEV TOOLS -->
  <div class="section" id="s4">
    <div class="section-title"><span class="emoji">🛠</span> Development Tools & Platforms</div>
    <div class="icon-grid" id="tools-grid"></div>
  </div>

  <div class="divider"></div>

  <!-- DATABASE -->
  <div class="section" id="s5">
    <div class="section-title"><span class="emoji">🌟</span> Database Technologies</div>
    <div class="icon-grid" id="db-grid"></div>
  </div>

  <div class="divider"></div>

  <!-- STREAK -->
  <div class="section" id="s6">
    <div class="section-title"><span class="emoji">🔥</span> GitHub Streak</div>
    <div class="streak-wrap">
      <img src="https://github-readme-streak-stats.herokuapp.com/?user=Buchi-dev&theme=tokyonight&hide_border=true&background=transparent" alt="GitHub Streak Stats" loading="lazy"/>
    </div>
  </div>

  <div class="divider"></div>

  <!-- GITHUB STATS -->
  <div class="section" id="s7">
    <div class="section-title"><span class="emoji">📊</span> GitHub Stats</div>
    <div class="stats-grid">
      <div class="stat-card">
        <img src="https://github-readme-stats.vercel.app/api?username=Buchi-dev&show_icons=true&theme=tokyonight&hide_border=true" alt="GitHub Stats" loading="lazy"/>
      </div>
      <div class="stat-card">
        <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Buchi-dev&layout=compact&theme=tokyonight&hide_border=true" alt="Top Languages" loading="lazy"/>
      </div>
    </div>
  </div>

  <div class="divider"></div>

  <!-- PACMAN -->
  <div class="section" id="s8">
    <div class="section-title"><span class="emoji">🎮</span> Contribution Pac-Man</div>
    <div class="pacman-wrap">
      <img src="https://raw.githubusercontent.com/Buchi-dev/Buchi-dev/output/pacman-contribution-graph.svg" alt="Pac-Man Contributions" loading="lazy"/>
    </div>
  </div>

  <div class="divider"></div>

  <!-- FOOTER -->
  <div class="footer" id="footer">
    <a href="https://github.com/Buchi-dev" class="made-badge">
      Made with <span class="heart">❤️</span> by Buchi-dev
    </a>
    <br/>
    <span>&copy; 2024 Buchi-dev — All rights reserved</span>
  </div>

</div>

<script>
// ===== STARFIELD =====
(function() {
  const container = document.getElementById('stars');
  for (let i = 0; i < 120; i++) {
    const s = document.createElement('div');
    s.className = 'star';
    const size = Math.random() * 2.5 + 0.5;
    s.style.cssText = `
      width:${size}px; height:${size}px;
      top:${Math.random()*100}%;
      left:${Math.random()*100}%;
      --d:${(Math.random()*4+2).toFixed(1)}s;
      --o:${(Math.random()*0.5+0.3).toFixed(2)};
      animation-delay:${(Math.random()*5).toFixed(2)}s;
    `;
    container.appendChild(s);
  }
})();

// ===== TYPEWRITER =====
(function() {
  const texts = ['Full Stack Developer','Software Engineer','UI/UX Designer','Problem Solver','Creative Innovator','Tech Enthusiast'];
  let ti = 0, ci = 0, typing = true;
  const el = document.getElementById('type-text');
  function tick() {
    const cur = texts[ti];
    if (typing) {
      ci++;
      el.textContent = cur.slice(0, ci);
      if (ci === cur.length) { typing = false; setTimeout(tick, 1800); return; }
      setTimeout(tick, 80 + Math.random()*40);
    } else {
      ci--;
      el.textContent = cur.slice(0, ci);
      if (ci === 0) { typing = true; ti = (ti+1) % texts.length; setTimeout(tick, 400); return; }
      setTimeout(tick, 40);
    }
  }
  setTimeout(tick, 800);
})();

// ===== TECH DATA =====
const devicons = 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons';
const techs = {
  lang: [
    { name:'Java', icon:`${devicons}/java/java-original.svg`, color:'#f89820', glow:'rgba(248,152,32,0.35)' },
    { name:'Python', icon:`${devicons}/python/python-original.svg`, color:'#3776ab', glow:'rgba(55,118,171,0.35)' },
    { name:'C', icon:`${devicons}/c/c-original.svg`, color:'#a8b9cc', glow:'rgba(168,185,204,0.35)' },
    { name:'C#', icon:`${devicons}/csharp/csharp-original.svg`, color:'#9b4f96', glow:'rgba(155,79,150,0.35)' },
    { name:'Kotlin', icon:`${devicons}/kotlin/kotlin-original.svg`, color:'#7f52ff', glow:'rgba(127,82,255,0.35)' },
    { name:'JavaScript', icon:`${devicons}/javascript/javascript-original.svg`, color:'#f7df1e', glow:'rgba(247,223,30,0.35)' },
    { name:'TypeScript', icon:`${devicons}/typescript/typescript-original.svg`, color:'#3178c6', glow:'rgba(49,120,198,0.35)' },
  ],
  frontend: [
    { name:'HTML5', icon:`${devicons}/html5/html5-original.svg`, color:'#e34f26', glow:'rgba(227,79,38,0.35)' },
    { name:'CSS3', icon:`${devicons}/css3/css3-original.svg`, color:'#1572b6', glow:'rgba(21,114,182,0.35)' },
    { name:'React', icon:`${devicons}/react/react-original.svg`, color:'#61dafb', glow:'rgba(97,218,251,0.35)' },
    { name:'Vue.js', icon:`${devicons}/vuejs/vuejs-original.svg`, color:'#42b883', glow:'rgba(66,184,131,0.35)' },
    { name:'Angular', icon:`${devicons}/angular/angular-original.svg`, color:'#dd0031', glow:'rgba(221,0,49,0.35)' },
    { name:'Node.js', icon:`${devicons}/nodejs/nodejs-original.svg`, color:'#339933', glow:'rgba(51,153,51,0.35)' },
  ],
  ui: [
    { name:'Bootstrap', icon:`${devicons}/bootstrap/bootstrap-original.svg`, color:'#7952b3', glow:'rgba(121,82,179,0.35)' },
    { name:'Tailwind', icon:'https://raw.githubusercontent.com/tailwindlabs/tailwindcss/master/.github/logo-dark.svg', color:'#38bdf8', glow:'rgba(56,189,248,0.35)' },
    { name:'Material UI', icon:`${devicons}/materialui/materialui-original.svg`, color:'#007fff', glow:'rgba(0,127,255,0.35)' },
    { name:'Ant Design', icon:'https://gw.alipayobjects.com/zos/rmsportal/KDpgvguMpGfqaHPjicRK.svg', color:'#1677ff', glow:'rgba(22,119,255,0.35)' },
    { name:'Figma', icon:`${devicons}/figma/figma-original.svg`, color:'#f24e1e', glow:'rgba(242,78,30,0.35)' },
  ],
  tools: [
    { name:'Git', icon:`${devicons}/git/git-original.svg`, color:'#f05032', glow:'rgba(240,80,50,0.35)' },
    { name:'Linux', icon:`${devicons}/linux/linux-original.svg`, color:'#fcc624', glow:'rgba(252,198,36,0.35)' },
    { name:'Android', icon:`${devicons}/android/android-original.svg`, color:'#3ddc84', glow:'rgba(61,220,132,0.35)' },
    { name:'Arduino', icon:`${devicons}/arduino/arduino-original.svg`, color:'#00979d', glow:'rgba(0,151,157,0.35)' },
    { name:'Vite', icon:`${devicons}/vitejs/vitejs-original.svg`, color:'#646cff', glow:'rgba(100,108,255,0.35)' },
  ],
  db: [
    { name:'MySQL', icon:`${devicons}/mysql/mysql-original.svg`, color:'#00758f', glow:'rgba(0,117,143,0.35)' },
    { name:'MongoDB', icon:`${devicons}/mongodb/mongodb-original.svg`, color:'#4db33d', glow:'rgba(77,179,61,0.35)' },
    { name:'Firebase', icon:`${devicons}/firebase/firebase-plain.svg`, color:'#ffca28', glow:'rgba(255,202,40,0.35)' },
  ],
};

function renderGrid(id, items) {
  const grid = document.getElementById(id);
  items.forEach((t, i) => {
    const chip = document.createElement('div');
    chip.className = 'tech-chip';
    chip.style.animationDelay = `${i * 0.06}s`;
    chip.style.setProperty('--chip-color', t.color);
    chip.style.setProperty('--chip-glow', t.glow);
    chip.innerHTML = `<img src="${t.icon}" alt="${t.name}" />${t.name}`;
    // Mouse radial effect
    chip.addEventListener('mousemove', e => {
      const r = chip.getBoundingClientRect();
      chip.style.setProperty('--mx', ((e.clientX - r.left)/r.width*100)+'%');
      chip.style.setProperty('--my', ((e.clientY - r.top)/r.height*100)+'%');
    });
    grid.appendChild(chip);
  });
}

renderGrid('lang-grid', techs.lang);
renderGrid('frontend-grid', techs.frontend);
renderGrid('ui-grid', techs.ui);
renderGrid('tools-grid', techs.tools);
renderGrid('db-grid', techs.db);

// ===== INTERSECTION OBSERVER (scroll reveal) =====
const sections = document.querySelectorAll('.section');
const obs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('visible');
      obs.unobserve(e.target);
    }
  });
}, { threshold: 0.1 });
sections.forEach(s => obs.observe(s));

// Footer fade
const footer = document.getElementById('footer');
const footerObs = new IntersectionObserver(entries => {
  if (entries[0].isIntersecting) { footer.classList.add('visible'); footerObs.unobserve(footer); }
}, { threshold: 0.5 });
footerObs.observe(footer);
</script>
</body>
</html>
