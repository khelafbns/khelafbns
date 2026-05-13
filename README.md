<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Khelaf Benabdesselam — Software Engineer</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet"/>
<style>
  :root {
    --bg: #080c10;
    --surface: #0d1117;
    --surface2: #161b22;
    --surface3: #1c2430;
    --accent: #00e5a0;
    --accent2: #0af;
    --accent3: #7c5cfc;
    --text: #e6edf3;
    --muted: #7d8590;
    --border: rgba(255,255,255,0.08);
    --mono: 'Space Mono', monospace;
    --sans: 'Syne', sans-serif;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--sans);
    overflow-x: hidden;
    line-height: 1.6;
  }

  /* CANVAS BACKGROUND */
  #bg-canvas {
    position: fixed;
    inset: 0;
    z-index: 0;
    pointer-events: none;
    opacity: 0.35;
  }

  /* NAV */
  nav {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 100;
    padding: 1.2rem 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: rgba(8,12,16,0.8);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
    animation: slideDown 0.6s ease both;
  }

  .nav-logo {
    font-family: var(--mono);
    font-size: 1rem;
    color: var(--accent);
    letter-spacing: 0.05em;
  }

  .nav-links {
    display: flex;
    gap: 2rem;
    list-style: none;
  }

  .nav-links a {
    font-size: 0.85rem;
    color: var(--muted);
    text-decoration: none;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    transition: color 0.2s;
  }

  .nav-links a:hover { color: var(--accent); }

  /* SECTIONS */
  section {
    position: relative;
    z-index: 1;
  }

  /* HERO */
  .hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 6rem 4rem 4rem;
    max-width: 1200px;
    margin: 0 auto;
  }

  .hero-label {
    font-family: var(--mono);
    font-size: 0.78rem;
    color: var(--accent);
    letter-spacing: 0.25em;
    text-transform: uppercase;
    margin-bottom: 1.5rem;
    opacity: 0;
    animation: fadeUp 0.6s 0.3s ease both;
  }

  .hero-label::before {
    content: '';
    display: inline-block;
    width: 2rem;
    height: 1px;
    background: var(--accent);
    vertical-align: middle;
    margin-right: 0.75rem;
  }

  .hero-name {
    font-size: clamp(3rem, 7vw, 6.5rem);
    font-weight: 800;
    line-height: 1.05;
    letter-spacing: -0.02em;
    margin-bottom: 1rem;
    opacity: 0;
    animation: fadeUp 0.7s 0.45s ease both;
  }

  .hero-name span {
    display: block;
    background: linear-gradient(135deg, var(--text) 0%, var(--muted) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-name .highlight {
    background: linear-gradient(135deg, var(--accent) 0%, var(--accent2) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-role {
    font-family: var(--mono);
    font-size: clamp(0.9rem, 2vw, 1.1rem);
    color: var(--muted);
    margin-bottom: 2.5rem;
    opacity: 0;
    animation: fadeUp 0.7s 0.6s ease both;
  }

  .typewriter-text {
    color: var(--accent2);
  }

  .cursor {
    display: inline-block;
    width: 2px;
    height: 1.1em;
    background: var(--accent2);
    vertical-align: text-bottom;
    animation: blink 1s step-end infinite;
  }

  .hero-desc {
    max-width: 540px;
    font-size: 1.05rem;
    color: var(--muted);
    line-height: 1.8;
    margin-bottom: 3rem;
    opacity: 0;
    animation: fadeUp 0.7s 0.75s ease both;
  }

  .hero-cta {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.7s 0.9s ease both;
  }

  .btn {
    font-family: var(--mono);
    font-size: 0.8rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    padding: 0.85rem 2rem;
    border-radius: 4px;
    cursor: pointer;
    text-decoration: none;
    transition: all 0.25s ease;
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
  }

  .btn-primary {
    background: var(--accent);
    color: #000;
    border: none;
    font-weight: 700;
  }

  .btn-primary:hover {
    background: #00ffb3;
    transform: translateY(-2px);
    box-shadow: 0 8px 30px rgba(0,229,160,0.3);
  }

  .btn-secondary {
    background: transparent;
    color: var(--text);
    border: 1px solid var(--border);
  }

  .btn-secondary:hover {
    border-color: var(--accent);
    color: var(--accent);
    transform: translateY(-2px);
  }

  /* SCROLL INDICATOR */
  .scroll-hint {
    position: absolute;
    bottom: 2.5rem;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    opacity: 0;
    animation: fadeIn 1s 1.5s ease both;
  }

  .scroll-hint span {
    font-family: var(--mono);
    font-size: 0.65rem;
    color: var(--muted);
    letter-spacing: 0.15em;
    text-transform: uppercase;
  }

  .scroll-line {
    width: 1px;
    height: 3rem;
    background: linear-gradient(to bottom, var(--accent), transparent);
    animation: scrollPulse 2s ease-in-out infinite;
  }

  /* ABOUT / STATUS */
  .status-grid {
    padding: 5rem 4rem;
    max-width: 1200px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem;
  }

  .status-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 1.75rem;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
    opacity: 0;
    transform: translateY(30px);
  }

  .status-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    transform: scaleX(0);
    transition: transform 0.3s ease;
  }

  .status-card:hover {
    border-color: rgba(0,229,160,0.2);
    transform: translateY(-4px);
    box-shadow: 0 20px 40px rgba(0,0,0,0.3);
  }

  .status-card:hover::before { transform: scaleX(1); }

  .card-icon {
    width: 40px;
    height: 40px;
    border-radius: 8px;
    background: rgba(0,229,160,0.1);
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 1rem;
    font-size: 1.1rem;
  }

  .card-label {
    font-family: var(--mono);
    font-size: 0.68rem;
    color: var(--accent);
    letter-spacing: 0.2em;
    text-transform: uppercase;
    margin-bottom: 0.5rem;
  }

  .card-title {
    font-size: 1rem;
    font-weight: 600;
    color: var(--text);
    line-height: 1.4;
  }

  /* SKILLS */
  .skills-section {
    padding: 5rem 4rem;
    max-width: 1200px;
    margin: 0 auto;
  }

  .section-header {
    margin-bottom: 3rem;
    opacity: 0;
    transform: translateY(20px);
  }

  .section-label {
    font-family: var(--mono);
    font-size: 0.72rem;
    color: var(--accent);
    letter-spacing: 0.25em;
    text-transform: uppercase;
    margin-bottom: 0.75rem;
    display: flex;
    align-items: center;
    gap: 0.75rem;
  }

  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
    max-width: 200px;
  }

  .section-title {
    font-size: clamp(2rem, 4vw, 3rem);
    font-weight: 800;
    letter-spacing: -0.02em;
    color: var(--text);
  }

  .skills-categories {
    display: flex;
    flex-direction: column;
    gap: 2.5rem;
  }

  .skill-category {
    opacity: 0;
    transform: translateY(20px);
  }

  .skill-cat-label {
    font-family: var(--mono);
    font-size: 0.68rem;
    color: var(--muted);
    letter-spacing: 0.2em;
    text-transform: uppercase;
    margin-bottom: 1rem;
    padding-left: 0.5rem;
    border-left: 2px solid var(--accent3);
  }

  .skills-row {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
  }

  .skill-pill {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 0.5rem 1rem;
    font-family: var(--mono);
    font-size: 0.78rem;
    color: var(--muted);
    transition: all 0.2s ease;
    cursor: default;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .skill-pill:hover {
    color: var(--accent);
    border-color: rgba(0,229,160,0.3);
    background: rgba(0,229,160,0.05);
    transform: translateY(-2px);
  }

  .skill-dot {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: var(--accent3);
    flex-shrink: 0;
  }

  /* STATS */
  .stats-section {
    padding: 5rem 4rem;
    background: var(--surface);
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
  }

  .stats-inner {
    max-width: 1200px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 4rem;
    align-items: center;
  }

  .stats-text { }

  .stats-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1.5rem;
  }

  .stat-box {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 1.5rem;
    text-align: center;
    transition: all 0.3s;
    opacity: 0;
    transform: scale(0.95);
  }

  .stat-box:hover {
    border-color: rgba(0,229,160,0.2);
    transform: scale(1.03);
  }

  .stat-num {
    font-size: 2.5rem;
    font-weight: 800;
    line-height: 1;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 0.5rem;
  }

  .stat-label {
    font-family: var(--mono);
    font-size: 0.7rem;
    color: var(--muted);
    letter-spacing: 0.12em;
    text-transform: uppercase;
  }

  /* CONTACT */
  .contact-section {
    padding: 7rem 4rem;
    max-width: 1200px;
    margin: 0 auto;
    text-align: center;
  }

  .contact-email {
    font-family: var(--mono);
    font-size: clamp(1rem, 2.5vw, 1.4rem);
    color: var(--accent);
    text-decoration: none;
    border-bottom: 1px solid rgba(0,229,160,0.3);
    padding-bottom: 4px;
    transition: all 0.2s;
  }

  .contact-email:hover {
    border-color: var(--accent);
    text-shadow: 0 0 20px rgba(0,229,160,0.4);
  }

  .contact-big {
    font-size: clamp(2.5rem, 5vw, 4.5rem);
    font-weight: 800;
    letter-spacing: -0.03em;
    margin-bottom: 1.5rem;
    color: var(--text);
  }

  .contact-sub {
    font-size: 1rem;
    color: var(--muted);
    max-width: 440px;
    margin: 0 auto 3rem;
    line-height: 1.8;
  }

  /* FOOTER */
  footer {
    border-top: 1px solid var(--border);
    padding: 2rem 4rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: relative;
    z-index: 1;
  }

  footer p {
    font-family: var(--mono);
    font-size: 0.72rem;
    color: var(--muted);
  }

  footer a {
    color: var(--accent);
    text-decoration: none;
  }

  /* DIVIDER LINE */
  .divider {
    width: 100%;
    height: 1px;
    background: var(--border);
  }

  /* AVAILABLE BADGE */
  .available-badge {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    background: rgba(0,229,160,0.08);
    border: 1px solid rgba(0,229,160,0.2);
    border-radius: 100px;
    padding: 0.4rem 1rem;
    font-family: var(--mono);
    font-size: 0.72rem;
    color: var(--accent);
    margin-bottom: 2rem;
    opacity: 0;
    animation: fadeUp 0.6s 0.15s ease both;
  }

  .badge-dot {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: var(--accent);
    animation: pulse 2s ease-in-out infinite;
  }

  /* TECH STACK LOGOS */
  .tech-logos {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
    margin-top: 3rem;
    opacity: 0;
  }

  .tech-logo-img {
    width: 36px;
    height: 36px;
    filter: grayscale(1) brightness(0.6);
    transition: all 0.3s;
    border-radius: 6px;
  }

  .tech-logo-img:hover {
    filter: grayscale(0) brightness(1);
    transform: translateY(-3px) scale(1.1);
  }

  /* ANIMATIONS */
  @keyframes slideDown {
    from { transform: translateY(-100%); opacity: 0; }
    to { transform: translateY(0); opacity: 1; }
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }

  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }

  @keyframes scrollPulse {
    0%, 100% { opacity: 1; transform: scaleY(1); transform-origin: top; }
    50% { opacity: 0.4; }
  }

  @keyframes pulse {
    0%, 100% { box-shadow: 0 0 0 0 rgba(0,229,160,0.4); }
    50% { box-shadow: 0 0 0 5px rgba(0,229,160,0); }
  }

  @keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-10px); }
  }

  .visible {
    opacity: 1 !important;
    transform: translateY(0) scale(1) !important;
    transition: opacity 0.6s ease, transform 0.6s ease;
  }

  /* GRID LINES DECORATION */
  .grid-decoration {
    position: absolute;
    right: 0;
    top: 50%;
    transform: translateY(-50%);
    width: 380px;
    height: 380px;
    opacity: 0.04;
    pointer-events: none;
    background-image:
      linear-gradient(var(--accent) 1px, transparent 1px),
      linear-gradient(90deg, var(--accent) 1px, transparent 1px);
    background-size: 40px 40px;
    border-radius: 12px;
  }

  @media (max-width: 768px) {
    .hero, .skills-section, .contact-section { padding: 5rem 1.5rem 3rem; }
    .status-grid { padding: 3rem 1.5rem; }
    .stats-inner { grid-template-columns: 1fr; gap: 2rem; }
    .stats-section { padding: 3rem 1.5rem; }
    footer { padding: 1.5rem; flex-direction: column; gap: 0.75rem; text-align: center; }
    .nav-links { display: none; }
  }
</style>
</head>
<body>

<canvas id="bg-canvas"></canvas>

<!-- NAV -->
<nav>
  <div class="nav-logo">_KB</div>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#skills">Skills</a></li>
    <li><a href="#stats">Stats</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <a href="mailto:kh.8bns@gmail.com" class="btn btn-primary" style="padding: 0.55rem 1.2rem; font-size: 0.72rem;">Hire Me →</a>
</nav>

<!-- HERO -->
<section class="hero" id="about">
  <div class="grid-decoration"></div>

  <div class="available-badge">
    <span class="badge-dot"></span>
    Available for collaboration
  </div>

  <p class="hero-label">Software Engineer</p>

  <h1 class="hero-name">
    <span>Khelaf</span>
    <span class="highlight">Benabdesselam</span>
  </h1>

  <p class="hero-role">
    &gt; Specializing in&nbsp;
    <span class="typewriter-text" id="typewriter"></span><span class="cursor"></span>
  </p>

  <p class="hero-desc">
    Building modern fullstack applications with React, NestJS, and Node.js.
    Currently crafting <strong style="color: var(--text);">JinStore</strong> — a modern e-commerce platform,
    while leveling up in Kubernetes & DevOps.
  </p>

  <div class="hero-cta">
    <a href="mailto:kh.8bns@gmail.com" class="btn btn-primary">Say Hello →</a>
    <a href="https://linkedin.com/in/khelaf-benabdesselam" class="btn btn-secondary" target="_blank">LinkedIn ↗</a>
  </div>

  <div class="scroll-hint">
    <span>Scroll</span>
    <div class="scroll-line"></div>
  </div>
</section>

<!-- STATUS CARDS -->
<section id="status">
  <div class="status-grid">

    <div class="status-card">
      <div class="card-icon">🚀</div>
      <div class="card-label">Currently Building</div>
      <div class="card-title">JinStore — Modern Fullstack E-Commerce Platform</div>
    </div>

    <div class="status-card">
      <div class="card-icon" style="background: rgba(10,170,255,0.1);">📖</div>
      <div class="card-label">Currently Learning</div>
      <div class="card-title">Kubernetes & DevOps — Container orchestration at scale</div>
    </div>

    <div class="status-card">
      <div class="card-icon" style="background: rgba(124,92,252,0.1);">🤝</div>
      <div class="card-label">Looking to Collaborate</div>
      <div class="card-title">Open Source Fullstack & SaaS Projects</div>
    </div>

    <div class="status-card">
      <div class="card-icon" style="background: rgba(255,160,50,0.1);">💡</div>
      <div class="card-label">Seeking Guidance On</div>
      <div class="card-title">Scalable System Design, DevOps & Cloud Architecture</div>
    </div>

  </div>
</section>

<div class="divider"></div>

<!-- SKILLS -->
<section class="skills-section" id="skills">
  <div class="section-header">
    <div class="section-label">Tech Stack</div>
    <h2 class="section-title">Languages & Tools</h2>
  </div>

  <div class="skills-categories">

    <div class="skill-category">
      <div class="skill-cat-label">Frontend</div>
      <div class="skills-row">
        <span class="skill-pill"><span class="skill-dot" style="background:#61dafb"></span>React</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#61dafb"></span>React Native</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#000"></span>Next.js</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#3178c6"></span>TypeScript</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#f7df1e"></span>JavaScript</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#e34f26"></span>HTML5</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#1572b6"></span>CSS3</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#06b6d4"></span>Tailwind CSS</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#7952b3"></span>Bootstrap</span>
      </div>
    </div>

    <div class="skill-category">
      <div class="skill-cat-label">Backend</div>
      <div class="skills-row">
        <span class="skill-pill"><span class="skill-dot" style="background:#e0234e"></span>NestJS</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#000"></span>Express.js</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#68a063"></span>Node.js</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#3776ab"></span>Python</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#b07219"></span>Java</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#00599c"></span>C/C++</span>
      </div>
    </div>

    <div class="skill-category">
      <div class="skill-cat-label">Data & Cloud</div>
      <div class="skills-row">
        <span class="skill-pill"><span class="skill-dot" style="background:#47a248"></span>MongoDB</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#4479a1"></span>MySQL</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#dc382d"></span>Redis</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#ff9900"></span>Firebase</span>
        <span class="skill-dot" style="display:none"></span>
      </div>
    </div>

    <div class="skill-category">
      <div class="skill-cat-label">DevOps & Tools</div>
      <div class="skills-row">
        <span class="skill-pill"><span class="skill-dot" style="background:#2496ed"></span>Docker</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#326ce5"></span>Kubernetes</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#f05032"></span>Git</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#fcc624"></span>Linux</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#ff6c37"></span>Postman</span>
        <span class="skill-pill"><span class="skill-dot" style="background:#f24e1e"></span>Figma</span>
      </div>
    </div>

  </div>
</section>

<div class="divider"></div>

<!-- STATS -->
<section class="stats-section" id="stats">
  <div class="stats-inner">
    <div class="stats-text">
      <div class="section-label" style="opacity:0;transform:translateY(20px)" id="stats-label">GitHub Activity</div>
      <h2 class="section-title" style="opacity:0;transform:translateY(20px);font-size:clamp(1.8rem,3vw,2.8rem);margin-bottom:1rem" id="stats-title">Code Stats</h2>
      <p style="color:var(--muted);font-size:0.95rem;line-height:1.8;opacity:0;transform:translateY(20px)" id="stats-desc">
        Passionate about clean architecture and scalable solutions.
        Always pushing commits, always learning.
      </p>
      <div style="margin-top:2rem;opacity:0;transform:translateY(20px)" id="stats-badges">
        <img src="https://github-readme-streak-stats.herokuapp.com/?user=khelafbns&theme=dark&background=0d1117&border=30363d&ring=00e5a0&fire=0af&currStreakLabel=00e5a0" alt="GitHub Streak" style="border-radius:8px;max-width:100%;border:1px solid var(--border)"/>
      </div>
    </div>

    <div class="stats-grid">
      <div class="stat-box">
        <div class="stat-num" id="c1">0</div>
        <div class="stat-label">Projects Built</div>
      </div>
      <div class="stat-box">
        <div class="stat-num" id="c2">0</div>
        <div class="stat-label">Technologies</div>
      </div>
      <div class="stat-box">
        <div class="stat-num" id="c3">0</div>
        <div class="stat-label">Years Coding</div>
      </div>
      <div class="stat-box">
        <div class="stat-num" id="c4">∞</div>
        <div class="stat-label">Lines of Code</div>
      </div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section class="contact-section" id="contact">
  <p class="section-label" style="justify-content:center;opacity:0;transform:translateY(20px)" id="contact-label">Get In Touch</p>
  <h2 class="contact-big" style="opacity:0;transform:translateY(20px)" id="contact-title">Let's Build Something.</h2>
  <p class="contact-sub" style="opacity:0;transform:translateY(20px)" id="contact-sub">
    Open to collaborations on Open Source, SaaS platforms, and fullstack projects. Reach out — I'd love to talk.
  </p>
  <div style="opacity:0;transform:translateY(20px)" id="contact-cta">
    <a href="mailto:kh.8bns@gmail.com" class="contact-email">kh.8bns@gmail.com</a>
    <div style="margin-top:2.5rem;display:flex;justify-content:center;gap:1rem;flex-wrap:wrap">
      <a href="mailto:kh.8bns@gmail.com" class="btn btn-primary">Send Email →</a>
      <a href="https://github.com/khelafbns" class="btn btn-secondary" target="_blank">GitHub ↗</a>
      <a href="https://linkedin.com/in/khelaf-benabdesselam" class="btn btn-secondary" target="_blank">LinkedIn ↗</a>
    </div>
  </div>
</section>

<footer>
  <p>© 2025 <a href="#">Khelaf Benabdesselam</a> — Built with passion</p>
  <p style="font-family:var(--mono);font-size:0.72rem;color:var(--muted)">
    React · NestJS · Node.js
  </p>
</footer>

<script>
/* Animated canvas background */
const canvas = document.getElementById('bg-canvas');
const ctx = canvas.getContext('2d');
let W, H, particles = [];

function resize() {
  W = canvas.width = window.innerWidth;
  H = canvas.height = window.innerHeight;
}
resize();
window.addEventListener('resize', resize);

class Particle {
  constructor() { this.reset(); }
  reset() {
    this.x = Math.random() * W;
    this.y = Math.random() * H;
    this.vx = (Math.random() - 0.5) * 0.3;
    this.vy = (Math.random() - 0.5) * 0.3;
    this.r = Math.random() * 1.5 + 0.5;
    this.alpha = Math.random() * 0.5 + 0.2;
  }
  update() {
    this.x += this.vx;
    this.y += this.vy;
    if (this.x < 0 || this.x > W || this.y < 0 || this.y > H) this.reset();
  }
}

for (let i = 0; i < 100; i++) particles.push(new Particle());

function drawCanvas() {
  ctx.clearRect(0, 0, W, H);
  particles.forEach(p => {
    p.update();
    ctx.beginPath();
    ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(0, 229, 160, ${p.alpha})`;
    ctx.fill();
  });

  /* Draw lines between close particles */
  for (let i = 0; i < particles.length; i++) {
    for (let j = i + 1; j < particles.length; j++) {
      const dx = particles[i].x - particles[j].x;
      const dy = particles[i].y - particles[j].y;
      const d = Math.sqrt(dx*dx + dy*dy);
      if (d < 120) {
        ctx.beginPath();
        ctx.moveTo(particles[i].x, particles[i].y);
        ctx.lineTo(particles[j].x, particles[j].y);
        ctx.strokeStyle = `rgba(0, 229, 160, ${0.06 * (1 - d/120)})`;
        ctx.lineWidth = 0.5;
        ctx.stroke();
      }
    }
  }
  requestAnimationFrame(drawCanvas);
}
drawCanvas();

/* Typewriter effect */
const phrases = [
  'Fullstack Web Development',
  'React & NestJS Expert',
  'E-Commerce Platforms',
  'Scalable APIs & Microservices',
];
let pI = 0, cI = 0, deleting = false;
const el = document.getElementById('typewriter');

function type() {
  const phrase = phrases[pI];
  if (!deleting) {
    el.textContent = phrase.slice(0, ++cI);
    if (cI === phrase.length) { deleting = true; setTimeout(type, 2000); return; }
  } else {
    el.textContent = phrase.slice(0, --cI);
    if (cI === 0) { deleting = false; pI = (pI + 1) % phrases.length; }
  }
  setTimeout(type, deleting ? 45 : 80);
}
setTimeout(type, 1200);

/* Scroll reveal */
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('visible');
      observer.unobserve(e.target);
    }
  });
}, { threshold: 0.12 });

document.querySelectorAll('.status-card, .section-header, .skill-category, .stat-box, .tech-logos,#stats-label,#stats-title,#stats-desc,#stats-badges,#contact-label,#contact-title,#contact-sub,#contact-cta').forEach(el => observer.observe(el));

/* Counter animation */
function animateCounter(el, target, duration) {
  let start = 0;
  const step = timestamp => {
    if (!start) start = timestamp;
    const prog = Math.min((timestamp - start) / duration, 1);
    el.textContent = Math.round(prog * target) + '+';
    if (prog < 1) requestAnimationFrame(step);
  };
  requestAnimationFrame(step);
}

const statsObserver = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      animateCounter(document.getElementById('c1'), 15, 1500);
      animateCounter(document.getElementById('c2'), 20, 1600);
      animateCounter(document.getElementById('c3'), 4, 800);
      statsObserver.disconnect();
    }
  });
}, { threshold: 0.4 });

statsObserver.observe(document.getElementById('stats'));

document.querySelectorAll('.stat-box').forEach(b => observer.observe(b));
</script>
</body>
</html>
