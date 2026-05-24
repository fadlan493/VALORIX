<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Valorix Nation — Minecraft Server</title>
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=VT323:wght@400&family=Rajdhani:wght@400;600;700&display=swap" rel="stylesheet">
<style>
  :root {
    --grass:#5D9E2F;--grass-dark:#3D7A1A;--dirt:#8B5E3C;--dirt-dark:#5C3A1E;
    --diamond:#4FE4E4;--gold:#F5C518;--neon:#00FF88;
    --bg:#0a0f1a;--panel:rgba(15,25,40,0.93);
    --wa:#25D366;--tt:#000000;
  }
  *{margin:0;padding:0;box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  body{font-family:'Rajdhani',sans-serif;background:var(--bg);color:#e8f4ff;min-height:100vh;overflow-x:hidden;position:relative;}

  /* BG */
  .sky-bg{position:fixed;inset:0;background:linear-gradient(180deg,#0a1628 0%,#1a3a5c 40%,#2a5080 70%,#3a6a9a 100%);z-index:0;}
  .stars{position:fixed;inset:0;z-index:1;pointer-events:none;}
  .star{position:absolute;background:white;border-radius:50%;animation:twinkle var(--d) ease-in-out infinite alternate;}
  @keyframes twinkle{from{opacity:.2;transform:scale(.8);}to{opacity:1;transform:scale(1.2);}}
  .clouds{position:fixed;top:60px;width:100%;z-index:2;pointer-events:none;}
  .cloud{position:absolute;image-rendering:pixelated;animation:floatCloud linear infinite;opacity:.22;}
  @keyframes floatCloud{from{transform:translateX(-200px);}to{transform:translateX(110vw);}}
  .ground{position:fixed;bottom:0;left:0;right:0;z-index:3;pointer-events:none;}
  .grass-layer{height:28px;background:repeating-linear-gradient(90deg,var(--grass) 0px,var(--grass) 28px,var(--grass-dark) 28px,var(--grass-dark) 56px);}
  .dirt-layer{height:20px;background:repeating-linear-gradient(90deg,var(--dirt) 0px,var(--dirt) 28px,var(--dirt-dark) 28px,var(--dirt-dark) 56px);}
  .trees{position:fixed;bottom:48px;width:100%;z-index:5;pointer-events:none;}

  /* CHARS */
  .character-container{position:fixed;bottom:48px;z-index:10;pointer-events:none;}
  .char-left{left:-10px;animation:charBob 3s ease-in-out infinite;}
  .char-right{right:-10px;animation:charBobRight 3s ease-in-out infinite 1.5s;}
  @keyframes charBob{0%,100%{transform:translateY(0);}50%{transform:translateY(-12px);}}
  @keyframes charBobRight{0%,100%{transform:scaleX(-1) translateY(0);}50%{transform:scaleX(-1) translateY(-12px);}}
  .steve-body{image-rendering:pixelated;}

  /* NAV */
  .nav{position:fixed;top:0;left:0;right:0;z-index:100;backdrop-filter:blur(16px);background:rgba(8,15,28,0.88);border-bottom:1px solid rgba(79,228,228,0.15);}
  .nav-inner{max-width:900px;margin:0 auto;display:flex;align-items:center;justify-content:space-between;padding:0 24px;height:52px;}
  .nav-logo{font-family:'Press Start 2P',monospace;font-size:10px;color:var(--diamond);letter-spacing:1px;text-decoration:none;text-shadow:0 0 12px rgba(79,228,228,0.6);cursor:pointer;}
  .nav-links{display:flex;gap:4px;}
  .nav-link{font-family:'VT323',monospace;font-size:16px;letter-spacing:1px;color:rgba(200,230,255,0.65);text-decoration:none;padding:6px 12px;border-radius:2px;transition:all .2s;border:1px solid transparent;cursor:pointer;background:none;}
  .nav-link:hover,.nav-link.active{color:var(--diamond);border-color:rgba(79,228,228,0.3);background:rgba(79,228,228,0.07);}
  .nav-mobile-btn{display:none;background:none;border:1px solid rgba(79,228,228,0.3);color:var(--diamond);font-size:18px;padding:4px 10px;cursor:pointer;border-radius:2px;}
  @media(max-width:600px){
    .nav-links{display:none;flex-direction:column;position:absolute;top:52px;left:0;right:0;background:rgba(8,15,28,0.97);border-bottom:1px solid rgba(79,228,228,0.15);padding:8px;}
    .nav-links.open{display:flex;}
    .nav-mobile-btn{display:block;}
  }

  /* CONTENT */
  .content{position:relative;z-index:20;min-height:100vh;display:flex;flex-direction:column;align-items:center;padding:80px 20px 180px;}

  /* ===== SERVER LOGO ===== */
  .server-logo-wrap{text-align:center;margin-bottom:20px;margin-top:10px;}
  .server-logo-img{width:120px;height:120px;border-radius:8px;border:3px solid rgba(79,228,228,.45);box-shadow:0 0 28px rgba(79,228,228,.35),0 0 60px rgba(79,228,228,.12);image-rendering:pixelated;transition:all .3s;}
  .server-logo-img:hover{transform:scale(1.06);box-shadow:0 0 40px rgba(79,228,228,.55),0 0 80px rgba(79,228,228,.2);}

  /* ===== PAGE TRANSITION SYSTEM ===== */
  .page-wrapper{position:relative;width:100%;max-width:720px;overflow:hidden;}

  /* Each section is a "page" that slides */
  .section{
    width:100%;
    display:none;
    opacity:0;
    transform:translateY(40px);
    transition:none;
  }
  .section.active{
    display:block;
    animation:pageSlideIn .45s cubic-bezier(.22,.68,0,1.2) forwards;
  }
  .section.exit-up{
    display:block;
    animation:pageSlideOutUp .3s ease-in forwards;
    pointer-events:none;
    position:absolute;
    top:0;left:0;right:0;
  }
  .section.exit-down{
    display:block;
    animation:pageSlideOutDown .3s ease-in forwards;
    pointer-events:none;
    position:absolute;
    top:0;left:0;right:0;
  }
  .section.enter-from-below{
    animation:pageSlideInUp .45s cubic-bezier(.22,.68,0,1.2) forwards !important;
  }
  .section.enter-from-above{
    animation:pageSlideInDown .45s cubic-bezier(.22,.68,0,1.2) forwards !important;
  }

  @keyframes pageSlideIn{
    from{opacity:0;transform:translateY(50px) scale(.97);}
    to{opacity:1;transform:translateY(0) scale(1);}
  }
  @keyframes pageSlideInUp{
    from{opacity:0;transform:translateY(60px) scale(.97);}
    to{opacity:1;transform:translateY(0) scale(1);}
  }
  @keyframes pageSlideInDown{
    from{opacity:0;transform:translateY(-60px) scale(.97);}
    to{opacity:1;transform:translateY(0) scale(1);}
  }
  @keyframes pageSlideOutUp{
    from{opacity:1;transform:translateY(0) scale(1);}
    to{opacity:0;transform:translateY(-50px) scale(.97);}
  }
  @keyframes pageSlideOutDown{
    from{opacity:1;transform:translateY(0) scale(1);}
    to{opacity:0;transform:translateY(50px) scale(.97);}
  }

  /* HEADER */
  .header{text-align:center;margin-bottom:36px;}
  .server-badge{display:inline-block;background:rgba(79,228,228,0.12);border:1px solid var(--diamond);color:var(--diamond);font-family:'Press Start 2P',monospace;font-size:7px;padding:6px 14px;letter-spacing:2px;margin-bottom:18px;animation:badgePulse 2s ease-in-out infinite;}
  @keyframes badgePulse{0%,100%{box-shadow:0 0 8px rgba(79,228,228,.3);}50%{box-shadow:0 0 22px rgba(79,228,228,.7);}}
  .server-title{font-family:'Press Start 2P',monospace;font-size:clamp(20px,5vw,42px);line-height:1.4;color:#fff;text-shadow:4px 4px 0 #0a4a1a,-2px -2px 0 rgba(0,0,0,.5);letter-spacing:2px;}
  .title-accent{color:var(--diamond);display:block;font-size:clamp(13px,3vw,24px);text-shadow:3px 3px 0 #003a5c,0 0 28px rgba(79,228,228,.8);}
  .subtitle{font-family:'VT323',monospace;font-size:19px;color:rgba(200,230,255,.65);letter-spacing:3px;margin-top:8px;}

  /* CARD */
  .mc-card{background:var(--panel);border:2px solid rgba(79,228,228,.28);border-radius:4px;padding:28px 36px;position:relative;backdrop-filter:blur(12px);box-shadow:0 0 36px rgba(79,228,228,.08),inset 0 1px 0 rgba(255,255,255,.04);margin-bottom:20px;}
  .mc-card::before,.mc-card::after{content:'';position:absolute;width:10px;height:10px;background:var(--diamond);}
  .mc-card::before{top:-2px;left:-2px;}.mc-card::after{bottom:-2px;right:-2px;}
  .cc-tr,.cc-bl{position:absolute;width:10px;height:10px;background:var(--diamond);}
  .cc-tr{top:-2px;right:-2px;}.cc-bl{bottom:-2px;left:-2px;}

  /* IP DUAL */
  .ip-dual{display:grid;grid-template-columns:1fr 1fr;gap:14px;margin-bottom:20px;}
  @media(max-width:520px){.ip-dual{grid-template-columns:1fr;}}
  .ip-card{background:rgba(0,0,0,.45);border:1px solid rgba(79,228,228,.22);border-radius:3px;padding:14px 16px;}
  .ip-card-label{font-family:'Press Start 2P',monospace;font-size:7px;color:var(--diamond);letter-spacing:1px;margin-bottom:8px;display:flex;align-items:center;gap:6px;}
  .ip-badge{padding:2px 8px;border-radius:2px;font-size:6px;}
  .badge-bedrock{background:rgba(245,197,24,.18);color:var(--gold);border:1px solid rgba(245,197,24,.4);}
  .badge-java{background:rgba(79,228,228,.15);color:var(--diamond);border:1px solid rgba(79,228,228,.35);}
  .ip-val-row{display:flex;align-items:center;justify-content:space-between;gap:6px;}
  .ip-val{font-family:'VT323',monospace;font-size:18px;color:#fff;letter-spacing:1px;word-break:break-all;}
  .ip-port{font-family:'VT323',monospace;font-size:14px;color:rgba(200,230,255,.5);margin-top:2px;}
  .copy-btn{background:none;border:none;cursor:pointer;color:rgba(79,228,228,.55);padding:4px;transition:all .2s;display:flex;align-items:center;flex-shrink:0;}
  .copy-btn:hover{color:var(--diamond);transform:scale(1.2);}

  /* JOIN BTN */
  .join-btn{width:100%;padding:15px;font-family:'Press Start 2P',monospace;font-size:11px;background:linear-gradient(180deg,var(--grass) 0%,var(--grass-dark) 100%);color:#fff;border:none;cursor:pointer;letter-spacing:1px;transition:all .15s;border-radius:2px;box-shadow:0 4px 0 var(--grass-dark),0 0 18px rgba(93,158,47,.35);}
  .join-btn:hover{transform:translateY(-2px);box-shadow:0 6px 0 var(--grass-dark),0 0 28px rgba(93,158,47,.55);}
  .join-btn:active{transform:translateY(2px);box-shadow:0 2px 0 var(--grass-dark);}

  /* PLAYER STATUS */
  .player-status{border-top:1px solid rgba(79,228,228,.13);padding-top:22px;margin-top:22px;}
  .status-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:14px;}
  .status-title{font-family:'Press Start 2P',monospace;font-size:8px;color:var(--diamond);letter-spacing:1px;}
  .refresh-btn{background:none;border:1px solid rgba(79,228,228,.28);border-radius:2px;color:var(--diamond);font-size:14px;padding:4px 10px;cursor:pointer;font-family:'VT323',monospace;letter-spacing:1px;transition:all .2s;}
  .refresh-btn:hover{background:rgba(79,228,228,.1);border-color:var(--diamond);}
  .online-indicator{display:flex;align-items:center;gap:14px;background:rgba(0,0,0,.38);border:1px solid rgba(79,228,228,.18);border-radius:2px;padding:12px 18px;margin-bottom:14px;}
  .status-dot{width:11px;height:11px;border-radius:50%;flex-shrink:0;}
  .status-dot.online{background:var(--neon);box-shadow:0 0 10px var(--neon);animation:dotPulse 1.5s ease-in-out infinite;}
  .status-dot.offline{background:#ff4444;box-shadow:0 0 8px #ff4444;}
  .status-dot.loading{background:var(--gold);animation:dotBlink 1s linear infinite;}
  @keyframes dotPulse{0%,100%{box-shadow:0 0 6px var(--neon);}50%{box-shadow:0 0 18px var(--neon),0 0 30px rgba(0,255,136,.4);}}
  @keyframes dotBlink{0%,100%{opacity:1;}50%{opacity:.2;}}
  .online-text{flex:1;}
  .online-status-label{font-family:'VT323',monospace;font-size:18px;letter-spacing:1px;}
  .online-desc{font-size:12px;color:rgba(200,230,255,.45);margin-top:2px;}
  .player-count{text-align:right;}
  .count-number{font-family:'Press Start 2P',monospace;font-size:20px;color:var(--diamond);display:block;}
  .count-label{font-size:11px;color:rgba(200,230,255,.45);}
  .player-list{display:flex;flex-wrap:wrap;gap:8px;}
  .player-tag{background:rgba(79,228,228,.07);border:1px solid rgba(79,228,228,.18);border-radius:2px;padding:4px 10px;font-family:'VT323',monospace;font-size:16px;color:#c8e8ff;display:flex;align-items:center;gap:6px;}
  .player-head{width:15px;height:15px;border-radius:1px;flex-shrink:0;image-rendering:pixelated;}
  .no-players{font-family:'VT323',monospace;font-size:17px;color:rgba(200,230,255,.35);text-align:center;padding:14px;letter-spacing:2px;}
  .motd-box{background:rgba(0,0,0,.35);border:1px solid rgba(79,228,228,.13);border-radius:2px;padding:8px 14px;margin-bottom:14px;font-family:'VT323',monospace;font-size:16px;color:rgba(200,230,255,.65);letter-spacing:1px;text-align:center;font-style:italic;}
  .loading-bar{height:3px;background:rgba(79,228,228,.1);border-radius:2px;overflow:hidden;margin-top:8px;}
  .loading-fill{height:100%;background:linear-gradient(90deg,transparent,var(--diamond),transparent);animation:loadSweep 1.5s ease-in-out infinite;width:40%;}
  @keyframes loadSweep{from{transform:translateX(-250%);}to{transform:translateX(400%);}}
  .ping-badge{font-family:'VT323',monospace;font-size:14px;padding:2px 8px;border-radius:2px;letter-spacing:1px;}
  .ping-good{background:rgba(0,255,136,.13);color:var(--neon);border:1px solid rgba(0,255,136,.28);}
  .ping-ok{background:rgba(245,197,24,.13);color:var(--gold);border:1px solid rgba(245,197,24,.28);}
  .ping-bad{background:rgba(255,80,80,.13);color:#ff6666;border:1px solid rgba(255,80,80,.28);}
  .version-badge{display:inline-block;background:rgba(85,171,38,.13);border:1px solid rgba(85,171,38,.38);color:#88dd44;font-family:'VT323',monospace;font-size:14px;padding:2px 10px;border-radius:2px;letter-spacing:1px;}

  /* ===== FEATURES — BRUTAL WEAPONS ===== */
  .features-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:12px;margin-bottom:0;}
  .feature-card{background:rgba(10,18,32,.88);border:1px solid rgba(79,228,228,.18);border-radius:2px;padding:18px 14px;text-align:center;backdrop-filter:blur(6px);transition:all .25s;cursor:default;position:relative;overflow:hidden;}
  .feature-card::after{content:'';position:absolute;inset:0;background:radial-gradient(circle at 50% 0%,rgba(79,228,228,.06),transparent 70%);opacity:0;transition:opacity .3s;}
  .feature-card:hover{border-color:rgba(79,228,228,.45);transform:translateY(-4px);box-shadow:0 8px 22px rgba(79,228,228,.14);}
  .feature-card:hover::after{opacity:1;}
  .weapon-icon{width:52px;height:52px;margin:0 auto 10px;display:flex;align-items:center;justify-content:center;position:relative;}
  .weapon-icon svg{width:48px;height:48px;filter:drop-shadow(0 0 6px currentColor);}
  .feature-card:hover .weapon-icon svg{animation:weaponShake .4s ease-in-out;}
  @keyframes weaponShake{0%,100%{transform:rotate(0);}25%{transform:rotate(-8deg);}75%{transform:rotate(8deg);}}
  .feature-name{font-family:'Press Start 2P',monospace;font-size:6px;color:var(--diamond);letter-spacing:1px;margin-bottom:5px;}
  .feature-desc{font-size:12px;color:rgba(200,230,255,.55);line-height:1.4;}

  /* ===== SOCIAL MEDIA SECTION ===== */
  .section-title{font-family:'Press Start 2P',monospace;font-size:10px;color:var(--diamond);letter-spacing:2px;margin-bottom:24px;text-align:center;text-shadow:0 0 14px rgba(79,228,228,.5);}
  .section-title span{display:block;font-size:7px;color:rgba(200,230,255,.4);letter-spacing:3px;margin-top:6px;font-family:'VT323',monospace;}

  .social-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:16px;}
  .social-card{background:var(--panel);border:1px solid rgba(79,228,228,.2);border-radius:4px;padding:24px;display:flex;align-items:center;gap:18px;text-decoration:none;transition:all .25s;position:relative;overflow:hidden;}
  .social-card::after{content:'';position:absolute;inset:0;opacity:0;transition:opacity .3s;}
  .social-card:hover{transform:translateY(-4px);border-color:rgba(79,228,228,.5);}
  .social-card.wa{border-color:rgba(37,211,102,.3);}
  .social-card.wa:hover{box-shadow:0 8px 30px rgba(37,211,102,.2);border-color:var(--wa);}
  .social-card.wa::after{background:radial-gradient(circle at 50% 0%,rgba(37,211,102,.06),transparent 70%);}
  .social-card.wa:hover::after{opacity:1;}
  .social-card.tt{border-color:rgba(255,255,255,.15);}
  .social-card.tt:hover{box-shadow:0 8px 30px rgba(255,255,255,.08);border-color:rgba(255,255,255,.4);}
  .social-card.tt::after{background:radial-gradient(circle at 50% 0%,rgba(255,255,255,.04),transparent 70%);}
  .social-card.tt:hover::after{opacity:1;}

  .social-icon-wrap{width:54px;height:54px;border-radius:12px;display:flex;align-items:center;justify-content:center;flex-shrink:0;}
  .social-icon-wrap.wa-ico{background:rgba(37,211,102,.18);border:1px solid rgba(37,211,102,.35);}
  .social-icon-wrap.tt-ico{background:rgba(255,255,255,.08);border:1px solid rgba(255,255,255,.15);}
  .social-icon{width:28px;height:28px;}
  .social-info{flex:1;}
  .social-platform{font-family:'Press Start 2P',monospace;font-size:8px;letter-spacing:1px;margin-bottom:5px;}
  .social-platform.wa-txt{color:var(--wa);}
  .social-platform.tt-txt{color:#fff;}
  .social-handle{font-family:'VT323',monospace;font-size:17px;color:rgba(200,230,255,.65);letter-spacing:1px;margin-bottom:4px;}
  .social-action{display:inline-flex;align-items:center;gap:5px;font-size:12px;font-family:'Rajdhani',sans-serif;font-weight:600;letter-spacing:1px;padding:4px 12px;border-radius:2px;transition:all .2s;}
  .social-action.wa-act{background:rgba(37,211,102,.15);color:var(--wa);border:1px solid rgba(37,211,102,.3);}
  .social-action.tt-act{background:rgba(255,255,255,.07);color:#fff;border:1px solid rgba(255,255,255,.15);}
  .social-arrow{font-size:14px;color:rgba(200,230,255,.25);transition:transform .2s;}
  .social-card:hover .social-arrow{transform:translateX(4px);}

  /* ===== STAFF SECTION ===== */
  .staff-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:14px;}
  .staff-card{background:var(--panel);border:1px solid rgba(79,228,228,.2);border-radius:4px;padding:20px 22px;display:flex;align-items:center;gap:16px;position:relative;overflow:hidden;transition:all .2s;}
  .staff-card::before{content:'';position:absolute;left:0;top:0;bottom:0;width:3px;}
  .staff-card.owner::before{background:linear-gradient(180deg,var(--gold),#e0a010);}
  .staff-card.admin::before{background:linear-gradient(180deg,#FF6B6B,#cc3333);}
  .staff-card.helper::before{background:linear-gradient(180deg,var(--diamond),#1ab8b8);}
  .staff-card:hover{transform:translateY(-2px);border-color:rgba(79,228,228,.38);}
  .staff-card.owner:hover{box-shadow:0 6px 24px rgba(245,197,24,.12);}
  .staff-card.admin:hover{box-shadow:0 6px 24px rgba(255,107,107,.12);}
  .staff-card.helper:hover{box-shadow:0 6px 24px rgba(79,228,228,.1);}

  .staff-avatar{width:48px;height:48px;border-radius:4px;flex-shrink:0;image-rendering:pixelated;display:flex;align-items:center;justify-content:center;font-family:'Press Start 2P',monospace;font-size:14px;}
  .staff-avatar.owner-av{background:rgba(245,197,24,.2);border:1px solid rgba(245,197,24,.4);color:var(--gold);}
  .staff-avatar.admin-av{background:rgba(255,107,107,.18);border:1px solid rgba(255,107,107,.35);color:#FF6B6B;}
  .staff-avatar.helper-av{background:rgba(79,228,228,.13);border:1px solid rgba(79,228,228,.3);color:var(--diamond);}

  .staff-info{flex:1;min-width:0;}
  .staff-role-badge{display:inline-block;font-family:'Press Start 2P',monospace;font-size:6px;padding:3px 8px;border-radius:2px;letter-spacing:1px;margin-bottom:6px;}
  .badge-owner{background:rgba(245,197,24,.18);color:var(--gold);border:1px solid rgba(245,197,24,.35);}
  .badge-admin{background:rgba(255,107,107,.15);color:#FF6B6B;border:1px solid rgba(255,107,107,.3);}
  .badge-helper{background:rgba(79,228,228,.12);color:var(--diamond);border:1px solid rgba(79,228,228,.28);}
  .staff-name{font-family:'VT323',monospace;font-size:22px;color:#fff;letter-spacing:1px;margin-bottom:3px;}
  .staff-contact{font-size:12px;color:rgba(200,230,255,.45);font-family:'Rajdhani',sans-serif;letter-spacing:.5px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
  .staff-contact a{color:var(--wa);text-decoration:none;}
  .staff-contact a:hover{text-decoration:underline;}
  .staff-crown{position:absolute;top:12px;right:14px;font-size:18px;opacity:.6;}

  /* ===== GALLERY SECTION ===== */
  .gallery-grid{
    display:grid;
    grid-template-columns:repeat(auto-fill,minmax(200px,1fr));
    gap:12px;
    margin-bottom:0;
  }
  .gallery-item{
    position:relative;
    border:2px solid rgba(79,228,228,.2);
    border-radius:4px;
    overflow:hidden;
    cursor:pointer;
    aspect-ratio:16/10;
    background:rgba(0,0,0,.4);
    transition:all .25s;
  }
  .gallery-item:hover{
    border-color:var(--diamond);
}
</style>
</head>
<body>

</body>
</html>
