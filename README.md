<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>PORTFOLIO WEBSITE</title>
<style>
body{margin:0;background:#03040a;color:#fff;font-family:Montserrat,Arial,sans-serif;display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:100vh;overflow:hidden}
main{position:relative;width:min(900px,90vw);text-align:center;padding:2rem 1rem;border-radius:25px;background:rgba(10,15,30,.65);backdrop-filter:blur(15px);box-shadow:0 30px 70px rgba(0,0,0,.6)}
h1{margin:0 0 .3rem;font-size:clamp(1.8rem,6vw,3rem);letter-spacing:.4rem}
p{margin:.3rem 0 1rem;color:#a0b0ff}
#halo{position:absolute;width:180%;height:180%;top:-40%;left:-40%;background:radial-gradient(circle,#072bff40,#ff00ff10,transparent);filter:blur(40px);animation:aura 12s linear infinite}
@keyframes aura{0%{transform:rotate(0deg)}100%{transform:rotate(360deg)}}
#scene{position:relative;width:100%;height:360px;perspective:1000px;margin:2rem 0}
#ring{width:100%;height:100%;transform-style:preserve-3d;animation:spin 18s linear infinite}
@keyframes spin{0%{transform:rotateX(-8deg) rotateY(0deg)}100%{transform:rotateX(-8deg) rotateY(360deg)}}
.card{position:absolute;top:50%;left:50%;width:180px;height:230px;margin:-115px -90px;background:rgba(15,25,50,.8);border:1px solid rgba(255,255,255,.2);border-radius:18px;padding:1.2rem;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:.6rem;box-shadow:0 15px 35px rgba(0,0,0,.45);transition:transform .4s,box-shadow .4s}
.card span{font-size:3rem}
.card h2{margin:0;font-size:1rem;letter-spacing:.15rem;color:#7df}
.card small{color:#9cb}
.card:hover{box-shadow:0 20px 50px rgba(0,255,255,.35);transform:translateZ(20px)}
.links{display:flex;flex-wrap:wrap;gap:1rem;justify-content:center;margin-top:1.5rem}
a.btn{padding:.9rem 1.6rem;border-radius:999px;text-decoration:none;font-weight:700;letter-spacing:.15rem;text-transform:uppercase}
a.primary{background:linear-gradient(120deg,#00f0ff,#7b61ff);color:#03122a;box-shadow:0 10px 25px rgba(0,240,255,.35)}
a.secondary{border:1px solid #ff7ad1;color:#ffb6ff;background:rgba(255,0,170,.1)}
@media(max-width:600px){#scene{height:280px} .card{width:140px;height:190px;margin:-95px -70px}}
</style>
</head>
<body>
<main>
<div id="halo"></div>
<h1>PORTFOLIO WEBSITE</h1>
<p>Game Developer • AI Automation Expert • 3D Artist • YouTuber • Researcher • Prompt Engineer</p>
<div id="scene">
<div id="ring">
<div class="card" style="--i:0;transform:rotateY(0deg) translateZ(320px)">
<span>🎮</span><h2>Game Dev</h2><small>Worlds & mechanics</small>
</div>
<div class="card" style="--i:1;transform:rotateY(60deg) translateZ(320px)">
<span>⚙️</span><h2>AI Auto</h2><small>Smart pipelines</small>
</div>
<div class="card" style="--i:2;transform:rotateY(120deg) translateZ(320px)">
<span>🧊</span><h2>3D Art</h2><small>Models & shaders</small>
</div>
<div class="card" style="--i:3;transform:rotateY(180deg) translateZ(320px)">
<span>🎥</span><h2>YouTuber</h2><small>Docs & devlogs</small>
</div>
<div class="card" style="--i:4;transform:rotateY(240deg) translateZ(320px)">
<span>🔬</span><h2>Research</h2><small>Future-focused</small>
</div>
<div class="card" style="--i:5;transform:rotateY(300deg) translateZ(320px)">
<span>🤖</span><h2>Prompt Eng</h2><small>LLM mastery</small>
</div>
</div>
</div>
<div class="links">
<a class="primary btn" href="mailto:aryankumar3261@gmail.com">Contact</a>
<a class="secondary btn" href="https://aryan-creations.itch.io/" target="_blank">GameDev Profile</a>
</div>
</main>
</body>
</html>
