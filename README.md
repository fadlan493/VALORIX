<!DOCTYPE html>
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
  
  .nav-mobile-btn{display:none;background:none;border:1px solid rgba(79,228,228,0.3);color:var(--diamond);font-size:18px;padding:4px 10px;cursor:pointer;border-radius:2px;transition:all .3s;position:relative;width:40px;height:40px;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:5px;}
  .nav-mobile-btn span{display:block;width:20px;height:2px;background:var(--diamond);border-radius:1px;transition:all .3s ease;transform-origin:center;}
  .nav-mobile-btn.active span:nth-child(1){transform:translateY(8px) rotate(45deg);}
  .nav-mobile-btn.active span:nth-child(2){opacity:0;transform:translateX(-10px);}
  .nav-mobile-btn.active span:nth-child(3){transform:translateY(-8px) rotate(-45deg);}
  
  @media(max-width:600px){
    .nav-links{display:none;flex-direction:column;position:absolute;top:52px;left:0;right:0;background:rgba(8,15,28,0.98);border-bottom:1px solid rgba(79,228,228,0.15);padding:12px 8px;backdrop-filter:blur(20px);max-height:0;overflow:hidden;transition:max-height .4s cubic-bezier(.34,.1,.68,.55);}
    .nav-links.open{display:flex;max-height:500px;}
    .nav-links.open .nav-link{animation:menuItemSlide .3s cubic-bezier(.34,.1,.68,.55) forwards;}
    .nav-links.open .nav-link:nth-child(1){animation-delay:.05s;}
    .nav-links.open .nav-link:nth-child(2){animation-delay:.1s;}
    .nav-links.open .nav-link:nth-child(3){animation-delay:.15s;}
    .nav-links.open .nav-link:nth-child(4){animation-delay:.2s;}
    .nav-links.open .nav-link:nth-child(5){animation-delay:.25s;}
    .nav-links.open .nav-link:nth-child(6){animation-delay:.3s;}
    .nav-links.open .nav-link:nth-child(7){animation-delay:.35s;}
    .nav-links.open .nav-link:nth-child(8){animation-delay:.4s;}
    .nav-links.open .nav-link:nth-child(9){animation-delay:.45s;}
    .nav-link{opacity:0;transform:translateX(-20px);}
    .nav-mobile-btn{display:flex;}
  }
  @keyframes menuItemSlide{from{opacity:0;transform:translateX(-20px);}to{opacity:1;transform:translateX(0);}}

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
    transform:scale(1.03);
    box-shadow:0 0 24px rgba(79,228,228,.3);
    z-index:2;
  }
  .gallery-item img{
    width:100%;
    height:100%;
    object-fit:cover;
    display:block;
    transition:transform .3s;
    image-rendering:auto;
  }
  .gallery-item:hover img{transform:scale(1.08);}
  .gallery-item .gallery-overlay{
    position:absolute;inset:0;
    background:linear-gradient(0deg,rgba(10,15,30,.7) 0%,transparent 60%);
    opacity:0;
    transition:opacity .25s;
    display:flex;align-items:flex-end;justify-content:center;
    padding-bottom:12px;
    font-family:'VT323',monospace;
    font-size:15px;
    color:var(--diamond);
    letter-spacing:2px;
  }
  .gallery-item:hover .gallery-overlay{opacity:1;}

  /* LIGHTBOX */
  .lightbox{
    display:none;
    position:fixed;inset:0;z-index:999;
    background:rgba(4,10,22,.95);
    backdrop-filter:blur(10px);
    align-items:center;justify-content:center;
    flex-direction:column;gap:18px;
    animation:lbFade .2s ease;
  }
  .lightbox.open{display:flex;}
  @keyframes lbFade{from{opacity:0;}to{opacity:1;}}
  .lightbox-img{
    max-width:90vw;max-height:75vh;
    border:3px solid rgba(79,228,228,.5);
    border-radius:4px;
    box-shadow:0 0 60px rgba(79,228,228,.25);
    object-fit:contain;
    animation:lbScale .25s cubic-bezier(.22,.68,0,1.2);
  }
  @keyframes lbScale{from{transform:scale(.88);}to{transform:scale(1);}}
  .lightbox-close{
    position:absolute;top:20px;right:24px;
    background:none;border:1px solid rgba(79,228,228,.3);
    color:var(--diamond);font-size:22px;
    padding:4px 14px;cursor:pointer;
    border-radius:2px;
    font-family:'VT323',monospace;
    transition:all .2s;
  }
  .lightbox-close:hover{background:rgba(79,228,228,.12);border-color:var(--diamond);}
  .lightbox-nav{display:flex;gap:16px;}
  .lightbox-btn{
    background:rgba(15,25,40,.9);
    border:1px solid rgba(79,228,228,.3);
    color:var(--diamond);
    font-family:'VT323',monospace;
    font-size:18px;
    padding:8px 22px;
    cursor:pointer;
    border-radius:2px;
    letter-spacing:1px;
    transition:all .2s;
  }
  .lightbox-btn:hover{background:rgba(79,228,228,.12);border-color:var(--diamond);}
  .lightbox-counter{
    font-family:'VT323',monospace;
    font-size:16px;
    color:rgba(200,230,255,.5);
    letter-spacing:2px;
  }

  /* ===== INTRO ANIMATION ===== */
  #introOverlay{position:fixed;inset:0;z-index:9999;display:flex;align-items:center;justify-content:center;background:#0a0f1a;animation:introFadeOut .6s ease-out 3.8s forwards;}
  @keyframes introFadeOut{to{opacity:0;pointer-events:none;}}
  .intro-bg{position:absolute;inset:0;background:linear-gradient(180deg,#0a1628 0%,#1a3a5c 40%,#2a5080 70%,#3a6a9a 100%);}
  .intro-particles{position:absolute;inset:0;overflow:hidden;}
  .intro-particle{position:absolute;background:rgba(255,255,255,.3);border-radius:50%;animation:particleFloat 3s ease-in-out infinite;}
  @keyframes particleFloat{0%,100%{transform:translateY(0) scale(1);opacity:0;}50%{opacity:1;}}
  .intro-content{position:relative;z-index:2;text-align:center;animation:introContentIn .5s cubic-bezier(.34,.1,.68,.55) .2s forwards;opacity:0;}
  @keyframes introContentIn{to{opacity:1;}}
  .intro-logo-wrap{margin-bottom:24px;perspective:1000px;}
  .intro-logo{width:140px;height:140px;border-radius:12px;border:4px solid rgba(79,228,228,.6);box-shadow:0 0 40px rgba(79,228,228,.4),0 0 80px rgba(79,228,228,.15);image-rendering:pixelated;animation:logoSpinIn .8s cubic-bezier(.34,.1,.68,.55) .4s forwards;opacity:0;transform:rotateY(90deg) scale(.7);}
  @keyframes logoSpinIn{to{opacity:1;transform:rotateY(0) scale(1);}}
  .intro-title-wrap{margin-bottom:20px;}
  .intro-word{font-family:'Press Start 2P',monospace;font-size:clamp(24px,8vw,48px);font-weight:bold;color:#fff;letter-spacing:3px;text-shadow:4px 4px 0 #0a4a1a;line-height:1.3;animation:wordSlideIn .6s cubic-bezier(.34,.1,.68,.55) .6s forwards;opacity:0;transform:translateY(30px);}
  .intro-word.accent{color:var(--diamond);text-shadow:3px 3px 0 #003a5c,0 0 32px rgba(79,228,228,.8);}
  @keyframes wordSlideIn{to{opacity:1;transform:translateY(0);}}
  .intro-sub{font-family:'VT323',monospace;font-size:18px;letter-spacing:3px;color:rgba(200,230,255,.65);margin-bottom:24px;animation:subFadeIn .5s ease .9s forwards;opacity:0;}
  @keyframes subFadeIn{to{opacity:1;}}
  .intro-bar-wrap{max-width:280px;margin:24px auto;}
  .intro-bar-track{height:4px;background:rgba(79,228,228,.15);border-radius:2px;overflow:hidden;border:1px solid rgba(79,228,228,.3);}
  .intro-bar-fill{height:100%;background:linear-gradient(90deg,var(--diamond),var(--neon),var(--gold));animation:introBarLoad 3.5s ease-in-out .3s forwards;width:0%;}
  @keyframes introBarLoad{to{width:100%;}}
  .intro-bar-label{font-family:'VT323',monospace;font-size:14px;color:rgba(200,230,255,.5);letter-spacing:2px;margin-top:8px;animation:labelFade .4s ease 1s forwards;opacity:0;}
  @keyframes labelFade{to{opacity:1;}}
  .intro-skip{position:absolute;bottom:60px;left:50%;transform:translateX(-50%);font-family:'VT323',monospace;font-size:16px;color:rgba(200,230,255,.4);letter-spacing:2px;cursor:pointer;transition:all .3s;animation:skipFade .3s ease 2s forwards;opacity:0;}
  .intro-skip:hover{color:var(--diamond);transform:translateX(-50%) scale(1.08);}
  @keyframes skipFade{to{opacity:1;}}
  .intro-blocks{position:absolute;inset:0;overflow:hidden;}
  .intro-block{position:absolute;background:rgba(79,228,228,.08);border:1px solid rgba(79,228,228,.2);animation:blockPixelate .3s ease;opacity:0;}
  @keyframes blockPixelate{from{opacity:.6;transform:scale(1.2);}to{opacity:0;transform:scale(.8);}}

  /* ===== RANK SECTION ===== */
  .rank-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:14px;margin-bottom:0;}
  .rank-card{background:var(--panel);border:2px solid rgba(79,228,228,.2);border-radius:4px;padding:20px;position:relative;overflow:hidden;transition:all .25s;backdrop-filter:blur(8px);}
  .rank-card::before{content:'';position:absolute;top:0;left:0;right:0;height:3px;background:linear-gradient(90deg,transparent,var(--diamond),transparent);}
  .rank-card:hover{transform:translateY(-6px);border-color:rgba(79,228,228,.45);box-shadow:0 12px 36px rgba(79,228,228,.15);}
  .rank-vip{border-color:rgba(79,228,228,.25);}
  .rank-vip:hover{box-shadow:0 12px 36px rgba(79,228,228,.15);}
  .rank-vipp{border-color:rgba(100,200,255,.25);}
  .rank-mvp{border-color:rgba(170,100,255,.25);}
  .rank-legend{border-color:rgba(255,200,50,.25);}
  .rank-deckhand{border-color:rgba(100,200,150,.25);}
  .rank-viscount{border-color:rgba(180,100,200,.25);}
  .rank-badge-sale{position:absolute;top:12px;right:12px;background:rgba(255,80,80,.2);border:1px solid rgba(255,80,80,.5);color:#ff8888;font-family:'Press Start 2P',monospace;font-size:6px;padding:4px 10px;border-radius:2px;letter-spacing:1px;animation:badgePulse 2s ease-in-out infinite;}
  .rank-header-bar{display:flex;align-items:center;justify-content:space-between;gap:10px;margin-bottom:16px;padding-bottom:12px;border-bottom:1px solid rgba(79,228,228,.15);}
  .rank-icon{font-size:24px;display:block;}
  .rank-name{font-family:'Press Start 2P',monospace;font-size:8px;color:var(--diamond);letter-spacing:2px;flex:1;text-align:center;}
  .rank-price{font-family:'VT323',monospace;font-size:14px;color:var(--gold);letter-spacing:1px;white-space:nowrap;font-weight:bold;}
  .rank-perks{list-style:none;margin-bottom:16px;}
  .rank-perks li{font-family:'VT323',monospace;font-size:14px;color:rgba(200,230,255,.7);margin-bottom:7px;padding-left:6px;letter-spacing:.5px;line-height:1.4;}
  .rank-buy-btn{display:block;width:100%;padding:12px;background:linear-gradient(180deg,rgba(79,228,228,.3),rgba(79,228,228,.1));border:1px solid rgba(79,228,228,.4);color:var(--diamond);font-family:'Press Start 2P',monospace;font-size:8px;letter-spacing:2px;border-radius:2px;cursor:pointer;transition:all .2s;text-decoration:none;text-align:center;}
  .rank-buy-btn:hover{background:linear-gradient(180deg,rgba(79,228,228,.5),rgba(79,228,228,.25));border-color:var(--diamond);transform:scale(1.02);}
  .vip-btn{background:linear-gradient(180deg,rgba(79,228,228,.3),rgba(79,228,228,.1));}
  .vipp-btn{background:linear-gradient(180deg,rgba(100,200,255,.25),rgba(100,200,255,.08));}
  .mvp-btn{background:linear-gradient(180deg,rgba(170,100,255,.25),rgba(170,100,255,.08));}
  .legend-btn{background:linear-gradient(180deg,rgba(255,200,50,.25),rgba(255,200,50,.08));}
  .deckhand-btn{background:linear-gradient(180deg,rgba(100,200,150,.25),rgba(100,200,150,.08));}
  .viscount-btn{background:linear-gradient(180deg,rgba(180,100,200,.25),rgba(180,100,200,.08));}

  /* ===== LAPOR SECTION ===== */
  .lapor-form{background:rgba(0,0,0,.3);border:1px solid rgba(79,228,228,.15);border-radius:3px;padding:22px;}
  .lapor-field{margin-bottom:18px;}
  .lapor-label{display:block;font-family:'Press Start 2P',monospace;font-size:7px;color:var(--diamond);letter-spacing:2px;margin-bottom:8px;text-transform:uppercase;}
  .lapor-input{width:100%;padding:12px;background:rgba(0,0,0,.4);border:1px solid rgba(79,228,228,.25);border-radius:2px;font-family:'VT323',monospace;font-size:16px;color:#fff;letter-spacing:1px;transition:all .2s;resize:none;}
  .lapor-input:focus{outline:none;background:rgba(0,0,0,.5);border-color:rgba(79,228,228,.6);box-shadow:0 0 14px rgba(79,228,228,.15);}
  .lapor-textarea{min-height:120px;font-size:15px;}
  .lapor-select{cursor:pointer;appearance:none;background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%234FE4E4' stroke-width='2'%3E%3Cpolyline points='6 9 12 15 18 9'%3E%3C/polyline%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 12px center;background-size:18px;padding-right:40px;}
  .lapor-btn{width:100%;padding:14px;background:linear-gradient(180deg,var(--grass),var(--grass-dark));color:#fff;font-family:'Press Start 2P',monospace;font-size:9px;letter-spacing:2px;border:none;border-radius:2px;cursor:pointer;transition:all .15s;box-shadow:0 4px 0 var(--grass-dark),0 0 16px rgba(93,158,47,.3);}
  .lapor-btn:hover{transform:translateY(-2px);box-shadow:0 6px 0 var(--grass-dark),0 0 24px rgba(93,158,47,.5);}
  .lapor-btn:active{transform:translateY(2px);box-shadow:0 2px 0 var(--grass-dark);}

  /* ===== PANDUAN SECTION ===== */
  .guides-container{display:grid;gap:16px;}
  .guide-card{background:rgba(0,0,0,.3);border:1px solid rgba(79,228,228,.18);border-radius:3px;padding:20px;transition:all .25s;}
  .guide-card:hover{border-color:rgba(79,228,228,.35);box-shadow:0 8px 24px rgba(79,228,228,.08);}
  .guide-icon{font-size:32px;margin-bottom:10px;}
  .guide-title{font-family:'Press Start 2P',monospace;font-size:9px;color:var(--diamond);letter-spacing:2px;margin-bottom:14px;text-transform:uppercase;}
  .guide-desc{font-family:'VT323',monospace;font-size:15px;color:rgba(200,230,255,.7);line-height:1.7;letter-spacing:.5px;}
  .guide-desc p{margin-bottom:12px;}
  .guide-desc strong{color:#fff;}
  .guide-desc code{background:rgba(79,228,228,.12);border:1px solid rgba(79,228,228,.25);padding:3px 8px;border-radius:2px;font-size:14px;color:var(--neon);letter-spacing:1px;display:inline-block;}
  .guide-steps{list-style:none;margin:12px 0;padding-left:0;}
  .guide-steps li{margin-bottom:10px;padding-left:24px;position:relative;}
  .guide-steps li::before{content:'▸';position:absolute;left:0;color:var(--diamond);}
  .guide-steps strong{color:var(--diamond);}
  .guide-tip{background:rgba(245,197,24,.08);border-left:3px solid var(--gold);padding:10px 12px;margin-top:12px;border-radius:2px;font-size:14px;color:rgba(200,230,255,.65);}

  /* ===== EVENT SECTION ===== */
  .events-container{display:grid;gap:16px;}
  .event-card{background:var(--panel);border:2px solid rgba(79,228,228,.2);border-radius:4px;overflow:hidden;transition:all .25s;}
  .event-card:hover{transform:translateY(-4px);border-color:rgba(79,228,228,.45);}
  .event-card.featured{border-color:rgba(79,228,228,.4);}
  .event-card.featured:hover{box-shadow:0 12px 36px rgba(79,228,228,.18);}
  .event-image-wrap{position:relative;overflow:hidden;aspect-ratio:16/9;background:rgba(0,0,0,.4);}
  .event-image{width:100%;height:100%;object-fit:cover;display:block;transition:transform .3s;}
  .event-card:hover .event-image{transform:scale(1.05);}
  .event-badge{position:absolute;top:14px;right:14px;background:rgba(255,200,50,.2);border:1px solid rgba(255,200,50,.5);color:var(--gold);font-family:'Press Start 2P',monospace;font-size:7px;padding:5px 11px;border-radius:2px;letter-spacing:1px;animation:badgePulse 2s ease-in-out infinite;}
  .event-content{padding:20px;}
  .event-title-wrap{margin-bottom:14px;border-bottom:1px solid rgba(79,228,228,.15);padding-bottom:12px;}
  .event-title{font-family:'Press Start 2P',monospace;font-size:9px;color:var(--diamond);letter-spacing:2px;margin:0 0 8px 0;text-transform:uppercase;}
  .event-date{font-family:'VT323',monospace;font-size:15px;color:rgba(200,230,255,.5);letter-spacing:1px;}
  .event-description{font-family:'VT323',monospace;font-size:15px;color:rgba(200,230,255,.7);margin-bottom:16px;line-height:1.6;letter-spacing:.5px;}
  .event-details{background:rgba(0,0,0,.3);border-left:3px solid var(--diamond);padding:14px;border-radius:2px;margin-bottom:14px;}
  .event-detail-item{display:flex;align-items:flex-start;gap:12px;margin-bottom:10px;font-family:'VT323',monospace;font-size:14px;}
  .event-detail-item:last-child{margin-bottom:0;}
  .detail-label{color:var(--diamond);font-weight:bold;white-space:nowrap;letter-spacing:1px;}
  .detail-value{color:rgba(200,230,255,.8);flex:1;}
  .event-rules{background:rgba(93,158,47,.08);border:1px solid rgba(93,158,47,.25);padding:12px;border-radius:2px;font-family:'VT323',monospace;font-size:14px;color:rgba(200,230,255,.7);line-height:1.6;letter-spacing:.5px;}
  .event-rules strong{color:#88dd44;}

  /* TOAST */
  .toast{position:fixed;top:20px;right:20px;background:rgba(12,24,42,.97);border:1px solid var(--diamond);border-radius:2px;padding:10px 18px;font-family:'VT323',monospace;font-size:17px;color:var(--diamond);z-index:9999;transform:translateX(140%);transition:transform .3s ease;letter-spacing:1px;}
  .toast.show{transform:translateX(0);}

  @media(max-width:520px){
    .mc-card{padding:22px 18px;}
    .server-title{font-size:17px;}
    .title-accent{font-size:13px;}
    .social-card{padding:18px 16px;gap:14px;}
    .staff-grid{grid-template-columns:1fr;}
    .gallery-grid{grid-template-columns:repeat(2,1fr);}
    .server-logo-img{width:90px;height:90px;}
  }
</style>
</head>
<body>

<div class="sky-bg"></div>
<div class="stars" id="stars"></div>
<div class="clouds" id="clouds"></div>
<div class="ground"><div class="grass-layer"></div><div class="dirt-layer"></div></div>
<div class="trees" id="trees"></div>

<!-- Steve Left -->
<div class="character-container char-left">
  <svg width="80" height="160" viewBox="0 0 16 32" class="steve-body">
    <rect x="4" y="0" width="8" height="8" fill="#C8A068"/>
    <rect x="4" y="0" width="8" height="2" fill="#5A3010"/>
    <rect x="4" y="2" width="2" height="2" fill="#5A3010"/>
    <rect x="5" y="3" width="2" height="2" fill="#5E3A1A"/>
    <rect x="9" y="3" width="2" height="2" fill="#5E3A1A"/>
    <rect x="6" y="6" width="4" height="1" fill="#8A5030"/>
    <rect x="4" y="8" width="8" height="12" fill="#3A5FCC"/>
    <rect x="4" y="8" width="8" height="2" fill="#2A4FAA"/>
    <rect x="7" y="11" width="2" height="1" fill="#2A4FAA"/>
    <rect x="7" y="14" width="2" height="1" fill="#2A4FAA"/>
    <rect x="1" y="8" width="3" height="10" fill="#C8A068"/>
    <rect x="12" y="8" width="3" height="10" fill="#3A5FCC"/>
    <rect x="1" y="18" width="3" height="2" fill="#C8A068"/>
    <rect x="12" y="18" width="3" height="2" fill="#C8A068"/>
    <rect x="4" y="20" width="4" height="12" fill="#1A2A88"/>
    <rect x="8" y="20" width="4" height="12" fill="#14228A"/>
    <rect x="4" y="29" width="4" height="3" fill="#3A2010"/>
    <rect x="8" y="29" width="4" height="3" fill="#3A2010"/>
  </svg>
</div>

<!-- Alex Right -->
<div class="character-container char-right">
  <svg width="80" height="160" viewBox="0 0 16 32" class="steve-body">
    <rect x="4" y="0" width="8" height="8" fill="#E0A060"/>
    <rect x="3" y="0" width="10" height="2" fill="#AA4400"/>
    <rect x="3" y="2" width="2" height="8" fill="#AA4400"/>
    <rect x="11" y="2" width="2" height="8" fill="#AA4400"/>
    <rect x="5" y="3" width="2" height="2" fill="#3A7A30"/>
    <rect x="9" y="3" width="2" height="2" fill="#3A7A30"/>
    <rect x="6" y="6" width="4" height="1" fill="#C07040"/>
    <rect x="4" y="8" width="8" height="12" fill="#2A9A88"/>
    <rect x="4" y="8" width="8" height="2" fill="#1A7A68"/>
    <rect x="4" y="18" width="8" height="2" fill="#6A3A10"/>
    <rect x="7" y="18" width="2" height="2" fill="#AA7A20"/>
    <rect x="2" y="8" width="2" height="10" fill="#E0A060"/>
    <rect x="12" y="8" width="2" height="10" fill="#2A9A88"/>
    <rect x="2" y="18" width="2" height="2" fill="#E0A060"/>
    <rect x="12" y="18" width="2" height="2" fill="#E0A060"/>
    <rect x="4" y="20" width="8" height="3" fill="#5A2A10"/>
    <rect x="4" y="23" width="4" height="9" fill="#4A2010"/>
    <rect x="8" y="23" width="4" height="9" fill="#3E1A0A"/>
    <rect x="4" y="29" width="4" height="3" fill="#3A2010"/>
    <rect x="8" y="29" width="4" height="3" fill="#3A2010"/>
  </svg>
</div>

<!-- INTRO OVERLAY -->
<div id="introOverlay">
  <div class="intro-bg"></div>
  <div class="intro-particles" id="introParticles"></div>
  <div class="intro-content">
    <div class="intro-logo-wrap">
      <img src="https://i.imgur.com/h7IUOYU.jpeg" alt="Logo" class="intro-logo" id="introLogo"/>
    </div>
    <div class="intro-title-wrap">
      <div class="intro-word" id="iw1">VALORIX</div>
      <div class="intro-word accent" id="iw2">NATION</div>
    </div>
    <div class="intro-sub" id="introSub">⛏ SURVIVAL · CREATIVE · PVP ⛏</div>
    <div class="intro-bar-wrap" id="introBarWrap">
      <div class="intro-bar-track"><div class="intro-bar-fill" id="introBarFill"></div></div>
      <div class="intro-bar-label" id="introBarLabel">Memuat server...</div>
    </div>
    <div class="intro-skip" id="introSkip" onclick="skipIntro()">[ SKIP ▶ ]</div>
  </div>
  <div class="intro-blocks" id="introBlocks"></div>
</div>

<!-- NAV --
<nav class="nav">
  <div class="nav-inner">
    <span class="nav-logo" onclick="showSection('home',0)">⛏ VALORIX</span>
    <button class="nav-mobile-btn" id="navMobileBtn" onclick="toggleMobile()"><span></span><span></span><span></span></button>
    <div class="nav-links" id="navLinks">
      <button class="nav-link active" data-section="home" onclick="showSection('home',0)">🏠 Home</button>
      <button class="nav-link" data-section="features" onclick="showSection('features',1)">⚔️ Features</button>
      <button class="nav-link" data-section="gallery" onclick="showSection('gallery',2)">🖼 Galeri</button>
      <button class="nav-link" data-section="rank" onclick="showSection('rank',3)">💎 Rank</button>
      <button class="nav-link" data-section="panduan" onclick="showSection('panduan',4)">📖 Panduan</button>
      <button class="nav-link" data-section="event" onclick="showSection('event',5)">🎉 Event</button>
      <button class="nav-link" data-section="social" onclick="showSection('social',6)">📢 Sosmed</button>
      <button class="nav-link" data-section="staff" onclick="showSection('staff',7)">👑 Staff</button>
      <button class="nav-link" data-section="lapor" onclick="showSection('lapor',8)">🚨 Lapor</button>
    </div>
  </div>
</nav>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<!-- LIGHTBOX -->
<div class="lightbox" id="lightbox">
  <button class="lightbox-close" onclick="closeLightbox()">✕ TUTUP</button>
  <img class="lightbox-img" id="lightboxImg" src="" alt="Gallery"/>
  <div class="lightbox-nav">
    <button class="lightbox-btn" onclick="lbPrev()">◀ PREV</button>
    <span class="lightbox-counter" id="lbCounter">1 / 5</span>
    <button class="lightbox-btn" onclick="lbNext()">NEXT ▶</button>
  </div>
</div>

<!-- CONTENT -->
<div class="content">

  <!-- Server Logo -->
  <div class="server-logo-wrap">
    <img src="https://i.imgur.com/h7IUOYU.jpeg" alt="Valorix Nation Logo" class="server-logo-img" onerror="this.style.display='none'"/>
  </div>

  <div class="page-wrapper" id="pageWrapper">

  <!-- HOME -->
  <div class="section active" id="section-home">
    <div class="header">
      <div class="server-badge">▶ SERVER AKTIF</div>
      <h1 class="server-title">
        VALORIX<br>
        <span class="title-accent">NATION</span>
      </h1>
      <p class="subtitle">▸ SURVIVAL · CREATIVE · PVP ◂</p>
    </div>

    <div class="mc-card">
      <div class="cc-tr"></div><div class="cc-bl"></div>
      <div class="ip-dual">
        <div class="ip-card">
          <div class="ip-card-label">
            SERVER IP
            <span class="ip-badge badge-bedrock">BEDROCK</span>
          </div>
          <div class="ip-val-row">
            <span class="ip-val" id="ip-bedrock">valorix-nation.my.id</span>
            <button class="copy-btn" onclick="copyIP('ip-bedrock','IP Bedrock')">
              <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="9" y="9" width="13" height="13" rx="2"/><path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"/></svg>
            </button>
          </div>
          <div class="ip-port">Port: 25123</div>
        </div>
        <div class="ip-card">
          <div class="ip-card-label">
            SERVER IP
            <span class="ip-badge badge-java">JAVA</span>
          </div>
          <div class="ip-val-row">
            <span class="ip-val" id="ip-java">25123</span>
            <button class="copy-btn" onclick="copyIP('ip-java','Port')">
              <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="9" y="9" width="13" height="13" rx="2"/><path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"/></svg>
            </button>
          </div>
          <div class="ip-port">Java / Bedrock Edition</div>
        </div>
      </div>
      <button class="join-btn" onclick="copyIP('ip-bedrock','IP Server')">⛏ COPY IP &amp; JOIN SEKARANG!</button>

      <div class="player-status">
        <div class="status-header">
          <span class="status-title">STATUS SERVER</span>
          <button class="refresh-btn" onclick="checkServer()">↻ REFRESH</button>
        </div>
        <div id="motd-box" class="motd-box" style="display:none;"></div>
        <div class="online-indicator" id="statusIndicator">
          <div class="status-dot loading" id="statusDot"></div>
          <div class="online-text">
            <div class="online-status-label" id="statusLabel">Memeriksa server...</div>
            <div class="online-desc" id="statusDesc">Sedang mengambil data</div>
            <div class="loading-bar"><div class="loading-fill" id="loadingFill"></div></div>
          </div>
          <div class="player-count" id="playerCountWrap" style="display:none;">
            <span class="count-number" id="playerCount">0</span>
            <span class="count-label">pemain online</span>
          </div>
        </div>
        <div class="player-list" id="playerList"></div>
      </div>
    </div>
  </div>

  <!-- FEATURES -->
  <div class="section" id="section-features">
    <div class="header">
      <div class="server-badge">⚔ BRUTAL LEGEND</div>
      <h2 class="server-title" style="font-size:clamp(14px,4vw,28px);">ARSENAL<br><span class="title-accent">VALORIX</span></h2>
      <p class="subtitle">▸ SENJATA TERKUAT DI SERVER ◂</p>
    </div>

    <div class="mc-card">
      <div class="cc-tr"></div><div class="cc-bl"></div>
      <div class="features-grid">

        <!-- Sword of Legends -->
        <div class="feature-card">
          <div class="weapon-icon">
            <svg viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg" style="color:#4FE4E4;">
              <rect x="22" y="4" width="4" height="32" rx="1" fill="#4FE4E4"/>
              <polygon points="24,2 26,8 22,8" fill="#88FFFF"/>
              <rect x="14" y="20" width="20" height="3" rx="1" fill="#F5C518"/>
              <rect x="22" y="36" width="4" height="8" rx="1" fill="#8B5E3C"/>
              <rect x="20" y="38" width="8" height="2" rx="1" fill="#5C3A1E"/>
              <line x1="24" y1="4" x2="20" y2="16" stroke="rgba(255,255,255,0.3)" stroke-width="1"/>
            </svg>
          </div>
          <div class="feature-name">SWORD OF LEGENDS</div>
          <div class="feature-desc">Pedang kuno dengan enchant max — satu tebas merobek armor netherite.</div>
        </div>

        <!-- Brutal Axe -->
        <div class="feature-card">
          <div class="weapon-icon">
            <svg viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg" style="color:#FF6B6B;">
              <rect x="23" y="8" width="3" height="34" rx="1" fill="#8B5E3C"/>
              <path d="M26 10 L38 8 L36 22 L26 18 Z" fill="#FF6B6B"/>
              <path d="M26 10 L38 8 L40 4 L28 4 Z" fill="#FF9999"/>
              <line x1="38" y1="8" x2="38" y2="22" stroke="#cc3333" stroke-width="1.5"/>
            </svg>
          </div>
          <div class="feature-name">BRUTAL AXE</div>
          <div class="feature-desc">Kapak brutal enchant Sharpness V + Smite V. Nether mob? Satu ayunan!</div>
        </div>

        <!-- Sniper Bow -->
        <div class="feature-card">
          <div class="weapon-icon">
            <svg viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg" style="color:#00FF88;">
              <path d="M12 8 Q8 24 12 40" stroke="#8B5E3C" stroke-width="3" fill="none" stroke-linecap="round"/>
              <line x1="12" y1="8" x2="12" y2="40" stroke="#00FF88" stroke-width="1.5" stroke-dasharray="3,2"/>
              <line x1="24" y1="24" x2="12" y2="8" stroke="#C8A068" stroke-width="1.5"/>
              <line x1="24" y1="24" x2="12" y2="40" stroke="#C8A068" stroke-width="1.5"/>
              <rect x="22" y="22" width="20" height="4" rx="1" fill="#00FF88"/>
              <polygon points="42,24 38,22 38,26" fill="#88FFAA"/>
            </svg>
          </div>
          <div class="feature-name">SNIPER BOW</div>
          <div class="feature-desc">Busur Power V + Infinity. Tembak musuh dari 200 blok tanpa ketinggalan!</div>
        </div>

        <!-- Dragon Trident -->
        <div class="feature-card">
          <div class="weapon-icon">
            <svg viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg" style="color:#AA44FF;">
              <rect x="22" y="14" width="4" height="30" rx="1" fill="#8844CC"/>
              <polygon points="24,4 20,14 28,14" fill="#AA44FF"/>
              <polygon points="18,8 14,16 20,14" fill="#CC66FF"/>
              <polygon points="30,8 34,16 28,14" fill="#CC66FF"/>
              <rect x="18" y="36" width="12" height="3" rx="1" fill="#5522AA"/>
            </svg>
          </div>
          <div class="feature-name">DRAGON TRIDENT</div>
          <div class="feature-desc">Trisula dengan Riptide III + Channeling. Terbang sambil menyambar petir!</div>
        </div>

        <!-- TNT Cannon -->
        <div class="feature-card">
          <div class="weapon-icon">
            <svg viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg" style="color:#F5C518;">
              <rect x="8" y="18" width="28" height="16" rx="3" fill="#555"/>
              <rect x="10" y="20" width="24" height="12" rx="2" fill="#444"/>
              <ellipse cx="36" cy="26" rx="6" ry="8" fill="#666"/>
              <rect x="14" y="34" width="20" height="5" rx="2" fill="#333"/>
              <circle cx="20" cy="26" r="5" fill="#FF4400"/>
              <text x="18" y="29" font-size="7" fill="white" font-weight="bold">TNT</text>
              <line x1="20" y1="18" x2="20" y2="14" stroke="#F5C518" stroke-width="2"/>
              <circle cx="20" cy="12" r="3" fill="#FFAA00" opacity="0.8"/>
            </svg>
          </div>
          <div class="feature-name">TNT CANNON</div>
          <div class="feature-desc">Meriam TNT custom dengan jangkauan 50 blok. Hancurkan base musuh!</div>
        </div>

        <!-- Soul Blade -->
        <div class="feature-card">
          <div class="weapon-icon">
            <svg viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg" style="color:#00CCFF;">
              <rect x="22" y="4" width="4" height="30" rx="1" fill="#0088AA"/>
              <polygon points="24,2 27,6 24,10 21,6" fill="#00CCFF"/>
              <rect x="14" y="18" width="20" height="3" rx="1" fill="#005566"/>
              <rect x="22" y="34" width="4" height="10" rx="1" fill="#444"/>
              <circle cx="18" cy="12" r="2" fill="#00FFFF" opacity="0.6"/>
              <circle cx="30" cy="8" r="1.5" fill="#00FFFF" opacity="0.5"/>
              <circle cx="26" cy="20" r="1" fill="#00FFFF" opacity="0.7"/>
            </svg>
          </div>
          <div class="feature-name">SOUL BLADE</div>
          <div class="feature-desc">Pedang jiwa dari dimensi Nether. Mencuri nyawa musuh setiap serangan.</div>
        </div>

      </div>
    </div>
  </div>

  <!-- GALLERY -->
  <div class="section" id="section-gallery">
    <div class="header">
      <div class="server-badge">📸 MOMEN EPIK</div>
      <h2 class="server-title" style="font-size:clamp(14px,4vw,28px);">GALERI<br><span class="title-accent">VALORIX</span></h2>
      <p class="subtitle">▸ SCREENSHOT TERBAIK SERVER ◂</p>
    </div>

    <div class="mc-card">
      <div class="cc-tr"></div><div class="cc-bl"></div>
      <div class="gallery-grid" id="galleryGrid">
        <!-- JS populated -->
      </div>
    </div>
  </div>

  <!-- PANDUAN -->
  <div class="section" id="section-panduan">
    <div class="header">
      <div class="server-badge">📖 TUTORIAL</div>
      <h2 class="server-title" style="font-size:clamp(14px,4vw,28px);">PANDUAN<br><span class="title-accent">BERMAIN</span></h2>
      <p class="subtitle">▸ CARA BERMAIN DI SERVER ◂</p>
    </div>
    
    <div class="mc-card">
      <div class="cc-tr"></div><div class="cc-bl"></div>
      <div class="guides-container">

        <!-- CLAIM LANE -->
        <div class="guide-card">
          <div class="guide-icon">🏗️</div>
          <div class="guide-title">Claim Lane</div>
          <div class="guide-desc">
            <p>Claim lane adalah area pribadi untuk bermain. Caranya sangat mudah:</p>
            <ol class="guide-steps">
              <li><strong>Pilih area</strong> yang ingin kamu gunakan di dunia Survival</li>
              <li><strong>Pasang pagar</strong> di sekeliling area tersebut sebagai penanda batas</li>
              <li><strong>Pasang sign</strong> bertuliskan <code>[rp]</code> di dekat pagar</li>
              <li><strong>Selesai!</strong> Area kamu sudah ter-claim dan aman dari gangguan pemain lain</li>
            </ol>
            <p class="guide-tip">💡 <strong>Tip:</strong> Semakin bagus desain pagar kamu, semakin keren penampilannya!</p>
          </div>
        </div>

        <!-- SURVIVAL -->
        <div class="guide-card">
          <div class="guide-icon">🌍</div>
          <div class="guide-title">Mode Survival</div>
          <div class="guide-desc">
            <p>Survival adalah mode klasik Minecraft. Untuk memulai:</p>
            <ol class="guide-steps">
              <li><strong>Ketik perintah</strong> <code>/rtp</code> untuk teleport random ke lokasi aman</li>
              <li><strong>Atau kunjungi NPC</strong> di Lobby yang bernama "RTP" untuk teleport</li>
              <li><strong>Mulai berkembang</strong> dengan menambang, berburu, dan berbisnis</li>
              <li><strong>Buka toko</strong> dengan ketik <code>/shop</code> atau bicara ke NPC "Shop" di Lobby untuk mulai berdagang</li>
            </ol>
            <p class="guide-tip">💡 <strong>Tip:</strong> Semakin banyak kamu berdagang, semakin kaya uangmu!</p>
          </div>
        </div>

        <!-- ONE BLOCK -->
        <div class="guide-card">
          <div class="guide-icon">📦</div>
          <div class="guide-title">One Block Challenge</div>
          <div class="guide-desc">
            <p>One Block adalah gamemode unik dimana kamu hanya punya 1 block untuk digali. Semakin banyak digali, semakin banyak resource yang muncul!</p>
            <ol class="guide-steps">
              <li><strong>Ketik perintah</strong> <code>/ob join</code> untuk mulai One Block</li>
              <li><strong>Atau kunjungi NPC</strong> di Lobby yang bernama "One Block" untuk join</li>
              <li><strong>Gali block</strong> terus-menerus untuk mendapatkan berbagai item</li>
              <li><strong>Kumpulkan resources</strong> dan bangun island kamu sendiri</li>
              <li><strong>Naik level</strong> dan dapatkan hadiah eksklusif saat mencapai milestone</li>
            </ol>
            <p class="guide-tip">💡 <strong>Tip:</strong> Jangan lupa harvest resources dengan cermat untuk efisiensi maksimal!</p>
          </div>
        </div>

      </div>
    </div>
  </div>

  <!-- EVENT -->
  <div class="section" id="section-event">
    <div class="header">
      <div class="server-badge">🎉 ACARA SPESIAL</div>
      <h2 class="server-title" style="font-size:clamp(14px,4vw,28px);">EVENT<br><span class="title-accent">TERBARU</span></h2>
      <p class="subtitle">▸ IKUTI EVENT DAN MENANG HADIAH ◂</p>
    </div>
    
    <div class="mc-card">
      <div class="cc-tr"></div><div class="cc-bl"></div>
      <div class="events-container">

        <!-- EVENT IDUL ADHA -->
        <div class="event-card featured">
          <div class="event-image-wrap">
            <img src="https://i.imgur.com/4gWvelC.png" alt="Event Idul Adha" class="event-image"/>
            <div class="event-badge">🎊 SPESIAL</div>
          </div>
          <div class="event-content">
            <div class="event-title-wrap">
              <h3 class="event-title">🐑 IDUL ADHA SPECIAL</h3>
              <div class="event-date">📅 26 Mei 2026 | 20.00 WIB— Malam Hari</div>
            </div>
            <p class="event-description">
              Rayakan Idul Adha bersama Valorix Nation! Event spesial dengan mini-games seru dan kompetisi yang penuh tantangan. 
            </p>
            <div class="event-details">
              <div class="event-detail-item">
                <span class="detail-label">🎁 HADIAH UTAMA:</span>
                <span class="detail-value">Senjata Brutal Legend Eksklusif</span>
              </div>
              <div class="event-detail-item">
                <span class="detail-label">⏰ WAKTU:</span>
                <span class="detail-value">26 Mei 2026 — Malam Hari</span>
              </div>
              <div class="event-detail-item">
                <span class="detail-label">👥 PESERTA:</span>
                <span class="detail-value">Semua pemain server Valorix Nation</span>
              </div>
            </div>
            <p class="event-rules">
              <strong>📌 Cara Ikutan:</strong> Datang ke lobby server pada waktu yang ditentukan dan ikuti mini-games menarik. Pemenang akan mendapatkan senjata brutal legend yang keren!
            </p>
          </div>
        </div>

      </div>
    </div>
  </div>

  <!-- SOCIAL -->
  <div class="section" id="section-social">
    <div class="header">
      <div class="server-badge">📢 KOMUNITAS</div>
      <h2 class="server-title" style="font-size:clamp(14px,4vw,28px);">SOSIAL<br><span class="title-accent">MEDIA</span></h2>
      <p class="subtitle">▸ GABUNG KOMUNITAS KAMI ◂</p>
    </div>

    <div class="mc-card" style="margin-bottom:0;">
      <div class="cc-tr"></div><div class="cc-bl"></div>
      <div class="social-grid">
        <a href="https://chat.whatsapp.com/Fzh6XsvTnWQ3RvrahXlVV5?s=cl&p=a&ilr=2" target="_blank" class="social-card wa">
          <div class="social-icon-wrap wa-ico">
            <svg class="social-icon" viewBox="0 0 24 24" fill="#25D366"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
          </div>
          <div class="social-info">
            <div class="social-platform wa-txt">GRUP WHATSAPP</div>
            <div class="social-handle">Valorix Nation Community</div>
            <span class="social-action wa-act">🔗 Gabung Grup →</span>
          </div>
          <span class="social-arrow">›</span>
        </a>

        <a href="https://tiktok.com/@valorixnation" target="_blank" class="social-card tt">
          <div class="social-icon-wrap tt-ico">
            <svg class="social-icon" viewBox="0 0 24 24" fill="white"><path d="M19.59 6.69a4.83 4.83 0 01-3.77-4.25V2h-3.45v13.67a2.89 2.89 0 01-2.88 2.5 2.89 2.89 0 01-2.89-2.89 2.89 2.89 0 012.89-2.89c.28 0 .54.04.79.1V9.01a6.27 6.27 0 00-.79-.05 6.34 6.34 0 00-6.34 6.34 6.34 6.34 0 006.34 6.34 6.34 6.34 0 006.33-6.34V8.69a8.18 8.18 0 004.79 1.54V6.78a4.85 4.85 0 01-1.02-.09z"/></svg>
          </div>
          <div class="social-info">
            <div class="social-platform tt-txt">TIKTOK</div>
            <div class="social-handle">@valorixnation</div>
                <span class="social-action tt-act">Lihat Konten →</span>
          </div>
          <span class="social-arrow">›</span>
        </a>
      </div>
    </div>
  </div>

  <!-- STAFF -->
  <div class="section" id="section-staff">
    <div class="header">
      <div class="server-badge">👑 TIM VALORIX</div>
      <h2 class="server-title" style="font-size:clamp(14px,4vw,28px);">STAFF<br><span class="title-accent">TEAM</span></h2>
      <p class="subtitle">▸ PENGURUS SERVER VALORIX ◂</p>
    </div>

    <div class="mc-card">
      <div class="cc-tr"></div><div class="cc-bl"></div>
      <div class="staff-grid">

        <!-- OWNER -->
        <div class="staff-card owner">
          <span class="staff-crown">👑</span>
          <div class="staff-avatar owner-av">F</div>
          <div class="staff-info">
            <span class="staff-role-badge badge-owner">OWNER</span>
            <div class="staff-name">Fadlangemer</div>
            <div class="staff-contact">
              <a href="https://wa.me/6285755152817" target="_blank">085755152817 · WA ›</a>
            </div>
          </div>
        </div>

        <!-- ADMIN -->
        <div class="staff-card admin">
          <div class="staff-avatar admin-av">L</div>
          <div class="staff-info">
            <span class="staff-role-badge badge-admin">ADMIN</span>
            <div class="staff-name">Lalo</div>
            <div class="staff-contact">Admin Server Valorix Nation</div>
          </div>
        </div>

        <!-- HELPER 1 -->
        <div class="staff-card helper">
          <div class="staff-avatar helper-av">F</div>
          <div class="staff-info">
            <span class="staff-role-badge badge-helper">HELPER</span>
            <div class="staff-name">fullower</div>
            <div class="staff-contact">Helper · Siap bantu pemain baru</div>
          </div>
        </div>

        <!-- HELPER 2 -->
        <div class="staff-card helper">
          <div class="staff-avatar helper-av">P</div>
          <div class="staff-info">
            <span class="staff-role-badge badge-helper">HELPER</span>
            <div class="staff-name">Petirisback</div>
            <div class="staff-contact">Helper · Siap bantu pemain baru</div>
          </div>
        </div>

      </div>
    </div>
  </div>

  <!-- RANK -->
  <div class="section" id="section-rank">
    <div class="header">
      <div class="server-badge">💎 DONASI RANK</div>
      <h2 class="server-title" style="font-size:clamp(14px,4vw,28px);">RANK<br><span class="title-accent">VALORIX</span></h2>
      <p class="subtitle">▸ PILIH RANK TERBAIKMU ◂</p>
    </div>
    <div class="rank-grid">

      <!-- VIP -->
      <div class="rank-card rank-vip">
        <div class="rank-header-bar">
          <span class="rank-icon">✨</span>
          <span class="rank-name">VIP</span>
          <span class="rank-price">Rp 10.000</span>
        </div>
        <ul class="rank-perks">
          <li>🏠 /sethome (3 slot)</li>
          <li>👥 /team create</li>
          <li>🍗 /feed</li>
          <li>🔧 /anvil</li>
          <li>🎁 /kit VIP</li>
          <li>💵 20k Money</li>
          <li>🪙 25 Coins</li>
        </ul>
        <a href="https://wa.me/6285755152817?text=Halo+Kak+Fadlan%2C+saya+mau+beli+rank+VIP+di+server+Valorix+Nation.+Boleh+info+lebih+lanjut%3F" target="_blank" class="rank-buy-btn vip-btn">🛒 BELI SEKARANG</a>
      </div>

      <!-- VIP+ -->
      <div class="rank-card rank-vipp">
        <div class="rank-header-bar">
          <span class="rank-icon">🩵</span>
          <span class="rank-name">VIP+</span>
          <span class="rank-price">Rp 25.000</span>
        </div>
        <ul class="rank-perks">
          <li>🎭 /Nick</li>
          <li>🕊️ /Fly</li>
          <li>🏠 /sethome (5 slot)</li>
          <li>💵 30k Money</li>
          <li>🪙 50 Coins</li>
          <li>⚔️ Free Senjata Legendaris</li>
        </ul>
        <a href="https://wa.me/6285755152817?text=Halo+Kak+Fadlan%2C+saya+mau+beli+rank+VIP%2B+di+server+Valorix+Nation.+Boleh+info+lebih+lanjut%3F" target="_blank" class="rank-buy-btn vipp-btn">🛒 BELI SEKARANG</a>
      </div>

      <!-- MVP+ -->
      <div class="rank-card rank-mvp">
        <div class="rank-badge-sale">DISKON</div>
        <div class="rank-header-bar">
          <span class="rank-icon">💜</span>
          <span class="rank-name">MVP+</span>
          <span class="rank-price">Rp 40.000</span>
        </div>
        <ul class="rank-perks">
          <li>🏠 /sethome (20 slot)</li>
          <li>📦 /ec</li>
          <li>🕊️ /fly</li>
          <li>🎭 /nick</li>
          <li>🔧 /repair</li>
          <li>⚒️ /anvil</li>
          <li>🎁 /kit legend</li>
          <li>💵 40k Money</li>
          <li>🪙 70 Coins</li>
          <li>⚔️ Free Senjata Legendaris</li>
        </ul>
        <a href="https://wa.me/6285755152817?text=Halo+Kak+Fadlan%2C+saya+mau+beli+rank+MVP%2B+di+server+Valorix+Nation.+Boleh+info+lebih+lanjut%3F" target="_blank" class="rank-buy-btn mvp-btn">🛒 BELI SEKARANG</a>
      </div>

      <!-- LEGEND -->
      <div class="rank-card rank-legend">
        <div class="rank-badge-sale">DISKON</div>
        <div class="rank-header-bar">
          <span class="rank-icon">💛</span>
          <span class="rank-name">LEGEND</span>
          <span class="rank-price">Rp 60.000</span>
        </div>
        <ul class="rank-perks">
          <li>🏠 /sethome (30 slot)</li>
          <li>📦 /ec</li>
          <li>💣 /beezooka</li>
          <li>🍗 /feed</li>
          <li>🕊️ /fly</li>
          <li>🎭 /nick</li>
          <li>❤️ /heal</li>
          <li>🔧 /repair</li>
          <li>🎁 /kit sultan</li>
          <li>🌤️ /day · 🌙 /night · ☀️ /sun</li>
          <li>💵 55k Money</li>
          <li>🪙 70 Coins</li>
          <li>⚔️ Free Senjata Legendaris</li>
        </ul>
        <a href="https://wa.me/6285755152817?text=Halo+Kak+Fadlan%2C+saya+mau+beli+rank+LEGEND+di+server+Valorix+Nation.+Boleh+info+lebih+lanjut%3F" target="_blank" class="rank-buy-btn legend-btn">🛒 BELI SEKARANG</a>
      </div>

      <!-- DECKHAND -->
      <div class="rank-card rank-deckhand">
        <div class="rank-header-bar">
          <span class="rank-icon">⚓</span>
          <span class="rank-name">DECKHAND</span>
          <span class="rank-price">Rp 80.000</span>
        </div>
        <ul class="rank-perks">
          <li>🏠 /sethome (50 slot)</li>
          <li>📦 /ec</li>
          <li>🍗 /feed</li>
          <li>🕊️ /fly</li>
          <li>🔧 /repair</li>
          <li>🎭 /nick</li>
          <li>❤️ /heal</li>
          <li>🛠️ /craft</li>
          <li>👤 /head</li>
          <li>💣 /beezooka</li>
          <li>🎁 /kit supreme</li>
          <li>🌙 /nv (nightvision)</li>
          <li>💵 100k Money</li>
          <li>🪙 100 Coins</li>
          <li>⚔️ Free Senjata Legendaris</li>
        </ul>
        <a href="https://wa.me/6285755152817?text=Halo+Kak+Fadlan%2C+saya+mau+beli+rank+DECKHAND+di+server+Valorix+Nation.+Boleh+info+lebih+lanjut%3F" target="_blank" class="rank-buy-btn deckhand-btn">🛒 BELI SEKARANG</a>
      </div>

      <!-- VISCOUNT -->
      <div class="rank-card rank-viscount">
        <div class="rank-header-bar">
          <span class="rank-icon">♠</span>
          <span class="rank-name">VISCOUNT</span>
          <span class="rank-price">Rp 140.000</span>
        </div>
        <ul class="rank-perks">
          <li>🏠 /sethome (80 slot)</li>
          <li>🫥 /vanish</li>
          <li>🎁 /kit jendral</li>
          <li>💵 250k Money</li>
          <li>🪙 200 Coins</li>
          <li>⚔️ Free Senjata Legendaris</li>
        </ul>
        <a href="https://wa.me/6285755152817?text=Halo+Kak+Fadlan%2C+saya+mau+beli+rank+VISCOUNT+di+server+Valorix+Nation.+Boleh+info+lebih+lanjut%3F" target="_blank" class="rank-buy-btn viscount-btn">🛒 BELI SEKARANG</a>
      </div>

    </div>
  </div>

  <!-- LAPOR -->
  <div class="section" id="section-lapor">
    <div class="header">
      <div class="server-badge">🚨 ADUAN PEMAIN</div>
      <h2 class="server-title" style="font-size:clamp(14px,4vw,28px);">LAPOR<br><span class="title-accent">MASALAH</span></h2>
      <p class="subtitle">▸ LAPORKAN KE OWNER / STAFF ◂</p>
    </div>
    <div class="mc-card">
      <div class="cc-tr"></div><div class="cc-bl"></div>
      <p style="font-family:'VT323',monospace;font-size:16px;color:rgba(200,230,255,.6);letter-spacing:1px;margin-bottom:18px;line-height:1.6;">Tulis laporanmu di bawah — setelah klik Kirim kamu akan diarahkan ke WhatsApp Owner dengan pesannya sudah terisi otomatis.</p>

      <div class="lapor-form">
        <div class="lapor-field">
          <label class="lapor-label">Nama IGN (In-Game Name)</label>
          <input type="text" id="laporIGN" class="lapor-input" placeholder="Nama kamu di server..."/>
        </div>
        <div class="lapor-field">
          <label class="lapor-label">Jenis Laporan</label>
          <select id="laporJenis" class="lapor-input lapor-select">
            <option value="Laporan Cheater/Hacker">🎮 Cheater / Hacker</option>
            <option value="Laporan Bug/Glitch">🐛 Bug / Glitch</option>
            <option value="Laporan Toxic/Spam">💬 Pemain Toxic / Spam</option>
            <option value="Laporan Item Hilang">📦 Item Hilang</option>
            <option value="Laporan Lainnya">⚠️ Lainnya</option>
          </select>
        </div>
        <div class="lapor-field">
          <label class="lapor-label">Detail Laporan</label>
          <textarea id="laporDetail" class="lapor-input lapor-textarea" placeholder="Ceritakan secara detail kejadiannya — siapa yang terlibat, kapan terjadi, apa yang terjadi..."></textarea>
        </div>
        <button class="lapor-btn" onclick="kirimLaporan()">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" style="vertical-align:middle;margin-right:8px;"><line x1="22" y1="2" x2="11" y2="13"/><polygon points="22 2 15 22 11 13 2 9 22 2"/></svg>
          KIRIM VIA WHATSAPP
        </button>
      </div>
    </div>
  </div>

  </div><!-- end page-wrapper -->
</div>

<script>
// ===== NAV ORDER =====
const sectionOrder = ['home','features','gallery','rank','panduan','event','social','staff','lapor'];
let currentSectionIndex = 0;

// ===== STARS =====
const starsEl = document.getElementById('stars');
for(let i=0;i<90;i++){
  const s=document.createElement('div');
  s.className='star';
  const size=Math.random()*2.5+.5;
  s.style.cssText=`width:${size}px;height:${size}px;top:${Math.random()*100}%;left:${Math.random()*100}%;--d:${2+Math.random()*4}s;animation-delay:${Math.random()*4}s;`;
  starsEl.appendChild(s);
}

// ===== CLOUDS =====
const cloudsEl=document.getElementById('clouds');
function makeCloud(){
  const c=document.createElement('div');
  c.className='cloud';
  const w=60+Math.random()*80,h=w*0.5;
  const dur=20+Math.random()*30;
  c.style.cssText=`top:${Math.random()*120}px;animation-duration:${dur}s;animation-delay:-${Math.random()*dur}s;`;
  c.innerHTML=`<svg width="${w}" height="${h}" viewBox="0 0 60 30" fill="white" xmlns="http://www.w3.org/2000/svg"><rect x="10" y="15" width="40" height="15"/><rect x="5" y="10" width="25" height="20"/><rect x="25" y="5" width="20" height="25"/></svg>`;
  cloudsEl.appendChild(c);
}
for(let i=0;i<6;i++) makeCloud();

// ===== GALLERY =====
const galleryPhotos = [
  { src: 'https://i.imgur.com/6IRXH14.jpeg', caption: 'SCREENSHOT 1' },
  { src: 'https://i.imgur.com/b7nixkA.jpeg', caption: 'SCREENSHOT 2' },
  { src: 'https://i.imgur.com/0cvSkYi.jpeg', caption: 'SCREENSHOT 3' },
  { src: 'https://i.imgur.com/17Yny4R.jpeg', caption: 'SCREENSHOT 4' },
  { src: 'https://i.imgur.com/wXFxLgY.jpeg', caption: 'SCREENSHOT 5' },
];
let lightboxIndex = 0;

function buildGallery(){
  const grid = document.getElementById('galleryGrid');
  grid.innerHTML = '';
  galleryPhotos.forEach((p, i) => {
    const item = document.createElement('div');
    item.className = 'gallery-item';
    item.innerHTML = `<img src="${p.src}" alt="${p.caption}" loading="lazy"/>
      <div class="gallery-overlay">${p.caption}</div>`;
    item.onclick = () => openLightbox(i);
    grid.appendChild(item);
  });
}
buildGallery();

function openLightbox(idx){
  lightboxIndex = idx;
  const lb = document.getElementById('lightbox');
  lb.classList.add('open');
  updateLightbox();
  document.body.style.overflow='hidden';
}
function closeLightbox(){
  document.getElementById('lightbox').classList.remove('open');
  document.body.style.overflow='';
}
function updateLightbox(){
  document.getElementById('lightboxImg').src = galleryPhotos[lightboxIndex].src;
  document.getElementById('lbCounter').textContent = `${lightboxIndex+1} / ${galleryPhotos.length}`;
}
function lbPrev(){ lightboxIndex=(lightboxIndex-1+galleryPhotos.length)%galleryPhotos.length; updateLightbox(); }
function lbNext(){ lightboxIndex=(lightboxIndex+1)%galleryPhotos.length; updateLightbox(); }
document.getElementById('lightbox').addEventListener('click', function(e){
  if(e.target===this) closeLightbox();
});
document.addEventListener('keydown', function(e){
  if(!document.getElementById('lightbox').classList.contains('open')) return;
  if(e.key==='ArrowLeft') lbPrev();
  if(e.key==='ArrowRight') lbNext();
  if(e.key==='Escape') closeLightbox();
});

// ===== SECTION TRANSITION =====
let isTransitioning = false;

function showSection(name, targetIdx){
  if(isTransitioning) return;
  const currentName = sectionOrder[currentSectionIndex];
  if(currentName === name) return;

  isTransitioning = true;

  const oldSection = document.getElementById('section-' + currentName);
  const newSection = document.getElementById('section-' + name);

  const goingDown = targetIdx > currentSectionIndex;

  // Exit animation for old section
  oldSection.classList.remove('active');
  oldSection.classList.add(goingDown ? 'exit-up' : 'exit-down');

  // After exit, bring in new section
  setTimeout(() => {
    oldSection.classList.remove('exit-up','exit-down');
    oldSection.style.display = 'none';

    newSection.style.display = 'block';
    newSection.classList.remove('active');
    newSection.classList.add('active', goingDown ? 'enter-from-below' : 'enter-from-above');

    currentSectionIndex = targetIdx;

    // Update nav
    document.querySelectorAll('.nav-link').forEach(l=>{
      l.classList.toggle('active', l.dataset.section===name);
    });

    // Close mobile nav
    document.getElementById('navLinks').classList.remove('open');

    setTimeout(()=>{
      newSection.classList.remove('enter-from-below','enter-from-above');
      isTransitioning = false;
    }, 500);

  }, 280);
}

// ===== COPY IP =====
function copyIP(id, label){
  const el=document.getElementById(id);
  if(!el) return;
  navigator.clipboard.writeText(el.textContent.trim()).catch(()=>{});
  showToast('✔ '+label+' disalin!');
}

function showToast(msg){
  const t=document.getElementById('toast');
  t.textContent=msg; t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'),2500);
}

// ===== MOBILE NAV =====
function toggleMobile(){
  const navLinks = document.getElementById('navLinks');
  const navBtn = document.getElementById('navMobileBtn');
  navLinks.classList.toggle('open');
  navBtn.classList.toggle('active');
}

// ===== SERVER CHECK =====
async function checkServer(){
  const dot=document.getElementById('statusDot');
  const label=document.getElementById('statusLabel');
  const desc=document.getElementById('statusDesc');
  const fill=document.getElementById('loadingFill');
  const pcWrap=document.getElementById('playerCountWrap');
  const pc=document.getElementById('playerCount');
  const pl=document.getElementById('playerList');
  const motd=document.getElementById('motd-box');

  dot.className='status-dot loading';
  label.textContent='Memeriksa server...';
  label.style.color='';
  desc.textContent='Mohon tunggu sebentar';
  if(fill) fill.style.display='block';
  pcWrap.style.display='none';
  pl.innerHTML=''; motd.style.display='none';

  const SERVER_IP = 'valorix-nation.my.id';
  const SERVER_PORT = '25123';

  // Try primary API: mcsrvstat v3
  async function tryMcsrvstat(){
    const r = await fetch(`https://api.mcsrvstat.us/3/${SERVER_IP}:${SERVER_PORT}`, {signal: AbortSignal.timeout(8000)});
    if(!r.ok) throw new Error('HTTP '+r.status);
    return await r.json();
  }

  // Try fallback API: mcstatus.io
  async function tryMcstatus(){
    const r = await fetch(`https://api.mcstatus.io/v2/status/java/${SERVER_IP}:${SERVER_PORT}`, {signal: AbortSignal.timeout(8000)});
    if(!r.ok) throw new Error('HTTP '+r.status);
    const d = await r.json();
    // normalize to mcsrvstat format
    return {
      online: d.online,
      version: d.version?.name_clean || d.version?.name,
      players: { online: d.players?.online, max: d.players?.max, list: d.players?.list?.map(p=>p.name_clean||p.name) },
      motd: { clean: [d.motd?.clean] }
    };
  }

  if(fill) fill.style.display='none';
  try{
    let d;
    try { d = await tryMcsrvstat(); }
    catch(e) {
      console.warn('mcsrvstat failed, trying mcstatus.io:', e);
      d = await tryMcstatus();
    }

    if(d && d.online){
      dot.className='status-dot online';
      label.textContent='🟢 SERVER ONLINE';
      label.style.color='var(--neon)';
      const ver = d.version || '?';
      desc.textContent=`Versi: ${ver} · IP: ${SERVER_IP}:${SERVER_PORT}`;
      pcWrap.style.display='block';
      const cur=d.players?.online||0, max=d.players?.max||20;
      pc.textContent=cur+'/'+max;
      if(d.motd?.clean && d.motd.clean[0]){
        motd.textContent=d.motd.clean[0];
        motd.style.display='block';
      }
      const plist = d.players?.list;
      if(plist && plist.length){
        pl.innerHTML=plist.map(p=>{
          const name = typeof p==='string'?p:(p.name_clean||p.name||p);
          return `<div class="player-tag">
            <img class="player-head" src="https://mc-heads.net/avatar/${name}/15" alt="" onerror="this.style.display='none'"/>
            ${name}</div>`;
        }).join('');
      } else {
        pl.innerHTML='<div class="no-players">[ Tidak ada pemain online saat ini ]</div>';
      }
    } else {
      dot.className='status-dot offline';
      label.textContent='🔴 SERVER OFFLINE';
      label.style.color='#ff6666';
      desc.textContent=`${SERVER_IP}:${SERVER_PORT} tidak dapat dijangkau`;
      pl.innerHTML='<div class="no-players">[ Server sedang offline atau maintenance ]</div>';
    }
  }catch(e){
    dot.className='status-dot offline';
    label.textContent='⚠ GAGAL MENGECEK';
    label.style.color='var(--gold)';
    desc.textContent='Error: '+e.message+' — coba refresh';
    pl.innerHTML='<div class="no-players">[ Gagal koneksi ke API ]</div>';
  }
}
checkServer();

// ===== TREES =====
(function makeTrees(){
  const treesEl = document.getElementById('trees');
  const treeCount = Math.floor(window.innerWidth / 80) + 4;
  const positions = [];
  for(let i=0;i<treeCount;i++){
    let x, tries=0, ok=false;
    do { x=Math.random()*95; ok=positions.every(p=>Math.abs(p-x)>4); tries++; } while(!ok && tries<30);
    positions.push(x);
    const h = 60+Math.random()*50;
    const trunkW = 10+Math.random()*4;
    const leavesW = 28+Math.random()*20;
    const leavesH = 24+Math.random()*18;
    const lColor = ['#2d7a1e','#3d9e2f','#1a6010','#4ab830'][Math.floor(Math.random()*4)];
    const lColor2 = ['#236015','#2e7a22','#155010','#3da025'][Math.floor(Math.random()*4)];
    const trunkColor = '#5C3A1E';
    const div = document.createElement('div');
    div.style.cssText=`position:absolute;bottom:0;left:${x}%;transform:translateX(-50%);`;
    div.innerHTML=`<svg width="${leavesW+10}" height="${h}" viewBox="0 0 ${leavesW+10} ${h}" xmlns="http://www.w3.org/2000/svg" style="image-rendering:pixelated;">
     <rect x="${(leavesW+10)/2-trunkW/2}" y="${h-28}" width="${trunkW}" height="28" fill="${trunkColor}"/>
      <rect x="${(leavesW+10)/2-trunkW/2+2}" y="${h-28}" width="3" height="28" fill="#4a2e14"/>
      <!-- leaves layer 3 (bottom) -->
      <rect x="${(leavesW+10)/2-leavesW/2}" y="${h-28-leavesH*0.5}" width="${leavesW}" height="${leavesH*0.6}" fill="${lColor}"/>
      <!-- leaves layer 2 -->
      <rect x="${(leavesW+10)/2-leavesW*0.7/2}" y="${h-28-leavesH*0.85}" width="${leavesW*0.7}" height="${leavesH*0.55}" fill="${lColor2}"/>
      <!-- leaves layer 1 (top) -->
      <rect x="${(leavesW+10)/2-leavesW*0.4/2}" y="${h-28-leavesH*1.1}" width="${leavesW*0.4}" height="${leavesH*0.45}" fill="${lColor}"/>
    </svg>`;
    treesEl.appendChild(div);
  }
})();

// ===== INTRO ANIMATION =====
function initIntro(){
  const overlay = document.getElementById('introOverlay');
  const particles = document.getElementById('introParticles');
  const blocks = document.getElementById('introBlocks');

  // Create particles
  for(let i=0;i<30;i++){
    const p = document.createElement('div');
    p.className = 'intro-particle';
    const s = Math.random()*3+2;
    p.style.cssText=`width:${s}px;height:${s}px;left:${Math.random()*100}%;top:${Math.random()*100}%;--d:${1+Math.random()*2}s;animation-duration:${2+Math.random()*2}s;animation-delay:${Math.random()*2}s;`;
    particles.appendChild(p);
  }

  // Create pixel blocks
  setTimeout(()=>{
    for(let i=0;i<15;i++){
      const block = document.createElement('div');
      block.className = 'intro-block';
      const size = 30+Math.random()*40;
      block.style.cssText=`width:${size}px;height:${size}px;left:${Math.random()*100}%;top:${Math.random()*100}%;animation-delay:${.1+Math.random()*.4}s;`;
      blocks.appendChild(block);
    }
  }, 1800);

  // Auto fadeout
  setTimeout(()=>skipIntro(), 4500);
}

function skipIntro(){
  const overlay = document.getElementById('introOverlay');
  if(overlay) overlay.style.animation='none';
  overlay.style.opacity='0';
  setTimeout(()=>overlay.remove(), 300);
}

initIntro();

// ===== LAPOR FUNCTION =====
function kirimLaporan(){
  const ign = document.getElementById('laporIGN').value.trim();
  const jenis = document.getElementById('laporJenis').value;
  const detail = document.getElementById('laporDetail').value.trim();

  if(!ign || !detail){
    showToast('⚠ Isi semua field dulu!');
    return;
  }

  const pesan = `${jenis}%0A%0ANama IGN: ${encodeURIComponent(ign)}%0A%0ADetail:%0A${encodeURIComponent(detail)}%0A%0A—%0ALaporan dikirim dari Valorix Nation Website`;
  window.open(`https://wa.me/6285755152817?text=${pesan}`, '_blank');

  // Clear form
  document.getElementById('laporIGN').value = '';
  document.getElementById('laporDetail').value = '';
  showToast('✔ Pesan siap dikirim ke WhatsApp!');
}
</script>
</body>
</html>
      
