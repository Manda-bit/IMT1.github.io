<!DOCTYPE html>
<html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Isaac Manda Tarigan</title>
<link href="https://fonts.googleapis.com/css2?family=Josefin+Sans:ital,wght@0,100;0,200;0,300;0,400;0,600;0,700;1,300;1,400&display=swap" rel="stylesheet">
<style>
  :root {
    --black: #080808;
    --deep: #0e0e0e;
    --surface: #141414;
    --card: #1a1a1a;
    --gold: #c9a84c;
    --gold-light: #e2c97e;
    --gold-dim: rgba(201,168,76,0.12);
    --white: #f0ece4;
    --muted: #787878;
    --border: rgba(201,168,76,0.2);
  }

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
  html { scroll-behavior: smooth; }

  body {
    background: var(--black);
    color: var(--white);
    font-family: 'Josefin Sans', sans-serif;
    font-weight: 300;
    overflow-x: hidden;
    cursor: none;
  }

  /* ─── CURSOR ─── */
  .cursor {
    width: 8px; height: 8px;
    background: var(--gold); border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9999;
    transition: transform 0.15s ease;
    transform: translate(-50%, -50%);
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1px solid rgba(201,168,76,0.5); border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9998;
    transition: all 0.3s ease;
    transform: translate(-50%, -50%);
  }

  /* ─── INTRO ─── */
  #intro {
    position: fixed; inset: 0;
    background: var(--black); z-index: 8000;
    display: flex; align-items: center; justify-content: center; flex-direction: column;
    gap: 10px;
    animation: introFade 0.9s ease 3s forwards;
  }
  @keyframes introFade { to { opacity: 0; pointer-events: none; } }

  .intro-item {
    overflow: hidden;
    text-align: center;
  }
  .intro-item span {
    display: block;
    animation: slideUpFade 0.65s cubic-bezier(0.16,1,0.3,1) both;
  }
  @keyframes slideUpFade {
    from { transform: translateY(20px); opacity: 0; }
    to   { transform: translateY(0);    opacity: 1; }
  }
  .intro-item:nth-child(1) span { animation-delay: 0.2s; }
  .intro-item:nth-child(2) span { animation-delay: 0.55s; }
  .intro-item:nth-child(3) span { animation-delay: 0.9s; }

  .intro-small {
    font-family: 'Josefin Sans', sans-serif;
    font-size: 0.65rem; letter-spacing: 0.7em;
    text-transform: uppercase; color: var(--gold); font-weight: 400;
  }
  .intro-medium {
    font-family: 'Josefin Sans', sans-serif;
    font-size: 0.65rem; letter-spacing: 0.55em;
    text-transform: uppercase; color: var(--muted); font-weight: 300;
  }
  .intro-big {
    font-family: 'Times New Roman', Times, serif;
    font-size: clamp(1.5rem, 4vw, 3rem);
    font-weight: 700; letter-spacing: 0.12em;
    text-transform: uppercase; color: var(--white);
  }
  @keyframes fadeIn { to { opacity: 1; } }

  /* ─── NAVBAR ─── */
  nav {
    position: fixed; top: 0; left: 0; right: 0;
    padding: 28px 60px;
    display: flex; justify-content: space-between; align-items: center;
    z-index: 1000; opacity: 0;
    animation: fadeIn 0.8s ease 3s forwards;
    transition: backdrop-filter 0.4s, background 0.4s;
  }
  nav.scrolled {
    background: rgba(8,8,8,0.92);
    backdrop-filter: blur(12px);
    border-bottom: 0.5px solid var(--border);
  }
  .nav-logo {
    font-family: 'Times New Roman', Times, serif;
    font-size: 1.2rem; letter-spacing: 0.2em;
    font-weight: 700;
    color: var(--white); text-decoration: none; text-transform: uppercase;
  }
  .nav-links { display: flex; gap: 44px; list-style: none; }
  .nav-links a {
    color: var(--muted); text-decoration: none;
    font-family: 'Josefin Sans', sans-serif;
    font-size: 0.72rem; letter-spacing: 0.4em; text-transform: uppercase;
    font-weight: 400;
    transition: color 0.3s;
  }
  .nav-links a:hover { color: var(--gold); }

  .nav-burger { display: none; flex-direction: column; gap: 5px; cursor: pointer; }
  .nav-burger span { width: 24px; height: 1px; background: var(--white); transition: 0.3s; display: block; }

  /* ─── HERO ─── */
  #hero {
    min-height: 100vh;
    display: flex; align-items: center; justify-content: center;
    flex-direction: column; text-align: center;
    padding: 140px 40px 120px;
    position: relative; overflow: hidden;
  }
  .hero-bg {
    position: absolute; inset: 0;
    background: radial-gradient(ellipse at 50% 55%, rgba(201,168,76,0.07) 0%, transparent 65%);
    pointer-events: none;
  }
  .hero-grain {
    position: absolute; inset: 0; opacity: 0.025;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
    background-size: 200px; pointer-events: none;
  }
  .hero-eyebrow {
    font-size: 0.66rem; letter-spacing: 0.55em;
    text-transform: uppercase; color: var(--gold);
    margin-bottom: 28px; opacity: 0;
    animation: fadeIn 0.6s ease 3.0s forwards;
  }
  #hero-name {
    font-family: 'Times New Roman', Times, serif;
    font-size: clamp(3rem, 9vw, 8rem);
    font-weight: 900; line-height: 1.05;
    letter-spacing: 0.06em; text-transform: uppercase;
    color: var(--white); position: relative; z-index: 1;
    opacity: 0;
    animation: heroReveal 1s cubic-bezier(0.16,1,0.3,1) 3.0s forwards;
  }
  #hero-name em { font-style: italic; font-weight: 400; color: var(--gold-light); letter-spacing: 0.04em; }

  @keyframes heroReveal {
    from { opacity: 0; transform: translateY(28px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .hero-origin {
    display: flex; align-items: center; gap: 12px;
    margin-top: 20px; opacity: 0;
    animation: fadeIn 0.6s ease 3.1s forwards;
    justify-content: center;
  }
  .hero-origin-line { width: 30px; height: 0.5px; background: var(--gold); }
  .hero-origin-text {
    font-size: 0.68rem; letter-spacing: 0.45em;
    text-transform: uppercase; color: var(--muted);
  }

  .hero-divider {
    width: 1px; height: 70px;
    background: linear-gradient(to bottom, var(--gold), transparent);
    margin: 44px auto 32px; opacity: 0;
    animation: fadeIn 0.6s ease 3.2s forwards;
  }
  .hero-subtitle {
    font-size: clamp(0.82rem, 2vw, 0.95rem);
    letter-spacing: 0.18em; color: var(--muted);
    text-transform: uppercase; max-width: 480px; line-height: 2.2;
    opacity: 0; animation: fadeIn 0.6s ease 3.3s forwards;
  }
  .hero-scroll-hint {
    position: absolute; bottom: 40px; left: 50%;
    transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center; gap: 10px;
    opacity: 0; animation: fadeIn 0.6s ease 3.5s forwards;
  }
  .scroll-label { font-size: 0.6rem; letter-spacing: 0.5em; color: var(--muted); text-transform: uppercase; }
  .scroll-line {
    width: 1px; height: 50px;
    background: linear-gradient(to bottom, var(--muted), transparent);
    animation: scrollPulse 2s ease-in-out infinite 4.5s;
  }
  @keyframes scrollPulse {
    0%,100% { opacity: 0.3; transform: scaleY(1); }
    50%      { opacity: 1; transform: scaleY(0.6); }
  }

  /* ─── ABOUT ─── */
  #about {
    display: flex; align-items: center;
    padding: 130px 10%; background: var(--deep); gap: 80px;
  }
  .about-num {
    font-family: 'Times New Roman', Times, serif;
    font-size: 7rem; color: var(--gold-dim);
    font-weight: 900; flex-shrink: 0; user-select: none;
  }
  .about-content { flex: 1; }

  .section-label {
    font-size: 0.63rem; letter-spacing: 0.6em;
    font-family: 'Josefin Sans', sans-serif;
    text-transform: uppercase; color: var(--gold); margin-bottom: 18px;
    font-weight: 400;
  }
  .section-heading {
    font-family: 'Times New Roman', Times, serif;
    font-size: clamp(2rem, 4vw, 3.2rem);
    font-weight: 700; line-height: 1.25; margin-bottom: 28px; color: var(--white);
    letter-spacing: 0.02em;
  }
  .section-heading em { font-style: italic; font-weight: 400; color: var(--gold-light); }

  .about-text {
    font-family: 'Josefin Sans', sans-serif;
    color: var(--muted); font-size: 0.9rem; line-height: 2.1; max-width: 560px;
    margin-bottom: 16px; font-weight: 300; letter-spacing: 0.04em;
  }
  .about-line { width: 40px; height: 1px; background: var(--gold); margin: 32px 0; }

  .info-grid {
    display: grid; grid-template-columns: 1fr 1fr; gap: 20px 48px; margin-top: 8px;
  }
  .info-item {}
  .info-label {
    font-size: 0.6rem; letter-spacing: 0.4em;
    text-transform: uppercase; color: var(--gold); margin-bottom: 6px;
  }
  .info-val {
    font-family: 'Times New Roman', Times, serif;
    font-size: 1.15rem; color: var(--white); font-weight: 600;
  }

  /* ─── MUSIC ─── */
  #music {
    padding: 130px 10%; background: var(--black);
  }
  .music-intro { max-width: 560px; margin-bottom: 70px; }
  .music-intro p { color: var(--muted); font-size: 0.93rem; line-height: 2; margin-top: 16px; }

  .instruments-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 2px;
  }
  .instrument-card {
    background: var(--surface);
    padding: 48px 28px 40px;
    text-align: center;
    position: relative; overflow: hidden;
    transition: background 0.4s;
    border: 0.5px solid transparent;
  }
  .instrument-card::before {
    content: '';
    position: absolute; bottom: 0; left: 0; right: 0;
    height: 1px;
    background: linear-gradient(to right, transparent, var(--gold), transparent);
    transform: scaleX(0);
    transition: transform 0.5s ease;
  }
  .instrument-card:hover { background: var(--card); border-color: var(--border); }
  .instrument-card:hover::before { transform: scaleX(1); }

  .instrument-img {
    font-size: 3.8rem; margin-bottom: 20px; display: block;
    filter: sepia(0.3) saturate(0.8);
    transition: transform 0.4s cubic-bezier(0.16,1,0.3,1), filter 0.4s;
  }
  .instrument-card:hover .instrument-img {
    transform: translateY(-6px) scale(1.08);
    filter: sepia(0) saturate(1.2);
  }
  .instrument-name {
    font-family: 'Times New Roman', Times, serif;
    font-size: 1.25rem; font-weight: 700; color: var(--white);
    letter-spacing: 0.08em; margin-bottom: 8px;
  }
  .instrument-note {
    font-family: 'Josefin Sans', sans-serif;
    font-size: 0.65rem; letter-spacing: 0.35em;
    color: var(--muted); text-transform: uppercase; font-weight: 300;
  }

  /* ─── PASSIONS ─── */
  #passions {
    padding: 130px 10%; background: var(--deep);
  }
  .passions-grid {
    display: grid; grid-template-columns: 1fr 1fr; gap: 2px; margin-top: 64px;
  }
  .passion-card {
    background: var(--surface); padding: 52px 44px;
    position: relative; overflow: hidden; transition: background 0.4s;
    min-height: 260px; display: flex; flex-direction: column; justify-content: flex-end;
  }
  .passion-card:hover { background: var(--card); }
  .passion-card:first-child { grid-row: span 2; }

  .passion-bg-num {
    font-family: 'Times New Roman', Times, serif;
    font-size: 6rem; color: rgba(201,168,76,0.07);
    position: absolute; top: 20px; right: 24px;
    font-weight: 300; line-height: 1; user-select: none;
  }
  .passion-icon {
    font-size: 1.5rem; margin-bottom: 20px; display: block;
  }
  .passion-tag {
    font-size: 0.6rem; letter-spacing: 0.45em;
    text-transform: uppercase; color: var(--gold); margin-bottom: 12px;
  }
  .passion-title {
    font-family: 'Times New Roman', Times, serif;
    font-size: 1.8rem; font-weight: 700; color: var(--white);
    margin-bottom: 14px; line-height: 1.3;
  }
  .passion-desc {
    font-family: 'Josefin Sans', sans-serif;
    font-size: 0.82rem; color: var(--muted); line-height: 2;
    font-weight: 300; letter-spacing: 0.03em;
  }

  /* ─── CONTACT ─── */
  #contact {
    padding: 160px 10%; background: var(--black);
    text-align: center; display: flex; align-items: center; justify-content: center;
    flex-direction: column; position: relative; overflow: hidden;
  }
  #contact::before {
    content: '';
    position: absolute; inset: 0;
    background: radial-gradient(ellipse at 50% 100%, rgba(201,168,76,0.055) 0%, transparent 60%);
    pointer-events: none;
  }
  .contact-pre {
    font-size: 0.63rem; letter-spacing: 0.55em;
    text-transform: uppercase; color: var(--gold); margin-bottom: 24px;
  }
  .contact-heading {
    font-family: 'Times New Roman', Times, serif;
    font-size: clamp(2.4rem, 7vw, 5.5rem);
    font-weight: 700; line-height: 1.1; margin-bottom: 20px;
  }
  .contact-heading em { font-style: italic; font-weight: 400; color: var(--gold-light); }
  .contact-sub {
    font-family: 'Josefin Sans', sans-serif;
    font-size: 0.85rem; color: var(--muted); line-height: 2;
    max-width: 420px; margin: 0 auto 48px;
    letter-spacing: 0.06em; font-weight: 300;
  }

  .socials {
    display: flex; gap: 0; list-style: none; margin-top: 56px;
    border: 0.5px solid var(--border);
  }
  .socials li { flex: 1; }
  .socials a {
    display: block; padding: 20px 40px;
    font-family: 'Josefin Sans', sans-serif;
    font-size: 0.68rem; letter-spacing: 0.5em;
    text-transform: uppercase; color: var(--muted);
    text-decoration: none; font-weight: 400;
    transition: color 0.3s, background 0.3s;
    border-right: 0.5px solid var(--border);
    text-align: center;
  }
  .socials li:last-child a { border-right: none; }
  .socials a:hover { color: var(--gold); background: var(--gold-dim); }

  .availability-badge {
    display: inline-flex; align-items: center; gap: 10px;
    border: 0.5px solid var(--border);
    padding: 12px 24px; margin-bottom: 52px;
    font-size: 0.68rem; letter-spacing: 0.3em; text-transform: uppercase; color: var(--muted);
  }
  .badge-dot {
    width: 6px; height: 6px; border-radius: 50%;
    background: #4caf89;
    box-shadow: 0 0 8px rgba(76,175,137,0.6);
    animation: pulse 2s ease-in-out infinite;
  }
  @keyframes pulse {
    0%,100% { opacity: 1; } 50% { opacity: 0.4; }
  }

  /* ─── FOOTER ─── */
  footer {
    padding: 28px 10%; border-top: 0.5px solid rgba(255,255,255,0.05);
    display: flex; justify-content: space-between; align-items: center;
    background: var(--black);
  }
  .footer-name {
    font-family: 'Times New Roman', Times, serif;
    font-size: 0.9rem; letter-spacing: 0.2em;
    font-weight: 700;
    color: var(--muted); text-transform: uppercase;
  }
  .footer-copy {
    font-size: 0.62rem; color: rgba(120,120,120,0.5); letter-spacing: 0.1em;
  }
  .footer-loc {
    font-size: 0.62rem; color: rgba(120,120,120,0.5);
    letter-spacing: 0.2em; text-transform: uppercase;
  }

  /* ─── SCROLL REVEAL ─── */
  .reveal {
    opacity: 0; transform: translateY(38px);
    transition: opacity 0.9s cubic-bezier(0.16,1,0.3,1), transform 0.9s cubic-bezier(0.16,1,0.3,1);
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }
  .reveal-delay-1 { transition-delay: 0.1s; }
  .reveal-delay-2 { transition-delay: 0.2s; }
  .reveal-delay-3 { transition-delay: 0.3s; }
  .reveal-delay-4 { transition-delay: 0.45s; }

  /* ─── MOBILE ─── */
  @media (max-width: 900px) {
    .instruments-grid { grid-template-columns: repeat(2, 1fr); }
    .passions-grid { grid-template-columns: 1fr; }
    .passion-card:first-child { grid-row: auto; }
  }
  @media (max-width: 768px) {
    nav { padding: 24px 28px; }
    .nav-links { display: none; }
    .nav-burger { display: flex; }
    #about { flex-direction: column; padding: 80px 7%; gap: 0; }
    .about-num { font-size: 5rem; margin-bottom: -20px; }
    .info-grid { grid-template-columns: 1fr; gap: 16px; }
    #music, #passions, #contact { padding: 80px 7%; }
    footer { flex-direction: column; gap: 12px; text-align: center; padding: 28px 7%; }
    .socials { flex-direction: column; }
    .socials a { border-right: none; border-bottom: 0.5px solid var(--border); }
    .socials li:last-child a { border-bottom: none; }
    .instruments-grid { grid-template-columns: repeat(2, 1fr); }
  }

  /* ─── MOBILE MENU ─── */
  .mobile-menu {
    position: fixed; inset: 0; background: var(--black); z-index: 900;
    display: flex; flex-direction: column; align-items: center; justify-content: center;
    gap: 36px; opacity: 0; pointer-events: none; transition: opacity 0.4s;
  }
  .mobile-menu.open { opacity: 1; pointer-events: all; }
  .mobile-menu a {
    font-family: 'Times New Roman', Times, serif;
    font-size: 2.5rem; color: var(--white); text-decoration: none;
    letter-spacing: 0.15em; text-transform: uppercase; transition: color 0.3s;
  }
  .mobile-menu a:hover { color: var(--gold); }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursor-ring"></div>

<!-- ─── INTRO ─── -->
<div id="intro">
  <div class="intro-item"><span class="intro-small">Welcome</span></div>
  <div class="intro-item"><span class="intro-medium">To</span></div>
  <div class="intro-item"><span class="intro-big">Isaac Manda Tarigan</span></div>
</div>

<!-- ─── NAV ─── -->
<nav id="navbar">
  <a href="#hero" class="nav-logo">IMT</a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#music">Music</a></li>
    <li><a href="#passions">Interests</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <div class="nav-burger" id="burger">
    <span></span><span></span><span></span>
  </div>
</nav>

<!-- ─── MOBILE MENU ─── -->
<div class="mobile-menu" id="mobile-menu">
  <a href="#about"    onclick="closeMobile()">About</a>
  <a href="#music"    onclick="closeMobile()">Music</a>
  <a href="#passions" onclick="closeMobile()">Interests</a>
  <a href="#contact"  onclick="closeMobile()">Contact</a>
</div>

<!-- ─── HERO ─── -->
<section id="hero">
  <div class="hero-bg"></div>
  <div class="hero-grain"></div>
  <p class="hero-eyebrow">Fresh Graduate · Curious Mind · Indonesia</p>
  <h1 id="hero-name">Isaac<br><em>Manda Tarigan</em></h1>
  <div class="hero-origin">
    <div class="hero-origin-line"></div>
    <span class="hero-origin-text">Young &nbsp;·&nbsp; Hungry to Learn &nbsp;·&nbsp; Ready for Everything</span>
    <div class="hero-origin-line"></div>
  </div>
  <div class="hero-divider"></div>
  <p class="hero-subtitle">Music &nbsp;·&nbsp; Code &nbsp;·&nbsp; Creativity</p>
  <div class="hero-scroll-hint">
    <span class="scroll-label">Scroll</span>
    <div class="scroll-line"></div>
  </div>
</section>

<!-- ─── ABOUT ─── -->
<section id="about">
  <div class="about-num">01</div>
  <div class="about-content">
    <p class="section-label reveal">Who I Am</p>
    <h2 class="section-heading reveal reveal-delay-1">Just a kid with<br><em>big curiosity</em></h2>
    <div class="about-line reveal reveal-delay-2"></div>
    <p class="about-text reveal reveal-delay-2">
      Hey there — I'm <strong style="color:var(--white);font-weight:600;">Isaac Manda Tarigan</strong>, a fresh SMA graduate from <strong style="color:var(--white);font-weight:600;">Indonesia</strong>. I'm young, thrilled, and completely open to what the world has to offer. I don't have a long résumé yet, but I bring something I believe matters more right now: a genuine <strong style="color:var(--gold-light);font-weight:600;">hunger to learn, grow, and explore</strong>.
    </p>
    <p class="about-text reveal reveal-delay-3">
      Whether it's picking up a new instrument, diving into <strong style="color:var(--white);font-weight:600;">code</strong>, or discovering how <strong style="color:var(--white);font-weight:600;">AI thinks</strong> — I'm the kind of person who can't help but want to understand how things work. Every day is a chance to <strong style="color:var(--gold-light);font-weight:600;">learn something new</strong>, and I wouldn't have it any other way.
    </p>
    <div class="about-line reveal reveal-delay-3"></div>
    <div class="info-grid reveal reveal-delay-4">
      <div class="info-item">
        <div class="info-label">Name</div>
        <div class="info-val">Isaac Manda Tarigan</div>
      </div>
      <div class="info-item">
        <div class="info-label">Nationality</div>
        <div class="info-val">Indonesian 🇮🇩</div>
      </div>
      <div class="info-item">
        <div class="info-label">Age</div>
        <div class="info-val">Young enough</div>
      </div>
      <div class="info-item">
        <div class="info-label">Education</div>
        <div class="info-val">SMA Graduate</div>
      </div>
    </div>
  </div>
</section>

<!-- ─── MUSIC ─── -->
<section id="music">
  <div class="music-intro">
    <p class="section-label reveal">Hobby — Music</p>
    <h2 class="section-heading reveal reveal-delay-1">The instruments<br><em>I play</em></h2>
    <p class="about-text reveal reveal-delay-2">
      Music is one of the ways I <strong style="color:var(--white);font-weight:600;">express myself</strong>. I play a few instruments — each one with its own voice, its own feel. From the smooth keys of a keyboard to the <strong style="color:var(--gold-light);font-weight:600;">soulful cry of a saxophone</strong>, music keeps me grounded.
    </p>
  </div>
  <div class="instruments-grid">
    <div class="instrument-card reveal reveal-delay-1">
      <span class="instrument-img">🎹</span>
      <div class="instrument-name">Keyboard</div>
      <div class="instrument-note">Keys &amp; Harmony</div>
    </div>
    <div class="instrument-card reveal reveal-delay-2">
      <span class="instrument-img">🎷</span>
      <div class="instrument-name">Saxophone</div>
      <div class="instrument-note">Wind &amp; Soul</div>
    </div>
    <div class="instrument-card reveal reveal-delay-3">
      <span class="instrument-img">🎸</span>
      <div class="instrument-name">Guitar</div>
      <div class="instrument-note">String &amp; Melody</div>
    </div>
    <div class="instrument-card reveal reveal-delay-4">
      <span class="instrument-img">🎸</span>
      <div class="instrument-name">Bass</div>
      <div class="instrument-note">Rhythm &amp; Groove</div>
    </div>
  </div>
</section>

<!-- ─── PASSIONS ─── -->
<section id="passions">
  <p class="section-label reveal">What Drives Me</p>
  <h2 class="section-heading reveal reveal-delay-1">My world of <em>interests</em></h2>
  <div class="passions-grid">

    <div class="passion-card reveal">
      <div class="passion-bg-num">01</div>
      <span class="passion-icon">✦</span>
      <p class="passion-tag">Lifelong Learning</p>
      <h3 class="passion-title">Always learning<br>something new</h3>
      <p class="passion-desc">I genuinely enjoy picking up new skills and knowledge — from reading about history to watching how a circuit board works. <strong style="color:var(--white);font-weight:500;">Curiosity is my compass</strong>, and I follow it wherever it leads. No subject is off-limits.</p>
    </div>

    <div class="passion-card reveal reveal-delay-1">
      <div class="passion-bg-num">02</div>
      <span class="passion-icon">⌨</span>
      <p class="passion-tag">Technology · Code</p>
      <h3 class="passion-title">Coding &amp; building things</h3>
      <p class="passion-desc">There's something magical about <strong style="color:var(--white);font-weight:500;">turning an idea into something that runs on a screen</strong>. I love exploring how code works and I'm actively building that skill set.</p>
    </div>

    <div class="passion-card reveal reveal-delay-2">
      <div class="passion-bg-num">03</div>
      <span class="passion-icon">◈</span>
      <p class="passion-tag">Artificial Intelligence</p>
      <h3 class="passion-title">Exploring the world of AI</h3>
      <p class="passion-desc">AI fascinates me — how machines learn, how they reason, and what they might become. I love diving deep into the tools and ideas shaping the next era of technology.</p>
    </div>

  </div>
</section>

<!-- ─── CONTACT ─── -->
<section id="contact">
  <p class="contact-pre reveal">Let's Connect</p>
  <h2 class="contact-heading reveal reveal-delay-1">Open to every<br><em>opportunity</em></h2>
  <p class="contact-sub reveal reveal-delay-2">
    I may be just starting out, but I'm ready to give everything I've got. If you'd like to connect, collaborate, or just say hello — I'd love to hear from you.
  </p>
  <div class="availability-badge reveal reveal-delay-3">
    <div class="badge-dot"></div>
    Available &amp; ready to learn
  </div>
  <ul class="socials reveal reveal-delay-4">
    <li><a href="https://instagram.com/" target="_blank">Instagram</a></li>
    <li><a href="https://linkedin.com/" target="_blank">LinkedIn</a></li>
  </ul>
</section>

<!-- ─── FOOTER ─── -->
<footer>
  <div class="footer-name">Isaac Manda Tarigan</div>
  <div class="footer-loc">Indonesia 🇮🇩</div>
  <div class="footer-copy">© 2025 — All rights reserved</div>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring   = document.getElementById('cursor-ring');
  document.addEventListener('mousemove', e => {
    cursor.style.left = e.clientX + 'px';
    cursor.style.top  = e.clientY + 'px';
    setTimeout(() => {
      ring.style.left = e.clientX + 'px';
      ring.style.top  = e.clientY + 'px';
    }, 80);
  });
  document.querySelectorAll('a, button').forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.style.transform = 'translate(-50%,-50%) scale(2.5)';
      ring.style.opacity = '0';
    });
    el.addEventListener('mouseleave', () => {
      cursor.style.transform = 'translate(-50%,-50%) scale(1)';
      ring.style.opacity = '1';
    });
  });

  // Navbar scroll effect
  const navbar = document.getElementById('navbar');
  window.addEventListener('scroll', () => {
    navbar.classList.toggle('scrolled', window.scrollY > 60);
  });

  // Mobile menu
  document.getElementById('burger').addEventListener('click', () => {
    document.getElementById('mobile-menu').classList.toggle('open');
  });
  function closeMobile() {
    document.getElementById('mobile-menu').classList.remove('open');
  }

  // Scroll reveal
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
  }, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });
  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

  // Parallax hero
  const heroName = document.getElementById('hero-name');
  window.addEventListener('scroll', () => {
    const y = window.scrollY;
    if (heroName) {
      heroName.style.transform = `translateY(${y * 0.16}px)`;
      heroName.style.opacity = Math.max(0, 1 - y / 480);
    }
  });

  // Remove intro overlay
  setTimeout(() => {
    const intro = document.getElementById('intro');
    if (intro) { intro.style.display = 'none'; }
  }, 3600);
</script>
</body>
</html>
