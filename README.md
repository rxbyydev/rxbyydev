<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>GitHub Profile</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;700;800&display=swap" rel="stylesheet">
<style>
  /* =============================================
     🔧 EASY CONFIG — change stuff here!
  ============================================= */
  :root {
    --name:        "YourName";          /* displayed in header */
    --accent:      #00ff88;             /* main glow color */
    --accent2:     #00c8ff;             /* secondary accent */
    --bg:          #060810;             /* background */
    --surface:     #0d1117;             /* card bg */
    --border:      #1e2a3a;             /* card border */
    --text:        #e6edf3;             /* main text */
    --muted:       #7d8590;             /* muted text */
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Space Mono', monospace;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* --- grid noise bg --- */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(0,255,136,.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,255,136,.03) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
    z-index: 0;
  }

  .page { position: relative; z-index: 1; max-width: 960px; margin: 0 auto; padding: 60px 24px; }

  /* ---- HEADER ---- */
  .header {
    display: flex;
    align-items: flex-start;
    gap: 40px;
    margin-bottom: 60px;
    animation: fadeUp .6s ease both;
  }

  .avatar-wrap {
    position: relative;
    flex-shrink: 0;
  }
  .avatar-wrap::before {
    content: '';
    position: absolute;
    inset: -4px;
    border-radius: 50%;
    background: conic-gradient(var(--accent), var(--accent2), var(--accent));
    animation: spin 4s linear infinite;
  }
  .avatar-wrap::after {
    content: '';
    position: absolute;
    inset: -12px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(0,255,136,.15), transparent 70%);
    animation: pulse 2s ease-in-out infinite;
  }
  .avatar {
    width: 110px; height: 110px;
    border-radius: 50%;
    border: 3px solid var(--bg);
    position: relative;
    z-index: 1;
    background: var(--surface);
    display: flex; align-items: center; justify-content: center;
    font-size: 48px;
    overflow: hidden;
  }
  /* If you have a real avatar image, uncomment + set src in HTML below */
  /* .avatar img { width:100%; height:100%; object-fit:cover; } */

  .header-text { padding-top: 8px; }
  .greeting {
    font-size: 13px;
    color: var(--accent);
    letter-spacing: .2em;
    text-transform: uppercase;
    margin-bottom: 6px;
    opacity: 0;
    animation: fadeUp .5s .1s ease forwards;
  }
  .name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2rem, 5vw, 3.2rem);
    font-weight: 800;
    line-height: 1;
    margin-bottom: 12px;
    opacity: 0;
    animation: fadeUp .5s .2s ease forwards;
  }
  .name span { color: var(--accent); }

  .role {
    font-size: 14px;
    color: var(--muted);
    margin-bottom: 18px;
    opacity: 0;
    animation: fadeUp .5s .3s ease forwards;
  }
  .role b { color: var(--accent2); }

  .badges {
    display: flex; flex-wrap: wrap; gap: 8px;
    opacity: 0;
    animation: fadeUp .5s .4s ease forwards;
  }
  .badge {
    font-size: 11px;
    padding: 4px 12px;
    border-radius: 99px;
    border: 1px solid var(--border);
    color: var(--muted);
    background: var(--surface);
    letter-spacing: .05em;
  }
  .badge.hot {
    border-color: var(--accent);
    color: var(--accent);
    background: rgba(0,255,136,.07);
  }

  /* ---- SECTION TITLE ---- */
  .section-label {
    font-size: 11px;
    letter-spacing: .25em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 16px;
    display: flex; align-items: center; gap: 10px;
  }
  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(to right, var(--border), transparent);
  }

  /* ---- ABOUT ---- */
  .about-block {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 28px;
    margin-bottom: 40px;
    position: relative;
    overflow: hidden;
    opacity: 0;
    animation: fadeUp .5s .5s ease forwards;
  }
  .about-block::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(to right, var(--accent), var(--accent2), transparent);
  }
  .about-text {
    font-size: 14px;
    line-height: 1.8;
    color: var(--text);
  }
  .about-text .hi { color: var(--accent); font-weight: 700; }
  .terminal-cursor {
    display: inline-block;
    width: 9px; height: 15px;
    background: var(--accent);
    vertical-align: text-bottom;
    animation: blink 1s step-end infinite;
    margin-left: 2px;
  }

  /* ---- SKILLS GRID ---- */
  .skills-section { margin-bottom: 40px; opacity: 0; animation: fadeUp .5s .6s ease forwards; }
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
    gap: 10px;
  }
  .skill-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 14px 16px;
    display: flex; align-items: center; gap: 10px;
    transition: border-color .2s, transform .2s, box-shadow .2s;
    cursor: default;
  }
  .skill-card:hover {
    border-color: var(--accent);
    transform: translateY(-3px);
    box-shadow: 0 8px 24px rgba(0,255,136,.1);
  }
  .skill-icon { font-size: 20px; }
  .skill-name { font-size: 12px; color: var(--text); }

  /* ---- STATS ROW ---- */
  .stats-row {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 12px;
    margin-bottom: 40px;
    opacity: 0;
    animation: fadeUp .5s .7s ease forwards;
  }
  .stat-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 20px;
    text-align: center;
    transition: border-color .2s;
  }
  .stat-card:hover { border-color: var(--accent2); }
  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 2rem;
    font-weight: 800;
    color: var(--accent);
    display: block;
    margin-bottom: 4px;
  }
  .stat-label { font-size: 11px; color: var(--muted); letter-spacing: .1em; }

  /* ---- PROJECTS ---- */
  .projects-section { margin-bottom: 40px; opacity: 0; animation: fadeUp .5s .8s ease forwards; }
  .projects-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
  @media(max-width:600px) { .projects-grid { grid-template-columns: 1fr; } }

  .project-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 22px;
    position: relative;
    overflow: hidden;
    transition: border-color .2s, transform .2s;
    text-decoration: none;
    display: block;
    color: inherit;
  }
  .project-card:hover {
    border-color: var(--accent);
    transform: translateY(-4px);
    box-shadow: 0 12px 32px rgba(0,255,136,.08);
  }
  .project-card::after {
    content: '↗';
    position: absolute;
    top: 16px; right: 18px;
    font-size: 18px;
    color: var(--border);
    transition: color .2s, transform .2s;
  }
  .project-card:hover::after { color: var(--accent); transform: translate(2px,-2px); }

  .project-name {
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 15px;
    margin-bottom: 6px;
    color: var(--text);
  }
  .project-desc { font-size: 12px; color: var(--muted); line-height: 1.6; margin-bottom: 14px; }
  .project-tags { display: flex; flex-wrap: wrap; gap: 6px; }
  .tag {
    font-size: 10px;
    padding: 3px 9px;
    background: rgba(0,200,255,.07);
    border: 1px solid rgba(0,200,255,.2);
    color: var(--accent2);
    border-radius: 99px;
  }

  /* ---- CONTACT ---- */
  .contact-section { opacity: 0; animation: fadeUp .5s .9s ease forwards; }
  .contact-links { display: flex; flex-wrap: wrap; gap: 12px; }
  .contact-link {
    display: flex; align-items: center; gap: 8px;
    padding: 10px 20px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 99px;
    text-decoration: none;
    font-size: 13px;
    color: var(--muted);
    transition: all .2s;
  }
  .contact-link:hover {
    border-color: var(--accent);
    color: var(--accent);
    box-shadow: 0 0 16px rgba(0,255,136,.15);
    transform: translateY(-2px);
  }

  /* ---- FOOTER ---- */
  .footer {
    margin-top: 60px;
    text-align: center;
    font-size: 11px;
    color: var(--border);
    letter-spacing: .1em;
  }

  /* ---- ANIMATIONS ---- */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  @keyframes spin  { to { transform: rotate(360deg); } }
  @keyframes pulse { 0%,100%{opacity:.4} 50%{opacity:.9} }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  /* ---- RESPONSIVE ---- */
  @media(max-width:600px) {
    .header { flex-direction: column; align-items: center; text-align: center; }
    .badges { justify-content: center; }
    .contact-links { justify-content: center; }
  }
</style>
</head>
<body>
<div class="page">

  <!-- ===========================
       🔧 CONFIG ZONE — edit here!
  =========================== -->

  <!-- HEADER -->
  <header class="header">
    <div class="avatar-wrap">
      <div class="avatar">
        <!-- Option A: Emoji avatar (default) -->
        🧑‍💻
        <!-- Option B: Real image — uncomment + put your image path:
        <img src="https://avatars.githubusercontent.com/u/YOUR_ID" alt="avatar">
        -->
      </div>
    </div>
    <div class="header-text">
      <div class="greeting">// Hello World</div>
      <h1 class="name">Your<span>Name</span></h1>
      <p class="role">
        Full-Stack Developer &amp; <b>Open Source Nerd</b><br>
        Building cool stuff from <b>Germany 🇩🇪</b>
      </p>
      <div class="badges">
        <span class="badge hot">🟢 Open to work</span>
        <span class="badge">React</span>
        <span class="badge">TypeScript</span>
        <span class="badge">Node.js</span>
        <span class="badge">Python</span>
        <!-- Add more badges as you like -->
      </div>
    </div>
  </header>

  <!-- ABOUT ME -->
  <div class="section-label">about_me.txt</div>
  <div class="about-block">
    <p class="about-text">
      <span class="hi">Hey, I'm YourName!</span> 👋<br><br>
      I'm a passionate developer who loves turning ideas into reality through code.
      Currently working on <b style="color:var(--accent2)">awesome projects</b> and always looking
      for the next challenge. When I'm not coding I'm probably playing games, listening to music,
      or discovering new tech stacks.<br><br>
      <span style="color:var(--muted)">→ Currently learning:</span> <span style="color:var(--accent)">Rust &amp; WebAssembly</span>
      <span class="terminal-cursor"></span>
    </p>
  </div>

  <!-- SKILLS -->
  <div class="skills-section">
    <div class="section-label">tech_stack</div>
    <div class="skills-grid">
      <!-- Add/remove skill cards freely -->
      <div class="skill-card"><span class="skill-icon">⚛️</span><span class="skill-name">React</span></div>
      <div class="skill-card"><span class="skill-icon">🟦</span><span class="skill-name">TypeScript</span></div>
      <div class="skill-card"><span class="skill-icon">🟩</span><span class="skill-name">Node.js</span></div>
      <div class="skill-card"><span class="skill-icon">🐍</span><span class="skill-name">Python</span></div>
      <div class="skill-card"><span class="skill-icon">🐳</span><span class="skill-name">Docker</span></div>
      <div class="skill-card"><span class="skill-icon">☁️</span><span class="skill-name">AWS</span></div>
      <div class="skill-card"><span class="skill-icon">🗄️</span><span class="skill-name">PostgreSQL</span></div>
      <div class="skill-card"><span class="skill-icon">⚡</span><span class="skill-name">Vite</span></div>
      <div class="skill-card"><span class="skill-icon">🐙</span><span class="skill-name">Git</span></div>
      <div class="skill-card"><span class="skill-icon">🦀</span><span class="skill-name">Rust</span></div>
    </div>
  </div>

  <!-- STATS -->
  <div class="stats-row">
    <!-- Change numbers to your real GitHub stats -->
    <div class="stat-card">
      <span class="stat-num">42</span>
      <span class="stat-label">Repositories</span>
    </div>
    <div class="stat-card">
      <span class="stat-num">1.2k</span>
      <span class="stat-label">Contributions</span>
    </div>
    <div class="stat-card">
      <span class="stat-num">128</span>
      <span class="stat-label">Stars Earned</span>
    </div>
    <div class="stat-card">
      <span class="stat-num">3</span>
      <span class="stat-label">Years Coding</span>
    </div>
  </div>

  <!-- PROJECTS -->
  <div class="projects-section">
    <div class="section-label">featured_projects</div>
    <div class="projects-grid">
      <!-- Replace href with your GitHub repo links -->
      <a class="project-card" href="https://github.com/yourusername/project-one" target="_blank">
        <div class="project-name">🚀 Project One</div>
        <div class="project-desc">A super cool open source tool that does amazing things. Built with love and caffeine.</div>
        <div class="project-tags">
          <span class="tag">TypeScript</span>
          <span class="tag">React</span>
          <span class="tag">Open Source</span>
        </div>
      </a>
      <a class="project-card" href="https://github.com/yourusername/project-two" target="_blank">
        <div class="project-name">⚡ Project Two</div>
        <div class="project-desc">Lightning fast REST API with full auth system, Docker support and clean code.</div>
        <div class="project-tags">
          <span class="tag">Node.js</span>
          <span class="tag">PostgreSQL</span>
          <span class="tag">Docker</span>
        </div>
      </a>
      <a class="project-card" href="https://github.com/yourusername/project-three" target="_blank">
        <div class="project-name">🤖 Project Three</div>
        <div class="project-desc">AI-powered CLI tool for automating boring dev tasks. 500+ downloads.</div>
        <div class="project-tags">
          <span class="tag">Python</span>
          <span class="tag">OpenAI API</span>
        </div>
      </a>
      <a class="project-card" href="https://github.com/yourusername/project-four" target="_blank">
        <div class="project-name">🎮 Project Four</div>
        <div class="project-desc">Multiplayer browser game built with WebSockets. Pure chaos. Very fun.</div>
        <div class="project-tags">
          <span class="tag">WebSockets</span>
          <span class="tag">Canvas API</span>
          <span class="tag">Phaser</span>
        </div>
      </a>
    </div>
  </div>

  <!-- CONTACT -->
  <div class="contact-section">
    <div class="section-label">find_me_at</div>
    <div class="contact-links">
      <!-- Replace # with your actual links -->
      <a class="contact-link" href="https://github.com/yourusername" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/></svg>
        GitHub
      </a>
      <a class="contact-link" href="https://twitter.com/yourusername" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/></svg>
        Twitter / X
      </a>
      <a class="contact-link" href="https://linkedin.com/in/yourusername" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
        LinkedIn
      </a>
      <a class="contact-link" href="mailto:you@example.com">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
        Email Me
      </a>
    </div>
  </div>

  <div class="footer">
    crafted with ❤️ &amp; too much coffee · © 2025 YourName
  </div>

</div>
</body>
</html>
