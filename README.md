<!DOCTYPE html>
<html lang="uz">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Baxodir AI</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#0a0a14;--bg2:#12121f;--bg3:#1a1a2e;--card:#1e1e35;--card2:#252542;
  --border:#2a2a45;--accent:#7c6fff;--accent2:#a78bfa;--accent3:#38bdf8;
  --pink:#f472b6;--green:#22c55e;--red:#ef4444;--text:#e2e8f0;
  --text2:#94a3b8;--text3:#4a5568;--radius:16px;
}
body{font-family:'Inter',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;overflow-x:hidden}

/* ===== AUTH SCREENS ===== */
.auth-wrap{min-height:100vh;display:flex;align-items:center;justify-content:center;padding:20px;position:relative;overflow:hidden}
.auth-wrap::before{content:'';position:fixed;inset:0;background:radial-gradient(ellipse 80% 60% at 50% -20%,rgba(124,111,255,0.18),transparent),radial-gradient(ellipse 60% 50% at 80% 80%,rgba(56,189,248,0.1),transparent);pointer-events:none}

.auth-card{background:var(--bg2);border:1px solid var(--border);border-radius:24px;padding:40px 36px;width:100%;max-width:420px;position:relative;z-index:1;box-shadow:0 24px 60px rgba(0,0,0,0.4)}

.auth-logo{text-align:center;margin-bottom:28px}
.auth-logo .logo-icon{width:64px;height:64px;border-radius:20px;background:linear-gradient(135deg,var(--accent),var(--accent3));display:inline-flex;align-items:center;justify-content:center;font-size:30px;margin-bottom:14px;box-shadow:0 8px 24px rgba(124,111,255,0.35)}
.auth-logo h1{font-size:24px;font-weight:800;background:linear-gradient(135deg,var(--accent2),var(--accent3));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.auth-logo p{font-size:13px;color:var(--text2);margin-top:4px}

.auth-tabs{display:flex;background:var(--bg3);border-radius:12px;padding:4px;margin-bottom:24px;gap:4px}
.auth-tab{flex:1;padding:9px;border-radius:9px;border:none;cursor:pointer;font-size:13px;font-weight:600;background:transparent;color:var(--text2);transition:all 0.2s}
.auth-tab.active{background:var(--card2);color:var(--text);box-shadow:0 2px 8px rgba(0,0,0,0.3)}

.social-btns{display:flex;flex-direction:column;gap:10px;margin-bottom:20px}
.social-btn{width:100%;padding:12px 16px;border-radius:12px;border:1px solid var(--border);background:var(--card);cursor:pointer;font-size:14px;font-weight:500;color:var(--text);display:flex;align-items:center;justify-content:center;gap:10px;transition:all 0.2s}
.social-btn:hover{border-color:var(--accent);background:var(--card2);transform:translateY(-1px)}
.social-btn svg{width:20px;height:20px;flex-shrink:0}

.divider{display:flex;align-items:center;gap:12px;margin:20px 0;color:var(--text3);font-size:12px}
.divider::before,.divider::after{content:'';flex:1;height:1px;background:var(--border)}

.form-group{margin-bottom:14px}
.form-label{font-size:12px;font-weight:600;color:var(--text2);margin-bottom:6px;display:block}
.form-input{width:100%;padding:12px 14px;border-radius:12px;border:1.5px solid var(--border);background:var(--card);color:var(--text);font-size:14px;outline:none;transition:border-color 0.2s;font-family:'Inter',sans-serif}
.form-input:focus{border-color:var(--accent)}
.form-input::placeholder{color:var(--text3)}

.form-row{display:flex;align-items:center;justify-content:space-between;margin-bottom:18px}
.checkbox-wrap{display:flex;align-items:center;gap:7px;cursor:pointer}
.checkbox-wrap input{accent-color:var(--accent);width:15px;height:15px}
.checkbox-wrap span{font-size:13px;color:var(--text2)}
.forgot-link{font-size:13px;color:var(--accent2);cursor:pointer;text-decoration:none}
.forgot-link:hover{text-decoration:underline}

.auth-btn{width:100%;padding:13px;border-radius:12px;border:none;background:linear-gradient(135deg,var(--accent),var(--accent3));color:#fff;font-size:15px;font-weight:700;cursor:pointer;transition:all 0.2s;margin-bottom:16px}
.auth-btn:hover{opacity:0.9;transform:translateY(-1px);box-shadow:0 8px 20px rgba(124,111,255,0.35)}
.auth-btn:active{transform:scale(0.98)}

.auth-footer{text-align:center;font-size:13px;color:var(--text2)}
.auth-footer a{color:var(--accent2);cursor:pointer}
.auth-footer a:hover{text-decoration:underline}

.terms{font-size:11px;color:var(--text3);text-align:center;margin-top:16px;line-height:1.6}
.terms a{color:var(--text3);text-decoration:underline;cursor:pointer}

/* ERROR / SUCCESS */
.msg-box{padding:10px 14px;border-radius:10px;font-size:13px;margin-bottom:14px;display:none}
.msg-box.error{background:rgba(239,68,68,0.1);border:1px solid rgba(239,68,68,0.3);color:#fca5a5}
.msg-box.success{background:rgba(34,197,94,0.1);border:1px solid rgba(34,197,94,0.3);color:#86efac}
.msg-box.show{display:block}

/* USER AVATAR in top */
.user-chip{display:flex;align-items:center;gap:8px;background:var(--card);border:1px solid var(--border);border-radius:999px;padding:5px 12px 5px 5px;cursor:pointer;transition:all 0.2s}
.user-chip:hover{border-color:var(--accent)}
.user-chip .uc-avatar{width:28px;height:28px;border-radius:50%;background:linear-gradient(135deg,var(--accent),var(--pink));display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:700;color:#fff}
.user-chip .uc-name{font-size:13px;font-weight:500;color:var(--text);max-width:100px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}

/* DROPDOWN */
.user-dropdown{position:absolute;top:calc(100% + 8px);right:0;background:var(--card);border:1px solid var(--border);border-radius:14px;padding:6px;min-width:180px;z-index:200;box-shadow:0 12px 32px rgba(0,0,0,0.4)}
.ud-item{padding:9px 12px;border-radius:9px;cursor:pointer;font-size:13px;color:var(--text2);display:flex;align-items:center;gap:8px;transition:all 0.15s}
.ud-item:hover{background:var(--card2);color:var(--text)}
.ud-item.danger:hover{color:var(--red);background:rgba(239,68,68,0.08)}
.ud-sep{height:1px;background:var(--border);margin:4px 0}

/* ===== MAIN APP ===== */
#app{display:none}
.layout{display:flex;min-height:100vh}

.sidebar{width:255px;min-height:100vh;background:var(--bg2);border-right:1px solid var(--border);display:flex;flex-direction:column;padding:16px 0;flex-shrink:0;transition:transform 0.3s}
.logo-wrap{padding:0 16px 16px;border-bottom:1px solid var(--border);margin-bottom:12px}
.logo-wrap h1{font-size:18px;font-weight:800;background:linear-gradient(135deg,var(--accent2),var(--accent3));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.logo-wrap span{font-size:11px;color:var(--text3)}

.sb-section{padding:0 10px;margin-bottom:8px}
.sb-label{font-size:10px;font-weight:700;color:var(--text3);text-transform:uppercase;letter-spacing:1px;padding:0 6px;margin-bottom:6px}
.new-btn{width:100%;padding:9px 12px;border-radius:10px;border:1px dashed var(--border);background:transparent;color:var(--accent2);cursor:pointer;font-size:13px;font-weight:600;display:flex;align-items:center;gap:8px;transition:all 0.2s;margin-bottom:14px}
.new-btn:hover{background:rgba(124,111,255,0.08);border-color:var(--accent)}

.recents-list{display:flex;flex-direction:column;gap:2px;max-height:280px;overflow-y:auto}
.r-item{padding:8px 10px;border-radius:9px;cursor:pointer;display:flex;align-items:center;gap:7px;transition:all 0.15s;border:1px solid transparent}
.r-item:hover{background:var(--card);border-color:var(--border)}
.r-ico{font-size:14px;flex-shrink:0}
.r-body{flex:1;min-width:0}
.r-title{font-size:12px;font-weight:500;color:var(--text);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.r-sub{font-size:10px;color:var(--text3);margin-top:1px}
.r-del{font-size:13px;color:var(--text3);opacity:0;padding:2px 5px;border-radius:5px}
.r-item:hover .r-del{opacity:1}
.r-del:hover{color:var(--red)!important;background:rgba(239,68,68,0.1)}
.no-rec{font-size:12px;color:var(--text3);text-align:center;padding:12px}

.sb-bottom{margin-top:auto;padding:12px 10px 0;border-top:1px solid var(--border)}
.ver{font-size:10px;color:var(--text3);text-align:center}

.main{flex:1;display:flex;flex-direction:column;min-width:0}
.topnav{padding:12px 20px;border-bottom:1px solid var(--border);display:flex;align-items:center;gap:12px;background:var(--bg2);position:relative}
.menu-btn{display:none;background:none;border:none;color:var(--text);font-size:20px;cursor:pointer}
.nav-title{font-size:14px;font-weight:600;flex:1}
.online-b{display:flex;align-items:center;gap:5px;font-size:11px;color:var(--green);background:rgba(34,197,94,0.08);padding:4px 10px;border-radius:999px;border:1px solid rgba(34,197,94,0.15)}
.online-dot{width:6px;height:6px;border-radius:50%;background:var(--green);animation:pulse 2s infinite}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:0.4}}

.subjects-bar{padding:12px 20px;border-bottom:1px solid var(--border);background:var(--bg3)}
.subjects{display:flex;gap:7px;overflow-x:auto;padding-bottom:2px;scrollbar-width:none}
.subjects::-webkit-scrollbar{display:none}
.s-btn{border:1px solid var(--border);background:var(--card);border-radius:10px;padding:8px 14px;cursor:pointer;display:flex;align-items:center;gap:6px;font-size:12px;font-weight:500;color:var(--text2);transition:all 0.18s;white-space:nowrap;flex-shrink:0}
.s-btn:hover{border-color:var(--accent);color:var(--text)}
.s-btn.active{background:rgba(124,111,255,0.15);border-color:var(--accent);color:var(--accent2);font-weight:600}

.chat-area{flex:1;overflow-y:auto;padding:20px;display:flex;flex-direction:column;gap:14px;scroll-behavior:smooth}
.welcome-s{text-align:center;padding:40px 20px;color:var(--text2)}
.w-icon{font-size:44px;margin-bottom:10px}
.welcome-s h2{font-size:18px;font-weight:700;color:var(--text);margin-bottom:6px}
.welcome-s p{font-size:13px;line-height:1.6}

.msg{display:flex;gap:10px;align-items:flex-start;animation:fadeIn 0.22s ease}
.msg.user{flex-direction:row-reverse}
@keyframes fadeIn{from{opacity:0;transform:translateY(7px)}to{opacity:1;transform:translateY(0)}}
.av{width:34px;height:34px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:700;flex-shrink:0}
.av.ai{background:linear-gradient(135deg,var(--accent),var(--accent3));color:#fff}
.av.user{background:linear-gradient(135deg,var(--pink),var(--accent2));color:#fff}
.bubble{max-width:74%;padding:11px 15px;border-radius:16px;font-size:14px;line-height:1.68;color:var(--text)}
.msg.ai .bubble{background:var(--card);border:1px solid var(--border);border-bottom-left-radius:4px}
.msg.user .bubble{background:linear-gradient(135deg,rgba(124,111,255,0.25),rgba(167,139,250,0.15));border:1px solid rgba(124,111,255,0.25);border-bottom-right-radius:4px}
.bubble img{max-width:100%;border-radius:10px;margin-top:8px;display:block}
.bubble video{max-width:100%;border-radius:10px;margin-top:8px;display:block}
.loading-dots span{display:inline-block;width:6px;height:6px;border-radius:50%;background:var(--accent2);margin:0 2px;animation:blink 1.2s infinite}
.loading-dots span:nth-child(2){animation-delay:0.2s}
.loading-dots span:nth-child(3){animation-delay:0.4s}
@keyframes blink{0%,80%,100%{opacity:0.2}40%{opacity:1}}

.quick-area{padding:6px 20px 0;display:flex;flex-wrap:wrap;gap:5px}
.q-btn{font-size:11px;padding:5px 12px;border-radius:999px;border:1px solid var(--border);background:var(--card);cursor:pointer;color:var(--text2);transition:all 0.15s}
.q-btn:hover{border-color:var(--accent);color:var(--accent2);background:rgba(124,111,255,0.08)}

.media-preview{padding:6px 20px 0;display:flex;flex-wrap:wrap;gap:7px}
.m-thumb{position:relative;border-radius:10px;overflow:hidden;border:1px solid var(--border)}
.m-thumb img,.m-thumb video{width:72px;height:72px;object-fit:cover;display:block}
.m-del{position:absolute;top:3px;right:3px;background:rgba(0,0,0,0.65);border:none;color:#fff;width:17px;height:17px;border-radius:50%;cursor:pointer;font-size:9px;display:flex;align-items:center;justify-content:center}

.input-area{padding:12px 20px;border-top:1px solid var(--border);background:var(--bg2)}
.input-tools{display:flex;gap:6px;margin-bottom:8px}
.t-btn{background:var(--card);border:1px solid var(--border);border-radius:8px;padding:6px 12px;cursor:pointer;color:var(--text2);font-size:11px;display:flex;align-items:center;gap:5px;transition:all 0.15s}
.t-btn:hover{border-color:var(--accent);color:var(--accent2)}
.t-btn input{display:none}
.input-row{display:flex;gap:8px;align-items:flex-end}
.input-row textarea{flex:1;font-size:13px;border-radius:12px;border:1.5px solid var(--border);padding:11px 14px;outline:none;background:var(--card);color:var(--text);resize:none;min-height:44px;max-height:110px;font-family:'Inter',sans-serif;line-height:1.5;transition:border-color 0.15s}
.input-row textarea:focus{border-color:var(--accent)}
.input-row textarea::placeholder{color:var(--text3)}
.send-b{padding:11px 18px;border-radius:12px;border:none;background:linear-gradient(135deg,var(--accent),var(--accent3));color:#fff;cursor:pointer;font-size:13px;font-weight:700;display:flex;align-items:center;gap:5px;white-space:nowrap;transition:all 0.15s}
.send-b:hover{opacity:0.9;transform:translateY(-1px)}
.send-b:disabled{background:var(--card2);color:var(--text3);cursor:not-allowed;transform:none}

.overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.55);z-index:99}
@media(max-width:680px){
  .sidebar{position:fixed;left:0;top:0;bottom:0;z-index:100;transform:translateX(-100%)}
  .sidebar.open{transform:translateX(0)}
  .menu-btn{display:block}
  .overlay.show{display:block}
}
</style>
</head>
<body>

<!-- ===== LOGIN PAGE ===== -->
<div id="login-page">
<div class="auth-wrap">
  <div class="auth-card">
    <div class="auth-logo">
      <div class="logo-icon">🎓</div>
      <h1>Baxodir AI</h1>
      <p>Ko'p fanli AI o'qituvchi</p>
    </div>

    <div class="auth-tabs">
      <button class="auth-tab active" onclick="switchTab('login')">Kirish</button>
      <button class="auth-tab" onclick="switchTab('register')">Ro'yxatdan o'tish</button>
    </div>

    <div id="msg-box" class="msg-box"></div>

    <!-- SOCIAL -->
    <div class="social-btns">
      <button class="social-btn" onclick="socialLogin('google')">
        <svg viewBox="0 0 24 24"><path fill="#4285F4" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/><path fill="#34A853" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/><path fill="#FBBC05" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z"/><path fill="#EA4335" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z"/></svg>
        Google bilan kirish
      </button>
      <button class="social-btn" onclick="socialLogin('apple')">
        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M18.71 19.5c-.83 1.24-1.71 2.45-3.05 2.47-1.34.03-1.77-.79-3.29-.79-1.53 0-2 .77-3.27.82-1.31.05-2.3-1.32-3.14-2.53C4.25 17 2.94 12.45 4.7 9.39c.87-1.52 2.43-2.48 4.12-2.51 1.28-.02 2.5.87 3.29.87.78 0 2.26-1.07 3.8-.91.65.03 2.47.26 3.64 1.98-.09.06-2.17 1.28-2.15 3.81.03 3.02 2.65 4.03 2.68 4.04-.03.07-.42 1.44-1.38 2.83M13 3.5c.73-.83 1.94-1.46 2.94-1.5.13 1.17-.34 2.35-1.04 3.19-.69.85-1.83 1.51-2.95 1.42-.15-1.15.41-2.35 1.05-3.11z"/></svg>
        Apple bilan kirish
      </button>
    </div>

    <div class="divider">yoki</div>

    <!-- LOGIN FORM -->
    <div id="login-form">
      <div class="form-group">
        <label class="form-label">Email</label>
        <input class="form-input" type="email" id="login-email" placeholder="email@gmail.com">
      </div>
      <div class="form-group">
        <label class="form-label">Parol</label>
        <input class="form-input" type="password" id="login-pass" placeholder="••••••••" onkeydown="if(event.key==='Enter')doLogin()">
      </div>
      <div class="form-row">
        <label class="checkbox-wrap">
          <input type="checkbox" id="remember-me" checked>
          <span>Eslab qol</span>
        </label>
        <a class="forgot-link" onclick="showForgot()">Parolni unutdim?</a>
      </div>
      <button class="auth-btn" onclick="doLogin()">Kirish</button>
      <div class="auth-footer">Hisob yo'qmi? <a onclick="switchTab('register')">Ro'yxatdan o'tish</a></div>
    </div>

    <!-- REGISTER FORM -->
    <div id="register-form" style="display:none">
      <div class="form-group">
        <label class="form-label">Ism familiya</label>
        <input class="form-input" type="text" id="reg-name" placeholder="Baxodir Rahimov">
      </div>
      <div class="form-group">
        <label class="form-label">Email</label>
        <input class="form-input" type="email" id="reg-email" placeholder="email@gmail.com">
      </div>
      <div class="form-group">
        <label class="form-label">Parol</label>
        <input class="form-input" type="password" id="reg-pass" placeholder="Kamida 6 ta belgi" onkeydown="if(event.key==='Enter')doRegister()">
      </div>
      <button class="auth-btn" onclick="doRegister()">Ro'yxatdan o'tish</button>
      <div class="auth-footer">Hisobingiz bormi? <a onclick="switchTab('login')">Kirish</a></div>
    </div>

    <div class="terms">
      Davom etish orqali siz <a>Foydalanish shartlari</a> va <a>Maxfiylik siyosati</a>ga rozilik bildirasiz.
    </div>
  </div>
</div>
</div>

<!-- ===== MAIN APP ===== -->
<div id="app">
<div class="layout">
  <div class="overlay" id="overlay" onclick="closeSB()"></div>

  <div class="sidebar" id="sidebar">
    <div class="logo-wrap">
      <h1>🎓 Baxodir AI</h1>
      <span>Ko'p fanli AI o'qituvchi</span>
    </div>
    <div class="sb-section">
      <button class="new-btn" onclick="newChat()">✏️ Yangi suhbat</button>
      <div class="sb-label">So'nggi suhbatlar</div>
      <div class="recents-list" id="recents-list"><div class="no-rec">Hali suhbat yo'q</div></div>
    </div>
    <div class="sb-bottom"><div class="ver">⚡ Baxodir AI v2.0</div></div>
  </div>

  <div class="main">
    <div class="topnav">
      <button class="menu-btn" onclick="toggleSB()">☰</button>
      <div class="nav-title" id="nav-title">🇬🇧 Ingliz tili</div>
      <div class="online-b"><span class="online-dot"></span> Online</div>
      <div style="position:relative">
        <div class="user-chip" id="user-chip" onclick="toggleDD()">
          <div class="uc-avatar" id="uc-av">B</div>
          <span class="uc-name" id="uc-name">Foydalanuvchi</span>
        </div>
        <div class="user-dropdown" id="user-dd" style="display:none">
          <div class="ud-item" onclick="openProfile()">👤 Profil</div>
          <div class="ud-sep"></div>
          <div class="ud-item danger" onclick="doLogout()">🚪 Chiqish</div>
        </div>
      </div>
    </div>

    <div class="subjects-bar">
      <div class="subjects">
        <button class="s-btn active" data-id="english" onclick="selSub(this)"><span>🇬🇧</span> Ingliz tili</button>
        <button class="s-btn" data-id="math" onclick="selSub(this)"><span>📐</span> Matematika</button>
        <button class="s-btn" data-id="chinese" onclick="selSub(this)"><span>🇨🇳</span> Xitoy tili</button>
        <button class="s-btn" data-id="physics" onclick="selSub(this)"><span>⚛️</span> Fizika</button>
        <button class="s-btn" data-id="medicine" onclick="selSub(this)"><span>🏥</span> Medetsina</button>
        <button class="s-btn" data-id="history" onclick="selSub(this)"><span>🏛️</span> Tarix</button>
      </div>
    </div>

    <div class="chat-area" id="chat-area">
      <div class="welcome-s">
        <div class="w-icon">🎓</div>
        <h2>Baxodir AI ga xush kelibsiz!</h2>
        <p>Fan tanlang va savolingizni yozing.<br>Rasm yoki video ham yuborishingiz mumkin.</p>
      </div>
    </div>

    <div class="quick-area" id="quick-area"></div>
    <div class="media-preview" id="media-preview"></div>

    <div class="input-area">
      <div class="input-tools">
        <label class="t-btn">🖼️ Rasm<input type="file" accept="image/*" multiple onchange="handleMedia(event,'image')"></label>
        <label class="t-btn">🎬 Video<input type="file" accept="video/*" onchange="handleMedia(event,'video')"></label>
      </div>
      <div class="input-row">
        <textarea id="user-input" placeholder="Savolingizni yozing..." rows="1" onkeydown="handleKey(event)" oninput="autoResize(this)"></textarea>
        <button class="send-b" onclick="sendMsg()" id="send-btn">➤ Yuborish</button>
      </div>
    </div>
  </div>
</div>
</div>

<script>
// ===== AUTH =====
const USERS_KEY = 'baxodir_users';
const SESSION_KEY = 'baxodir_session';

function getUsers(){ return JSON.parse(localStorage.getItem(USERS_KEY)||'[]'); }
function saveUsers(u){ localStorage.setItem(USERS_KEY, JSON.stringify(u)); }
function getSession(){ return JSON.parse(localStorage.getItem(SESSION_KEY)||'null'); }
function setSession(u){ localStorage.setItem(SESSION_KEY, JSON.stringify(u)); }
function clearSession(){ localStorage.removeItem(SESSION_KEY); }

function showMsg(text, type='error'){
  const b = document.getElementById('msg-box');
  b.textContent = text; b.className = 'msg-box '+type+' show';
  setTimeout(()=>b.classList.remove('show'), 3500);
}

function switchTab(t){
  document.querySelectorAll('.auth-tab').forEach((el,i)=>el.classList.toggle('active', (i===0&&t==='login')||(i===1&&t==='register')));
  document.getElementById('login-form').style.display = t==='login'?'block':'none';
  document.getElementById('register-form').style.display = t==='register'?'block':'none';
}

function doLogin(){
  const email = document.getElementById('login-email').value.trim();
  const pass = document.getElementById('login-pass').value;
  if(!email||!pass){showMsg('Email va parolni kiriting');return;}
  const users = getUsers();
  const user = users.find(u=>u.email===email && u.pass===pass);
  if(!user){showMsg('Email yoki parol noto\'g\'ri');return;}
  setSession(user);
  enterApp(user);
}

function doRegister(){
  const name = document.getElementById('reg-name').value.trim();
  const email = document.getElementById('reg-email').value.trim();
  const pass = document.getElementById('reg-pass').value;
  if(!name||!email||!pass){showMsg('Barcha maydonlarni to\'ldiring');return;}
  if(pass.length<6){showMsg('Parol kamida 6 ta belgi bo\'lishi kerak');return;}
  if(!/\S+@\S+\.\S+/.test(email)){showMsg('Email noto\'g\'ri formatda');return;}
  const users = getUsers();
  if(users.find(u=>u.email===email)){showMsg('Bu email allaqachon ro\'yxatdan o\'tgan');return;}
  const user = {id:Date.now(), name, email, pass, avatar:name[0].toUpperCase(), provider:'email'};
  users.push(user); saveUsers(users);
  setSession(user);
  showMsg('Muvaffaqiyatli ro\'yxatdan o\'tdingiz!','success');
  setTimeout(()=>enterApp(user), 800);
}

function socialLogin(provider){
  const providerName = provider==='google'?'Google':'Apple';
  const fakeName = provider==='google'?'Google Foydalanuvchi':'Apple Foydalanuvchi';
  const fakeEmail = provider==='google'?'user@gmail.com':'user@icloud.com';
  const users = getUsers();
  let user = users.find(u=>u.email===fakeEmail && u.provider===provider);
  if(!user){
    user = {id:Date.now(), name:fakeName, email:fakeEmail, pass:'', avatar:providerName[0], provider};
    users.push(user); saveUsers(users);
  }
  setSession(user);
  enterApp(user);
}

function showForgot(){
  const email = document.getElementById('login-email').value.trim();
  if(!email){showMsg('Avval emailingizni kiriting');return;}
  const users = getUsers();
  const user = users.find(u=>u.email===email);
  if(!user){showMsg('Bu email topilmadi');return;}
  showMsg('Parol: '+user.pass+' (demo rejim)','success');
}

function doLogout(){
  clearSession(); location.reload();
}

function enterApp(user){
  document.getElementById('login-page').style.display='none';
  document.getElementById('app').style.display='block';
  document.getElementById('uc-name').textContent = user.name.split(' ')[0];
  document.getElementById('uc-av').textContent = user.avatar||user.name[0].toUpperCase();
  renderRecents();
  updateQuick();
}

function toggleDD(){
  const dd = document.getElementById('user-dd');
  dd.style.display = dd.style.display==='none'?'block':'none';
}
document.addEventListener('click', e=>{
  if(!e.target.closest('#user-chip')&&!e.target.closest('#user-dd'))
    document.getElementById('user-dd').style.display='none';
});
function openProfile(){
  const u = getSession();
  if(u) alert('👤 Profil\n\nIsm: '+u.name+'\nEmail: '+u.email+'\nKirish usuli: '+u.provider);
  document.getElementById('user-dd').style.display='none';
}

// Check session on load
window.addEventListener('DOMContentLoaded',()=>{
  const s = getSession();
  if(s) enterApp(s);
});

// ===== SUBJECTS =====
const subjects = {
  english:{name:"Ingliz tili",emoji:"🇬🇧",system:"Sen ingliz tili o'qituvchisisn. O'zbek tilida javob ber.",quick:["Grammar nima?","Present Perfect misollar","5 ta yangi so'z"]},
  math:{name:"Matematika",emoji:"📐",system:"Sen matematika o'qituvchisisn. O'zbek tilida javob ber. Misollarni bosqichma-bosqich yech.",quick:["2x+5=13 ni yech","Kvadrat tenglama","Pitagor teoremasi"]},
  chinese:{name:"Xitoy tili",emoji:"🇨🇳",system:"Sen xitoy tili o'qituvchisisn. O'zbek tilida javob ber. Xitoy harflari va pinyinni ko'rsat.",quick:["Salom xitoycha","Sonlarni o'rgat","O'zingni tanishtir"]},
  physics:{name:"Fizika",emoji:"⚛️",system:"Sen fizika o'qituvchisisn. O'zbek tilida javob ber. Formulalar va masalalarni tushuntir.",quick:["Newton 2-qonuni","Ohm qonuni","v=20 t=5 yo'l topi"]},
  medicine:{name:"Medetsina",emoji:"🏥",system:"Sen tibbiyot yordamchisisn. O'zbek tilida javob ber. Kasalliklar, simptomlar haqida tushuntir. Bu professional tibbiy maslahat emas deb eslatib tur.",quick:["Gripp alomatlari","Qon bosimi","Vitamin D nima uchun?"]},
  history:{name:"Tarix",emoji:"🏛️",system:"Sen tarix o'qituvchisisn. O'zbek tilida javob ber.",quick:["Amir Temur kim?","Ipak yo'li","O'zbekiston mustaqilligi"]}
};

let curSub='english', chatHist=[], pendMedia=[];
const RECENTS_KEY='baxodir_recents_v2';
let allRecents=JSON.parse(localStorage.getItem(RECENTS_KEY)||'[]');

function renderRecents(){
  const list=document.getElementById('recents-list');
  if(!allRecents.length){list.innerHTML='<div class="no-rec">Hali suhbat yo\'q</div>';return;}
  list.innerHTML=allRecents.slice().reverse().map((r,i)=>`
    <div class="r-item" onclick="loadRecent(${allRecents.length-1-i})">
      <span class="r-ico">${subjects[r.subject]?.emoji||'💬'}</span>
      <div class="r-body"><div class="r-title">${r.title}</div><div class="r-sub">${subjects[r.subject]?.name||''} · ${r.date}</div></div>
      <span class="r-del" onclick="event.stopPropagation();delRecent(${allRecents.length-1-i})">✕</span>
    </div>`).join('');
}

function saveRecent(){
  if(!chatHist.length) return;
  const fu=chatHist.find(m=>m.role==='user');
  if(!fu) return;
  const t=typeof fu.content==='string'?fu.content:(fu.content.find?.(c=>c.type==='text')?.text||'Suhbat');
  const date=new Date().toLocaleDateString('uz-UZ',{month:'short',day:'numeric'});
  allRecents.push({subject:curSub,title:t.slice(0,38),date,history:chatHist,html:document.getElementById('chat-area').innerHTML});
  if(allRecents.length>30) allRecents.shift();
  localStorage.setItem(RECENTS_KEY,JSON.stringify(allRecents));
  renderRecents();
}

function loadRecent(i){
  const r=allRecents[i];if(!r)return;
  curSub=r.subject;chatHist=r.history||[];
  document.querySelectorAll('.s-btn').forEach(b=>b.classList.toggle('active',b.dataset.id===curSub));
  document.getElementById('nav-title').textContent=(subjects[curSub]?.emoji||'')+' '+(subjects[curSub]?.name||'');
  document.getElementById('chat-area').innerHTML=r.html||'';
  updateQuick();closeSB();
}

function delRecent(i){allRecents.splice(i,1);localStorage.setItem(RECENTS_KEY,JSON.stringify(allRecents));renderRecents();}

function newChat(){if(chatHist.length)saveRecent();chatHist=[];pendMedia=[];document.getElementById('media-preview').innerHTML='';document.getElementById('chat-area').innerHTML='<div class="welcome-s"><div class="w-icon">🎓</div><h2>Yangi suhbat</h2><p>Savolingizni yozing!</p></div>';closeSB();}

function selSub(btn){
  if(chatHist.length)saveRecent();chatHist=[];
  document.querySelectorAll('.s-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');curSub=btn.dataset.id;
  const s=subjects[curSub];
  document.getElementById('nav-title').textContent=s.emoji+' '+s.name;
  document.getElementById('chat-area').innerHTML=`<div class="welcome-s"><div class="w-icon">${s.emoji}</div><h2>${s.name}</h2><p>Savolingizni yozing yoki quyidagi mavzulardan birini tanlang.</p></div>`;
  updateQuick();
}

function updateQuick(){
  const s=subjects[curSub];
  document.getElementById('quick-area').innerHTML=(s.quick||[]).map(q=>`<button class="q-btn" onclick="quickAsk(this)">${q}</button>`).join('');
}

function quickAsk(btn){document.getElementById('user-input').value=btn.textContent;sendMsg();}
function autoResize(el){el.style.height='auto';el.style.height=Math.min(el.scrollHeight,110)+'px';}
function handleKey(e){if(e.key==='Enter'&&!e.shiftKey){e.preventDefault();sendMsg();}}

function handleMedia(e,type){
  Array.from(e.target.files).forEach(file=>{
    const r=new FileReader();
    r.onload=ev=>{pendMedia.push({type,file,dataUrl:ev.target.result});renderMediaPrev();};
    r.readAsDataURL(file);
  });e.target.value='';
}

function renderMediaPrev(){
  document.getElementById('media-preview').innerHTML=pendMedia.map((m,i)=>`
    <div class="m-thumb">
      ${m.type==='image'?`<img src="${m.dataUrl}">`:`<video src="${m.dataUrl}"></video>`}
      <button class="m-del" onclick="removeMedia(${i})">✕</button>
    </div>`).join('');
}

function removeMedia(i){pendMedia.splice(i,1);renderMediaPrev();}

function addMsg(role,text,media){
  const area=document.getElementById('chat-area');
  area.querySelector('.welcome-s')?.remove();
  const d=document.createElement('div');d.className='msg '+role;
  const mediaHtml=(media||[]).map(m=>m.type==='image'?`<img src="${m.dataUrl}">`:`<video src="${m.dataUrl}" controls>`).join('');
  d.innerHTML=`<div class="av ${role}">${role==='ai'?'B':'S'}</div><div class="bubble">${text}${mediaHtml}</div>`;
  area.appendChild(d);area.scrollTop=area.scrollHeight;return d;
}

async function sendMsg(){
  const inp=document.getElementById('user-input');
  const btn=document.getElementById('send-btn');
  const text=inp.value.trim();
  if(!text&&!pendMedia.length)return;
  const media=[...pendMedia];pendMedia=[];document.getElementById('media-preview').innerHTML='';
  addMsg('user',text||'📎 Media',media);
  inp.value='';inp.style.height='auto';btn.disabled=true;

  let content;
  if(media.length){
    content=[];
    media.forEach(m=>{if(m.type==='image'){const b64=m.dataUrl.split(',')[1];content.push({type:'image',source:{type:'base64',media_type:m.file.type||'image/jpeg',data:b64}});}});
    content.push({type:'text',text:text||'Bu rasmdagi nima? Tushuntir.'});
  } else {content=text;}
  chatHist.push({role:'user',content});

  const area=document.getElementById('chat-area');
  const ld=document.createElement('div');ld.className='msg ai';
  ld.innerHTML=`<div class="av ai">B</div><div class="bubble"><div class="loading-dots"><span></span><span></span><span></span></div></div>`;
  area.appendChild(ld);area.scrollTop=area.scrollHeight;

  try{
    const res=await fetch('https://api.anthropic.com/v1/messages',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({model:'claude-sonnet-4-6',max_tokens:1000,system:subjects[curSub].system,messages:chatHist})});
    const data=await res.json();
    const reply=(data.content||[]).map(c=>c.text||'').join('');
    chatHist.push({role:'assistant',content:reply});
    ld.remove();addMsg('ai',reply.replace(/\n/g,'<br>'));
  }catch(e){ld.remove();addMsg('ai','❌ Xatolik yuz berdi.');}
  btn.disabled=false;inp.focus();
}

function toggleSB(){document.getElementById('sidebar').classList.toggle('open');document.getElementById('overlay').classList.toggle('show');}
function closeSB(){document.getElementById('sidebar').classList.remove('open');document.getElementById('overlay').classList.remove('show');}
</script>
</body>
</html>
