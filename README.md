# ludo-star-<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Ludo Star 3D</title>

<!-- ═══ GOOGLE ADSENSE ═══ -->
<!-- STEP 1: Replace ca-pub-XXXXXXXXXXXXXXXXX with YOUR AdSense Publisher ID -->
<script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-XXXXXXXXXXXXXXXXX"
     crossorigin="anonymous"></script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Fredoka+One&family=Nunito:wght@700;800&display=swap');

:root{
  --red:#ff1a3a;--red-d:#990020;--red-l:#ffc0cc;
  --green:#00bb44;--green-d:#006622;--green-l:#aaffcc;
  --yellow:#ffcc00;--yellow-d:#997700;--yellow-l:#fff3a0;
  --blue:#1166ff;--blue-d:#003399;--blue-l:#aaccff;
  --gold:#ffd700;
}

*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent;touch-action:manipulation;user-select:none}

html,body{
  width:100%;height:100%;overflow:hidden;
  font-family:'Nunito',sans-serif;
  background:#0a0118;
}

/* ═══════════ AUTH SCREEN (Login / Signup) ═══════════ */
#authScreen{
  position:fixed;inset:0;z-index:900;
  display:flex;flex-direction:column;align-items:center;justify-content:center;
  padding:16px;
  overflow-y:auto;
  background:#07010f;
}
.auth-bg{position:absolute;inset:0;overflow:hidden;pointer-events:none}
.auth-bg .orb{
  position:absolute;border-radius:50%;filter:blur(60px);
  animation:orbFloat 8s ease-in-out infinite;
}
@keyframes orbFloat{0%,100%{transform:translateY(0) scale(1)}50%{transform:translateY(-30px) scale(1.1)}}

.auth-logo{
  text-align:center;margin-bottom:22px;flex-shrink:0;
}
.auth-logo .logo-txt{
  font-family:'Fredoka One',cursive;
  font-size:clamp(2.4rem,9vw,3.8rem);
  background:linear-gradient(135deg,#ff4400,#ffcc00,#00ff88,#0088ff);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
  letter-spacing:4px;filter:drop-shadow(0 0 28px rgba(255,180,0,.7));
  animation:logoPulse 2.5s ease-in-out infinite;
}
.auth-logo .logo-tag{
  color:rgba(255,255,255,.4);font-size:.75rem;letter-spacing:5px;margin-top:2px;
}

.auth-card{
  background:rgba(255,255,255,.05);
  border:1px solid rgba(255,215,0,.2);
  border-radius:26px;padding:28px 24px 24px;
  width:100%;max-width:380px;
  backdrop-filter:blur(24px);
  box-shadow:0 0 60px rgba(255,120,0,.1),0 40px 80px rgba(0,0,0,.6);
  position:relative;z-index:1;
}

/* Tab switcher */
.auth-tabs{display:flex;background:rgba(255,255,255,.06);border-radius:14px;padding:4px;margin-bottom:24px;gap:4px}
.auth-tab{
  flex:1;padding:10px;border:none;border-radius:10px;
  font-family:'Fredoka One',cursive;font-size:.95rem;letter-spacing:1.5px;
  cursor:pointer;transition:all .25s;
  background:transparent;color:rgba(255,255,255,.4);
}
.auth-tab.active{
  background:linear-gradient(135deg,#ff6600,#ffcc00);
  color:#1a0800;
  box-shadow:0 4px 16px rgba(255,120,0,.4);
}

/* Form fields */
.auth-field{
  position:relative;margin-bottom:14px;
}
.auth-field label{
  display:block;font-size:.72rem;font-weight:800;letter-spacing:2px;
  color:rgba(255,255,255,.5);margin-bottom:6px;text-transform:uppercase;
}
.auth-field input{
  width:100%;padding:13px 16px 13px 44px;
  background:rgba(255,255,255,.07);
  border:1.5px solid rgba(255,255,255,.1);
  border-radius:12px;color:white;
  font-family:'Nunito',sans-serif;font-size:.95rem;font-weight:700;
  outline:none;transition:all .22s;
  -webkit-text-fill-color:white;
}
.auth-field input::placeholder{color:rgba(255,255,255,.28);-webkit-text-fill-color:rgba(255,255,255,.28)}
.auth-field input:focus{
  border-color:rgba(255,215,0,.55);
  background:rgba(255,255,255,.1);
  box-shadow:0 0 0 3px rgba(255,215,0,.1);
}
.auth-field .ficon{
  position:absolute;left:14px;bottom:13px;
  font-size:1.1rem;pointer-events:none;
}
.auth-field .eye-toggle{
  position:absolute;right:14px;bottom:12px;
  font-size:1rem;cursor:pointer;opacity:.5;
  background:none;border:none;color:white;padding:0;
}
.auth-field .eye-toggle:hover{opacity:.9}

/* Avatar picker */
.avatar-row{
  display:flex;gap:8px;justify-content:center;margin-bottom:16px;flex-wrap:wrap;
}
.av-btn{
  width:48px;height:48px;border-radius:50%;border:2.5px solid rgba(255,255,255,.15);
  background:rgba(255,255,255,.06);font-size:1.5rem;cursor:pointer;
  transition:all .22s;display:flex;align-items:center;justify-content:center;
}
.av-btn.picked{border-color:var(--gold);box-shadow:0 0 16px rgba(255,215,0,.5);transform:scale(1.15)}

/* Error / success messages */
.auth-err{
  background:rgba(255,50,50,.15);border:1px solid rgba(255,80,80,.3);
  border-radius:10px;padding:9px 14px;
  color:#ff8888;font-size:.78rem;font-weight:700;
  margin-bottom:14px;display:none;letter-spacing:.5px;
}
.auth-err.show{display:block}
.auth-ok{
  background:rgba(0,200,80,.12);border:1px solid rgba(0,200,80,.3);
  border-radius:10px;padding:9px 14px;
  color:#88ffaa;font-size:.78rem;font-weight:700;
  margin-bottom:14px;display:none;letter-spacing:.5px;
}
.auth-ok.show{display:block}

/* Submit button */
.auth-submit{
  width:100%;padding:15px;border:none;border-radius:14px;
  background:linear-gradient(135deg,#ffe566,#ff6600);
  font-family:'Fredoka One',cursive;font-size:1.15rem;
  color:#1a0800;cursor:pointer;letter-spacing:3px;
  box-shadow:0 6px 22px rgba(255,100,0,.45);
  transition:all .2s;margin-top:4px;
}
.auth-submit:active{transform:scale(.96)}
.auth-submit:disabled{opacity:.4;cursor:not-allowed}

/* Divider */
.auth-divider{
  display:flex;align-items:center;gap:12px;margin:16px 0;
}
.auth-divider::before,.auth-divider::after{
  content:'';flex:1;height:1px;background:rgba(255,255,255,.1);
}
.auth-divider span{color:rgba(255,255,255,.3);font-size:.75rem;letter-spacing:2px;font-weight:700}

/* Guest button */
.guest-btn{
  width:100%;padding:12px;border:1.5px solid rgba(255,255,255,.15);
  border-radius:14px;background:transparent;
  font-family:'Fredoka One',cursive;font-size:1rem;
  color:rgba(255,255,255,.6);cursor:pointer;letter-spacing:2px;
  transition:all .2s;
}
.guest-btn:hover{border-color:rgba(255,255,255,.35);color:white}

/* Profile badge in topbar */
#profileBadge{
  display:flex;align-items:center;gap:7px;
  background:rgba(255,255,255,.08);border-radius:20px;
  padding:4px 12px 4px 4px;cursor:pointer;
  border:1px solid rgba(255,215,0,.15);
  transition:all .2s;
}
#profileBadge:hover{background:rgba(255,255,255,.13);border-color:rgba(255,215,0,.3)}
#profileBadge .pav{font-size:1.3rem;width:28px;height:28px;border-radius:50%;background:rgba(255,255,255,.1);display:flex;align-items:center;justify-content:center}
#profileBadge .pname-txt{font-size:.75rem;font-weight:800;color:rgba(255,255,255,.8);max-width:70px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}

/* Strength meter */
.strength-bar{height:4px;border-radius:4px;background:rgba(255,255,255,.1);margin-top:6px;overflow:hidden}
.strength-fill{height:100%;border-radius:4px;transition:all .3s;width:0%}

/* ═══════════ GOOGLE ADSENSE AD SLOTS ═══════════ */

/* Top banner ad (below topbar) */
#adTop{
  width:100%;
  background:rgba(0,0,0,.3);
  border-bottom:1px solid rgba(255,215,0,.08);
  display:flex;align-items:center;justify-content:center;
  flex-shrink:0;overflow:hidden;
  min-height:50px;
  position:relative;
}
#adTop .ad-label{
  position:absolute;top:2px;left:6px;
  font-size:.5rem;color:rgba(255,255,255,.2);
  letter-spacing:1px;pointer-events:none;
}

/* Bottom banner ad (above botbar) */
#adBottom{
  width:100%;
  background:rgba(0,0,0,.3);
  border-top:1px solid rgba(255,215,0,.08);
  border-bottom:1px solid rgba(255,215,0,.08);
  display:flex;align-items:center;justify-content:center;
  flex-shrink:0;overflow:hidden;
  min-height:50px;
  position:relative;
}
#adBottom .ad-label{
  position:absolute;top:2px;left:6px;
  font-size:.5rem;color:rgba(255,255,255,.2);
  letter-spacing:1px;pointer-events:none;
}

/* Interstitial ad overlay (shown between games) */
#adInterstitial{
  position:fixed;inset:0;z-index:800;
  background:rgba(0,0,0,.95);
  display:none;flex-direction:column;
  align-items:center;justify-content:center;
  gap:16px;padding:20px;
}
#adInterstitial .ad-skip-bar{
  width:100%;max-width:400px;
  display:flex;align-items:center;justify-content:space-between;
}
#adInterstitial .ad-skip-txt{
  font-size:.8rem;color:rgba(255,255,255,.5);letter-spacing:1px;
}
#adInterstitial .ad-skip-btn{
  padding:8px 20px;border:1px solid rgba(255,255,255,.3);
  border-radius:10px;background:rgba(255,255,255,.1);
  color:white;font-family:'Fredoka One',cursive;font-size:.85rem;
  cursor:pointer;letter-spacing:1px;transition:all .2s;
}
#adInterstitial .ad-skip-btn:hover{background:rgba(255,255,255,.2)}
#adInterstitial .ad-skip-btn:disabled{opacity:.4;cursor:not-allowed}
#adInterstitial .ad-box{
  width:100%;max-width:400px;
  background:rgba(255,255,255,.04);
  border:1px solid rgba(255,255,255,.1);
  border-radius:16px;overflow:hidden;
  min-height:260px;display:flex;align-items:center;justify-content:center;
}
#adInterstitial .ad-countdown{
  font-family:'Fredoka One',cursive;font-size:1rem;
  color:rgba(255,255,255,.6);letter-spacing:2px;
}

/* ═══════════ SETUP SCREEN ═══════════ */
#setup{
  position:fixed;inset:0;z-index:500;
  background:linear-gradient(135deg,#0d0220 0%,#1a0535 50%,#0d0220 100%);
  display:flex;flex-direction:column;align-items:center;justify-content:center;
  padding:20px;
}
.setup-bg{
  position:absolute;inset:0;overflow:hidden;pointer-events:none;
}
.setup-bg .bubble{
  position:absolute;border-radius:50%;
  background:radial-gradient(circle,rgba(255,215,0,.15),rgba(255,100,0,.05));
  animation:float 6s ease-in-out infinite;
}
@keyframes float{0%,100%{transform:translateY(0) scale(1)}50%{transform:translateY(-20px) scale(1.05)}}

.logo-wrap{text-align:center;margin-bottom:30px}
.logo{
  font-family:'Fredoka One',cursive;
  font-size:clamp(2.8rem,10vw,4.5rem);
  background:linear-gradient(135deg,#ff4400,#ffcc00,#00ff88,#0088ff);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
  letter-spacing:4px;line-height:1;
  filter:drop-shadow(0 0 30px rgba(255,180,0,.7));
  animation:logoPulse 2s ease-in-out infinite;
}
@keyframes logoPulse{0%,100%{filter:drop-shadow(0 0 20px rgba(255,180,0,.5))}50%{filter:drop-shadow(0 0 40px rgba(255,180,0,.9))}}
.logo-sub{color:rgba(255,255,255,.5);font-size:.9rem;letter-spacing:5px;margin-top:4px}

.setup-card{
  background:rgba(255,255,255,.05);
  border:1px solid rgba(255,215,0,.25);
  border-radius:24px;padding:28px 24px;
  width:100%;max-width:380px;
  backdrop-filter:blur(20px);
  box-shadow:0 0 60px rgba(255,140,0,.12),0 30px 60px rgba(0,0,0,.5);
}
.sc-label{
  color:rgba(255,255,255,.7);font-size:.8rem;
  letter-spacing:3px;text-transform:uppercase;
  margin-bottom:14px;font-weight:800;text-align:center;
}
.pbtns{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;margin-bottom:22px}
.pbtn{
  aspect-ratio:1;border-radius:14px;
  border:2px solid rgba(255,215,0,.2);
  background:rgba(255,255,255,.06);
  color:white;cursor:pointer;transition:all .22s;
  display:flex;flex-direction:column;align-items:center;justify-content:center;gap:4px;
  font-family:'Fredoka One',cursive;
}
.pbtn .num{font-size:1.8rem;line-height:1}
.pbtn .lbl{font-size:.55rem;opacity:.5;letter-spacing:1px;font-family:'Nunito',sans-serif;font-weight:800}
.pbtn:active,.pbtn.sel{
  border-color:var(--gold);
  background:rgba(255,215,0,.18);
  box-shadow:0 0 20px rgba(255,215,0,.35);
  transform:scale(1.06);
}
.players-preview{
  display:flex;flex-direction:column;gap:7px;margin-bottom:22px;
}
.pp-row{
  display:flex;align-items:center;gap:10px;
  background:rgba(255,255,255,.04);
  border-radius:10px;padding:8px 14px;
  border:1px solid rgba(255,255,255,.06);
}
.pp-dot{width:14px;height:14px;border-radius:50%;flex-shrink:0}
.pp-name{font-weight:800;font-size:.82rem;flex:1}
.pp-type{
  font-size:.62rem;padding:3px 10px;border-radius:8px;
  font-weight:800;letter-spacing:1px;
}
.pp-type.human{background:rgba(0,200,80,.2);color:#00ff88}
.pp-type.bot{background:rgba(255,140,0,.18);color:#ffaa44}
.startbtn{
  width:100%;padding:16px;border:none;border-radius:16px;
  background:linear-gradient(135deg,#ffe566,#ff6600);
  font-family:'Fredoka One',cursive;font-size:1.4rem;
  color:#1a0800;cursor:pointer;letter-spacing:3px;
  box-shadow:0 6px 24px rgba(255,100,0,.45);
  transition:all .2s;
}
.startbtn:active{transform:scale(.96)}

/* ═══════════ GAME SCREEN ═══════════ */
#game{
  display:none;
  position:fixed;inset:0;
  flex-direction:column;
  background:linear-gradient(180deg,#0a0118 0%,#120230 100%);
}

/* Top bar */
#topbar{
  display:flex;align-items:center;justify-content:space-between;
  padding:8px 12px;
  background:rgba(0,0,0,.4);
  border-bottom:1px solid rgba(255,215,0,.1);
  flex-shrink:0;
  height:52px;
}
#topbar .gtitle{
  font-family:'Fredoka One',cursive;
  font-size:1.3rem;
  background:linear-gradient(135deg,#ffe566,#ff6600);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
  letter-spacing:4px;
}
#topbar .tbbtns{display:flex;gap:8px}
.tbbtn{
  background:rgba(255,255,255,.08);
  border:1px solid rgba(255,255,255,.12);
  border-radius:8px;padding:5px 10px;
  color:rgba(255,255,255,.7);font-size:.7rem;
  cursor:pointer;font-weight:800;letter-spacing:1px;
  font-family:'Nunito',sans-serif;
}
.tbbtn:active{background:rgba(255,255,255,.15)}

/* Board area - takes all available space */
#board-area{
  flex:1;display:flex;align-items:center;justify-content:center;
  padding:4px;min-height:0;
  position:relative;
}

canvas#ludo{
  display:block;
  border-radius:12px;
  box-shadow:
    0 0 0 3px rgba(255,215,0,.3),
    0 0 40px rgba(255,120,0,.25),
    0 20px 60px rgba(0,0,0,.6);
  cursor:pointer;
  touch-action:none;
}

/* Bottom bar */
#botbar{
  flex-shrink:0;
  background:rgba(0,0,0,.5);
  border-top:1px solid rgba(255,215,0,.1);
  padding:8px 10px;
  display:flex;flex-direction:column;align-items:center;gap:6px;
}

/* Player cards strip */
#pcards{
  display:flex;gap:6px;width:100%;justify-content:center;
}
.pcard{
  flex:1;max-width:90px;
  border-radius:10px;padding:6px 8px;
  border:2px solid;opacity:.4;
  transition:all .25s;
  position:relative;overflow:hidden;
}
.pcard.active{
  opacity:1;
  box-shadow:0 0 14px currentColor;
  transform:translateY(-2px);
}
.pcard .pn{font-family:'Fredoka One',cursive;font-size:.78rem;letter-spacing:1px}
.pcard .pb{
  font-size:.52rem;padding:1px 5px;border-radius:5px;
  border:1px solid currentColor;opacity:.6;
  letter-spacing:1px;font-weight:800;display:inline-block;margin-top:1px;
}
.pcard .pdots{display:flex;gap:3px;margin-top:5px;flex-wrap:wrap}
.pdot{
  width:10px;height:10px;border-radius:50%;
  border:1.5px solid rgba(255,255,255,.2);transition:all .3s;
}
.pdot.home{opacity:.22}
.pdot.board{opacity:1;box-shadow:0 0 6px currentColor}
.pdot.won{background:var(--gold)!important;border-color:var(--gold);box-shadow:0 0 8px var(--gold)}

/* Dice + message */
#dice-row{
  display:flex;align-items:center;gap:14px;width:100%;justify-content:center;
}
#diceWrap{
  position:relative;cursor:pointer;flex-shrink:0;
  width:64px;height:64px;
}
#diceWrap:active{transform:scale(.9)}
#diceCanvas{
  display:block;border-radius:14px;
  transition:transform .1s;
}
#diceWrap .diceShake{
  animation:diceShake .08s linear infinite;
}
@keyframes diceShake{
  0%{transform:rotate(-8deg) scale(1.05)}
  50%{transform:rotate(8deg) scale(1.08)}
  100%{transform:rotate(-8deg) scale(1.05)}
}
#rollbtn{
  flex:1;max-width:180px;padding:13px 10px;
  background:linear-gradient(135deg,#ffe566,#ff6600);
  border:none;border-radius:14px;
  font-family:'Fredoka One',cursive;font-size:1.1rem;
  color:#1a0800;cursor:pointer;letter-spacing:2px;
  box-shadow:0 4px 18px rgba(255,100,0,.45);transition:all .15s;
}
#rollbtn:active:not(:disabled){transform:scale(.93)}
#rollbtn:disabled{opacity:.32;cursor:not-allowed}

#msgbox{
  font-size:.75rem;color:#c0b0e0;letter-spacing:.5px;
  text-align:center;min-height:18px;
  padding:0 10px;
}

/* ═══════════ TOAST / POPUP ═══════════ */
#toast{
  position:fixed;top:60px;left:50%;transform:translateX(-50%);
  background:rgba(0,0,0,.85);border:1px solid rgba(255,215,0,.3);
  border-radius:12px;padding:10px 22px;
  font-family:'Fredoka One',cursive;font-size:1rem;
  color:white;letter-spacing:2px;
  pointer-events:none;opacity:0;
  transition:opacity .3s;z-index:200;
  text-align:center;white-space:nowrap;
}
#toast.show{opacity:1}

/* ═══════════ WINNER SCREEN ═══════════ */
#winscreen{
  position:fixed;inset:0;z-index:600;
  display:none;align-items:center;justify-content:center;
  background:rgba(0,0,0,.92);backdrop-filter:blur(12px);
}
.winbox{
  text-align:center;
  animation:winPop .7s cubic-bezier(.175,.885,.32,1.275);
}
@keyframes winPop{from{transform:scale(.2);opacity:0}to{transform:scale(1);opacity:1}}
.win-trophy{font-size:5rem;margin-bottom:10px;display:block;animation:trophySpin 2s linear infinite}
@keyframes trophySpin{0%{transform:rotateY(0)}100%{transform:rotateY(360deg)}}
.win-name{
  font-family:'Fredoka One',cursive;font-size:clamp(2rem,8vw,3.5rem);
  margin-bottom:6px;
  text-shadow:0 0 30px currentColor;
}
.win-sub{color:rgba(255,255,255,.6);letter-spacing:4px;font-size:.85rem;margin-bottom:28px}
.win-confetti{font-size:1.8rem;margin-bottom:20px;animation:confSpin 1s linear infinite}
@keyframes confSpin{to{transform:rotate(360deg)}}
.win-btns{display:flex;gap:12px;justify-content:center;flex-wrap:wrap}
.win-btn{
  padding:14px 30px;border:none;border-radius:14px;
  font-family:'Fredoka One',cursive;font-size:1rem;
  cursor:pointer;letter-spacing:2px;
}
.win-btn.primary{background:linear-gradient(135deg,#ffe566,#ff6600);color:#1a0800}
.win-btn.secondary{background:rgba(255,255,255,.1);color:white;border:1px solid rgba(255,255,255,.2)}

/* Particles */
#particles{position:fixed;inset:0;pointer-events:none;z-index:150;overflow:hidden}
.particle{
  position:absolute;border-radius:50%;
  animation:particleFly 1.2s ease-out forwards;
  pointer-events:none;
}
@keyframes particleFly{
  0%{transform:translate(0,0) scale(1);opacity:1}
  100%{transform:translate(var(--tx),var(--ty)) scale(0);opacity:0}
}

/* Sound wave animation */
.soundwave{
  position:fixed;top:50%;left:50%;
  transform:translate(-50%,-50%);
  border-radius:50%;border:3px solid rgba(255,215,0,.6);
  animation:wave .6s ease-out forwards;
  pointer-events:none;z-index:100;
}
@keyframes wave{
  0%{width:20px;height:20px;opacity:1;margin-left:-10px;margin-top:-10px}
  100%{width:200px;height:200px;opacity:0;margin-left:-100px;margin-top:-100px}
}
</style>
</head>
<body>

<!-- ═══ AUTH SCREEN ═══ -->
<div id="authScreen">
  <div class="auth-bg" id="authBg"></div>

  <div class="auth-logo">
    <div class="logo-txt">LUDO STAR</div>
    <div class="logo-tag">✦ 3D CLASSIC ✦</div>
  </div>

  <div class="auth-card">
    <!-- Tabs -->
    <div class="auth-tabs">
      <button class="auth-tab active" id="tabLogin" onclick="switchTab('login')">LOGIN</button>
      <button class="auth-tab" id="tabSignup" onclick="switchTab('signup')">SIGN UP</button>
    </div>

    <!-- Error / OK -->
    <div class="auth-err" id="authErr"></div>
    <div class="auth-ok"  id="authOk"></div>

    <!-- LOGIN FORM -->
    <div id="loginForm">
      <div class="auth-field">
        <label>Username or Email</label>
        <span class="ficon">👤</span>
        <input type="text" id="loginUser" placeholder="Enter username or email" autocomplete="username"/>
      </div>
      <div class="auth-field">
        <label>Password</label>
        <span class="ficon">🔒</span>
        <input type="password" id="loginPass" placeholder="Enter password" autocomplete="current-password"/>
        <button class="eye-toggle" onclick="toggleEye('loginPass',this)">👁</button>
      </div>
      <button class="auth-submit" onclick="doLogin()">LOGIN  →</button>
    </div>

    <!-- SIGNUP FORM -->
    <div id="signupForm" style="display:none">
      <div class="avatar-row" id="avatarRow"></div>
      <div class="auth-field">
        <label>Username</label>
        <span class="ficon">🎮</span>
        <input type="text" id="regUser" placeholder="Choose a username" maxlength="18" autocomplete="username"/>
      </div>
      <div class="auth-field">
        <label>Email</label>
        <span class="ficon">📧</span>
        <input type="email" id="regEmail" placeholder="your@email.com" autocomplete="email"/>
      </div>
      <div class="auth-field">
        <label>Password</label>
        <span class="ficon">🔒</span>
        <input type="password" id="regPass" placeholder="Min 6 characters" autocomplete="new-password" oninput="checkStrength(this.value)"/>
        <button class="eye-toggle" onclick="toggleEye('regPass',this)">👁</button>
        <div class="strength-bar"><div class="strength-fill" id="strengthFill"></div></div>
      </div>
      <div class="auth-field">
        <label>Confirm Password</label>
        <span class="ficon">✅</span>
        <input type="password" id="regPass2" placeholder="Repeat password" autocomplete="new-password"/>
        <button class="eye-toggle" onclick="toggleEye('regPass2',this)">👁</button>
      </div>
      <button class="auth-submit" onclick="doSignup()">CREATE ACCOUNT  →</button>
    </div>

    <div class="auth-divider"><span>OR</span></div>
    <button class="guest-btn" onclick="guestLogin()">🎲  Play as Guest</button>
  </div>
</div>

<!-- ═══ SETUP ═══ -->
<div id="setup" style="display:none">
  <div class="setup-bg" id="setupBg"></div>
  <div class="logo-wrap">
    <div class="logo">LUDO STAR</div>
    <div class="logo-sub">✦ 3D CLASSIC ✦</div>
  </div>
  <div class="setup-card">
    <div class="sc-label">👥 How many human players?</div>
    <div class="pbtns">
      <button class="pbtn" data-n="1" onclick="selP(1)"><div class="num">1</div><div class="lbl">SOLO</div></button>
      <button class="pbtn" data-n="2" onclick="selP(2)"><div class="num">2</div><div class="lbl">DUO</div></button>
      <button class="pbtn" data-n="3" onclick="selP(3)"><div class="num">3</div><div class="lbl">TRIO</div></button>
      <button class="pbtn sel" data-n="4" onclick="selP(4)"><div class="num">4</div><div class="lbl">FULL</div></button>
    </div>
    <div class="players-preview" id="pprev"></div>
    <button class="startbtn" onclick="startGame()">▶  START GAME</button>
  </div>
</div>

<!-- ═══ GAME ═══ -->
<div id="game">
  <!-- Top bar -->
  <div id="topbar">
    <div id="profileBadge" onclick="showProfile()">
      <div class="pav" id="topAvatar">🎮</div>
      <div class="pname-txt" id="topName">Player</div>
    </div>
    <div class="tbbtns">
      <div class="tbbtn" onclick="toggleSound()">🔊 <span id="soundlbl">ON</span></div>
      <div class="tbbtn" onclick="goSetup()">⚙ MENU</div>
      <div class="tbbtn" onclick="doLogout()">🚪 LOGOUT</div>
    </div>
  </div>

  <!-- Top banner ad -->
  <div id="adTop">
    <span class="ad-label">ADVERTISEMENT</span>
    <!-- STEP 2: Replace data-ad-slot value with YOUR Ad Slot ID from AdSense dashboard -->
    <ins class="adsbygoogle"
         style="display:inline-block;width:320px;height:50px"
         data-ad-client="ca-pub-XXXXXXXXXXXXXXXXX"
         data-ad-slot="XXXXXXXXXX"></ins>
  </div>

  <!-- Board -->
  <div id="board-area">
    <canvas id="ludo"></canvas>
  </div>

  <!-- Bottom banner ad -->
  <div id="adBottom">
    <span class="ad-label">ADVERTISEMENT</span>
    <!-- STEP 3: Replace with YOUR Ad Slot ID (can be same or different slot) -->
    <ins class="adsbygoogle"
         style="display:inline-block;width:320px;height:50px"
         data-ad-client="ca-pub-XXXXXXXXXXXXXXXXX"
         data-ad-slot="XXXXXXXXXX"></ins>
  </div>

  <!-- Bottom bar -->
  <div id="botbar">
    <div id="pcards">
      <div class="pcard" id="pc0" style="color:var(--red);border-color:var(--red)">
        <div class="pn">🔴 RED</div>
        <div class="pb" id="b0">BOT</div>
        <div class="pdots" id="pd0"></div>
      </div>
      <div class="pcard" id="pc1" style="color:var(--green);border-color:var(--green)">
        <div class="pn">🟢 GRN</div>
        <div class="pb" id="b1">BOT</div>
        <div class="pdots" id="pd1"></div>
      </div>
      <div class="pcard" id="pc2" style="color:var(--yellow);border-color:var(--yellow)">
        <div class="pn">🟡 YLW</div>
        <div class="pb" id="b2">BOT</div>
        <div class="pdots" id="pd2"></div>
      </div>
      <div class="pcard" id="pc3" style="color:var(--blue);border-color:var(--blue)">
        <div class="pn">🔵 BLU</div>
        <div class="pb" id="b3">BOT</div>
        <div class="pdots" id="pd3"></div>
      </div>
    </div>
    <div id="dice-row">
      <div id="diceWrap" onclick="rollDice()">
        <canvas id="diceCanvas" width="64" height="64"></canvas>
      </div>
      <button id="rollbtn" onclick="rollDice()">ROLL DICE</button>
    </div>
    <div id="msgbox">Tap ROLL DICE to start!</div>
  </div>
</div>

<!-- Toast -->
<div id="toast"></div>
<!-- Particles -->
<div id="particles"></div>

<!-- Winner -->
<div id="winscreen">
  <div class="winbox">
    <span class="win-trophy">🏆</span>
    <div class="win-confetti">🎊🎉🎊</div>
    <div class="win-name" id="wname"></div>
    <div class="win-sub">WINS THE GAME!</div>
    <div class="win-btns">
      <button class="win-btn primary" onclick="playAgainAd()">🔄 PLAY AGAIN</button>
      <button class="win-btn secondary" onclick="goSetup()">⚙ MENU</button>
    </div>
  </div>
</div>

<script>
// ════════════════════════════════════════════════════
//   AUTH SYSTEM — Login / Signup / Guest / LocalStorage
// ════════════════════════════════════════════════════

const AVATARS = ['🎮','🦁','🐯','🦊','🐺','🦅','👑','🌟','🔥','⚡','🎯','🏆'];
let pickedAvatar = '🎮';
let currentUser = null; // { username, email, avatar, isGuest }

// ── Build avatar picker ──
function buildAvatarRow(){
  const row = document.getElementById('avatarRow');
  row.innerHTML = AVATARS.map((a,i)=>
    `<button class="av-btn${i===0?' picked':''}" onclick="pickAvatar(this,'${a}')">${a}</button>`
  ).join('');
}
buildAvatarRow();

// Build auth background orbs
(function(){
  const bg = document.getElementById('authBg');
  const orbs = [
    {color:'rgba(255,80,0,.18)',size:300,x:'-10%',y:'-10%',delay:0},
    {color:'rgba(0,150,255,.14)',size:250,x:'70%',y:'60%',delay:2},
    {color:'rgba(255,215,0,.1)',size:200,x:'40%',y:'80%',delay:4},
    {color:'rgba(100,0,255,.12)',size:280,x:'80%',y:'-5%',delay:1},
  ];
  orbs.forEach(o=>{
    const el=document.createElement('div');
    el.className='orb';
    el.style.cssText=`width:${o.size}px;height:${o.size}px;left:${o.x};top:${o.y};background:${o.color};animation-delay:${o.delay}s`;
    bg.appendChild(el);
  });
})();

// ── Tab switch ──
function switchTab(tab){
  const isLogin = tab==='login';
  document.getElementById('tabLogin').classList.toggle('active', isLogin);
  document.getElementById('tabSignup').classList.toggle('active', !isLogin);
  document.getElementById('loginForm').style.display  = isLogin?'block':'none';
  document.getElementById('signupForm').style.display = isLogin?'none':'block';
  clearAuthMsg();
}

function clearAuthMsg(){
  document.getElementById('authErr').classList.remove('show');
  document.getElementById('authOk').classList.remove('show');
}
function showAuthErr(msg){
  const e=document.getElementById('authErr');
  e.textContent='⚠️  '+msg; e.classList.add('show');
  document.getElementById('authOk').classList.remove('show');
}
function showAuthOk(msg){
  const o=document.getElementById('authOk');
  o.textContent='✅  '+msg; o.classList.add('show');
  document.getElementById('authErr').classList.remove('show');
}

// ── Password eye toggle ──
function toggleEye(inputId, btn){
  const inp = document.getElementById(inputId);
  const show = inp.type==='password';
  inp.type = show?'text':'password';
  btn.textContent = show?'🙈':'👁';
}

// ── Avatar pick ──
function pickAvatar(btn, av){
  document.querySelectorAll('.av-btn').forEach(b=>b.classList.remove('picked'));
  btn.classList.add('picked');
  pickedAvatar = av;
}

// ── Password strength ──
function checkStrength(val){
  const fill = document.getElementById('strengthFill');
  let score = 0;
  if(val.length>=6) score++;
  if(val.length>=10) score++;
  if(/[A-Z]/.test(val)) score++;
  if(/[0-9]/.test(val)) score++;
  if(/[^A-Za-z0-9]/.test(val)) score++;
  const colors = ['#ff2244','#ff6600','#ffcc00','#88cc00','#00cc55'];
  const widths  = ['20%','40%','60%','80%','100%'];
  fill.style.background = colors[score-1]||'transparent';
  fill.style.width = widths[score-1]||'0%';
}

// ── LocalStorage helpers ──
function getUsers(){ try{return JSON.parse(localStorage.getItem('ludoUsers')||'{}');}catch{return{};} }
function saveUsers(u){ localStorage.setItem('ludoUsers',JSON.stringify(u)); }
function saveSession(user){ localStorage.setItem('ludoSession',JSON.stringify(user)); }
function loadSession(){ try{return JSON.parse(localStorage.getItem('ludoSession'));}catch{return null;} }
function clearSession(){ localStorage.removeItem('ludoSession'); }

// ── SIGNUP ──
function doSignup(){
  clearAuthMsg();
  const uname = document.getElementById('regUser').value.trim();
  const email  = document.getElementById('regEmail').value.trim();
  const pass   = document.getElementById('regPass').value;
  const pass2  = document.getElementById('regPass2').value;

  if(!uname)            return showAuthErr('Username is required!');
  if(uname.length < 3)  return showAuthErr('Username must be at least 3 characters.');
  if(!/^[a-zA-Z0-9_]+$/.test(uname)) return showAuthErr('Username: only letters, numbers, _ allowed.');
  if(!email || !email.includes('@')) return showAuthErr('Please enter a valid email.');
  if(pass.length < 6)   return showAuthErr('Password must be at least 6 characters.');
  if(pass !== pass2)    return showAuthErr('Passwords do not match!');

  const users = getUsers();
  if(users[uname.toLowerCase()]) return showAuthErr('Username already taken! Try another.');
  if(Object.values(users).some(u=>u.email===email)) return showAuthErr('Email already registered!');

  // Save user
  users[uname.toLowerCase()] = {
    username: uname,
    email, avatar: pickedAvatar,
    password: btoa(pass), // basic obfuscation
    createdAt: Date.now(),
    gamesPlayed:0, wins:0,
  };
  saveUsers(users);

  showAuthOk(`Account created! Welcome, ${uname}! 🎉`);
  const btn = document.querySelector('#signupForm .auth-submit');
  btn.disabled=true;
  setTimeout(()=>{
    btn.disabled=false;
    enterGame({ username:uname, email, avatar:pickedAvatar, isGuest:false });
  }, 1200);
}

// ── LOGIN ──
function doLogin(){
  clearAuthMsg();
  const input = document.getElementById('loginUser').value.trim();
  const pass  = document.getElementById('loginPass').value;

  if(!input) return showAuthErr('Please enter username or email!');
  if(!pass)  return showAuthErr('Please enter your password!');

  const users = getUsers();
  // Find by username or email
  let found = users[input.toLowerCase()];
  if(!found) found = Object.values(users).find(u=>u.email===input);

  if(!found)              return showAuthErr('Account not found! Please sign up.');
  if(atob(found.password)!==pass) return showAuthErr('Wrong password! Try again.');

  showAuthOk(`Welcome back, ${found.username}! 🎮`);
  setTimeout(()=>{
    enterGame({ username:found.username, email:found.email, avatar:found.avatar, isGuest:false });
  }, 800);
}

// ── GUEST ──
function guestLogin(){
  clearAuthMsg();
  const guestName = 'Guest_' + Math.floor(Math.random()*9000+1000);
  enterGame({ username:guestName, avatar:'🎲', isGuest:true });
}

function playAgainAd(){
  document.getElementById('winscreen').style.display='none';
  showInterstitialAd(()=>{
    // After ad: go back to setup
    document.getElementById('game').style.display='none';
    document.getElementById('setup').style.display='flex';
  });
}

// ── Enter game after auth ──
function enterGame(user){
  currentUser = user;
  if(!user.isGuest) saveSession(user);

  // Update topbar profile
  document.getElementById('topAvatar').textContent = user.avatar;
  document.getElementById('topName').textContent   = user.username;

  // Hide auth, show setup
  document.getElementById('authScreen').style.display='none';
  document.getElementById('setup').style.display='flex';

  // Initialize AdSense banner slots
  setTimeout(initAds, 500);
}

// ── Logout ──
function doLogout(){
  if(!confirm('Logout and return to login?')) return;
  clearSession();
  currentUser=null;
  document.getElementById('game').style.display='none';
  document.getElementById('setup').style.display='none';
  document.getElementById('authScreen').style.display='flex';
  clearAuthMsg();
  document.getElementById('loginUser').value='';
  document.getElementById('loginPass').value='';
  switchTab('login');
}

// ── Profile popup ──
function showProfile(){
  if(!currentUser) return;
  const u=currentUser;
  alert(`${u.avatar} ${u.username}\n${u.isGuest?'🎲 Guest Account':'📧 '+u.email}\n\nEnjoy the game!`);
}

// ── Auto-login on page load ──
(function checkAutoLogin(){
  const sess = loadSession();
  if(sess && sess.username){
    currentUser = sess;
    document.getElementById('topAvatar').textContent = sess.avatar||'🎮';
    document.getElementById('topName').textContent   = sess.username;
    document.getElementById('authScreen').style.display='none';
    document.getElementById('setup').style.display='flex';
  }
})();

// ════════════════════════════════════════════════════
//   Yalla Ludo style: sounds, animations, AI bots,
//   click home pieces, full screen mobile
// ════════════════════════════════════════════════════

// ════════════════════════════════════════════════════
//   GOOGLE ADSENSE — Ad Management
// ════════════════════════════════════════════════════

let adSkipTimer = null;
let afterAdCallback = null;

function initAds(){
  try{
    document.querySelectorAll('.adsbygoogle[data-ad-slot]').forEach(()=>{
      (window.adsbygoogle = window.adsbygoogle || []).push({});
    });
  }catch(e){}
}

function showInterstitialAd(callback){
  afterAdCallback = callback;
  const overlay = document.getElementById('adInterstitial');
  const skipBtn  = document.getElementById('adSkipBtn');
  const timerEl  = document.getElementById('adTimer');
  const msgEl    = document.getElementById('adMsg');
  overlay.style.display='flex';
  skipBtn.disabled=true;
  skipBtn.textContent='SKIP ▶';
  let secs=5; timerEl.textContent=secs;
  msgEl.textContent='Loading next game...';
  try{ (window.adsbygoogle=window.adsbygoogle||[]).push({}); }catch(e){}
  clearInterval(adSkipTimer);
  adSkipTimer=setInterval(()=>{
    secs--; timerEl.textContent=secs;
    if(secs<=0){
      clearInterval(adSkipTimer);
      skipBtn.disabled=false;
      skipBtn.textContent='SKIP ▶▶';
      msgEl.textContent='You can skip now!';
    }
  },1000);
}

function skipAd(){
  clearInterval(adSkipTimer);
  document.getElementById('adInterstitial').style.display='none';
  if(afterAdCallback){ afterAdCallback(); afterAdCallback=null; }
}

// ── Audio Engine (Web Audio API) ──────────────────
let AudioCtx;
let soundOn = true;

function initAudio(){
  try{ AudioCtx = new (window.AudioContext||window.webkitAudioContext)(); }catch(e){}
}

function playSound(type){
  if(!soundOn || !AudioCtx) return;
  try{
    const ctx = AudioCtx;
    if(ctx.state==='suspended') ctx.resume();
    const g = ctx.createGain();
    g.connect(ctx.destination);

    switch(type){
      case 'dice':{
        // Rolling click sound
        for(let i=0;i<6;i++){
          const o=ctx.createOscillator();
          const gi=ctx.createGain();
          o.connect(gi);gi.connect(ctx.destination);
          o.frequency.setValueAtTime(200+Math.random()*300, ctx.currentTime+i*.05);
          gi.gain.setValueAtTime(.15, ctx.currentTime+i*.05);
          gi.gain.exponentialRampToValueAtTime(.001, ctx.currentTime+i*.05+.08);
          o.start(ctx.currentTime+i*.05);
          o.stop(ctx.currentTime+i*.05+.08);
        }
        break;
      }
      case 'move':{
        const o=ctx.createOscillator();o.type='sine';
        o.frequency.setValueAtTime(440,ctx.currentTime);
        o.frequency.exponentialRampToValueAtTime(660,ctx.currentTime+.1);
        g.gain.setValueAtTime(.2,ctx.currentTime);
        g.gain.exponentialRampToValueAtTime(.001,ctx.currentTime+.15);
        o.connect(g);o.start(ctx.currentTime);o.stop(ctx.currentTime+.15);
        break;
      }
      case 'capture':{
        [880,440,220].forEach((f,i)=>{
          const o=ctx.createOscillator();const gi=ctx.createGain();
          o.type='sawtooth';o.frequency.setValueAtTime(f,ctx.currentTime+i*.08);
          gi.gain.setValueAtTime(.2,ctx.currentTime+i*.08);
          gi.gain.exponentialRampToValueAtTime(.001,ctx.currentTime+i*.08+.12);
          o.connect(gi);gi.connect(ctx.destination);
          o.start(ctx.currentTime+i*.08);o.stop(ctx.currentTime+i*.08+.12);
        });
        break;
      }
      case 'home':{
        [523,659,784,1047].forEach((f,i)=>{
          const o=ctx.createOscillator();const gi=ctx.createGain();
          o.type='sine';o.frequency.setValueAtTime(f,ctx.currentTime+i*.1);
          gi.gain.setValueAtTime(.25,ctx.currentTime+i*.1);
          gi.gain.exponentialRampToValueAtTime(.001,ctx.currentTime+i*.1+.15);
          o.connect(gi);gi.connect(ctx.destination);
          o.start(ctx.currentTime+i*.1);o.stop(ctx.currentTime+i*.1+.2);
        });
        break;
      }
      case 'win':{
        const notes=[523,587,659,698,784,880,988,1047];
        notes.forEach((f,i)=>{
          const o=ctx.createOscillator();const gi=ctx.createGain();
          o.type='sine';o.frequency.setValueAtTime(f,ctx.currentTime+i*.12);
          gi.gain.setValueAtTime(.3,ctx.currentTime+i*.12);
          gi.gain.exponentialRampToValueAtTime(.001,ctx.currentTime+i*.12+.2);
          o.connect(gi);gi.connect(ctx.destination);
          o.start(ctx.currentTime+i*.12);o.stop(ctx.currentTime+i*.12+.25);
        });
        break;
      }
      case 'six':{
        [660,880,1100].forEach((f,i)=>{
          const o=ctx.createOscillator();const gi=ctx.createGain();
          o.type='triangle';o.frequency.setValueAtTime(f,ctx.currentTime+i*.07);
          gi.gain.setValueAtTime(.28,ctx.currentTime+i*.07);
          gi.gain.exponentialRampToValueAtTime(.001,ctx.currentTime+i*.07+.12);
          o.connect(gi);gi.connect(ctx.destination);
          o.start(ctx.currentTime+i*.07);o.stop(ctx.currentTime+i*.07+.15);
        });
        break;
      }
      case 'tick':{
        const o=ctx.createOscillator();const gi=ctx.createGain();
        o.frequency.value=800;gi.gain.setValueAtTime(.08,ctx.currentTime);
        gi.gain.exponentialRampToValueAtTime(.001,ctx.currentTime+.04);
        o.connect(gi);gi.connect(ctx.destination);
        o.start(ctx.currentTime);o.stop(ctx.currentTime+.04);
        break;
      }
    }
  }catch(e){}
}

function toggleSound(){
  soundOn=!soundOn;
  document.getElementById('soundlbl').textContent=soundOn?'ON':'OFF';
  showToast(soundOn?'🔊 Sound ON':'🔇 Sound OFF');
}

// ── Player Config ──────────────────────────────────
const PC=[
  {name:'Red',   full:'RED',   css:'#ff1a3a',dark:'#990020',light:'#ffc0cc',lighter:'#fff0f3',icon:'🔴',cssvar:'--red'},
  {name:'Green', full:'GREEN', css:'#00bb44',dark:'#006622',light:'#aaffcc',lighter:'#f0fff5',icon:'🟢',cssvar:'--green'},
  {name:'Yellow',full:'YELLOW',css:'#ffcc00',dark:'#997700',light:'#fff3a0',lighter:'#fffef0',icon:'🟡',cssvar:'--yellow'},
  {name:'Blue',  full:'BLUE',  css:'#1166ff',dark:'#003399',light:'#aaccff',lighter:'#f0f7ff',icon:'🔵',cssvar:'--blue'},
];
const DFACES=['⚀','⚁','⚂','⚃','⚄','⚅'];

// ── Board Path (52 cells) ──────────────────────────
function mkPath(){
  const p=[];
  for(let c=1;c<=5;c++)p.push([6,c]);
  for(let r=5;r>=1;r--)p.push([r,5]);
  p.push([0,5],[0,6],[0,7],[0,8]);
  for(let r=1;r<=5;r++)p.push([r,8]);
  for(let c=9;c<=13;c++)p.push([6,c]);
  p.push([7,13],[8,13],[9,13]);
  for(let c=12;c>=8;c--)p.push([9,c]);
  for(let r=10;r<=14;r++)p.push([r,8]);
  p.push([14,7],[14,6],[14,5]);
  for(let r=13;r>=9;r--)p.push([r,5]);
  for(let c=4;c>=0;c--)p.push([8,c]);
  p.push([7,0],[6,0]);
  return p;
}
const BPATH=mkPath();
const ENTRY=[0,13,26,39];
const HCOL=[
  [[6,7],[5,7],[4,7],[3,7],[2,7],[1,7]],
  [[7,8],[7,9],[7,10],[7,11],[7,12],[7,13]],
  [[8,7],[9,7],[10,7],[11,7],[12,7],[13,7]],
  [[7,6],[7,5],[7,4],[7,3],[7,2],[7,1]],
];
const HBASE=[
  [[1,1],[1,3],[3,1],[3,3]],
  [[1,11],[1,13],[3,11],[3,13]],
  [[11,11],[11,13],[13,11],[13,13]],
  [[11,1],[11,3],[13,1],[13,3]],
];
const SAFE=new Set(['6,1','0,8','9,13','14,5','1,6','6,2','2,8','8,12','13,6','8,2','6,12','12,8','6,0','0,6']);

// ── Canvas Dice Drawing ───────────────────────────
const diceCanvas = document.getElementById('diceCanvas');
const dctx = diceCanvas.getContext('2d');
let diceValue = 1;
let diceShaking = false;

// Dot positions for each face (normalized 0-1 on a 0.8 grid)
const DOT_POS = {
  1:[[.5,.5]],
  2:[[.25,.25],[.75,.75]],
  3:[[.25,.25],[.5,.5],[.75,.75]],
  4:[[.25,.25],[.75,.25],[.25,.75],[.75,.75]],
  5:[[.25,.25],[.75,.25],[.5,.5],[.25,.75],[.75,.75]],
  6:[[.25,.22],[.75,.22],[.25,.5],[.75,.5],[.25,.78],[.75,.78]],
};

function drawDice(val, playerColorCSS, isRolling){
  const dc = diceCanvas;
  const dx = dctx;
  const W = dc.width, H = dc.height;
  dx.clearRect(0,0,W,H);

  const pcolor = playerColorCSS || '#ffffff';

  // Outer glow (player color)
  dx.save();
  dx.shadowColor = pcolor;
  dx.shadowBlur = isRolling ? 22 : 14;

  // Dice body — white rounded rect with 3D gradient
  const pad = 4;
  const bodyGrad = dx.createLinearGradient(pad, pad, W-pad, H-pad);
  bodyGrad.addColorStop(0, '#ffffff');
  bodyGrad.addColorStop(0.45, '#f5f5f5');
  bodyGrad.addColorStop(1, '#d8d8d8');
  dx.fillStyle = bodyGrad;
  diceRR(dx, pad, pad, W-pad*2, H-pad*2, 14);
  dx.fill();

  // Colored border (player color)
  dx.strokeStyle = pcolor;
  dx.lineWidth = isRolling ? 3.5 : 2.5;
  diceRR(dx, pad, pad, W-pad*2, H-pad*2, 14);
  dx.stroke();
  dx.restore();

  // Top-left shine
  const shineGrad = dx.createLinearGradient(pad+2, pad+2, pad+20, pad+20);
  shineGrad.addColorStop(0, 'rgba(255,255,255,0.85)');
  shineGrad.addColorStop(1, 'rgba(255,255,255,0)');
  dx.fillStyle = shineGrad;
  diceRR(dx, pad+2, pad+2, (W-pad*2)*.55, (H-pad*2)*.55, 10);
  dx.fill();

  // Dots (colored = player color)
  const dotR = W * 0.08;
  const margin = W * 0.18;
  const area = W - margin*2;
  const dots = DOT_POS[val] || DOT_POS[1];

  dots.forEach(([nx,ny])=>{
    const cx = margin + nx * area;
    const cy = margin + ny * area;

    // Dot shadow
    dx.beginPath();
    dx.arc(cx+1, cy+1.5, dotR, 0, Math.PI*2);
    dx.fillStyle = 'rgba(0,0,0,0.2)';
    dx.fill();

    // Dot body — colored gradient
    const dg = dx.createRadialGradient(cx-dotR*.3, cy-dotR*.3, 1, cx, cy, dotR);
    dg.addColorStop(0, lightenColor(pcolor, 0.4));
    dg.addColorStop(0.6, pcolor);
    dg.addColorStop(1, darkenColor(pcolor, 0.3));
    dx.beginPath();
    dx.arc(cx, cy, dotR, 0, Math.PI*2);
    dx.fillStyle = dg;
    dx.fill();

    // Dot highlight
    dx.beginPath();
    dx.arc(cx - dotR*.3, cy - dotR*.3, dotR*.3, 0, Math.PI*2);
    dx.fillStyle = 'rgba(255,255,255,0.55)';
    dx.fill();
  });

  // If rolling: show "?" overlay
  if(isRolling){
    dx.fillStyle = 'rgba(255,255,255,0.15)';
    diceRR(dx, pad, pad, W-pad*2, H-pad*2, 14);
    dx.fill();
  }

  // Bottom-right shadow edge
  dx.save();
  dx.globalAlpha = 0.15;
  dx.fillStyle = '#000';
  diceRR(dx, pad+2, pad+2, W-pad*2, H-pad*2, 14);
  dx.fill();
  dx.restore();
}

function diceRR(dx, x, y, w, h, r){
  dx.beginPath();
  dx.moveTo(x+r, y);
  dx.lineTo(x+w-r, y);
  dx.quadraticCurveTo(x+w, y, x+w, y+r);
  dx.lineTo(x+w, y+h-r);
  dx.quadraticCurveTo(x+w, y+h, x+w-r, y+h);
  dx.lineTo(x+r, y+h);
  dx.quadraticCurveTo(x, y+h, x, y+h-r);
  dx.lineTo(x, y+r);
  dx.quadraticCurveTo(x, y, x+r, y);
  dx.closePath();
}

function lightenColor(hex, amt){
  let [r,g,b] = h2r(hex);
  r = Math.min(255, r + Math.round(255*amt));
  g = Math.min(255, g + Math.round(255*amt));
  b = Math.min(255, b + Math.round(255*amt));
  return `rgb(${r},${g},${b})`;
}
function darkenColor(hex, amt){
  let [r,g,b] = h2r(hex);
  r = Math.max(0, r - Math.round(255*amt));
  g = Math.max(0, g - Math.round(255*amt));
  b = Math.max(0, b - Math.round(255*amt));
  return `rgb(${r},${g},${b})`;
}

// Initial dice draw
function getCurrentPlayerColor(){
  if(!G || !G.pieces) return '#ffffff';
  return PC[G.cur].css;
}

// Shake animation frame
let shakeAnim = null;
function startDiceShake(){
  diceShaking = true;
  document.getElementById('diceWrap').style.animation = 'diceShake .09s linear infinite';
}
function stopDiceShake(){
  diceShaking = false;
  document.getElementById('diceWrap').style.animation = '';
}

// Draw dice initially
drawDice(1, '#ffffff', false);


const cv=document.getElementById('ludo');
const ctx=cv.getContext('2d');
let SZ=400, C=SZ/15;

function resizeBoard(){
  const topH=52, botH=document.getElementById('botbar').offsetHeight||165;
  const avW=window.innerWidth-8;
  const avH=window.innerHeight-topH-botH-8;
  SZ=Math.floor(Math.min(avW,avH,640));
  SZ=Math.max(SZ,260);
  C=SZ/15;
  cv.width=SZ;cv.height=SZ;
  cv.style.width=SZ+'px';cv.style.height=SZ+'px';
}

// ── Setup Screen ──────────────────────────────────
let humanCnt=4;

// Animated bubbles
function setupBubbles(){
  const bg=document.getElementById('setupBg');
  for(let i=0;i<8;i++){
    const b=document.createElement('div');
    b.className='bubble';
    const sz=40+Math.random()*120;
    b.style.cssText=`width:${sz}px;height:${sz}px;left:${Math.random()*100}%;top:${Math.random()*100}%;animation-delay:${Math.random()*4}s;animation-duration:${4+Math.random()*4}s`;
    bg.appendChild(b);
  }
}
setupBubbles();

function selP(n){
  humanCnt=n;
  document.querySelectorAll('.pbtn').forEach(b=>b.classList.toggle('sel',+b.dataset.n===n));
  buildPrev(n);
}

function buildPrev(n){
  const d=document.getElementById('pprev');
  d.innerHTML=PC.map((p,i)=>{
    const bot=i>=n;
    return`<div class="pp-row" style="color:${p.css}">
      <div class="pp-dot" style="background:${p.css}"></div>
      <div class="pp-name">${p.icon} ${p.full}</div>
      <div class="pp-type ${bot?'bot':'human'}">${bot?'🤖 BOT':'👤 HUMAN'}</div>
    </div>`;
  }).join('');
}
buildPrev(4);

function goSetup(){
  document.getElementById('winscreen').style.display='none';
  document.getElementById('game').style.display='none';
  document.getElementById('setup').style.display='flex';
}

function startGame(){
  initAudio();
  document.getElementById('setup').style.display='none';
  document.getElementById('game').style.display='flex';
  setTimeout(()=>{
    resizeBoard();
    initGame(humanCnt);
  },50);
}

// ── Game State ────────────────────────────────────
let G={};

function initGame(humans){
  for(let i=0;i<4;i++){
    const bd=document.getElementById('b'+i);
    bd.textContent=i<humans?'YOU':'BOT';
  }
  G={
    humans, bot:[0,1,2,3].map(i=>i>=humans),
    pieces:Array.from({length:4},()=>Array.from({length:4},()=>({pos:-1,animX:0,animY:0}))),
    cur:0, dice:0, prevDice:0,
    rolling:false, moving:false, selecting:false,
    movable:[], done:false,
    wonOrder:[],
  };
  document.getElementById('winscreen').style.display='none';
  document.getElementById('rollbtn').disabled=false;
  diceValue = 1;
  drawDice(1, PC[0].css, false);
  updateUI();
  setMsg(`${PC[0].icon} ${PC[0].full}${G.bot[0]?' (Bot)':''} — Roll the dice!`);
  if(G.bot[0]) setTimeout(rollDice,1000);
}

// ── Piece helpers ─────────────────────────────────
function pRC(pi,pos){
  if(pos<0||pos>=58) return null;
  if(pos>=52){const x=pos-52;return x<6?HCOL[pi][x]:null;}
  return BPATH[(ENTRY[pi]+pos)%52];
}
function hRC(pi,i){return HBASE[pi][i];}

function canMove(pi,i,dice){
  const pos=G.pieces[pi][i].pos;
  if(pos>=58) return false;
  if(pos===-1) return dice===6;
  if(pos>=52) return (pos-52)+dice<=5;
  const np=pos+dice;
  return np<=51||(np-52)<=5;
}

function getMovable(pi,dice){
  return[0,1,2,3].filter(i=>canMove(pi,i,dice));
}

// ── Bot AI ────────────────────────────────────────
function botPick(pi,dice,mv){
  if(mv.length===1) return mv[0];
  let best=mv[0],bsc=-Infinity;
  for(const i of mv){
    let sc=0;
    const pos=G.pieces[pi][i].pos;
    // Capture check
    if(pos!==-1&&pos+dice<52){
      const rc2=BPATH[(ENTRY[pi]+pos+dice)%52];
      if(!SAFE.has(rc2[0]+','+rc2[1])){
        for(let opi=0;opi<4;opi++){
          if(opi===pi) continue;
          for(let oi=0;oi<4;oi++){
            const op=G.pieces[opi][oi];
            if(op.pos<0||op.pos>=52) continue;
            const orc=BPATH[(ENTRY[opi]+op.pos)%52];
            if(orc[0]===rc2[0]&&orc[1]===rc2[1]) sc+=500;
          }
        }
      }
    }
    const np=pos===-1?0:pos+dice;
    if(np>=52) sc+=200;
    if(pos>=52) sc+=300+np;
    sc+=np*2;
    if(pos===-1) sc+=60;
    if(sc>bsc){bsc=sc;best=i;}
  }
  return best;
}

// ── Dice Roll ─────────────────────────────────────
function rollDice(){
  if(G.rolling||G.moving||G.selecting||G.done) return;
  initAudio();
  G.rolling=true;
  document.getElementById('rollbtn').disabled=true;
  playSound('dice');
  startDiceShake();

  const pcolor = PC[G.cur].css;
  let t=0;
  const spin=setInterval(()=>{
    const v=Math.floor(Math.random()*6)+1;
    diceValue = v;
    drawDice(v, pcolor, true); // draw rolling state
    playSound('tick');
    if(++t>16){
      clearInterval(spin);
      stopDiceShake();
      G.dice=v; G.rolling=false;
      drawDice(v, pcolor, false); // final settled dice
      // Bounce animation on dice wrap
      const dw = document.getElementById('diceWrap');
      dw.style.transition='transform .15s';
      dw.style.transform='scale(1.25)';
      setTimeout(()=>{ dw.style.transform='scale(1)'; },150);
      if(v===6) playSound('six');
      showDiceResult(G.cur,v);
      onRoll(G.cur,v);
    }
  },65);
}

function showDiceResult(pi,v){
  showToast(`${PC[pi].icon} ${PC[pi].full} rolled a ${v}!`);
}

function onRoll(pi,dice){
  const mv=getMovable(pi,dice);
  if(!mv.length){
    setMsg(`${PC[pi].icon} ${PC[pi].full}: No moves for ${dice}`);
    showToast('No moves — next turn!');
    setTimeout(nextTurn,900); return;
  }
  if(G.bot[pi]){
    const c=botPick(pi,dice,mv);
    setMsg(`${PC[pi].icon} ${PC[pi].full} (Bot) moving piece ${c+1}...`);
    setTimeout(()=>doMove(pi,c,dice,()=>{if(!G.done)endTurn(pi,dice);}),500);
    return;
  }
  if(mv.length===1&&G.pieces[pi][mv[0]].pos!==-1){
    setMsg(`${PC[pi].icon} ${PC[pi].full} rolled ${dice}!`);
    doMove(pi,mv[0],dice,()=>{if(!G.done)endTurn(pi,dice);});
    return;
  }
  // Let human choose (includes home base pieces)
  G.selecting=true; G.movable=mv;
  if(mv.some(i=>G.pieces[pi][i].pos===-1)){
    setMsg(`🏠 Tap your home piece or board piece to move! (${dice})`);
  } else {
    setMsg(`Tap a glowing piece to move! (rolled ${dice})`);
  }
}

// ── Move piece step by step ────────────────────────
let stepTimer=null;

function doMove(pi,i,dice,cb){
  G.moving=true;
  const piece=G.pieces[pi][i];

  if(piece.pos===-1){
    piece.pos=0;
    playSound('move');
    render();
    setTimeout(()=>afterMove(pi,i,cb),200);
    return;
  }

  let steps=dice;
  function step(){
    if(steps<=0){afterMove(pi,i,cb);return;}
    steps--;
    piece.pos++;
    playSound('move');
    render();
    stepTimer=setTimeout(step,120);
  }
  step();
}

function afterMove(pi,i,cb){
  const piece=G.pieces[pi][i];

  // Win check
  if(piece.pos>=58){
    piece.pos=58;
    playSound('home');
    G.wonOrder.push(pi);
    const w=G.pieces[pi].filter(p=>p.pos>=58).length;
    updateDots(pi);
    render();
    showToast(`${PC[pi].icon} ${PC[pi].full} piece reached home! 🏠`);
    spawnParticles(PC[pi].css,20);
    if(w===4){
      setTimeout(()=>showWin(pi),500);
      G.moving=false; return;
    }
    setMsg(`${PC[pi].icon} Piece home! ${4-w} to go.`);
    G.moving=false; cb(); return;
  }

  // Capture
  if(piece.pos>=0&&piece.pos<52){
    const rc=pRC(pi,piece.pos);
    if(rc&&!SAFE.has(rc[0]+','+rc[1])){
      for(let opi=0;opi<4;opi++){
        if(opi===pi) continue;
        for(let oi=0;oi<4;oi++){
          const op=G.pieces[opi][oi];
          if(op.pos<0||op.pos>=52) continue;
          const orc=pRC(opi,op.pos);
          if(orc&&orc[0]===rc[0]&&orc[1]===rc[1]){
            op.pos=-1;
            playSound('capture');
            render();
            showToast(`✂️ ${PC[pi].full} captured ${PC[opi].full}!`);
            spawnParticles('#ff4400',15);
          }
        }
      }
    }
  }
  G.moving=false; cb();
}

function endTurn(pi,dice){
  if(dice===6){
    showToast(`🎲 ${PC[pi].full} rolled 6 — ROLL AGAIN!`);
    playSound('six');
    drawDice(6, PC[pi].css, false);
    setMsg(`${PC[pi].icon} Rolled 6! Roll again!`);
    document.getElementById('rollbtn').disabled=G.bot[pi];
    if(G.bot[pi]) setTimeout(rollDice,800);
  } else nextTurn();
}

function nextTurn(){
  G.cur=(G.cur+1)%4;
  diceValue = 1; // reset dice display
  updateUI();
  const pi=G.cur;
  drawDice(1, PC[pi].css, false);
  setMsg(`${PC[pi].icon} ${PC[pi].full}${G.bot[pi]?' (Bot)':''}'s turn — Roll!`);
  document.getElementById('rollbtn').disabled=G.bot[pi];
  if(G.bot[pi]) setTimeout(rollDice,900);
}

// ── Click Handler ─────────────────────────────────
cv.addEventListener('click',e=>{
  if(!G.selecting) return;
  const r=cv.getBoundingClientRect();
  const scaleX=SZ/r.width, scaleY=SZ/r.height;
  const mx=(e.clientX-r.left)*scaleX;
  const my=(e.clientY-r.top)*scaleY;
  const pi=G.cur;

  for(const i of G.movable){
    const p=G.pieces[pi][i];
    // Check home base click OR board piece click
    const rc=p.pos===-1?hRC(pi,i):pRC(pi,p.pos);
    if(!rc) continue;
    const cx=rc[1]*C+C/2, cy=rc[0]*C+C/2;
    const hitR=p.pos===-1 ? C*.55 : C*.5; // slightly bigger hit area for home
    if(Math.hypot(mx-cx,my-cy)<hitR){
      G.selecting=false; G.movable=[];
      setMsg(`Moving piece ${i+1}...`);
      doMove(pi,i,G.dice,()=>{if(!G.done)endTurn(pi,G.dice);});
      return;
    }
  }
});

cv.addEventListener('touchend',e=>{
  if(!G.selecting) return;
  e.preventDefault();
  const r=cv.getBoundingClientRect();
  const touch=e.changedTouches[0];
  const scaleX=SZ/r.width, scaleY=SZ/r.height;
  const mx=(touch.clientX-r.left)*scaleX;
  const my=(touch.clientY-r.top)*scaleY;
  const pi=G.cur;

  for(const i of G.movable){
    const p=G.pieces[pi][i];
    const rc=p.pos===-1?hRC(pi,i):pRC(pi,p.pos);
    if(!rc) continue;
    const cx=rc[1]*C+C/2, cy=rc[0]*C+C/2;
    const hitR=p.pos===-1?C*.6:C*.52;
    if(Math.hypot(mx-cx,my-cy)<hitR){
      G.selecting=false; G.movable=[];
      setMsg(`Moving piece ${i+1}...`);
      doMove(pi,i,G.dice,()=>{if(!G.done)endTurn(pi,G.dice);});
      return;
    }
  }
},{passive:false});

// ── Drawing ───────────────────────────────────────
function render(){
  drawBoard();
  drawPieces();
}

function drawBoard(){
  // Base board
  const bg=ctx.createLinearGradient(0,0,SZ,SZ);
  bg.addColorStop(0,'#f0ddb5');bg.addColorStop(1,'#e6d09c');
  ctx.fillStyle=bg;ctx.fillRect(0,0,SZ,SZ);

  drawQuads();
  drawPath();
  drawHCols();
  drawCenter();
  drawGrid();
}

function drawQuads(){
  [[0,0],[0,9],[9,9],[9,0]].forEach(([qr,qc],qi)=>{
    const p=PC[qi];
    const x=qc*C,y=qr*C,w=6*C,h=6*C;
    // Outer frame
    ctx.fillStyle=p.lighter;ctx.strokeStyle=p.dark;ctx.lineWidth=2;
    rr(x+1,y+1,w-2,h-2,10);ctx.fill();ctx.stroke();
    // Inner colored box (4x4)
    const ix=(qc+1)*C,iy=(qr+1)*C,iw=4*C,ih=4*C;
    const g=ctx.createLinearGradient(ix,iy,ix+iw,iy+ih);
    g.addColorStop(0,p.css);g.addColorStop(1,p.dark);
    ctx.fillStyle=g;rr(ix+1,iy+1,iw-2,ih-2,8);ctx.fill();
    // Inner shine
    ctx.fillStyle='rgba(255,255,255,.22)';rr(ix+3,iy+3,iw-6,ih*.28,5);ctx.fill();

    // Home circles with 3D effect
    HBASE[qi].forEach(([hr,hc])=>{
      const cx=hc*C+C/2,cy=hr*C+C/2,rv=C*.38;
      // Shadow
      ctx.beginPath();ctx.ellipse(cx+1.5,cy+2,rv,rv*.5,0,0,Math.PI*2);
      ctx.fillStyle='rgba(0,0,0,.25)';ctx.fill();
      // Circle
      ctx.beginPath();ctx.arc(cx,cy,rv,0,Math.PI*2);
      ctx.fillStyle='rgba(255,255,255,.3)';ctx.fill();
      ctx.strokeStyle='rgba(255,255,255,.55)';ctx.lineWidth=2;ctx.stroke();
      // Inner glow
      ctx.beginPath();ctx.arc(cx-rv*.25,cy-rv*.25,rv*.35,0,Math.PI*2);
      ctx.fillStyle='rgba(255,255,255,.2)';ctx.fill();
    });

    // Player icon
    ctx.font=C*.75+'px serif';ctx.textAlign='center';ctx.textBaseline='middle';
    ctx.fillText(p.icon,(qc+3)*C,(qr+3)*C);
  });
}

function drawPath(){
  BPATH.forEach(([r,c],idx)=>{
    const x=c*C,y=r*C;
    const ei=ENTRY.findIndex(e=>e===idx);
    const safe=SAFE.has(r+','+c);
    if(ei>=0) ctx.fillStyle=PC[ei].light;
    else if(safe) ctx.fillStyle='#d0f0d0';
    else ctx.fillStyle='#eeddc8';

    ctx.fillRect(x+.5,y+.5,C-1,C-1);
    // Bevel
    ctx.fillStyle='rgba(0,0,0,.08)';ctx.fillRect(x+1,y+C-3,C-2,2);ctx.fillRect(x+C-3,y+1,2,C-3);
    ctx.fillStyle='rgba(255,255,255,.3)';ctx.fillRect(x+1,y+1,C-3,2);ctx.fillRect(x+1,y+1,2,C-3);
    ctx.strokeStyle='rgba(160,120,70,.28)';ctx.lineWidth=.7;ctx.strokeRect(x+.5,y+.5,C-1,C-1);

    if(ei>=0){
      ctx.font=C*.5+'px serif';ctx.textAlign='center';ctx.textBaseline='middle';
      ctx.fillText('⭐',c*C+C/2,r*C+C/2+1);
    } else if(safe){
      star5(c*C+C/2,r*C+C/2,C*.2,C*.1,'#44aa44',.7);
    }
  });
}

function drawHCols(){
  HCOL.forEach((hs,pi)=>{
    hs.forEach(([r,c],step)=>{
      const x=c*C,y=r*C,t=step/5;
      if(step===5) ctx.fillStyle=PC[pi].css;
      else{const [R,G2,B]=h2r(PC[pi].css);ctx.fillStyle=`rgba(${R},${G2},${B},${.18+t*.55})`;}
      ctx.fillRect(x+.5,y+.5,C-1,C-1);
      ctx.fillStyle='rgba(255,255,255,.18)';ctx.fillRect(x+1,y+1,C-3,2);
      ctx.strokeStyle=PC[pi].dark;ctx.lineWidth=.8;ctx.strokeRect(x+.5,y+.5,C-1,C-1);
      if(step===5){
        ctx.font=C*.55+'px serif';ctx.textAlign='center';ctx.textBaseline='middle';
        ctx.fillText('🏠',c*C+C/2,r*C+C/2+1);
      } else {
        const arr=['▲','▶','▼','◀'];
        ctx.fillStyle='rgba(255,255,255,.45)';ctx.font='bold '+C*.38+'px Arial';
        ctx.textAlign='center';ctx.textBaseline='middle';
        ctx.fillText(arr[pi],c*C+C/2,r*C+C/2);
      }
    });
  });
}

function drawCenter(){
  const cs=[[6*C,6*C],[9*C,6*C],[9*C,9*C],[6*C,9*C]],cn=[7.5*C,7.5*C];
  PC.forEach((p,pi)=>{
    ctx.beginPath();ctx.moveTo(cs[pi][0],cs[pi][1]);
    ctx.lineTo(cs[(pi+1)%4][0],cs[(pi+1)%4][1]);
    ctx.lineTo(cn[0],cn[1]);ctx.closePath();
    ctx.fillStyle=p.css;ctx.globalAlpha=.72;ctx.fill();
    ctx.strokeStyle=p.dark;ctx.lineWidth=1.2;ctx.globalAlpha=1;ctx.stroke();
  });
  ctx.beginPath();ctx.arc(cn[0],cn[1],C*.72,0,Math.PI*2);
  const g=ctx.createRadialGradient(cn[0]-C*.22,cn[1]-C*.22,3,cn[0],cn[1],C*.72);
  g.addColorStop(0,'#fffde0');g.addColorStop(.5,'#ffd700');g.addColorStop(1,'#cc8800');
  ctx.fillStyle=g;ctx.fill();ctx.strokeStyle='#996600';ctx.lineWidth=2.5;ctx.stroke();
  ctx.font='bold '+C*.9+'px Arial';ctx.textAlign='center';ctx.textBaseline='middle';
  ctx.fillStyle='rgba(255,255,255,.92)';ctx.fillText('★',cn[0],cn[1]+2);
}

function drawGrid(){
  ctx.strokeStyle='rgba(130,100,60,.1)';ctx.lineWidth=.5;
  for(let i=0;i<=15;i++){
    ctx.beginPath();ctx.moveTo(i*C,0);ctx.lineTo(i*C,SZ);ctx.stroke();
    ctx.beginPath();ctx.moveTo(0,i*C);ctx.lineTo(SZ,i*C);ctx.stroke();
  }
}

// ── Draw Pieces ───────────────────────────────────
function drawPieces(){
  const occ={};
  for(let pi=0;pi<4;pi++){
    for(let i=0;i<4;i++){
      const p=G.pieces[pi][i];
      if(p.pos>=58){drawWon(pi,i);continue;}
      const rc=p.pos===-1?hRC(pi,i):pRC(pi,p.pos);
      if(!rc) continue;
      const k=rc[0]+','+rc[1];
      if(!occ[k]) occ[k]=[];
      occ[k].push({pi,i,rc});
    }
  }
  Object.values(occ).forEach(grp=>{
    grp.forEach(({pi,i,rc},idx)=>{
      const off=[[-0.22,-0.22],[0.22,-0.22],[-0.22,0.22],[0.22,0.22]];
      const ox=grp.length>1?off[idx%4][0]*C:0;
      const oy=grp.length>1?off[idx%4][1]*C:0;
      drawPiece(rc[1]*C+C/2+ox,rc[0]*C+C/2+oy,pi,i);
    });
  });
}

function drawPiece(cx,cy,pi,i){
  const sel=G.selecting&&G.movable.includes(i)&&pi===G.cur;
  const p=PC[pi];
  const rv=C*.33;

  // Glow ring for selectable pieces
  if(sel){
    const t=Date.now()*.009;
    const pulse=.85+.15*Math.sin(t);
    // Outer glow
    ctx.save();
    ctx.shadowColor=p.css;ctx.shadowBlur=25;
    ctx.beginPath();ctx.arc(cx,cy,rv*1.8*pulse,0,Math.PI*2);
    ctx.strokeStyle=p.css;ctx.lineWidth=3;ctx.stroke();
    ctx.restore();
    // Inner ring
    ctx.beginPath();ctx.arc(cx,cy,rv*1.4,0,Math.PI*2);
    ctx.strokeStyle='rgba(255,255,255,.5)';ctx.lineWidth=1.5;ctx.stroke();
    // Sparkle dots
    for(let s=0;s<6;s++){
      const a=(s/6)*Math.PI*2+t;
      const sr=rv*2;
      ctx.beginPath();ctx.arc(cx+Math.cos(a)*sr,cy+Math.sin(a)*sr,2.5,0,Math.PI*2);
      ctx.fillStyle=p.css;ctx.globalAlpha=.8;ctx.fill();ctx.globalAlpha=1;
    }
  }

  // Shadow
  ctx.beginPath();ctx.ellipse(cx+2,cy+3,rv*.82,rv*.45,0,0,Math.PI*2);
  ctx.fillStyle='rgba(0,0,0,.3)';ctx.fill();

  // Piece body — metallic look
  const gr=ctx.createRadialGradient(cx-rv*.35,cy-rv*.35,rv*.05,cx,cy,rv);
  gr.addColorStop(0,'rgba(255,255,255,.95)');
  gr.addColorStop(.25,p.css);
  gr.addColorStop(.7,p.css);
  gr.addColorStop(1,p.dark);

  ctx.save();
  if(sel){ctx.shadowColor=p.css;ctx.shadowBlur=16;}
  ctx.beginPath();ctx.arc(cx,cy,rv,0,Math.PI*2);
  ctx.fillStyle=gr;ctx.fill();
  ctx.strokeStyle=p.dark;ctx.lineWidth=1.8;ctx.stroke();
  ctx.restore();

  // Top dome highlight
  const dg=ctx.createRadialGradient(cx-rv*.3,cy-rv*.35,1,cx-rv*.1,cy-rv*.1,rv*.5);
  dg.addColorStop(0,'rgba(255,255,255,.6)');
  dg.addColorStop(1,'rgba(255,255,255,0)');
  ctx.beginPath();ctx.arc(cx,cy,rv,0,Math.PI*2);
  ctx.fillStyle=dg;ctx.fill();

  // Piece number
  ctx.fillStyle='rgba(255,255,255,.92)';
  ctx.font='bold '+C*.26+'px Nunito';
  ctx.textAlign='center';ctx.textBaseline='middle';
  ctx.fillText(i+1,cx,cy+.5);
}

function drawWon(pi,i){
  const t=Date.now()*.001;
  const a=t*(1+pi*.35)+i*(Math.PI*.5);
  const or2=C*(1.1+pi*.28);
  const cx=7.5*C+Math.cos(a)*or2,cy=7.5*C+Math.sin(a)*or2;
  drawPiece(cx,cy,pi,i);
  ctx.font=C*.26+'px serif';ctx.textAlign='center';
  ctx.fillText('👑',cx,cy-C*.48);
}

// ── UI ────────────────────────────────────────────
function setMsg(t){document.getElementById('msgbox').textContent=t;}

function updateUI(){
  if(!G.pieces) return;
  for(let p=0;p<4;p++){
    document.getElementById('pc'+p).classList.toggle('active',p===G.cur);
    updateDots(p);
  }
  // Redraw dice with current player's color
  drawDice(diceValue, PC[G.cur].css, false);
}

function updateDots(p){
  const pw=document.getElementById('pd'+p);
  pw.innerHTML='';
  for(let i=0;i<4;i++){
    const d=document.createElement('div');
    d.className='pdot';
    d.style.background=PC[p].css;
    d.style.borderColor=PC[p].dark;
    d.style.color=PC[p].css;
    const pos=G.pieces[p][i].pos;
    d.classList.add(pos>=58?'won':pos===-1?'home':'board');
    pw.appendChild(d);
  }
}

function showWin(pi){
  G.done=true;
  playSound('win');
  spawnParticles(PC[pi].css,40);
  setTimeout(()=>spawnParticles('#ffd700',30),300);
  document.getElementById('wname').textContent=`${PC[pi].icon} ${PC[pi].full}`;
  document.getElementById('wname').style.color=PC[pi].css;
  document.getElementById('winscreen').style.display='flex';
}

// ── Toast ─────────────────────────────────────────
let toastTimer;
function showToast(msg){
  const t=document.getElementById('toast');
  t.textContent=msg;t.classList.add('show');
  clearTimeout(toastTimer);
  toastTimer=setTimeout(()=>t.classList.remove('show'),2200);
}

// ── Particles ─────────────────────────────────────
function spawnParticles(color,count){
  const container=document.getElementById('particles');
  const bRect=cv.getBoundingClientRect();
  const cx=bRect.left+bRect.width/2;
  const cy=bRect.top+bRect.height/2;

  for(let i=0;i<count;i++){
    const el=document.createElement('div');
    el.className='particle';
    const sz=4+Math.random()*8;
    const tx=(Math.random()-0.5)*200+'px';
    const ty=(-100-Math.random()*150)+'px';
    el.style.cssText=`
      width:${sz}px;height:${sz}px;
      background:${color};
      left:${cx}px;top:${cy}px;
      --tx:${tx};--ty:${ty};
      animation-delay:${Math.random()*.3}s;
      animation-duration:${.8+Math.random()*.6}s;
      box-shadow:0 0 6px ${color};
    `;
    container.appendChild(el);
    setTimeout(()=>el.remove(),1800);
  }
}

// ── Helpers ───────────────────────────────────────
function rr(x,y,w,h,r){
  ctx.beginPath();
  ctx.moveTo(x+r,y);ctx.lineTo(x+w-r,y);ctx.quadraticCurveTo(x+w,y,x+w,y+r);
  ctx.lineTo(x+w,y+h-r);ctx.quadraticCurveTo(x+w,y+h,x+w-r,y+h);
  ctx.lineTo(x+r,y+h);ctx.quadraticCurveTo(x,y+h,x,y+h-r);
  ctx.lineTo(x,y+r);ctx.quadraticCurveTo(x,y,x+r,y);
  ctx.closePath();
}
function star5(x,y,oR,iR,col,a){
  ctx.save();ctx.globalAlpha=a;ctx.beginPath();
  for(let i=0;i<10;i++){
    const ang=(i*Math.PI)/5-Math.PI/2,rv=i%2===0?oR:iR;
    i===0?ctx.moveTo(x+rv*Math.cos(ang),y+rv*Math.sin(ang)):ctx.lineTo(x+rv*Math.cos(ang),y+rv*Math.sin(ang));
  }
  ctx.closePath();ctx.fillStyle=col;ctx.fill();ctx.restore();
}
function h2r(h){return[parseInt(h.slice(1,3),16),parseInt(h.slice(3,5),16),parseInt(h.slice(5,7),16)];}

// ── Animation Loop ────────────────────────────────
function loop(){
  if(G.pieces) render();
  requestAnimationFrame(loop);
}
loop();

// ── Resize ────────────────────────────────────────
let rzTimer;
window.addEventListener('resize',()=>{
  clearTimeout(rzTimer);
  rzTimer=setTimeout(()=>{
    if(G.pieces&&document.getElementById('game').style.display!=='none'){
      resizeBoard();render();
    }
  },150);
});
</script>
<!-- ═══ INTERSTITIAL AD (between games) ═══ -->
<div id="adInterstitial">
  <div class="ad-skip-bar">
    <span class="ad-skip-txt">Ad • <span id="adTimer">5</span>s</span>
    <button class="ad-skip-btn" id="adSkipBtn" disabled onclick="skipAd()">SKIP ▶</button>
  </div>
  <div class="ad-box">
    <!-- STEP 4: Interstitial / Rectangle ad slot -->
    <ins class="adsbygoogle"
         style="display:inline-block;width:300px;height:250px"
         data-ad-client="ca-pub-XXXXXXXXXXXXXXXXX"
         data-ad-slot="XXXXXXXXXX"></ins>
  </div>
  <div class="ad-countdown" id="adMsg">Loading next game...</div>
</div>

</body>
</html>
