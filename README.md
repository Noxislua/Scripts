<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Comet Hub</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Space+Mono:wght@400;700&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
  :root {
    --bg:     #06060f;
    --white:  #f0f0ff;
    --sub:    rgba(180,175,230,0.5);
    --dim:    rgba(255,255,255,0.07);
    --border: rgba(255,255,255,0.08);
    --p1:     rgba(110,90,255,0.9);
    --p2:     rgba(60,170,255,0.85);
    --p3:     rgba(200,110,255,0.8);
  }

  * { margin:0; padding:0; box-sizing:border-box; }
  html { scroll-behavior:smooth; }

  body {
    background: var(--bg);
    color: var(--white);
    font-family: 'Inter', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ── ORBS ── */
  .orb {
    position: fixed;
    border-radius: 50%;
    pointer-events: none;
    z-index: 0;
    animation: drift 20s ease-in-out infinite alternate;
  }
  .orb1 { width:700px; height:700px; top:-300px; left:-250px;
    background: radial-gradient(circle, rgba(100,80,255,0.18) 0%, transparent 65%);
    filter: blur(80px); animation-delay:0s; }
  .orb2 { width:550px; height:550px; top:25%; right:-200px;
    background: radial-gradient(circle, rgba(40,155,255,0.14) 0%, transparent 65%);
    filter: blur(90px); animation-delay:-7s; }
  .orb3 { width:500px; height:500px; bottom:-150px; left:25%;
    background: radial-gradient(circle, rgba(190,80,255,0.12) 0%, transparent 65%);
    filter: blur(100px); animation-delay:-14s; }

  @keyframes drift {
    0%   { transform: translate(0,0) scale(1); }
    40%  { transform: translate(25px,-18px) scale(1.04); }
    100% { transform: translate(-15px,22px) scale(0.97); }
  }

  /* ── GRID ── */
  body::before {
    content:'';
    position:fixed; inset:0;
    background-image:
      linear-gradient(rgba(110,90,255,0.035) 1px, transparent 1px),
      linear-gradient(90deg, rgba(110,90,255,0.035) 1px, transparent 1px);
    background-size:50px 50px;
    pointer-events:none; z-index:0;
  }

  /* ── LAYOUT ── */
  .container {
    max-width: 800px;
    margin: 0 auto;
    padding: 0 24px;
    position: relative;
    z-index: 1;
  }

  /* ════════════════════════════
     LIQUID GLASS BASE
  ════════════════════════════ */
  .lg {
    background: linear-gradient(
      145deg,
      rgba(255,255,255,0.075) 0%,
      rgba(255,255,255,0.025) 50%,
      rgba(255,255,255,0.055) 100%
    );
    backdrop-filter: blur(28px) saturate(180%) brightness(1.06);
    -webkit-backdrop-filter: blur(28px) saturate(180%) brightness(1.06);
    border: 1px solid rgba(255,255,255,0.1);
    box-shadow:
      inset 0 1.5px 0 rgba(255,255,255,0.14),
      inset 0 -1px 0 rgba(255,255,255,0.04),
      inset 1px 0 0 rgba(255,255,255,0.05),
      0 8px 40px rgba(0,0,0,0.45),
      0 2px 8px rgba(0,0,0,0.25);
  }

  /* ── HEADER ── */
  header {
    padding: 80px 0 64px;
    border-bottom: 1px solid rgba(255,255,255,0.06);
    margin-bottom: 60px;
  }

  .badge {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    color: rgba(170,155,255,0.9);
    background: rgba(100,80,255,0.1);
    border: 1px solid rgba(110,90,255,0.28);
    padding: 5px 14px;
    border-radius: 100px;
    display: inline-flex;
    align-items: center;
    gap: 8px;
    margin-bottom: 26px;
    box-shadow: 0 0 24px rgba(110,90,255,0.18), inset 0 1px 0 rgba(255,255,255,0.1);
    animation: fadeUp 0.4s ease both;
  }
  .badge::before {
    content:'';
    width:5px; height:5px;
    border-radius:50%;
    background: rgba(150,135,255,1);
    box-shadow: 0 0 10px rgba(150,135,255,1), 0 0 20px rgba(150,135,255,0.5);
    animation: ping 2s infinite;
  }
  @keyframes ping {
    0%,100% { opacity:1; box-shadow: 0 0 10px rgba(150,135,255,1), 0 0 20px rgba(150,135,255,0.5); }
    50%      { opacity:0.3; box-shadow: 0 0 4px rgba(150,135,255,0.3); }
  }

  .logo {
    font-family: 'Syne', sans-serif;
    font-size: clamp(52px, 10vw, 90px);
    font-weight: 800;
    letter-spacing: -0.03em;
    line-height: 1;
    margin-bottom: 20px;
    background: linear-gradient(130deg, #ffffff 0%, rgba(190,175,255,0.92) 45%, rgba(105,185,255,0.85) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    filter: drop-shadow(0 0 50px rgba(110,90,255,0.55)) drop-shadow(0 0 100px rgba(110,90,255,0.2));
    animation: fadeUp 0.5s ease 0.05s both;
  }

  .tagline {
    font-size: 15px;
    color: var(--sub);
    max-width: 460px;
    line-height: 1.75;
    margin-bottom: 28px;
    animation: fadeUp 0.5s ease 0.12s both;
  }

  .meta-row {
    display: flex; gap: 8px; flex-wrap: wrap;
    animation: fadeUp 0.5s ease 0.18s both;
  }
  .meta-pill {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.06em;
    color: rgba(200,195,255,0.6);
    padding: 5px 12px;
    border-radius: 8px;
    background: rgba(255,255,255,0.04);
    border: 1px solid rgba(255,255,255,0.07);
    box-shadow: inset 0 1px 0 rgba(255,255,255,0.08);
  }
  .meta-pill strong { color: rgba(210,200,255,0.95); }

  @keyframes fadeUp {
    from { opacity:0; transform:translateY(14px); }
    to   { opacity:1; transform:translateY(0); }
  }

  /* ── SECTION ── */
  .section { margin-bottom: 56px; }
  .sec-hdr {
    display:flex; align-items:center; gap:12px;
    margin-bottom: 18px;
  }
  .sec-title {
    font-family: 'Space Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    color: rgba(160,145,255,0.45);
    white-space: nowrap;
  }
  .sec-line {
    flex:1; height:1px;
    background: linear-gradient(90deg, rgba(110,90,255,0.22), transparent);
  }

  /* ── GAME CARDS ── */
  .game-card {
    border-radius: 16px;
    overflow: hidden;
    margin-bottom: 10px;
    position: relative;
    transition: box-shadow 0.3s, transform 0.25s;
    animation: fadeUp 0.5s ease both;
    /* liquid glass */
    background: linear-gradient(
      148deg,
      rgba(255,255,255,0.08) 0%,
      rgba(255,255,255,0.025) 55%,
      rgba(255,255,255,0.06) 100%
    );
    backdrop-filter: blur(24px) saturate(170%) brightness(1.05);
    -webkit-backdrop-filter: blur(24px) saturate(170%) brightness(1.05);
    border: 1px solid rgba(255,255,255,0.09);
    box-shadow:
      inset 0 1.5px 0 rgba(255,255,255,0.13),
      inset 0 -1px 0 rgba(255,255,255,0.03),
      0 4px 30px rgba(0,0,0,0.35);
  }
  .game-card:nth-child(1){ animation-delay:0.08s; }
  .game-card:nth-child(2){ animation-delay:0.16s; }
  .game-card:nth-child(3){ animation-delay:0.24s; }

  .game-card:hover {
    transform: translateY(-2px);
    box-shadow:
      inset 0 1.5px 0 rgba(255,255,255,0.16),
      0 0 0 1px rgba(110,90,255,0.3),
      0 0 50px rgba(90,70,220,0.22),
      0 0 100px rgba(90,70,220,0.1),
      0 8px 40px rgba(0,0,0,0.4);
  }

  /* Glint top */
  .game-card::before {
    content:'';
    position:absolute; top:0; left:10%; right:10%; height:1px;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
    pointer-events:none;
  }

  .game-hdr {
    display:flex; align-items:center; justify-content:space-between;
    padding: 18px 22px;
    cursor: pointer;
    user-select: none;
  }

  .game-left { display:flex; align-items:center; gap:12px; }

  .game-ver {
    font-family: 'Space Mono', monospace;
    font-size: 9px;
    color: rgba(160,145,255,0.8);
    background: rgba(100,80,255,0.12);
    border: 1px solid rgba(110,90,255,0.25);
    padding: 3px 10px;
    border-radius: 100px;
    letter-spacing: 0.05em;
    box-shadow: 0 0 10px rgba(110,90,255,0.15);
  }

  .game-name {
    font-family: 'Syne', sans-serif;
    font-size: 17px;
    font-weight: 700;
    background: linear-gradient(90deg, #fff, rgba(200,190,255,0.85));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .game-count {
    font-family: 'Space Mono', monospace;
    font-size: 9px;
    color: rgba(180,170,255,0.35);
    letter-spacing: 0.1em;
  }

  .chev {
    width:24px; height:24px;
    border-radius:7px;
    display:flex; align-items:center; justify-content:center;
    font-size:11px;
    color: rgba(160,150,255,0.5);
    transition: all 0.25s;
    flex-shrink:0;
    background: rgba(255,255,255,0.04);
    border: 1px solid rgba(255,255,255,0.07);
  }
  .game-card.open .chev {
    background: rgba(100,80,255,0.18);
    border-color: rgba(110,90,255,0.35);
    color: rgba(190,175,255,1);
    transform: rotate(180deg);
    box-shadow: 0 0 14px rgba(110,90,255,0.4), inset 0 1px 0 rgba(255,255,255,0.12);
  }

  .game-body {
    display:none;
    padding: 0 22px 22px;
    border-top: 1px solid rgba(255,255,255,0.06);
  }
  .game-card.open .game-body { display:block; }

  .feat-group { padding-top: 18px; }

  .feat-lbl {
    font-family: 'Space Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.25em;
    color: rgba(150,135,255,0.38);
    text-transform: uppercase;
    margin-bottom: 11px;
  }

  .feat-grid {
    display:grid;
    grid-template-columns: repeat(auto-fill, minmax(185px,1fr));
    gap: 2px 6px;
  }

  .feat {
    font-size: 13px;
    color: rgba(195,190,235,0.42);
    padding: 5px 0;
    display:flex; align-items:center; gap:8px;
    transition: color 0.15s;
  }
  .feat:hover { color: rgba(225,220,255,0.9); }
  .feat::before {
    content:'';
    width:3px; height:3px;
    border-radius:50%;
    background: rgba(110,90,255,0.45);
    flex-shrink:0;
    box-shadow: 0 0 5px rgba(110,90,255,0.35);
    transition: all 0.15s;
  }
  .feat:hover::before {
    background: rgba(170,155,255,1);
    box-shadow: 0 0 10px rgba(170,155,255,0.8), 0 0 20px rgba(170,155,255,0.3);
  }

  /* ── INFO GRID ── */
  .info-grid {
    display:grid;
    grid-template-columns: repeat(2,1fr);
    gap:10px;
    margin-bottom:56px;
  }
  @media(max-width:520px){ .info-grid{ grid-template-columns:1fr; } }

  .info-card {
    border-radius: 14px;
    padding: 20px 22px;
    position: relative;
    overflow: hidden;
    transition: box-shadow 0.3s, transform 0.25s;
    background: linear-gradient(
      145deg,
      rgba(255,255,255,0.07) 0%,
      rgba(255,255,255,0.02) 100%
    );
    backdrop-filter: blur(22px) saturate(160%) brightness(1.04);
    -webkit-backdrop-filter: blur(22px) saturate(160%) brightness(1.04);
    border: 1px solid rgba(255,255,255,0.08);
    box-shadow:
      inset 0 1.5px 0 rgba(255,255,255,0.12),
      0 4px 24px rgba(0,0,0,0.3);
  }
  .info-card::before {
    content:'';
    position:absolute; top:0; left:10%; right:10%; height:1px;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.14), transparent);
  }
  .info-card:hover {
    transform: translateY(-2px);
    box-shadow:
      inset 0 1.5px 0 rgba(255,255,255,0.15),
      0 0 0 1px rgba(110,90,255,0.22),
      0 0 40px rgba(90,70,220,0.18),
      0 8px 32px rgba(0,0,0,0.35);
  }

  .info-icon { font-size:20px; margin-bottom:12px; display:block; }
  .info-card strong {
    display:block; font-size:13px; font-weight:600;
    color:rgba(225,218,255,0.95); margin-bottom:7px;
  }
  .info-card p { font-size:13px; color:var(--sub); line-height:1.65; }
  .info-card a { color:rgba(170,155,255,0.85); text-decoration:underline; text-underline-offset:3px; }

  /* ── LOADSTRINGS ── */
  .ls-lbl {
    font-family: 'Space Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.25em;
    text-transform: uppercase;
    color: rgba(155,140,255,0.4);
    margin-bottom: 8px;
  }

  .ls-wrap {
    border-radius: 14px;
    overflow: hidden;
    margin-bottom: 14px;
    position: relative;
    background: linear-gradient(
      160deg,
      rgba(18,15,38,0.88) 0%,
      rgba(8,8,18,0.92) 100%
    );
    backdrop-filter: blur(20px) saturate(140%);
    -webkit-backdrop-filter: blur(20px) saturate(140%);
    border: 1px solid rgba(255,255,255,0.08);
    box-shadow:
      inset 0 1.5px 0 rgba(255,255,255,0.07),
      0 4px 28px rgba(0,0,0,0.45);
    transition: box-shadow 0.3s;
  }
  .ls-wrap:hover {
    box-shadow:
      inset 0 1.5px 0 rgba(255,255,255,0.1),
      0 0 0 1px rgba(110,90,255,0.22),
      0 0 50px rgba(80,60,200,0.2),
      0 4px 28px rgba(0,0,0,0.5);
  }

  .ls-top {
    display:flex; align-items:center; justify-content:space-between;
    padding: 10px 16px;
    border-bottom: 1px solid rgba(255,255,255,0.05);
    background: rgba(255,255,255,0.025);
    position:relative;
  }
  .ls-top::after {
    content:'';
    position:absolute; bottom:0; left:0; right:0; height:1px;
    background: linear-gradient(90deg, transparent, rgba(110,90,255,0.18), transparent);
  }

  .dots { display:flex; gap:5px; }
  .dots span { width:9px; height:9px; border-radius:50%; }
  .dots span:nth-child(1){ background:#ff5f57; box-shadow:0 0 7px rgba(255,95,87,0.6); }
  .dots span:nth-child(2){ background:#febc2e; box-shadow:0 0 7px rgba(254,188,46,0.5); }
  .dots span:nth-child(3){ background:#28c840; box-shadow:0 0 7px rgba(40,200,64,0.6); }

  .file-lbl {
    font-family:'Space Mono',monospace;
    font-size:10px; color:var(--sub); letter-spacing:0.1em;
  }

  .copy-btn {
    background: rgba(100,80,255,0.1);
    border: 1px solid rgba(110,90,255,0.22);
    color: rgba(165,150,255,0.75);
    font-family:'Space Mono',monospace;
    font-size:9px; letter-spacing:0.15em; text-transform:uppercase;
    padding:4px 12px; border-radius:6px; cursor:pointer;
    transition:all 0.2s;
  }
  .copy-btn:hover {
    background:rgba(100,80,255,0.22);
    border-color:rgba(110,90,255,0.45);
    color:rgba(210,200,255,1);
    box-shadow:0 0 16px rgba(110,90,255,0.3);
  }
  .copy-btn.ok {
    background:rgba(40,200,64,0.1);
    border-color:rgba(40,200,64,0.32);
    color:rgba(80,225,110,0.95);
    box-shadow:0 0 12px rgba(40,200,64,0.25);
  }

  .code-body {
    padding:20px; font-family:'Space Mono',monospace;
    font-size:12px; line-height:1.9;
    overflow-x:auto; white-space:pre;
  }
  .kw  { color:rgba(200,190,255,0.82); }
  .fn  { color:rgba(130,200,255,0.88); }
  .str { color:rgba(130,220,140,0.72); }
  .pn  { color:rgba(255,255,255,0.18); }

  /* ── FOOTER ── */
  footer {
    border-top: 1px solid rgba(255,255,255,0.05);
    padding:28px 0 52px;
    display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:12px;
  }
  .foot-l {
    font-family:'Syne',sans-serif; font-size:14px; font-weight:700;
    background: linear-gradient(90deg,rgba(200,190,255,0.75),rgba(100,180,255,0.6));
    -webkit-background-clip:text; -webkit-text-fill-color:transparent; background-clip:text;
    filter: drop-shadow(0 0 20px rgba(110,90,255,0.4));
  }
  .foot-r {
    font-family:'Space Mono',monospace; font-size:9px;
    color:rgba(255,255,255,0.14); letter-spacing:0.15em; text-transform:uppercase;
  }
</style>
</head>
<body>

<div class="orb orb1"></div>
<div class="orb orb2"></div>
<div class="orb orb3"></div>

<div class="container">

  <header>
    <div class="badge">noxis.lua · Script Hub</div>
    <h1 class="logo">Comet Hub</h1>
    <p class="tagline">A lightweight, multi-game script collection. Clean UI. No key system. Compatible with all major executors.</p>
    <div class="meta-row">
      <div class="meta-pill">Version <strong>3.2</strong></div>
      <div class="meta-pill"><strong>3</strong> Games</div>
      <div class="meta-pill">Toggle <strong>F8</strong></div>
      <div class="meta-pill"><strong>Keyless</strong></div>
    </div>
  </header>

  <!-- GAMES -->
  <div class="section">
    <div class="sec-hdr">
      <span class="sec-title">Supported Games</span>
      <div class="sec-line"></div>
    </div>

    <div class="game-card" onclick="this.classList.toggle('open')">
      <div class="game-hdr">
        <div class="game-left">
          <span class="game-ver">v3.2</span>
          <span class="game-name">Be a Youtuber</span>
        </div>
        <div style="display:flex;align-items:center;gap:12px">
          <span class="game-count">21 features</span>
          <div class="chev">▾</div>
        </div>
      </div>
      <div class="game-body">
        <div class="feat-group">
          <div class="feat-lbl">Automation</div>
          <div class="feat-grid">
            <div class="feat">Auto Collect</div><div class="feat">Auto Upload</div>
            <div class="feat">Auto Claim</div><div class="feat">Auto Submit</div>
            <div class="feat">Auto Claim Quests</div><div class="feat">Smart Auto Rebirth</div>
            <div class="feat">Auto Upgrades</div><div class="feat">Auto Buy House</div>
            <div class="feat">Auto Buy Youtuber</div><div class="feat">Auto Bulk Hatch</div>
            <div class="feat">Sell All Youtubers</div><div class="feat">Redeem All Codes</div>
          </div>
        </div>
        <div class="feat-group">
          <div class="feat-lbl">Speed & Movement</div>
          <div class="feat-grid">
            <div class="feat">Walk Speed Presets</div><div class="feat">Jump Power Presets</div>
            <div class="feat">Custom Speed Input</div><div class="feat">Custom Jump Input</div>
          </div>
        </div>
        <div class="feat-group">
          <div class="feat-lbl">Floor Navigation</div>
          <div class="feat-grid">
            <div class="feat">Auto Floor Cycle</div><div class="feat">Fast Teleport 1–10</div>
            <div class="feat">Floor Status Display</div>
          </div>
        </div>
      </div>
    </div>

    <div class="game-card" onclick="this.classList.toggle('open')">
      <div class="game-hdr">
        <div class="game-left">
          <span class="game-ver">v3.0</span>
          <span class="game-name">Pls Donate</span>
        </div>
        <div style="display:flex;align-items:center;gap:12px">
          <span class="game-count">36 features</span>
          <div class="chev">▾</div>
        </div>
      </div>
      <div class="game-body">
        <div class="feat-group">
          <div class="feat-lbl">Booth</div>
          <div class="feat-grid">
            <div class="feat">Auto Update Booth Text</div><div class="feat">Custom Booth Text</div>
            <div class="feat">Text Color (Hex)</div><div class="feat">Robux Goal Offset</div>
            <div class="feat">Font Selector</div><div class="feat">Standing Position</div>
            <div class="feat">Tagged Booth Hop</div>
          </div>
        </div>
        <div class="feat-group">
          <div class="feat-lbl">Player Effects</div>
          <div class="feat-grid">
            <div class="feat">Spin on Donate</div><div class="feat">Spin Speed Multiplier</div>
            <div class="feat">Jump on Donate</div><div class="feat">Jump Power Boost</div>
            <div class="feat">Gravity Reduction</div><div class="feat">Helicopter Mode</div>
            <div class="feat">1R$ = 1 Map Lap</div><div class="feat">Dance Emote</div>
            <div class="feat">Anonymous Mode</div><div class="feat">FPS Boost</div>
          </div>
        </div>
        <div class="feat-group">
          <div class="feat-lbl">Server</div>
          <div class="feat-grid">
            <div class="feat">Auto Server Hop</div><div class="feat">Hop After Donation</div>
            <div class="feat">Goal Server Hop</div><div class="feat">VC Server Preference</div>
            <div class="feat">Friend Hop</div><div class="feat">Anti-Bot Detection</div>
          </div>
        </div>
        <div class="feat-group">
          <div class="feat-lbl">Chat & Auto Reply</div>
          <div class="feat-grid">
            <div class="feat">Auto Thanks</div><div class="feat">Auto Beg</div>
            <div class="feat">Auto Reply Nearby</div><div class="feat">Custom Reply Sets</div>
          </div>
        </div>
      </div>
    </div>

    <div class="game-card" onclick="this.classList.toggle('open')">
      <div class="game-hdr">
        <div class="game-left">
          <span class="game-ver">v1.7</span>
          <span class="game-name">Starving Arts</span>
        </div>
        <div style="display:flex;align-items:center;gap:12px">
          <span class="game-count">10 features</span>
          <div class="chev">▾</div>
        </div>
      </div>
      <div class="game-body">
        <div class="feat-group">
          <div class="feat-lbl">Drawing</div>
          <div class="feat-grid">
            <div class="feat">Web Image Import</div><div class="feat">Randomize / Step Mode</div>
            <div class="feat">17 Brush Styles</div><div class="feat">Brush Size 1–5</div>
            <div class="feat">Skip White Background</div><div class="feat">Cancel Drawing</div>
          </div>
        </div>
        <div class="feat-group">
          <div class="feat-lbl">Utilities</div>
          <div class="feat-grid">
            <div class="feat">Anti-AFK</div><div class="feat">Donation Webhook</div>
            <div class="feat">Webhook Test</div><div class="feat">Discord Copy Link</div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- INFO -->
  <div class="info-grid">
    <div class="info-card">
      <span class="info-icon">🔑</span>
      <strong>Keyless</strong>
      <p>No key system. No ads. Execute and go instantly.</p>
    </div>
    <div class="info-card">
      <span class="info-icon">🛠</span>
      <strong>Support</strong>
      <p>Join Discord : <a href="https://discord.com/invite/NkYSkdAkey" target="_blank">discord.gg/NkYSkdAkey</a></p>
    </div>
    <div class="info-card">
      <span class="info-icon">⚡</span>
      <strong>Executor Compatible</strong>
      <p>Works across low-UNC and high-UNC executors.</p>
    </div>
    <div class="info-card">
      <span class="info-icon">🗂</span>
      <strong>Hotkey</strong>
      <p>Press <strong style="color:rgba(200,185,255,0.95)">F8</strong> to toggle the UI at any time.</p>
    </div>
  </div>

  <!-- LOADSTRINGS -->
  <div class="section">
    <div class="sec-hdr">
      <span class="sec-title">Loadstrings</span>
      <div class="sec-line"></div>
    </div>

    <div class="ls-lbl">Be a Youtuber</div>
    <div class="ls-wrap">
      <div class="ls-top">
        <div class="dots"><span></span><span></span><span></span></div>
        <div class="file-lbl">youtuber.lua</div>
        <button class="copy-btn" onclick="copyCode(this,'ytc')">Copy</button>
      </div>
      <div class="code-body" id="ytc"><span class="fn">loadstring</span><span class="pn">(</span><span class="kw">game</span><span class="pn">:</span><span class="fn">HttpGet</span><span class="pn">(</span><span class="str">"https://raw.githubusercontent.com/Noxislua/Scripts/refs/heads/main/Be%20A%20Youtuber"</span><span class="pn">))()</span></div>
    </div>

    <div class="ls-lbl">Pls Donate</div>
    <div class="ls-wrap">
      <div class="ls-top">
        <div class="dots"><span></span><span></span><span></span></div>
        <div class="file-lbl">plsdonate.lua</div>
        <button class="copy-btn" onclick="copyCode(this,'pdc')">Copy</button>
      </div>
      <div class="code-body" id="pdc"><span class="fn">loadstring</span><span class="pn">(</span><span class="kw">game</span><span class="pn">:</span><span class="fn">HttpGet</span><span class="pn">(</span><span class="str">"https://raw.githubusercontent.com/Noxislua/Scripts/refs/heads/main/Pls%20Donate"</span><span class="pn">))()</span></div>
    </div>

    <div class="ls-lbl">Starving Arts</div>
    <div class="ls-wrap">
      <div class="ls-top">
        <div class="dots"><span></span><span></span><span></span></div>
        <div class="file-lbl">starvingarts.lua</div>
        <button class="copy-btn" onclick="copyCode(this,'sac')">Copy</button>
      </div>
      <div class="code-body" id="sac"><span class="fn">loadstring</span><span class="pn">(</span><span class="kw">game</span><span class="pn">:</span><span class="fn">HttpGet</span><span class="pn">(</span><span class="str">"https://raw.githubusercontent.com/Noxislua/Scripts/refs/heads/main/Starving%20Arts"</span><span class="pn">))()</span></div>
    </div>
  </div>

  <footer>
    <div class="foot-l">Comet Hub</div>
    <div class="foot-r">noxis.lua · v3.2 · 2024</div>
  </footer>

</div>
<script>
  function copyCode(btn, id) {
    navigator.clipboard.writeText(document.getElementById(id).innerText).then(() => {
      btn.textContent = 'Copied!';
      btn.classList.add('ok');
      setTimeout(() => { btn.textContent = 'Copy'; btn.classList.remove('ok'); }, 2000);
    });
  }
</script>
</body>
</html>
