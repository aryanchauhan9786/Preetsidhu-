<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0"/>
<title>Preet Sidhu — Visual Creator</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;1,300;1,400;1,600&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;}
html{scroll-behavior:smooth;}
body{background:#000;color:#fff;font-family:'DM Mono',monospace;font-size:14px;line-height:1.7;overflow-x:hidden;cursor:none;}
img,video{max-width:100%;display:block;}
a{color:inherit;text-decoration:none;}
:root{--font-sys:-apple-system,BlinkMacSystemFont,"SF Pro Display","Helvetica Neue",Arial,sans-serif;}

.cursor{position:fixed;width:12px;height:12px;background:#fff;border-radius:50%;pointer-events:none;z-index:9999;transform:translate(-50%,-50%);transition:width .2s,height .2s;mix-blend-mode:difference;}
.cursor-ring{position:fixed;width:36px;height:36px;border:1px solid rgba(255,255,255,.4);border-radius:50%;pointer-events:none;z-index:9998;transform:translate(-50%,-50%);transition:width .2s,height .2s;}

.grain{
  position:fixed;inset:0;z-index:9990;pointer-events:none;opacity:.11;
  background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
  background-repeat:repeat;background-size:200px 200px;
  animation:grainShift .08s steps(1) infinite;
}
@keyframes grainShift{
  0%{background-position:0 0;}10%{background-position:-5% -10%;}20%{background-position:-15% 5%;}
  30%{background-position:7% -25%;}40%{background-position:-5% 25%;}50%{background-position:-15% 10%;}
  60%{background-position:15% 0%;}70%{background-position:0 15%;}80%{background-position:3% 35%;}
  90%{background-position:-10% 10%;}100%{background-position:0 0;}
}

/* NAV */
nav{position:fixed;top:0;left:0;right:0;z-index:1000;padding:1.4rem 2.5rem;display:flex;justify-content:space-between;align-items:center;}
nav::before{content:'';position:absolute;inset:0;background:linear-gradient(to bottom,rgba(0,0,0,.85),transparent);backdrop-filter:blur(10px);-webkit-backdrop-filter:blur(10px);z-index:-1;}
.nav-logo{font-family:'Cormorant Garamond',serif;font-size:1.6rem;font-weight:300;letter-spacing:.08em;color:#fff;cursor:pointer;}
.nav-logo span{font-style:italic;}
.nav-links{display:flex;gap:1.5rem;list-style:none;align-items:center;flex-wrap:wrap;}
.nav-links a{font-size:9px;letter-spacing:.18em;text-transform:uppercase;color:rgba(255,255,255,.45);transition:color .25s;position:relative;}
.nav-links a::after{content:'';position:absolute;bottom:-4px;left:0;right:0;height:1px;background:currentColor;transform:scaleX(0);transform-origin:right;transition:transform .3s ease;}
.nav-links a:hover{color:#fff;}
.nav-links a:hover::after{transform:scaleX(1);transform-origin:left;}
.nav-burger{display:none;flex-direction:column;gap:5px;cursor:pointer;padding:4px;}
.nav-burger span{width:22px;height:1px;background:#fff;display:block;}
.nav-mobile{display:none;position:fixed;inset:0;z-index:999;background:rgba(0,0,0,.97);backdrop-filter:blur(20px);flex-direction:column;align-items:center;justify-content:center;gap:2.5rem;}
.nav-mobile.open{display:flex;}
.nav-mobile a{font-family:'Cormorant Garamond',serif;font-size:2rem;font-weight:300;color:rgba(255,255,255,.7);letter-spacing:.08em;transition:color .2s;}
.nav-mobile a:hover{color:#fff;}
.nav-mobile-close{position:absolute;top:2rem;right:2.5rem;font-size:1.5rem;color:rgba(255,255,255,.4);cursor:pointer;}

/* PAGE */
.page{display:none;min-height:100vh;position:relative;overflow:hidden;}
.page.active{display:block;}
#page-home.active{display:flex;flex-direction:column;}
.page-curtain{position:fixed;inset:0;z-index:2000;background:#000;transform:translateY(-100%);pointer-events:none;}
.page-curtain.in{animation:curtainIn .5s cubic-bezier(.76,0,.24,1) forwards;}
.page-curtain.out{animation:curtainOut .5s cubic-bezier(.76,0,.24,1) forwards;}
@keyframes curtainIn{from{transform:translateY(100%);}to{transform:translateY(0);}}
@keyframes curtainOut{from{transform:translateY(0);}to{transform:translateY(-100%);}}
.reveal{opacity:0;transform:translateY(35px);transition:opacity .85s ease,transform .85s ease;}
.reveal.visible{opacity:1;transform:none;}

/* HOME */
#page-home{background:#000;}
.hero-bg{position:absolute;inset:0;z-index:0;background:radial-gradient(ellipse 65% 75% at 22% 32%,rgba(180,200,255,.09) 0%,transparent 60%),radial-gradient(ellipse 50% 60% at 80% 72%,rgba(255,210,180,.06) 0%,transparent 55%),#000;}
.hero-glow{position:absolute;top:30%;left:8%;width:55%;height:55%;z-index:1;background:radial-gradient(ellipse,rgba(255,255,255,.09) 0%,rgba(255,255,255,.03) 40%,transparent 70%);filter:blur(45px);animation:glowPulse 6s ease-in-out infinite alternate;pointer-events:none;}
@keyframes glowPulse{0%{opacity:.55;transform:scale(1);}100%{opacity:1;transform:scale(1.1);}}
.hero-scanlines{position:absolute;inset:0;z-index:1;background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(255,255,255,.012) 2px,rgba(255,255,255,.012) 4px);}
.hero-content{position:relative;z-index:2;display:flex;flex-direction:column;justify-content:flex-end;min-height:90vh;padding:0 clamp(2rem,6vw,6rem) clamp(2rem,5vh,4rem);}
.hero-eyebrow{font-size:10px;letter-spacing:.25em;text-transform:uppercase;color:rgba(255,255,255,.5);margin-bottom:1.4rem;text-shadow:0 0 20px rgba(255,255,255,.2);}
.hero-name{font-family:'Cormorant Garamond',serif;font-size:clamp(4rem,12vw,10rem);font-weight:300;line-height:.9;letter-spacing:-.02em;color:#fff;text-shadow:0 0 40px rgba(255,255,255,.14),0 0 80px rgba(180,200,255,.07);}
.hero-name em{font-style:italic;color:rgba(255,255,255,.55);}
.hero-about-block{margin-top:2rem;max-width:700px;}
.hero-about-block p{font-family:'Cormorant Garamond',serif;font-size:clamp(1.1rem,2.2vw,1.55rem);font-weight:300;font-style:italic;color:rgba(255,255,255,.72);line-height:1.6;letter-spacing:.005em;}
.hero-about-block p+p{margin-top:.9rem;}
.hero-about-block strong{font-weight:500;font-style:normal;color:#fff;}
.hero-tagline-main{margin-top:1.4rem;font-family:'Cormorant Garamond',serif;font-size:clamp(1rem,2vw,1.35rem);font-weight:300;font-style:italic;color:rgba(255,255,255,.45);max-width:680px;line-height:1.6;}
.hero-divider{width:80px;height:1px;background:rgba(255,255,255,.22);margin:2.2rem 0;}
.hero-nav-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:1px;border:1px solid rgba(255,255,255,.12);max-width:960px;margin-top:2.5rem;background:rgba(255,255,255,.02);backdrop-filter:blur(6px);}
.hero-nav-item{padding:1.4rem 1.6rem;border-right:1px solid rgba(255,255,255,.1);cursor:pointer;transition:background .3s;position:relative;overflow:hidden;}
.hero-nav-item:last-child{border-right:none;}
.hero-nav-item::before{content:'';position:absolute;inset:0;background:rgba(255,255,255,.055);transform:translateY(100%);transition:transform .3s ease;}
.hero-nav-item:hover::before{transform:translateY(0);}
.hero-nav-num{font-size:9px;letter-spacing:.14em;color:rgba(255,255,255,.32);margin-bottom:.5rem;}
.hero-nav-label{font-family:'Cormorant Garamond',serif;font-size:1.05rem;font-weight:300;color:rgba(255,255,255,.8);line-height:1.2;}
.hero-nav-label em{font-style:italic;color:rgba(255,255,255,.5);}

.hero-contact-strip{position:relative;z-index:2;padding:3rem clamp(2rem,6vw,6rem);border-top:1px solid rgba(255,255,255,.12);display:flex;align-items:flex-start;justify-content:space-between;flex-wrap:wrap;gap:2rem;background:rgba(0,0,0,.4);backdrop-filter:blur(4px);}
.home-contact-label{font-family:var(--font-sys);font-size:10px;letter-spacing:.28em;text-transform:uppercase;color:rgba(255,255,255,.4);padding-top:.6rem;flex-shrink:0;}
.home-contact-items{display:flex;align-items:flex-start;gap:clamp(2rem,6vw,6rem);flex-wrap:wrap;flex:1;}
.home-contact-item{display:flex;flex-direction:column;gap:.4rem;cursor:pointer;transition:opacity .2s;}
.home-contact-item:hover{opacity:.6;}
.hci-platform{font-family:var(--font-sys);font-size:9px;letter-spacing:.22em;text-transform:uppercase;color:rgba(255,255,255,.38);}
.hci-value{font-family:var(--font-sys);font-size:clamp(1.1rem,2.1vw,1.55rem);font-weight:300;letter-spacing:-.01em;color:#fff;line-height:1.2;position:relative;display:inline-block;}
.hci-value em{font-style:italic;color:rgba(255,255,255,.75);}
.hci-value::after{content:'';position:absolute;left:0;bottom:-4px;width:100%;height:1px;background:rgba(255,255,255,.28);transform:scaleX(0);transform-origin:left;transition:transform .3s ease;}
.home-contact-item:hover .hci-value::after{transform:scaleX(1);}
.hero-bottom{position:relative;z-index:2;padding:1.4rem clamp(2rem,6vw,6rem);display:flex;justify-content:space-between;align-items:center;border-top:1px solid rgba(255,255,255,.07);}
.hero-bottom-info{font-family:var(--font-sys);font-size:11px;letter-spacing:.1em;color:rgba(255,255,255,.28);}
.scroll-hint{position:absolute;right:3rem;bottom:10rem;display:flex;flex-direction:column;align-items:center;gap:.6rem;z-index:10;}
.scroll-hint-line{width:1px;height:50px;background:rgba(255,255,255,.2);position:relative;overflow:hidden;}
.scroll-hint-line::after{content:'';position:absolute;top:0;left:0;right:0;height:50%;background:#fff;animation:scrollLine 2s ease-in-out infinite;}
@keyframes scrollLine{0%{transform:translateY(-100%);}100%{transform:translateY(200%);}}
.scroll-hint-text{font-size:8px;letter-spacing:.2em;text-transform:uppercase;color:rgba(255,255,255,.28);writing-mode:vertical-rl;}

/* SECTIONS */
.sec-inner{position:relative;z-index:2;min-height:100vh;display:flex;flex-direction:column;padding:clamp(5rem,10vh,8rem) clamp(1.5rem,4vw,4rem) clamp(2rem,4vh,4rem);}
.sec-label{font-size:9px;letter-spacing:.22em;text-transform:uppercase;color:rgba(255,255,255,.45);margin-bottom:.8rem;display:flex;align-items:center;gap:.8rem;}
.sec-label::before{content:'';display:inline-block;width:28px;height:1px;background:currentColor;}
.sec-title{font-family:'Cormorant Garamond',serif;font-size:clamp(2.6rem,6vw,5rem);font-weight:300;line-height:1;letter-spacing:-.02em;}
.sec-title em{font-style:italic;}
.sec-header{margin-bottom:2.5rem;}

/* ══════════════════════════════
   CARD SYSTEM
══════════════════════════════ */
.card-list{display:flex;flex-direction:column;gap:2rem;flex:1;}

/* Two-col grid for 9:16 reels */
.card-list.two-col-tall{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(260px,1fr));
  gap:1.5rem;
}
.card-list.two-col-tall .card-item{margin-bottom:0;}

/* Two-col grid for 16:9 wide videos */
.card-list.two-col-wide{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(380px,1fr));
  gap:1.5rem;
}
.card-list.two-col-wide .card-item{margin-bottom:0;}

/* Four-col grid for posters */
.card-list.four-col{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(200px,1fr));
  gap:1.5rem;
}
.card-list.four-col .card-item{margin-bottom:0;}

/* Color grading — 3-col square */
.card-list.three-col-square{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(280px,1fr));
  gap:1.5rem;
}
.card-list.three-col-square .card-item{margin-bottom:0;}

.card-item{display:flex;flex-direction:column;border:1px solid rgba(255,255,255,.07);cursor:pointer;transition:border-color .3s;}
.card-item:hover{border-color:rgba(255,255,255,.22);}

.card-media{position:relative;overflow:hidden;background:#050505;width:100%;}
.card-media img,.card-media video{width:100%;height:100%;object-fit:cover;display:block;transition:transform .6s cubic-bezier(.25,.46,.45,.94);}
.card-item:hover .card-media img,
.card-item:hover .card-media video{transform:scale(1.03);}

/* Gradient placeholder */
.card-media-inner{width:100%;height:100%;display:flex;align-items:center;justify-content:center;position:relative;}

.play-btn{
  width:58px;height:58px;border-radius:50%;
  background:rgba(255,255,255,.15);backdrop-filter:blur(8px);
  display:flex;align-items:center;justify-content:center;
  border:1px solid rgba(255,255,255,.25);
  transition:background .3s,transform .3s;
  flex-shrink:0;
  position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);
}
.card-item:hover .play-btn{background:rgba(255,255,255,.28);transform:translate(-50%,-50%) scale(1.08);}
.play-btn svg{width:18px;height:18px;fill:#fff;margin-left:3px;}

/* Poster cards — no play btn */
.card-media.is-poster .play-btn{display:none;}

.card-meta{padding:1rem 1.2rem 1.2rem;border-top:1px solid rgba(255,255,255,.07);background:rgba(0,0,0,.3);}
.card-tag{display:inline-block;font-size:8px;letter-spacing:.18em;text-transform:uppercase;color:rgba(255,255,255,.55);border:1px solid rgba(255,255,255,.18);padding:.2rem .6rem;margin-bottom:.55rem;}
.card-title-text{font-family:'Cormorant Garamond',serif;font-size:1.2rem;font-weight:300;color:rgba(255,255,255,.8);letter-spacing:.02em;}

/* ══════════════════════════════
   ASPECT RATIOS
   Reels        = 9:16  (tall portrait)
   Cinematic    = 16:9  (landscape)
   Documentary  = 16:9
   Brand        = 16:9
   Music        = 16:9
   3D           = 16:9
   Color Grade  = 1:1   (square — matches image style)
   Song Poster  = 3:4   (portrait — matches Badla/Entry etc)
══════════════════════════════ */
.ratio-9-16  .card-media{aspect-ratio:9/16;}
.ratio-16-9  .card-media{aspect-ratio:16/9;}
.ratio-square .card-media{aspect-ratio:1/1;}
.ratio-poster .card-media{aspect-ratio:3/4;}

/* Section nav */
.sec-page-nav{display:flex;justify-content:space-between;align-items:center;padding:2rem clamp(1.5rem,4vw,4rem);border-top:1px solid rgba(255,255,255,.08);position:relative;z-index:2;}
.sec-page-links{display:flex;gap:1.5rem;}
.sec-page-link{font-size:9px;letter-spacing:.15em;text-transform:uppercase;color:rgba(255,255,255,.38);cursor:pointer;transition:color .2s;}
.sec-page-link:hover{color:#fff;}
.sec-count{font-size:9px;letter-spacing:.1em;color:rgba(255,255,255,.28);}

/* CONTACT */
#page-contact{background:#000;}
#page-contact::after{content:'';position:absolute;inset:0;background:radial-gradient(ellipse 70% 50% at 50% 50%,rgba(255,255,255,.04) 0%,transparent 60%);}
.contact-grid{display:grid;grid-template-columns:1fr 1fr;gap:clamp(3rem,8vw,8rem);align-items:center;margin-top:3rem;}
.contact-heading{font-family:'Cormorant Garamond',serif;font-size:clamp(3.5rem,8vw,7rem);font-weight:300;line-height:.95;letter-spacing:-.02em;}
.contact-heading em{font-style:italic;color:rgba(255,255,255,.4);}
.contact-sub{margin-top:2rem;font-size:12px;color:rgba(255,255,255,.38);line-height:1.9;max-width:360px;}
.contact-items{display:flex;flex-direction:column;}
.contact-item{padding:1.8rem 0;border-bottom:1px solid rgba(255,255,255,.08);display:flex;align-items:flex-start;gap:1.5rem;cursor:pointer;transition:padding-left .3s;}
.contact-item:hover{padding-left:.8rem;}
.contact-item:first-child{border-top:1px solid rgba(255,255,255,.08);}
.ci-num{font-size:9px;letter-spacing:.14em;color:rgba(255,255,255,.28);padding-top:.2rem;}
.ci-platform{font-family:var(--font-sys);font-size:9px;letter-spacing:.2em;text-transform:uppercase;color:rgba(255,255,255,.38);margin-bottom:.3rem;}
.ci-value{font-family:var(--font-sys);font-size:1.4rem;font-weight:300;letter-spacing:.01em;}
.ci-value em{font-style:italic;color:rgba(255,255,255,.7);}

/* PAGE BACKGROUNDS */
#page-reels{background:linear-gradient(135deg,#050e1a 0%,#0a1f3d 30%,#0d2952 55%,#d0dcff 100%);}
#page-reels::after{content:'';position:absolute;inset:0;background:linear-gradient(to bottom,transparent 40%,rgba(0,0,10,.65) 100%);}
#page-cinematic{background:linear-gradient(160deg,#000 0%,#020d1f 40%,#041428 65%,#e8edf5 100%);}
#page-cinematic::after{content:'';position:absolute;inset:0;background:linear-gradient(to bottom,rgba(0,0,20,.3) 0%,rgba(0,0,20,.7) 100%);}
#page-documentary{background:linear-gradient(140deg,#0a0500 0%,#1a0800 25%,#3d1400 50%,#c45c00 80%,#e87020 100%);}
#page-documentary::after{content:'';position:absolute;inset:0;background:linear-gradient(to bottom,rgba(10,5,0,.5) 0%,rgba(10,5,0,.3) 100%);}
#page-brand{background:linear-gradient(135deg,#080000 0%,#1a0000 30%,#3d0000 55%,#cc0000 80%,#ff1a00 100%);}
#page-brand::after{content:'';position:absolute;inset:0;background:linear-gradient(to bottom,rgba(8,0,0,.4) 0%,rgba(8,0,0,.3) 100%);}
#page-colorgrading{background:radial-gradient(ellipse 50% 50% at 20% 40%,#00ff66 0%,transparent 40%),radial-gradient(ellipse 50% 60% at 50% 50%,#3300ff 0%,transparent 50%),radial-gradient(ellipse 40% 50% at 80% 60%,#ff6600 0%,transparent 40%),radial-gradient(ellipse 30% 40% at 40% 80%,#ff00cc 0%,transparent 35%),radial-gradient(ellipse 30% 30% at 70% 20%,#0099ff 0%,transparent 30%),#000;}
#page-colorgrading::after{content:'';position:absolute;inset:0;background:rgba(0,0,0,.34);}
#page-music{background:linear-gradient(160deg,#000 0%,#111 40%,#888 75%,#f5f5f5 100%);}
#page-music::after{content:'';position:absolute;inset:0;background:linear-gradient(to bottom,rgba(0,0,0,.5) 0%,rgba(0,0,0,.2) 100%);}
#page-songposter{background:#000;}
#page-songposter::after{content:'';position:absolute;inset:0;background:radial-gradient(ellipse 50% 50% at 50% 50%,rgba(255,255,255,.025) 0%,transparent 70%);}
#page-3d{background:linear-gradient(140deg,#04001a 0%,#0d0030 25%,#1a0066 50%,#2200aa 70%,#4400ff 85%,#6633ff 100%);}
#page-3d::after{content:'';position:absolute;inset:0;background:radial-gradient(ellipse 60% 60% at 80% 20%,rgba(100,0,255,.3) 0%,transparent 50%),radial-gradient(ellipse 40% 40% at 20% 80%,rgba(0,80,255,.2) 0%,transparent 40%);}

@media(max-width:900px){
  nav{padding:1.2rem 1.5rem;}
  .nav-links{display:none;}
  .nav-burger{display:flex;}
  .hero-nav-grid{grid-template-columns:repeat(2,1fr);}
  .sec-inner{padding:5rem 1.2rem 2.5rem;}
  .contact-grid{grid-template-columns:1fr;}
  .card-list.two-col-wide{grid-template-columns:1fr;}
  .card-list.two-col-tall{grid-template-columns:repeat(2,1fr);}
  .card-list.four-col{grid-template-columns:repeat(2,1fr);}
  .card-list.three-col-square{grid-template-columns:repeat(2,1fr);}
  .hero-contact-strip{flex-direction:column;align-items:flex-start;gap:1.5rem;}
  .scroll-hint{display:none;}
}
@media(max-width:480px){
  .hero-name{font-size:clamp(3.2rem,16vw,5rem);}
  .card-list.two-col-tall,.card-list.four-col,.card-list.three-col-square{grid-template-columns:repeat(2,1fr);}
  .hci-value{font-size:1rem;}
}
</style>
</head>
<body>

<div class="grain"></div>
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>
<div class="page-curtain" id="curtain"></div>

<div class="nav-mobile" id="mobileNav">
  <span class="nav-mobile-close" onclick="closeMobileNav()">✕</span>
  <a href="#" onclick="navigateTo('reels');closeMobileNav();return false;">Reels</a>
  <a href="#" onclick="navigateTo('cinematic');closeMobileNav();return false;">Cinematic</a>
  <a href="#" onclick="navigateTo('documentary');closeMobileNav();return false;">Documentary</a>
  <a href="#" onclick="navigateTo('brand');closeMobileNav();return false;">Brand</a>
  <a href="#" onclick="navigateTo('colorgrading');closeMobileNav();return false;">Grading</a>
  <a href="#" onclick="navigateTo('music');closeMobileNav();return false;">Music</a>
  <a href="#" onclick="navigateTo('songposter');closeMobileNav();return false;">Poster</a>
  <a href="#" onclick="navigateTo('3d');closeMobileNav();return false;">3D</a>
  <a href="#" onclick="navigateTo('contact');closeMobileNav();return false;">Contact</a>
</div>

<nav>
  <div class="nav-logo" onclick="navigateTo('home')">P<span>reet</span></div>
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
  <div class="nav-burger" onclick="openMobileNav()"><span></span><span></span><span></span></div>
</nav>

<!-- HOME -->
<section class="page active" id="page-home">
  <div class="hero-bg"></div><div class="hero-glow"></div><div class="hero-scanlines"></div>
  <div class="hero-content">
    <p class="hero-eyebrow reveal">Visual Creator · Editor · Motion Designer · Chandigarh</p>
    <h1 class="hero-name reveal">Preet<br><em>Sidhu</em></h1>
    <div class="hero-about-block reveal">
      <p>I'm <strong>Preet Sidhu</strong> — a visual creator obsessed with the space between a raw idea and a finished cinematic moment.</p>
      <p>From motion graphics that stop thumbs mid-scroll to long-form cinematic edits that hold you in your seat — I craft stories that move people, frame by frame.</p>
    </div>
    <p class="hero-tagline-main reveal">From concept to final cut — creating visuals that move people, tell stories, and make every second count.</p>
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
        <span class="hci-platform">Instagram</span><span class="hci-value"><em>@Preet_Sidhu_364</em></span>
      </div>
      <div class="home-contact-item" onclick="window.location='mailto:preett978@gmail.com'">
        <span class="hci-platform">Gmail</span><span class="hci-value">preett978@gmail.com</span>
      </div>
      <div class="home-contact-item" onclick="window.location='tel:+918360747667'">
        <span class="hci-platform">Phone</span><span class="hci-value">+91&nbsp;83607&nbsp;47667</span>
      </div>
    </div>
  </div>
  <div class="hero-bottom">
    <span class="hero-bottom-info">© 2026 Preet Sidhu</span>
    <span class="hero-bottom-info" onclick="navigateTo('contact')" style="cursor:pointer;">Contact →</span>
  </div>
  <div class="scroll-hint"><div class="scroll-hint-line"></div><span class="scroll-hint-text">scroll</span></div>
</section>

<!-- 01 REELS — 9:16 TALL PORTRAIT -->
<section class="page" id="page-reels">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">01 / 08 — Reels Edits</div>
      <h2 class="sec-title reveal">Reels <em>Edits</em></h2>
    </div>
    <div class="card-list ratio-9-16 two-col-tall">
      <div class="card-item reveal">
        <div class="card-media">
          <!-- <video src="reel1.mp4" muted loop playsinline></video> -->
          <div class="card-media-inner" style="background:linear-gradient(160deg,#05183a,#0a3070,#1a4a9a);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Featured · Reel</span><p class="card-title-text">Drop your reel title here</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(160deg,#031428,#0a2550);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Reel</span><p class="card-title-text">Reel Title</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(160deg,#081c3c,#102c5a);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Reel</span><p class="card-title-text">Reel Title</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(160deg,#051020,#0d2244);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Reel</span><p class="card-title-text">Reel Title</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(160deg,#061828,#0e2e50);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Reel</span><p class="card-title-text">Reel Title</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(160deg,#040e20,#0a1e40);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Reel</span><p class="card-title-text">Reel Title</p></div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links"><span class="sec-page-link" onclick="navigateTo('home')">Home</span><span class="sec-page-link" onclick="navigateTo('cinematic')">Next: Cinematic →</span></div>
    <span class="sec-count">01 / 08</span>
  </div>
</section>

<!-- 02 CINEMATIC — 16:9 LANDSCAPE -->
<section class="page" id="page-cinematic">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">02 / 08 — Cinematic Videos</div>
      <h2 class="sec-title reveal">Cinematic <em>Videos</em></h2>
    </div>
    <div class="card-list ratio-16-9 two-col-wide">
      <div class="card-item reveal">
        <div class="card-media">
          <!-- <video src="cinematic1.mp4" muted loop playsinline></video> -->
          <div class="card-media-inner" style="background:linear-gradient(135deg,#000,#020c1e,#041428);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Featured · Cinematic</span><p class="card-title-text">Drop your video title here</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#010810,#020f1e);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Cinematic</span><p class="card-title-text">Film Title</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#02101e,#031525);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Cinematic</span><p class="card-title-text">Film Title</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#010c18,#021220);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Cinematic</span><p class="card-title-text">Film Title</p></div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links"><span class="sec-page-link" onclick="navigateTo('reels')">← Reels</span><span class="sec-page-link" onclick="navigateTo('documentary')">Next: Documentary →</span></div>
    <span class="sec-count">02 / 08</span>
  </div>
</section>

<!-- 03 DOCUMENTARY — 16:9 LANDSCAPE -->
<section class="page" id="page-documentary">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">03 / 08 — Documentary Edits</div>
      <h2 class="sec-title reveal">Documentary <em>Edits</em></h2>
    </div>
    <div class="card-list ratio-16-9 two-col-wide">
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#0a0500,#3d1400,#a03000);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Featured · Documentary</span><p class="card-title-text">Drop your video title here</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#100700,#280f00);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Documentary</span><p class="card-title-text">Doc Title</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#180a00,#301500);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Documentary</span><p class="card-title-text">Doc Title</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#0d0600,#221000);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Documentary</span><p class="card-title-text">Doc Title</p></div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links"><span class="sec-page-link" onclick="navigateTo('cinematic')">← Cinematic</span><span class="sec-page-link" onclick="navigateTo('brand')">Next: Brand →</span></div>
    <span class="sec-count">03 / 08</span>
  </div>
</section>

<!-- 04 BRAND — 16:9 LANDSCAPE -->
<section class="page" id="page-brand">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">04 / 08 — Brand Videos</div>
      <h2 class="sec-title reveal">Brand <em>Videos</em></h2>
    </div>
    <div class="card-list ratio-16-9 two-col-wide">
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#080000,#300000,#880000);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Featured · Brand</span><p class="card-title-text">Drop your video title here</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#0e0000,#200000);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Brand</span><p class="card-title-text">Brand Film</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#160000,#280000);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Brand</span><p class="card-title-text">Brand Film</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#100000,#1c0000);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Brand</span><p class="card-title-text">Brand Film</p></div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links"><span class="sec-page-link" onclick="navigateTo('documentary')">← Documentary</span><span class="sec-page-link" onclick="navigateTo('colorgrading')">Next: Color Grading →</span></div>
    <span class="sec-count">04 / 08</span>
  </div>
</section>

<!-- 05 COLOR GRADING — 1:1 SQUARE -->
<section class="page" id="page-colorgrading">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">05 / 08 — Color Grading</div>
      <h2 class="sec-title reveal">Color <em>Grading</em></h2>
    </div>
    <div class="card-list ratio-square three-col-square">
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#001a0d,#00338a,#440088,#880044);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Featured · Grade</span><p class="card-title-text">Drop your project here</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#001808,#003388);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Grade</span><p class="card-title-text">Grading Project</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#330066,#880033);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Grade</span><p class="card-title-text">Grading Project</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#004400,#002266);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Grade</span><p class="card-title-text">Grading Project</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#220044,#004466);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Grade</span><p class="card-title-text">Grading Project</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#440022,#002244);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Grade</span><p class="card-title-text">Grading Project</p></div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links"><span class="sec-page-link" onclick="navigateTo('brand')">← Brand</span><span class="sec-page-link" onclick="navigateTo('music')">Next: Music Videos →</span></div>
    <span class="sec-count">05 / 08</span>
  </div>
</section>

<!-- 06 MUSIC — 16:9 LANDSCAPE -->
<section class="page" id="page-music">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">06 / 08 — Music Videos</div>
      <h2 class="sec-title reveal">Music <em>Videos</em></h2>
    </div>
    <div class="card-list ratio-16-9 two-col-wide">
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#000,#222,#555);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Featured · Music</span><p class="card-title-text">Drop your video title here</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#111,#333);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Music</span><p class="card-title-text">Music Video</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#1a1a1a,#3a3a3a);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Music</span><p class="card-title-text">Music Video</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#080808,#282828);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Music</span><p class="card-title-text">Music Video</p></div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links"><span class="sec-page-link" onclick="navigateTo('colorgrading')">← Color Grading</span><span class="sec-page-link" onclick="navigateTo('songposter')">Next: Song Poster →</span></div>
    <span class="sec-count">06 / 08</span>
  </div>
</section>

<!-- 07 SONG POSTER — 3:4 PORTRAIT with real images -->
<section class="page" id="page-songposter">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">07 / 08 — Song Posters</div>
      <h2 class="sec-title reveal">Song <em>Poster</em></h2>
    </div>
    <div class="card-list ratio-poster four-col">

      <!-- Entry — Amrit Maan (IMG_5783) -->
      <div class="card-item reveal">
        <div class="card-media is-poster">
          <img src="/mnt/user-data/uploads/IMG_5783.jpeg" alt="Entry — Amrit Maan" loading="lazy"/>
        </div>
        <div class="card-meta">
          <span class="card-tag">Poster · Artwork</span>
          <p class="card-title-text">Entry — Amrit Maan</p>
        </div>
      </div>

      <!-- Jatt Lagde — Noor Tung (IMG_5781) -->
      <div class="card-item reveal">
        <div class="card-media is-poster">
          <img src="/mnt/user-data/uploads/IMG_5781.jpeg" alt="Jatt Lagde — Noor Tung" loading="lazy"/>
        </div>
        <div class="card-meta">
          <span class="card-tag">Poster · Artwork</span>
          <p class="card-title-text">Jatt Lagde — Noor Tung</p>
        </div>
      </div>

      <!-- Badla — Watan Sahi (IMG_5779) -->
      <div class="card-item reveal">
        <div class="card-media is-poster">
          <img src="/mnt/user-data/uploads/IMG_5779.jpeg" alt="Badla — Watan Sahi" loading="lazy"/>
        </div>
        <div class="card-meta">
          <span class="card-tag">Poster · Artwork</span>
          <p class="card-title-text">Badla — Watan Sahi</p>
        </div>
      </div>

      <!-- Waari Jaavan — Satkar Sandhu (IMG_5782) -->
      <div class="card-item reveal">
        <div class="card-media is-poster">
          <img src="/mnt/user-data/uploads/IMG_5782.jpeg" alt="Waari Jaavan — Satkar Sandhu" loading="lazy"/>
        </div>
        <div class="card-meta">
          <span class="card-tag">Poster · Artwork</span>
          <p class="card-title-text">Waari Jaavan — Satkar Sandhu</p>
        </div>
      </div>

      <!-- Placeholder slots -->
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:#060606;border:1px solid rgba(255,255,255,.06);">
            <div class="play-btn" style="background:rgba(255,255,255,.05);border-color:rgba(255,255,255,.1);">
              <svg viewBox="0 0 24 24" style="margin-left:0;"><path d="M19 13H13V19H11V13H5V11H11V5H13V11H19V13Z" fill="#fff"/></svg>
            </div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Poster</span><p class="card-title-text">Coming Soon</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:#040404;border:1px solid rgba(255,255,255,.06);">
            <div class="play-btn" style="background:rgba(255,255,255,.05);border-color:rgba(255,255,255,.1);">
              <svg viewBox="0 0 24 24" style="margin-left:0;"><path d="M19 13H13V19H11V13H5V11H11V5H13V11H19V13Z" fill="#fff"/></svg>
            </div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Poster</span><p class="card-title-text">Coming Soon</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:#050505;border:1px solid rgba(255,255,255,.06);">
            <div class="play-btn" style="background:rgba(255,255,255,.05);border-color:rgba(255,255,255,.1);">
              <svg viewBox="0 0 24 24" style="margin-left:0;"><path d="M19 13H13V19H11V13H5V11H11V5H13V11H19V13Z" fill="#fff"/></svg>
            </div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Poster</span><p class="card-title-text">Coming Soon</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:#030303;border:1px solid rgba(255,255,255,.06);">
            <div class="play-btn" style="background:rgba(255,255,255,.05);border-color:rgba(255,255,255,.1);">
              <svg viewBox="0 0 24 24" style="margin-left:0;"><path d="M19 13H13V19H11V13H5V11H11V5H13V11H19V13Z" fill="#fff"/></svg>
            </div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Poster</span><p class="card-title-text">Coming Soon</p></div>
      </div>

    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links"><span class="sec-page-link" onclick="navigateTo('music')">← Music Videos</span><span class="sec-page-link" onclick="navigateTo('3d')">Next: 3D Visualiser →</span></div>
    <span class="sec-count">07 / 08</span>
  </div>
</section>

<!-- 08 3D — 16:9 LANDSCAPE -->
<section class="page" id="page-3d">
  <div class="sec-inner">
    <div class="sec-header">
      <div class="sec-label reveal">08 / 08 — 3D Visualiser</div>
      <h2 class="sec-title reveal">3D <em>Visualiser</em></h2>
    </div>
    <div class="card-list ratio-16-9 two-col-wide">
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#04001a,#1a0066,#4400ff);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">Featured · 3D</span><p class="card-title-text">Drop your video title here</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#06001c,#1c0070);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">3D</span><p class="card-title-text">Visualiser Project</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#08001e,#200080);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">3D</span><p class="card-title-text">Visualiser Project</p></div>
      </div>
      <div class="card-item reveal">
        <div class="card-media">
          <div class="card-media-inner" style="background:linear-gradient(135deg,#040018,#140060);">
            <div class="play-btn"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div>
          </div>
        </div>
        <div class="card-meta"><span class="card-tag">3D</span><p class="card-title-text">Visualiser Project</p></div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav">
    <div class="sec-page-links"><span class="sec-page-link" onclick="navigateTo('songposter')">← Song Poster</span><span class="sec-page-link" onclick="navigateTo('contact')">Contact →</span></div>
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
            <div><p class="ci-platform">Phone</p><p class="ci-value">+91&nbsp;83607&nbsp;47667</p></div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="sec-page-nav" style="position:relative;z-index:2;">
    <div class="sec-page-links"><span class="sec-page-link" onclick="navigateTo('home')">← Home</span></div>
    <span class="sec-count">© 2026 Preet Sidhu</span>
  </div>
</section>

<script>
const cursor=document.getElementById('cursor');
const ring=document.getElementById('cursorRing');
let mx=0,my=0,rx=0,ry=0;
document.addEventListener('mousemove',e=>{mx=e.clientX;my=e.clientY;cursor.style.left=mx+'px';cursor.style.top=my+'px';});
(function loop(){rx+=(mx-rx)*.12;ry+=(my-ry)*.12;ring.style.left=rx+'px';ring.style.top=ry+'px';requestAnimationFrame(loop);})();
document.querySelectorAll('a,button,[onclick],.card-item,.hero-nav-item,.contact-item,.home-contact-item,.sec-page-link').forEach(el=>{
  el.addEventListener('mouseenter',()=>{cursor.style.width='20px';cursor.style.height='20px';ring.style.width='60px';ring.style.height='60px';});
  el.addEventListener('mouseleave',()=>{cursor.style.width='12px';cursor.style.height='12px';ring.style.width='36px';ring.style.height='36px';});
});

function openMobileNav(){document.getElementById('mobileNav').classList.add('open');}
function closeMobileNav(){document.getElementById('mobileNav').classList.remove('open');}

const curtain=document.getElementById('curtain');
let historyStack=['home'];
let currentPage='home';
let isAnimating=false;

function showPage(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.reveal.visible').forEach(el=>el.classList.remove('visible'));
  const next=document.getElementById('page-'+id);
  if(next)next.classList.add('active');
  currentPage=id;window.scrollTo(0,0);triggerReveals();
}
function navigateTo(id){
  if(id===currentPage||isAnimating)return;
  isAnimating=true;
  curtain.className='page-curtain in';
  setTimeout(()=>{historyStack.push(id);showPage(id);curtain.className='page-curtain out';setTimeout(()=>{curtain.className='page-curtain';isAnimating=false;},520);},480);
}
function goBack(){
  if(historyStack.length<=1||isAnimating)return;
  isAnimating=true;historyStack.pop();
  const prev=historyStack[historyStack.length-1];
  curtain.className='page-curtain in';
  setTimeout(()=>{showPage(prev);curtain.className='page-curtain out';setTimeout(()=>{curtain.className='page-curtain';isAnimating=false;},520);},480);
}

window.addEventListener('mouseup',e=>{if(e.button===3)goBack();});
window.addEventListener('mousedown',e=>{if(e.button===3||e.button===4)e.preventDefault();});
history.pushState(null,'',window.location.href);
window.addEventListener('popstate',()=>{history.pushState(null,'',window.location.href);goBack();});

let touchStartX=0,touchStartY=0;
document.addEventListener('touchstart',e=>{touchStartX=e.touches[0].clientX;touchStartY=e.touches[0].clientY;},{passive:true});
document.addEventListener('touchend',e=>{
  const dx=e.changedTouches[0].clientX-touchStartX;
  const dy=Math.abs(e.changedTouches[0].clientY-touchStartY);
  if(dx>72&&dy<60)goBack();
},{passive:true});

function triggerReveals(){
  setTimeout(()=>{document.querySelectorAll('.page.active .reveal').forEach((el,i)=>{setTimeout(()=>el.classList.add('visible'),i*80);});},120);
}
const ro=new IntersectionObserver(entries=>{entries.forEach(e=>{if(e.isIntersecting)e.target.classList.add('visible');});},{threshold:0.1});
document.querySelectorAll('.reveal').forEach(el=>ro.observe(el));
triggerReveals();
</script>
</body>
</html>

