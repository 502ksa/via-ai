<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Via AI</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800;900&display=swap');
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
:root{
  --bg:#09090b;--s1:#121218;--s2:#181825;--s3:#1f1f30;
  --border:rgba(255,255,255,0.05);--border2:rgba(255,255,255,0.09);
  --p:#8b5cf6;--p2:#a78bfa;--pg:rgba(139,92,246,0.15);--pg2:rgba(139,92,246,0.05);
  --text:#f4f4f5;--t2:#a1a1aa;--t3:#71717a;
  --green:#10b981;--red:#ef4444;--glow:rgba(139,92,246,0.2);
}
[data-theme="light"]{
  --bg:#f8fafc;--s1:#ffffff;--s2:#f1f5f9;--s3:#e2e8f0;
  --border:rgba(0,0,0,0.04);--border2:rgba(0,0,0,0.08);
  --p:#6d28d9;--p2:#8b5cf6;--pg:rgba(109,40,217,0.08);--pg2:rgba(109,40,217,0.03);
  --text:#0f172a;--t2:#475569;--t3:#94a3b8;--green:#059669;--red:#dc2626;--glow:rgba(109,40,217,0.05);
}
html,body{height:100%;font-family:'Cairo',sans-serif;background:var(--bg);color:var(--text);overflow:hidden;transition:background 0.3s,color 0.3s}

/* GATE */
#gate{position:fixed;inset:0;z-index:9999;background:var(--bg);display:flex;align-items:center;justify-content:center;padding:20px}
.gate-card{width:100%;max-width:460px;background:var(--s1);border:1px solid var(--border2);border-radius:24px;padding:50px 40px;text-align:center;box-shadow:0 25px 50px -12px rgba(0,0,0,0.5);position:relative;overflow:hidden}
.gate-card::before{content:'';position:absolute;top:0;left:50%;transform:translateX(-50%);width:150px;height:1px;background:linear-gradient(90deg,transparent,var(--p),transparent)}
.gate-logo{width:64px;height:64px;background:linear-gradient(135deg,var(--s2),var(--s3));border:1px solid var(--border2);border-radius:20px;display:flex;align-items:center;justify-content:center;margin:0 auto 24px;color:var(--p);font-weight:900;font-size:22px}
.gate-title{font-size:28px;font-weight:900;margin-bottom:10px}
.gate-title span{background:linear-gradient(135deg,var(--p),#c4b5fd);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.gate-sub{font-size:13px;color:var(--t2);margin-bottom:32px;line-height:1.8}
.inp-wrap{position:relative;margin-bottom:20px}
.inp-wrap input{width:100%;background:var(--s2);border:1px solid var(--border2);border-radius:14px;padding:16px 48px 16px 20px;font-family:'Cairo',sans-serif;font-size:14px;color:var(--text);direction:ltr;outline:none;transition:all 0.3s}
.inp-wrap input:focus{border-color:var(--p);box-shadow:0 0 20px var(--glow)}
.inp-wrap input::placeholder{color:var(--t3)}
.eye{position:absolute;left:16px;top:50%;transform:translateY(-50%);background:none;border:none;cursor:pointer;color:var(--t3);font-size:16px}
.gate-hint{font-size:12px;color:var(--t3);margin-bottom:22px;line-height:1.7}
.gate-hint a{color:var(--p);text-decoration:none}
.gate-err{background:rgba(239,68,68,0.1);border:1px solid rgba(239,68,68,0.3);border-radius:10px;padding:10px 14px;color:var(--red);font-size:13px;margin-bottom:14px;display:none}
.gate-btn{width:100%;background:var(--p);border:none;border-radius:14px;padding:16px;color:white;font-family:'Cairo',sans-serif;font-size:15px;font-weight:700;cursor:pointer;transition:all 0.2s;box-shadow:0 4px 20px var(--glow)}
.gate-btn:hover{background:var(--p2);transform:translateY(-1px)}

/* APP */
#app{display:none;height:100vh;flex-direction:column;overflow:hidden}
#app.show{display:flex}

/* TOPNAV */
.topnav{background:var(--s1);border-bottom:1px solid var(--border);padding:0 20px;height:60px;display:flex;align-items:center;justify-content:space-between;flex-shrink:0;z-index:50;position:relative}
.nav-logo{display:flex;align-items:center;gap:10px}
.nav-logo-icon{width:30px;height:30px;background:var(--s2);border:1px solid var(--border2);border-radius:8px;display:flex;align-items:center;justify-content:center;color:var(--p);font-weight:900;font-size:13px}
.nav-logo-text{font-size:17px;font-weight:900}
.nav-logo-text span{color:var(--p)}
.nav-right-btns{display:flex;align-items:center;gap:8px}
.icon-btn{width:36px;height:36px;background:var(--s2);border:1px solid var(--border2);border-radius:9px;display:flex;align-items:center;justify-content:center;cursor:pointer;font-size:15px;transition:all 0.2s;flex-shrink:0}
.icon-btn:hover{border-color:var(--p);background:var(--pg2)}
.hbtn{width:36px;height:36px;background:transparent;border:none;display:flex;flex-direction:column;gap:4px;cursor:pointer;align-items:center;justify-content:center;flex-shrink:0;display:none}
.hbtn span{width:18px;height:2px;background:var(--text);border-radius:2px;transition:all 0.25s;display:block}
.hbtn.open span:nth-child(1){transform:rotate(45deg) translate(4px,4px)}
.hbtn.open span:nth-child(2){opacity:0}
.hbtn.open span:nth-child(3){transform:rotate(-45deg) translate(4px,-4px)}

/* BODY */
.app-body{display:flex;flex:1;overflow:hidden;position:relative}

/* SIDEBAR */
.sidebar{width:250px;min-width:250px;background:var(--s1);border-left:1px solid var(--border);overflow-y:auto;flex-shrink:0;padding:12px 0 20px;transition:transform 0.28s cubic-bezier(0.4,0,0.2,1)}
.sidebar::-webkit-scrollbar{width:3px}
.sidebar::-webkit-scrollbar-thumb{background:var(--border2);border-radius:3px}
.nav-sec{font-size:10px;font-weight:700;color:var(--t3);text-transform:uppercase;letter-spacing:1.5px;padding:16px 20px 6px}
.nav-item{display:flex;align-items:center;gap:12px;padding:11px 20px;cursor:pointer;font-size:13.5px;font-weight:600;color:var(--t2);transition:all 0.15s;border-right:3px solid transparent;user-select:none}
.nav-item:hover{background:var(--pg2);color:var(--text)}
.nav-item.active{background:var(--pg);color:var(--p);border-right-color:var(--p);font-weight:700}
.nav-item .ni{width:28px;height:28px;border-radius:7px;display:flex;align-items:center;justify-content:center;background:var(--s2);font-size:14px;flex-shrink:0;transition:all 0.15s}
.nav-item.active .ni{background:var(--p);color:#fff}

/* OVERLAY */
.overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.6);z-index:45;backdrop-filter:blur(3px)}
.overlay.show{display:block}

/* CONTENT */
.content{flex:1;overflow:hidden;display:flex;flex-direction:column;background:var(--bg)}

/* PAGES */
.page{display:none;flex:1;overflow:hidden;flex-direction:column}
.page.active{display:flex}

/* HOME */
.home-scroll{flex:1;overflow-y:auto;padding:28px 24px}
.home-scroll::-webkit-scrollbar{width:5px}
.home-scroll::-webkit-scrollbar-thumb{background:var(--border2);border-radius:5px}
.home-hero{background:linear-gradient(135deg,var(--s1),var(--s2));border:1px solid var(--border2);border-radius:20px;padding:32px;margin-bottom:28px;position:relative;overflow:hidden}
.home-hero::after{content:'';position:absolute;top:-50%;right:-20%;width:60%;height:200%;background:radial-gradient(circle,var(--glow),transparent 70%);pointer-events:none}
.home-hero h1{font-size:24px;font-weight:900;margin-bottom:8px}
.home-hero h1 span{color:var(--p)}
.home-hero p{font-size:13.5px;color:var(--t2);line-height:1.8;max-width:500px}
.sec-h{font-size:13px;font-weight:800;color:var(--text);margin:24px 0 14px;padding-right:10px;border-right:3px solid var(--p)}
.tgrid{display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:12px;margin-bottom:8px}
.tbtn{background:var(--s1);border:1px solid var(--border);border-radius:16px;padding:20px;cursor:pointer;transition:all 0.22s;text-align:right}
.tbtn:hover{border-color:var(--p);background:var(--s2);transform:translateY(-2px);box-shadow:0 8px 20px rgba(0,0,0,0.15)}
.tbtn:active{transform:translateY(0)}
.tbtn .ti{font-size:20px;margin-bottom:12px;background:var(--pg);width:38px;height:38px;border-radius:10px;display:flex;align-items:center;justify-content:center}
.tbtn .tn{font-size:13.5px;font-weight:700;margin-bottom:4px}
.tbtn .td{font-size:11.5px;color:var(--t2);line-height:1.5}

/* KEY LAYOUT - CRITICAL FIX */
/* الـ tool-layout يملأ المساحة المتبقية بالكامل */
.tool-layout{display:flex;flex:1;overflow:hidden;height:100%}

/* الفورم: scroll مستقل تماماً، بحيث الزر دائماً وصال */
.tool-form-side{
  width:360px;min-width:300px;
  border-left:1px solid var(--border);
  display:flex;flex-direction:column; /* flex column مهم */
  overflow:hidden; /* لا scroll هنا */
  flex-shrink:0;background:var(--bg);
}
.form-inner{
  flex:1;overflow-y:auto; /* scroll هنا فقط */
  padding:24px 20px 0;
}
.form-inner::-webkit-scrollbar{width:4px}
.form-inner::-webkit-scrollbar-thumb{background:var(--border2);border-radius:4px}
.form-footer{
  padding:16px 20px 20px;
  background:var(--bg);
  border-top:1px solid var(--border);
  flex-shrink:0; /* لا يضغط */
}

/* الشات: scroll مستقل */
.tool-chat-side{flex:1;display:flex;flex-direction:column;overflow:hidden;background:var(--s1)}

.tool-header{margin-bottom:20px}
.tool-header h2{font-size:18px;font-weight:800;margin-bottom:4px}
.tool-header p{font-size:12.5px;color:var(--t2);line-height:1.6}
.field{margin-bottom:14px}
.field label{display:block;font-size:11px;font-weight:700;color:var(--t3);text-transform:uppercase;letter-spacing:0.5px;margin-bottom:7px}
.field input,.field textarea,.field select{width:100%;background:var(--s2);border:1px solid var(--border2);border-radius:11px;padding:12px 14px;font-family:'Cairo',sans-serif;font-size:13.5px;color:var(--text);outline:none;transition:all 0.2s}
.field textarea{resize:vertical;min-height:85px;line-height:1.7}
.field input:focus,.field textarea:focus,.field select:focus{border-color:var(--p);box-shadow:0 0 10px var(--glow);background:var(--s3)}
.field input::placeholder,.field textarea::placeholder{color:var(--t3)}
.row2{display:flex;gap:10px}
.row2 .field{flex:1}
.tool-err{background:rgba(239,68,68,0.1);border:1px solid rgba(239,68,68,0.25);border-radius:9px;padding:9px 13px;color:var(--red);font-size:12.5px;margin-bottom:10px;display:none}
.run-btn{width:100%;background:var(--p);border:none;border-radius:11px;padding:14px;color:white;font-family:'Cairo',sans-serif;font-size:14.5px;font-weight:700;cursor:pointer;transition:all 0.2s;box-shadow:0 4px 16px var(--glow)}
.run-btn:hover{background:var(--p2);transform:translateY(-1px)}
.run-btn:active{transform:translateY(0)}
.run-btn:disabled{opacity:0.5;cursor:not-allowed;transform:none}

/* CHAT */
.chat-msgs{flex:1;overflow-y:auto;padding:20px;display:flex;flex-direction:column;gap:14px}
.chat-msgs::-webkit-scrollbar{width:5px}
.chat-msgs::-webkit-scrollbar-thumb{background:var(--border2);border-radius:5px}
.chat-empty{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;color:var(--t3);text-align:center;padding:30px}
.chat-empty .ce{font-size:32px;margin-bottom:12px;opacity:0.4}
.chat-empty p{font-size:13px;line-height:1.7}

.msg{max-width:86%;display:flex;flex-direction:column;animation:fu 0.25s ease}
@keyframes fu{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}
.msg.ai{align-self:flex-start}
.msg.user{align-self:flex-end;align-items:flex-end}
.msg-label{font-size:10px;color:var(--t3);margin-bottom:4px;font-weight:700;padding:0 3px}
.msg-bubble{padding:13px 16px;border-radius:16px;font-size:13.5px;line-height:1.85;white-space:pre-wrap;word-break:break-word}
.msg.ai .msg-bubble{background:var(--s2);border:1px solid var(--border2);border-radius:4px 16px 16px 16px}
.msg.user .msg-bubble{background:var(--p);color:white;border-radius:16px 4px 16px 16px}

/* زر النسخ ثابت ومرئي دائماً */
.msg-actions{display:flex;gap:8px;margin-top:8px;flex-wrap:wrap}
.mcopy{background:var(--s2);border:1px solid var(--border2);border-radius:8px;padding:6px 14px;font-family:'Cairo',sans-serif;font-size:12px;color:var(--t2);cursor:pointer;transition:all 0.2s;font-weight:600}
.mcopy:hover{border-color:var(--p);color:var(--p)}
.mcopy.ok{border-color:var(--green);color:var(--green);background:rgba(16,185,129,0.08)}

/* TYPING */
.typing{display:flex;gap:5px;align-items:center;background:var(--s2);border:1px solid var(--border2);border-radius:4px 16px 16px 16px;padding:14px 18px;width:fit-content}
.td{width:7px;height:7px;background:var(--p);border-radius:50%;animation:bo 1.1s infinite}
.td:nth-child(2){animation-delay:0.18s}
.td:nth-child(3){animation-delay:0.36s}
@keyframes bo{0%,80%,100%{transform:translateY(0)}40%{transform:translateY(-7px)}}

/* CHAT BAR */
.chat-bar{border-top:1px solid var(--border);padding:12px 16px;background:var(--s1);display:flex;gap:10px;align-items:flex-end;flex-shrink:0}
.chat-bar textarea{flex:1;background:var(--s2);border:1px solid var(--border2);border-radius:12px;padding:11px 14px;font-family:'Cairo',sans-serif;font-size:13.5px;color:var(--text);resize:none;outline:none;max-height:100px;min-height:42px;line-height:1.5;transition:border-color 0.2s}
.chat-bar textarea:focus{border-color:var(--p)}
.chat-bar textarea::placeholder{color:var(--t3)}
.send{width:42px;height:42px;min-width:42px;background:var(--p);border:none;border-radius:11px;cursor:pointer;display:flex;align-items:center;justify-content:center;color:white;font-size:16px;transition:all 0.2s;flex-shrink:0}
.send:hover{background:var(--p2);transform:scale(1.04)}
.send:active{transform:scale(0.95)}
.send:disabled{opacity:0.4;cursor:not-allowed;transform:none}

/* STREAMING cursor */
.streaming-cursor{display:inline-block;width:2px;height:1em;background:var(--p);margin-right:2px;animation:blink 1s step-end infinite;vertical-align:text-bottom}
@keyframes blink{0%,100%{opacity:1}50%{opacity:0}}

/* SETTINGS */
.settings-scroll{flex:1;overflow-y:auto;padding:28px 24px}
.settings-scroll::-webkit-scrollbar{width:5px}
.settings-scroll::-webkit-scrollbar-thumb{background:var(--border2);border-radius:5px}
.settings-card{background:var(--s1);border:1px solid var(--border);border-radius:18px;padding:24px;margin-bottom:18px}
.settings-card h3{font-size:15px;font-weight:800;margin-bottom:16px;display:flex;align-items:center;gap:8px}
.theme-btns{display:flex;gap:10px}
.theme-btn{flex:1;padding:13px;border-radius:11px;border:1px solid var(--border2);background:var(--s2);color:var(--text);font-family:'Cairo',sans-serif;font-weight:700;cursor:pointer;transition:all 0.2s;font-size:13.5px}
.theme-btn.active{background:var(--p);color:#fff;border-color:var(--p)}

/* مؤشرات الإحصاء */
.stats-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-bottom:0}
.stat-card{background:var(--s2);border:1px solid var(--border2);border-radius:12px;padding:16px;text-align:center}
.stat-num{font-size:22px;font-weight:900;color:var(--p);margin-bottom:4px}
.stat-lbl{font-size:11px;color:var(--t3);font-weight:600}

/* الأرشيف */
.archive-list{display:flex;flex-direction:column;gap:12px;margin-top:14px}
.arch-item{background:var(--s2);border:1px solid var(--border2);border-radius:13px;padding:18px}
.arch-meta{display:flex;justify-content:space-between;font-size:11px;color:var(--t3);font-weight:700;text-transform:uppercase;margin-bottom:8px}
.arch-title{font-size:13.5px;font-weight:700;color:var(--text);margin-bottom:6px}
.arch-body{font-size:12.5px;color:var(--t2);line-height:1.6;max-height:60px;overflow:hidden;mask-image:linear-gradient(to bottom,black 60%,transparent 100%)}
.arch-actions{display:flex;gap:8px;margin-top:10px}
.a-btn{background:var(--s1);border:1px solid var(--border2);padding:5px 13px;border-radius:7px;font-size:12px;color:var(--t2);cursor:pointer;font-family:'Cairo';font-weight:600;transition:all 0.2s}
.a-btn:hover{border-color:var(--p);color:var(--text)}
.a-btn.del{color:var(--red)}
.a-btn.del:hover{background:rgba(239,68,68,0.06);border-color:var(--red)}
.empty-arch{font-size:13px;color:var(--t3);text-align:center;padding:24px}

/* RESPONSIVE */
@media(max-width:900px){
  .tool-form-side{width:100%;min-width:0;border-left:none;position:absolute;inset:0;z-index:10;background:var(--bg)}
  .tool-chat-side{position:absolute;inset:0;z-index:20;display:none}
  .tool-chat-side.mob-show{display:flex}
  .tool-layout{position:relative}
  .back-btn{display:flex!important}
}
@media(max-width:768px){
  .hbtn{display:flex}
  .sidebar{position:fixed;top:0;bottom:0;right:0;z-index:100;transform:translateX(100%);box-shadow:-10px 0 30px rgba(0,0,0,0.4)}
  .sidebar.open{transform:translateX(0)}
  .tgrid{grid-template-columns:1fr 1fr}
}
@media(max-width:480px){
  .tgrid{grid-template-columns:1fr}
  .home-scroll{padding:16px}
  .form-inner{padding:16px 14px 0}
  .form-footer{padding:12px 14px 16px}
}

/* زر الرجوع للجوال */
.back-btn{display:none;align-items:center;gap:8px;background:var(--s2);border:1px solid var(--border2);border-radius:10px;padding:9px 16px;font-family:'Cairo';font-size:13px;font-weight:700;color:var(--text);cursor:pointer;margin:16px 16px 0;width:fit-content;transition:all 0.2s}
.back-btn:hover{border-color:var(--p);color:var(--p)}
</style>
</head>
<body>

<!-- GATE -->
<div id="gate">
  <div class="gate-card">
    <div class="gate-logo">V</div>
    <h1 class="gate-title"><span>Via AI</span></h1>
    <p class="gate-sub">المنصة الذكية للجامعة والتوظيف والبريزنتيشن<br>أدخل Claude API Key للبدء</p>
    <div class="inp-wrap">
      <input type="password" id="gkey" placeholder="sk-ant-api03-..." autocomplete="off">
      <button class="eye" onclick="tEye()">👁</button>
    </div>
    <p class="gate-hint">من <a href="https://console.anthropic.com" target="_blank">console.anthropic.com</a> ← API Keys ← Create Key<br>يُحفظ على جهازك فقط ولا يُرسل لأحد</p>
    <div class="gate-err" id="gerr"></div>
    <button class="gate-btn" onclick="enterApp()">ابدأ الآن ←</button>
  </div>
</div>

<!-- APP -->
<div id="app">
  <div class="topnav">
    <div style="display:flex;align-items:center;gap:10px">
      <button class="hbtn" id="hbtn" onclick="toggleSB()"><span></span><span></span><span></span></button>
      <div class="nav-logo">
        <div class="nav-logo-icon">V</div>
        <span class="nav-logo-text">Via <span>AI</span></span>
      </div>
    </div>
    <div class="nav-right-btns">
      <div class="icon-btn" onclick="toggleTheme()" id="themeBtn" title="تغيير المظهر">🌙</div>
      <div class="icon-btn" onclick="goTo('settings')" title="الإعدادات">⚙️</div>
    </div>
  </div>

  <div class="app-body">
    <div class="overlay" id="overlay" onclick="closeSB()"></div>
    <div class="sidebar" id="sidebar">
      <div class="nav-sec">الرئيسية</div>
      <div class="nav-item active" onclick="goTo('home')"><div class="ni">🏠</div>الرئيسية</div>
      <div class="nav-sec">التوظيف</div>
      <div class="nav-item" onclick="goTo('cv')"><div class="ni">📄</div>مصمم السيرة الذاتية</div>
      <div class="nav-item" onclick="goTo('cover')"><div class="ni">✉️</div>الخطاب التعريفي</div>
      <div class="nav-item" onclick="goTo('interview')"><div class="ni">🎤</div>تحضير المقابلات</div>
      <div class="nav-item" onclick="goTo('ats')"><div class="ni">🔍</div>فاحص ATS</div>
      <div class="nav-sec">الجامعة</div>
      <div class="nav-item" onclick="goTo('summary')"><div class="ni">📝</div>ملخص المحاضرات</div>
      <div class="nav-item" onclick="goTo('questions')"><div class="ni">❓</div>توليد الاختبارات</div>
      <div class="nav-item" onclick="goTo('explain')"><div class="ni">💡</div>شرح المفاهيم</div>
      <div class="nav-item" onclick="goTo('solve')"><div class="ni">🧬</div>حل المسائل</div>
      <div class="nav-sec">العروض والمراسلات</div>
      <div class="nav-item" onclick="goTo('slides')"><div class="ni">🖥️</div>مخطط السلايدات</div>
      <div class="nav-item" onclick="goTo('script')"><div class="ni">🎙️</div>سكريبت الإلقاء</div>
      <div class="nav-item" onclick="goTo('email')"><div class="ni">📬</div>الإيميل الرسمي</div>
      <div class="nav-item" onclick="goTo('kpi')"><div class="ni">🎯</div>مخطط الأهداف</div>
      <div class="nav-sec">النظام</div>
      <div class="nav-item" onclick="goTo('settings')"><div class="ni">⚙️</div>الإعدادات والمكتبة</div>
    </div>

    <div class="content">

      <!-- HOME -->
      <div class="page active" id="page-home">
        <div class="home-scroll">
          <div class="home-hero">
            <h1>منصة <span>Via AI</span> 👋</h1>
            <p>نظام ذكي متكامل لإدارة مسيرتك الأكاديمية وصناعة مستقبلك المهني بأعلى كفاءة</p>
          </div>
          <div class="sec-h">التوظيف والمهن 💼</div>
          <div class="tgrid">
            <div class="tbtn" onclick="goTo('cv')"><div class="ti">📄</div><div class="tn">مصمم السيرة الذاتية</div><div class="td">سيرة ذاتية فاخرة جاهزة</div></div>
            <div class="tbtn" onclick="goTo('cover')"><div class="ti">✉️</div><div class="tn">الخطاب التعريفي</div><div class="td">Cover Letter مخصص</div></div>
            <div class="tbtn" onclick="goTo('interview')"><div class="ti">🎤</div><div class="tn">تحضير المقابلات</div><div class="td">أسئلة ونماذج إجابات</div></div>
            <div class="tbtn" onclick="goTo('ats')"><div class="ti">🔍</div><div class="tn">فاحص ATS</div><div class="td">مطابقة الكلمات المفتاحية</div></div>
          </div>
          <div class="sec-h">التعليم الأكاديمي 🎓</div>
          <div class="tgrid">
            <div class="tbtn" onclick="goTo('summary')"><div class="ti">📝</div><div class="tn">ملخص المحاضرات</div><div class="td">تكثيف المناهج بنقاط</div></div>
            <div class="tbtn" onclick="goTo('questions')"><div class="ti">❓</div><div class="tn">توليد الاختبارات</div><div class="td">أسئلة للمذاكرة</div></div>
            <div class="tbtn" onclick="goTo('explain')"><div class="ti">💡</div><div class="tn">شرح المفاهيم</div><div class="td">تبسيط أي نظرية</div></div>
            <div class="tbtn" onclick="goTo('solve')"><div class="ti">🧬</div><div class="tn">حل المسائل</div><div class="td">رياضيات وعلوم خطوة بخطوة</div></div>
          </div>
          <div class="sec-h">العروض والمراسلات 🖥️</div>
          <div class="tgrid">
            <div class="tbtn" onclick="goTo('slides')"><div class="ti">🖥️</div><div class="tn">مخطط السلايدات</div><div class="td">هيكل كامل لكل شريحة</div></div>
            <div class="tbtn" onclick="goTo('script')"><div class="ti">🎙️</div><div class="tn">سكريبت الإلقاء</div><div class="td">نص شفهي كامل</div></div>
            <div class="tbtn" onclick="goTo('email')"><div class="ti">📬</div><div class="tn">الإيميل الرسمي</div><div class="td">خطابات رسمية احترافية</div></div>
            <div class="tbtn" onclick="goTo('kpi')"><div class="ti">🎯</div><div class="tn">مخطط الأهداف</div><div class="td">OKRs وKPIs مفصلة</div></div>
          </div>
        </div>
      </div>

      <!-- TOOL PAGES - each uses the same structure -->
      <div class="page" id="page-cv"><div class="tool-layout">
        <div class="tool-form-side">
          <div class="form-inner">
            <div class="tool-header"><h2>📄 مصمم السيرة الذاتية</h2><p>سيرة ذاتية فاخرة جاهزة للمؤسسات الكبرى</p></div>
            <div class="row2"><div class="field"><label>الاسم الكامل</label><input id="cv-name" placeholder="عبدالله محمد"></div><div class="field"><label>المسمى المستهدف</label><input id="cv-title" placeholder="محلل نظم أول"></div></div>
            <div class="field"><label>الخبرات المهنية</label><textarea id="cv-exp" placeholder="الشركة - المسمى - أبرز الإنجازات"></textarea></div>
            <div class="field"><label>المؤهلات التعليمية</label><textarea id="cv-edu" placeholder="الدرجة - التخصص - الجامعة"></textarea></div>
            <div class="field"><label>المهارات</label><input id="cv-skills" placeholder="مفصولة بفاصلة"></div>
            <div class="field"><label>اللغة</label><select id="cv-lang"><option value="عربي">العربية</option><option value="إنجليزي">English</option></select></div>
          </div>
          <div class="form-footer">
            <div class="tool-err" id="cv-err"></div>
            <button class="run-btn" onclick="runTool('cv')">توليد السيرة الذاتية ✨</button>
          </div>
        </div>
        <div class="tool-chat-side" id="cv-chat"><div class="chat-empty"><div class="ce">📄</div><p>النتيجة ستظهر هنا<br>ثم تحدّث مع المساعد لتحسينها</p></div><div class="chat-bar"><textarea id="cv-inp" placeholder="اطلب تعديل أو تحسين..." rows="1" oninput="ar(this)" onkeydown="ck(event,'cv')"></textarea><button class="send" id="cv-send" onclick="sc('cv')">➤</button></div></div>
      </div></div>

      <div class="page" id="page-cover"><div class="tool-layout">
        <div class="tool-form-side">
          <div class="form-inner">
            <div class="tool-header"><h2>✉️ الخطاب التعريفي</h2><p>Cover Letter مقنع ومخصص للشركة</p></div>
            <div class="row2"><div class="field"><label>اسمك</label><input id="cl-name" placeholder="سلطان بن علي"></div><div class="field"><label>الجهة</label><input id="cl-company" placeholder="مجموعة الراجحي"></div></div>
            <div class="field"><label>الوظيفة الشاغرة</label><input id="cl-job" placeholder="أخصائي موارد بشرية"></div>
            <div class="field"><label>نقاط قوتك</label><textarea id="cl-skills" placeholder="لماذا أنت الأنسب؟ إنجازاتك..."></textarea></div>
            <div class="field"><label>اللغة</label><select id="cl-lang"><option value="عربي">العربية</option><option value="إنجليزي">English</option></select></div>
          </div>
          <div class="form-footer">
            <button class="run-btn" onclick="runTool('cover')">توليد الخطاب التعريفي ✨</button>
          </div>
        </div>
        <div class="tool-chat-side" id="cover-chat"><div class="chat-empty"><div class="ce">✉️</div><p>أدخل البيانات واضغط توليد</p></div><div class="chat-bar"><textarea id="cover-inp" placeholder="اطلب تعديل..." rows="1" oninput="ar(this)" onkeydown="ck(event,'cover')"></textarea><button class="send" id="cover-send" onclick="sc('cover')">➤</button></div></div>
      </div></div>

      <div class="page" id="page-interview"><div class="tool-layout">
        <div class="tool-form-side">
          <div class="form-inner">
            <div class="tool-header"><h2>🎤 تحضير المقابلات</h2><p>أسئلة متوقعة مع نماذج إجابات احترافية</p></div>
            <div class="field"><label>المسمى الوظيفي</label><input id="int-job" placeholder="مهندس أمن سيبراني"></div>
            <div class="field"><label>المستوى</label><select id="int-exp"><option value="حديث تخرج">حديث تخرج</option><option value="خبرة متوسطة">خبرة متوسطة</option><option value="مستوى قيادي">مستوى قيادي</option></select></div>
          </div>
          <div class="form-footer">
            <button class="run-btn" onclick="runTool('interview')">توليد دليل المقابلة ✨</button>
          </div>
        </div>
        <div class="tool-chat-side" id="interview-chat"><div class="chat-empty"><div class="ce">🎤</div><p>أدخل الوظيفة واضغط توليد</p></div><div class="chat-bar"><textarea id="interview-inp" placeholder="اطلب تعديل..." rows="1" oninput="ar(this)" onkeydown="ck(event,'interview')"></textarea><button class="send" id="interview-send" onclick="sc('interview')">➤</button></div></div>
      </div></div>

      <div class="page" id="page-ats"><div class="tool-layout">
        <div class="tool-form-side">
          <div class="form-inner">
            <div class="tool-header"><h2>🔍 فاحص ATS</h2><p>مطابقة السيرة الذاتية مع الوصف الوظيفي</p></div>
            <div class="field"><label>نص السيرة الذاتية</label><textarea id="ats-cv" placeholder="الصق نص سيرتك..."></textarea></div>
            <div class="field"><label>الوصف الوظيفي</label><textarea id="ats-jd" placeholder="الصق متطلبات الوظيفة..."></textarea></div>
          </div>
          <div class="form-footer">
            <button class="run-btn" onclick="runTool('ats')">بدء الفحص الآلي ✨</button>
          </div>
        </div>
        <div class="tool-chat-side" id="ats-chat"><div class="chat-empty"><div class="ce">🔍</div><p>الصق البيانات واضغط فحص</p></div><div class="chat-bar"><textarea id="ats-inp" placeholder="اطلب تعديل..." rows="1" oninput="ar(this)" onkeydown="ck(event,'ats')"></textarea><button class="send" id="ats-send" onclick="sc('ats')">➤</button></div></div>
      </div></div>

      <div class="page" id="page-summary"><div class="tool-layout">
        <div class="tool-form-side">
          <div class="form-inner">
            <div class="tool-header"><h2>📝 ملخص المحاضرات</h2><p>تكثيف المناهج في نقاط رئيسية</p></div>
            <div class="field"><label>النص أو المنهج</label><textarea id="sum-text" style="min-height:150px" placeholder="الصق محتوى المحاضرة..."></textarea></div>
            <div class="field"><label>طول الملخص</label><select id="sum-len"><option value="مركز جداً">مركز جداً</option><option value="متوسط" selected>متوسط</option><option value="تفصيلي">تفصيلي</option></select></div>
          </div>
          <div class="form-footer">
            <button class="run-btn" onclick="runTool('summary')">بدء التلخيص ✨</button>
          </div>
        </div>
        <div class="tool-chat-side" id="summary-chat"><div class="chat-empty"><div class="ce">📝</div><p>الصق المحتوى واضغط تلخيص</p></div><div class="chat-bar"><textarea id="summary-inp" placeholder="اطلب تعديل..." rows="1" oninput="ar(this)" onkeydown="ck(event,'summary')"></textarea><button class="send" id="summary-send" onclick="sc('summary')">➤</button></div></div>
      </div></div>

      <div class="page" id="page-questions"><div class="tool-layout">
        <div class="tool-form-side">
          <div class="form-inner">
            <div class="tool-header"><h2>❓ توليد الاختبارات</h2><p>أسئلة مراجعة من المنهج الدراسي</p></div>
            <div class="field"><label>المحتوى الدراسي</label><textarea id="q-text" style="min-height:140px" placeholder="الصق المنهج..."></textarea></div>
            <div class="field"><label>نوع الأسئلة</label><select id="q-type"><option value="مزيج شامل">مزيج شامل</option><option value="مقالي">مقالي عميق</option></select></div>
          </div>
          <div class="form-footer">
            <button class="run-btn" onclick="runTool('questions')">إنشاء بنك الأسئلة ✨</button>
          </div>
        </div>
        <div class="tool-chat-side" id="questions-chat"><div class="chat-empty"><div class="ce">❓</div><p>الصق المحتوى واضغط توليد</p></div><div class="chat-bar"><textarea id="questions-inp" placeholder="اطلب تعديل..." rows="1" oninput="ar(this)" onkeydown="ck(event,'questions')"></textarea><button class="send" id="questions-send" onclick="sc('questions')">➤</button></div></div>
      </div></div>

      <div class="page" id="page-explain"><div class="tool-layout">
        <div class="tool-form-side">
          <div class="form-inner">
            <div class="tool-header"><h2>💡 شرح المفاهيم</h2><p>تبسيط أي نظرية أو مفهوم صعب</p></div>
            <div class="field"><label>المفهوم أو النظرية</label><input id="exp-topic" placeholder="نظرية الألعاب، الذكاء الاصطناعي..."></div>
            <div class="field"><label>المستوى</label><select id="exp-level"><option value="مبتدئ">تبسيط مطلق</option><option value="جامعي" selected>طالب جامعي</option></select></div>
          </div>
          <div class="form-footer">
            <button class="run-btn" onclick="runTool('explain')">بدء الشرح ✨</button>
          </div>
        </div>
        <div class="tool-chat-side" id="explain-chat"><div class="chat-empty"><div class="ce">💡</div><p>أدخل الموضوع واضغط شرح</p></div><div class="chat-bar"><textarea id="explain-inp" placeholder="اطلب تعديل..." rows="1" oninput="ar(this)" onkeydown="ck(event,'explain')"></textarea><button class="send" id="explain-send" onclick="sc('explain')">➤</button></div></div>
      </div></div>

      <div class="page" id="page-solve"><div class="tool-layout">
        <div class="tool-form-side">
          <div class="form-inner">
            <div class="tool-header"><h2>🧬 حل المسائل العلمية</h2><p>تفكيك المعادلات والمسائل خطوة بخطوة</p></div>
            <div class="field"><label>نص المسألة</label><textarea id="solve-text" style="min-height:150px" placeholder="اكتب المسألة أو المعادلة..."></textarea></div>
          </div>
          <div class="form-footer">
            <button class="run-btn" onclick="runTool('solve')">تفكيك وحل المسألة ✨</button>
          </div>
        </div>
        <div class="tool-chat-side" id="solve-chat"><div class="chat-empty"><div class="ce">🧬</div><p>اكتب المسألة واضغط حل</p></div><div class="chat-bar"><textarea id="solve-inp" placeholder="اطلب تعديل..." rows="1" oninput="ar(this)" onkeydown="ck(event,'solve')"></textarea><button class="send" id="solve-send" onclick="sc('solve')">➤</button></div></div>
      </div></div>

      <div class="page" id="page-slides"><div class="tool-layout">
        <div class="tool-form-side">
          <div class="form-inner">
            <div class="tool-header"><h2>🖥️ مخطط السلايدات</h2><p>هيكل نصي كامل لكل شريحة مع ملاحظات</p></div>
            <div class="field"><label>موضوع العرض</label><input id="sl-topic" placeholder="التحول الرقمي في التعليم"></div>
            <div class="field"><label>عدد الشرائح</label><select id="sl-count"><option value="5">5 شرائح</option><option value="8" selected>8 شرائح</option><option value="12">12 شريحة</option></select></div>
          </div>
          <div class="form-footer">
            <button class="run-btn" onclick="runTool('slides')">توليد هيكل السلايدات ✨</button>
          </div>
        </div>
        <div class="tool-chat-side" id="slides-chat"><div class="chat-empty"><div class="ce">🖥️</div><p>أدخل الموضوع واضغط توليد</p></div><div class="chat-bar"><textarea id="slides-inp" placeholder="اطلب تعديل..." rows="1" oninput="ar(this)" onkeydown="ck(event,'slides')"></textarea><button class="send" id="slides-send" onclick="sc('slides')">➤</button></div></div>
      </div></div>

      <div class="page" id="page-script"><div class="tool-layout">
        <div class="tool-form-side">
          <div class="form-inner">
            <div class="tool-header"><h2>🎙️ سكريبت الإلقاء</h2><p>النص الكامل الذي ستتحدث به أمام الجمهور</p></div>
            <div class="field"><label>الموضوع</label><input id="sc-topic" placeholder="موضوع العرض"></div>
            <div class="field"><label>عناوين السلايدات (سطر لكل شريحة)</label><textarea id="sc-slides" placeholder="المقدمة&#10;المشكلة&#10;الحل المقترح&#10;التوصيات&#10;الخلاصة"></textarea></div>
          </div>
          <div class="form-footer">
            <button class="run-btn" onclick="runTool('script')">توليد نص الإلقاء ✨</button>
          </div>
        </div>
        <div class="tool-chat-side" id="script-chat"><div class="chat-empty"><div class="ce">🎙️</div><p>أدخل البيانات واضغط توليد</p></div><div class="chat-bar"><textarea id="script-inp" placeholder="اطلب تعديل..." rows="1" oninput="ar(this)" onkeydown="ck(event,'script')"></textarea><button class="send" id="script-send" onclick="sc('script')">➤</button></div></div>
      </div></div>

      <div class="page" id="page-email"><div class="tool-layout">
        <div class="tool-form-side">
          <div class="form-inner">
            <div class="tool-header"><h2>📬 الإيميل الرسمي</h2><p>تحويل مسودتك إلى خطاب رسمي فاخر</p></div>
            <div class="field"><label>فكرة الإيميل أو المسودة</label><textarea id="em-text" style="min-height:140px" placeholder="مثال: إيميل للدكتور أطلب إعادة الاختبار بسبب عذر..."></textarea></div>
            <div class="field"><label>نبرة الخطاب</label><select id="em-tone"><option value="رسمية جداً">رسمية جداً</option><option value="ودية واحترافية">ودية واحترافية</option></select></div>
          </div>
          <div class="form-footer">
            <button class="run-btn" onclick="runTool('email')">صياغة البريد الرسمي ✨</button>
          </div>
        </div>
        <div class="tool-chat-side" id="email-chat"><div class="chat-empty"><div class="ce">📬</div><p>أدخل الفكرة واضغط توليد</p></div><div class="chat-bar"><textarea id="email-inp" placeholder="اطلب تعديل..." rows="1" oninput="ar(this)" onkeydown="ck(event,'email')"></textarea><button class="send" id="email-send" onclick="sc('email')">➤</button></div></div>
      </div></div>

      <div class="page" id="page-kpi"><div class="tool-layout">
        <div class="tool-form-side">
          <div class="form-inner">
            <div class="tool-header"><h2>🎯 مخطط الأهداف الذكية</h2><p>خطة استراتيجية مع OKRs وKPIs</p></div>
            <div class="field"><label>هدفك الأساسي</label><textarea id="kp-target" style="min-height:120px" placeholder="مثال: أريد رفع معدلي الجامعي هذا الترم..."></textarea></div>
          </div>
          <div class="form-footer">
            <button class="run-btn" onclick="runTool('kpi')">بناء الخطة الاستراتيجية ✨</button>
          </div>
        </div>
        <div class="tool-chat-side" id="kpi-chat"><div class="chat-empty"><div class="ce">🎯</div><p>أدخل هدفك واضغط توليد</p></div><div class="chat-bar"><textarea id="kpi-inp" placeholder="اطلب تعديل..." rows="1" oninput="ar(this)" onkeydown="ck(event,'kpi')"></textarea><button class="send" id="kpi-send" onclick="sc('kpi')">➤</button></div></div>
      </div></div>

      <!-- SETTINGS -->
      <div class="page" id="page-settings">
        <div class="settings-scroll">
          <!-- Stats -->
          <div class="settings-card">
            <h3>📊 إحصاءات الاستخدام</h3>
            <div class="stats-grid">
              <div class="stat-card"><div class="stat-num" id="stat-gen">0</div><div class="stat-lbl">توليد كلي</div></div>
              <div class="stat-card"><div class="stat-num" id="stat-arch">0</div><div class="stat-lbl">محفوظ في المكتبة</div></div>
              <div class="stat-card"><div class="stat-num" id="stat-days">0</div><div class="stat-lbl">أيام الاستخدام</div></div>
            </div>
          </div>
          <!-- Theme -->
          <div class="settings-card">
            <h3>🎨 مظهر المنصة</h3>
            <div class="theme-btns">
              <button class="theme-btn active" id="thm-dark" onclick="setTheme('dark')">🌙 الوضع الداكن</button>
              <button class="theme-btn" id="thm-light" onclick="setTheme('light')">☀️ الوضع الفاتح</button>
            </div>
          </div>
          <!-- Key -->
          <div class="settings-card">
            <h3>🔑 إدارة API Key</h3>
            <div class="field" style="margin:0">
              <input type="password" id="settings-key" placeholder="sk-ant-..." style="width:100%;background:var(--s2);border:1px solid var(--border2);border-radius:11px;padding:12px 14px;font-family:'Cairo';font-size:14px;color:var(--text);outline:none">
            </div>
            <button onclick="saveKeyFromSettings()" style="margin-top:12px;background:var(--p);border:none;border-radius:10px;padding:11px 22px;color:white;font-family:'Cairo';font-size:13.5px;font-weight:700;cursor:pointer">حفظ المفتاح</button>
          </div>
          <!-- Archive -->
          <div class="settings-card">
            <h3>📚 مكتبة الأعمال المحفوظة</h3>
            <p style="font-size:12.5px;color:var(--t3);margin-bottom:4px">يتم حفظ كل توليد تلقائياً هنا</p>
            <div class="archive-list" id="archList"></div>
          </div>
        </div>
      </div>

    </div><!-- content -->
  </div><!-- app-body -->
</div><!-- app -->

<script>
var KEY='', hx={}, theme='dark', genCount=0;

// GATE
function tEye(){var i=document.getElementById('gkey');i.type=i.type==='password'?'text':'password';}
function enterApp(){
  var k=document.getElementById('gkey').value.trim();
  var err=document.getElementById('gerr');
  if(!k){err.textContent='أدخل API Key';err.style.display='block';return;}
  if(!k.startsWith('sk-ant-')){err.textContent='المفتاح يبدأ بـ sk-ant-';err.style.display='block';return;}
  err.style.display='none';
  KEY=k;
  localStorage.setItem('via_key',k);
  document.getElementById('gate').style.display='none';
  document.getElementById('app').classList.add('show');
  document.getElementById('settings-key').value=k;
  updateStats();renderArchive();
  var savedTheme=localStorage.getItem('via_theme');
  if(savedTheme)setTheme(savedTheme);
}
document.getElementById('gkey').addEventListener('keydown',function(e){if(e.key==='Enter')enterApp();});
(function(){var s=localStorage.getItem('via_key');if(s)document.getElementById('gkey').value=s;})();

function saveKeyFromSettings(){
  var k=document.getElementById('settings-key').value.trim();
  if(k.startsWith('sk-ant-')){KEY=k;localStorage.setItem('via_key',k);alert('تم حفظ المفتاح');}
}

// THEME
function setTheme(t){
  theme=t;
  document.documentElement.setAttribute('data-theme',t);
  localStorage.setItem('via_theme',t);
  document.getElementById('thm-dark').classList.toggle('active',t==='dark');
  document.getElementById('thm-light').classList.toggle('active',t==='light');
  document.getElementById('themeBtn').textContent=t==='dark'?'🌙':'☀️';
}
function toggleTheme(){setTheme(theme==='dark'?'light':'dark');}

// NAV
function goTo(id){
  document.querySelectorAll('.page').forEach(function(p){p.classList.remove('active');});
  document.querySelectorAll('.nav-item').forEach(function(n){n.classList.remove('active');});
  var pg=document.getElementById('page-'+id);if(pg)pg.classList.add('active');
  document.querySelectorAll('.nav-item').forEach(function(n){
    if(n.getAttribute('onclick')&&n.getAttribute('onclick').includes("'"+id+"'"))n.classList.add('active');
  });
  closeSB();
  // الجوال: أظهر الفورم واخفِ الشات
  document.querySelectorAll('.tool-chat-side').forEach(function(el){el.classList.remove('mob-show');});
  if(id==='settings')updateStats();
}
function toggleSB(){
  var s=document.getElementById('sidebar'),h=document.getElementById('hbtn'),o=document.getElementById('overlay');
  var op=s.classList.toggle('open');h.classList.toggle('open',op);o.classList.toggle('show',op);
}
function closeSB(){
  document.getElementById('sidebar').classList.remove('open');
  document.getElementById('hbtn').classList.remove('open');
  document.getElementById('overlay').classList.remove('show');
}

// CLAUDE - STREAMING
async function callClaude(messages, onChunk){
  var res=await fetch('https://api.anthropic.com/v1/messages',{
    method:'POST',
    headers:{
      'Content-Type':'application/json',
      'x-api-key':KEY,
      'anthropic-version':'2023-06-01',
      'anthropic-dangerous-direct-browser-access':'true'
    },
    body:JSON.stringify({
      model:'claude-sonnet-4-6',
      max_tokens:4000,
      stream:true,
      messages:messages
    })
  });
  if(!res.ok){var d=await res.json();throw new Error(d.error?d.error.message:'فشل الاتصال');}
  var reader=res.body.getReader();
  var decoder=new TextDecoder();
  var fullText='';
  while(true){
    var result=await reader.read();
    if(result.done)break;
    var chunk=decoder.decode(result.value,{stream:true});
    var lines=chunk.split('\n');
    for(var i=0;i<lines.length;i++){
      var line=lines[i].trim();
      if(line.startsWith('data: ')){
        var data=line.slice(6);
        if(data==='[DONE]')continue;
        try{
          var parsed=JSON.parse(data);
          if(parsed.type==='content_block_delta'&&parsed.delta&&parsed.delta.text){
            fullText+=parsed.delta.text;
            if(onChunk)onChunk(parsed.delta.text,fullText);
          }
        }catch(e){}
      }
    }
  }
  return fullText;
}

// CHAT UI
function v(id){var e=document.getElementById(id);return e?e.value.trim():'';}
function ar(el){el.style.height='auto';el.style.height=Math.min(el.scrollHeight,100)+'px';}
function ck(e,tid){if(e.key==='Enter'&&!e.shiftKey){e.preventDefault();sc(tid);}}

function getChatMsgs(tid){
  var c=document.getElementById(tid+'-chat');
  var existing=c.querySelector('.chat-msgs');
  if(existing)return existing;
  // init
  var empty=c.querySelector('.chat-empty');
  var bar=c.querySelector('.chat-bar');
  c.innerHTML='';
  var msgs=document.createElement('div');msgs.className='chat-msgs';msgs.id=tid+'-msgs';
  c.appendChild(msgs);
  if(bar)c.appendChild(bar);
  // زر رجوع للجوال
  var back=document.createElement('button');
  back.className='back-btn';
  back.innerHTML='← رجوع للحقول';
  back.onclick=function(){document.getElementById(tid+'-chat').classList.remove('mob-show');};
  msgs.before(back);
  return msgs;
}

function addMsg(tid,role,text){
  var msgs=getChatMsgs(tid);
  var d=document.createElement('div');d.className='msg '+role;
  var lbl=role==='ai'?'Via AI':'أنت';
  var acts=role==='ai'?'<div class="msg-actions"><button class="mcopy" onclick="cp(this)">نسخ الكل</button></div>':'';
  d.innerHTML='<div class="msg-label">'+lbl+'</div><div class="msg-bubble">'+esc(text)+'</div>'+acts;
  msgs.appendChild(d);
  setTimeout(function(){msgs.scrollTop=msgs.scrollHeight;},30);
  return d;
}

function addStreamMsg(tid){
  var msgs=getChatMsgs(tid);
  var d=document.createElement('div');d.className='msg ai';
  d.innerHTML='<div class="msg-label">Via AI</div><div class="msg-bubble"><span class="streaming-cursor"></span></div><div class="msg-actions"><button class="mcopy" onclick="cp(this)">نسخ الكل</button></div>';
  msgs.appendChild(d);
  setTimeout(function(){msgs.scrollTop=msgs.scrollHeight;},30);
  return d.querySelector('.msg-bubble');
}

function addTypingMsg(tid){
  var msgs=getChatMsgs(tid);
  var d=document.createElement('div');d.className='msg ai';d.id=tid+'-typ';
  d.innerHTML='<div class="msg-label">Via AI</div><div class="typing"><div class="td"></div><div class="td"></div><div class="td"></div></div>';
  msgs.appendChild(d);
  setTimeout(function(){msgs.scrollTop=msgs.scrollHeight;},30);
}
function rmTyping(tid){var e=document.getElementById(tid+'-typ');if(e)e.remove();}

async function sc(tid){
  var inp=document.getElementById(tid+'-inp');if(!inp)return;
  var msg=inp.value.trim();if(!msg)return;
  inp.value='';inp.style.height='auto';
  if(!hx[tid])hx[tid]=[];
  addMsg(tid,'user',msg);
  hx[tid].push({role:'user',content:msg});
  var sb=document.getElementById(tid+'-send');if(sb)sb.disabled=true;
  addTypingMsg(tid);
  try{
    var reply=await callClaude(hx[tid]);
    rmTyping(tid);addMsg(tid,'ai',reply);
    hx[tid].push({role:'assistant',content:reply});
  }catch(e){rmTyping(tid);addMsg(tid,'ai','خطأ: '+e.message);}
  finally{if(sb)sb.disabled=false;}
}

// PROMPTS
var P={
  cv:function(){return 'صمم سيرة ذاتية احترافية باللغة '+v('cv-lang')+' لـ:\nالاسم: '+v('cv-name')+'\nالمسمى: '+v('cv-title')+'\nالخبرات: '+v('cv-exp')+'\nالتعليم: '+v('cv-edu')+'\nالمهارات: '+v('cv-skills')+'\nنظّم السيرة بهيكل فاخر وجاهز للمؤسسات الكبرى.';},
  cover:function(){return 'اكتب خطاب تعريفي (Cover Letter) احترافي باللغة '+v('cl-lang')+' إلى ('+v('cl-company')+') لوظيفة ('+v('cl-job')+').\nنقاط قوتي: '+v('cl-skills');},
  interview:function(){return 'أتقدم لوظيفة ('+v('int-job')+') مستوى ('+v('int-exp')+'). اكتب 7 أسئلة مقابلة متوقعة مع نموذج إجابة احترافي لكل سؤال.';},
  ats:function(){return 'حلّل مطابقة هذه السيرة الذاتية مع الوصف الوظيفي:\nالسيرة:\n'+v('ats-cv')+'\n\nالوصف:\n'+v('ats-jd')+'\nأعطني: نسبة المطابقة، الكلمات المفقودة، ونصائح التحسين.';},
  summary:function(){return 'لخّص المحتوى التالي تلخيصاً '+v('sum-len')+' بنقاط مرقمة وواضحة:\n\n'+v('sum-text');},
  questions:function(){return 'من المحتوى التالي أنشئ أسئلة اختبار ('+v('q-type')+') مع إجابات:\n\n'+v('q-text');},
  explain:function(){return 'اشرح "'+v('exp-topic')+'" لمستوى ('+v('exp-level')+') بأمثلة واقعية مبسطة.';},
  solve:function(){return 'فكّك وحل المسألة التالية خطوة بخطوة مع شرح المنطق:\n\n'+v('solve-text');},
  slides:function(){return 'أنشئ هيكل '+v('sl-count')+' شرائح عرض عن: "'+v('sl-topic')+'".\nلكل شريحة: العنوان، النقاط، وملاحظات المتحدث.';},
  script:function(){return 'اكتب سكريبت إلقاء كامل لعرض عن "'+v('sc-topic')+'".\nالشرائح:\n'+v('sc-slides');},
  email:function(){return 'أعد صياغة هذه الفكرة كإيميل رسمي بنبرة ('+v('em-tone')+'):\n\n'+v('em-text');},
  kpi:function(){return 'ضع خطة OKRs وKPIs مفصلة لهدفي:\n'+v('kp-target');},
};

async function runTool(tid){
  var prompt=P[tid]?P[tid]():'';if(!prompt)return;
  if(!hx[tid])hx[tid]=[];

  // الجوال: أظهر منطقة الشات
  document.getElementById(tid+'-chat').classList.add('mob-show');

  var btn=document.querySelector('#page-'+tid+' .run-btn');if(btn)btn.disabled=true;

  // مسح الرسائل السابقة
  var msgs=document.getElementById(tid+'-msgs');
  if(msgs)msgs.innerHTML='';
  getChatMsgs(tid); // reinit

  // streaming
  var bubble=addStreamMsg(tid);
  var accum='';

  try{
    var final=await callClaude([{role:'user',content:prompt}],function(chunk,full){
      accum=full;
      bubble.innerHTML=esc(full)+'<span class="streaming-cursor"></span>';
      var msgsEl=document.getElementById(tid+'-msgs');
      if(msgsEl)msgsEl.scrollTop=msgsEl.scrollHeight;
    });
    // remove cursor
    bubble.innerHTML=esc(final);
    hx[tid]=[{role:'user',content:prompt},{role:'assistant',content:final}];
    genCount++;
    localStorage.setItem('via_gen',genCount);
    saveArch(tid,final);
  }catch(e){
    bubble.innerHTML='خطأ: '+esc(e.message);
  }finally{
    if(btn)btn.disabled=false;
  }
}

// ARCHIVE
var titleMap={cv:'سيرة ذاتية',cover:'خطاب تعريفي',interview:'تحضير مقابلة',ats:'فحص ATS',summary:'تلخيص محاضرة',questions:'أسئلة اختبار',explain:'شرح مفهوم',solve:'حل مسألة',slides:'شرائح عرض',script:'سكريبت إلقاء',email:'إيميل رسمي',kpi:'مخطط أهداف'};

function saveArch(tid,text){
  var arch=JSON.parse(localStorage.getItem('via_arch')||'[]');
  arch.unshift({id:Date.now(),tool:titleMap[tid]||tid,date:new Date().toLocaleDateString('ar-SA',{hour:'2-digit',minute:'2-digit'}),content:text});
  if(arch.length>50)arch=arch.slice(0,50);
  localStorage.setItem('via_arch',JSON.stringify(arch));
}

function renderArchive(){
  var c=document.getElementById('archList');if(!c)return;
  var arch=JSON.parse(localStorage.getItem('via_arch')||'[]');
  if(!arch.length){c.innerHTML='<div class="empty-arch">لا توجد أعمال محفوظة بعد</div>';return;}
  c.innerHTML='';
  arch.forEach(function(item){
    var d=document.createElement('div');d.className='arch-item';
    d.innerHTML='<div class="arch-meta"><span>'+item.tool+'</span><span>'+item.date+'</span></div><div class="arch-body">'+esc(item.content.substring(0,200))+'</div><div class="arch-actions"><button class="a-btn" onclick="cpText(\''+item.id+'\')">نسخ</button><button class="a-btn del" onclick="delArch('+item.id+')">حذف</button></div>';
    c.appendChild(d);
  });
}

function cpText(id){
  var arch=JSON.parse(localStorage.getItem('via_arch')||'[]');
  var item=arch.find(function(a){return a.id===id;});
  if(item)navigator.clipboard.writeText(item.content).then(function(){alert('تم النسخ!');});
}

function delArch(id){
  var arch=JSON.parse(localStorage.getItem('via_arch')||'[]');
  arch=arch.filter(function(a){return a.id!==id;});
  localStorage.setItem('via_arch',JSON.stringify(arch));
  renderArchive();updateStats();
}

function updateStats(){
  var arch=JSON.parse(localStorage.getItem('via_arch')||'[]');
  var gen=parseInt(localStorage.getItem('via_gen')||'0');
  var days=parseInt(localStorage.getItem('via_days')||'1');
  var today=new Date().toDateString();
  if(localStorage.getItem('via_last_day')!==today){
    days++;localStorage.setItem('via_days',days);localStorage.setItem('via_last_day',today);
  }
  var sn=document.getElementById('stat-gen');if(sn)sn.textContent=gen;
  var sa=document.getElementById('stat-arch');if(sa)sa.textContent=arch.length;
  var sd=document.getElementById('stat-days');if(sd)sd.textContent=days;
  renderArchive();
}

// UTILS
function cp(btn){
  var bubble=btn.closest('.msg').querySelector('.msg-bubble');
  if(!bubble)return;
  navigator.clipboard.writeText(bubble.innerText).then(function(){
    btn.textContent='تم النسخ ✓';btn.classList.add('ok');
    setTimeout(function(){btn.textContent='نسخ الكل';btn.classList.remove('ok');},2000);
  });
}
function esc(t){return(t||'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/\n/g,'<br>');}

// Load gen count
genCount=parseInt(localStorage.getItem('via_gen')||'0');
</script>
</body>
</html>
