<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Dhavarsanam — Flutter & AI Engineer</title>
<link href="https://fonts.googleapis.com/css2?family=Rajdhani:wght@300;400;500;600;700&family=Share+Tech+Mono&family=Exo+2:wght@100;300;400;700;900&display=swap" rel="stylesheet"/>
<style>
:root {
  --cyan:    #00f7ff;
  --blue:    #0066ff;
  --violet:  #a855f7;
  --green:   #00ff88;
  --dark:    #020812;
  --dark2:   #070f1f;
  --dark3:   #0a0a2e;
  --text:    #e2e8f0;
  --muted:   #64748b;
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

html { scroll-behavior: smooth; }

body {
  background: var(--dark);
  color: var(--text);
  font-family: 'Exo 2', sans-serif;
  overflow-x: hidden;
  cursor: none;
}

/* ── CUSTOM CURSOR ── */
#cursor {
  position: fixed; width: 12px; height: 12px;
  background: var(--cyan); border-radius: 50%;
  pointer-events: none; z-index: 9999;
  transform: translate(-50%,-50%);
  transition: transform .1s, background .2s;
  mix-blend-mode: screen;
}
#cursor-ring {
  position: fixed; width: 36px; height: 36px;
  border: 1.5px solid var(--cyan); border-radius: 50%;
  pointer-events: none; z-index: 9998;
  transform: translate(-50%,-50%);
  transition: transform .18s ease, width .2s, height .2s, opacity .2s;
  opacity: .5;
}

/* ── CANVAS PARTICLES ── */
#bg-canvas {
  position: fixed; inset: 0;
  z-index: 0; pointer-events: none;
}

/* ── SCROLLBAR ── */
::-webkit-scrollbar { width: 4px; }
::-webkit-scrollbar-track { background: var(--dark2); }
::-webkit-scrollbar-thumb { background: var(--blue); border-radius: 2px; }

/* ── SECTION WRAPPER ── */
section { position: relative; z-index: 1; }

/* ══════════════════════════════════
   HERO
══════════════════════════════════ */
#hero {
  min-height: 100vh;
  display: flex; flex-direction: column;
  align-items: center; justify-content: center;
  text-align: center;
  padding: 2rem;
  background: radial-gradient(ellipse 80% 60% at 50% 40%, #0a1a3e55 0%, transparent 70%);
}

.hero-grid-lines {
  position: absolute; inset: 0; overflow: hidden; pointer-events: none;
  background-image:
    linear-gradient(rgba(0,102,255,.04) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,102,255,.04) 1px, transparent 1px);
  background-size: 60px 60px;
  animation: gridShift 20s linear infinite;
}
@keyframes gridShift {
  0%   { background-position: 0 0; }
  100% { background-position: 60px 60px; }
}

.hero-tag {
  font-family: 'Share Tech Mono', monospace;
  font-size: .78rem; letter-spacing: .18em;
  color: var(--cyan); opacity: .7;
  animation: fadeSlideDown .8s ease both;
}

.hero-name {
  font-family: 'Rajdhani', sans-serif;
  font-size: clamp(4rem, 12vw, 9rem);
  font-weight: 700;
  line-height: .95;
  letter-spacing: -.02em;
  background: linear-gradient(135deg, #fff 30%, var(--cyan) 70%, var(--blue) 100%);
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  animation: fadeSlideUp .9s .1s ease both;
  position: relative;
}

/* glitch effect */
.hero-name::before,
.hero-name::after {
  content: attr(data-text);
  position: absolute; inset: 0;
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  animation: glitch 4s infinite;
}
.hero-name::before {
  background: linear-gradient(135deg, var(--violet), var(--cyan));
  -webkit-background-clip: text;
  clip-path: polygon(0 30%, 100% 30%, 100% 50%, 0 50%);
  animation: glitch1 4s infinite;
}
.hero-name::after {
  background: linear-gradient(135deg, var(--cyan), var(--green));
  -webkit-background-clip: text;
  clip-path: polygon(0 55%, 100% 55%, 100% 75%, 0 75%);
  animation: glitch2 4s infinite;
}
@keyframes glitch1 {
  0%,92%,100% { transform: none; opacity: 0; }
  93% { transform: translateX(-3px); opacity: .6; }
  95% { transform: translateX(3px); opacity: .4; }
  97% { transform: none; opacity: 0; }
}
@keyframes glitch2 {
  0%,88%,100% { transform: none; opacity: 0; }
  89% { transform: translateX(4px); opacity: .5; }
  91% { transform: translateX(-2px); opacity: .3; }
  93% { transform: none; opacity: 0; }
}

.hero-subtitle {
  font-family: 'Share Tech Mono', monospace;
  font-size: clamp(.85rem, 2.2vw, 1.1rem);
  color: var(--cyan);
  letter-spacing: .1em;
  margin-top: .8rem;
  animation: fadeSlideUp .9s .25s ease both;
}

/* typing cursor blink */
.hero-subtitle::after {
  content: '|';
  animation: blink .8s infinite;
  margin-left: 2px;
}
@keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

.hero-badges {
  display: flex; flex-wrap: wrap; gap: .6rem;
  justify-content: center;
  margin-top: 2rem;
  animation: fadeSlideUp .9s .4s ease both;
}
.badge {
  font-family: 'Share Tech Mono', monospace;
  font-size: .72rem; letter-spacing: .12em;
  padding: .35rem .9rem;
  border: 1px solid;
  border-radius: 2px;
  position: relative; overflow: hidden;
  transition: transform .2s, box-shadow .2s;
}
.badge::before {
  content: '';
  position: absolute; inset: 0;
  background: currentColor; opacity: 0;
  transition: opacity .2s;
}
.badge:hover { transform: translateY(-2px); }
.badge:hover::before { opacity: .08; }
.badge.cyan  { color: var(--cyan);   border-color: var(--cyan);   box-shadow: 0 0 12px #00f7ff22; }
.badge.blue  { color: var(--blue);   border-color: var(--blue);   box-shadow: 0 0 12px #0066ff22; }
.badge.green { color: var(--green);  border-color: var(--green);  box-shadow: 0 0 12px #00ff8822; }
.badge.violet{ color: var(--violet); border-color: var(--violet); box-shadow: 0 0 12px #a855f722; }
.badge:hover.cyan   { box-shadow: 0 0 24px #00f7ff55; }
.badge:hover.blue   { box-shadow: 0 0 24px #0066ff55; }
.badge:hover.green  { box-shadow: 0 0 24px #00ff8855; }
.badge:hover.violet { box-shadow: 0 0 24px #a855f755; }

.scroll-hint {
  margin-top: 3.5rem;
  display: flex; flex-direction: column; align-items: center; gap: .5rem;
  animation: fadeSlideUp 1s .7s ease both;
  opacity: .45;
}
.scroll-hint span { font-family: 'Share Tech Mono', monospace; font-size: .65rem; letter-spacing: .2em; color: var(--muted); }
.scroll-arrow {
  width: 20px; height: 20px;
  border-right: 1.5px solid var(--muted);
  border-bottom: 1.5px solid var(--muted);
  transform: rotate(45deg);
  animation: scrollBounce 1.4s infinite;
}
@keyframes scrollBounce {
  0%,100%{transform:rotate(45deg) translateY(0)}
  50%{transform:rotate(45deg) translateY(5px)}
}

@keyframes fadeSlideDown {
  from{opacity:0;transform:translateY(-16px)} to{opacity:1;transform:none}
}
@keyframes fadeSlideUp {
  from{opacity:0;transform:translateY(20px)} to{opacity:1;transform:none}
}

/* ══════════════════════════════════
   SECTION COMMON
══════════════════════════════════ */
.section-inner {
  max-width: 1100px;
  margin: 0 auto;
  padding: 5rem 2rem;
}

.section-label {
  font-family: 'Share Tech Mono', monospace;
  font-size: .7rem; letter-spacing: .25em;
  color: var(--cyan); opacity: .6;
  margin-bottom: .4rem;
}

.section-title {
  font-family: 'Rajdhani', sans-serif;
  font-size: clamp(1.8rem, 5vw, 3rem);
  font-weight: 700;
  line-height: 1;
  margin-bottom: 2.5rem;
}
.section-title .accent { color: var(--cyan); }

.divider {
  width: 100%; height: 1px;
  background: linear-gradient(90deg, transparent, var(--blue)44, var(--cyan)66, var(--blue)44, transparent);
  margin: 0;
}

/* reveal on scroll */
.reveal {
  opacity: 0; transform: translateY(30px);
  transition: opacity .7s ease, transform .7s ease;
}
.reveal.visible { opacity: 1; transform: none; }

/* ══════════════════════════════════
   ABOUT / SUMMARY
══════════════════════════════════ */
#about { background: var(--dark2); }

.about-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
}
@media(max-width:700px){ .about-grid{ grid-template-columns:1fr; } }

.about-item {
  display: flex; gap: 1rem; align-items: flex-start;
  padding: 1.2rem 1.4rem;
  border: 1px solid rgba(0,102,255,.15);
  border-radius: 4px;
  background: rgba(0,102,255,.03);
  transition: border-color .3s, background .3s, transform .3s;
}
.about-item:hover {
  border-color: var(--cyan); background: rgba(0,247,255,.05);
  transform: translateX(4px);
}
.about-icon { font-size: 1.4rem; flex-shrink: 0; }
.about-item p { font-size: .92rem; color: #94a3b8; line-height: 1.6; }
.about-item p strong { color: var(--text); }

/* ══════════════════════════════════
   TECH STACK
══════════════════════════════════ */
#stack { background: var(--dark); }

.stack-groups {
  display: flex; flex-direction: column; gap: 2rem;
}
.stack-group-label {
  font-family: 'Share Tech Mono', monospace;
  font-size: .7rem; letter-spacing: .2em;
  color: var(--muted); margin-bottom: .8rem;
}
.stack-pills {
  display: flex; flex-wrap: wrap; gap: .6rem;
}
.pill {
  font-family: 'Share Tech Mono', monospace;
  font-size: .75rem; padding: .45rem 1rem;
  border-radius: 2px;
  border: 1px solid rgba(255,255,255,.08);
  background: rgba(255,255,255,.03);
  color: #94a3b8;
  transition: all .25s;
  position: relative; overflow: hidden;
}
.pill::after {
  content: '';
  position: absolute; bottom: 0; left: 0;
  width: 100%; height: 2px;
  background: var(--cyan);
  transform: scaleX(0); transform-origin: left;
  transition: transform .25s;
}
.pill:hover {
  color: var(--cyan); border-color: var(--cyan);
  background: rgba(0,247,255,.07);
  box-shadow: 0 0 16px #00f7ff22;
}
.pill:hover::after { transform: scaleX(1); }
.pill.ai:hover  { color: var(--violet); border-color: var(--violet); background: rgba(168,85,247,.07); box-shadow: 0 0 16px #a855f722; }
.pill.ai::after { background: var(--violet); }
.pill.tool:hover{ color: var(--green);  border-color: var(--green);  background: rgba(0,255,136,.07); box-shadow: 0 0 16px #00ff8822; }
.pill.tool::after{ background: var(--green); }

/* ══════════════════════════════════
   EXPERTISE CARDS
══════════════════════════════════ */
#expertise { background: var(--dark2); }

.cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1.2rem;
}
.card {
  padding: 1.8rem;
  border: 1px solid rgba(0,102,255,.12);
  border-radius: 6px;
  background: linear-gradient(135deg, rgba(7,15,31,.9), rgba(10,10,46,.6));
  position: relative; overflow: hidden;
  transition: transform .3s, box-shadow .3s, border-color .3s;
}
.card::before {
  content: '';
  position: absolute; top: 0; left: 0; right: 0;
  height: 2px;
  background: linear-gradient(90deg, transparent, var(--card-color, var(--cyan)), transparent);
  transform: scaleX(0); transition: transform .4s;
}
.card:hover { transform: translateY(-5px); border-color: var(--card-color, var(--cyan)); }
.card:hover { box-shadow: 0 12px 40px -8px color-mix(in srgb, var(--card-color, var(--cyan)) 30%, transparent); }
.card:hover::before { transform: scaleX(1); }
.card-icon { font-size: 1.8rem; margin-bottom: 1rem; display: block; }
.card-title {
  font-family: 'Rajdhani', sans-serif;
  font-size: 1.05rem; font-weight: 600;
  color: var(--card-color, var(--cyan));
  margin-bottom: .6rem;
}
.card-desc { font-size: .85rem; color: #64748b; line-height: 1.7; }
.card-desc strong { color: #94a3b8; }

/* ══════════════════════════════════
   AI SECTION
══════════════════════════════════ */
#ai {
  background: var(--dark);
  position: relative; overflow: hidden;
}
#ai::before {
  content: '';
  position: absolute; top: -60%; left: -20%;
  width: 140%; height: 140%;
  background: radial-gradient(ellipse 60% 50% at 50% 50%, rgba(168,85,247,.06) 0%, transparent 60%);
  pointer-events: none;
  animation: aiGlow 6s ease-in-out infinite alternate;
}
@keyframes aiGlow {
  from { transform: scale(1); opacity: .7; }
  to   { transform: scale(1.15); opacity: 1; }
}

.ai-banner {
  text-align: center; margin-bottom: 3rem;
}
.ai-banner-tag {
  font-family: 'Share Tech Mono', monospace;
  font-size: .75rem; letter-spacing: .22em;
  color: var(--violet); margin-bottom: .6rem;
}
.ai-banner h2 {
  font-family: 'Rajdhani', sans-serif;
  font-size: clamp(1.6rem,4vw,2.6rem); font-weight: 700;
  background: linear-gradient(135deg, var(--violet), var(--cyan));
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
}
.ai-banner p { font-size: .9rem; color: var(--muted); margin-top: .5rem; font-style: italic; }

.ai-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 1.2rem;
}
.ai-card {
  padding: 1.6rem;
  border: 1px solid rgba(168,85,247,.15);
  border-radius: 6px;
  background: rgba(168,85,247,.03);
  transition: transform .3s, border-color .3s, box-shadow .3s;
  position: relative; overflow: hidden;
}
.ai-card::after {
  content: '';
  position: absolute; bottom: 0; left: 0;
  width: 100%; height: 1px;
  background: linear-gradient(90deg, transparent, var(--violet), transparent);
  transform: scaleX(0); transition: transform .4s;
}
.ai-card:hover {
  transform: translateY(-4px);
  border-color: var(--violet);
  box-shadow: 0 8px 32px -8px rgba(168,85,247,.35);
}
.ai-card:hover::after { transform: scaleX(1); }
.ai-card-icon { font-size: 2rem; margin-bottom: .8rem; }
.ai-card-title {
  font-family: 'Rajdhani', sans-serif;
  font-size: 1rem; font-weight: 600;
  color: var(--violet); margin-bottom: .5rem;
}
.ai-card-desc { font-size: .83rem; color: #64748b; line-height: 1.7; }
.ai-card-desc strong { color: #94a3b8; }

.ai-toolkit {
  margin-top: 2.5rem; text-align: center;
}
.ai-toolkit-label {
  font-family: 'Share Tech Mono', monospace;
  font-size: .68rem; letter-spacing: .2em; color: var(--muted); margin-bottom: 1rem;
}
.ai-pills {
  display: flex; flex-wrap: wrap; gap: .6rem; justify-content: center;
}
.ai-pill {
  font-family: 'Share Tech Mono', monospace;
  font-size: .72rem; padding: .4rem .95rem;
  border: 1px solid rgba(168,85,247,.3);
  border-radius: 2px;
  background: rgba(168,85,247,.05);
  color: var(--violet);
  transition: all .25s;
}
.ai-pill:hover {
  background: rgba(168,85,247,.15);
  box-shadow: 0 0 14px rgba(168,85,247,.3);
  transform: translateY(-2px);
}

/* ══════════════════════════════════
   ACHIEVEMENTS
══════════════════════════════════ */
#achievements { background: var(--dark2); }

.ach-list { display: flex; flex-direction: column; gap: .8rem; }
.ach-item {
  display: flex; align-items: center; gap: 1.2rem;
  padding: 1rem 1.4rem;
  border: 1px solid rgba(0,247,255,.08);
  border-radius: 4px;
  background: rgba(0,247,255,.02);
  transition: all .25s;
  position: relative; overflow: hidden;
}
.ach-item::before {
  content: '';
  position: absolute; left: 0; top: 0; bottom: 0;
  width: 3px;
  background: var(--ach-color, var(--cyan));
  transform: scaleY(0); transform-origin: bottom;
  transition: transform .35s ease;
}
.ach-item:hover {
  border-color: var(--ach-color, var(--cyan));
  background: rgba(0,247,255,.04);
  transform: translateX(6px);
}
.ach-item:hover::before { transform: scaleY(1); }
.ach-num {
  font-family: 'Share Tech Mono', monospace;
  font-size: .7rem; color: var(--muted);
  flex-shrink: 0; width: 24px;
}
.ach-emoji { font-size: 1.2rem; flex-shrink: 0; }
.ach-text { font-size: .9rem; color: #94a3b8; }
.ach-text strong { color: var(--text); }

/* ══════════════════════════════════
   FOOTER
══════════════════════════════════ */
footer {
  position: relative; z-index: 1;
  text-align: center;
  padding: 3rem 2rem;
  background: var(--dark);
  border-top: 1px solid rgba(0,102,255,.12);
}
.footer-name {
  font-family: 'Rajdhani', sans-serif;
  font-size: 2.4rem; font-weight: 700;
  background: linear-gradient(135deg, var(--cyan), var(--blue));
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  margin-bottom: .3rem;
}
.footer-sub {
  font-family: 'Share Tech Mono', monospace;
  font-size: .72rem; letter-spacing: .2em;
  color: var(--muted);
}
.footer-line {
  width: 120px; height: 1px;
  background: linear-gradient(90deg, transparent, var(--cyan), transparent);
  margin: 1.5rem auto;
  animation: linePulse 2.5s ease-in-out infinite;
}
@keyframes linePulse {
  0%,100%{opacity:.3;width:80px} 50%{opacity:1;width:160px}
}
.footer-copy {
  font-size: .72rem; color: #334155;
  font-family: 'Share Tech Mono', monospace;
}

/* ── SCAN LINE OVERLAY ── */
.scanlines {
  position: fixed; inset: 0; pointer-events: none; z-index: 9990;
  background: repeating-linear-gradient(
    0deg, transparent, transparent 2px,
    rgba(0,0,0,.03) 2px, rgba(0,0,0,.03) 4px
  );
  animation: scanMove 8s linear infinite;
}
@keyframes scanMove {
  from { background-position: 0 0; }
  to   { background-position: 0 100px; }
}
</style>
</head>
<body>

<!-- Overlays -->
<div class="scanlines"></div>
<div id="cursor"></div>
<div id="cursor-ring"></div>
<canvas id="bg-canvas"></canvas>

<!-- ═══ HERO ═══ -->
<section id="hero">
  <div class="hero-grid-lines"></div>
  <p class="hero-tag">// FLUTTER DEVELOPER · AI ENGINEER · MOBILE ARCHITECT</p>
  <h1 class="hero-name" data-text="DHAVARSANAM">DHAVARSANAM</h1>
  <p class="hero-subtitle" id="typed-subtitle"></p>
  <div class="hero-badges">
    <span class="badge cyan">Flutter Expert</span>
    <span class="badge blue">Dart Specialist</span>
    <span class="badge violet">Gen AI Integrator</span>
    <span class="badge green">Open to Work</span>
    <span class="badge cyan">Firebase Advanced</span>
    <span class="badge violet">LLM Engineer</span>
    <span class="badge blue">Clean Architecture</span>
    <span class="badge green">On-Device ML</span>
  </div>
  <div class="scroll-hint">
    <span>SCROLL</span>
    <div class="scroll-arrow"></div>
  </div>
</section>

<div class="divider"></div>

<!-- ═══ ABOUT ═══ -->
<section id="about">
  <div class="section-inner">
    <p class="section-label reveal">// 01 — ABOUT</p>
    <h2 class="section-title reveal">Professional <span class="accent">Summary</span></h2>
    <div class="about-grid">
      <div class="about-item reveal"><span class="about-icon">📱</span><p>Building <strong>production-ready Flutter apps</strong> with pixel-perfect UIs for iOS & Android</p></div>
      <div class="about-item reveal"><span class="about-icon">🤖</span><p>Integrating <strong>Generative AI & LLMs</strong> (Gemini, GPT-4, Claude) into mobile applications</p></div>
      <div class="about-item reveal"><span class="about-icon">⚡</span><p>Deep expertise in <strong>Dart, Firebase & REST API</strong> integration and architecture</p></div>
      <div class="about-item reveal"><span class="about-icon">🏗</span><p>Passionate about <strong>Clean Architecture & scalable design patterns</strong> (BLoC, Riverpod, MVVM)</p></div>
      <div class="about-item reveal"><span class="about-icon">🧠</span><p>Hands-on with <strong>On-Device ML, TFLite & AI-powered UX</strong> for offline intelligence</p></div>
      <div class="about-item reveal"><span class="about-icon">🚀</span><p>Focused on <strong>60fps performance</strong>, cold start optimization & maintainable codebases</p></div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ═══ STACK ═══ -->
<section id="stack">
  <div class="section-inner">
    <p class="section-label reveal">// 02 — TECHNOLOGY</p>
    <h2 class="section-title reveal">Tech <span class="accent">Stack</span></h2>
    <div class="stack-groups reveal">
      <div>
        <p class="stack-group-label">MOBILE CORE</p>
        <div class="stack-pills">
          <span class="pill">Flutter</span><span class="pill">Dart</span>
          <span class="pill">iOS</span><span class="pill">Android</span>
          <span class="pill">BLoC</span><span class="pill">Riverpod</span>
          <span class="pill">MVVM</span><span class="pill">Clean Architecture</span>
        </div>
      </div>
      <div>
        <p class="stack-group-label">AI / MACHINE LEARNING</p>
        <div class="stack-pills">
          <span class="pill ai">Gemini API</span><span class="pill ai">OpenAI GPT-4</span>
          <span class="pill ai">Claude API</span><span class="pill ai">TFLite</span>
          <span class="pill ai">MediaPipe</span><span class="pill ai">LangChain</span>
          <span class="pill ai">Vertex AI</span><span class="pill ai">Firebase ML</span>
          <span class="pill ai">RAG Pipelines</span><span class="pill ai">Embeddings</span>
        </div>
      </div>
      <div>
        <p class="stack-group-label">BACKEND & CLOUD</p>
        <div class="stack-pills">
          <span class="pill">Firebase Auth</span><span class="pill">Firestore</span>
          <span class="pill">Cloud Functions</span><span class="pill">REST APIs</span>
          <span class="pill">GCP</span><span class="pill">Push Notifications</span>
        </div>
      </div>
      <div>
        <p class="stack-group-label">DEV TOOLS</p>
        <div class="stack-pills">
          <span class="pill tool">Git</span><span class="pill tool">GitHub</span>
          <span class="pill tool">VS Code</span><span class="pill tool">Android Studio</span>
          <span class="pill tool">Postman</span><span class="pill tool">Figma</span>
          <span class="pill tool">CI/CD</span><span class="pill tool">App Store Connect</span>
          <span class="pill tool">Play Console</span>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ═══ EXPERTISE CARDS ═══ -->
<section id="expertise">
  <div class="section-inner">
    <p class="section-label reveal">// 03 — EXPERTISE</p>
    <h2 class="section-title reveal">Core <span class="accent">Expertise</span></h2>
    <div class="cards-grid">
      <div class="card reveal" style="--card-color:#00f7ff">
        <span class="card-icon">📱</span>
        <p class="card-title">Cross-Platform Development</p>
        <p class="card-desc">Pixel-perfect apps for <strong>iOS & Android</strong> from a single codebase with native performance via Flutter's Skia/Impeller rendering.</p>
      </div>
      <div class="card reveal" style="--card-color:#ff6b35">
        <span class="card-icon">🔥</span>
        <p class="card-title">Firebase Integration</p>
        <p class="card-desc">Expert in <strong>Auth, Firestore, Cloud Functions</strong>, push notifications, real-time sync & Firebase Performance Monitoring.</p>
      </div>
      <div class="card reveal" style="--card-color:#00ff88">
        <span class="card-icon">🏗</span>
        <p class="card-title">Clean Architecture</p>
        <p class="card-desc">Scalable, testable architectures using <strong>BLoC, Riverpod, MVVM</strong> — built for long-term team collaboration.</p>
      </div>
      <div class="card reveal" style="--card-color:#ffa000">
        <span class="card-icon">⚡</span>
        <p class="card-title">Performance Optimization</p>
        <p class="card-desc">Consistent <strong>60fps rendering</strong>, reduced cold start times, efficient widget trees & memory leak prevention.</p>
      </div>
      <div class="card reveal" style="--card-color:#00c8d4">
        <span class="card-icon">🌐</span>
        <p class="card-title">REST API Integration</p>
        <p class="card-desc">Robust API layers with <strong>error handling, caching, interceptors</strong> & offline-first architectural patterns.</p>
      </div>
      <div class="card reveal" style="--card-color:#0066ff">
        <span class="card-icon">🚀</span>
        <p class="card-title">Deployment & Releases</p>
        <p class="card-desc">End-to-end <strong>App Store & Play Store</strong> releases, CI/CD setup, semantic versioning & staged rollout management.</p>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ═══ GEN AI SECTION ═══ -->
<section id="ai">
  <div class="section-inner">
    <div class="ai-banner reveal">
      <p class="ai-banner-tag">// 04 — GENERATIVE AI</p>
      <h2>Generative AI & LLM Integration</h2>
      <p>Bridging cutting-edge AI capabilities with production-grade Flutter applications</p>
    </div>
    <div class="ai-grid">
      <div class="ai-card reveal">
        <div class="ai-card-icon">🧠</div>
        <p class="ai-card-title">LLM Integration</p>
        <p class="ai-card-desc">Integrating <strong>Gemini, GPT-4, Claude</strong> APIs for conversational features, smart search & AI-driven UX flows inside mobile apps.</p>
      </div>
      <div class="ai-card reveal">
        <div class="ai-card-icon">📷</div>
        <p class="ai-card-title">Multimodal AI</p>
        <p class="ai-card-desc"><strong>Vision-language</strong> features using Gemini Vision & OpenAI Vision — image understanding, OCR, scene analysis in mobile.</p>
      </div>
      <div class="ai-card reveal">
        <div class="ai-card-icon">📲</div>
        <p class="ai-card-title">On-Device ML</p>
        <p class="ai-card-desc"><strong>TFLite & MediaPipe</strong> models deployed directly on device — real-time inference, zero latency, full offline support.</p>
      </div>
      <div class="ai-card reveal">
        <div class="ai-card-icon">✍️</div>
        <p class="ai-card-title">AI-Powered Features</p>
        <p class="ai-card-desc">Smart <strong>writing assistants, auto-summarization, semantic search</strong> & intelligent recommendations inside Flutter.</p>
      </div>
      <div class="ai-card reveal">
        <div class="ai-card-icon">🔗</div>
        <p class="ai-card-title">RAG & Embeddings</p>
        <p class="ai-card-desc"><strong>RAG pipelines</strong>, vector embeddings & context-aware AI responses for knowledge-base mobile applications.</p>
      </div>
      <div class="ai-card reveal">
        <div class="ai-card-icon">🛡</div>
        <p class="ai-card-title">Responsible AI</p>
        <p class="ai-card-desc"><strong>Prompt engineering</strong>, safety filters, content moderation & user-trust-first AI design principles in every integration.</p>
      </div>
    </div>
    <div class="ai-toolkit reveal">
      <p class="ai-toolkit-label">AI / ML TOOLKIT</p>
      <div class="ai-pills">
        <span class="ai-pill">Google Gemini</span>
        <span class="ai-pill">OpenAI GPT-4</span>
        <span class="ai-pill">Anthropic Claude</span>
        <span class="ai-pill">TFLite</span>
        <span class="ai-pill">MediaPipe</span>
        <span class="ai-pill">LangChain</span>
        <span class="ai-pill">Firebase ML</span>
        <span class="ai-pill">Vertex AI</span>
        <span class="ai-pill">RAG Pipelines</span>
        <span class="ai-pill">Embeddings</span>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ═══ ACHIEVEMENTS ═══ -->
<section id="achievements">
  <div class="section-inner">
    <p class="section-label reveal">// 05 — ACHIEVEMENTS</p>
    <h2 class="section-title reveal">Professional <span class="accent">Achievements</span></h2>
    <div class="ach-list">
      <div class="ach-item reveal" style="--ach-color:#00f7ff"><span class="ach-num">01</span><span class="ach-emoji">🚀</span><p class="ach-text"><strong>Production-Ready Flutter Application Development</strong> — shipped apps on both stores</p></div>
      <div class="ach-item reveal" style="--ach-color:#ff6b35"><span class="ach-num">02</span><span class="ach-emoji">🔥</span><p class="ach-text"><strong>Advanced Firebase & REST API Integration</strong> — real-time sync & offline-first architecture</p></div>
      <div class="ach-item reveal" style="--ach-color:#00ff88"><span class="ach-num">03</span><span class="ach-emoji">🏗</span><p class="ach-text"><strong>Clean Architecture & State Management</strong> — BLoC, Riverpod, MVVM at scale</p></div>
      <div class="ach-item reveal" style="--ach-color:#ffa000"><span class="ach-num">04</span><span class="ach-emoji">⚡</span><p class="ach-text"><strong>Performance Optimization — 40% faster load times</strong> via widget tree & memory optimization</p></div>
      <div class="ach-item reveal" style="--ach-color:#a855f7"><span class="ach-num">05</span><span class="ach-emoji">🤖</span><p class="ach-text"><strong>Generative AI (Gemini / GPT-4) Integration</strong> in production Flutter applications</p></div>
      <div class="ach-item reveal" style="--ach-color:#a855f7"><span class="ach-num">06</span><span class="ach-emoji">🧠</span><p class="ach-text"><strong>On-Device ML with TFLite & MediaPipe</strong> — zero latency inference, fully offline</p></div>
      <div class="ach-item reveal" style="--ach-color:#a855f7"><span class="ach-num">07</span><span class="ach-emoji">✍️</span><p class="ach-text"><strong>AI-Powered Feature Development</strong> — Smart Search, Auto-Summarize, LLM chat features</p></div>
      <div class="ach-item reveal" style="--ach-color:#0066ff"><span class="ach-num">08</span><span class="ach-emoji">🔄</span><p class="ach-text"><strong>Git Workflow & Deployment Management</strong> — led team of 5+ with CI/CD pipelines</p></div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ═══ FOOTER ═══ -->
<footer>
  <p class="footer-name">DHAVARSANAM</p>
  <p class="footer-sub">FLUTTER DEVELOPER · AI ENGINEER · MOBILE ARCHITECT</p>
  <div class="footer-line"></div>
  <p class="footer-copy">// PASSIONATE ABOUT BUILDING IMPACTFUL MOBILE APPS POWERED BY GENERATIVE AI</p>
</footer>

<script>
/* ── CURSOR ── */
const cursor = document.getElementById('cursor');
const ring   = document.getElementById('cursor-ring');
let mx=0, my=0, rx=0, ry=0;
document.addEventListener('mousemove', e => { mx=e.clientX; my=e.clientY; });
(function animCursor(){
  rx += (mx-rx)*.18; ry += (my-ry)*.18;
  cursor.style.left = mx+'px'; cursor.style.top = my+'px';
  ring.style.left   = rx+'px'; ring.style.top  = ry+'px';
  requestAnimationFrame(animCursor);
})();
document.querySelectorAll('a,button,.card,.ai-card,.pill,.badge,.ach-item,.about-item').forEach(el=>{
  el.addEventListener('mouseenter',()=>{
    cursor.style.transform='translate(-50%,-50%) scale(2.2)';
    ring.style.width='56px'; ring.style.height='56px'; ring.style.opacity='.3';
  });
  el.addEventListener('mouseleave',()=>{
    cursor.style.transform='translate(-50%,-50%) scale(1)';
    ring.style.width='36px'; ring.style.height='36px'; ring.style.opacity='.5';
  });
});

/* ── PARTICLE CANVAS ── */
const canvas = document.getElementById('bg-canvas');
const ctx    = canvas.getContext('2d');
let W, H, particles=[], connections=[];

function resize(){ W=canvas.width=window.innerWidth; H=canvas.height=window.innerHeight; }
resize();
window.addEventListener('resize', resize);

class Particle {
  constructor(){
    this.x = Math.random()*W;
    this.y = Math.random()*H;
    this.vx= (Math.random()-.5)*.35;
    this.vy= (Math.random()-.5)*.35;
    this.r = Math.random()*1.5+.5;
    this.alpha = Math.random()*.5+.15;
    const cols=['#00f7ff','#0066ff','#a855f7','#00ff88'];
    this.color = cols[Math.floor(Math.random()*cols.length)];
  }
  update(){ 
    this.x+=this.vx; this.y+=this.vy;
    if(this.x<0||this.x>W) this.vx*=-1;
    if(this.y<0||this.y>H) this.vy*=-1;
  }
  draw(){
    ctx.beginPath();
    ctx.arc(this.x,this.y,this.r,0,Math.PI*2);
    ctx.fillStyle=this.color;
    ctx.globalAlpha=this.alpha;
    ctx.fill();
  }
}

for(let i=0;i<110;i++) particles.push(new Particle());

/* mouse repulsion */
let mouseX=W/2, mouseY=H/2;
document.addEventListener('mousemove',e=>{mouseX=e.clientX;mouseY=e.clientY;});

function drawParticles(){
  ctx.clearRect(0,0,W,H);
  /* connections */
  for(let i=0;i<particles.length;i++){
    for(let j=i+1;j<particles.length;j++){
      const dx=particles[i].x-particles[j].x;
      const dy=particles[i].y-particles[j].y;
      const dist=Math.sqrt(dx*dx+dy*dy);
      if(dist<130){
        ctx.beginPath();
        ctx.moveTo(particles[i].x,particles[i].y);
        ctx.lineTo(particles[j].x,particles[j].y);
        ctx.globalAlpha=(1-dist/130)*.09;
        ctx.strokeStyle='#00f7ff';
        ctx.lineWidth=.6;
        ctx.stroke();
      }
    }
    /* mouse proximity glow */
    const dx=particles[i].x-mouseX;
    const dy=particles[i].y-mouseY;
    const md=Math.sqrt(dx*dx+dy*dy);
    if(md<120){
      ctx.beginPath();
      ctx.arc(particles[i].x,particles[i].y,particles[i].r*2.5,0,Math.PI*2);
      ctx.fillStyle=particles[i].color;
      ctx.globalAlpha=.35*(1-md/120);
      ctx.fill();
    }
  }
  ctx.globalAlpha=1;
  particles.forEach(p=>{ p.update(); p.draw(); });
  requestAnimationFrame(drawParticles);
}
drawParticles();

/* ── TYPED SUBTITLE ── */
const lines = [
  'Flutter & Dart Expert',
  'Cross-Platform App Architect',
  'Generative AI & LLM Integrator',
  'On-Device ML Engineer',
  'Firebase & REST API Specialist',
  'Clean Architecture Practitioner',
  '60fps Performance Optimizer'
];
let li=0, ci=0, deleting=false;
const el = document.getElementById('typed-subtitle');
function type(){
  const cur = lines[li];
  if(!deleting){
    el.textContent = cur.slice(0,ci++);
    if(ci>cur.length){ deleting=true; setTimeout(type,1400); return; }
  } else {
    el.textContent = cur.slice(0,ci--);
    if(ci<0){ deleting=false; li=(li+1)%lines.length; ci=0; setTimeout(type,300); return; }
  }
  setTimeout(type, deleting?45:70);
}
type();

/* ── SCROLL REVEAL ── */
const obs = new IntersectionObserver(entries=>{
  entries.forEach((e,i)=>{
    if(e.isIntersecting){
      setTimeout(()=>e.target.classList.add('visible'), i*60);
    }
  });
},{threshold:.12});
document.querySelectorAll('.reveal').forEach(el=>obs.observe(el));
</script>
</body>
</html>
