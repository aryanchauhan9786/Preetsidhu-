<!DOCTYPE html>
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
  background:#000;
  color:#fff;
  font-family:'DM Mono',monospace;
  font-size:14px;
  line-height:1.7;
  overflow-x:hidden;
  cursor:none;
}
img,video{max-width:100%;display:block;}
a{color:inherit;text-decoration:none;}

/* CURSOR */
.cursor{
  position:fixed;width:12px;height:12px;
  background:#fff;border-radius:50%;
  pointer-events:none;z-index:9999;
  transform:translate(-50%,-50%);
  transition:width .2s,height .2s,background .2s;
  mix-blend-mode:difference;
}
.cursor-ring{
  position:fixed;width:36px;height:36px;
  border:1px solid rgba(255,255,255,.4);border-radius:50%;
  pointer-events:none;z-index:9998;
  transform:translate(-50%,-50%);
  transition:width .2s,height .2s,border-color .2s;
}

/* GRAIN */
.grain{
  position:fixed;inset:0;z-index:9990;
  pointer-events:none;opacity:.12;
  background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
  background-repeat:repeat;
  background-size:200px 200px;
  animation:grainShift .08s steps(1) infinite;
}
@keyframes grainShift{
  0%{background-position:0 0;}
  10%{background-position:-5% -10%;}
  20%{background-position:-15% 5%;}
  30%{background-position:7% -25%;}
  40%{background-position:-5% 25%;}
  50%{background-position:-15% 10%;}
  60%{background-position:15% 0%;}
  70%{background-position:0 15%;}
  80%{background-position:3% 35%;}
  90%{background-position:-10% 10%;}
  100%{background-position:0 0;}
}

/* NAV */
nav{
  position:fixed;top:0;left:0;right:0;z-index:1000;
  padding:1.4rem 3rem;
  display:flex;justify-content:space-between;align-items:center;
}
nav::before{
  content:'';position:absolute;inset:0;
  background:linear-gradient(to bottom,rgba(0,0,0,.75),transparent);
  backdrop-filter:blur(8px);
  -webkit-backdrop-filter:blur(8px);
  z-index:-1;
}
.nav-logo{
  font-family:'Cormorant Garamond',serif;
  font-size:1.6rem;font-weight:300;letter-spacing:.08em;color:#fff;
  cursor:pointer;
}
.nav-logo span{font-style:italic;}
.nav-links{display:flex;gap:1.8rem;list-style:none;align-items:center;}
.nav-links a{
  font-size:9px;letter-spacing:.18em;text-transform:uppercase;
  color:rgba(255,255,255,.45);transition:color .25s;
  position:relative;
}
.nav-links a::after{
  content:'';position:absolute;bottom:-4px;left:0;right:0;
  height:1px;background:currentColor;
  transform:scaleX(0);transform-origin:right;
  transition:transform .3s ease;
}
.nav-links a:hover{color:#fff;}
.nav-links a:hover::after{transform:scaleX(1);transform-origin:left;}

/* PAGE SYSTEM */
.page{display:none;min-height:100vh;position:relative;overflow:hidden;}
.page.active{display:block;}

/* PAGE CURTAIN */
.page-curtain{
  position:fixed;inset:0;z-index:2000;
  background:#000;transform:translateY(-100%);pointer-events:none;
}
.page-curtain.in{animation:curtainIn .5s cubic-bezier(.76,0,.24,1) forwards;}
.page-curtain.out{animation:curtainOut .5s cubic-bezier(.76,0,.24,1) forwards;}
@keyframes curtainIn{from{transform:translateY(100%);}to{transform:translateY(0);}}
@keyframes curtainOut{from{transform:translateY(0);}to{transform:translateY(-100%);}}

/* REVEAL */
.reveal{opacity:0;transform:translateY(40px);transition:opacity .9s ease,transform .9s ease;}
.reveal.visible{opacity:1;transform:none;}

/* BACK BUTTON */
.back-btn{
  position:fixed;bottom:2.5rem;left:clamp(2rem,6vw,6rem);
  z-index:500;display:none;align-items:center;gap:.7rem;
  font-size:9px;letter-spacing:.18em;text-transform:uppercase;
  color:rgba(255,255,255,.4);cursor:pointer;transition:color .2s;
  background:rgba(0,0,0,.4);padding:.7rem 1.2rem;
  border:1px solid rgba(255,255,255,.1);backdrop-filter:blur(6px);
}
.back-btn:hover{color:#fff;}
.back-btn.visible{display:flex;}

/* ── HOME ── */
#page-home{background:#000;}
#page-home.active{display:flex;flex-direction:column;}
.hero-bg{
  position:absolute;inset:0;z-index:0;
  background:
    radial-gradient(ellipse 60% 70% at 20% 30%,rgba(255,255,255,.04) 0%,transparent 60%),
    radial-gradient(ellipse 40% 50% at 80% 70%,rgba(255,255,255,.03) 0%,transparent 50%),#000;
}
.hero-scanlines{
  position:absolute;inset:0;z-index:1;
  background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(255,255,255,.012) 2px,rgba(255,255,255,.012) 4px);
}
.hero-content{
  position:relative;z-index:2;
  display:flex;flex-direction:column;justify-content:flex-end;
  min-height:100vh;
  padding:0 clamp(2rem,6vw,6rem) clamp(3rem,8vh,6rem);
}
.hero-eyebrow{font-size:9px;letter-spacing:.25em;text-transform:uppercase;color:rgba(255,255,255,.35);margin-bottom:1.4rem;}
.hero-name{
  font-family:'Cormorant Garamond',serif;
  font-size:clamp(4rem,12vw,10rem);font-weight:300;line-height:.9;letter-spacing:-.02em;color:#fff;
}
.hero-name em{font-style:italic;color:rgba(255,255,255,.45);}
.hero-tagline{margin-top:2rem;font-size:clamp(10px,1.2vw,13px);color:rgba(255,255,255,.3);max-width:500px;letter-spacing:.06em;line-height:1.9;}
.hero-divider{width:80px;height:1px;background:rgba(255,255,255,.18);margin:2rem 0;}
.hero-nav-grid{
  display:grid;grid-template-columns:repeat(4,1fr);gap:1px;
  border:1px solid rgba(255,255,255,.07);max-width:920px;margin-top:4rem;
}
.hero-nav-item{
  padding:1.4rem 1.8rem;
  border-right:1px solid rgba(255,255,255,.07);
  cursor:pointer;transition:background .3s;position:relative;overflow:hidden;
}
.hero-nav-item:last-child{border-right:none;}
.hero-nav-item::before{
  content:'';position:absolute;inset:0;
  background:rgba(255,255,255,.04);
  transform:translateY(100%);transition:transform .3s ease;
}
.hero-nav-item:hover::before{transform:translateY(0);}
.hero-nav-num{font-size:9px;letter-spacing:.14em;color:rgba(255,255,255,.22);margin-bottom:.5rem;}
.hero-nav-label{font-family:'Cormorant Garamond',serif;font-size:1.1rem;font-weight:300;color:rgba(255,255,255,.65);line-height:1.2;}
.hero-nav-label em{font-style:italic;}
.hero-bottom{
  position:relative;z-index:2;padding:1.8rem clamp(2rem,6vw,6rem);
  display:flex;justify-content:space-between;align-items:center;
  border-top:1px solid rgba(255,255,255,.07);
}
.hero-bottom-info{font-size:9px;letter-spacing:.14em;color:rgba(255,255,255,.22);}
.scroll-hint{position:absolute;right:3rem;bottom:3rem;display:flex;flex-direction:column;align-items:center;gap:.6rem;z-index:10;}
.scroll-hint-line{width:1px;height:50px;background:rgba(255,255,255,.15);position:relative;overflow:hidden;}
.scroll-hint-line::after{
  content:'';position:absolute;top:0;left:0;right:0;height:50%;background:#fff;
  animation:scrollLine 2s ease-in-out infinite;
}
@keyframes scrollLine{0%{transform:translateY(-100%);}100%{transform:translateY(200%);}}
.scroll-hint-text{font-size:8px;letter-spacing:.2em;text-transform:uppercase;color:rgba(255,255,255,.22);writing-mode:vertical-rl;}

/* ── SECTION INNER ── */
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

/* ── CARD GRID ── */
.card-grid{
  display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));
  gap:1.5px;flex:1;
}
.card{position:relative;overflow:hidden;aspect-ratio:9/12;cursor:pointer;background:rgba(255,255,255,.03);}
.card-thumb{width:100%;height:100%;transition:transform .7s cubic-bezier(.25,.46,.45,.94);}
.card:hover .card-thumb{transform:scale(1.06);}
.card-overlay{
  position:absolute;inset:0;
  background:linear-gradient(to top,rgba(0,0,0,.8) 0%,transparent 50%);
  opacity:0;transition:opacity .4s;
}
.card:hover .card-overlay{opacity:1;}
.card-info{
  position:absolute;bottom:0;left:0;right:0;padding:1.5rem;
  transform:translateY(8px);opacity:0;transition:transform .4s,opacity .4s;
}
.card:hover .card-info{transform:translateY(0);opacity:1;}
.card-cat{font-size:8px;letter-spacing:.18em;text-transform:uppercase;color:rgba(255,255,255,.5);margin-bottom:.3rem;}
.card-name{font-family:'Cormorant Garamond',serif;font-size:1.3rem;font-weight:300;}
.card-placeholder{width:100%;height:100%;display:flex;align-items:center;justify-content:center;}
.card-placeholder-icon{font-family:'Cormorant Garamond',serif;font-size:3rem;font-weight:300;color:rgba(255,255,255,.07);font-style:italic;}
.card.wide{grid-column:span 2;aspect-ratio:16/9;}

/* ── SECTION NAV BAR ── */
.sec-page-nav{
  display:flex;justify-content:space-between;align-items:center;
  padding:2rem clamp(2rem,6vw,6rem);
  border-top:1px solid rgba(255,255,255,.07);
  position:relative;z-index:2;
}
.sec-page-links{display:flex;gap:1.5rem;}
.sec-page-link{font-size:9px;letter-spacing:.15em;text-transform:uppercase;color:rgba(255,255,255,.3);cursor:pointer;transition:color .2s;}
.sec-page-link:hover{color:#fff;}
.sec-count{font-size:9px;letter-spacing:.1em;color:rgba(255,255,255,.2);}

/* ── CONTACT ── */
.contact-grid{display:grid;grid-template-columns:1fr 1fr;gap:clamp(3rem,8vw,8rem);align-items:center;margin-top:3rem;}
.contact-heading{font-family:'Cormorant Garamond',serif;font-size:clamp(3.5rem,8vw,7rem);font-weight:300;line-height:.95;letter-spacing:-.02em;}
.contact-heading em{font-style:italic;color:rgba(255,255,255,.38);}
.contact-sub{margin-top:2rem;font-size:12px;color:rgba(255,255,255,.3);line-height:1.9;max-width:360px;}
.contact-items{display:flex;flex-direction:column;gap:0;}
.contact-item{
  padding:1.8rem 0;border-bottom:1px solid rgba(255,255,255,.07);
  display:flex;align-items:flex-start;gap:1.5rem;
  cursor:pointer;transition:padding-left .3s;
}
.contact-item:hover{padding-left:.8rem;}
.contact-item:first-child{border-top:1px solid rgba(255,255,255,.07);}
.ci-num{font-size:9px;letter-spacing:.14em;color:rgba(255,255,255,.2);padding-top:.2rem;}
.ci-platform{font-size:9px;letter-spacing:.2em;text-transform:uppercase;color:rgba(255,255,255,.28);margin-bottom:.3rem;}
.ci-value{font-family:'Cormorant Garamond',serif;font-size:1.5rem;font-weight:300;letter-spacing:.02em;}
.ci-value em{font-style:italic;}

/* ── PAGE BACKGROUNDS ── */
#page-reels{background:linear-gradient(135deg,#050e1a 0%,#0a1f3d 30%,#0d2952 50%,#f0f4ff 100%);}
#page-reels::after{content:'';position:absolute;inset:0;background:linear-gradient(to bottom,transparent 40%,rgba(0,0,10,.6) 100%);}

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
#page-colorgrading::after{content:'';position:absolute;inset:0;background:rgba(0,0,0,.35);}

#page-music{background:linear-gradient(160deg,#000 0%,#111 40%,#888 75%,#f5f5f5 100%);}
#page-music::after{content:'';position:absolute;inset:0;background:linear-gradient(to bottom,rgba(0,0,0,.5) 0%,rgba(0,0,0,.2) 100%);}

#page-songposter{background:#000;}
#page-songposter::after{content:'';position:absolute;inset:0;background:radial-gradient(ellipse 50% 50% at 50% 50%,rgba(255,255,255,.025) 0%,transparent 70%);}

#page-3d{background:linear-gradient(140deg,#04001a 0%,#0d0030 25%,#1a0066 50%,#2200aa 70%,#4400ff 85%,#6633ff 100%);}
#page-3d::after{
  content:'';position:absolute;inset:0;
  background:
    radial-gradient(ellipse 60% 60% at 80% 20%,rgba(100,0,255,.3) 0%,transparent 50%),
    radial-gradient(ellipse 40% 40% at 20% 80%,rgba(0,80,255,.2) 0%,transparent 40%);
}

#page-contact{background:#000;}
#page-contact::after{content:'';position:absolute;inset:0;background:radial-gradient(ellipse 70% 50% at 50% 50%,rgba(255,255,255,.03) 0%,transparent 60%);}

/* ── RESPONSIVE ── */
@media(max-width:768px){
  nav{padding:1.2rem 1.5rem;}
  .nav-links{display:none;}
  .hero-nav-grid{grid-template-columns:repeat(2,1fr);}
  .sec-inner{padding:5rem 1.5rem 3rem;}
  .contact-grid{grid-template-columns:1fr;}
  .card.wide{grid-column:span 1;aspect-ratio:16/9;}
  .back-btn{left:1.5rem;}
}
</style>
</head>
<body>

<div class="grain"></div>
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>
<div class="page-curtain" id="curtain"></div>
<div class="back-btn" id="backBtn" onclick="goHome()">← Back</div>

<!-- NAV -->
<nav>
  <div class="nav-logo" onclick="goHome()">P<span>reet</span></div>
  <ul class="nav-links">
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

<!-- HOME -->
<section class="page active" id="page-home">
  <div class="hero-bg"></div>
  <div class="hero-scanlines"></div>
  <div class="hero-content">
    <p class="hero-eyebrow reveal">Visual Creator · Editor · Motion Designer · Ludhiana, Punjab</p>
    <h1 class="hero-name reveal">Preet<br><em>Sidhu</em></h1>
    <div class="hero-divider reveal"></div>
    <p class="hero-tagline reveal">Crafting cinematic visuals frame by frame —<br>from reels that stop thumbs to films that hold you in your seat.</p>
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
  <div class="hero-bottom reveal">
    <span class="hero-bottom-info">© 2026 Preet Sidhu</span>
    <span class="hero-bottom-info" onclick="navigateTo('contact')" style="cursor:pointer;">Get in Touch →</span>
  </div>
  <div class="scroll-hint">
    <div class="scroll-hint-line"></div>
    <span class="scroll-hint-text">scroll</span>
  </div>
</section>

<!-- 01 REELS -->
<section class="page" id="page-reels">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">01 / 08 — Reels Edits</div>
      <h2 class="sec-title reveal">Reels <em>Edits</em></h2>
    </div>
    <div class="card-grid">
      <div class="card wide reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#05183a,#0a3070,#2060c0);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Featured · Reel</p><p class="card-name">Drop your video here</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#031428,#0a2550);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Reel</p><p class="card-name">Reel Title</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#081c3c,#102c5a);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Reel</p><p class="card-name">Reel Title</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#051020,#0d2244);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Reel</p><p class="card-name">Reel Title</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#081830,#122e5c);"><span class="card-placeholder-icon">▶</span></div>
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

<!-- 02 CINEMATIC -->
<section class="page" id="page-cinematic">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">02 / 08 — Cinematic Videos</div>
      <h2 class="sec-title reveal">Cinematic <em>Videos</em></h2>
    </div>
    <div class="card-grid">
      <div class="card wide reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#000,#020c1e,#041428);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Featured · Cinematic</p><p class="card-name">Drop your video here</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#010810,#020f1e);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Cinematic</p><p class="card-name">Film Title</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#02101e,#031525);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Cinematic</p><p class="card-name">Film Title</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#010c18,#021220);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Cinematic</p><p class="card-name">Film Title</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#020e1c,#031828);"><span class="card-placeholder-icon">▶</span></div>
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

<!-- 03 DOCUMENTARY -->
<section class="page" id="page-documentary">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">03 / 08 — Documentary Edits</div>
      <h2 class="sec-title reveal">Documentary <em>Edits</em></h2>
    </div>
    <div class="card-grid">
      <div class="card wide reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#0a0500,#3d1400,#a03000);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Featured · Documentary</p><p class="card-name">Drop your video here</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#100700,#280f00);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Documentary</p><p class="card-name">Doc Title</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#180a00,#301500);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Documentary</p><p class="card-name">Doc Title</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#0d0600,#221000);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Documentary</p><p class="card-name">Doc Title</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#140800,#281200);"><span class="card-placeholder-icon">▶</span></div>
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

<!-- 04 BRAND -->
<section class="page" id="page-brand">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">04 / 08 — Brand Videos</div>
      <h2 class="sec-title reveal">Brand <em>Videos</em></h2>
    </div>
    <div class="card-grid">
      <div class="card wide reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#080000,#300000,#880000);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Featured · Brand</p><p class="card-name">Drop your video here</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#0e0000,#200000);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Brand</p><p class="card-name">Brand Film</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#160000,#280000);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Brand</p><p class="card-name">Brand Film</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#100000,#1c0000);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Brand</p><p class="card-name">Brand Film</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#140000,#240000);"><span class="card-placeholder-icon">▶</span></div>
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

<!-- 05 COLOR GRADING -->
<section class="page" id="page-colorgrading">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">05 / 08 — Color Grading</div>
      <h2 class="sec-title reveal">Color <em>Grading</em></h2>
    </div>
    <div class="card-grid">
      <div class="card wide reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#001a0d,#00338a,#440088,#880044);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Featured · Grade</p><p class="card-name">Drop your video here</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#001808,#003388);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Grade</p><p class="card-name">Grading Project</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#330066,#880033);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Grade</p><p class="card-name">Grading Project</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#004400,#002266);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Grade</p><p class="card-name">Grading Project</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#440000,#004466);"><span class="card-placeholder-icon">▶</span></div>
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

<!-- 06 MUSIC VIDEOS -->
<section class="page" id="page-music">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">06 / 08 — Music Videos</div>
      <h2 class="sec-title reveal">Music <em>Videos</em></h2>
    </div>
    <div class="card-grid">
      <div class="card wide reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#000,#222,#666);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Featured · Music</p><p class="card-name">Drop your video here</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#111,#333);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Music</p><p class="card-name">Music Video</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#1a1a1a,#3a3a3a);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Music</p><p class="card-name">Music Video</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#080808,#282828);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Music</p><p class="card-name">Music Video</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#0d0d0d,#2d2d2d);"><span class="card-placeholder-icon">▶</span></div>
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

<!-- 07 SONG POSTER -->
<section class="page" id="page-songposter">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">07 / 08 — Song Posters</div>
      <h2 class="sec-title reveal">Song <em>Poster</em></h2>
    </div>
    <div class="card-grid" style="grid-template-columns:repeat(auto-fill,minmax(220px,1fr));">
      <div class="card reveal" style="aspect-ratio:2/3;">
        <div class="card-placeholder" style="background:#060606;border:1px solid rgba(255,255,255,.06);"><span class="card-placeholder-icon" style="font-size:2rem;">✦</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Poster</p><p class="card-name">Song Title</p></div>
      </div>
      <div class="card reveal" style="aspect-ratio:2/3;">
        <div class="card-placeholder" style="background:#040404;border:1px solid rgba(255,255,255,.06);"><span class="card-placeholder-icon" style="font-size:2rem;">✦</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Poster</p><p class="card-name">Song Title</p></div>
      </div>
      <div class="card reveal" style="aspect-ratio:2/3;">
        <div class="card-placeholder" style="background:#080808;border:1px solid rgba(255,255,255,.06);"><span class="card-placeholder-icon" style="font-size:2rem;">✦</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Poster</p><p class="card-name">Song Title</p></div>
      </div>
      <div class="card reveal" style="aspect-ratio:2/3;">
        <div class="card-placeholder" style="background:#050505;border:1px solid rgba(255,255,255,.06);"><span class="card-placeholder-icon" style="font-size:2rem;">✦</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Poster</p><p class="card-name">Song Title</p></div>
      </div>
      <div class="card reveal" style="aspect-ratio:2/3;">
        <div class="card-placeholder" style="background:#070707;border:1px solid rgba(255,255,255,.06);"><span class="card-placeholder-icon" style="font-size:2rem;">✦</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Poster</p><p class="card-name">Song Title</p></div>
      </div>
      <div class="card reveal" style="aspect-ratio:2/3;">
        <div class="card-placeholder" style="background:#060606;border:1px solid rgba(255,255,255,.06);"><span class="card-placeholder-icon" style="font-size:2rem;">✦</span></div>
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

<!-- 08 3D VISUALISER -->
<section class="page" id="page-3d">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">08 / 08 — 3D Visualiser</div>
      <h2 class="sec-title reveal">3D <em>Visualiser</em></h2>
    </div>
    <div class="card-grid">
      <div class="card wide reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#04001a,#1a0066,#4400ff);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">Featured · 3D</p><p class="card-name">Drop your video here</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#06001c,#1c0070);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">3D</p><p class="card-name">Visualiser Project</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#08001e,#200080);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">3D</p><p class="card-name">Visualiser Project</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#040018,#140060);"><span class="card-placeholder-icon">▶</span></div>
        <div class="card-overlay"></div>
        <div class="card-info"><p class="card-cat">3D</p><p class="card-name">Visualiser Project</p></div>
      </div>
      <div class="card reveal">
        <div class="card-placeholder" style="background:linear-gradient(135deg,#0a001e,#240088);"><span class="card-placeholder-icon">▶</span></div>
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

<!-- CONTACT -->
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
// CURSOR
const cursor = document.getElementById('cursor');
const ring = document.getElementById('cursorRing');
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
document.querySelectorAll('a,button,[onclick],.card,.hero-nav-item,.contact-item,.sec-page-link,.back-btn').forEach(el=>{
  el.addEventListener('mouseenter',()=>{cursor.style.width='20px';cursor.style.height='20px';ring.style.width='60px';ring.style.height='60px';});
  el.addEventListener('mouseleave',()=>{cursor.style.width='12px';cursor.style.height='12px';ring.style.width='36px';ring.style.height='36px';});
});

// PAGE NAV
const curtain = document.getElementById('curtain');
let current = 'home';
function navigateTo(id){
  if(id===current) return;
  curtain.className='page-curtain in';
  setTimeout(()=>{
    document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
    const next = document.getElementById('page-'+id);
    if(next) next.classList.add('active');
    current = id;
    const bb = document.getElementById('backBtn');
    id==='home' ? bb.classList.remove('visible') : bb.classList.add('visible');
    window.scrollTo(0,0);
    triggerReveals();
    curtain.className='page-curtain out';
    setTimeout(()=>{ curtain.className='page-curtain'; },520);
  },480);
}
function goHome(){ navigateTo('home'); }

// REVEAL
function triggerReveals(){
  setTimeout(()=>{
    document.querySelectorAll('.page.active .reveal').forEach((el,i)=>{
      setTimeout(()=>el.classList.add('visible'), i*80);
    });
  },100);
}
triggerReveals();
const ro = new IntersectionObserver(entries=>{
  entries.forEach(e=>{ if(e.isIntersecting) e.target.classList.add('visible'); });
},{threshold:.1});
document.querySelectorAll('.reveal').forEach(el=>ro.observe(el));
</script>
</body>
</html>
