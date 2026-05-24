<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0"/>
<title>Preet Sidhu — Visual Creator</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400;1,600&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;}
html{scroll-behavior:smooth;}
body{
  background:#000;color:#fff;
  font-family:'DM Mono',monospace;
  font-size:14px;line-height:1.7;
  overflow-x:hidden;cursor:none;
}
img,video{max-width:100%;display:block;}
a{color:inherit;text-decoration:none;}

/* CURSOR */
.cursor{
  position:fixed;width:12px;height:12px;background:#fff;border-radius:50%;
  pointer-events:none;z-index:9999;transform:translate(-50%,-50%);
  transition:width .2s,height .2s;mix-blend-mode:difference;
}
.cursor-ring{
  position:fixed;width:36px;height:36px;border:1px solid rgba(255,255,255,.4);border-radius:50%;
  pointer-events:none;z-index:9998;transform:translate(-50%,-50%);
  transition:width .2s,height .2s,border-color .2s;
}

/* GRAIN */
.grain{
  position:fixed;inset:0;z-index:9990;pointer-events:none;opacity:.12;
  background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
  background-repeat:repeat;background-size:200px 200px;
  animation:grainShift .08s steps(1) infinite;
}
@keyframes grainShift{
  0%{background-position:0 0;}10%{background-position:-5% -10%;}
  20%{background-position:-15% 5%;}30%{background-position:7% -25%;}
  40%{background-position:-5% 25%;}50%{background-position:-15% 10%;}
  60%{background-position:15% 0%;}70%{background-position:0 15%;}
  80%{background-position:3% 35%;}90%{background-position:-10% 10%;}
  100%{background-position:0 0;}
}

/* NAV */
nav{
  position:fixed;top:0;left:0;right:0;z-index:1000;
  padding:1.4rem 3rem;display:flex;justify-content:space-between;align-items:center;
}
nav::before{
  content:'';position:absolute;inset:0;
  background:linear-gradient(to bottom,rgba(0,0,0,.8),transparent);
  backdrop-filter:blur(8px);-webkit-backdrop-filter:blur(8px);z-index:-1;
}
.nav-logo{
  font-family:'Cormorant Garamond',serif;font-size:1.6rem;
  font-weight:300;letter-spacing:.08em;color:#fff;cursor:pointer;
}
.nav-logo span{font-style:italic;}
.nav-links{display:flex;gap:1.6rem;list-style:none;align-items:center;flex-wrap:wrap;}
.nav-links a{
  font-size:9px;letter-spacing:.18em;text-transform:uppercase;
  color:rgba(255,255,255,.45);transition:color .25s;position:relative;
}
.nav-links a::after{
  content:'';position:absolute;bottom:-4px;left:0;right:0;height:1px;
  background:currentColor;transform:scaleX(0);transform-origin:right;transition:transform .3s ease;
}
.nav-links a:hover{color:#fff;}
.nav-links a:hover::after{transform:scaleX(1);transform-origin:left;}

/* PAGE SYSTEM */
.page{display:none;min-height:100vh;position:relative;overflow:hidden;}
.page.active{display:block;}

/* CURTAIN */
.page-curtain{
  position:fixed;inset:0;z-index:2000;background:#000;
  transform:translateY(-100%);pointer-events:none;
}
.page-curtain.in{animation:curtainIn .5s cubic-bezier(.76,0,.24,1) forwards;}
.page-curtain.out{animation:curtainOut .5s cubic-bezier(.76,0,.24,1) forwards;}
@keyframes curtainIn{from{transform:translateY(100%);}to{transform:translateY(0);}}
@keyframes curtainOut{from{transform:translateY(0);}to{transform:translateY(-100%);}}

/* REVEAL */
.reveal{opacity:0;transform:translateY(40px);transition:opacity .9s ease,transform .9s ease;}
.reveal.visible{opacity:1;transform:none;}

/* ══════════════════════════════
   HOME PAGE
══════════════════════════════ */
#page-home{background:#000;}
#page-home.active{display:flex;flex-direction:column;}

/* Glow effects on hero */
.hero-bg{
  position:absolute;inset:0;z-index:0;
  background:
    radial-gradient(ellipse 55% 55% at 15% 25%, rgba(255,255,255,.07) 0%, transparent 60%),
    radial-gradient(ellipse 45% 45% at 85% 75%, rgba(255,255,255,.05) 0%, transparent 55%),
    radial-gradient(ellipse 30% 40% at 50% 50%, rgba(180,180,180,.04) 0%, transparent 50%),
    #000;
}
.hero-glow{
  position:absolute;inset:0;z-index:1;
  background:
    radial-gradient(ellipse 70% 50% at 50% 0%, rgba(255,255,255,.06) 0%, transparent 60%),
    radial-gradient(ellipse 40% 30% at 0% 100%, rgba(255,255,255,.04) 0%, transparent 50%);
  animation:glowPulse 6s ease-in-out infinite alternate;
}
@keyframes glowPulse{
  0%{opacity:.6;}
  100%{opacity:1;}
}
.hero-scanlines{
  position:absolute;inset:0;z-index:2;
  background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(255,255,255,.014) 2px,rgba(255,255,255,.014) 4px);
}
.hero-content{
  position:relative;z-index:3;display:flex;flex-direction:column;
  justify-content:flex-end;min-height:88vh;
  padding:0 clamp(2rem,6vw,6rem) clamp(2rem,5vh,4rem);
}
.hero-eyebrow{
  font-size:9px;letter-spacing:.25em;text-transform:uppercase;
  color:rgba(255,255,255,.5);margin-bottom:1.4rem;
  text-shadow:0 0 20px rgba(255,255,255,.3);
}
.hero-name{
  font-family:'Cormorant Garamond',serif;
  font-size:clamp(4.5rem,13vw,11rem);font-weight:300;line-height:.88;letter-spacing:-.02em;
  color:#fff;
  text-shadow:0 0 80px rgba(255,255,255,.18), 0 0 30px rgba(255,255,255,.1);
}
.hero-name em{
  font-style:italic;color:rgba(255,255,255,.55);
  text-shadow:0 0 60px rgba(255,255,255,.15);
}
.hero-tagline-main{
  margin-top:1.8rem;
  font-family:'Cormorant Garamond',serif;
  font-size:clamp(1.05rem,2.3vw,1.6rem);
  font-weight:300;font-style:italic;
  color:rgba(255,255,255,.65);
  max-width:660px;line-height:1.5;letter-spacing:.01em;
  text-shadow:0 0 30px rgba(255,255,255,.15);
}
.hero-divider{
  width:80px;height:1px;
  background:linear-gradient(to right, rgba(255,255,255,.5), transparent);
  margin:2rem 0;
  box-shadow:0 0 10px rgba(255,255,255,.2);
}

/* HOME 8-SECTION GRID */
.hero-nav-grid{
  display:grid;grid-template-columns:repeat(4,1fr);gap:1px;
  border:1px solid rgba(255,255,255,.1);max-width:960px;margin-top:3rem;
  box-shadow:0 0 40px rgba(255,255,255,.04);
}
.hero-nav-item{
  padding:clamp(1.2rem,2.5vh,2rem) clamp(1.2rem,2vw,2rem);
  border-right:1px solid rgba(255,255,255,.08);
  cursor:pointer;transition:background .3s;position:relative;overflow:hidden;
}
.hero-nav-item:last-child{border-right:none;}
.hero-nav-item::before{
  content:'';position:absolute;inset:0;background:rgba(255,255,255,.05);
  transform:translateY(100%);transition:transform .35s ease;
}
.hero-nav-item:hover::before{transform:translateY(0);}
.hero-nav-num{
  font-size:10px;letter-spacing:.16em;
  color:rgba(255,255,255,.28);margin-bottom:.6rem;
}
.hero-nav-label{
  font-family:'Cormorant Garamond',serif;
  font-size:clamp(1rem,1.6vw,1.35rem);
  font-weight:300;color:rgba(255,255,255,.75);line-height:1.2;
}
.hero-nav-label em{font-style:italic;}

/* HOME CONTACT STRIP */
.hero-contact-strip{
  position:relative;z-index:3;
  padding:2.5rem clamp(2rem,6vw,6rem);
  border-top:1px solid rgba(255,255,255,.09);
  display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:1.5rem;
  background:rgba(255,255,255,.015);
}
.home-contact-label{font-size:9px;letter-spacing:.22em;text-transform:uppercase;color:rgba(255,255,255,.3);}
.home-contact-items{display:flex;align-items:center;gap:clamp(1.5rem,4vw,4rem);flex-wrap:wrap;}
.home-contact-item{display:flex;flex-direction:column;gap:.25rem;cursor:pointer;transition:opacity .2s;}
.home-contact-item:hover{opacity:.65;}
.hci-platform{font-size:8px;letter-spacing:.2em;text-transform:uppercase;color:rgba(255,255,255,.32);}
.hci-value{
  font-family:-apple-system,'SF Pro Display','Helvetica Neue',Arial,sans-serif;
  font-size:clamp(1rem,1.7vw,1.3rem);font-weight:300;letter-spacing:.01em;color:#fff;
}
.hci-value em{font-style:italic;color:rgba(255,255,255,.6);}
.hero-bottom{
  position:relative;z-index:3;padding:1.4rem clamp(2rem,6vw,6rem);
  display:flex;justify-content:space-between;align-items:center;
  border-top:1px solid rgba(255,255,255,.05);
}
.hero-bottom-info{font-size:9px;letter-spacing:.14em;color:rgba(255,255,255,.22);}
.scroll-hint{position:absolute;right:3rem;bottom:14rem;display:flex;flex-direction:column;align-items:center;gap:.6rem;z-index:10;}
.scroll-hint-line{width:1px;height:50px;background:rgba(255,255,255,.18);position:relative;overflow:hidden;}
.scroll-hint-line::after{content:'';position:absolute;top:0;left:0;right:0;height:50%;background:#fff;animation:scrollLine 2s ease-in-out infinite;}
@keyframes scrollLine{0%{transform:translateY(-100%);}100%{transform:translateY(200%);}}
.scroll-hint-text{font-size:8px;letter-spacing:.2em;text-transform:uppercase;color:rgba(255,255,255,.25);writing-mode:vertical-rl;}

/* ══════════════════════════════
   ABOUT PAGE
══════════════════════════════ */
#page-about{background:#050505;}
#page-about.active{display:flex;flex-direction:column;}
.about-inner{
  position:relative;z-index:2;min-height:100vh;
  display:flex;flex-direction:column;justify-content:center;
  padding:clamp(6rem,12vh,9rem) clamp(2rem,6vw,6rem) clamp(3rem,6vh,5rem);
}
.about-grid{
  display:grid;grid-template-columns:1fr 1.3fr;
  gap:clamp(3rem,8vw,8rem);align-items:start;margin-top:2rem;
}
.about-heading{
  font-family:'Cormorant Garamond',serif;
  font-size:clamp(2.8rem,6vw,5.5rem);
  font-weight:300;line-height:1.0;letter-spacing:-.02em;
  position:sticky;top:8rem;
}
.about-heading em{font-style:italic;color:rgba(255,255,255,.35);}
.about-intro{
  font-family:'Cormorant Garamond',serif;
  font-size:clamp(1.2rem,2.2vw,1.65rem);
  font-weight:300;line-height:1.55;color:rgba(255,255,255,.85);margin-bottom:2.2rem;
}
.about-intro strong{color:#fff;font-weight:400;}
.about-body{font-size:13px;color:rgba(255,255,255,.38);line-height:1.95;letter-spacing:.03em;display:flex;flex-direction:column;gap:1.4rem;}
.about-divider{width:40px;height:1px;background:rgba(255,255,255,.15);margin:1.5rem 0;}
.about-skills{display:flex;flex-wrap:wrap;gap:.5rem;margin-top:2rem;}
.about-skill{
  padding:.35rem 1rem;border:1px solid rgba(255,255,255,.1);
  font-size:9px;letter-spacing:.14em;text-transform:uppercase;
  color:rgba(255,255,255,.3);font-family:'Cormorant Garamond',serif;font-style:italic;font-size:13px;
  transition:border-color .2s,color .2s;
}
.about-skill:hover{border-color:rgba(255,255,255,.4);color:rgba(255,255,255,.7);}

/* ══════════════════════════════
   SECTION SHARED
══════════════════════════════ */
.sec-inner{
  position:relative;z-index:2;min-height:100vh;
  display:flex;flex-direction:column;
  padding:clamp(5rem,10vh,8rem) clamp(2rem,6vw,6rem) clamp(2rem,4vh,4rem);
}
.sec-label{
  font-size:9px;letter-spacing:.22em;text-transform:uppercase;
  color:rgba(255,255,255,.38);margin-bottom:1rem;
  display:flex;align-items:center;gap:.8rem;
}
.sec-label::before{content:'';display:inline-block;width:30px;height:1px;background:currentColor;}
.sec-title{
  font-family:'Cormorant Garamond',serif;
  font-size:clamp(3rem,7vw,6rem);font-weight:300;line-height:1;letter-spacing:-.02em;
}
.sec-title em{font-style:italic;}
.sec-header{margin-bottom:3rem;}

/* CARD GRID */
.card-grid{
  display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));
  gap:3px;flex:1;
}

/* BASE CARD */
.card{position:relative;overflow:hidden;cursor:pointer;background:rgba(255,255,255,.03);}
.card-thumb{width:100%;height:100%;object-fit:cover;transition:transform .7s cubic-bezier(.25,.46,.45,.94);}
.card:hover .card-thumb{transform:scale(1.06);}
.card-overlay{
  position:absolute;inset:0;
  background:linear-gradient(to top,rgba(0,0,0,.85) 0%,transparent 55%);
  opacity:0;transition:opacity .4s;
}
.card:hover .card-overlay{opacity:1;}
.card-info{
  position:absolute;bottom:0;left:0;right:0;padding:1.8rem;
  transform:translateY(8px);opacity:0;transition:transform .4s,opacity .4s;
}
.card:hover .card-info{transform:translateY(0);opacity:1;}
.card-cat{font-size:8px;letter-spacing:.18em;text-transform:uppercase;color:rgba(255,255,255,.5);margin-bottom:.4rem;}
.card-name{font-family:'Cormorant Garamond',serif;font-size:1.5rem;font-weight:300;}
.card-placeholder{width:100%;height:100%;display:flex;align-items:center;justify-content:center;}
.card-placeholder-icon{font-family:'Cormorant Garamond',serif;font-size:4rem;font-weight:300;color:rgba(255,255,255,.07);font-style:italic;}

/* RATIO CLASSES */
/* 16:9 — Reels */
.ratio-16-9{aspect-ratio:16/9;}
/* 9:16 — Cinematic, Documentary, Music, Brand, 3D */
.ratio-9-16{aspect-ratio:9/16;}
/* Song Poster — same as image (3:4 portrait) */
.ratio-poster{aspect-ratio:3/4;}
/* Color Grading — square-ish like image (1:1) */
.ratio-square{aspect-ratio:1/1;}
/* Wide featured card */
.card.wide{grid-column:span 2;}

/* SECTION NAV */
.sec-page-nav{
  display:flex;justify-content:space-between;align-items:center;
  padding:2rem clamp(2rem,6vw,6rem);
  border-top:1px solid rgba(255,255,255,.07);position:relative;z-index:2;
}
.sec-page-links{display:flex;gap:1.5rem;}
.sec-page-link{font-size:9px;letter-spacing:.15em;text-transform:uppercase;color:rgba(255,255,255,.3);cursor:pointer;transition:color .2s;}
.sec-page-link:hover{color:#fff;}
.sec-count{font-size:9px;letter-spacing:.1em;color:rgba(255,255,255,.2);}

/* CONTACT PAGE */
#page-contact{background:#000;}
#page-contact::after{content:'';position:absolute;inset:0;background:radial-gradient(ellipse 70% 50% at 50% 50%,rgba(255,255,255,.03) 0%,transparent 60%);}
.contact-grid{display:grid;grid-template-columns:1fr 1fr;gap:clamp(3rem,8vw,8rem);align-items:center;margin-top:3rem;}
.contact-heading{font-family:'Cormorant Garamond',serif;font-size:clamp(3.5rem,8vw,7rem);font-weight:300;line-height:.95;letter-spacing:-.02em;}
.contact-heading em{font-style:italic;color:rgba(255,255,255,.38);}
.contact-sub{margin-top:2rem;font-size:12px;color:rgba(255,255,255,.3);line-height:1.9;max-width:360px;}
.contact-items{display:flex;flex-direction:column;}
.contact-item{
  padding:1.8rem 0;border-bottom:1px solid rgba(255,255,255,.07);
  display:flex;align-items:flex-start;gap:1.5rem;cursor:pointer;transition:padding-left .3s;
}
.contact-item:hover{padding-left:.8rem;}
.contact-item:first-child{border-top:1px solid rgba(255,255,255,.07);}
.ci-num{font-size:9px;letter-spacing:.14em;color:rgba(255,255,255,.2);padding-top:.2rem;}
.ci-platform{font-size:9px;letter-spacing:.2em;text-transform:uppercase;color:rgba(255,255,255,.28);margin-bottom:.3rem;}
.ci-value{font-family:-apple-system,'SF Pro Display','Helvetica Neue',Arial,sans-serif;font-size:1.4rem;font-weight:300;letter-spacing:.01em;}
.ci-value em{font-style:italic;color:rgba(255,255,255,.6);}

/* ── PAGE BACKGROUNDS ── */
#page-reels{background:linear-gradient(135deg,#050e1a 0%,#0a1f3d 30%,#0d2952 55%,#d0dcff 100%);}
#page-reels::after{content:'';position:absolute;inset:0;background:linear-gradient(to bottom,transparent 40%,rgba(0,0,10,.65) 100%);}
#page-cinematic{background:linear-gradient(160deg,#000 0%,#020d1f 40%,#041428 65%,#e8edf5 100%);}
#page-cinematic::after{content:'';position:absolute;inset:0;background:linear-gradient(to bottom,rgba(0,0,20,.3) 0%,rgba(0,0,20,.7) 100%);}
#page-documentary{background:linear-gradient(140deg,#0a0500 0%,#1a0800 25%,#3d1400 50%,#c45c00 80%,#e87020 100%);}
#page-documentary::after{content:'';position:absolute;inset:0;background:linear-gradient(to bottom,rgba(10,5,0,.5) 0%,rgba(10,5,0,.3) 100%);}
#page-brand{background:linear-gradient(135deg,#080000 0%,#1a0000 30%,#3d0000 55%,#cc0000 80%,#ff1a00 100%);}
#page-brand::after{content:'';position:absolute;inset:0;background:linear-gradient(to bottom,rgba(8,0,0,.4) 0%,rgba(8,0,0,.3) 100%);}
#page-colorgrading{
  background:
    radial-gradient(ellipse 50% 50% at 20% 40%,#00ff66 0%,transparent 40%),
    radial-gradient(ellipse 50% 60% at 50% 50%,#3300ff 0%,transparent 50%),
    radial-gradient(ellipse 40% 50% at 80% 60%,#ff6600 0%,transparent 40%),
    radial-gradient(ellipse 30% 40% at 40% 80%,#ff00cc 0%,transparent 35%),
    radial-gradient(ellipse 30% 30% at 70% 20%,#0099ff 0%,transparent 30%),#000;
}
#page-colorgrading::after{content:'';position:absolute;inset:0;background:rgba(0,0,0,.32);}
#page-music{background:linear-gradient(160deg,#000 0%,#111 40%,#888 75%,#f5f5f5 100%);}
#page-music::after{content:'';position:absolute;inset:0;background:linear-gradient(to bottom,rgba(0,0,0,.5) 0%,rgba(0,0,0,.2) 100%);}
#page-songposter{background:#000;}
#page-songposter::after{content:'';position:absolute;inset:0;background:radial-gradient(ellipse 50% 50% at 50% 50%,rgba(255,255,255,.025) 0%,transparent 70%);}
#page-3d{background:linear-gradient(140deg,#04001a 0%,#0d0030 25%,#1a0066 50%,#2200aa 70%,#4400ff 85%,#6633ff 100%);}
#page-3d::after{content:'';position:absolute;inset:0;background:radial-gradient(ellipse 60% 60% at 80% 20%,rgba(100,0,255,.3) 0%,transparent 50%),radial-gradient(ellipse 40% 40% at 20% 80%,rgba(0,80,255,.2) 0%,transparent 40%);}

/* ── RESPONSIVE ── */
@media(max-width:900px){
  nav{padding:1.2rem 1.5rem;}
  .nav-links{display:none;}
  .hero-nav-grid{grid-template-columns:repeat(2,1fr);}
  .sec-inner{padding:5rem 1.5rem 3rem;}
  .about-grid{grid-template-columns:1fr;}
  .about-heading{position:static;}
  .contact-grid{grid-template-columns:1fr;}
  .card.wide{grid-column:span 1;}
  .home-contact-items{gap:1.5rem;}
  .hci-value{font-size:1rem;}
  .hero-contact-strip{flex-direction:column;align-items:flex-start;}
  .scroll-hint{display:none;}
}
@media(max-width:600px){
  .card-grid{grid-template-columns:repeat(2,1fr);}
  .card.wide{grid-column:span 2;}
}
</style>
</head>
<body>

<div class="grain"></div>
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>
<div class="page-curtain" id="curtain"></div>

<!-- NAV -->
<nav>
  <div class="nav-logo" onclick="navigateTo('home')">P<span>reet</span></div>
  <ul class="nav-links">
    <li><a href="#" onclick="navigateTo('about');return false;">About</a></li>
    <li><a href="#" onclick="navigateTo('reels');return false;">Reels</a></li>
    <li><a href="#" onclick="navigateTo('cinematic');return false;">Cinematic</a></li>
    <li><a href="#" onclick="navigateTo('documentary');return false;">Documentary</a></li>
    <li><a href="#" onclick="navigateTo('brand');return false;">Brand</a></li>
    <li><a href="#" onclick="navigateTo('colorgrading');return false;">Grading</a></li>
    <li><a href="#" onclick="navigateTo('music');return false;">Music</a></li>
    <li><a href="#" onclick="navigateTo('songposter');return false;">Poster</a></li>
    <li><a href="#" onclick="navigateTo('3d');return false;">3D</a></li>
    <li><a href="#" onclick="navigateTo('contact');return false;">Contact</a></li>
  </ul>
</nav>

<!-- ══ HOME ══ -->
<section class="page active" id="page-home">
  <div class="hero-bg"></div>
  <div class="hero-glow"></div>
  <div class="hero-scanlines"></div>
  <div class="hero-content">
    <p class="hero-eyebrow reveal">Visual Creator · Editor · Motion Designer · Chandigarh</p>
    <h1 class="hero-name reveal">Preet<br><em>Sidhu</em></h1>
    <p class="hero-tagline-main reveal">
      From concept to final cut — creating visuals that move people,<br>
      tell stories, and make every second count.
    </p>
    <div class="hero-divider reveal"></div>
    <div class="hero-nav-grid reveal">
      <div class="hero-nav-item" onclick="navigateTo('reels')"><div class="hero-nav-num">01</div><div class="hero-nav-label">Reels <em>Edits</em></div></div>
      <div class="hero-nav-item" onclick="navigateTo('cinematic')"><div class="hero-nav-num">02</div><div class="hero-nav-label">Cinematic <em>Videos</em></div></div>
      <div class="hero-nav-item" onclick="navigateTo('documentary')"><div class="hero-nav-num">03</div><div class="hero-nav-label">Documentary <em>Edits</em></div></div>
      <div class="hero-nav-item" onclick="navigateTo('brand')"><div class="hero-nav-num">04</div><div class="hero-nav-label">Brand <em>Videos</em></div></div>
      <div class="hero-nav-item" onclick="navigateTo('colorgrading')"><div class="hero-nav-num">05</div><div class="hero-nav-label">Color <em>Grading</em></div></div>
      <div class="hero-nav-item" onclick="navigateTo('music')"><div class="hero-nav-num">06</div><div class="hero-nav-label">Music <em>Videos</em></div></div>
      <div class="hero-nav-item" onclick="navigateTo('songposter')"><div class="hero-nav-num">07</div><div class="hero-nav-label">Song <em>Poster</em></div></div>
      <div class="hero-nav-item" onclick="navigateTo('3d')"><div class="hero-nav-num">08</div><div class="hero-nav-label">3D <em>Visualiser</em></div></div>
    </div>
  </div>
  <div class="hero-contact-strip reveal">
    <span class="home-contact-label">Get in touch</span>
    <div class="home-contact-items">
      <div class="home-contact-item" onclick="window.open('https://instagram.com/Preet_Sidhu_364','_blank')">
        <span class="hci-platform">Instagram</span>
        <span class="hci-value"><em>@Preet_Sidhu_364</em></span>
      </div>
      <div class="home-contact-item" onclick="window.location='mailto:preett978@gmail.com'">
        <span class="hci-platform">Gmail</span>
        <span class="hci-value">preett978@gmail.com</span>
      </div>
      <div class="home-contact-item" onclick="window.location='tel:+918360747667'">
        <span class="hci-platform">Phone</span>
        <span class="hci-value">+91 8360747667</span>
      </div>
    </div>
  </div>
  <div class="hero-bottom">
    <span class="hero-bottom-info">© 2026 Preet Sidhu</span>
    <span class="hero-bottom-info" onclick="navigateTo('about')" style="cursor:pointer;">About Me →</span>
  </div>
  <div class="scroll-hint">
    <div class="scroll-hint-line"></div>
    <span class="scroll-hint-text">scroll</span>
  </div>
</section>

<!-- ══ ABOUT ══ -->
<section class="page" id="page-about">
  <div class="about-inner">
    <div class="sec-label reveal">About Me</div>
    <div class="about-grid">
      <div>
        <h2 class="about-heading reveal">
          Crafting stories<br><em>frame by</em><br>frame
        </h2>
      </div>
      <div class="about-right">
        <p class="about-intro reveal">
          I'm <strong>Preet Sidhu</strong> — a visual creator obsessed with the space between a raw idea and a finished cinematic moment.
        </p>
        <div class="about-divider reveal"></div>
        <div class="about-body reveal">
          <p>From motion graphics that stop thumbs mid-scroll to long-form cinematic edits that hold you in your seat — I work across formats, moods, and platforms to make visuals that don't just look good, but feel right.</p>
          <p>My process starts with understanding the story, then shaping it with light, rhythm, and motion until it truly stands out.</p>
        </div>
        <div class="about-skills reveal">
          <span class="about-skill">Reels Editing</span>
          <span class="about-skill">Cinematic Film</span>
          <span class="about-skill">Motion Graphics</span>
          <span class="about-skill">Color Grading</span>
          <span class="about-skill">Documentary</span>
          <span class="about-skill">Brand Films</span>
          <span class="about-skill">Music Videos</span>
          <span class="about-skill">3D Visualiser</span>
          <span class="about-skill">Song Posters</span>
          <span class="about-skill">Premiere Pro</span>
          <span class="about-skill">After Effects</span>
          <span class="about-skill">DaVinci Resolve</span>
        </div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links">
      <span class="sec-page-link" onclick="navigateTo('home')">← Home</span>
      <span class="sec-page-link" onclick="navigateTo('reels')">Work →</span>
    </div>
    <span class="sec-count">About</span>
  </div>
</section>

<!-- ══ 01 REELS — 16:9 ══ -->
<section class="page" id="page-reels">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">01 / 08 — Reels Edits</div>
      <h2 class="sec-title reveal">Reels <em>Edits</em></h2>
    </div>
    <div class="card-grid" style="grid-template-columns:1fr;">
      <div class="card wide ratio-16-9 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#05183a,#0a3070,#2060c0);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Featured · Reel</p><p class="card-name">Drop your video here</p></div>
      </div>
    </div>
    <div class="card-grid" style="grid-template-columns:repeat(2,1fr);margin-top:3px;">
      <div class="card ratio-16-9 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#031428,#0a2550);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Reel</p><p class="card-name">Reel Title</p></div>
      </div>
      <div class="card ratio-16-9 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#081c3c,#102c5a);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Reel</p><p class="card-name">Reel Title</p></div>
      </div>
      <div class="card ratio-16-9 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#051020,#0d2244);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Reel</p><p class="card-name">Reel Title</p></div>
      </div>
      <div class="card ratio-16-9 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#081830,#122e5c);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Reel</p><p class="card-name">Reel Title</p></div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links">
      <span class="sec-page-link" onclick="navigateTo('home')">Home</span>
      <span class="sec-page-link" onclick="navigateTo('cinematic')">Next: Cinematic →</span>
    </div>
    <span class="sec-count">01 / 08</span>
  </div>
</section>

<!-- ══ 02 CINEMATIC — 9:16 ══ -->
<section class="page" id="page-cinematic">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">02 / 08 — Cinematic Videos</div>
      <h2 class="sec-title reveal">Cinematic <em>Videos</em></h2>
    </div>
    <div class="card-grid" style="grid-template-columns:repeat(auto-fill,minmax(200px,1fr));">
      <div class="card ratio-9-16 reveal" style="grid-column:span 2;">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#000,#020c1e,#041428);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Featured · Cinematic</p><p class="card-name">Drop your video here</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#010810,#020f1e);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Cinematic</p><p class="card-name">Film Title</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#02101e,#031525);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Cinematic</p><p class="card-name">Film Title</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#010c18,#021220);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Cinematic</p><p class="card-name">Film Title</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#020e1c,#031828);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Cinematic</p><p class="card-name">Film Title</p></div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links">
      <span class="sec-page-link" onclick="navigateTo('reels')">← Reels</span>
      <span class="sec-page-link" onclick="navigateTo('documentary')">Next: Documentary →</span>
    </div>
    <span class="sec-count">02 / 08</span>
  </div>
</section>

<!-- ══ 03 DOCUMENTARY — 9:16 ══ -->
<section class="page" id="page-documentary">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">03 / 08 — Documentary Edits</div>
      <h2 class="sec-title reveal">Documentary <em>Edits</em></h2>
    </div>
    <div class="card-grid" style="grid-template-columns:repeat(auto-fill,minmax(200px,1fr));">
      <div class="card ratio-9-16 reveal" style="grid-column:span 2;">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#0a0500,#3d1400,#a03000);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Featured · Documentary</p><p class="card-name">Drop your video here</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#100700,#280f00);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Documentary</p><p class="card-name">Doc Title</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#180a00,#301500);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Documentary</p><p class="card-name">Doc Title</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#0d0600,#221000);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Documentary</p><p class="card-name">Doc Title</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#140800,#281200);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Documentary</p><p class="card-name">Doc Title</p></div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links">
      <span class="sec-page-link" onclick="navigateTo('cinematic')">← Cinematic</span>
      <span class="sec-page-link" onclick="navigateTo('brand')">Next: Brand →</span>
    </div>
    <span class="sec-count">03 / 08</span>
  </div>
</section>

<!-- ══ 04 BRAND — 9:16 ══ -->
<section class="page" id="page-brand">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">04 / 08 — Brand Videos</div>
      <h2 class="sec-title reveal">Brand <em>Videos</em></h2>
    </div>
    <div class="card-grid" style="grid-template-columns:repeat(auto-fill,minmax(200px,1fr));">
      <div class="card ratio-9-16 reveal" style="grid-column:span 2;">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#080000,#300000,#880000);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Featured · Brand</p><p class="card-name">Drop your video here</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#0e0000,#200000);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Brand</p><p class="card-name">Brand Film</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#160000,#280000);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Brand</p><p class="card-name">Brand Film</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#100000,#1c0000);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Brand</p><p class="card-name">Brand Film</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#140000,#240000);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Brand</p><p class="card-name">Brand Film</p></div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links">
      <span class="sec-page-link" onclick="navigateTo('documentary')">← Documentary</span>
      <span class="sec-page-link" onclick="navigateTo('colorgrading')">Next: Color Grading →</span>
    </div>
    <span class="sec-count">04 / 08</span>
  </div>
</section>

<!-- ══ 05 COLOR GRADING — Square 1:1 ══ -->
<section class="page" id="page-colorgrading">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">05 / 08 — Color Grading</div>
      <h2 class="sec-title reveal">Color <em>Grading</em></h2>
    </div>
    <div class="card-grid" style="grid-template-columns:repeat(auto-fill,minmax(260px,1fr));">
      <div class="card ratio-square reveal" style="grid-column:span 2;">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#001a0d,#00338a,#440088,#880044);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Featured · Grade</p><p class="card-name">Drop your video here</p></div>
      </div>
      <div class="card ratio-square reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#001808,#003388);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Grade</p><p class="card-name">Grading Project</p></div>
      </div>
      <div class="card ratio-square reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#330066,#880033);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Grade</p><p class="card-name">Grading Project</p></div>
      </div>
      <div class="card ratio-square reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#004400,#002266);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Grade</p><p class="card-name">Grading Project</p></div>
      </div>
      <div class="card ratio-square reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#440000,#004466);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Grade</p><p class="card-name">Grading Project</p></div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links">
      <span class="sec-page-link" onclick="navigateTo('brand')">← Brand</span>
      <span class="sec-page-link" onclick="navigateTo('music')">Next: Music Videos →</span>
    </div>
    <span class="sec-count">05 / 08</span>
  </div>
</section>

<!-- ══ 06 MUSIC — 9:16 ══ -->
<section class="page" id="page-music">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">06 / 08 — Music Videos</div>
      <h2 class="sec-title reveal">Music <em>Videos</em></h2>
    </div>
    <div class="card-grid" style="grid-template-columns:repeat(auto-fill,minmax(200px,1fr));">
      <div class="card ratio-9-16 reveal" style="grid-column:span 2;">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#000,#222,#666);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Featured · Music</p><p class="card-name">Drop your video here</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#111,#333);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Music</p><p class="card-name">Music Video</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#1a1a1a,#3a3a3a);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Music</p><p class="card-name">Music Video</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#080808,#282828);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Music</p><p class="card-name">Music Video</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#0d0d0d,#2d2d2d);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Music</p><p class="card-name">Music Video</p></div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links">
      <span class="sec-page-link" onclick="navigateTo('colorgrading')">← Color Grading</span>
      <span class="sec-page-link" onclick="navigateTo('songposter')">Next: Song Poster →</span>
    </div>
    <span class="sec-count">06 / 08</span>
  </div>
</section>

<!-- ══ 07 SONG POSTER — 3:4 like image ══ -->
<section class="page" id="page-songposter">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">07 / 08 — Song Posters</div>
      <h2 class="sec-title reveal">Song <em>Poster</em></h2>
    </div>
    <div class="card-grid" style="grid-template-columns:repeat(auto-fill,minmax(220px,1fr));">
      <div class="card ratio-poster reveal">
        <div class="card-placeholder" style="background:#060606;border:1px solid rgba(255,255,255,.06);width:100%;height:100%;"><span class="card-placeholder-icon" style="font-size:2.5rem;">✦</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Poster</p><p class="card-name">Song Title</p></div>
      </div>
      <div class="card ratio-poster reveal">
        <div class="card-placeholder" style="background:#040404;border:1px solid rgba(255,255,255,.06);width:100%;height:100%;"><span class="card-placeholder-icon" style="font-size:2.5rem;">✦</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Poster</p><p class="card-name">Song Title</p></div>
      </div>
      <div class="card ratio-poster reveal">
        <div class="card-placeholder" style="background:#080808;border:1px solid rgba(255,255,255,.06);width:100%;height:100%;"><span class="card-placeholder-icon" style="font-size:2.5rem;">✦</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Poster</p><p class="card-name">Song Title</p></div>
      </div>
      <div class="card ratio-poster reveal">
        <div class="card-placeholder" style="background:#050505;border:1px solid rgba(255,255,255,.06);width:100%;height:100%;"><span class="card-placeholder-icon" style="font-size:2.5rem;">✦</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Poster</p><p class="card-name">Song Title</p></div>
      </div>
      <div class="card ratio-poster reveal">
        <div class="card-placeholder" style="background:#070707;border:1px solid rgba(255,255,255,.06);width:100%;height:100%;"><span class="card-placeholder-icon" style="font-size:2.5rem;">✦</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Poster</p><p class="card-name">Song Title</p></div>
      </div>
      <div class="card ratio-poster reveal">
        <div class="card-placeholder" style="background:#060606;border:1px solid rgba(255,255,255,.06);width:100%;height:100%;"><span class="card-placeholder-icon" style="font-size:2.5rem;">✦</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Poster</p><p class="card-name">Song Title</p></div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links">
      <span class="sec-page-link" onclick="navigateTo('music')">← Music Videos</span>
      <span class="sec-page-link" onclick="navigateTo('3d')">Next: 3D Visualiser →</span>
    </div>
    <span class="sec-count">07 / 08</span>
  </div>
</section>

<!-- ══ 08 3D — 9:16 ══ -->
<section class="page" id="page-3d">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">08 / 08 — 3D Visualiser</div>
      <h2 class="sec-title reveal">3D <em>Visualiser</em></h2>
    </div>
    <div class="card-grid" style="grid-template-columns:repeat(auto-fill,minmax(200px,1fr));">
      <div class="card ratio-9-16 reveal" style="grid-column:span 2;">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#04001a,#1a0066,#4400ff);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Featured · 3D</p><p class="card-name">Drop your video here</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#06001c,#1c0070);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">3D</p><p class="card-name">Visualiser Project</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#08001e,#200080);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">3D</p><p class="card-name">Visualiser Project</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#040018,#140060);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">3D</p><p class="card-name">Visualiser Project</p></div>
      </div>
      <div class="card ratio-9-16 reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#0a001e,#240088);width:100%;height:100%;"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">3D</p><p class="card-name">Visualiser Project</p></div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links">
      <span class="sec-page-link" onclick="navigateTo('songposter')">← Song Poster</span>
      <span class="sec-page-link" onclick="navigateTo('contact')">Contact →</span>
    </div>
    <span class="sec-count">08 / 08</span>
  </div>
</section>

<!-- ══ CONTACT ══ -->
<section class="page" id="page-contact">
  <div class="sec-inner">
    <div class="sec-label reveal">Contact</div>
    <div class="contact-grid">
      <div>
        <h2 class="contact-heading reveal">Let's create<br>something<br><em>cinematic</em></h2>
        <p class="contact-sub reveal">Have a project in mind? Whether it's a reel, brand film, 3D visualiser or a song poster — let's make it unforgettable.</p>
      </div>
      <div class="reveal">
        <div class="contact-items">
          <div class="contact-item" onclick="window.open('https://instagram.com/Preet_Sidhu_364','_blank')">
            <span class="ci-num">01</span>
            <div><p class="ci-platform">Instagram</p><p class="ci-value"><em>@Preet_Sidhu_364</em></p></div>
          </div>
          <div class="contact-item" onclick="window.location='mailto:preett978@gmail.com'">
            <span class="ci-num">02</span>
            <div><p class="ci-platform">Gmail</p><p class="ci-value">preett978@gmail.com</p></div>
          </div>
          <div class="contact-item" onclick="window.location='tel:+918360747667'">
            <span class="ci-num">03</span>
            <div><p class="ci-platform">Phone</p><p class="ci-value">+91 8360747667</p></div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav" style="position:relative;z-index:2;">
    <div class="sec-page-links">
      <span class="sec-page-link" onclick="navigateTo('home')">← Home</span>
    </div>
    <span class="sec-count">© 2026 Preet Sidhu</span>
  </div>
</section>

<script>
// ── CURSOR ─────────────────────────────────────
const cursor = document.getElementById('cursor');
const ring   = document.getElementById('cursorRing');
let mx=0,my=0,rx=0,ry=0;
document.addEventListener('mousemove',e=>{
  mx=e.clientX; my=e.clientY;
  cursor.style.left=mx+'px'; cursor.style.top=my+'px';
});
(function animateRing(){
  rx+=(mx-rx)*.12; ry+=(my-ry)*.12;
  ring.style.left=rx+'px'; ring.style.top=ry+'px';
  requestAnimationFrame(animateRing);
})();
document.querySelectorAll('a,button,[onclick],.card,.hero-nav-item,.contact-item,.home-contact-item,.sec-page-link').forEach(el=>{
  el.addEventListener('mouseenter',()=>{cursor.style.width='20px';cursor.style.height='20px';ring.style.width='60px';ring.style.height='60px';});
  el.addEventListener('mouseleave',()=>{cursor.style.width='12px';cursor.style.height='12px';ring.style.width='36px';ring.style.height='36px';});
});

// ── PAGE NAV WITH HISTORY ───────────────────────
const curtain = document.getElementById('curtain');
let historyStack = ['home'];
let current = 'home';
let isAnimating = false;

function navigateTo(id){
  if(id===current || isAnimating) return;
  isAnimating=true;
  curtain.className='page-curtain in';
  setTimeout(()=>{
    document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
    document.querySelectorAll('.reveal.visible').forEach(el=>el.classList.remove('visible'));
    document.getElementById('page-'+id).classList.add('active');
    historyStack.push(id);
    current=id;
    window.scrollTo(0,0);
    triggerReveals();
    curtain.className='page-curtain out';
    setTimeout(()=>{curtain.className='page-curtain';isAnimating=false;},520);
  },480);
}

function goBack(){
  if(historyStack.length<=1||isAnimating) return;
  historyStack.pop();
  const prev=historyStack[historyStack.length-1];
  isAnimating=true;
  curtain.className='page-curtain in';
  setTimeout(()=>{
    document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
    document.querySelectorAll('.reveal.visible').forEach(el=>el.classList.remove('visible'));
    document.getElementById('page-'+prev).classList.add('active');
    current=prev;
    window.scrollTo(0,0);
    triggerReveals();
    curtain.className='page-curtain out';
    setTimeout(()=>{curtain.className='page-curtain';isAnimating=false;},520);
  },480);
}

// Mouse button 4 (side back button)
window.addEventListener('mouseup',e=>{ if(e.button===3) goBack(); });

// Browser back button
history.pushState(null,'',window.location.href);
window.addEventListener('popstate',e=>{ e.preventDefault(); goBack(); history.pushState(null,'',window.location.href); });

// Mobile swipe right to go back
let touchStartX=0, touchStartY=0;
document.addEventListener('touchstart',e=>{ touchStartX=e.touches[0].clientX; touchStartY=e.touches[0].clientY; },{passive:true});
document.addEventListener('touchend',e=>{
  const dx=e.changedTouches[0].clientX-touchStartX;
  const dy=Math.abs(e.changedTouches[0].clientY-touchStartY);
  if(dx>75&&dy<40) goBack();
},{passive:true});

// ── REVEAL ────────────────────────────────────
function triggerReveals(){
  setTimeout(()=>{
    document.querySelectorAll('.page.active .reveal').forEach((el,i)=>{
      setTimeout(()=>el.classList.add('visible'),i*80);
    });
  },100);
}
triggerReveals();
const ro=new IntersectionObserver(entries=>{
  entries.forEach(e=>{ if(e.isIntersecting) e.target.classList.add('visible'); });
},{threshold:.1});
document.querySelectorAll('.reveal').forEach(el=>ro.observe(el));
</script>
</body>
</html>
