<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>AI Pro - مساعد الجامعة والتوظيف</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800;900&display=swap');

*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
:root{
  --bg:#07070e;
  --s1:#0e0e1a;
  --s2:#141420;
  --s3:#1a1a28;
  --border:#ffffff0f;
  --border2:#ffffff18;
  --p:#7c6dfa;
  --p2:#9d91fb;
  --pg:rgba(124,109,250,0.15);
  --pg2:rgba(124,109,250,0.08);
  --text:#f2f2f8;
  --t2:#aaaacc;
  --t3:#666688;
  --green:#2ecc71;
  --red:#e74c3c;
  --gold:#f39c12;
}
html,body{height:100%;font-family:'Cairo',sans-serif;background:var(--bg);color:var(--text);overflow:hidden}

/* ===== API GATE ===== */
#gate{
  position:fixed;inset:0;z-index:9999;
  background:var(--bg);
  display:flex;align-items:center;justify-content:center;
  padding:20px;
}
.gate-card{
  width:100%;max-width:480px;
  background:var(--s1);
  border:1px solid var(--border2);
  border-radius:28px;
  padding:48px 40px;
  text-align:center;
  box-shadow:0 40px 80px rgba(0,0,0,0.6),0 0 0 1px var(--border);
  position:relative;overflow:hidden;
}
.gate-card::before{
  content:'';position:absolute;top:-80px;left:50%;transform:translateX(-50%);
  width:300px;height:300px;
  background:radial-gradient(circle,rgba(124,109,250,0.12),transparent 70%);
  pointer-events:none;
}
.gate-logo{
  width:72px;height:72px;
  background:linear-gradient(135deg,var(--p),#a78bfa);
  border-radius:22px;
  display:flex;align-items:center;justify-content:center;
  font-size:32px;
  margin:0 auto 24px;
  box-shadow:0 8px 32px rgba(124,109,250,0.4);
}
.gate-title{font-size:26px;font-weight:900;margin-bottom:8px;letter-spacing:-0.5px}
.gate-title span{
  background:linear-gradient(135deg,var(--p),#c4b5fd);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
}
.gate-sub{font-size:14px;color:var(--t2);margin-bottom:32px;line-height:1.7}
.gate-input-wrap{position:relative;margin-bottom:12px}
.gate-input-wrap input{
  width:100%;background:var(--s2);
  border:1.5px solid var(--border2);
  border-radius:14px;padding:16px 48px 16px 20px;
  font-family:'Cairo',sans-serif;font-size:15px;
  color:var(--text);direction:ltr;outline:none;
  transition:all 0.2s;
}
.gate-input-wrap input:focus{border-color:var(--p);box-shadow:0 0 0 4px var(--pg)}
.gate-input-wrap input::placeholder{color:var(--t3)}
.eye-btn{
  position:absolute;left:16px;top:50%;transform:translateY(-50%);
  background:none;border:none;cursor:pointer;color:var(--t3);font-size:18px;
  padding:4px;
}
.gate-hint{font-size:12px;color:var(--t3);margin-bottom:24px;line-height:1.7}
.gate-hint a{color:var(--p);text-decoration:none}
.gate-btn{
  width:100%;
  background:linear-gradient(135deg,var(--p),#6d5cf8);
  border:none;border-radius:14px;
  padding:16px;color:white;
  font-family:'Cairo',sans-serif;font-size:16px;font-weight:700;
  cursor:pointer;transition:all 0.2s;
  box-shadow:0 8px 24px rgba(124,109,250,0.4);
}
.gate-btn:hover{transform:translateY(-2px);box-shadow:0 12px 32px rgba(124,109,250,0.5)}
.gate-btn:active{transform:translateY(0)}
.gate-err{
  background:rgba(231,76,60,0.1);border:1px solid rgba(231,76,60,0.3);
  border-radius:10px;padding:10px 14px;
  color:#e74c3c;font-size:13px;margin-bottom:16px;display:none;
}

/* ===== APP LAYOUT ===== */
#app{display:none;height:100vh;overflow:hidden;flex-direction:column}
#app.show{display:flex}

/* TOP NAV */
.topnav{
  background:var(--s1);
  border-bottom:1px solid var(--border);
  padding:0 20px;
  height:60px;
  display:flex;align-items:center;gap:12px;
  flex-shrink:0;
  position:relative;z-index:50;
}
.nav-logo{
  display:flex;align-items:center;gap:10px;
  margin-left:auto;
}
.nav-logo-icon{
  width:34px;height:34px;
  background:linear-gradient(135deg,var(--p),#a78bfa);
  border-radius:10px;
  display:flex;align-items:center;justify-content:center;
  font-size:15px;
  box-shadow:0 4px 12px rgba(124,109,250,0.35);
}
.nav-logo-text{font-size:15px;font-weight:800}
.nav-logo-text span{color:var(--p)}

.hamburger{
  background:var(--s2);border:1px solid var(--border2);
  border-radius:10px;padding:8px;cursor:pointer;
  display:none;flex-direction:column;gap:4px;
  width:38px;height:38px;align-items:center;justify-content:center;
}
.hamburger span{width:16px;height:2px;background:var(--t2);border-radius:2px;transition:all 0.3s}
.hamburger.open span:nth-child(1){transform:rotate(45deg) translate(4px,4px)}
.hamburger.open span:nth-child(2){opacity:0}
.hamburger.open span:nth-child(3){transform:rotate(-45deg) translate(4px,-4px)}

.nav-key-badge{
  margin-right:auto;
  display:flex;align-items:center;gap:8px;
  background:var(--pg2);border:1px solid rgba(124,109,250,0.2);
  border-radius:20px;padding:6px 14px;
  font-size:12px;color:var(--p);font-weight:600;cursor:pointer;
}

/* BODY */
.app-body{display:flex;flex:1;overflow:hidden}

/* SIDEBAR */
.sidebar{
  width:240px;min-width:240px;
  background:var(--s1);
  border-left:1px solid var(--border);
  overflow-y:auto;
  padding:12px 0 20px;
  transition:transform 0.3s;
  flex-shrink:0;
}
.sidebar::-webkit-scrollbar{width:4px}
.sidebar::-webkit-scrollbar-track{background:transparent}
.sidebar::-webkit-scrollbar-thumb{background:var(--border2);border-radius:4px}

.nav-section{
  font-size:10px;font-weight:700;color:var(--t3);
  text-transform:uppercase;letter-spacing:1.5px;
  padding:16px 18px 6px;
}
.nav-item{
  display:flex;align-items:center;gap:10px;
  padding:11px 18px;cursor:pointer;
  font-size:13.5px;font-weight:600;color:var(--t2);
  transition:all 0.15s;border-right:3px solid transparent;
  user-select:none;
}
.nav-item:hover{background:var(--pg2);color:var(--text)}
.nav-item.active{background:var(--pg);color:var(--p);border-right-color:var(--p)}
.nav-item .ni{
  width:32px;height:32px;border-radius:9px;
  display:flex;align-items:center;justify-content:center;
  font-size:15px;background:var(--s2);flex-shrink:0;
  transition:all 0.15s;
}
.nav-item.active .ni,.nav-item:hover .ni{background:var(--pg)}

/* OVERLAY */
.overlay{
  display:none;position:fixed;inset:0;
  background:rgba(0,0,0,0.6);z-index:40;
  backdrop-filter:blur(2px);
}
.overlay.show{display:block}

/* CONTENT */
.content{flex:1;overflow-y:auto;display:flex;flex-direction:column}
.content::-webkit-scrollbar{width:6px}
.content::-webkit-scrollbar-track{background:transparent}
.content::-webkit-scrollbar-thumb{background:var(--border2);border-radius:4px}

/* PAGE */
.page{display:none;flex:1;flex-direction:column;height:100%}
.page.active{display:flex}

/* HOME PAGE */
.home-wrap{padding:28px 28px 20px;flex:1;overflow-y:auto}
.home-hero{
  background:linear-gradient(135deg,var(--s2),var(--s3));
  border:1px solid var(--border2);
  border-radius:24px;padding:32px;margin-bottom:24px;
  position:relative;overflow:hidden;
}
.home-hero::before{
  content:'';position:absolute;top:-40px;right:-40px;
  width:200px;height:200px;
  background:radial-gradient(circle,rgba(124,109,250,0.15),transparent 70%);
}
.home-hero h1{font-size:24px;font-weight:900;margin-bottom:8px}
.home-hero h1 span{color:var(--p)}
.home-hero p{font-size:14px;color:var(--t2);line-height:1.7;max-width:400px}

.tools-section h2{font-size:15px;font-weight:700;color:var(--t2);margin-bottom:14px}
.tools-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(160px,1fr));gap:12px;margin-bottom:24px}
.tool-btn{
  background:var(--s2);border:1px solid var(--border);
  border-radius:16px;padding:18px 16px;
  cursor:pointer;transition:all 0.2s;text-align:right;
}
.tool-btn:hover{border-color:var(--p);background:var(--pg2);transform:translateY(-2px)}
.tool-btn .tb-icon{font-size:26px;margin-bottom:10px}
.tool-btn .tb-name{font-size:13px;font-weight:700;margin-bottom:4px}
.tool-btn .tb-desc{font-size:11px;color:var(--t3);line-height:1.5}

/* TOOL PAGE */
.tool-layout{display:flex;flex:1;overflow:hidden;height:100%}

/* TOOL FORM SIDE */
.tool-form-side{
  width:340px;min-width:300px;
  border-left:1px solid var(--border);
  overflow-y:auto;padding:24px 20px;
  flex-shrink:0;
}
.tool-form-side::-webkit-scrollbar{width:4px}
.tool-form-side::-webkit-scrollbar-thumb{background:var(--border2);border-radius:4px}

.tool-header{margin-bottom:20px}
.tool-header h2{font-size:20px;font-weight:800;margin-bottom:4px}
.tool-header p{font-size:13px;color:var(--t2);line-height:1.6}

.field{margin-bottom:14px}
.field label{
  display:block;font-size:11px;font-weight:700;color:var(--t3);
  text-transform:uppercase;letter-spacing:0.8px;margin-bottom:7px;
}
.field input,.field textarea,.field select{
  width:100%;
  background:var(--s2);border:1.5px solid var(--border2);
  border-radius:11px;padding:11px 14px;
  font-family:'Cairo',sans-serif;font-size:13.5px;
  color:var(--text);outline:none;transition:all 0.2s;
}
.field textarea{resize:vertical;min-height:90px;line-height:1.7}
.field input:focus,.field textarea:focus,.field select:focus{
  border-color:var(--p);box-shadow:0 0 0 3px var(--pg);
}
.field input::placeholder,.field textarea::placeholder{color:var(--t3)}
.row2{display:flex;gap:10px}
.row2 .field{flex:1}

.run-btn{
  width:100%;
  background:linear-gradient(135deg,var(--p),#6d5cf8);
  border:none;border-radius:12px;
  padding:14px;color:white;
  font-family:'Cairo',sans-serif;font-size:15px;font-weight:700;
  cursor:pointer;transition:all 0.2s;
  box-shadow:0 6px 20px rgba(124,109,250,0.35);
  margin-top:4px;
}
.run-btn:hover{transform:translateY(-1px);box-shadow:0 8px 28px rgba(124,109,250,0.45)}
.run-btn:active{transform:translateY(0)}
.run-btn:disabled{opacity:0.5;cursor:not-allowed;transform:none}

.tool-err{
  background:rgba(231,76,60,0.1);border:1px solid rgba(231,76,60,0.25);
  border-radius:10px;padding:10px 14px;
  color:#e74c3c;font-size:13px;margin-bottom:12px;display:none;
}

/* CHAT/RESULT SIDE */
.tool-chat-side{
  flex:1;display:flex;flex-direction:column;
  overflow:hidden;
  background:var(--bg);
}

.chat-messages{
  flex:1;overflow-y:auto;padding:20px;
  display:flex;flex-direction:column;gap:14px;
}
.chat-messages::-webkit-scrollbar{width:6px}
.chat-messages::-webkit-scrollbar-thumb{background:var(--border2);border-radius:4px}

.msg{max-width:85%;animation:fadeUp 0.3s ease}
@keyframes fadeUp{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}

.msg.ai{align-self:flex-end}
.msg.user{align-self:flex-start}

.msg-bubble{
  padding:14px 18px;border-radius:18px;
  font-size:14px;line-height:1.8;white-space:pre-wrap;
}
.msg.ai .msg-bubble{
  background:var(--s2);border:1px solid var(--border2);
  border-radius:18px 4px 18px 18px;
}
.msg.user .msg-bubble{
  background:linear-gradient(135deg,var(--p),#6d5cf8);
  color:white;
  border-radius:4px 18px 18px 18px;
}
.msg-label{font-size:11px;color:var(--t3);margin-bottom:5px;padding:0 4px}
.msg-actions{display:flex;gap:8px;margin-top:8px;flex-wrap:wrap}
.msg-copy{
  background:var(--s2);border:1px solid var(--border2);
  border-radius:8px;padding:5px 12px;
  font-family:'Cairo',sans-serif;font-size:12px;color:var(--t2);
  cursor:pointer;transition:all 0.2s;
}
.msg-copy:hover{border-color:var(--p);color:var(--p)}
.msg-copy.ok{border-color:var(--green);color:var(--green)}

.chat-empty{
  flex:1;display:flex;flex-direction:column;
  align-items:center;justify-content:center;
  color:var(--t3);text-align:center;padding:40px;
}
.chat-empty .ce-icon{font-size:48px;margin-bottom:16px;opacity:0.5}
.chat-empty p{font-size:14px;line-height:1.7}

/* CHAT INPUT BAR */
.chat-input-bar{
  border-top:1px solid var(--border);
  padding:14px 16px;
  background:var(--s1);
  display:flex;gap:10px;align-items:flex-end;
}
.chat-input-bar textarea{
  flex:1;background:var(--s2);
  border:1.5px solid var(--border2);
  border-radius:14px;
  padding:11px 16px;
  font-family:'Cairo',sans-serif;font-size:14px;
  color:var(--text);resize:none;outline:none;
  max-height:120px;min-height:44px;
  line-height:1.6;transition:border-color 0.2s;
}
.chat-input-bar textarea:focus{border-color:var(--p)}
.chat-input-bar textarea::placeholder{color:var(--t3)}
.send-btn{
  width:44px;height:44px;min-width:44px;
  background:linear-gradient(135deg,var(--p),#6d5cf8);
  border:none;border-radius:12px;
  cursor:pointer;display:flex;align-items:center;justify-content:center;
  font-size:18px;transition:all 0.2s;flex-shrink:0;
}
.send-btn:hover{transform:scale(1.05)}
.send-btn:active{transform:scale(0.95)}
.send-btn:disabled{opacity:0.5;cursor:not-allowed;transform:none}

/* TYPING */
.typing-indicator{display:flex;gap:5px;align-items:center;padding:14px 18px}
.typing-dot{width:7px;height:7px;background:var(--p);border-radius:50%;animation:bounce 1.2s infinite}
.typing-dot:nth-child(2){animation-delay:0.2s}
.typing-dot:nth-child(3){animation-delay:0.4s}
@keyframes bounce{0%,80%,100%{transform:translateY(0)}40%{transform:translateY(-8px)}}

/* CHANGE KEY MODAL */
#keyModal{
  display:none;position:fixed;inset:0;z-index:200;
  background:rgba(0,0,0,0.7);backdrop-filter:blur(4px);
  align-items:center;justify-content:center;padding:20px;
}
#keyModal.show{display:flex}
.key-modal-card{
  background:var(--s1);border:1px solid var(--border2);
  border-radius:20px;padding:28px;width:100%;max-width:400px;
}
.key-modal-card h3{font-size:18px;font-weight:800;margin-bottom:16px}
.modal-actions{display:flex;gap:10px;margin-top:16px}
.btn-cancel{
  flex:1;background:var(--s2);border:1px solid var(--border2);
  border-radius:10px;padding:12px;
  font-family:'Cairo',sans-serif;font-size:14px;font-weight:600;
  color:var(--t2);cursor:pointer;transition:all 0.2s;
}
.btn-save{
  flex:1;background:linear-gradient(135deg,var(--p),#6d5cf8);
  border:none;border-radius:10px;padding:12px;
  font-family:'Cairo',sans-serif;font-size:14px;font-weight:700;
  color:white;cursor:pointer;
}

/* RESPONSIVE */
@media(max-width:900px){
  .tool-form-side{width:100%;min-width:0;border-left:none;border-bottom:1px solid var(--border)}
  .tool-layout{flex-direction:column}
  .tool-form-side{max-height:50vh}
}

@media(max-width:680px){
  .hamburger{display:flex}
  .sidebar{
    position:fixed;top:60px;right:0;bottom:0;z-index:45;
    transform:translateX(100%);width:260px;
  }
  .sidebar.open{transform:translateX(0)}
  .home-wrap{padding:16px}
  .tools-grid{grid-template-columns:1fr 1fr}
  .tool-form-side{padding:16px}
  .chat-messages{padding:14px}
  .gate-card{padding:32px 24px}
}

@media(max-width:400px){
  .tools-grid{grid-template-columns:1fr}
  .tool-layout{flex-direction:column}
}
</style>
</head>
<body>

<!-- GATE -->
<div id="gate">
  <div class="gate-card">
    <div class="gate-logo">🎓</div>
    <h1 class="gate-title"><span>AI Pro</span></h1>
    <p class="gate-sub">مساعدك الذكي للجامعة والتوظيف والبريزنتيشن<br>أدخل Claude API Key عشان تبدأ</p>
    <div class="gate-input-wrap">
      <input type="password" id="gate-key" placeholder="sk-ant-api03-..." autocomplete="off">
      <button class="eye-btn" onclick="toggleEye()" id="eyeBtn">👁</button>
    </div>
    <p class="gate-hint">
      احصل على مفتاحك من
      <a href="https://console.anthropic.com" target="_blank">console.anthropic.com</a>
      &larr; API Keys &larr; Create Key<br>
      المفتاح يُحفظ على جهازك فقط ولا يُرسل لأي جهة
    </p>
    <div class="gate-err" id="gate-err"></div>
    <button class="gate-btn" onclick="enterApp()">ابدأ الاستخدام &larr;</button>
  </div>
</div>

<!-- APP -->
<div id="app">
  <!-- TOP NAV -->
  <div class="topnav">
    <button class="hamburger" id="hamburger" onclick="toggleSidebar()">
      <span></span><span></span><span></span>
    </button>
    <div class="nav-key-badge" onclick="showKeyModal()">
      <span>🔑</span>
      <span id="keyPreview">sk-ant-...</span>
      <span style="color:var(--t3)">تغيير</span>
    </div>
    <div class="nav-logo">
      <span class="nav-logo-text">AI <span>Pro</span></span>
      <div class="nav-logo-icon">🎓</div>
    </div>
  </div>

  <div class="app-body">
    <!-- SIDEBAR -->
    <div class="sidebar" id="sidebar">
      <div class="nav-section">الرئيسية</div>
      <div class="nav-item active" onclick="goTo('home')"><div class="ni">🏠</div>الرئيسية</div>

      <div class="nav-section">التوظيف</div>
      <div class="nav-item" onclick="goTo('cv')"><div class="ni">📄</div>مصمم CV</div>
      <div class="nav-item" onclick="goTo('cover')"><div class="ni">✉️</div>Cover Letter</div>
      <div class="nav-item" onclick="goTo('interview')"><div class="ni">🎤</div>تحضير مقابلة</div>
      <div class="nav-item" onclick="goTo('jobdesc')"><div class="ni">🔍</div>تحليل وصف وظيفي</div>

      <div class="nav-section">الجامعة</div>
      <div class="nav-item" onclick="goTo('summary')"><div class="ni">📝</div>ملخص محاضرات</div>
      <div class="nav-item" onclick="goTo('questions')"><div class="ni">❓</div>أسئلة اختبار</div>
      <div class="nav-item" onclick="goTo('essay')"><div class="ni">✍️</div>تصحيح مقالات</div>
      <div class="nav-item" onclick="goTo('explain')"><div class="ni">💡</div>شرح مفاهيم</div>

      <div class="nav-section">البريزنتيشن</div>
      <div class="nav-item" onclick="goTo('slides')"><div class="ni">🖥️</div>مولّد سلايدات</div>
      <div class="nav-item" onclick="goTo('script')"><div class="ni">🎙️</div>سكريبت العرض</div>
      <div class="nav-item" onclick="goTo('trainer')"><div class="ni">🏋️</div>مدرّب عروض</div>
    </div>

    <div class="overlay" id="overlay" onclick="closeSidebar()"></div>

    <!-- CONTENT -->
    <div class="content" id="content">

      <!-- HOME -->
      <div class="page active" id="page-home">
        <div class="home-wrap">
          <div class="home-hero">
            <h1>أهلاً بك في <span>AI Pro</span> 👋</h1>
            <p>مساعدك الذكي المتكامل للجامعة والتوظيف والبريزنتيشن. اختر الأداة التي تحتاجها وابدأ فوراً.</p>
          </div>
          <div class="tools-section">
            <h2>التوظيف 💼</h2>
            <div class="tools-grid">
              <div class="tool-btn" onclick="goTo('cv')"><div class="tb-icon">📄</div><div class="tb-name">مصمم CV</div><div class="tb-desc">CV احترافي جاهز</div></div>
              <div class="tool-btn" onclick="goTo('cover')"><div class="tb-icon">✉️</div><div class="tb-name">Cover Letter</div><div class="tb-desc">رسالة تقديم مخصصة</div></div>
              <div class="tool-btn" onclick="goTo('interview')"><div class="tb-icon">🎤</div><div class="tb-name">مقابلة عمل</div><div class="tb-desc">أسئلة متوقعة وإجابات</div></div>
              <div class="tool-btn" onclick="goTo('jobdesc')"><div class="tb-icon">🔍</div><div class="tb-name">تحليل وظيفي</div><div class="tb-desc">افهم المتطلبات</div></div>
            </div>
            <h2>الجامعة 🎓</h2>
            <div class="tools-grid">
              <div class="tool-btn" onclick="goTo('summary')"><div class="tb-icon">📝</div><div class="tb-name">ملخص محاضرات</div><div class="tb-desc">نقاط واضحة ومرتبة</div></div>
              <div class="tool-btn" onclick="goTo('questions')"><div class="tb-icon">❓</div><div class="tb-name">أسئلة اختبار</div><div class="tb-desc">استعد للامتحان</div></div>
              <div class="tool-btn" onclick="goTo('essay')"><div class="tb-icon">✍️</div><div class="tb-name">تصحيح مقالات</div><div class="tb-desc">صحّح وحسّن كتابتك</div></div>
              <div class="tool-btn" onclick="goTo('explain')"><div class="tb-icon">💡</div><div class="tb-name">شرح مفاهيم</div><div class="tb-desc">فهم أعمق لأي موضوع</div></div>
            </div>
            <h2>البريزنتيشن 🖥️</h2>
            <div class="tools-grid">
              <div class="tool-btn" onclick="goTo('slides')"><div class="tb-icon">🖥️</div><div class="tb-name">مولّد سلايدات</div><div class="tb-desc">محتوى كامل لكل سلايد</div></div>
              <div class="tool-btn" onclick="goTo('script')"><div class="tb-icon">🎙️</div><div class="tb-name">سكريبت العرض</div><div class="tb-desc">كلام جاهز للتقديم</div></div>
              <div class="tool-btn" onclick="goTo('trainer')"><div class="tb-icon">🏋️</div><div class="tb-name">مدرّب عروض</div><div class="tb-desc">تدرّب قبل العرض</div></div>
            </div>
          </div>
        </div>
      </div>

      <!-- CV -->
      <div class="page" id="page-cv">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>📄 مصمم CV</h2><p>أدخل معلوماتك واحصل على CV احترافي</p></div>
            <div class="row2"><div class="field"><label>الاسم الكامل</label><input id="cv-name" placeholder="محمد الغامدي"></div><div class="field"><label>المسمى المطلوب</label><input id="cv-title" placeholder="مهندس برمجيات"></div></div>
            <div class="row2"><div class="field"><label>البريد</label><input id="cv-email" placeholder="email@example.com" dir="ltr"></div><div class="field"><label>الجوال</label><input id="cv-phone" placeholder="+966 5X..." dir="ltr"></div></div>
            <div class="field"><label>الخبرات العملية</label><textarea id="cv-exp" placeholder="شركة X - مطور - 2022 الى 2024"></textarea></div>
            <div class="field"><label>التعليم</label><textarea id="cv-edu" placeholder="بكالوريوس - جامعة الملك سعود - 2020"></textarea></div>
            <div class="field"><label>المهارات</label><input id="cv-skills" placeholder="Python, React, SQL..."></div>
            <div class="field"><label>اللغة</label><select id="cv-lang"><option value="عربي">عربي</option><option value="إنجليزي">إنجليزي</option></select></div>
            <div class="tool-err" id="cv-err"></div>
            <button class="run-btn" onclick="runTool('cv')">توليد CV ✨</button>
          </div>
          <div class="tool-chat-side" id="cv-chat"><div class="chat-empty"><div class="ce-icon">📄</div><p>أدخل معلوماتك واضغط توليد<br>أو تحدّث مع المساعد لتحسين CV</p></div></div>
        </div>
      </div>

      <!-- COVER -->
      <div class="page" id="page-cover">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>✉️ Cover Letter</h2><p>رسالة تقديم مخصصة للوظيفة</p></div>
            <div class="field"><label>اسمك</label><input id="cl-name" placeholder="محمد عبدالله"></div>
            <div class="field"><label>المسمى الوظيفي</label><input id="cl-job" placeholder="مطور تطبيقات"></div>
            <div class="field"><label>اسم الشركة</label><input id="cl-company" placeholder="شركة أرامكو"></div>
            <div class="field"><label>خبراتك ومهاراتك</label><textarea id="cl-skills" placeholder="3 سنوات خبرة في..."></textarea></div>
            <div class="field"><label>لماذا هذه الوظيفة؟</label><textarea id="cl-why" placeholder="أريد الانضمام لأن..."></textarea></div>
            <div class="field"><label>اللغة</label><select id="cl-lang"><option value="عربي">عربي</option><option value="إنجليزي">إنجليزي</option></select></div>
            <div class="tool-err" id="cover-err"></div>
            <button class="run-btn" onclick="runTool('cover')">توليد الرسالة ✨</button>
          </div>
          <div class="tool-chat-side" id="cover-chat"><div class="chat-empty"><div class="ce-icon">✉️</div><p>أدخل البيانات واضغط توليد<br>أو تحدّث مع المساعد</p></div></div>
        </div>
      </div>

      <!-- INTERVIEW -->
      <div class="page" id="page-interview">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>🎤 تحضير مقابلة</h2><p>أسئلة متوقعة مع نماذج إجابات</p></div>
            <div class="field"><label>الوظيفة</label><input id="int-job" placeholder="محلل بيانات في بنك الرياض"></div>
            <div class="field"><label>مستوى الخبرة</label><select id="int-exp"><option value="حديث تخرج">حديث تخرج</option><option value="1-3 سنوات">1-3 سنوات</option><option value="3-7 سنوات">3-7 سنوات</option><option value="أكثر من 7 سنوات">أكثر من 7 سنوات</option></select></div>
            <div class="field"><label>عدد الأسئلة</label><select id="int-count"><option value="5">5 أسئلة</option><option value="10" selected>10 أسئلة</option><option value="15">15 سؤال</option></select></div>
            <div class="tool-err" id="interview-err"></div>
            <button class="run-btn" onclick="runTool('interview')">توليد الأسئلة ✨</button>
          </div>
          <div class="tool-chat-side" id="interview-chat"><div class="chat-empty"><div class="ce-icon">🎤</div><p>أدخل الوظيفة واضغط توليد<br>أو اسأل المساعد أي سؤال</p></div></div>
        </div>
      </div>

      <!-- JOBDESC -->
      <div class="page" id="page-jobdesc">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>🔍 تحليل وصف وظيفي</h2><p>افهم وش يبحثون عنه بالضبط</p></div>
            <div class="field"><label>وصف الوظيفة</label><textarea id="jd-text" style="min-height:160px" placeholder="الصق نص الوظيفة هنا..."></textarea></div>
            <div class="tool-err" id="jobdesc-err"></div>
            <button class="run-btn" onclick="runTool('jobdesc')">تحليل الوظيفة ✨</button>
          </div>
          <div class="tool-chat-side" id="jobdesc-chat"><div class="chat-empty"><div class="ce-icon">🔍</div><p>الصق الوصف الوظيفي واضغط تحليل</p></div></div>
        </div>
      </div>

      <!-- SUMMARY -->
      <div class="page" id="page-summary">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>📝 ملخص محاضرات</h2><p>لخّص أي محتوى بنقاط واضحة</p></div>
            <div class="field"><label>المحتوى</label><textarea id="sum-text" style="min-height:160px" placeholder="الصق نص المحاضرة..."></textarea></div>
            <div class="field"><label>طول الملخص</label><select id="sum-len"><option value="قصير">قصير - نقاط رئيسية</option><option value="متوسط" selected>متوسط</option><option value="تفصيلي">تفصيلي</option></select></div>
            <div class="tool-err" id="summary-err"></div>
            <button class="run-btn" onclick="runTool('summary')">تلخيص ✨</button>
          </div>
          <div class="tool-chat-side" id="summary-chat"><div class="chat-empty"><div class="ce-icon">📝</div><p>الصق المحتوى واضغط تلخيص</p></div></div>
        </div>
      </div>

      <!-- QUESTIONS -->
      <div class="page" id="page-questions">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>❓ أسئلة اختبار</h2><p>أسئلة متوقعة للمذاكرة</p></div>
            <div class="field"><label>محتوى المادة</label><textarea id="q-text" style="min-height:140px" placeholder="الصق محتوى الفصل..."></textarea></div>
            <div class="row2">
              <div class="field"><label>النوع</label><select id="q-type"><option value="اختيار متعدد">اختيار متعدد</option><option value="مقالي">مقالي</option><option value="صح وخطأ">صح وخطأ</option><option value="مزيج" selected>مزيج</option></select></div>
              <div class="field"><label>العدد</label><select id="q-count"><option value="5">5</option><option value="10" selected>10</option><option value="20">20</option></select></div>
            </div>
            <div class="tool-err" id="questions-err"></div>
            <button class="run-btn" onclick="runTool('questions')">توليد الأسئلة ✨</button>
          </div>
          <div class="tool-chat-side" id="questions-chat"><div class="chat-empty"><div class="ce-icon">❓</div><p>الصق المحتوى واضغط توليد</p></div></div>
        </div>
      </div>

      <!-- ESSAY -->
      <div class="page" id="page-essay">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>✍️ تصحيح مقالات</h2><p>صحّح وحسّن كتابتك الأكاديمية</p></div>
            <div class="field"><label>نص المقالة</label><textarea id="essay-text" style="min-height:160px" placeholder="الصق مقالتك هنا..."></textarea></div>
            <div class="field"><label>اللغة</label><select id="essay-lang"><option value="عربي">عربي</option><option value="إنجليزي">إنجليزي</option></select></div>
            <div class="tool-err" id="essay-err"></div>
            <button class="run-btn" onclick="runTool('essay')">تصحيح وتحسين ✨</button>
          </div>
          <div class="tool-chat-side" id="essay-chat"><div class="chat-empty"><div class="ce-icon">✍️</div><p>الصق مقالتك واضغط تصحيح</p></div></div>
        </div>
      </div>

      <!-- EXPLAIN -->
      <div class="page" id="page-explain">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>💡 شرح مفاهيم</h2><p>فهم عميق لأي موضوع صعب</p></div>
            <div class="field"><label>الموضوع</label><input id="exp-topic" placeholder="نظرية النسبية، الذكاء الاصطناعي..."></div>
            <div class="field"><label>مستواك</label><select id="exp-level"><option value="مبتدئ">مبتدئ</option><option value="متوسط" selected>متوسط - طالب جامعي</option><option value="متقدم">متقدم</option></select></div>
            <div class="tool-err" id="explain-err"></div>
            <button class="run-btn" onclick="runTool('explain')">شرح الموضوع ✨</button>
          </div>
          <div class="tool-chat-side" id="explain-chat"><div class="chat-empty"><div class="ce-icon">💡</div><p>أدخل الموضوع واضغط شرح<br>ثم تحدّث مع المساعد</p></div></div>
        </div>
      </div>

      <!-- SLIDES -->
      <div class="page" id="page-slides">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>🖥️ مولّد سلايدات</h2><p>محتوى كامل لكل سلايد</p></div>
            <div class="field"><label>الموضوع</label><input id="sl-topic" placeholder="تأثير الذكاء الاصطناعي على العمل"></div>
            <div class="row2"><div class="field"><label>عدد السلايدات</label><select id="sl-count"><option value="5">5</option><option value="8" selected>8</option><option value="12">12</option></select></div><div class="field"><label>اللغة</label><select id="sl-lang"><option value="عربي">عربي</option><option value="إنجليزي">إنجليزي</option></select></div></div>
            <div class="field"><label>ملاحظات (اختياري)</label><input id="sl-notes" placeholder="للجمهور الأكاديمي..."></div>
            <div class="tool-err" id="slides-err"></div>
            <button class="run-btn" onclick="runTool('slides')">توليد السلايدات ✨</button>
          </div>
          <div class="tool-chat-side" id="slides-chat"><div class="chat-empty"><div class="ce-icon">🖥️</div><p>أدخل الموضوع واضغط توليد</p></div></div>
        </div>
      </div>

      <!-- SCRIPT -->
      <div class="page" id="page-script">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>🎙️ سكريبت العرض</h2><p>كلام جاهز تقوله مع كل سلايد</p></div>
            <div class="field"><label>الموضوع</label><input id="sc-topic" placeholder="موضوع بريزنتيشنك"></div>
            <div class="field"><label>عناوين السلايدات (سطر لكل سلايد)</label><textarea id="sc-slides" placeholder="مقدمة&#10;الخلفية&#10;التحديات&#10;الحلول&#10;الخلاصة"></textarea></div>
            <div class="field"><label>مدة العرض</label><select id="sc-time"><option value="5 دقائق">5 دقائق</option><option value="10 دقائق" selected>10 دقائق</option><option value="20 دقيقة">20 دقيقة</option></select></div>
            <div class="tool-err" id="script-err"></div>
            <button class="run-btn" onclick="runTool('script')">توليد السكريبت ✨</button>
          </div>
          <div class="tool-chat-side" id="script-chat"><div class="chat-empty"><div class="ce-icon">🎙️</div><p>أدخل البيانات واضغط توليد</p></div></div>
        </div>
      </div>

      <!-- TRAINER -->
      <div class="page" id="page-trainer">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>🏋️ مدرّب عروض</h2><p>تدرّب على تقديم بريزنتيشنك</p></div>
            <div class="field"><label>موضوع بريزنتيشنك</label><input id="tr-topic" placeholder="موضوع عرضك"></div>
            <div class="tool-err" id="trainer-err"></div>
            <button class="run-btn" id="tr-btn" onclick="startTrainer()">ابدأ التدريب ✨</button>
          </div>
          <div class="tool-chat-side" id="trainer-chat"><div class="chat-empty"><div class="ce-icon">🏋️</div><p>أدخل الموضوع واضغط ابدأ التدريب<br>ثم تحدّث مع المدرّب</p></div></div>
        </div>
      </div>

    </div><!-- content -->
  </div><!-- app-body -->
</div><!-- app -->

<!-- KEY MODAL -->
<div id="keyModal">
  <div class="key-modal-card">
    <h3>🔑 تغيير API Key</h3>
    <div class="field"><label>Claude API Key</label><input type="password" id="modal-key" placeholder="sk-ant-..."></div>
    <div class="modal-actions">
      <button class="btn-cancel" onclick="hideKeyModal()">إلغاء</button>
      <button class="btn-save" onclick="saveNewKey()">حفظ</button>
    </div>
  </div>
</div>

<script>
var API_KEY = '';
var chatHistories = {};
var trainerActive = false;

// ===== GATE =====
function toggleEye(){
  var inp = document.getElementById('gate-key');
  var btn = document.getElementById('eyeBtn');
  if(inp.type==='password'){inp.type='text';btn.textContent='🙈';}
  else{inp.type='password';btn.textContent='👁';}
}

function enterApp(){
  var k = document.getElementById('gate-key').value.trim();
  if(!k){showGateErr('أدخل API Key');return;}
  if(!k.startsWith('sk-ant-')){showGateErr('المفتاح يجب أن يبدأ بـ sk-ant-');return;}
  API_KEY = k;
  localStorage.setItem('aipro_key', k);
  document.getElementById('gate').style.display='none';
  document.getElementById('app').classList.add('show');
  document.getElementById('keyPreview').textContent = k.substring(0,14)+'...';
}

function showGateErr(msg){
  var el=document.getElementById('gate-err');
  el.textContent=msg;el.style.display='block';
}

// Check saved key
(function(){
  var saved = localStorage.getItem('aipro_key');
  if(saved&&saved.startsWith('sk-ant-')){
    document.getElementById('gate-key').value=saved;
  }
})();

// ===== KEY MODAL =====
function showKeyModal(){
  document.getElementById('modal-key').value=API_KEY;
  document.getElementById('keyModal').classList.add('show');
}
function hideKeyModal(){document.getElementById('keyModal').classList.remove('show');}
function saveNewKey(){
  var k=document.getElementById('modal-key').value.trim();
  if(!k||!k.startsWith('sk-ant-'))return;
  API_KEY=k;localStorage.setItem('aipro_key',k);
  document.getElementById('keyPreview').textContent=k.substring(0,14)+'...';
  hideKeyModal();
}

// ===== NAVIGATION =====
function goTo(id){
  document.querySelectorAll('.page').forEach(function(p){p.classList.remove('active');});
  document.querySelectorAll('.nav-item').forEach(function(n){n.classList.remove('active');});
  var pg=document.getElementById('page-'+id);
  if(pg)pg.classList.add('active');
  document.querySelectorAll('.nav-item').forEach(function(n){
    if(n.getAttribute('onclick')&&n.getAttribute('onclick').includes("'"+id+"'"))n.classList.add('active');
  });
  closeSidebar();
  // init chat if needed
  if(id!=='home'&&id!=='trainer'){
    initChat(id);
  }
}

function toggleSidebar(){
  var sb=document.getElementById('sidebar');
  var hb=document.getElementById('hamburger');
  var ov=document.getElementById('overlay');
  sb.classList.toggle('open');
  hb.classList.toggle('open');
  ov.classList.toggle('show');
}
function closeSidebar(){
  document.getElementById('sidebar').classList.remove('open');
  document.getElementById('hamburger').classList.remove('open');
  document.getElementById('overlay').classList.remove('show');
}

// ===== CLAUDE API =====
async function callClaude(messages){
  var res = await fetch('https://api.anthropic.com/v1/messages',{
    method:'POST',
    headers:{
      'Content-Type':'application/json',
      'x-api-key':API_KEY,
      'anthropic-version':'2023-06-01',
      'anthropic-dangerous-direct-browser-access':'true'
    },
    body:JSON.stringify({model:'claude-sonnet-4-6',max_tokens:4000,messages:messages})
  });
  var data=await res.json();
  if(data.error)throw new Error(data.error.message);
  return data.content.map(function(i){return i.text||'';}).join('');
}

// ===== CHAT SYSTEM =====
function initChat(toolId){
  var chatEl=document.getElementById(toolId+'-chat');
  if(!chatEl)return;
  if(!chatHistories[toolId]){
    chatHistories[toolId]=[];
    setupChatUI(toolId);
  }
}

function setupChatUI(toolId){
  var chatEl=document.getElementById(toolId+'-chat');
  chatEl.innerHTML='<div class="chat-messages" id="'+toolId+'-msgs"><div class="chat-empty"><div class="ce-icon">💬</div><p>النتيجة ستظهر هنا<br>ويمكنك التحدث مع المساعد لتحسينها</p></div></div><div class="chat-input-bar"><textarea id="'+toolId+'-inp" placeholder="اسأل المساعد أو اطلب تعديل..." rows="1" oninput="autoResize(this)" onkeydown="chatKey(event,\''+toolId+'\')"></textarea><button class="send-btn" id="'+toolId+'-send" onclick="sendChat(\''+toolId+'\')">&#10148;</button></div>';
}

function autoResize(el){
  el.style.height='auto';
  el.style.height=Math.min(el.scrollHeight,120)+'px';
}

function chatKey(e,toolId){
  if(e.key==='Enter'&&!e.shiftKey){e.preventDefault();sendChat(toolId);}
}

function addChatMsg(toolId,role,text){
  var msgsEl=document.getElementById(toolId+'-msgs');
  if(!msgsEl)return;
  // remove empty state
  var empty=msgsEl.querySelector('.chat-empty');
  if(empty)empty.remove();

  var div=document.createElement('div');
  div.className='msg '+role;
  var label=role==='ai'?'المساعد':'أنت';
  var actionsHTML=role==='ai'?'<div class="msg-actions"><button class="msg-copy" onclick="copyMsg(this,\''+escAttr(text)+'\')">نسخ</button></div>':'';
  div.innerHTML='<div class="msg-label">'+label+'</div><div class="msg-bubble">'+escHTML(text)+'</div>'+actionsHTML;
  msgsEl.appendChild(div);
  msgsEl.scrollTop=msgsEl.scrollHeight;
}

function addTyping(toolId){
  var msgsEl=document.getElementById(toolId+'-msgs');
  if(!msgsEl)return;
  var div=document.createElement('div');
  div.className='msg ai';div.id=toolId+'-typing';
  div.innerHTML='<div class="msg-label">المساعد</div><div class="msg-bubble"><div class="typing-indicator"><div class="typing-dot"></div><div class="typing-dot"></div><div class="typing-dot"></div></div></div>';
  msgsEl.appendChild(div);
  msgsEl.scrollTop=msgsEl.scrollHeight;
}

function removeTyping(toolId){
  var el=document.getElementById(toolId+'-typing');
  if(el)el.remove();
}

async function sendChat(toolId){
  var inp=document.getElementById(toolId+'-inp');
  if(!inp)return;
  var msg=inp.value.trim();
  if(!msg)return;
  inp.value='';inp.style.height='auto';

  if(!chatHistories[toolId])chatHistories[toolId]=[];
  addChatMsg(toolId,'user',msg);
  chatHistories[toolId].push({role:'user',content:msg});

  var sendBtn=document.getElementById(toolId+'-send');
  if(sendBtn)sendBtn.disabled=true;
  addTyping(toolId);

  try{
    var reply=await callClaude(chatHistories[toolId]);
    removeTyping(toolId);
    addChatMsg(toolId,'ai',reply);
    chatHistories[toolId].push({role:'assistant',content:reply});
  }catch(e){
    removeTyping(toolId);
    addChatMsg(toolId,'ai','خطأ: '+e.message);
  }finally{
    if(sendBtn)sendBtn.disabled=false;
  }
}

// ===== TOOL PROMPTS =====
function v(id){var el=document.getElementById(id);return el?el.value.trim():'';}

var toolPrompts={
  cv:function(){return 'اكتب CV احترافي '+v('cv-lang')+' لهذا الشخص:\nالاسم: '+v('cv-name')+'\nالمسمى: '+v('cv-title')+'\nالبريد: '+v('cv-email')+'\nالجوال: '+v('cv-phone')+'\nالخبرات: '+v('cv-exp')+'\nالتعليم: '+v('cv-edu')+'\nالمهارات: '+v('cv-skills')+'\n\nاكتب CV كامل منظم وجاهز للاستخدام.';},
  cover:function(){return 'اكتب Cover Letter '+v('cl-lang')+' احترافية:\nالاسم: '+v('cl-name')+'\nالوظيفة: '+v('cl-job')+'\nالشركة: '+v('cl-company')+'\nالخبرات: '+v('cl-skills')+'\nالسبب: '+v('cl-why')+'\n\nاكتب رسالة تقديم مقنعة ومخصصة.';},
  interview:function(){return 'أتقدم لوظيفة: '+v('int-job')+'\nخبرتي: '+v('int-exp')+'\n\nاكتب '+v('int-count')+' سؤال مقابلة متوقع مع نموذج إجابة احترافية لكل سؤال.';},
  jobdesc:function(){return 'حلّل وصف الوظيفة التالي:\n'+v('jd-text')+'\n\nأعطني:\n1- المهارات الأساسية المطلوبة\n2- المهارات الإضافية\n3- نوع الشخصية المطلوبة\n4- الكلمات المفتاحية للـCV\n5- نصيحة للتقديم';},
  summary:function(){return 'لخّص النص التالي تلخيصاً '+v('sum-len')+' بنقاط مرقمة وواضحة:\n\n'+v('sum-text');},
  questions:function(){return 'من المحتوى التالي أنشئ '+v('q-count')+' سؤال من نوع "'+v('q-type')+'" مع الإجابات الصحيحة:\n\n'+v('q-text');},
  essay:function(){return 'صحّح وحسّن المقالة الأكاديمية التالية باللغة '+v('essay-lang')+'.\nأذكر الأخطاء ثم أعد كتابة النص المحسّن:\n\n'+v('essay-text');},
  explain:function(){return 'اشرح "'+v('exp-topic')+'" بأسلوب مناسب لمستوى '+v('exp-level')+'. استخدم أمثلة وتشبيهات مبسطة ونظّم الشرح بشكل واضح.';},
  slides:function(){return 'أنشئ '+v('sl-count')+' سلايد بريزنتيشن احترافية عن: '+v('sl-topic')+'\nاللغة: '+v('sl-lang')+(v('sl-notes')?'\nملاحظات: '+v('sl-notes'):'')+'\n\nلكل سلايد:\n**السلايد [رقم]: [العنوان]**\nالنقاط الرئيسية:\n- ...\nملاحظات المقدّم: ...\n---';},
  script:function(){return 'اكتب سكريبت عرض تقديمي مدته '+v('sc-time')+' عن: '+v('sc-topic')+'\nالسلايدات:\n'+v('sc-slides')+'\n\nاكتب الكلام الذي يقوله المقدّم مع كل سلايد بالتفصيل.';},
};

async function runTool(toolId){
  var err=document.getElementById(toolId+'-err');
  if(err){err.style.display='none';}
  var prompt=toolPrompts[toolId]?toolPrompts[toolId]():'';
  if(!prompt)return;

  // init chat
  if(!chatHistories[toolId]){
    chatHistories[toolId]=[];
    setupChatUI(toolId);
  }

  var btn=document.querySelector('#page-'+toolId+' .run-btn');
  if(btn)btn.disabled=true;

  addChatMsg(toolId,'user','[طلب التوليد]');
  chatHistories[toolId]=[{role:'user',content:prompt}];
  addTyping(toolId);

  try{
    var reply=await callClaude([{role:'user',content:prompt}]);
    removeTyping(toolId);
    // remove the [طلب التوليد] msg
    var msgs=document.getElementById(toolId+'-msgs');
    if(msgs){var userMsgs=msgs.querySelectorAll('.msg.user');if(userMsgs.length)userMsgs[userMsgs.length-1].remove();}
    addChatMsg(toolId,'ai',reply);
    chatHistories[toolId]=[{role:'user',content:prompt},{role:'assistant',content:reply}];
  }catch(e){
    removeTyping(toolId);
    if(err){err.textContent='خطأ: '+e.message;err.style.display='block';}
  }finally{
    if(btn)btn.disabled=false;
  }
}

// ===== TRAINER =====
var trainerHistory=[];

function startTrainer(){
  var topic=v('tr-topic');
  if(!topic){
    var err=document.getElementById('trainer-err');
    err.textContent='أدخل موضوع البريزنتيشن';err.style.display='block';return;
  }
  document.getElementById('trainer-err').style.display='none';
  document.getElementById('tr-btn').disabled=true;
  trainerHistory=[];
  var chatEl=document.getElementById('trainer-chat');
  chatEl.innerHTML='<div class="chat-messages" id="trainer-msgs"></div><div class="chat-input-bar"><textarea id="trainer-inp" placeholder="اكتب إجابتك هنا..." rows="1" oninput="autoResize(this)" onkeydown="trainerKey(event)"></textarea><button class="send-btn" id="trainer-send" onclick="sendTrainer()">&#10148;</button></div>';

  var initPrompt='أنت مدرّب عروض تقديمية محترف وودود. سأقدم بريزنتيشن عن: '+topic+'. ابدأ بترحيب قصير ثم اسألني سؤالاً واحداً لتقييم استعدادي. بعد كل إجابة أعطني تقييماً بنجوم (من 5) ثم سؤالاً جديداً. استمر لـ 5 أسئلة ثم أعطني تقييماً نهائياً.';
  trainerHistory=[{role:'user',content:initPrompt}];
  addTyping('trainer');

  callClaude(trainerHistory).then(function(reply){
    removeTyping('trainer');
    var msgs=document.getElementById('trainer-msgs');
    if(msgs){var empty=msgs.querySelector('.chat-empty');if(empty)empty.remove();}
    addChatMsg('trainer','ai',reply);
    trainerHistory.push({role:'assistant',content:reply});
    document.getElementById('tr-btn').disabled=false;
  }).catch(function(e){
    removeTyping('trainer');
    addChatMsg('trainer','ai','خطأ: '+e.message);
    document.getElementById('tr-btn').disabled=false;
  });
}

function trainerKey(e){
  if(e.key==='Enter'&&!e.shiftKey){e.preventDefault();sendTrainer();}
}

async function sendTrainer(){
  var inp=document.getElementById('trainer-inp');
  if(!inp)return;
  var msg=inp.value.trim();if(!msg)return;
  inp.value='';inp.style.height='auto';
  addChatMsg('trainer','user',msg);
  trainerHistory.push({role:'user',content:msg});
  var sendBtn=document.getElementById('trainer-send');
  if(sendBtn)sendBtn.disabled=true;
  addTyping('trainer');
  try{
    var reply=await callClaude(trainerHistory);
    removeTyping('trainer');
    addChatMsg('trainer','ai',reply);
    trainerHistory.push({role:'assistant',content:reply});
  }catch(e){
    removeTyping('trainer');
    addChatMsg('trainer','ai','خطأ: '+e.message);
  }finally{
    if(sendBtn)sendBtn.disabled=false;
  }
}

// ===== COPY =====
function copyMsg(btn,text){
  navigator.clipboard.writeText(text).then(function(){
    btn.textContent='تم النسخ';btn.classList.add('ok');
    setTimeout(function(){btn.textContent='نسخ';btn.classList.remove('ok');},2000);
  });
}

function escHTML(t){return t.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/\n/g,'<br>');}
function escAttr(t){return t.replace(/'/g,'&#39;').replace(/"/g,'&quot;');}

// Enter on gate
document.getElementById('gate-key').addEventListener('keydown',function(e){if(e.key==='Enter')enterApp();});
</script>
</body>
</html>
