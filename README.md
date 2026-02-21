<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>3D Immersive Portfolio</title>
    <style>
        :root {
            --bg-color: #05050a;
            --text-main: #ffffff;
            --text-muted: #8892b0;
            --primary: #00f3ff;
            --accent: #ff007b;
            --glass: rgba(10, 10, 25, 0.8);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            user-select: none;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            overflow: hidden;
            width: 100vw;
            height: 100vh;
            touch-action: none;
        }

        /* UI Layer */
        #ui-layer {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 100;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            padding: 2rem;
        }

        header {
            text-align: center;
            text-shadow: 0 0 10px rgba(0, 243, 255, 0.5);
        }

        h1 {
            font-size: clamp(1.8rem, 6vw, 3.5rem);
            font-weight: 900;
            letter-spacing: 4px;
            text-transform: uppercase;
            background: linear-gradient(90deg, var(--primary), #fff, var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .subtitle {
            color: var(--text-muted);
            font-size: 0.9rem;
            margin-top: 0.5rem;
            letter-spacing: 2px;
            text-transform: uppercase;
        }

        /* Action Buttons */
        .action-container {
            position: absolute;
            top: 2rem;
            right: 2rem;
            display: flex;
            gap: 1rem;
            pointer-events: auto;
        }

        .btn {
            padding: 0.8rem 1.2rem;
            border-radius: 12px;
            background: var(--glass);
            border: 1px solid rgba(255, 255, 255, 0.1);
            color: white;
            text-decoration: none;
            font-size: 0.85rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 8px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
        }

        .btn:hover {
            transform: translateY(-3px);
            border-color: var(--primary);
            box-shadow: 0 0 20px rgba(0, 243, 255, 0.4);
        }

        .btn-itch {
            border-color: var(--accent);
        }
        
        .btn-itch:hover {
            border-color: #fff;
            box-shadow: 0 0 20px rgba(255, 0, 123, 0.4);
        }

        #info-panel {
            background: var(--glass);
            border: 1px solid rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            padding: 1.5rem;
            border-radius: 20px;
            max-width: 500px;
            margin: 0 auto;
            text-align: center;
            transform: translateY(120px);
            opacity: 0;
            transition: all 0.6s cubic-bezier(0.23, 1, 0.32, 1);
            pointer-events: auto;
        }

        #info-panel.visible {
            transform: translateY(0);
            opacity: 1;
        }

        #info-title {
            font-size: 1.6rem;
            margin-bottom: 0.8rem;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
        }

        .controls-hint {
            position: absolute;
            bottom: 2rem;
            left: 50%;
            transform: translateX(-50%);
            color: rgba(255,255,255,0.4);
            font-size: 0.7rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            animation: pulse 2s infinite;
        }

        /* 3D Scene Setup */
        #world {
            position: absolute;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            perspective: 1200px;
            overflow: hidden;
            cursor: grab;
        }

        #world:active { cursor: grabbing; }

        #camera {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            transform-style: preserve-3d;
            transform: translateZ(-600px);
        }

        #scene {
            position: absolute;
            top: 0;
            left: 0;
            width: 0;
            height: 0;
            transform-style: preserve-3d;
        }

        /* Floating Cube Core */
        .core {
            position: absolute;
            top: -50px;
            left: -50px;
            width: 100px;
            height: 100px;
            transform-style: preserve-3d;
            animation: coreSpin 20s infinite linear;
        }

        .core-face {
            position: absolute;
            width: 100px;
            height: 100px;
            background: rgba(0, 243, 255, 0.05);
            border: 1px solid rgba(0, 243, 255, 0.3);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.5rem;
        }

        .core-face:nth-child(1) { transform: translateZ(50px); }
        .core-face:nth-child(2) { transform: rotateY(180deg) translateZ(50px); }
        .core-face:nth-child(3) { transform: rotateY(90deg) translateZ(50px); }
        .core-face:nth-child(4) { transform: rotateY(-90deg) translateZ(50px); }
        .core-face:nth-child(5) { transform: rotateX(90deg) translateZ(50px); }
        .core-face:nth-child(6) { transform: rotateX(-90deg) translateZ(50px); }

        /* Skill Cards */
        .card {
            position: absolute;
            width: 220px;
            height: 300px;
            left: -110px;
            top: -150px;
            background: rgba(15, 15, 30, 0.7);
            border: 2px solid var(--clr);
            border-radius: 24px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            transform-style: preserve-3d;
            transition: transform 0.4s, box-shadow 0.3s;
            pointer-events: auto;
            backdrop-filter: blur(8px);
            -webkit-backdrop-filter: blur(8px);
        }

        .card:hover {
            background: rgba(25, 25, 45, 0.9);
            box-shadow: 0 0 30px var(--clr);
        }

        .card-icon {
            font-size: 5rem;
            margin-bottom: 1.2rem;
            transform: translateZ(40px);
            filter: drop-shadow(0 0 10px var(--clr));
        }

        .card-title {
            font-size: 1rem;
            font-weight: 800;
            color: #fff;
            text-transform: uppercase;
            text-align: center;
            transform: translateZ(25px);
            text-shadow: 0 0 5px var(--clr);
        }

        /* Background Dust */
        .particle {
            position: absolute;
            width: 2px;
            height: 2px;
            background: #fff;
            border-radius: 50%;
            transform-style: preserve-3d;
        }

        @keyframes coreSpin {
            0% { transform: rotateX(0deg) rotateY(0deg); }
            100% { transform: rotateX(360deg) rotateY(720deg); }
        }

        @keyframes pulse {
            0%, 100% { opacity: 0.2; }
            50% { opacity: 0.7; }
        }

        @media (max-width: 768px) {
            .action-container { 
                top: auto;
                bottom: 8rem;
                right: 0;
                left: 0;
                justify-content: center;
            }
            #camera { transform: translateZ(-900px); }
            .card { width: 180px; height: 260px; left: -90px; top: -130px; }
        }
    </style>
</head>
<body>

    <div id="ui-layer">
        <header>
            <h1>PORTFOLIO WEBSITE</h1>
            <div class="subtitle">Creator • Innovator • Developer</div>
        </header>

        <div class="action-container">
            <a href="mailto:aryankumar3261@gmail.com" class="btn">
                <span>📧</span> Contact Me
            </a>
            <a href="https://aryan-creations.itch.io/" target="_blank" class="btn btn-itch">
                <span>🕹️</span> GameDev Profile
            </a>
        </div>

        <div id="info-panel">
            <h2 id="info-title"><span></span></h2>
            <p id="info-desc"></p>
        </div>

        <div class="controls-hint">Drag Space to Rotate • Click Cards to View Skills</div>
    </div>

    <div id="world">
        <div id="camera">
            <div id="scene">
                <div class="core">
                    <div class="core-face">💠</div>
                    <div class="core-face">⚡</div>
                    <div class="core-face">🌌</div>
                    <div class="core-face">🛡️</div>
                    <div class="core-face">🔮</div>
                    <div class="core-face">💎</div>
                </div>
            </div>
        </div>
    </div>

    <script>
        const skills = [
            { id: 'game', title: "Game Developer", icon: "🎮", color: "#ff0055", desc: "Building interactive experiences with polished mechanics, custom physics, and engaging game loops." },
            { id: 'ai-auto', title: "AI Automation Expert", icon: "⚙️", color: "#00ff99", desc: "Expertise in creating autonomous agents and integrating AI models into existing business workflows for maximum efficiency." },
            { id: '3d', title: "3D Modelling Artist", icon: "🧊", color: "#00ccff", desc: "Creating detailed 3D assets, characters, and environments with a focus on optimized geometry and realistic textures." },
            { id: 'youtube', title: "YouTuber", icon: "🎥", color: "#ff3300", desc: "Educating and entertaining the developer community through high-quality video content and technical breakdowns." },
            { id: 'research', title: "Research Expert", icon: "🔬", color: "#9900ff", desc: "Deep diving into emerging tech trends, algorithms, and methodologies to stay at the forefront of the industry." },
            { id: 'prompt', title: "AI Prompt Engineer", icon: "🤖", color: "#ffcc00", desc: "Mastering the art of communicating with LLMs to generate high-quality code, art, and complex logic structures." }
        ];

        const scene = document.getElementById('scene');
        const infoPanel = document.getElementById('info-panel');
        const infoTitle = document.getElementById('info-title');
        const infoDesc = document.getElementById('info-desc');

        const radius = window.innerWidth < 600 ? 400 : 500;
        
        // Build Cards
        skills.forEach((skill, index) => {
            const angle = (index / skills.length) * Math.PI * 2;
            const x = Math.sin(angle) * radius;
            const z = Math.cos(angle) * radius;

            const card = document.createElement('div');
            card.className = 'card';
            card.style.setProperty('--clr', skill.color);
            card.style.transform = `translate3d(${x}px, 0px, ${z}px) rotateY(${angle}rad)`;

            card.innerHTML = `
                <div class="card-icon">${skill.icon}</div>
                <div class="card-title">${skill.title}</div>
            `;

            card.addEventListener('pointerup', (e) => {
                if (isDragging) return; 
                infoTitle.innerHTML = `<span style="text-shadow: 0 0 10px ${skill.color}">${skill.icon}</span> <span style="color: ${skill.color}">${skill.title}</span>`;
                infoDesc.innerText = skill.desc;
                infoPanel.style.border = `1px solid ${skill.color}50`;
                infoPanel.classList.add('visible');
                targetRotY = -angle * (180 / Math.PI);
                targetRotX = 0;
            });

            scene.appendChild(card);
        });

        // Background Particles
        for (let i = 0; i < 200; i++) {
            const star = document.createElement('div');
            star.className = 'particle';
            const dist = 800 + Math.random() * 1000;
            const t = Math.random() * Math.PI * 2;
            const p = Math.acos((Math.random() * 2) - 1);
            const px = dist * Math.sin(p) * Math.cos(t);
            const py = dist * Math.sin(p) * Math.sin(t);
            const pz = dist * Math.cos(p);
            star.style.transform = `translate3d(${px}px, ${py}px, ${pz}px)`;
            star.style.opacity = Math.random();
            scene.appendChild(star);
        }

        // Camera Logic
        let isPointerDown = false, isDragging = false;
        let startX = 0, startY = 0;
        let rotX = -10, rotY = 0;
        let targetRotX = -10, targetRotY = 0;
        let lastInteraction = Date.now();

        const world = document.getElementById('world');
        world.addEventListener('pointerdown', (e) => {
            isPointerDown = true; isDragging = false;
            startX = e.clientX; startY = e.clientY;
            lastInteraction = Date.now();
            if(e.target === world) infoPanel.classList.remove('visible');
        });

        window.addEventListener('pointermove', (e) => {
            if (!isPointerDown) return;
            const dx = e.clientX - startX;
            const dy = e.clientY - startY;
            if (Math.abs(dx) > 5 || Math.abs(dy) > 5) isDragging = true;
            if (isDragging) {
                targetRotY += dx * 0.2;
                targetRotX -= dy * 0.2;
                targetRotX = Math.max(-45, Math.min(45, targetRotX));
                startX = e.clientX; startY = e.clientY;
                lastInteraction = Date.now();
            }
        });

        window.addEventListener('pointerup', () => isPointerDown = false);

        function animate() {
            if (!isPointerDown && (Date.now() - lastInteraction > 3000)) {
                targetRotY -= 0.1; // Gentle idle spin
            }
            rotX += (targetRotX - rotX) * 0.05;
            rotY += (targetRotY - rotY) * 0.05;
            scene.style.transform = `rotateX(${rotX}deg) rotateY(${rotY}deg)`;
            requestAnimationFrame(animate);
        }
        animate();

        window.addEventListener('resize', () => {
            const cam = document.getElementById('camera');
            cam.style.transform = window.innerWidth < 600 ? `translateZ(-900px)` : `translateZ(-600px)`;
        });
    </script>
</body>
</html>
