
# I'll write the complete HTML file directly to avoid truncation issues
html_code = r'''<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>إلى شهوده... ❤️</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;500;700;800;900&family=Reem+Kufi:wght@400;700&display=swap" rel="stylesheet">
    <style>
        /* ═══════════════════════════════════════════════════════════════
           CONFIGURATION — Replace these with your actual photo paths
           ═══════════════════════════════════════════════════════════════ */
        :root {
            /* Photo paths — replace with your uploaded images */
            --photo-01: url('photos/nonty-01.jpg');
            --photo-02: url('photos/nonty-02.jpg');
            --photo-03: url('photos/nonty-03.jpg');
            --photo-04: url('photos/nonty-04.jpg');
            --photo-05: url('photos/nonty-05.jpg');
            --photo-best: var(--photo-01);
            --music-file: 'music.mp3';
            --midnight: #0a0a0f;
            --deep-burgundy: #4a0e0e;
            --dark-wine: #2d0a0a;
            --soft-rose: #c9a0a0;
            --warm-white: #f5e6d3;
            --subtle-gold: #d4af37;
            --rose-glow: rgba(201, 160, 160, 0.3);
            --gold-glow: rgba(212, 175, 55, 0.2);
        }

        *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
        html { scroll-behavior: smooth; overflow-x: hidden; }
        body {
            font-family: 'Tajawal', 'Reem Kufi', sans-serif;
            background: var(--midnight);
            color: var(--warm-white);
            overflow-x: hidden;
            min-height: 100vh;
            direction: rtl;
            -webkit-font-smoothing: antialiased;
        }
        ::selection { background: var(--deep-burgundy); color: var(--warm-white); }

        #particle-canvas {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            z-index: 0; pointer-events: none;
        }

        .scene {
            position: relative; z-index: 1; min-height: 100vh;
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            padding: 2rem; opacity: 0; transform: translateY(30px);
            transition: opacity 1.2s cubic-bezier(0.4, 0, 0.2, 1), transform 1.2s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .scene.active { opacity: 1; transform: translateY(0); }
        .scene.hidden { display: none !important; }

        .title-main {
            font-family: 'Reem Kufi', sans-serif; font-size: clamp(2rem, 8vw, 4.5rem);
            font-weight: 700; color: var(--warm-white); text-align: center; line-height: 1.3;
            text-shadow: 0 0 40px var(--rose-glow), 0 0 80px rgba(201, 160, 160, 0.1);
            opacity: 0; transform: translateY(20px); animation: fadeInUp 1.5s ease forwards;
        }
        .title-sub {
            font-size: clamp(1.1rem, 4vw, 1.8rem); font-weight: 300; color: var(--soft-rose);
            text-align: center; margin-top: 1rem; line-height: 1.6;
            opacity: 0; animation: fadeInUp 1.5s ease 0.5s forwards;
        }
        .text-body {
            font-size: clamp(1rem, 3vw, 1.3rem); font-weight: 400; color: var(--soft-rose);
            text-align: center; line-height: 1.8; max-width: 600px;
            opacity: 0; animation: fadeInUp 1.5s ease 0.8s forwards;
        }
        .text-glow { color: var(--subtle-gold); text-shadow: 0 0 20px var(--gold-glow); }

        @keyframes fadeInUp { to { opacity: 1; transform: translateY(0); } }

        .btn-glow {
            position: relative; display: inline-flex; align-items: center; justify-content: center;
            gap: 0.5rem; padding: 1rem 2.5rem; font-family: 'Tajawal', sans-serif;
            font-size: clamp(1rem, 3vw, 1.2rem); font-weight: 700; color: var(--warm-white);
            background: linear-gradient(135deg, var(--deep-burgundy), var(--dark-wine));
            border: 1px solid rgba(201, 160, 160, 0.3); border-radius: 50px; cursor: pointer;
            overflow: hidden; transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 0 4px 30px rgba(74, 14, 14, 0.4), 0 0 60px rgba(201, 160, 160, 0.1);
            margin-top: 2rem; opacity: 0; animation: fadeInUp 1.5s ease 1.2s forwards;
            text-decoration: none; user-select: none; -webkit-tap-highlight-color: transparent;
        }
        .btn-glow::before {
            content: ''; position: absolute; inset: 0;
            background: linear-gradient(135deg, transparent, rgba(255,255,255,0.1), transparent);
            transform: translateX(-100%); transition: transform 0.6s ease;
        }
        .btn-glow:hover::before, .btn-glow:active::before { transform: translateX(100%); }
        .btn-glow:hover, .btn-glow:active {
            transform: translateY(-3px) scale(1.02);
            box-shadow: 0 8px 40px rgba(74, 14, 14, 0.6), 0 0 80px rgba(201, 160, 160, 0.2);
            border-color: rgba(201, 160, 160, 0.6);
        }
        .btn-glow:active { transform: translateY(-1px) scale(0.98); }

        /* SCENE 01 */
        #scene-01 {
            background: var(--midnight); position: fixed; inset: 0; z-index: 100;
            transition: opacity 1.5s ease, visibility 1.5s ease;
        }
        #scene-01.fade-out { opacity: 0; visibility: hidden; pointer-events: none; }
        .star-field { position: absolute; inset: 0; overflow: hidden; }
        .star {
            position: absolute; width: 2px; height: 2px; background: white; border-radius: 50%; opacity: 0;
            animation: twinkle var(--duration) ease-in-out infinite; animation-delay: var(--delay);
        }
        @keyframes twinkle {
            0%, 100% { opacity: 0; transform: scale(0.5); }
            50% { opacity: var(--max-opacity); transform: scale(1); }
        }
        .glow-particle {
            position: absolute; width: 4px; height: 4px; background: var(--soft-rose);
            border-radius: 50%; filter: blur(2px); opacity: 0;
            animation: floatParticle 8s ease-in-out infinite; animation-delay: var(--delay);
        }
        @keyframes floatParticle {
            0% { opacity: 0; transform: translateY(100vh) scale(0); }
            10% { opacity: 0.6; } 90% { opacity: 0.6; }
            100% { opacity: 0; transform: translateY(-100px) scale(1.5); }
        }

        /* SCENE 02 */
        .photo-reveal {
            position: relative; width: min(85vw, 400px); aspect-ratio: 3/4;
            border-radius: 20px; overflow: hidden;
            box-shadow: 0 20px 60px rgba(0,0,0,0.5), 0 0 100px rgba(201, 160, 160, 0.15);
            opacity: 0; transform: scale(0.9); animation: photoReveal 2s ease 0.5s forwards;
        }
        .photo-reveal img { width: 100%; height: 100%; object-fit: cover; transition: transform 8s ease; }
        .photo-reveal:hover img, .photo-reveal.active img { transform: scale(1.1); }
        .photo-reveal::after {
            content: ''; position: absolute; inset: 0;
            background: linear-gradient(to bottom, transparent 50%, rgba(10,10,15,0.6) 100%); pointer-events: none;
        }
        @keyframes photoReveal { to { opacity: 1; transform: scale(1); } }

        /* SCENE 03 */
        .counter-container {
            display: grid; grid-template-columns: repeat(2, 1fr); gap: 1rem;
            margin-top: 2rem; max-width: 500px; width: 100%;
        }
        .counter-box {
            background: rgba(74, 14, 14, 0.3); backdrop-filter: blur(10px);
            border: 1px solid rgba(201, 160, 160, 0.2); border-radius: 16px;
            padding: 1.5rem 1rem; text-align: center;
            opacity: 0; transform: translateY(20px); animation: fadeInUp 1s ease forwards;
        }
        .counter-box:nth-child(1) { animation-delay: 0.3s; }
        .counter-box:nth-child(2) { animation-delay: 0.5s; }
        .counter-box:nth-child(3) { animation-delay: 0.7s; }
        .counter-box:nth-child(4) { animation-delay: 0.9s; }
        .counter-number {
            font-family: 'Reem Kufi', sans-serif; font-size: clamp(2rem, 6vw, 3rem);
            font-weight: 700; color: var(--subtle-gold); text-shadow: 0 0 20px var(--gold-glow); line-height: 1;
        }
        .counter-label { font-size: clamp(0.9rem, 2.5vw, 1.1rem); color: var(--soft-rose); margin-top: 0.5rem; font-weight: 500; }

        /* SCENE 04 */
        .timeline { position: relative; max-width: 700px; width: 100%; margin-top: 2rem; }
        .timeline::before {
            content: ''; position: absolute; right: 50%; transform: translateX(50%);
            width: 2px; height: 100%;
            background: linear-gradient(to bottom, var(--deep-burgundy), var(--soft-rose), var(--deep-burgundy));
            opacity: 0.5;
        }
        .timeline-card {
            position: relative; background: rgba(45, 10, 10, 0.6); backdrop-filter: blur(15px);
            border: 1px solid rgba(201, 160, 160, 0.15); border-radius: 20px;
            padding: 1.5rem; margin-bottom: 1.5rem; width: calc(50% - 2rem);
            opacity: 0; transform: translateX(-30px); transition: all 0.6s ease;
        }
        .timeline-card.visible { opacity: 1; transform: translateX(0); }
        .timeline-card:nth-child(even) { margin-right: auto; transform: translateX(30px); }
        .timeline-card:nth-child(even).visible { transform: translateX(0); }
        .timeline-card::after {
            content: ''; position: absolute; top: 50%; width: 12px; height: 12px;
            background: var(--subtle-gold); border-radius: 50%; box-shadow: 0 0 20px var(--gold-glow);
        }
        .timeline-card:nth-child(odd)::after { left: -2rem; transform: translate(-50%, -50%); }
        .timeline-card:nth-child(even)::after { right: -2rem; transform: translate(50%, -50%); }
        .timeline-date { font-family: 'Reem Kufi', sans-serif; font-size: 1.1rem; color: var(--subtle-gold); font-weight: 700; margin-bottom: 0.5rem; }
        .timeline-text { font-size: 1rem; color: var(--soft-rose); line-height: 1.7; }

        @media (max-width: 640px) {
            .timeline::before { right: 1rem; }
            .timeline-card { width: calc(100% - 3rem); margin-right: 3rem !important; }
            .timeline-card::after { right: -2rem !important; left: auto !important; transform: translate(50%, -50%) !important; }
            .timeline-card:nth-child(even) { margin-right: 3rem !important; }
        }

        /* SCENE 05 */
        .gallery-container { max-width: 1000px; width: 100%; margin-top: 2rem; columns: 2; column-gap: 1rem; }
        @media (min-width: 768px) { .gallery-container { columns: 3; } }
        .gallery-item {
            break-inside: avoid; margin-bottom: 1rem; position: relative;
            border-radius: 16px; overflow: hidden; cursor: pointer;
            opacity: 0; transform: translateY(30px) rotate(var(--rotation, 0deg));
            transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }
        .gallery-item.visible { opacity: 1; transform: translateY(0) rotate(var(--rotation, 0deg)); }
        .gallery-item:hover {
            transform: translateY(-5px) scale(1.02) rotate(0deg) !important;
            box-shadow: 0 20px 50px rgba(0,0,0,0.5), 0 0 40px rgba(201, 160, 160, 0.2);
            z-index: 10;
        }
        .gallery-item img { width: 100%; display: block; transition: transform 0.6s ease; }
        .gallery-item:hover img { transform: scale(1.1); }
        .gallery-caption {
            position: absolute; bottom: 0; left: 0; right: 0;
            padding: 1.5rem 1rem 1rem;
            background: linear-gradient(to top, rgba(10,10,15,0.9), transparent);
            font-size: 0.9rem; color: var(--soft-rose);
            transform: translateY(100%); transition: transform 0.4s ease;
        }
        .gallery-item:hover .gallery-caption { transform: translateY(0); }
        .gallery-item.polaroid { background: var(--warm-white); padding: 0.75rem 0.75rem 3rem; border-radius: 4px; }
        .gallery-item.polaroid img { border-radius: 2px; }
        .gallery-item.polaroid .gallery-caption {
            background: none; color: var(--dark-wine); bottom: 0.5rem;
            transform: none; padding: 0.5rem; text-align: center; font-weight: 700;
        }

        /* LIGHTBOX */
        .lightbox {
            position: fixed; inset: 0; z-index: 1000;
            background: rgba(10, 10, 15, 0.95); backdrop-filter: blur(20px);
            display: flex; align-items: center; justify-content: center;
            opacity: 0; visibility: hidden; transition: all 0.5s ease;
        }
        .lightbox.active { opacity: 1; visibility: visible; }
        .lightbox-img {
            max-width: 90vw; max-height: 80vh; object-fit: contain; border-radius: 12px;
            box-shadow: 0 30px 80px rgba(0,0,0,0.5);
            transform: scale(0.8); transition: transform 0.5s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .lightbox.active .lightbox-img { transform: scale(1); }
        .lightbox-caption { position: absolute; bottom: 2rem; text-align: center; color: var(--soft-rose); font-size: 1.1rem; padding: 0 2rem; }
        .lightbox-close, .lightbox-nav {
            position: absolute; background: rgba(45, 10, 10, 0.6);
            border: 1px solid rgba(201, 160, 160, 0.3); color: var(--warm-white);
            width: 50px; height: 50px; border-radius: 50%;
            display: flex; align-items: center; justify-content: center;
            cursor: pointer; font-size: 1.5rem; transition: all 0.3s ease; backdrop-filter: blur(10px);
        }
        .lightbox-close:hover, .lightbox-nav:hover { background: var(--deep-burgundy); transform: scale(1.1); }
        .lightbox-close { top: 1.5rem; left: 1.5rem; }
        .lightbox-prev { left: 1.5rem; top: 50%; transform: translateY(-50%); }
        .lightbox-next { right: 1.5rem; top: 50%; transform: translateY(-50%); }
        .lightbox-prev:hover { transform: translateY(-50%) scale(1.1); }
        .lightbox-next:hover { transform: translateY(-50%) scale(1.1); }

        /* SCENE 06 */
        .question-buttons { display: flex; gap: 1.5rem; margin-top: 2rem; flex-wrap: wrap; justify-content: center; }
        .btn-yes { background: linear-gradient(135deg, var(--deep-burgundy), #6b1515); border-color: rgba(201, 160, 160, 0.5); }
        .btn-escape { background: rgba(45, 10, 10, 0.5); border-color: rgba(201, 160, 160, 0.2); position: relative; transition: transform 0.3s ease; }

        /* SCENE 07 */
        .envelope-container { position: relative; width: min(90vw, 320px); aspect-ratio: 1.4; cursor: pointer; perspective: 1000px; margin: 2rem 0; }
        .envelope { position: relative; width: 100%; height: 100%; transform-style: preserve-3d; transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1); }
        .envelope.open { transform: rotateX(180deg); }
        .envelope-front {
            position: absolute; inset: 0;
            background: linear-gradient(135deg, #3d0e0e, var(--dark-wine));
            border-radius: 8px; border: 1px solid rgba(201, 160, 160, 0.3);
            display: flex; align-items: center; justify-content: center;
            backface-visibility: hidden; box-shadow: 0 20px 60px rgba(0,0,0,0.4);
        }
        .envelope-front::before { content: '💌'; font-size: 3rem; filter: drop-shadow(0 0 20px rgba(212, 175, 55, 0.5)); }
        .envelope-back { position: absolute; inset: 0; background: var(--dark-wine); border-radius: 8px; backface-visibility: hidden; transform: rotateX(180deg); }

        .letter {
            position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%) scale(0.8);
            width: min(90vw, 600px); max-height: 85vh;
            background: linear-gradient(135deg, #1a0f0f, #2d1a1a);
            border: 1px solid rgba(201, 160, 160, 0.3); border-radius: 16px;
            padding: 2rem; overflow-y: auto; z-index: 500;
            opacity: 0; visibility: hidden;
            transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 0 30px 100px rgba(0,0,0,0.6), 0 0 60px rgba(201, 160, 160, 0.1);
        }
        .letter.active { opacity: 1; visibility: visible; transform: translate(-50%, -50%) scale(1); }
        .letter-overlay {
            position: fixed; inset: 0; background: rgba(10, 10, 15, 0.8);
            backdrop-filter: blur(10px); z-index: 400;
            opacity: 0; visibility: hidden; transition: all 0.5s ease;
        }
        .letter-overlay.active { opacity: 1; visibility: visible; }
        .letter-content { font-family: 'Tajawal', sans-serif; font-size: clamp(1rem, 3vw, 1.15rem); line-height: 2; color: var(--soft-rose); white-space: pre-line; }
        .letter-content p { margin-bottom: 1rem; }
        .letter-signature { margin-top: 2rem; text-align: left; color: var(--subtle-gold); font-weight: 700; font-size: 1.1rem; }

        /* SCENE 09 */
        .final-reveal {
            position: fixed; inset: 0; z-index: 200; background: var(--midnight);
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            opacity: 0; visibility: hidden; transition: all 2s ease;
        }
        .final-reveal.active { opacity: 1; visibility: visible; }
        .final-photo {
            width: min(80vw, 450px); aspect-ratio: 3/4; border-radius: 20px; overflow: hidden;
            box-shadow: 0 30px 80px rgba(0,0,0,0.6), 0 0 100px rgba(201, 160, 160, 0.2);
            opacity: 0; transform: scale(1.1); transition: all 3s ease;
        }
        .final-reveal.active .final-photo { opacity: 1; transform: scale(1); }
        .final-photo img { width: 100%; height: 100%; object-fit: cover; animation: slowZoom 20s ease forwards; }
        @keyframes slowZoom { to { transform: scale(1.15); } }
        .final-text { text-align: center; margin-top: 2rem; opacity: 0; animation: fadeInUp 2s ease 2s forwards; }

        /* MUSIC */
        .music-btn {
            position: fixed; bottom: 1.5rem; left: 1.5rem; z-index: 300;
            width: 50px; height: 50px; border-radius: 50%;
            background: rgba(45, 10, 10, 0.6); backdrop-filter: blur(10px);
            border: 1px solid rgba(201, 160, 160, 0.3); color: var(--soft-rose);
            font-size: 1.3rem; cursor: pointer;
            display: flex; align-items: center; justify-content: center;
            transition: all 0.3s ease; box-shadow: 0 4px 20px rgba(0,0,0,0.3);
        }
        .music-btn:hover { background: var(--deep-burgundy); transform: scale(1.1); }
        .music-btn.playing { animation: pulse 2s ease infinite; border-color: var(--subtle-gold); color: var(--subtle-gold); }
        @keyframes pulse { 0%, 100% { box-shadow: 0 0 0 0 rgba(212, 175, 55, 0.4); } 50% { box-shadow: 0 0 0 15px rgba(212, 175, 55, 0); } }

        /* HEART PARTICLES */
        .heart-particle { position: fixed; font-size: 1.5rem; pointer-events: none; z-index: 999; animation: heartFloat 3s ease-out forwards; }
        @keyframes heartFloat { 0% { opacity: 1; transform: translateY(0) scale(1); } 100% { opacity: 0; transform: translateY(-200px) scale(1.5); } }

        /* SCROLL REVEAL */
        .reveal { opacity: 0; transform: translateY(40px); transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1); }
        .reveal.visible { opacity: 1; transform: translateY(0); }

        /* INFINITY */
        .infinity { font-size: clamp(2rem, 6vw, 3rem); color: var(--subtle-gold); text-shadow: 0 0 30px var(--gold-glow); display: inline-block; animation: gentlePulse 3s ease infinite; }
        @keyframes gentlePulse { 0%, 100% { opacity: 0.7; transform: scale(1); } 50% { opacity: 1; transform: scale(1.1); } }

        /* BEATING HEART */
        .beating-heart { display: inline-block; font-size: 1.5rem; animation: heartbeat 1.5s ease infinite; }
        @keyframes heartbeat { 0%, 100% { transform: scale(1); } 14% { transform: scale(1.3); } 28% { transform: scale(1); } 42% { transform: scale(1.3); } 70% { transform: scale(1); } }

        /* REDUCED MOTION */
        @media (prefers-reduced-motion: reduce) {
            *, *::before, *::after { animation-duration: 0.01ms !important; animation-iteration-count: 1 !important; transition-duration: 0.01ms !important; }
        }

        /* SCROLLBAR */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: var(--midnight); }
        ::-webkit-scrollbar-thumb { background: var(--deep-burgundy); border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: var(--dark-wine); }
    </style>
</head>
<body>
    <canvas id="particle-canvas"></canvas>

    <!-- SCENE 01 -->
    <div id="scene-01" class="scene active">
        <div class="star-field" id="star-field"></div>
        <div style="position: relative; z-index: 2; text-align: center;">
            <h1 class="title-main" style="animation-delay: 2s;">شهووود... ❤️</h1>
            <p class="title-sub" style="animation-delay: 4s;">في حاجة صغيرة عملتها مخصوص عشانك...</p>
            <p class="text-body" style="animation-delay: 6s;">بس أوعديني تكملي للآخر.</p>
            <button class="btn-glow" id="start-btn" style="animation-delay: 8s;" onclick="startJourney()">أبدأ المفاجأة ✨</button>
        </div>
    </div>

    <!-- MAIN CONTENT -->
    <main id="main-content" style="display: none;">
        <!-- SCENE 02 -->
        <section class="scene" id="scene-02">
            <div class="photo-reveal" id="photo-reveal-1">
                <img src="photos/nonty-01.jpeg" alt="نونتي" id="img-01" onerror="this.src='data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 width=%22400%22 height=%22533%22><rect fill=%22%232d0a0a%22 width=%22400%22 height=%22533%22/><text fill=%22%23c9a0a0%22 font-family=%22Tajawal%22 x=%2250%%22 y=%2250%%22 text-anchor=%22middle%22 font-size=%2220%22>بحبك وهفضل احبك مهما حصل يا غلسه </text></svg>'">
            </div>
            <h2 class="title-sub reveal" style="margin-top: 2rem;">عارفة إيه أكتر حاجة حلوة حصلتلي؟</h2>
            <p class="text-body reveal">إني عرفتك يا اللي محليه ايامي . ❤️</p>
            <p class="text-body reveal" style="animation-delay: 0.3s;">ومن يوم <span class="text-glow">20/04/2026</span>... الحكاية بدأت.</p>
        </section>

        <!-- SCENE 03 -->
        <section class="scene" id="scene-03">
            <h2 class="title-main reveal">20 ابريل 2026</h2>
            <p class="title-sub reveal">اليوم اللي بدأت فيه حكايتنا.</p>
            <div class="counter-container reveal">
                <div class="counter-box"><div class="counter-number" id="counter-days">0</div><div class="counter-label">يوم</div></div>
                <div class="counter-box"><div class="counter-number" id="counter-hours">0</div><div class="counter-label">ساعة</div></div>
                <div class="counter-box"><div class="counter-number" id="counter-minutes">0</div><div class="counter-label">دقيقة</div></div>
                <div class="counter-box"><div class="counter-number" id="counter-seconds">0</div><div class="counter-label">ثانية</div></div>
            </div>
            <p class="text-body reveal" style="margin-top: 2rem;">بقالنا...</p>
            <p class="text-body reveal" style="animation-delay: 0.2s;">وكل ثانية منهم ليها حكاية كل موقف مرينا بيه واتحطينا فيه . ❤️</p>
        </section>

        <!-- SCENE 04 -->
        <section class="scene" id="scene-04">
            <h2 class="title-main reveal">حكايتنا الصغيرة 🤍</h2>
            <div class="timeline">
                <div class="timeline-card reveal"><div class="timeline-date">14/06/2026</div><div class="timeline-text">اليوم اللي اتعرفت فيه على شهودتي...</div></div>
                <div class="timeline-card reveal"><div class="timeline-date">✨</div><div class="timeline-text">ومن هنا بدأت تفاصيل صغيرة تكبر جوايا.</div></div>
                <div class="timeline-card reveal"><div class="timeline-date">🤍</div><div class="timeline-text">ضحكة، كلام، تفاصيل...</div></div>
                <div class="timeline-card reveal"><div class="timeline-date">❤️</div><div class="timeline-text">وحاجات يمكن بسيطة بالنسبة للعالم، بس بالنسبالي كبيرة.</div></div>
                <div class="timeline-card reveal"><div class="timeline-date">والأجمل؟</div><div class="timeline-text">إن الحكاية لسه في أولها. ❤️</div></div>
            </div>
        </section>

        <!-- SCENE 05 -->
        <section class="scene" id="scene-05">
            <h2 class="title-main reveal">ربنا يخليكي ليا وميحرمنيش منك ابدا ❤️</h2>
            <div class="gallery-container" id="gallery"></div>
        </section>

        <!-- SCENE 06 -->
        <section class="scene" id="scene-06">
            <h2 class="title-main reveal">شهودتي... عندي سؤال مهم جدًا 👀</h2>
            <p class="title-sub reveal">لو رجعنا لأول يوم اتعرفنا فيه...</p>
            <p class="text-body reveal" style="font-size: clamp(1.2rem, 4vw, 1.8rem); font-weight: 700; color: var(--warm-white);">هتختاري حمدي تاني؟ ❤️</p>
            <div class="question-buttons reveal">
                <button class="btn-glow btn-yes" id="btn-yes" onclick="handleYes()" style="animation: fadeInUp 1s ease 0.5s forwards;">آه طبعًا ❤️</button>
                <button class="btn-glow btn-escape" id="btn-escape" onmouseover="moveButton()" ontouchstart="moveButton()" style="animation: fadeInUp 1s ease 0.7s forwards;">مش عارفة 😏</button>
            </div>
            <div id="yes-response" style="display: none; text-align: center; margin-top: 2rem;">
                <p class="title-sub" style="font-size: 1.5rem;">كنت عارف يا حبيبتي 😂❤️</p>
                <p class="text-body">أصل أنا كنت هختارك برضه.</p>
            </div>
        </section>

        <!-- SCENE 07 -->
        <section class="scene" id="scene-07">
            <p class="title-sub reveal">بس في حاجة أهم...</p>
            <p class="text-body reveal">في كلام مش عايز أقوله بسرعة.</p>
            <div class="envelope-container reveal" onclick="openLetter()">
                <div class="envelope" id="envelope">
                    <div class="envelope-front"></div>
                    <div class="envelope-back"></div>
                </div>
            </div>
            <button class="btn-glow reveal" onclick="openLetter()" style="margin-top: 1rem;">افتحي جواب حمدي 💌</button>
        </section>

        <!-- SCENE 08 -->
        <section class="scene" id="scene-08">
            <h2 class="title-main reveal">خلصت المفاجأة؟</h2>
            <p class="title-sub reveal" style="animation-delay: 1s;">لا يا شهودتي ... 😂</p>
            <p class="text-body reveal" style="animation-delay: 2s;">لسه في آخر حاجة.</p>
            <p class="text-body reveal" style="animation-delay: 3s;">لو وصلتي لهنا...</p>
            <button class="btn-glow reveal" style="animation-delay: 4s;" onclick="showFinal()">اضغطي هنا ❤️</button>
        </section>

        <!-- FINAL SCREEN -->
        <section class="scene" id="final-screen">
            <p class="text-body reveal">دي مش نهاية الحكاية...</p>
            <p class="title-sub reveal" style="animation-delay: 0.5s;">دي أول صفحة بس. 🤍</p>
            <div style="margin-top: 2rem; opacity: 0; animation: fadeInUp 1.5s ease 1s forwards;"><span class="beating-heart">❤️</span></div>
            <div style="margin-top: 3rem; padding: 2rem; text-align: center; opacity: 0; animation: fadeInUp 1.5s ease 1.5s forwards;">
                <p style="color: var(--subtle-gold); font-size: 0.9rem; letter-spacing: 2px;">حمدي ❤️ شهد</p>
                <p style="color: var(--soft-rose); font-size: 0.8rem; margin-top: 0.5rem;">From Hamdy, to shahad— with love. ❤️</p>
            </div>
        </section>
    </main>

    <!-- SCENE 09 — FINAL REVEAL -->
    <div class="final-reveal" id="final-reveal">
        <div class="final-photo" id="final-photo">
            <img src="" alt="نونتي" id="img-final" onerror="this.src='data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 width=%22400%22 height=%22533%22><rect fill=%22%232d0a0a%22 width=%22400%22 height=%22533%22/><text fill=%22%23c9a0a0%22 font-family=%22Tajawal%22 x=%2250%%22 y=%2250%%22 text-anchor=%22middle%22 font-size=%2220%22>ضع صورة نونتي هنا</text></svg>'">
        </div>
        <div class="final-text">
            <p class="title-sub">لو كان عندي أمنية واحدة...</p>
            <p class="title-main" style="font-size: clamp(1.3rem, 5vw, 2.5rem); margin-top: 1rem;">كنت هختار إن كل لحظة حلوة جاية...</p>
            <p class="title-main" style="font-size: clamp(1.5rem, 6vw, 3rem); color: var(--subtle-gold); margin-top: 1rem;">تكون وإنتِ فيها. ❤️</p>
            <p class="text-body" style="margin-top: 2rem; font-size: 1.5rem; color: var(--warm-white);">بحبك يا شهد ومش هعرف احب حد زيك .</p>
            <p class="text-body" style="margin-top: 1rem; color: var(--subtle-gold); font-weight: 700;">— حمدي ❤️</p>
            <p style="margin-top: 2rem; font-size: 1.2rem; color: var(--soft-rose);">20/04/2026 <span class="infinity">→ ∞</span></p>
        </div>
        <button class="btn-glow" style="margin-top: 2rem;" onclick="closeFinal()">استكملي الرحلة 🤍</button>
    </div>

    <!-- LETTER -->
    <div class="letter-overlay" id="letter-overlay" onclick="closeLetter()"></div>
    <div class="letter" id="letter">
        <div class="letter-content">حبيبتي 

مش عارف أبدأ منين،
بس يمكن أحسن بداية هي اليوم اللي اتعرفنا فيه...

20/04/2026.

يمكن بالنسبة لأي حد تاني مجرد تاريخ،
بس بالنسبالي هو اليوم اللي دخلت فيه واحدة من أجمل التفاصيل لحياتي.

يا شهد،
يمكن مش دايمًا بعرف أقول كل اللي جوايا،
وممكن ساعات كلامي مايبقاش كفاية،
بس الحقيقة إن وجودك بيفرق معايا أكتر مما تتخيلي.

بحب تفاصيلك،
ضحكتك،
كلامك،
عينك اللي احلي من الالماظ 
وحتى الحاجات الصغيرة اللي يمكن إنتِ مش واخدة بالك منها.


وعملتلك الموقع ده عشان أقولك بطريقة مختلفة ومحدش يكون عملها قبل كدا عشان احنا دايما بنعمل الكريتيف حتا في حبنا فاكره لما قولتلك هقول لطنط وقولتي اعمل حاجه جديده اهو اديني بعبرلك عن حبي بحاجه محدش عملها قبل كدا:

إنتِ مش مجرد صورة حلوة عندي،
ولا مجرد اسم على موبايلي.

إنتِ حكاية بدأت يوم 20/04/2026،
ونفسي أشوف لها فصول كتير جاية.

من حمدي...

إلى اغلي الناس علي قلبي شهد . ❤️</div>
        <div class="letter-signature">— شهد ❤️</div>
    </div>

    <!-- LIGHTBOX -->
    <div class="lightbox" id="lightbox">
        <button class="lightbox-close" onclick="closeLightbox()">✕</button>
        <button class="lightbox-nav lightbox-prev" onclick="prevImage()">‹</button>
        <img class="lightbox-img" id="lightbox-img" src="" alt="نونتي">
        <button class="lightbox-nav lightbox-next" onclick="nextImage()">›</button>
        <div class="lightbox-caption" id="lightbox-caption"></div>
    </div>

    <!-- MUSIC -->
    <button class="music-btn" id="music-btn" onclick="toggleMusic()" title="تشغيل الموسيقى">🎵</button>
    <audio id="bg-music" loop><source src="music.mp3" type="audio/mpeg"></audio>

    <script>
        /* ═══════════════════════════════════════════════════════════════
           PHOTO CONFIGURATION
           ═══════════════════════════════════════════════════════════════ */
        const PHOTOS = [
          { src: 'photos/nonty-01.jpeg', caption: 'نونتي... ❤️' },
        ];
        const BEST_PHOTO = 'photos/nonty-01.jpeg';

        /* STATE */
        let currentScene = 1, lightboxIndex = 0, musicPlaying = false, escapeAttempts = 0, counterInterval;

        /* PARTICLE SYSTEM */
        const canvas = document.getElementById('particle-canvas');
        const ctx = canvas.getContext('2d');
        let particles = [], stars = [];

        function resizeCanvas() { canvas.width = window.innerWidth; canvas.height = window.innerHeight; }
        resizeCanvas();
        window.addEventListener('resize', resizeCanvas);

        class Particle {
            constructor() { this.reset(); }
            reset() {
                this.x = Math.random() * canvas.width; this.y = Math.random() * canvas.height;
                this.size = Math.random() * 2 + 0.5;
                this.speedX = (Math.random() - 0.5) * 0.3; this.speedY = (Math.random() - 0.5) * 0.3;
                this.opacity = Math.random() * 0.5 + 0.1;
                this.color = Math.random() > 0.7 ? '212, 175, 55' : '201, 160, 160';
            }
            update() {
                this.x += this.speedX; this.y += this.speedY;
                if (this.x < 0 || this.x > canvas.width || this.y < 0 || this.y > canvas.height) this.reset();
            }
            draw() { ctx.beginPath(); ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2); ctx.fillStyle = `rgba(${this.color}, ${this.opacity})`; ctx.fill(); }
        }

        class Star {
            constructor() {
                this.x = Math.random() * canvas.width; this.y = Math.random() * canvas.height;
                this.size = Math.random() * 1.5 + 0.5; this.opacity = Math.random();
                this.twinkleSpeed = Math.random() * 0.02 + 0.005;
            }
            update() {
                this.opacity += this.twinkleSpeed;
                if (this.opacity > 1 || this.opacity < 0.2) this.twinkleSpeed = -this.twinkleSpeed;
            }
            draw() { ctx.beginPath(); ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2); ctx.fillStyle = `rgba(255, 255, 255, ${this.opacity})`; ctx.fill(); }
        }

        for (let i = 0; i < 50; i++) particles.push(new Particle());
        for (let i = 0; i < 100; i++) stars.push(new Star());

        function animateParticles() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            stars.forEach(s => { s.update(); s.draw(); });
            particles.forEach(p => { p.update(); p.draw(); });
            requestAnimationFrame(animateParticles);
        }
        animateParticles();

        /* STAR FIELD */
        function generateStarField() {
            const container = document.getElementById('star-field');
            for (let i = 0; i < 80; i++) {
                const star = document.createElement('div'); star.className = 'star';
                star.style.left = `${Math.random() * 100}%`; star.style.top = `${Math.random() * 100}%`;
                star.style.setProperty('--duration', `${Math.random() * 3 + 2}s`);
                star.style.setProperty('--delay', `${Math.random() * 5}s`);
                star.style.setProperty('--max-opacity', `${Math.random() * 0.8 + 0.2}`);
                container.appendChild(star);
            }
            for (let i = 0; i < 20; i++) {
                const p = document.createElement('div'); p.className = 'glow-particle';
                p.style.left = `${Math.random() * 100}%`;
                p.style.setProperty('--delay', `${Math.random() * 10}s`);
                container.appendChild(p);
            }
        }
        generateStarField();

        /* START JOURNEY */
        function startJourney() {
            const scene01 = document.getElementById('scene-01');
            const mainContent = document.getElementById('main-content');
            scene01.classList.add('fade-out');
            setTimeout(() => {
                scene01.style.display = 'none';
                mainContent.style.display = 'block';
                document.getElementById('img-01').src = PHOTOS[0].src;
                initGallery();
                document.getElementById('img-final').src = BEST_PHOTO;
                activateScene('scene-02');
                startCounter();
                setupScrollReveals();
            }, 1500);
        }

        function activateScene(id) {
            const scene = document.getElementById(id);
            if (scene) scene.classList.add('active');
        }

        /* COUNTER */
        function startCounter() {
            const startDate = new Date('2026-06-14T00:00:00');
            function update() {
                const now = new Date(), diff = now - startDate;
                document.getElementById('counter-days').textContent = Math.floor(diff / (1000 * 60 * 60 * 24));
                document.getElementById('counter-hours').textContent = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                document.getElementById('counter-minutes').textContent = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
                document.getElementById('counter-seconds').textContent = Math.floor((diff % (1000 * 60)) / 1000);
            }
            update();
            counterInterval = setInterval(update, 1000);
        }

        /* SCROLL REVEALS */
        function setupScrollReveals() {
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('visible');
                        const scene = entry.target.closest('.scene');
                        if (scene && !scene.classList.contains('active')) scene.classList.add('active');
                    }
                });
            }, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });
            document.querySelectorAll('.reveal, .timeline-card, .gallery-item').forEach(el => observer.observe(el));
        }

        /* GALLERY */
        function initGallery() {
            const gallery = document.getElementById('gallery');
            const styles = ['', 'polaroid'];
            const rotations = [-2, 1, -1, 2, 0, 1.5, -1.5];
            PHOTOS.forEach((photo, index) => {
                const item = document.createElement('div');
                item.className = `gallery-item reveal ${styles[index % styles.length]}`;
                item.style.setProperty('--rotation', `${rotations[index % rotations.length]}deg`);
                item.style.animationDelay = `${index * 0.15}s`;
                item.onclick = () => openLightbox(index);
                item.innerHTML = `<img src="${photo.src}" alt="نونتي" loading="lazy" onerror="this.parentElement.style.display='none'"><div class="gallery-caption">${photo.caption}</div>`;
                gallery.appendChild(item);
            });
        }

        /* LIGHTBOX */
        function openLightbox(index) { lightboxIndex = index; updateLightbox(); document.getElementById('lightbox').classList.add('active'); document.body.style.overflow = 'hidden'; }
        function closeLightbox() { document.getElementById('lightbox').classList.remove('active'); document.body.style.overflow = ''; }
        function updateLightbox() { document.getElementById('lightbox-img').src = PHOTOS[lightboxIndex].src; document.getElementById('lightbox-caption').textContent = PHOTOS[lightboxIndex].caption; }
        function nextImage() { lightboxIndex = (lightboxIndex + 1) % PHOTOS.length; updateLightbox(); }
        function prevImage() { lightboxIndex = (lightboxIndex - 1 + PHOTOS.length) % PHOTOS.length; updateLightbox(); }
        document.addEventListener('keydown', (e) => {
            if (!document.getElementById('lightbox').classList.contains('active')) return;
            if (e.key === 'Escape') closeLightbox();
            if (e.key === 'ArrowRight') nextImage();
            if (e.key === 'ArrowLeft') prevImage();
        });

        /* PLAYFUL QUESTION */
        function moveButton() {
            const btn = document.getElementById('btn-escape');
            escapeAttempts++;
            if (escapeAttempts > 5) { btn.style.opacity = '0'; btn.style.pointerEvents = 'none'; return; }
            const rect = btn.getBoundingClientRect();
            const maxX = window.innerWidth - rect.width - 20;
            const maxY = window.innerHeight - rect.height - 20;
            btn.style.position = 'fixed';
            btn.style.left = `${Math.random() * maxX}px`;
            btn.style.top = `${Math.random() * maxY}px`;
            btn.style.zIndex = '100';
            btn.style.transition = 'all 0.4s cubic-bezier(0.4, 0, 0.2, 1)';
        }

        function handleYes() {
            document.getElementById('yes-response').style.display = 'block';
            document.getElementById('btn-yes').style.display = 'none';
            document.getElementById('btn-escape').style.display = 'none';
            for (let i = 0; i < 30; i++) setTimeout(() => createHeartParticle(), i * 50);
            createFireworks();
        }

        function createHeartParticle() {
            const heart = document.createElement('div'); heart.className = 'heart-particle';
            heart.textContent = ['❤️', '✨', '🤍', '💖'][Math.floor(Math.random() * 4)];
            heart.style.left = `${Math.random() * 100}vw`;
            heart.style.top = `${50 + Math.random() * 30}vh`;
            heart.style.fontSize = `${Math.random() * 1.5 + 1}rem`;
            document.body.appendChild(heart);
            setTimeout(() => heart.remove(), 3000);
        }

        function createFireworks() {
            for (let i = 0; i < 5; i++) {
                setTimeout(() => {
                    const x = Math.random() * window.innerWidth;
                    const y = Math.random() * window.innerHeight * 0.5;
                    for (let j = 0; j < 12; j++) {
                        const p = document.createElement('div');
                        p.style.cssText = `position:fixed;left:${x}px;top:${y}px;width:4px;height:4px;border-radius:50%;background:${['#d4af37','#c9a0a0','#f5e6d3'][Math.floor(Math.random()*3)]};pointer-events:none;z-index:999;box-shadow:0 0 10px currentColor;`;
                        document.body.appendChild(p);
                        const angle = (j / 12) * Math.PI * 2;
                        const velocity = 100 + Math.random() * 100;
                        let posX = x, posY = y, opacity = 1;
                        const vx = Math.cos(angle) * velocity, vy = Math.sin(angle) * velocity;
                        const animate = () => {
                            posX += vx * 0.02; posY += vy * 0.02 + 2; opacity -= 0.02;
                            p.style.left = `${posX}px`; p.style.top = `${posY}px`; p.style.opacity = opacity;
                            if (opacity > 0) requestAnimationFrame(animate); else p.remove();
                        };
                        requestAnimationFrame(animate);
                    }
                }, i * 300);
            }
        }

        /* LETTER */
        function openLetter() {
            document.getElementById('envelope').classList.add('open');
            setTimeout(() => {
                document.getElementById('letter-overlay').classList.add('active');
                document.getElementById('letter').classList.add('active');
            }, 400);
        }

        function closeLetter() {
            document.getElementById('letter').classList.remove('active');
            document.getElementById('letter-overlay').classList.remove('active');
            setTimeout(() => document.getElementById('envelope').classList.remove('open'), 300);
        }

        /* FINAL REVEAL */
        function showFinal() {
            document.getElementById('final-reveal').classList.add('active');
            document.body.style.overflow = 'hidden';
            for (let i = 0; i < 50; i++) setTimeout(() => createHeartParticle(), i * 80);
        }

        function closeFinal() {
            document.getElementById('final-reveal').classList.remove('active');
            document.body.style.overflow = '';
            setTimeout(() => {
                document.getElementById('final-screen').scrollIntoView({ behavior: 'smooth' });
            }, 500);
        }

        /* MUSIC */
        function toggleMusic() {
            const audio = document.getElementById('bg-music');
            const btn = document.getElementById('music-btn');
            if (musicPlaying) {
                audio.pause();
                btn.classList.remove('playing');
                btn.textContent = '🎵';
            } else {
                audio.play().catch(() => {});
                btn.classList.add('playing');
                btn.textContent = '⏸';
            }
            musicPlaying = !musicPlaying;
        }
    </script>
</body>
</html>'''

# Write to file
with open('/mnt/agents/output/index.html', 'w', encoding='utf-8') as f:
    f.write(html_code)

print(f"File written successfully: {len(html_code)} characters")
