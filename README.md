<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Sheffy Samra — Dev Profile</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&family=Fira+Code:wght@300;400;600&display=swap" rel="stylesheet"/>
<style>
  :root {
    --cyan: #00e5ff;
    --green: #00ff88;
    --pink: #ff006e;
    --yellow: #ffe600;
    --bg: #020810;
    --bg2: #040f1a;
    --card: #061525;
    --border: rgba(0,229,255,0.2);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: #c9f0ff;
    font-family: 'Fira Code', monospace;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  #cursor {
    position: fixed;
    width: 20px; height: 20px;
    border: 2px solid var(--cyan);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9999;
    transition: transform 0.1s;
    mix-blend-mode: difference;
  }
  #cursor-dot {
    position: fixed;
    width: 5px; height: 5px;
    background: var(--cyan);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9999;
  }

  /* Matrix rain canvas */
  #matrix {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    opacity: 0.06;
    z-index: 0;
    pointer-events: none;
  }

  /* Scanlines overlay */
  body::after {
    content: '';
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,0.08) 2px,
      rgba(0,0,0,0.08) 4px
    );
    pointer-events: none;
    z-index: 100;
  }

  .container {
    max-width: 900px;
    margin: 0 auto;
    padding: 0 20px 80px;
    position: relative;
    z-index: 1;
  }

  /* ── HEADER ── */
  header {
    text-align: center;
    padding: 60px 0 40px;
    position: relative;
  }

  .avatar-ring {
    position: relative;
    width: 120px; height: 120px;
    margin: 0 auto 24px;
  }
  .avatar-ring svg {
    position: absolute;
    top: 0; left: 0;
    width: 120px; height: 120px;
    animation: spin 8s linear infinite;
  }
  .avatar-inner {
    position: absolute;
    top: 12px; left: 12px;
    width: 96px; height: 96px;
    border-radius: 50%;
    background: linear-gradient(135deg, #061525, #0a2040);
    border: 2px solid var(--cyan);
    display: flex; align-items: center; justify-content: center;
    font-size: 42px;
    box-shadow: 0 0 30px rgba(0,229,255,0.4), inset 0 0 20px rgba(0,229,255,0.05);
    animation: avatarPulse 3s ease-in-out infinite;
  }
  @keyframes spin {
    from { transform: rotate(0deg); }
    to   { transform: rotate(360deg); }
  }
  @keyframes avatarPulse {
    0%,100% { box-shadow: 0 0 20px rgba(0,229,255,0.3), inset 0 0 20px rgba(0,229,255,0.05); }
    50%      { box-shadow: 0 0 50px rgba(0,229,255,0.7), inset 0 0 30px rgba(0,229,255,0.1); }
  }

  .name {
    font-family: 'Orbitron', sans-serif;
    font-size: clamp(2rem, 6vw, 3.5rem);
    font-weight: 900;
    letter-spacing: 0.08em;
    color: #fff;
    position: relative;
    display: inline-block;
    animation: fadeSlideDown 0.8s ease both;
  }
  .name::before,
  .name::after {
    content: attr(data-text);
    position: absolute;
    top: 0; left: 0;
    width: 100%; height: 100%;
  }
  .name::before {
    color: var(--pink);
    animation: glitch1 4s infinite;
    clip-path: polygon(0 0, 100% 0, 100% 45%, 0 45%);
  }
  .name::after {
    color: var(--cyan);
    animation: glitch2 4s infinite;
    clip-path: polygon(0 55%, 100% 55%, 100% 100%, 0 100%);
  }
  @keyframes glitch1 {
    0%,94%,100% { transform: none; opacity: 0; }
    95% { transform: translate(-4px, 2px); opacity: 0.8; }
    97% { transform: translate(4px, -2px); opacity: 0.8; }
    99% { transform: translate(-2px, 0); opacity: 0.6; }
  }
  @keyframes glitch2 {
    0%,94%,100% { transform: none; opacity: 0; }
    96% { transform: translate(4px, -3px); opacity: 0.8; }
    98% { transform: translate(-4px, 3px); opacity: 0.8; }
  }

  .tagline {
    font-family: 'Share Tech Mono', monospace;
    font-size: 1rem;
    color: var(--cyan);
    margin-top: 10px;
    letter-spacing: 0.15em;
    animation: fadeSlideDown 0.8s 0.2s ease both;
  }
  .tagline span { animation: blink 1s step-end infinite; }

  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }
  @keyframes fadeSlideDown {
    from { opacity:0; transform: translateY(-20px); }
    to   { opacity:1; transform: translateY(0); }
  }

  /* Status badges */
  .badges {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 10px;
    margin-top: 20px;
    animation: fadeSlideDown 0.8s 0.4s ease both;
  }
  .badge {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.75rem;
    padding: 5px 14px;
    border: 1px solid var(--cyan);
    color: var(--cyan);
    letter-spacing: 0.1em;
    position: relative;
    overflow: hidden;
    transition: all 0.3s;
  }
  .badge::before {
    content: '';
    position: absolute;
    top: 0; left: -100%;
    width: 100%; height: 100%;
    background: linear-gradient(90deg, transparent, rgba(0,229,255,0.2), transparent);
    transition: left 0.4s;
  }
  .badge:hover::before { left: 100%; }
  .badge:hover {
    background: rgba(0,229,255,0.1);
    box-shadow: 0 0 20px rgba(0,229,255,0.4);
    transform: scale(1.05);
  }

  /* ── SECTION ── */
  section {
    margin: 50px 0;
    animation: fadeIn 0.6s ease both;
  }

  .section-title {
    font-family: 'Orbitron', sans-serif;
    font-size: 0.85rem;
    font-weight: 700;
    letter-spacing: 0.25em;
    color: var(--cyan);
    text-transform: uppercase;
    display: flex;
    align-items: center;
    gap: 14px;
    margin-bottom: 24px;
  }
  .section-title::before {
    content: '//';
    color: var(--pink);
    font-family: 'Share Tech Mono', monospace;
  }
  .section-title::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, var(--cyan), transparent);
    animation: lineGrow 1s ease both;
  }
  @keyframes lineGrow {
    from { transform: scaleX(0); transform-origin: left; }
    to   { transform: scaleX(1); }
  }

  /* ── CODE BLOCK ── */
  .code-block {
    background: var(--card);
    border: 1px solid var(--border);
    border-left: 3px solid var(--cyan);
    padding: 28px 32px;
    position: relative;
    overflow: hidden;
    font-family: 'Fira Code', monospace;
    font-size: 0.88rem;
    line-height: 1.9;
    box-shadow: 0 0 40px rgba(0,229,255,0.05), inset 0 0 40px rgba(0,229,255,0.02);
    animation: glitchIn 0.6s ease both;
  }
  .code-block::before {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background: linear-gradient(135deg, rgba(0,229,255,0.03) 0%, transparent 60%);
    pointer-events: none;
  }
  .code-block:hover {
    border-left-color: var(--green);
    box-shadow: 0 0 60px rgba(0,255,136,0.1), inset 0 0 40px rgba(0,255,136,0.02);
    transition: all 0.4s;
  }

  @keyframes glitchIn {
    0%   { opacity:0; transform: translateX(-10px) skewX(-2deg); filter: blur(4px); }
    60%  { opacity:1; transform: translateX(4px) skewX(1deg); filter: blur(0); }
    100% { transform: translateX(0) skewX(0deg); }
  }

  .kw  { color: #ff79c6; }
  .fn  { color: var(--cyan); }
  .st  { color: var(--green); }
  .cm  { color: #44607a; font-style: italic; }
  .var { color: #bd93f9; }
  .num { color: var(--yellow); }
  .at  { color: #ffb86c; }
  .ln  { color: #2a4a6a; margin-right: 20px; user-select: none; font-size: 0.78rem; }

  .typing-line {
    display: inline-block;
    overflow: hidden;
    white-space: nowrap;
    animation: typeIn 0.04s steps(1) both;
    border-right: 2px solid var(--cyan);
  }
  .typing-line:last-child { animation: typeIn 0.04s steps(1) 1.5s both, blinkCaret 1s 2s step-end infinite; }

  @keyframes typeIn {
    from { max-width: 0; }
    to   { max-width: 100%; }
  }
  @keyframes blinkCaret {
    0%,100% { border-color: var(--cyan); }
    50%     { border-color: transparent; }
  }

  /* Stagger each line */
  .code-block .line { display: block; opacity: 0; animation: lineAppear 0.3s ease forwards; }
  .code-block .line:nth-child(1)  { animation-delay: 0.1s; }
  .code-block .line:nth-child(2)  { animation-delay: 0.2s; }
  .code-block .line:nth-child(3)  { animation-delay: 0.3s; }
  .code-block .line:nth-child(4)  { animation-delay: 0.4s; }
  .code-block .line:nth-child(5)  { animation-delay: 0.5s; }
  .code-block .line:nth-child(6)  { animation-delay: 0.6s; }
  .code-block .line:nth-child(7)  { animation-delay: 0.7s; }
  .code-block .line:nth-child(8)  { animation-delay: 0.8s; }
  .code-block .line:nth-child(9)  { animation-delay: 0.9s; }
  .code-block .line:nth-child(10) { animation-delay: 1.0s; }
  .code-block .line:nth-child(11) { animation-delay: 1.1s; }
  .code-block .line:nth-child(12) { animation-delay: 1.2s; }
  .code-block .line:nth-child(13) { animation-delay: 1.3s; }
  .code-block .line:nth-child(14) { animation-delay: 1.4s; }
  .code-block .line:nth-child(15) { animation-delay: 1.5s; }
  @keyframes lineAppear {
    from { opacity:0; transform: translateX(-6px); }
    to   { opacity:1; transform: translateX(0); }
  }

  /* ── TECH GRID ── */
  .tech-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(110px, 1fr));
    gap: 12px;
  }
  .tech-item {
    background: var(--card);
    border: 1px solid var(--border);
    padding: 16px 10px;
    text-align: center;
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.78rem;
    color: #8ab4cc;
    letter-spacing: 0.08em;
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
    cursor: default;
    animation: popIn 0.4s ease both;
  }
  .tech-item:nth-child(1)  { animation-delay: 0.05s; }
  .tech-item:nth-child(2)  { animation-delay: 0.10s; }
  .tech-item:nth-child(3)  { animation-delay: 0.15s; }
  .tech-item:nth-child(4)  { animation-delay: 0.20s; }
  .tech-item:nth-child(5)  { animation-delay: 0.25s; }
  .tech-item:nth-child(6)  { animation-delay: 0.30s; }
  .tech-item:nth-child(7)  { animation-delay: 0.35s; }
  .tech-item:nth-child(8)  { animation-delay: 0.40s; }
  .tech-item:nth-child(9)  { animation-delay: 0.45s; }
  @keyframes popIn {
    from { opacity:0; transform: scale(0.8) translateY(10px); }
    to   { opacity:1; transform: scale(1) translateY(0); }
  }
  .tech-item .icon { font-size: 1.8rem; margin-bottom: 8px; display: block; }
  .tech-item::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0;
    width: 0; height: 2px;
    background: var(--cyan);
    transition: width 0.3s;
  }
  .tech-item:hover { color: var(--cyan); border-color: var(--cyan); background: rgba(0,229,255,0.06); transform: translateY(-4px); box-shadow: 0 8px 24px rgba(0,229,255,0.15); }
  .tech-item:hover::after { width: 100%; }
  .tech-item:hover .icon { animation: iconBounce 0.4s ease; }
  @keyframes iconBounce {
    0%,100% { transform: translateY(0); }
    40%     { transform: translateY(-6px); }
    70%     { transform: translateY(-2px); }
  }

  /* ── STATS ── */
  .stats-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }
  .stat-card {
    background: var(--card);
    border: 1px solid var(--border);
    padding: 20px;
    position: relative;
    overflow: hidden;
    animation: slideUp 0.5s ease both;
  }
  .stat-card:nth-child(1) { animation-delay: 0.1s; }
  .stat-card:nth-child(2) { animation-delay: 0.2s; }
  .stat-card:nth-child(3) { animation-delay: 0.3s; grid-column: span 2; }
  @keyframes slideUp {
    from { opacity:0; transform: translateY(20px); }
    to   { opacity:1; transform: translateY(0); }
  }
  .stat-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 100%; height: 2px;
    background: linear-gradient(90deg, var(--cyan), var(--pink));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.6s ease;
  }
  .stat-card:hover::before { transform: scaleX(1); }
  .stat-card img { width: 100%; display: block; filter: brightness(0.9); transition: filter 0.3s; }
  .stat-card:hover img { filter: brightness(1.1); }

  /* ── SOCIAL ── */
  .social-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 14px;
  }
  .social-btn {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 14px 20px;
    background: var(--card);
    border: 1px solid var(--border);
    color: #8ab4cc;
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.82rem;
    text-decoration: none;
    letter-spacing: 0.1em;
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
    animation: popIn 0.4s ease both;
  }
  .social-btn::before {
    content: '';
    position: absolute;
    left: -100%; top: 0;
    width: 100%; height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.04), transparent);
    transition: left 0.5s;
  }
  .social-btn:hover::before { left: 100%; }
  .social-btn:nth-child(1) { animation-delay:0.05s; --sc: #2CA5E0; }
  .social-btn:nth-child(2) { animation-delay:0.10s; --sc: #E4405F; }
  .social-btn:nth-child(3) { animation-delay:0.15s; --sc: #FF0000; }
  .social-btn:nth-child(4) { animation-delay:0.20s; --sc: #D14836; }
  .social-btn:hover { color: var(--sc, var(--cyan)); border-color: var(--sc, var(--cyan)); background: rgba(0,229,255,0.04); transform: translateX(6px); box-shadow: -4px 0 16px rgba(0,0,0,0.3); }
  .social-icon { font-size: 1.3rem; width: 24px; text-align: center; }

  /* ── FOOTER ── */
  footer {
    text-align: center;
    padding: 40px 0 20px;
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.78rem;
    color: #2a4a6a;
    letter-spacing: 0.15em;
    position: relative;
    z-index: 1;
  }
  footer::before {
    content: '';
    display: block;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--cyan), transparent);
    margin-bottom: 20px;
    animation: pulse 3s ease-in-out infinite;
  }
  @keyframes pulse {
    0%,100% { opacity:0.3; }
    50%     { opacity:1; }
  }

  /* Glitch flicker on body */
  @keyframes screenFlicker {
    0%,98%,100% { opacity:1; }
    99% { opacity:0.95; filter: brightness(1.05) hue-rotate(5deg); }
  }
  body { animation: screenFlicker 8s infinite; }

  @keyframes fadeIn {
    from { opacity: 0; }
    to   { opacity: 1; }
  }

  /* Responsive */
  @media(max-width:600px) {
    .stats-grid { grid-template-columns: 1fr; }
    .stat-card:nth-child(3) { grid-column: span 1; }
    .code-block { padding: 18px; font-size: 0.78rem; }
  }
</style>
</head>
<body>

<canvas id="matrix"></canvas>
<div id="cursor"></div>
<div id="cursor-dot"></div>

<div class="container">

  <!-- HEADER -->
  <header>
    <div class="avatar-ring">
      <svg viewBox="0 0 120 120">
        <defs>
          <linearGradient id="ringGrad" x1="0%" y1="0%" x2="100%" y2="100%">
            <stop offset="0%" style="stop-color:#00e5ff"/>
            <stop offset="50%" style="stop-color:#ff006e"/>
            <stop offset="100%" style="stop-color:#00ff88"/>
          </linearGradient>
        </defs>
        <circle cx="60" cy="60" r="56" fill="none" stroke="url(#ringGrad)" stroke-width="2" stroke-dasharray="8 4"/>
        <circle cx="60" cy="60" r="50" fill="none" stroke="rgba(0,229,255,0.15)" stroke-width="1"/>
      </svg>
      <div class="avatar-inner">👨‍💻</div>
    </div>

    <div class="name" data-text="SHEFFY SAMRA">SHEFFY SAMRA</div>
    <div class="tagline">[ FRONTEND_DEV &amp; PYTHON_ENTHUSIAST ]<span>_</span></div>

    <div class="badges">
      <span class="badge">📍 INDIA</span>
      <span class="badge">🐍 PYTHON</span>
      <span class="badge">🎨 FRONTEND</span>
      <span class="badge">🚀 OPEN SOURCE</span>
      <span class="badge">⚡ ALWAYS LEARNING</span>
    </div>
  </header>

  <!-- WHOAMI -->
  <section>
    <div class="section-title">whoami</div>
    <div class="code-block">
      <span class="line"><span class="kw">class</span> <span class="fn">SheffySamra</span>:</span>
      <span class="line">    <span class="kw">def</span> <span class="fn">__init__</span>(<span class="var">self</span>):</span>
      <span class="line">        <span class="var">self</span>.<span class="at">name</span>        = <span class="st">"Sheffy Samra"</span></span>
      <span class="line">        <span class="var">self</span>.<span class="at">location</span>    = <span class="st">"India 🇮🇳"</span></span>
      <span class="line">        <span class="var">self</span>.<span class="at">role</span>        = <span class="st">"Frontend Developer &amp; Python Enthusiast"</span></span>
      <span class="line">        <span class="var">self</span>.<span class="at">languages</span>   = [<span class="st">"Python"</span>, <span class="st">"JavaScript"</span>, <span class="st">"HTML"</span>, <span class="st">"CSS"</span>, <span class="st">"C"</span>, <span class="st">"Java"</span>]</span>
      <span class="line">        <span class="var">self</span>.<span class="at">passions</span>    = [<span class="st">"Clean Code"</span>, <span class="st">"UI/UX"</span>, <span class="st">"Automation"</span>, <span class="st">"Open Source"</span>]</span>
      <span class="line">        <span class="var">self</span>.<span class="at">currently</span>   = <span class="st">"Diving deep into advanced Python 🐍"</span></span>
      <span class="line">        <span class="var">self</span>.<span class="at">fun_fact</span>    = <span class="st">"Humor is the best debugger 😄"</span></span>
      <span class="line">        <span class="var">self</span>.<span class="at">contact</span>     = <span class="st">"sheffysamra30@gmail.com"</span></span>
      <span class="line"></span>
      <span class="line">    <span class="kw">def</span> <span class="fn">say_hi</span>(<span class="var">self</span>):</span>
      <span class="line">        <span class="fn">print</span>(<span class="st">"Thanks for visiting! Let's build something amazing."</span>)</span>
      <span class="line"></span>
      <span class="line"><span class="var">me</span> = <span class="fn">SheffySamra</span>()</span>
      <span class="line"><span class="var">me</span>.<span class="fn">say_hi</span>()  <span class="cm"># &gt;&gt;&gt; Thanks for visiting! Let's build something amazing.</span></span>
    </div>
  </section>

  <!-- TECH STACK -->
  <section>
    <div class="section-title">tech_stack</div>
    <div class="tech-grid">
      <div class="tech-item"><span class="icon">🐍</span>Python</div>
      <div class="tech-item"><span class="icon">⚡</span>JavaScript</div>
      <div class="tech-item"><span class="icon">🌐</span>HTML5</div>
      <div class="tech-item"><span class="icon">🎨</span>CSS3</div>
      <div class="tech-item"><span class="icon">🅱️</span>Bootstrap</div>
      <div class="tech-item"><span class="icon">🔀</span>Git</div>
      <div class="tech-item"><span class="icon">⚙️</span>C Lang</div>
      <div class="tech-item"><span class="icon">☕</span>Java</div>
      <div class="tech-item"><span class="icon">💻</span>VS Code</div>
    </div>
  </section>

  <!-- GITHUB STATS -->
  <section>
    <div class="section-title">github_stats</div>
    <div class="stats-grid">
      <div class="stat-card">
        <img src="https://github-readme-stats.vercel.app/api?username=sheffykhlg&show_icons=true&theme=github_dark&hide_border=true&bg_color=061525&title_color=00e5ff&icon_color=00e5ff&text_color=c9d1d9&ring_color=00e5ff" alt="stats"/>
      </div>
      <div class="stat-card">
        <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=sheffykhlg&layout=compact&theme=github_dark&hide_border=true&bg_color=061525&title_color=00e5ff&text_color=c9d1d9" alt="langs"/>
      </div>
      <div class="stat-card">
        <img src="https://github-readme-streak-stats.herokuapp.com/?user=sheffykhlg&theme=github-dark-blue&hide_border=true&background=061525&ring=00e5ff&fire=ff006e&currStreakLabel=00e5ff" alt="streak"/>
      </div>
    </div>
  </section>

  <!-- CONNECT -->
  <section>
    <div class="section-title">connect_with_me</div>
    <div class="social-grid">
      <a class="social-btn" href="https://t.me/SAMRABOTS" target="_blank">
        <span class="social-icon">✈️</span> TELEGRAM
      </a>
      <a class="social-btn" href="https://instagram.com/sheffy_samra" target="_blank">
        <span class="social-icon">📸</span> INSTAGRAM
      </a>
      <a class="social-btn" href="https://www.youtube.com/c/@samratechnical" target="_blank">
        <span class="social-icon">▶️</span> YOUTUBE
      </a>
      <a class="social-btn" href="mailto:sheffysamra30@gmail.com">
        <span class="social-icon">📧</span> GMAIL
      </a>
    </div>
  </section>

  <footer>
    &gt;&gt; "First, solve the problem. Then, write the code." &lt;&lt;<br/>
    <br/>© 2025 SHEFFY SAMRA · BUILT WITH ❤️ &amp; ☕
  </footer>

</div>

<script>
// Custom cursor
const cursor = document.getElementById('cursor');
const dot    = document.getElementById('cursor-dot');
document.addEventListener('mousemove', e => {
  cursor.style.left = (e.clientX - 10) + 'px';
  cursor.style.top  = (e.clientY - 10) + 'px';
  dot.style.left    = (e.clientX - 2.5) + 'px';
  dot.style.top     = (e.clientY - 2.5) + 'px';
});
document.querySelectorAll('a, .tech-item, .badge').forEach(el => {
  el.addEventListener('mouseenter', () => cursor.style.transform = 'scale(2)');
  el.addEventListener('mouseleave', () => cursor.style.transform = 'scale(1)');
});

// Matrix rain
const canvas = document.getElementById('matrix');
const ctx = canvas.getContext('2d');
function resize() { canvas.width = window.innerWidth; canvas.height = window.innerHeight; }
resize();
window.addEventListener('resize', resize);

const chars = 'アイウエオカキクケコサシスセソタチツテトナニヌネノ01アβΣΩ#@%';
const cols = Math.floor(canvas.width / 16);
const drops = Array(cols).fill(1);

function drawMatrix() {
  ctx.fillStyle = 'rgba(2,8,16,0.05)';
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  ctx.fillStyle = '#00e5ff';
  ctx.font = '14px Share Tech Mono, monospace';
  drops.forEach((y, i) => {
    const ch = chars[Math.floor(Math.random() * chars.length)];
    ctx.fillStyle = Math.random() > 0.95 ? '#ffffff' : '#00e5ff';
    ctx.fillText(ch, i * 16, y * 16);
    if (y * 16 > canvas.height && Math.random() > 0.975) drops[i] = 0;
    drops[i]++;
  });
}
setInterval(drawMatrix, 60);

// Random glitch on elements
const glitchTargets = document.querySelectorAll('.section-title, .name');
setInterval(() => {
  const el = glitchTargets[Math.floor(Math.random() * glitchTargets.length)];
  el.style.filter = 'hue-rotate(180deg) brightness(1.5)';
  el.style.transform = `translateX(${(Math.random()-0.5)*6}px)`;
  setTimeout(() => {
    el.style.filter = '';
    el.style.transform = '';
  }, 80);
}, 2500);

// Intersection observer for staggered reveal
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) e.target.style.animationPlayState = 'running';
  });
}, { threshold: 0.1 });
document.querySelectorAll('section').forEach(s => observer.observe(s));
</script>
</body>
</html>
