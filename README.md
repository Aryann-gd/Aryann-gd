<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PORTFOLIO WEBSITE</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;400;600;700&display=swap');

* { margin: 0; padding: 0; box-sizing: border-box; }

:root {
  --neon-blue: #00f0ff;
  --neon-purple: #b400ff;
  --neon-pink: #ff00aa;
  --neon-green: #00ff88;
  --dark-bg: #050510;
}

html {
  scroll-behavior: smooth;
  scrollbar-width: thin;
  scrollbar-color: var(--neon-blue) #111;
}

body {
  font-family: 'Rajdhani', sans-serif;
  background: var(--dark-bg);
  color: #fff;
  overflow-x: hidden;
  min-height: 100vh;
  width: 100%;
}

canvas#particles {
  position: fixed;
  top: 0; left: 0;
  width: 100%; height: 100%;
  z-index: 0;
  pointer-events: none;
}

.cursor-glow {
  position: fixed;
  width: 300px; height: 300px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(0,240,255,0.08) 0%, transparent 70%);
  pointer-events: none;
  z-index: 1;
  transform: translate(-50%, -50%);
  transition: opacity 0.3s;
}

/* NAV */
nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  padding: 15px 30px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  backdrop-filter: blur(20px);
  background: rgba(5,5,16,0.7);
  border-bottom: 1px solid rgba(0,240,255,0.1);
}

.nav-logo {
  font-family: 'Orbitron', monospace;
  font-size: 1.4rem;
  font-weight: 900;
  background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-shadow: none;
}

.nav-links { display: flex; gap: 25px; list-style: none; }

.nav-links a {
  color: #aaa;
  text-decoration: none;
  font-size: 0.95rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
  transition: all 0.3s;
  position: relative;
}

.nav-links a:hover { color: var(--neon-blue); }
.nav-links a::after {
  content: '';
  position: absolute;
  bottom: -4px; left: 0;
  width: 0; height: 2px;
  background: var(--neon-blue);
  transition: width 0.3s;
}
.nav-links a:hover::after { width: 100%; }

/* HERO */
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  perspective: 1200px;
  overflow: hidden;
  z-index: 2;
}

.hero-grid {
  position: absolute;
  bottom: 0; left: -50%;
  width: 200%; height: 60%;
  background:
    linear-gradient(90deg, rgba(0,240,255,0.05) 1px, transparent 1px),
    linear-gradient(rgba(0,240,255,0.05) 1px, transparent 1px);
  background-size: 60px 60px;
  transform: perspective(500px) rotateX(60deg);
  transform-origin: center top;
  animation: gridScroll 10s linear infinite;
}

@keyframes gridScroll {
  0% { background-position: 0 0; }
  100% { background-position: 60px 60px; }
}

.hero-content {
  text-align: center;
  z-index: 5;
  transform-style: preserve-3d;
  animation: heroFloat 6s ease-in-out infinite;
}

@keyframes heroFloat {
  0%, 100% { transform: translateY(0) rotateX(0deg); }
  50% { transform: translateY(-15px) rotateX(2deg); }
}

.hero-badge {
  display: inline-block;
  padding: 6px 20px;
  border: 1px solid var(--neon-blue);
  border-radius: 50px;
  font-size: 0.85rem;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--neon-blue);
  margin-bottom: 20px;
  animation: pulseBorder 2s ease-in-out infinite;
}

@keyframes pulseBorder {
  0%, 100% { box-shadow: 0 0 5px rgba(0,240,255,0.3); }
  50% { box-shadow: 0 0 20px rgba(0,240,255,0.6), inset 0 0 20px rgba(0,240,255,0.1); }
}

.hero-title {
  font-family: 'Orbitron', monospace;
  font-size: clamp(2.5rem, 7vw, 5.5rem);
  font-weight: 900;
  line-height: 1.1;
  margin-bottom: 10px;
}

.hero-title .line1 { color: #fff; }
.hero-title .line2 {
  background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple), var(--neon-pink));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  filter: drop-shadow(0 0 30px rgba(0,240,255,0.3));
}

.hero-sub {
  font-size: clamp(1rem, 2.5vw, 1.4rem);
  color: #888;
  margin: 15px 0 30px;
  font-weight: 300;
}

.hero-roles {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: center;
  margin-bottom: 30px;
}

.role-chip {
  padding: 6px 16px;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 600;
  letter-spacing: 1px;
  text-transform: uppercase;
  border: 1px solid;
  background: rgba(255,255,255,0.03);
}

.role-chip:nth-child(1) { border-color: var(--neon-blue); color: var(--neon-blue); }
.role-chip:nth-child(2) { border-color: var(--neon-purple); color: var(--neon-purple); }
.role-chip:nth-child(3) { border-color: var(--neon-pink); color: var(--neon-pink); }
.role-chip:nth-child(4) { border-color: #ff4444; color: #ff4444; }
.role-chip:nth-child(5) { border-color: var(--neon-green); color: var(--neon-green); }
.role-chip:nth-child(6) { border-color: #ffaa00; color: #ffaa00; }

.cta-btn {
  display: inline-block;
  padding: 14px 40px;
  border: none;
  border-radius: 50px;
  font-family: 'Orbitron', monospace;
  font-size: 0.95rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 2px;
  cursor: pointer;
  background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
  color: #fff;
  position: relative;
  overflow: hidden;
  transition: all 0.4s;
  text-decoration: none;
}

.cta-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 40px rgba(0,240,255,0.4);
}

.cta-btn::before {
  content: '';
  position: absolute;
  top: -50%; left: -50%;
  width: 200%; height: 200%;
  background: linear-gradient(45deg, transparent, rgba(255,255,255,0.1), transparent);
  transform: rotate(45deg);
  animation: shimmer 3s infinite;
}

@keyframes shimmer {
  0% { transform: translateX(-100%) rotate(45deg); }
  100% { transform: translateX(100%) rotate(45deg); }
}

/* 3D AVATAR */
.avatar-3d {
  width: 160px; height: 160px;
  margin: 0 auto 25px;
  position: relative;
  transform-style: preserve-3d;
  animation: avatarSpin 8s ease-in-out infinite;
}

@keyframes avatarSpin {
  0%, 100% { transform: rotateY(0deg) rotateX(5deg); }
  25% { transform: rotateY(15deg) rotateX(-5deg); }
  50% { transform: rotateY(0deg) rotateX(5deg); }
  75% { transform: rotateY(-15deg) rotateX(-5deg); }
}

.avatar-face {
  width: 100%; height: 100%;
  border-radius: 50%;
  background: linear-gradient(135deg, #1a1a3e, #0a0a20);
  border: 3px solid var(--neon-blue);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 4rem;
  box-shadow: 0 0 40px rgba(0,240,255,0.3), inset 0 0 40px rgba(0,240,255,0.1);
  position: relative;
}

.avatar-ring {
  position: absolute;
  width: 130%; height: 130%;
  border: 2px solid rgba(180,0,255,0.3);
  border-radius: 50%;
  top: -15%; left: -15%;
  animation: ringPulse 3s ease-in-out infinite;
}

.avatar-ring:nth-child(2) {
  width: 160%; height: 160%;
  top: -30%; left: -30%;
  border-color: rgba(0,240,255,0.15);
  animation-delay: 1s;
}

@keyframes ringPulse {
  0%, 100% { transform: rotate(0deg) scale(1); opacity: 0.5; }
  50% { transform: rotate(180deg) scale(1.05); opacity: 1; }
}

/* SECTIONS */
section {
  position: relative;
  z-index: 2;
  padding: 80px 20px;
}

.section-title {
  font-family: 'Orbitron', monospace;
  font-size: clamp(1.8rem, 4vw, 2.8rem);
  text-align: center;
  margin-bottom: 15px;
  background: linear-gradient(135deg, #fff, var(--neon-blue));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.section-sub {
  text-align: center;
  color: #666;
  font-size: 1rem;
  margin-bottom: 50px;
  letter-spacing: 2px;
  text-transform: uppercase;
}

/* SKILLS 3D CARDS */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 25px;
  max-width: 1200px;
  margin: 0 auto;
  perspective: 1000px;
}

.skill-card {
  background: linear-gradient(145deg, rgba(15,15,40,0.9), rgba(5,5,20,0.9));
  border: 1px solid rgba(255,255,255,0.05);
  border-radius: 20px;
  padding: 35px 25px;
  text-align: center;
  transition: all 0.5s cubic-bezier(0.23, 1, 0.32, 1);
  transform-style: preserve-3d;
  position: relative;
  overflow: hidden;
  cursor: pointer;
}

.skill-card::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 3px;
  border-radius: 20px 20px 0 0;
}

.skill-card:nth-child(1)::before { background: linear-gradient(90deg, var(--neon-blue), var(--neon-purple)); }
.skill-card:nth-child(2)::before { background: linear-gradient(90deg, var(--neon-purple), var(--neon-pink)); }
.skill-card:nth-child(3)::before { background: linear-gradient(90deg, var(--neon-pink), #ff4444); }
.skill-card:nth-child(4)::before { background: linear-gradient(90deg, #ff4444, #ffaa00); }
.skill-card:nth-child(5)::before { background: linear-gradient(90deg, var(--neon-green), var(--neon-blue)); }
.skill-card:nth-child(6)::before { background: linear-gradient(90deg, #ffaa00, var(--neon-green)); }

.skill-card:hover {
  border-color: rgba(0,240,255,0.2);
  box-shadow: 0 20px 60px rgba(0,0,0,0.5), 0 0 30px rgba(0,240,255,0.1);
}

.skill-icon {
  font-size: 3.5rem;
  margin-bottom: 15px;
  display: block;
  filter: drop-shadow(0 0 10px rgba(0,240,255,0.5));
  transition: transform 0.5s;
}

.skill-card:hover .skill-icon { transform: translateZ(30px) scale(1.15); }

.skill-card h3 {
  font-family: 'Orbitron', monospace;
  font-size: 1.1rem;
  margin-bottom: 10px;
  color: #fff;
}

.skill-card p {
  color: #777;
  font-size: 0.9rem;
  line-height: 1.6;
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  justify-content: center;
  margin-top: 15px;
}

.skill-tags span {
  padding: 3px 10px;
  border-radius: 10px;
  font-size: 0.7rem;
  background: rgba(0,240,255,0.08);
  color: var(--neon-blue);
  border: 1px solid rgba(0,240,255,0.15);
}

/* STATS */
.stats-section {
  background: linear-gradient(180deg, transparent, rgba(0,240,255,0.03), transparent);
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 20px;
  max-width: 900px;
  margin: 0 auto;
}

.stat-item {
  text-align: center;
  padding: 30px 15px;
  border-radius: 15px;
  background: rgba(10,10,30,0.5);
  border: 1px solid rgba(255,255,255,0.03);
  transition: all 0.4s;
}

.stat-item:hover {
  transform: translateY(-5px);
  border-color: rgba(0,240,255,0.2);
}

.stat-number {
  font-family: 'Orbitron', monospace;
  font-size: clamp(2rem, 4vw, 2.8rem);
  font-weight: 900;
  background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.stat-label {
  color: #666;
  font-size: 0.85rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-top: 5px;
}

/* TIMELINE */
.timeline {
  max-width: 700px;
  margin: 0 auto;
  position: relative;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 20px;
  top: 0; bottom: 0;
  width: 2px;
  background: linear-gradient(to bottom, var(--neon-blue), var(--neon-purple), var(--neon-pink));
}

.timeline-item {
  padding-left: 55px;
  margin-bottom: 35px;
  position: relative;
  opacity: 0;
  transform: translateX(-20px);
  animation: fadeSlide 0.6s forwards;
}

.timeline-item:nth-child(1) { animation-delay: 0.2s; }
.timeline-item:nth-child(2) { animation-delay: 0.4s; }
.timeline-item:nth-child(3) { animation-delay: 0.6s; }
.timeline-item:nth-child(4) { animation-delay: 0.8s; }

@keyframes fadeSlide {
  to { opacity: 1; transform: translateX(0); }
}

.timeline-dot {
  position: absolute;
  left: 12px; top: 5px;
  width: 18px; height: 18px;
  border-radius: 50%;
  background: var(--neon-blue);
  box-shadow: 0 0 15px var(--neon-blue);
}

.timeline-item h4 {
  font-family: 'Orbitron', monospace;
  font-size: 1rem;
  color: var(--neon-blue);
  margin-bottom: 5px;
}

.timeline-item .year {
  font-size: 0.8rem;
  color: var(--neon-purple);
  letter-spacing: 1px;
}

.timeline-item p {
  color: #777;
  font-size: 0.9rem;
  margin-top: 5px;
  line-height: 1.5;
}

/* FLOATING SHAPES */
.floating-shapes {
  position: fixed;
  top: 0; left: 0;
  width: 100%; height: 100%;
  z-index: 1;
  pointer-events: none;
  overflow: hidden;
}

.shape {
  position: absolute;
  border-radius: 50%;
  opacity: 0.03;
  animation: float 20s ease-in-out infinite;
}

.shape:nth-child(1) {
  width: 400px; height: 400px;
  background: var(--neon-blue);
  top: -100px; right: -100px;
  animation-duration: 25s;
}
.shape:nth-child(2) {
  width: 300px; height: 300px;
  background: var(--neon-purple);
  bottom: -50px; left: -50px;
  animation-duration: 20s;
  animation-delay: 5s;
}
.shape:nth-child(3) {
  width: 200px; height: 200px;
  background: var(--neon-pink);
  top: 50%; left: 50%;
  animation-duration: 15s;
  animation-delay: 10s;
}

@keyframes float {
  0%, 100% { transform: translate(0, 0) scale(1); }
  25% { transform: translate(50px, -50px) scale(1.1); }
  50% { transform: translate(-30px, 30px) scale(0.95); }
  75% { transform: translate(20px, 50px) scale(1.05); }
}

/* CONTACT */
.contact-section { text-align: center; }

.contact-links {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
  justify-content: center;
  margin-top: 20px;
}

.contact-link {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 12px 24px;
  border-radius: 50px;
  background: rgba(15,15,40,0.8);
  border: 1px solid rgba(255,255,255,0.08);
  color: #ccc;
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s;
  cursor: pointer;
}

.contact-link:hover {
  border-color: var(--neon-blue);
  color: var(--neon-blue);
  box-shadow: 0 5px 25px rgba(0,240,255,0.2);
  transform: translateY(-3px);
}

.contact-link.primary {
  background: linear-gradient(135deg, rgba(0,240,255,0.15), rgba(180,0,255,0.15));
  border-color: var(--neon-blue);
  color: var(--neon-blue);
}

.contact-link.primary:hover {
  background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
  color: #fff;
  box-shadow: 0 8px 35px rgba(0,240,255,0.35);
}

.contact-link.secondary {
  background: linear-gradient(135deg, rgba(255,68,68,0.1), rgba(255,170,0,0.1));
  border-color: #ff6b4a;
  color: #ff6b4a;
}

.contact-link.secondary:hover {
  background: linear-gradient(135deg, #ff4444, #ffaa00);
  color: #fff;
  box-shadow: 0 8px 35px rgba(255,68,68,0.35);
}

/* FOOTER */
footer {
  text-align: center;
  padding: 30px;
  border-top: 1px solid rgba(255,255,255,0.05);
  color: #444;
  font-size: 0.85rem;
  position: relative;
  z-index: 2;
}

/* MOBILE NAV */
.nav-toggle { display: none; background: none; border: none; color: #fff; font-size: 1.5rem; cursor: pointer; }

@media (max-width: 700px) {
  .nav-links {
    display: none;
    position: absolute;
    top: 100%; left: 0; right: 0;
    flex-direction: column;
    background: rgba(5,5,16,0.95);
    padding: 20px;
    gap: 15px;
    backdrop-filter: blur(20px);
  }
  .nav-links.active { display: flex; }
  .nav-toggle { display: block; }
  .skills-grid { grid-template-columns: 1fr; }
  .hero { padding: 20px; }
}

/* SCROLL ANIMATION */
.reveal {
  opacity: 0;
  transform: translateY(40px);
  transition: all 0.8s cubic-bezier(0.23, 1, 0.32, 1);
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}

/* Glitch effect */
.glitch { position: relative; }
.glitch::before, .glitch::after {
  content: attr(data-text);
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
}
.glitch::before {
  animation: glitch1 3s infinite;
  clip-path: polygon(0 0, 100% 0, 100% 35%, 0 35%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background: linear-gradient(135deg, #ff00aa, #b400ff);
}
.glitch::after {
  animation: glitch2 3s infinite;
  clip-path: polygon(0 65%, 100% 65%, 100% 100%, 0 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
}

@keyframes glitch1 {
  0%, 90%, 100% { transform: translate(0); }
  92% { transform: translate(3px, -1px); }
  94% { transform: translate(-3px, 1px); }
  96% { transform: translate(2px, 1px); }
}
@keyframes glitch2 {
  0%, 90%, 100% { transform: translate(0); }
  91% { transform: translate(-3px, 1px); }
  93% { transform: translate(3px, -1px); }
  95% { transform: translate(-2px, -1px); }
}

/* Typewriter */
.typewriter {
  border-right: 2px solid var(--neon-blue);
  animation: blink 0.8s step-end infinite;
  white-space: nowrap;
  overflow: hidden;
  display: inline-block;
}
@keyframes blink { 50% { border-color: transparent; } }
</style>
</head>
<body>

<canvas id="particles"></canvas>

<div class="floating-shapes">
  <div class="shape"></div>
  <div class="shape"></div>
  <div class="shape"></div>
</div>

<div class="cursor-glow" id="cursorGlow"></div>

<nav>
  <div class="nav-logo">⟨DEV/⟩</div>
  <button class="nav-toggle" id="navToggle">☰</button>
  <ul class="nav-links" id="navLinks">
    <li><a href="#home">Home</a></li>
    <li><a href="#skills">Skills</a></li>
    <li><a href="#journey">Journey</a></li>
    <li><a href="#stats">Stats</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<!-- HERO -->
<section class="hero" id="home">
  <div class="hero-grid"></div>
  <div class="hero-content">
    <div class="avatar-3d">
      <div class="avatar-face">
        🧑‍💻
        <div class="avatar-ring"></div>
        <div class="avatar-ring"></div>
      </div>
    </div>
    <div class="hero-badge">🌐 Available for Collaboration</div>
    <h1 class="hero-title">
      <span class="line1">PORTFOLIO</span><br>
      <span class="line2 glitch" data-text="WEBSITE">WEBSITE</span>
    </h1>
    <p class="hero-sub">
      <span class="typewriter" id="typewriter"></span>
    </p>
    <div class="hero-roles">
      <span class="role-chip">🎮 Game Dev</span>
      <span class="role-chip">💻 Coder</span>
      <span class="role-chip">🎨 3D Artist</span>
      <span class="role-chip">🎬 YouTuber</span>
      <span class="role-chip">🔬 Researcher</span>
      <span class="role-chip">🤖 AI Prompt Engineer</span>
    </div>
    <a href="#skills" class="cta-btn">Explore My Universe ↓</a>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="reveal">
    <h2 class="section-title">⚡ Skill Arsenal</h2>
    <p class="section-sub">Multidisciplinary expertise across digital domains</p>
  </div>
  <div class="skills-grid">
    <div class="skill-card reveal">
      <span class="skill-icon">🎮</span>
      <h3>Game Developer</h3>
      <p>Crafting immersive gameplay experiences with cutting-edge engines and custom mechanics that captivate players.</p>
      <div class="skill-tags">
        <span>Unity</span><span>Unreal</span><span>Godot</span><span>C#</span><span>Game Design</span>
      </div>
    </div>
    <div class="skill-card reveal">
      <span class="skill-icon">⚙️</span>
      <h3>AI Automation Expert</h3>
      <p>Designing and deploying intelligent automation pipelines that streamline workflows and amplify productivity using cutting-edge AI.</p>
      <div class="skill-tags">
        <span>n8n</span><span>Zapier</span><span>LangChain</span><span>AutoGPT</span><span>Pipelines</span>
      </div>
    </div>
    <div class="skill-card reveal">
      <span class="skill-icon">🎨</span>
      <h3>3D Modelling Artist</h3>
      <p>Sculpting stunning 3D assets, environments, and characters from concept to final render.</p>
      <div class="skill-tags">
        <span>Blender</span><span>ZBrush</span><span>Substance</span><span>UV Mapping</span><span>Rigging</span>
      </div>
    </div>
    <div class="skill-card reveal">
      <span class="skill-icon">🎬</span>
      <h3>YouTuber & Creator</h3>
      <p>Producing engaging video content, tutorials, and devlogs that educate and inspire communities.</p>
      <div class="skill-tags">
        <span>Editing</span><span>Storytelling</span><span>Thumbnails</span><span>SEO</span><span>Growth</span>
      </div>
    </div>
    <div class="skill-card reveal">
      <span class="skill-icon">🔬</span>
      <h3>Research Expert</h3>
      <p>Deep-diving into emerging technologies, publishing findings, and pushing the boundaries of knowledge.</p>
      <div class="skill-tags">
        <span>AI/ML</span><span>Papers</span><span>Analysis</span><span>Data</span><span>Innovation</span>
      </div>
    </div>
    <div class="skill-card reveal">
      <span class="skill-icon">🤖</span>
      <h3>AI Prompt Engineer</h3>
      <p>Mastering the art of AI communication—designing prompts that unlock maximum potential from LLMs.</p>
      <div class="skill-tags">
        <span>GPT</span><span>Claude</span><span>MidJourney</span><span>Chains</span><span>Fine-tuning</span>
      </div>
    </div>
  </div>
</section>

<!-- STATS -->
<section class="stats-section" id="stats">
  <div class="reveal">
    <h2 class="section-title">📊 By The Numbers</h2>
    <p class="section-sub">Impact measured in milestones</p>
  </div>
  <div class="stats-grid reveal">
    <div class="stat-item">
      <div class="stat-number" data-target="50">0</div>
      <div class="stat-label">Projects Built</div>
    </div>
    <div class="stat-item">
      <div class="stat-number" data-target="10">0</div>
      <div class="stat-label">Games Shipped</div>
    </div>
    <div class="stat-item">
      <div class="stat-number" data-target="500">0</div>
      <div class="stat-label">3D Models</div>
    </div>
    <div class="stat-item">
      <div class="stat-number" data-target="100">0</div>
      <div class="stat-label">Videos Made</div>
    </div>
    <div class="stat-item">
      <div class="stat-number" data-target="15">0</div>
      <div class="stat-label">Research Papers</div>
    </div>
    <div class="stat-item">
      <div class="stat-number" data-target="1000">0</div>
      <div class="stat-label">AI Prompts</div>
    </div>
  </div>
</section>

<!-- JOURNEY -->
<section id="journey">
  <div class="reveal">
    <h2 class="section-title">🚀 The Journey</h2>
    <p class="section-sub">Key milestones in my evolution</p>
  </div>
  <div class="timeline">
    <div class="timeline-item">
      <div class="timeline-dot"></div>
      <span class="year">🟢 THE BEGINNING</span>
      <h4>First Line of Code</h4>
      <p>Fell in love with programming and discovered the power of creating something from nothing.</p>
    </div>
    <div class="timeline-item">
      <div class="timeline-dot" style="background:var(--neon-purple);box-shadow:0 0 15px var(--neon-purple)"></div>
      <span class="year">🎮 GAME DEV ERA</span>
      <h4>First Game Published</h4>
      <p>Shipped my first indie game — combining code, art, and design into a cohesive interactive experience.</p>
    </div>
    <div class="timeline-item">
      <div class="timeline-dot" style="background:var(--neon-pink);box-shadow:0 0 15px var(--neon-pink)"></div>
      <span class="year">🎬 CONTENT CREATION</span>
      <h4>YouTube Channel Launch</h4>
      <p>Started sharing knowledge through devlogs, tutorials, and deep-dives into game development and AI.</p>
    </div>
    <div class="timeline-item">
      <div class="timeline-dot" style="background:var(--neon-green);box-shadow:0 0 15px var(--neon-green)"></div>
      <span class="year">🤖 AI REVOLUTION</span>
      <h4>AI & Automation Mastery</h4>
      <p>Pioneered advanced AI automation pipelines and prompt engineering techniques integrated into creative workflows.</p>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section class="contact-section" id="contact">
  <div class="reveal">
    <h2 class="section-title">🌐 Let's Connect</h2>
    <p class="section-sub">Ready to build something extraordinary together?</p>
    <div class="contact-links">
      <a href="https://aryan-creations.itch.io/" target="_blank" class="contact-link secondary">🎮 GameDev Portfolio</a>
      <a href="mailto:aryankumar3261@gmail.com" class="contact-link primary">📧 Email Me</a>
      <div class="contact-link">📺 YouTube Channel</div>
      <div class="contact-link">💻 GitHub Profile</div>
      <div class="contact-link">🐦 Twitter / X</div>
      <div class="contact-link">💼 LinkedIn</div>
    </div>
  </div>
</section>

<footer>
  <p>⟨/⟩ Designed & Built with 💜 — Portfolio Website © 2026</p>
</footer>

<script>
// ========== PARTICLE SYSTEM ==========
const canvas = document.getElementById('particles');
const ctx = canvas.getContext('2d');
let particles = [];
let mouse = { x: -1000, y: -1000 };

function resizeCanvas() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
}
resizeCanvas();
window.addEventListener('resize', resizeCanvas);

class Particle {
  constructor() { this.reset(); }
  reset() {
    this.x = Math.random() * canvas.width;
    this.y = Math.random() * canvas.height;
    this.size = Math.random() * 2 + 0.5;
    this.speedX = (Math.random() - 0.5) * 0.5;
    this.speedY = (Math.random() - 0.5) * 0.5;
    this.opacity = Math.random() * 0.5 + 0.1;
    this.color = ['0,240,255','180,0,255','255,0,170','0,255,136'][Math.floor(Math.random()*4)];
  }
  update() {
    this.x += this.speedX;
    this.y += this.speedY;
    const dx = mouse.x - this.x;
    const dy = mouse.y - this.y;
    const dist = Math.sqrt(dx*dx + dy*dy);
    if(dist < 150) {
      this.x -= dx * 0.01;
      this.y -= dy * 0.01;
      this.opacity = Math.min(1, this.opacity + 0.02);
    }
    if(this.x < 0 || this.x > canvas.width || this.y < 0 || this.y > canvas.height) this.reset();
  }
  draw() {
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(${this.color},${this.opacity})`;
    ctx.fill();
  }
}

for(let i = 0; i < 120; i++) particles.push(new Particle());

function drawConnections() {
  for(let i = 0; i < particles.length; i++) {
    for(let j = i+1; j < particles.length; j++) {
      const dx = particles[i].x - particles[j].x;
      const dy = particles[i].y - particles[j].y;
      const dist = Math.sqrt(dx*dx + dy*dy);
      if(dist < 120) {
        ctx.beginPath();
        ctx.moveTo(particles[i].x, particles[i].y);
        ctx.lineTo(particles[j].x, particles[j].y);
        ctx.strokeStyle = `rgba(0,240,255,${0.08 * (1 - dist/120)})`;
        ctx.lineWidth = 0.5;
        ctx.stroke();
      }
    }
  }
}

function animateParticles() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  particles.forEach(p => { p.update(); p.draw(); });
  drawConnections();
  requestAnimationFrame(animateParticles);
}
animateParticles();

// ========== CURSOR GLOW ==========
const glow = document.getElementById('cursorGlow');
document.addEventListener('mousemove', e => {
  mouse.x = e.clientX;
  mouse.y = e.clientY;
  glow.style.left = e.clientX + 'px';
  glow.style.top = e.clientY + 'px';
});

// ========== 3D CARD TILT ==========
document.querySelectorAll('.skill-card').forEach(card => {
  card.addEventListener('mousemove', e => {
    const rect = card.getBoundingClientRect();
    const x = e.clientX - rect.left;
    const y = e.clientY - rect.top;
    const centerX = rect.width / 2;
    const centerY = rect.height / 2;
    const rotateX = (y - centerY) / 12;
    const rotateY = (centerX - x) / 12;
    card.style.transform = `perspective(800px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) scale(1.03)`;
  });
  card.addEventListener('mouseleave', () => {
    card.style.transform = 'perspective(800px) rotateX(0) rotateY(0) scale(1)';
  });
});

// ========== TYPEWRITER ==========
const phrases = [
  "Game Developer crafting immersive worlds 🎮",
  "AI Automation Expert building smart pipelines ⚙️",
  "3D Modelling Artist shaping digital dreams 🎨",
  "YouTuber sharing knowledge & creativity 🎬",
  "Research Expert pushing boundaries 🔬",
  "AI Prompt Engineer mastering LLMs 🤖"
];
let phraseIdx = 0, charIdx = 0, deleting = false;
const typeEl = document.getElementById('typewriter');

function typewrite() {
  const current = phrases[phraseIdx];
  if(!deleting) {
    typeEl.textContent = current.substring(0, charIdx + 1);
    charIdx++;
    if(charIdx === current.length) {
      setTimeout(() => { deleting = true; typewrite(); }, 2000);
      return;
    }
    setTimeout(typewrite, 60);
  } else {
    typeEl.textContent = current.substring(0, charIdx - 1);
    charIdx--;
    if(charIdx === 0) {
      deleting = false;
      phraseIdx = (phraseIdx + 1) % phrases.length;
      setTimeout(typewrite, 400);
      return;
    }
    setTimeout(typewrite, 30);
  }
}
typewrite();

// ========== NAV TOGGLE ==========
document.getElementById('navToggle').addEventListener('click', () => {
  document.getElementById('navLinks').classList.toggle('active');
});

document.querySelectorAll('.nav-links a').forEach(a => {
  a.addEventListener('click', () => {
    document.getElementById('navLinks').classList.remove('active');
  });
});

// ========== SCROLL REVEAL ==========
const observer = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if(entry.isIntersecting) entry.target.classList.add('visible');
  });
}, { threshold: 0.1 });

document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

// ========== COUNTER ANIMATION ==========
const counterObserver = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if(entry.isIntersecting) {
      entry.target.querySelectorAll('.stat-number').forEach(num => {
        const target = parseInt(num.dataset.target);
        let count = 0;
        const step = Math.max(1, Math.floor(target / 60));
        const timer = setInterval(() => {
          count += step;
          if(count >= target) { count = target; clearInterval(timer); }
          num.textContent = count + '+';
        }, 30);
      });
      counterObserver.unobserve(entry.target);
    }
  });
}, { threshold: 0.3 });

document.querySelectorAll('.stats-grid').forEach(el => counterObserver.observe(el));

// ========== SMOOTH SECTION TRANSITIONS ==========
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
  anchor.addEventListener('click', function(e) {
    e.preventDefault();
    const target = document.querySelector(this.getAttribute('href'));
    if(target) target.scrollIntoView({ behavior: 'smooth' });
  });
});
</script>
</body>
</html>
