<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mohammad Mahdi Mohammadi — Developer</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=Inter:wght@300;400;500&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #07070d;
    --bg2: #0d0d1a;
    --blue: #00d4ff;
    --purple: #7c3aed;
    --pink: #f43f8e;
    --text: #e2e8f0;
    --muted: #64748b;
    --card: rgba(255,255,255,0.03);
    --border: rgba(0,212,255,0.12);
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Inter', sans-serif;
    overflow-x: hidden;
    line-height: 1.6;
  }

  /* ── CANVAS ── */
  #canvas {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    pointer-events: none;
    z-index: 0;
    opacity: 0.35;
  }

  /* ── HERO ── */
  .hero {
    position: relative;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1;
    padding: 2rem;
  }

  .hero-inner {
    text-align: center;
    max-width: 800px;
  }

  .badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: rgba(0,212,255,0.08);
    border: 1px solid rgba(0,212,255,0.25);
    border-radius: 100px;
    padding: 6px 18px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem;
    color: var(--blue);
    letter-spacing: 0.08em;
    margin-bottom: 2rem;
    animation: fadeUp 0.8s ease both;
  }

  .badge .dot {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: var(--blue);
    animation: pulse 2s infinite;
  }

  .hero h1 {
    font-family: 'Space Grotesk', sans-serif;
    font-size: clamp(2.8rem, 7vw, 6rem);
    font-weight: 700;
    line-height: 1.05;
    letter-spacing: -0.03em;
    animation: fadeUp 0.9s ease both;
    animation-delay: 0.1s;
  }

  .hero h1 .name-grad {
    background: linear-gradient(135deg, var(--blue) 0%, var(--purple) 50%, var(--pink) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-sub {
    font-family: 'JetBrains Mono', monospace;
    font-size: 1rem;
    color: var(--muted);
    margin-top: 1.2rem;
    animation: fadeUp 1s ease both;
    animation-delay: 0.2s;
  }

  .hero-sub .cursor {
    display: inline-block;
    width: 2px; height: 1.1em;
    background: var(--blue);
    vertical-align: middle;
    margin-left: 3px;
    animation: blink 1.1s step-end infinite;
  }

  .hero-desc {
    font-size: 1.05rem;
    color: var(--muted);
    max-width: 500px;
    margin: 1.8rem auto 0;
    animation: fadeUp 1.1s ease both;
    animation-delay: 0.3s;
  }

  .hero-links {
    display: flex;
    gap: 1rem;
    justify-content: center;
    flex-wrap: wrap;
    margin-top: 2.5rem;
    animation: fadeUp 1.2s ease both;
    animation-delay: 0.4s;
  }

  .btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 12px 24px;
    border-radius: 10px;
    font-family: 'Space Grotesk', sans-serif;
    font-weight: 500;
    font-size: 0.9rem;
    text-decoration: none;
    transition: all 0.25s ease;
    cursor: pointer;
  }

  .btn-primary {
    background: linear-gradient(135deg, var(--blue), var(--purple));
    color: #fff;
    border: none;
    box-shadow: 0 0 30px rgba(0,212,255,0.25);
  }

  .btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 0 50px rgba(0,212,255,0.4);
  }

  .btn-ghost {
    background: transparent;
    color: var(--text);
    border: 1px solid var(--border);
  }

  .btn-ghost:hover {
    border-color: var(--blue);
    color: var(--blue);
    background: rgba(0,212,255,0.05);
    transform: translateY(-2px);
  }

  /* ── SCROLL INDICATOR ── */
  .scroll-hint {
    position: absolute;
    bottom: 2.5rem;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    color: var(--muted);
    font-size: 0.72rem;
    letter-spacing: 0.1em;
    font-family: 'JetBrains Mono', monospace;
    animation: fadeUp 1.5s ease both 0.8s;
  }

  .scroll-bar {
    width: 1px;
    height: 40px;
    background: linear-gradient(to bottom, var(--blue), transparent);
    animation: scrollAnim 1.8s ease-in-out infinite;
  }

  /* ── SECTIONS ── */
  section {
    position: relative;
    z-index: 1;
    padding: 6rem 2rem;
    max-width: 1100px;
    margin: 0 auto;
  }

  .section-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem;
    color: var(--blue);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 1rem;
  }

  .section-title {
    font-family: 'Space Grotesk', sans-serif;
    font-size: clamp(1.8rem, 4vw, 2.8rem);
    font-weight: 700;
    letter-spacing: -0.02em;
    margin-bottom: 0.5rem;
  }

  .section-title span {
    background: linear-gradient(90deg, var(--blue), var(--purple));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .divider {
    width: 50px;
    height: 2px;
    background: linear-gradient(90deg, var(--blue), transparent);
    margin: 1.2rem 0 2.5rem;
  }

  /* ── STATS ── */
  .stats-row {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 1rem;
    margin-top: 3rem;
  }

  .stat-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 1.8rem 1.5rem;
    text-align: center;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }

  .stat-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--blue), var(--purple));
    transform: scaleX(0);
    transition: transform 0.4s ease;
  }

  .stat-card:hover::before { transform: scaleX(1); }

  .stat-card:hover {
    transform: translateY(-4px);
    border-color: rgba(0,212,255,0.3);
    box-shadow: 0 20px 50px rgba(0,212,255,0.08);
  }

  .stat-num {
    font-family: 'Space Grotesk', sans-serif;
    font-size: 2.5rem;
    font-weight: 700;
    background: linear-gradient(135deg, var(--blue), var(--purple));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    line-height: 1;
    margin-bottom: 0.5rem;
  }

  .stat-label {
    font-size: 0.85rem;
    color: var(--muted);
  }

  /* ── SKILLS ── */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.2rem;
  }

  .skill-group {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 1.8rem;
    transition: all 0.3s ease;
  }

  .skill-group:hover {
    border-color: rgba(124,58,237,0.3);
    transform: translateY(-3px);
    box-shadow: 0 20px 50px rgba(124,58,237,0.08);
  }

  .skill-group-title {
    font-family: 'Space Grotesk', sans-serif;
    font-weight: 600;
    font-size: 1rem;
    margin-bottom: 1.2rem;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .skill-icon {
    width: 32px; height: 32px;
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1rem;
  }

  .skill-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }

  .tag {
    padding: 5px 14px;
    border-radius: 100px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem;
    transition: all 0.2s ease;
    cursor: default;
  }

  .tag-blue { background: rgba(0,212,255,0.08); color: var(--blue); border: 1px solid rgba(0,212,255,0.2); }
  .tag-purple { background: rgba(124,58,237,0.08); color: #a78bfa; border: 1px solid rgba(124,58,237,0.2); }
  .tag-pink { background: rgba(244,63,142,0.08); color: #f9a8d4; border: 1px solid rgba(244,63,142,0.2); }
  .tag-green { background: rgba(16,185,129,0.08); color: #34d399; border: 1px solid rgba(16,185,129,0.2); }

  .tag:hover { transform: scale(1.05); filter: brightness(1.2); }

  /* ── PROJECTS ── */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.2rem;
  }

  .project-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 1.8rem;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }

  .project-card::after {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba(0,212,255,0.03), rgba(124,58,237,0.03));
    opacity: 0;
    transition: opacity 0.3s ease;
  }

  .project-card:hover { transform: translateY(-5px); border-color: rgba(0,212,255,0.25); }
  .project-card:hover::after { opacity: 1; }

  .project-header {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    margin-bottom: 1rem;
  }

  .project-emoji {
    font-size: 2rem;
    line-height: 1;
  }

  .project-arrow {
    color: var(--muted);
    font-size: 1.2rem;
    transition: all 0.2s ease;
  }

  .project-card:hover .project-arrow {
    color: var(--blue);
    transform: translate(3px, -3px);
  }

  .project-name {
    font-family: 'Space Grotesk', sans-serif;
    font-weight: 600;
    font-size: 1.05rem;
    margin-bottom: 0.5rem;
  }

  .project-desc {
    font-size: 0.85rem;
    color: var(--muted);
    line-height: 1.6;
  }

  /* ── CONTACT ── */
  .contact-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 1rem;
  }

  .contact-card {
    display: flex;
    align-items: center;
    gap: 14px;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 1.2rem 1.5rem;
    text-decoration: none;
    color: var(--text);
    transition: all 0.3s ease;
  }

  .contact-card:hover {
    transform: translateY(-3px);
    border-color: var(--blue);
    box-shadow: 0 15px 40px rgba(0,212,255,0.1);
  }

  .contact-icon {
    width: 40px; height: 40px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.1rem;
    flex-shrink: 0;
  }

  .contact-info .label {
    font-size: 0.72rem;
    color: var(--muted);
    letter-spacing: 0.05em;
    margin-bottom: 2px;
  }

  .contact-info .value {
    font-family: 'Space Grotesk', sans-serif;
    font-weight: 500;
    font-size: 0.9rem;
  }

  /* ── FOOTER ── */
  footer {
    position: relative;
    z-index: 1;
    text-align: center;
    padding: 3rem 2rem;
    border-top: 1px solid var(--border);
    color: var(--muted);
    font-size: 0.82rem;
    font-family: 'JetBrains Mono', monospace;
  }

  footer span {
    background: linear-gradient(90deg, var(--blue), var(--purple));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50%       { opacity: 0.5; transform: scale(0.85); }
  }

  @keyframes blink {
    0%, 100% { opacity: 1; }
    50%       { opacity: 0; }
  }

  @keyframes scrollAnim {
    0%   { transform: scaleY(0); transform-origin: top; }
    50%  { transform: scaleY(1); transform-origin: top; }
    51%  { transform: scaleY(1); transform-origin: bottom; }
    100% { transform: scaleY(0); transform-origin: bottom; }
  }

  /* Scroll reveal */
  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }

  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  @media (max-width: 640px) {
    section { padding: 4rem 1.2rem; }
    .hero h1 { font-size: 2.5rem; }
  }
</style>
</head>
<body>

<canvas id="canvas"></canvas>

<!-- ══ HERO ══ -->
<div class="hero">
  <div class="hero-inner">

    <div class="badge">
      <span class="dot"></span>
      Available for collaboration
    </div>

    <h1>
      <span class="name-grad">Mohammad Mahdi</span><br>
      Mohammadi
    </h1>

    <p class="hero-sub">
      <span id="typewriter"></span><span class="cursor"></span>
    </p>

    <p class="hero-desc">
      Backend developer crafting robust systems with Python — blending clean architecture with real-world solutions.
    </p>

    <div class="hero-links">
      <a href="https://github.com/bluelifemmd2007-cell" target="_blank" class="btn btn-primary">
        <svg width="16" height="16" fill="currentColor" viewBox="0 0 24 24"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
        GitHub
      </a>
      <a href="https://bluelifemmd2007-cell.github.io/-mmd-web-profile/" target="_blank" class="btn btn-ghost">
        🌐 Portfolio
      </a>
      <a href="https://www.linkedin.com/in/mohammad-mahdi-mohammadi-864822385" target="_blank" class="btn btn-ghost">
        💼 LinkedIn
      </a>
    </div>

  </div>

  <div class="scroll-hint">
    <span>scroll</span>
    <div class="scroll-bar"></div>
  </div>
</div>

<!-- ══ STATS ══ -->
<section class="reveal">
  <div class="section-label">// overview</div>
  <h2 class="section-title">By the <span>Numbers</span></h2>
  <div class="divider"></div>

  <div class="stats-row">
    <div class="stat-card">
      <div class="stat-num">13+</div>
      <div class="stat-label">GitHub Projects</div>
    </div>
    <div class="stat-card">
      <div class="stat-num">2+</div>
      <div class="stat-label">Languages</div>
    </div>
    <div class="stat-card">
      <div class="stat-num">∞</div>
      <div class="stat-label">Python Libraries</div>
    </div>
    <div class="stat-card">
      <div class="stat-num">100%</div>
      <div class="stat-label">Passion</div>
    </div>
  </div>
</section>

<!-- ══ SKILLS ══ -->
<section class="reveal">
  <div class="section-label">// tech stack</div>
  <h2 class="section-title">Skills &amp; <span>Technologies</span></h2>
  <div class="divider"></div>

  <div class="skills-grid">

    <div class="skill-group">
      <div class="skill-group-title">
        <div class="skill-icon" style="background:rgba(0,212,255,0.1)">🐍</div>
        Core Language
      </div>
      <div class="skill-tags">
        <span class="tag tag-blue">Python</span>
        <span class="tag tag-blue">OOP</span>
        <span class="tag tag-blue">Algorithms</span>
        <span class="tag tag-blue">Clean Code</span>
      </div>
    </div>

    <div class="skill-group">
      <div class="skill-group-title">
        <div class="skill-icon" style="background:rgba(124,58,237,0.1)">⚙️</div>
        Backend Frameworks
      </div>
      <div class="skill-tags">
        <span class="tag tag-purple">Django</span>
        <span class="tag tag-purple">Flask</span>
        <span class="tag tag-purple">FastAPI</span>
        <span class="tag tag-purple">REST API</span>
      </div>
    </div>

    <div class="skill-group">
      <div class="skill-group-title">
        <div class="skill-icon" style="background:rgba(244,63,142,0.1)">🗄️</div>
        Databases &amp; ORM
      </div>
      <div class="skill-tags">
        <span class="tag tag-pink">SQLAlchemy</span>
        <span class="tag tag-pink">PostgreSQL</span>
        <span class="tag tag-pink">SQLite</span>
        <span class="tag tag-pink">ORM</span>
      </div>
    </div>

    <div class="skill-group">
      <div class="skill-group-title">
        <div class="skill-icon" style="background:rgba(16,185,129,0.1)">📦</div>
        Python Libraries
      </div>
      <div class="skill-tags">
        <span class="tag tag-green">NumPy</span>
        <span class="tag tag-green">Pandas</span>
        <span class="tag tag-green">Requests</span>
        <span class="tag tag-green">Tkinter</span>
        <span class="tag tag-green">Pygame</span>
        <span class="tag tag-green">Pillow</span>
      </div>
    </div>

    <div class="skill-group">
      <div class="skill-group-title">
        <div class="skill-icon" style="background:rgba(0,212,255,0.1)">🌐</div>
        Web &amp; Runtime
      </div>
      <div class="skill-tags">
        <span class="tag tag-blue">Node.js</span>
        <span class="tag tag-blue">JavaScript</span>
        <span class="tag tag-blue">HTML/CSS</span>
        <span class="tag tag-blue">Jinja2</span>
      </div>
    </div>

    <div class="skill-group">
      <div class="skill-group-title">
        <div class="skill-icon" style="background:rgba(124,58,237,0.1)">🛠️</div>
        Tools &amp; DevOps
      </div>
      <div class="skill-tags">
        <span class="tag tag-purple">Git</span>
        <span class="tag tag-purple">GitHub</span>
        <span class="tag tag-purple">VS Code</span>
        <span class="tag tag-purple">Linux</span>
      </div>
    </div>

  </div>
</section>

<!-- ══ PROJECTS ══ -->
<section class="reveal">
  <div class="section-label">// portfolio</div>
  <h2 class="section-title">Featured <span>Projects</span></h2>
  <div class="divider"></div>

  <div class="projects-grid">

    <div class="project-card">
      <div class="project-header">
        <span class="project-emoji">🏥</span>
        <span class="project-arrow">↗</span>
      </div>
      <div class="project-name">Medical Diagnosis AI</div>
      <div class="project-desc">Intelligent symptom-based diagnostic system powered by Python logic and medical datasets.</div>
      <div class="skill-tags" style="margin-top:1rem">
        <span class="tag tag-blue">Python</span>
        <span class="tag tag-purple">AI/ML</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-header">
        <span class="project-emoji">🔐</span>
        <span class="project-arrow">↗</span>
      </div>
      <div class="project-name">Password Generator</div>
      <div class="project-desc">Cryptographically secure password generation with custom rules, entropy scoring, and export.</div>
      <div class="skill-tags" style="margin-top:1rem">
        <span class="tag tag-blue">Python</span>
        <span class="tag tag-green">Security</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-header">
        <span class="project-emoji">🗂️</span>
        <span class="project-arrow">↗</span>
      </div>
      <div class="project-name">File Organizer</div>
      <div class="project-desc">Automated file management system that sorts, renames, and archives by type, date, and rules.</div>
      <div class="skill-tags" style="margin-top:1rem">
        <span class="tag tag-blue">Python</span>
        <span class="tag tag-purple">Automation</span>
      </div>
    </div>

    <div class="project-card">
      <div class="project-header">
        <span class="project-emoji">🧮</span>
        <span class="project-arrow">↗</span>
      </div>
      <div class="project-name">Smart Calculator</div>
      <div class="project-desc">Feature-rich calculator with history, expression parsing, and a clean GUI interface.</div>
      <div class="skill-tags" style="margin-top:1rem">
        <span class="tag tag-blue">Python</span>
        <span class="tag tag-green">Tkinter</span>
      </div>
    </div>

    <div class="project-card" style="border-style: dashed; opacity: 0.5;">
      <div class="project-header">
        <span class="project-emoji">🚀</span>
      </div>
      <div class="project-name" style="color: var(--muted)">Next Project</div>
      <div class="project-desc">Building something new — stay tuned.</div>
      <div class="skill-tags" style="margin-top:1rem">
        <span class="tag tag-purple">Coming Soon</span>
      </div>
    </div>

  </div>
</section>

<!-- ══ CONTACT ══ -->
<section class="reveal">
  <div class="section-label">// connect</div>
  <h2 class="section-title">Get in <span>Touch</span></h2>
  <div class="divider"></div>

  <div class="contact-grid">

    <a href="https://github.com/bluelifemmd2007-cell" target="_blank" class="contact-card">
      <div class="contact-icon" style="background:rgba(255,255,255,0.06)">
        <svg width="18" height="18" fill="white" viewBox="0 0 24 24"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
      </div>
      <div class="contact-info">
        <div class="label">GITHUB</div>
        <div class="value">bluelifemmd2007-cell</div>
      </div>
    </a>

    <a href="https://bluelifemmd2007-cell.github.io/-mmd-web-profile/" target="_blank" class="contact-card">
      <div class="contact-icon" style="background:rgba(0,212,255,0.1)">🌐</div>
      <div class="contact-info">
        <div class="label">PORTFOLIO</div>
        <div class="value">mmd-web-profile</div>
      </div>
    </a>

    <a href="https://www.linkedin.com/in/mohammad-mahdi-mohammadi-864822385" target="_blank" class="contact-card">
      <div class="contact-icon" style="background:rgba(10,102,194,0.15)">💼</div>
      <div class="contact-info">
        <div class="label">LINKEDIN</div>
        <div class="value">Mohammad Mahdi</div>
      </div>
    </a>

    <a href="https://www.instagram.com/mmd_m2007" target="_blank" class="contact-card">
      <div class="contact-icon" style="background:rgba(244,63,142,0.1)">📸</div>
      <div class="contact-info">
        <div class="label">INSTAGRAM</div>
        <div class="value">@mmd_m2007</div>
      </div>
    </a>

    <a href="https://t.me/MMD_MM10" target="_blank" class="contact-card">
      <div class="contact-icon" style="background:rgba(0,136,204,0.1)">✈️</div>
      <div class="contact-info">
        <div class="label">TELEGRAM</div>
        <div class="value">@MMD_MM10</div>
      </div>
    </a>

  </div>
</section>

<!-- ══ FOOTER ══ -->
<footer>
  <span>Mohammad Mahdi Mohammadi</span> — Built with passion &amp; Python
</footer>

<!-- ══ SCRIPTS ══ -->
<script>
// ── PARTICLE NETWORK ──
const canvas = document.getElementById('canvas');
const ctx = canvas.getContext('2d');
let W, H, particles, mouse = { x: -9999, y: -9999 };

function resize() {
  W = canvas.width = window.innerWidth;
  H = canvas.height = window.innerHeight;
  init();
}

function init() {
  const count = Math.floor((W * H) / 12000);
  particles = Array.from({ length: count }, () => ({
    x: Math.random() * W,
    y: Math.random() * H,
    vx: (Math.random() - 0.5) * 0.4,
    vy: (Math.random() - 0.5) * 0.4,
    r: Math.random() * 1.5 + 0.5
  }));
}

function draw() {
  ctx.clearRect(0, 0, W, H);

  particles.forEach(p => {
    p.x += p.vx;
    p.y += p.vy;
    if (p.x < 0 || p.x > W) p.vx *= -1;
    if (p.y < 0 || p.y > H) p.vy *= -1;

    ctx.beginPath();
    ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
    ctx.fillStyle = 'rgba(0,212,255,0.6)';
    ctx.fill();
  });

  for (let i = 0; i < particles.length; i++) {
    for (let j = i + 1; j < particles.length; j++) {
      const dx = particles[i].x - particles[j].x;
      const dy = particles[i].y - particles[j].y;
      const dist = Math.sqrt(dx * dx + dy * dy);
      if (dist < 120) {
        ctx.beginPath();
        ctx.moveTo(particles[i].x, particles[i].y);
        ctx.lineTo(particles[j].x, particles[j].y);
        ctx.strokeStyle = `rgba(0,212,255,${(1 - dist / 120) * 0.3})`;
        ctx.lineWidth = 0.5;
        ctx.stroke();
      }
    }

    const dx = particles[i].x - mouse.x;
    const dy = particles[i].y - mouse.y;
    const md = Math.sqrt(dx * dx + dy * dy);
    if (md < 150) {
      ctx.beginPath();
      ctx.moveTo(particles[i].x, particles[i].y);
      ctx.lineTo(mouse.x, mouse.y);
      ctx.strokeStyle = `rgba(124,58,237,${(1 - md / 150) * 0.5})`;
      ctx.lineWidth = 0.8;
      ctx.stroke();
    }
  }

  requestAnimationFrame(draw);
}

window.addEventListener('resize', resize);
window.addEventListener('mousemove', e => { mouse.x = e.clientX; mouse.y = e.clientY; });
window.addEventListener('mouseleave', () => { mouse.x = -9999; mouse.y = -9999; });
resize();
draw();

// ── TYPEWRITER ──
const roles = [
  'Backend Developer',
  'Python Specialist',
  'Problem Solver',
  'API Architect',
  'Automation Engineer'
];
let ri = 0, ci = 0, deleting = false;
const tw = document.getElementById('typewriter');

function typeLoop() {
  const current = roles[ri];
  if (!deleting) {
    tw.textContent = current.slice(0, ci + 1);
    ci++;
    if (ci === current.length) { deleting = true; setTimeout(typeLoop, 1800); return; }
    setTimeout(typeLoop, 80);
  } else {
    tw.textContent = current.slice(0, ci - 1);
    ci--;
    if (ci === 0) { deleting = false; ri = (ri + 1) % roles.length; setTimeout(typeLoop, 400); return; }
    setTimeout(typeLoop, 45);
  }
}
typeLoop();

// ── SCROLL REVEAL ──
const revealEls = document.querySelectorAll('.reveal');
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) { e.target.classList.add('visible'); observer.unobserve(e.target); }
  });
}, { threshold: 0.1 });
revealEls.forEach(el => observer.observe(el));
</script>
</body>
</html>
