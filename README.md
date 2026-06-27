<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Via AI - مساعدك الذكي</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800;900&display=swap');

*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}

/* نظام الألوان - الوضع الداكن الافتراضي */
:root {
  --bg: #07070e;
  --s1: #0e0e1a;
  --s2: #141420;
  --s3: #1a1a28;
  --border: rgba(255, 255, 255, 0.06);
  --border2: rgba(255, 255, 255, 0.1);
  --p: #7c6dfa;
  --p2: #9d91fb;
  --pg: rgba(124, 109, 250, 0.15);
  --pg2: rgba(124, 109, 250, 0.08);
  --text: #f2f2f8;
  --t2: #aaaacc;
  --t3: #666688;
  --green: #2ecc71;
  --red: #e74c3c;
  --card-bg: #141420;
}

/* نظام الألوان - الوضع الفاتح */
[data-theme="light"] {
  --bg: #f5f6fa;
  --s1: #ffffff;
  --s2: #f0f2f9;
  --s3: #e8eaf4;
  --border: rgba(0, 0, 0, 0.06);
  --border2: rgba(0, 0, 0, 0.1);
  --p: #5b4bf5;
  --p2: #7c6dfa;
  --pg: rgba(91, 75, 245, 0.15);
  --pg2: rgba(91, 75, 245, 0.08);
  --text: #1e1e2f;
  --t2: #4a4a6a;
  --t3: #8888aa;
  --green: #27ae60;
  --red: #c0392b;
  --card-bg: #ffffff;
}

html,body{height:100%;font-family:'Cairo',sans-serif;background:var(--bg);color:var(--text);overflow:hidden;transition: background 0.3s, color 0.3s;}

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
  box-shadow:0 40px 80px rgba(0,0,0,0.3),0 0 0 1px var(--border);
  position:relative;overflow:hidden;
}
.gate-logo{
  width:72px;height:72px;
  background:linear-gradient(135deg,var(--p),#a78bfa);
  border-radius:22px;
  display:flex;align-items:center;justify-content:center;
  font-size:32px;margin:0 auto 24px;
  box-shadow:0 8px 32px rgba(124,109,250,0.4);
}
.gate-title{font-size:26px;font-weight:900;margin-bottom:8px;}
.gate-title span{
  background:linear-gradient(135deg,var(--p),#c4b5fd);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
}
.gate-sub{font-size:14px;color:var(--t2);margin-bottom:32px;line-height:1.7}
.gate-input-wrap{position:relative;margin-bottom:12px}
.gate-input-wrap input{
  width:100%;background:var(--s2);border:1.5px solid var(--border2);
  border-radius:14px;padding:16px 48px 16px 20px;
  font-family:'Cairo',sans-serif;font-size:15px;
  color:var(--text);direction:ltr;outline:none;transition:all 0.2s;
}
.gate-input-wrap input:focus{border-color:var(--p);box-shadow:0 0 0 4px var(--pg)}
.eye-btn{
  position:absolute;left:16px;top:50%;transform:translateY(-50%);
  background:none;border:none;cursor:pointer;color:var(--t3);font-size:18px;
}
.gate-hint{font-size:12px;color:var(--t3);margin-bottom:24px;line-height:1.7}
.gate-hint a{color:var(--p);text-decoration:none}
.gate-btn{
  width:100%;background:linear-gradient(135deg,var(--p),#6d5cf8);
  border:none;border-radius:14px;padding:16px;color:white;
  font-family:'Cairo',sans-serif;font-size:16px;font-weight:700;
  cursor:pointer;transition:all 0.2s;box-shadow:0 8px 24px rgba(124,109,250,0.4);
}

/* ===== APP LAYOUT ===== */
#app{display:none;height:100vh;overflow:hidden;flex-direction:column}
#app.show{display:flex}

.topnav{
  background:var(--s1);border-bottom:1px solid var(--border);
  padding:0 20px;height:60px;display:flex;align-items:center;
  justify-content:space-between;flex-shrink:0;position:relative;z-index:50;
}
.nav-right, .nav-left { display:flex; align-items:center; gap:12px; }
.nav-logo{display:flex;align-items:center;gap:10px;}
.nav-logo-icon{
  width:34px;height:34px;background:linear-gradient(135deg,var(--p),#a78bfa);
  border-radius:10px;display:flex;align-items:center;justify-content:center;
  font-size:15px;box-shadow:0 4px 12px rgba(124,109,250,0.35);
}
.nav-logo-text{font-size:16px;font-weight:900}
.nav-logo-text span{color:var(--p)}

.hamburger{
  background:var(--s2);border:1px solid var(--border2);
  border-radius:10px;width:38px;height:38px;
  display:none;flex-direction:column;gap:4px;
  align-items:center;justify-content:center;cursor:pointer;
}
.hamburger span{width:16px;height:2px;background:var(--t2);border-radius:2px;transition:all 0.3s}
.hamburger.open span:nth-child(1){transform:rotate(45deg) translate(4px,4px)}
.hamburger.open span:nth-child(2){opacity:0}
.hamburger.open span:nth-child(3){transform:rotate(-45deg) translate(4px,-4px)}

.app-body{display:flex;flex:1;overflow:hidden;position:relative;}

/* SIDEBAR */
.sidebar{
  width:240px;min-width:240px;background:var(--s1);
  border-left:1px solid var(--border);overflow-y:auto;
  padding:12px 0 20px;flex-shrink:0;transition:transform 0.3s;
}
.nav-section{font-size:10px;font-weight:700;color:var(--t3);text-transform:uppercase;letter-spacing:1.5px;padding:16px 18px 6px;}
.nav-item{
  display:flex;align-items:center;gap:10px;padding:11px 18px;cursor:pointer;
  font-size:13.5px;font-weight:600;color:var(--t2);transition:all 0.15s;
  border-right:3px solid transparent;user-select:none;
}
.nav-item:hover{background:var(--pg2);color:var(--text)}
.nav-item.active{background:var(--pg);color:var(--p);border-right-color:var(--p)}
.nav-item .ni{
  width:32px;height:32px;border-radius:9px;display:flex;align-items:center;
  justify-content:center;font-size:15px;background:var(--s2);flex-shrink:0;
}

.overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.5);z-index:40;backdrop-filter:blur(2px);}
.overlay.show{display:block}

/* CONTENT CONTAINER */
.content{flex:1;overflow:hidden;display:flex;flex-direction:column;position:relative;}
.page{display:none;flex:1;flex-direction:column;height:100%;overflow-y:auto;}
.page.active{display:flex}

/* HOME */
.home-wrap{padding:24px; max-width:1200px; margin:0 auto; width:100%;}
.home-hero{
  background:linear-gradient(135deg,var(--s2),var(--s3));
  border:1px solid var(--border2);border-radius:24px;padding:32px;margin-bottom:24px;
}
.home-hero h1{font-size:24px;font-weight:900;margin-bottom:8px}
.home-hero h1 span{color:var(--p)}
.home-hero p{font-size:14px;color:var(--t2);line-height:1.7;}
.tools-section h2{font-size:15px;font-weight:700;color:var(--t2);margin-bottom:14px;margin-top:20px;}
.tools-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:14px;margin-bottom:24px}
.tool-btn{
  background:var(--card-bg);border:1px solid var(--border);
  border-radius:16px;padding:20px;cursor:pointer;transition:all 0.2s;text-align:right;
}
.tool-btn:hover{border-color:var(--p);background:var(--pg2);transform:translateY(-2px)}
.tool-btn .tb-icon{font-size:28px;margin-bottom:10px}
.tool-btn .tb-name{font-size:14px;font-weight:700;margin-bottom:4px}
.tool-btn .tb-desc{font-size:12px;color:var(--t3);line-height:1.5}

/* Dynamic Split Layout (Fixed Interlocking Page Bug) */
.tool-layout{display:flex;flex:1;overflow:hidden;height:100%;width:100%;position:relative;}
.tool-form-side{
  width:360px;min-width:360px;border-left:1px solid var(--border);
  overflow-y:auto;padding:24px;flex-shrink:0;background:var(--bg);
}
.tool-chat-side{
  flex:1;display:flex;flex-direction:column;overflow:hidden;background:var(--s1);
}

/* Fields Styling */
.tool-header{margin-bottom:20px}
.tool-header h2{font-size:18px;font-weight:800;margin-bottom:4px}
.tool-header p{font-size:13px;color:var(--t2)}
.field{margin-bottom:14px}
.field label{display:block;font-size:12px;font-weight:700;color:var(--t3);margin-bottom:6px;}
.field input,.field textarea,.field select{
  width:100%;background:var(--s2);border:1.5px solid var(--border2);
  border-radius:11px;padding:12px;font-family:'Cairo',sans-serif;
  font-size:13.5px;color:var(--text);outline:none;transition:all 0.2s;
}
.field input:focus,.field textarea:focus,.field select:focus{border-color:var(--p);box-shadow:0 0 0 3px var(--pg);}
.row2{display:flex;gap:10px}
.row2 .field{flex:1}
.run-btn{
  width:100%;background:linear-gradient(135deg,var(--p),#6d5cf8);
  border:none;border-radius:12px;padding:14px;color:white;
  font-family:'Cairo',sans-serif;font-size:15px;font-weight:700;
  cursor:pointer;transition:all 0.2s;margin-top:10px;
}

/* CHAT AREA */
.chat-messages{flex:1;overflow-y:auto;padding:24px;display:flex;flex-direction:column;gap:16px;}
.chat-empty{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;color:var(--t3);text-align:center;}
.chat-empty .ce-icon{font-size:48px;margin-bottom:12px;opacity:0.5}
.msg{max-width:85%;animation:fadeUp 0.25s ease;display:flex;flex-direction:column;}
@keyframes fadeUp{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}
.msg.ai{align-self:flex-start;align-items: flex-start;}
.msg.user{align-self:flex-end;align-items: flex-end;}
.msg-label{font-size:11px;color:var(--t3);margin-bottom:4px;padding:0 4px}
.msg-bubble{padding:14px 18px;border-radius:18px;font-size:14px;line-height:1.7;white-space:pre-wrap;word-break:break-word;}
.msg.ai .msg-bubble{background:var(--s2);border:1px solid var(--border2);border-radius:0px 18px 18px 18px;}
.msg.user .msg-bubble{background:linear-gradient(135deg,var(--p),#6d5cf8);color:white;border-radius:18px 0px 18px 18px;}
.msg-actions{margin-top:6px;display:flex;gap:8px;}
.msg-copy{background:var(--s2);border:1px solid var(--border2);border-radius:8px;padding:4px 10px;font-size:11px;color:var(--t2);cursor:pointer;}

.chat-input-bar{border-top:1px solid var(--border);padding:14px;background:var(--s1);display:flex;gap:10px;align-items:center;}
.chat-input-bar textarea{
  flex:1;background:var(--s2);border:1.5px solid var(--border2);border-radius:12px;
  padding:12px;font-family:'Cairo',sans-serif;font-size:14px;color:var(--text);
  resize:none;outline:none;max-height:100px;min-height:44px;line-height:1.5;
}
.send-btn{
  width:44px;height:44px;background:linear-gradient(135deg,var(--p),#6d5cf8);
  border:none;border-radius:12px;cursor:pointer;display:flex;align-items:center;justify-content:center;color:white;font-size:16px;
}
.mobile-back-btn {
  display: none; background: var(--s2); border: 1px solid var(--border2);
  padding: 8px 14px; border-radius: 8px; color: var(--text); font-size: 13px;
  font-weight: 600; cursor: pointer; margin-bottom: 12px; width: fit-content;
}

/* SETTINGS & LIBRARY PAGE */
.settings-container { padding: 30px; max-width: 800px; margin: 0 auto; width: 100%; }
.settings-card { background: var(--s1); border: 1px solid var(--border); border-radius: 20px; padding: 24px; margin-bottom: 20px; }
.settings-card h3 { font-size: 16px; font-weight: 800; margin-bottom: 16px; display: flex; align-items: center; gap: 8px; }
.theme-switch-box { display: flex; gap: 10px; }
.theme-btn {
  flex: 1; padding: 12px; border-radius: 10px; border: 1px solid var(--border2);
  background: var(--s2); color: var(--text); font-family: 'Cairo'; font-weight: 700; cursor: pointer; transition: 0.2s;
}
.theme-btn.active { background: var(--p); color: #fff; border-color: var(--p); }

.archive-list { display: flex; flex-direction: column; gap: 12px; margin-top: 10px; }
.archive-item {
  background: var(--s2); border: 1px solid var(--border2); border-radius: 12px; padding: 16px;
  display: flex; flex-direction: column; gap: 8px; position: relative;
}
.archive-meta { display: flex; justify-content: space-between; font-size: 11px; color: var(--t3); font-weight: 700; }
.archive-title { font-size: 13.5px; font-weight: 700; color: var(--text); }
.archive-body { font-size: 12.5px; color: var(--t2); line-height: 1.6; max-height: 80px; overflow: hidden; text-overflow: ellipsis; display: -webkit-box; -webkit-line-clamp: 3; -webkit-box-orient: vertical; }
.archive-actions { display: flex; gap: 8px; margin-top: 4px; }
.arch-btn { background: var(--s1); border: 1px solid var(--border2); padding: 5px 10px; border-radius: 6px; font-size: 11px; color: var(--t2); cursor: pointer; font-family: 'Cairo'; }
.arch-btn.del { color: var(--red); }

/* TYPING */
.typing-indicator{display:flex;gap:4px;align-items:center;padding:10px}
.typing-dot{width:6px;height:6px;background:var(--p);border-radius:50%;animation:bounce 1.2s infinite}
.typing-dot:nth-child(2){animation-delay:0.2s}
.typing-dot:nth-child(3){animation-delay:0.4s}
@keyframes bounce{0%,80%,100%{transform:translateY(0)}40%{transform:translateY(-6px)}}

/* ===== RESPONSIVE CRITICAL FIXES ===== */
@media(max-width:992px){
  .tool-layout { position: relative; }
  /* لمنع تداخل الشاشات: إخفاء جهة المحادثة مؤقتاً حتى يتم الضغط على التوليد */
  .tool-chat-side { position: absolute; inset: 0; z-index: 10; display: none; }
  .tool-chat-side.active-mobile { display: flex; }
  .tool-form-side { width: 100%; min-width: 0; border-left: none; }
  .mobile-back-btn { display: block; }
}

@media(max-width:680px){
  .hamburger{display:flex}
  .sidebar{
    position:fixed;top:60px;right:0;bottom:0;z-index:45;
    transform:translateX(100%);width:260px;
  }
  .sidebar.open{transform:translateX(0)}
  .home-wrap, .settings-container{padding:16px}
  .tools-grid{grid-template-columns:1fr}
}
</style>
</head>
<body>

<!-- GATE -->
<div id="gate">
  <div class="gate-card">
    <div class="gate-logo">✨</div>
    <h1 class="gate-title"><span>Via AI</span></h1>
    <p class="gate-sub">مساعدك الذكي الشامل للجامعة والتوظيف والبريزنتيشن<br>أدخل Claude API Key للمتابعة</p>
    <div class="gate-input-wrap">
      <input type="password" id="gate-key" placeholder="sk-ant-api03-..." autocomplete="off">
      <button class="eye-btn" onclick="toggleEye()" id="eyeBtn">👁</button>
    </div>
    <p class="gate-hint">
      احصل على مفتاحك من 
      <a href="https://console.anthropic.com" target="_blank">console.anthropic.com</a>
    </p>
    <div class="gate-btn" onclick="enterApp()">ابدأ الاستخدام &larr;</div>
  </div>
</div>

<!-- MAIN APP -->
<div id="app">
  <div class="topnav">
    <div class="nav-right">
      <button class="hamburger" id="hamburger" onclick="toggleSidebar()">
        <span></span><span></span><span></span>
      </button>
      <div class="nav-logo">
        <div class="nav-logo-icon">✨</div>
        <span class="nav-logo-text">Via <span>AI</span></span>
      </div>
    </div>
    <div class="nav-left">
      <div class="nav-item" style="padding:0;" onclick="goTo('settings')"><div class="ni" style="margin:0;">⚙️</div></div>
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

      <div class="nav-section">الجامعة</div>
      <div class="nav-item" onclick="goTo('summary')"><div class="ni">📝</div>ملخص محاضرات</div>
      <div class="nav-item" onclick="goTo('questions')"><div class="ni">❓</div>أسئلة اختبار</div>
      <div class="nav-item" onclick="goTo('explain')"><div class="ni">💡</div>شرح مفاهيم</div>

      <div class="nav-section">البريزنتيشن</div>
      <div class="nav-item" onclick="goTo('slides')"><div class="ni">🖥️</div>مولّد سلايدات</div>
      <div class="nav-item" onclick="goTo('script')"><div class="ni">🎙️</div>سكريبت العرض</div>
      
      <div class="nav-section">المنصة</div>
      <div class="nav-item" onclick="goTo('settings')"><div class="ni">⚙️</div>الإعدادات والمكتبة</div>
    </div>

    <div class="overlay" id="overlay" onclick="closeSidebar()"></div>

    <!-- CONTENT AREAS -->
    <div class="content" id="content">

      <!-- HOME PAGE -->
      <div class="page active" id="page-home">
        <div class="home-wrap">
          <div class="home-hero">
            <h1>مرحباً بك في <span>Via AI</span> 👋</h1>
            <p>منصتك الذكية المتكاملة لتسهيل المهام الجامعية، بناء المستقبل الوظيفي، واحتراف العروض التقديمية.</p>
          </div>
          
          <div class="tools-section">
            <h2>التوظيف 💼</h2>
            <div class="tools-grid">
              <div class="tool-btn" onclick="goTo('cv')"><div class="tb-icon">📄</div><div class="tb-name">مصمم CV</div><div class="tb-desc">توليد سيرة ذاتية منظمة واحترافية</div></div>
              <div class="tool-btn" onclick="goTo('cover')"><div class="tb-icon">✉️</div><div class="tb-name">Cover Letter</div><div class="tb-desc">رسالة خطاب تقديم مخصصة ومقنعة</div></div>
              <div class="tool-btn" onclick="goTo('interview')"><div class="tb-icon">🎤</div><div class="tb-name">مقابلة عمل</div><div class="tb-desc">الأسئلة المتوقعة مع نماذج إجاباتها</div></div>
            </div>

            <h2>الجامعة 🎓</h2>
            <div class="tools-grid">
              <div class="tool-btn" onclick="goTo('summary')"><div class="tb-icon">📝</div><div class="tb-name">ملخص محاضرات</div><div class="tb-desc">تلخيص ذكي وشامل للنصوص الأكاديمية</div></div>
              <div class="tool-btn" onclick="goTo('questions')"><div class="tb-icon">❓</div><div class="tb-name">أسئلة اختبار</div><div class="tb-desc">توليد نماذج اختبارات للمذاكرة والمراجعة</div></div>
              <div class="tool-btn" onclick="goTo('explain')"><div class="tb-icon">💡</div><div class="tb-name">شرح مفاهيم</div><div class="tb-desc">تبسيط وشرح أعمق لأعقد النظريات والدروس</div></div>
            </div>

            <h2>البريزنتيشن 🖥️</h2>
            <div class="tools-grid">
              <div class="tool-btn" onclick="goTo('slides')"><div class="tb-icon">🖥️</div><div class="tb-name">مولّد سلايدات</div><div class="tb-desc">تصميم محتوى السلايدات خطوة بخطوة</div></div>
              <div class="tool-btn" onclick="goTo('script')"><div class="tb-icon">🎙️</div><div class="tb-name">سكريبت العرض</div><div class="tb-desc">كتابة النص اللفظي الكامل الذي ستلقيه</div></div>
            </div>
          </div>
        </div>
      </div>

      <!-- CV TOOL -->
      <div class="page" id="page-cv">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>📄 مصمم السيرة الذاتية</h2><p>املأ بياناتك لإنشاء سيرة ذاتية قوية</p></div>
            <div class="row2"><div class="field"><label>الاسم</label><input id="cv-name" placeholder="أحمد عبدالله"></div><div class="field"><label>المسمى المستهدف</label><input id="cv-title" placeholder="مطور واجهات"></div></div>
            <div class="field"><label>الخبرات السابقة</label><textarea id="cv-exp" placeholder="اسم الشركة - الوظيفة - من.. إلى.."></textarea></div>
            <div class="field"><label>التعليم والشهادات</label><textarea id="cv-edu" placeholder="البكالوريوس - التخصص - الجامعة"></textarea></div>
            <div class="field"><label>المهارات الأساسية</label><input id="cv-skills" placeholder="مهارات تقنية أو شخصية"></div>
            <div class="field"><label>اللغة</label><select id="cv-lang"><option value="عربي">العربي</option><option value="إنجليزي">الإنجليزي</option></select></div>
            <button class="run-btn" onclick="runTool('cv')">توليد المحتوى ✨</button>
          </div>
          <div class="tool-chat-side" id="cv-chat"></div>
        </div>
      </div>

      <!-- COVER LETTER TOOL -->
      <div class="page" id="page-cover">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>✉️ الخطاب التعريفي (Cover Letter)</h2><p>صياغة خطاب تقديم مخصص للشركة</p></div>
            <div class="field"><label>اسمك</label><input id="cl-name" placeholder="سارة خالد"></div>
            <div class="field"><label>المسمى الوظيفي المستهدف</label><input id="cl-job" placeholder="أخصائي تسويق"></div>
            <div class="field"><label>اسم الشركة/الجهة</label><input id="cl-company" placeholder="شركة نون"></div>
            <div class="field"><label>أبرز مهاراتك وخبراتك</label><textarea id="cl-skills" placeholder="خبرة سنتين في إدارة الحملات الإعلانية..."></textarea></div>
            <div class="field"><label>اللغة</label><select id="cl-lang"><option value="عربي">العربي</option><option value="إنجليزي">الإنجليزي</option></select></div>
            <button class="run-btn" onclick="runTool('cover')">توليد الخطاب ✨</button>
          </div>
          <div class="tool-chat-side" id="cover-chat"></div>
        </div>
      </div>

      <!-- INTERVIEW TOOL -->
      <div class="page" id="page-interview">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>🎤 تحضير مقابلات العمل</h2><p>توقع الأسئلة الذكية بناءً على تخصصك</p></div>
            <div class="field"><label>المسمى الوظيفي أو المجال</label><input id="int-job" placeholder="مهندس برمجيات، محاسب..."></div>
            <div class="field"><label>مستوى الخبرة</label><select id="int-exp"><option value="حديث تخرج">حديث تخرج</option><option value="متوسط">خبرة متوسطة</option><option value="متقدم">خبير / قيادي</option></select></div>
            <button class="run-btn" onclick="runTool('interview')">توليد الأسئلة والإجابات ✨</button>
          </div>
          <div class="tool-chat-side" id="interview-chat"></div>
        </div>
      </div>

      <!-- SUMMARY TOOL -->
      <div class="page" id="page-summary">
        <div class="tool-layout">
          <div class="tool-layout">
            <div class="tool-form-side">
              <div class="tool-header"><h2>📝 تلخيص المحاضرات والنصوص</h2><p>استخرج الأفكار الرئيسية في ثوانٍ</p></div>
              <div class="field"><label>النص أو محتوى المحاضرة</label><textarea id="sum-text" style="min-height:160px" placeholder="الصق النص هنا..."></textarea></div>
              <button class="run-btn" onclick="runTool('summary')">ابدأ التلخيص ✨</button>
            </div>
            <div class="tool-chat-side" id="summary-chat"></div>
          </div>
        </div>
      </div>

      <!-- QUESTIONS TOOL -->
      <div class="page" id="page-questions">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>❓ مولد أسئلة الاختبارات</h2><p>اختبر معلوماتك قبل الامتحان الفعلي</p></div>
            <div class="field"><label>المادة أو النص الدراسي</label><textarea id="q-text" style="min-height:140px" placeholder="الصق المنهج أو الفصل هنا..."></textarea></div>
            <div class="field"><label>نوع الأسئلة</label><select id="q-type"><option value="مزيج">مزيج (خيارات وصح وخطأ)</option><option value="مقالي">أسئلة مقالية وشرح</option></select></div>
            <button class="run-btn" onclick="runTool('questions')">إنشاء الاختبار ✨</button>
          </div>
          <div class="tool-chat-side" id="questions-chat"></div>
        </div>
      </div>

      <!-- EXPLAIN TOOL -->
      <div class="page" id="page-explain">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>💡 شرح وتبسيط المفاهيم</h2><p>شرح ذكي مدعوم بالأمثلة الواقعية</p></div>
            <div class="field"><label>المفهوم أو النظرية المراد شرحها</label><input id="exp-topic" placeholder="مثال: الحوسبة السحابية، بلوكشين.."></div>
            <div class="field"><label>المستوى الدراسي الحالي</label><select id="exp-level"><option value="مبتدئ">مبتدئ / من الصفر</option><option value="جامعي">طالب جامعي متخصص</option></select></div>
            <button class="run-btn" onclick="runTool('explain')">اشرح لي ✨</button>
          </div>
          <div class="tool-chat-side" id="explain-chat"></div>
        </div>
      </div>

      <!-- SLIDES TOOL -->
      <div class="page" id="page-slides">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>🖥️ مخطط السلايدات والعروض</h2><p>بناء الهيكل النصي لكل شريحة عرض</p></div>
            <div class="field"><label>موضوع البريزنتيشن</label><input id="sl-topic" placeholder="مثال: أمن المعلومات"></div>
            <div class="field"><label>عدد السلايدات المطلوبة</label><select id="sl-count"><option value="5">5 شريحة</option><option value="8">8 شرائح</option><option value="12">12 شريحة</option></select></div>
            <button class="run-btn" onclick="runTool('slides')">توليد الشرائح ✨</button>
          </div>
          <div class="tool-chat-side" id="slides-chat"></div>
        </div>
      </div>

      <!-- SCRIPT TOOL -->
      <div class="page" id="page-script">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>🎙️ كاتِب سكريبت الإلقاء</h2><p>ماذا تقول خلف المايك أثناء العرض</p></div>
            <div class="field"><label>عنوان أو فكرة العرض الرئيسية</label><input id="sc-topic" placeholder="موضوع العرض الرسمي"></div>
            <div class="field"><label>عناوين السلايدات الأساسية (سطر لكل عنوان)</label><textarea id="sc-slides" placeholder="المقدمة&#10;المشكلة&#10;الحل التقني&#10;التوصيات"></textarea></div>
            <button class="run-btn" onclick="runTool('script')">توليد النص اللفظي ✨</button>
          </div>
          <div class="tool-chat-side" id="script-chat"></div>
        </div>
      </div>

      <!-- SETTINGS & LIBRARY PAGE -->
      <div class="page" id="page-settings">
        <div class="settings-container">
          <div class="settings-card">
            <h3>🎨 مظهر المنصة</h3>
            <div class="theme-switch-box">
              <button class="theme-btn active" id="thm-dark" onclick="setTheme('dark')">الوضع الداكن 🌙</button>
              <button class="theme-btn" id="thm-light" onclick="setTheme('light')">الوضع الفاتح ☀️</button>
            </div>
          </div>

          <div class="settings-card">
            <h3>🔑 إدارة مفتاح الربط (API Key)</h3>
            <div class="field" style="margin:0;"><input type="password" id="settings-key-input" placeholder="sk-ant-..." onchange="updateKeyFromSettings()"></div>
          </div>

          <div class="settings-card">
            <h3>📚 مكتبة الأعمال المحفوظة (Archive)</h3>
            <p style="font-size:12px; color:var(--t3); margin-bottom:12px;">يتم هنا حفظ كافة استجابات Via AI الأساسية تلقائياً للرجوع لها لاحقاً.</p>
            <div class="archive-list" id="archiveContainer">
              <!-- الوجت الديناميكي للمكتبة سيظهر هنا -->
            </div>
          </div>
        </div>
      </div>

    </div><!-- content -->
  </div><!-- app-body -->
</div><!-- app -->

<script>
var API_KEY = '';
var chatHistories = {};
var currentTheme = 'dark';

// ===== GATE & AUTH =====
function toggleEye(){
  var inp = document.getElementById('gate-key');
  var btn = document.getElementById('eyeBtn');
  if(inp.type==='password'){inp.type='text';btn.textContent='🙈';}
  else{inp.type='password';btn.textContent='👁';}
}

function enterApp(){
  var k = document.getElementById('gate-key').value.trim();
  if(!k || !k.startsWith('sk-ant-')){alert('يرجى إدخال مفتاح Claude API صحيح يبدأ بـ sk-ant-');return;}
  API_KEY = k;
  localStorage.setItem('via_ai_key', k);
  document.getElementById('gate').style.display='none';
  document.getElementById('app').classList.add('show');
  document.getElementById('settings-key-input').value = k;
  renderArchive();
}

function updateKeyFromSettings() {
  var k = document.getElementById('settings-key-input').value.trim();
  if(k.startsWith('sk-ant-')) {
    API_KEY = k;
    localStorage.setItem('via_ai_key', k);
  }
}

// Check Local Storage on load
(function(){
  var savedKey = localStorage.getItem('via_ai_key');
  if(savedKey && savedKey.startsWith('sk-ant-')){
    document.getElementById('gate-key').value = savedKey;
  }
  var savedTheme = localStorage.getItem('via_ai_theme');
  if(savedTheme) setTheme(savedTheme);
})();

// ===== THEME =====
function setTheme(theme) {
  currentTheme = theme;
  document.documentElement.setAttribute('data-theme', theme);
  localStorage.setItem('via_ai_theme', theme);
  document.getElementById('thm-dark').classList.remove('active');
  document.getElementById('thm-light').classList.remove('active');
  if(theme === 'dark') document.getElementById('thm-dark').classList.add('active');
  else document.getElementById('thm-light').classList.add('active');
}

// ===== NAVIGATION =====
function goTo(id){
  document.querySelectorAll('.page').forEach(function(p){p.classList.remove('active');});
  document.querySelectorAll('.nav-item').forEach(function(n){n.classList.remove('active');});
  
  var pg = document.getElementById('page-'+id);
  if(pg) pg.classList.add('active');
  
  // إخفاء واجهات المحادثة النشطة في الجوال عند التنقل
  document.querySelectorAll('.tool-chat-side').forEach(el => el.classList.remove('active-mobile'));

  document.querySelectorAll('.nav-item').forEach(function(n){
    if(n.getAttribute('onclick') && n.getAttribute('onclick').includes("'"+id+"'")) n.classList.add('active');
  });
  closeSidebar();
  if(id !== 'home' && id !== 'settings'){
    initChat(id);
  }
}

function toggleSidebar(){
  document.getElementById('sidebar').classList.toggle('open');
  document.getElementById('hamburger').classList.toggle('open');
  document.getElementById('overlay').classList.toggle('show');
}
function closeSidebar(){
  document.getElementById('sidebar').classList.remove('open');
  document.getElementById('hamburger').classList.remove('open');
  document.getElementById('overlay').classList.remove('show');
}
function exitMobileChat(toolId) {
  document.getElementById(toolId+'-chat').classList.remove('active-mobile');
}

// ===== CALL CLAUDE API =====
async function callClaude(messages){
  var res = await fetch('https://api.anthropic.com/v1/messages',{
    method:'POST',
    headers:{
      'Content-Type':'application/json',
      'x-api-key':API_KEY,
      'anthropic-version':'2023-06-01',
      'anthropic-dangerous-direct-browser-access':'true'
    },
    body:JSON.stringify({model:'claude-3-5-sonnet-20241022',max_tokens:4000,messages:messages})
  });
  var data = await res.json();
  if(data.error) throw new Error(data.error.message);
  return data.content.map(function(i){return i.text||'';}).join('');
}

// ===== CHAT SYSTEM SYSTEM =====
function initChat(toolId){
  if(!chatHistories[toolId]){
    chatHistories[toolId] = [];
    setupChatUI(toolId);
  }
}

function setupChatUI(toolId){
  var chatEl = document.getElementById(toolId+'-chat');
  if(!chatEl) return;
  chatEl.innerHTML = `
    <div class="chat-messages" id="${toolId}-msgs">
      <div class="chat-empty">
        <div class="mobile-back-btn" onclick="exitMobileChat('${toolId}')">⬅️ العودة للنموذج</div>
        <div class="ce-icon">💬</div>
        <p>النتيجة ومتابعة النقاش والتعديلات ستظهر هنا</p>
      </div>
    </div>
    <div class="chat-input-bar">
      <textarea id="${toolId}-inp" placeholder="اطلب تعديل، إضافة أو تحسين على النتيجة..." rows="1" onkeydown="chatKey(event,'${toolId}')"></textarea>
      <button class="send-btn" id="${toolId}-send" onclick="sendChat('${toolId}')">↩️</button>
    </div>
  `;
}

function chatKey(e,toolId){
  if(e.key==='Enter' && !e.shiftKey){e.preventDefault(); sendChat(toolId);}
}

function addChatMsg(toolId,role,text){
  var msgsEl = document.getElementById(toolId+'-msgs');
  if(!msgsEl) return;
  var empty = msgsEl.querySelector('.chat-empty');
  if(empty && role === 'user') empty.remove();

  var div = document.createElement('div');
  div.className = 'msg ' + role;
  var label = role === 'ai' ? 'Via AI' : 'أنت';
  var actionsHTML = role === 'ai' ? `<div class="msg-actions"><button class="msg-copy" onclick="copyMsg(this,\`${escAttr(text)}\`)">نسخ النص</button></div>` : '';
  
  // زر رجوع للجوال في أول رسالة من الـ AI
  var backBtnMobile = (role==='ai' && msgsEl.children.length <= 1) ? `<button class="mobile-back-btn" onclick="exitMobileChat('${toolId}')" style="margin-top:0; margin-bottom:10px;">⬅️ تعديل الحقول</button>` : '';

  div.innerHTML = backBtnMobile + '<div class="msg-label">'+label+'</div><div class="msg-bubble">'+escHTML(text)+'</div>'+actionsHTML;
  msgsEl.appendChild(div);
  msgsEl.scrollTop = msgsEl.scrollHeight;
}

function addTyping(toolId){
  var msgsEl = document.getElementById(toolId+'-msgs');
  if(!msgsEl) return;
  var div = document.createElement('div');
  div.className = 'msg ai'; div.id = toolId+'-typing';
  div.innerHTML = '<div class="msg-label">Via AI جاري التفكير...</div><div class="msg-bubble"><div class="typing-indicator"><div class="typing-dot"></div><div class="typing-dot"></div><div class="typing-dot"></div></div></div>';
  msgsEl.appendChild(div);
  msgsEl.scrollTop = msgsEl.scrollHeight;
}

function removeTyping(toolId){
  var el = document.getElementById(toolId+'-typing');
  if(el) el.remove();
}

async function sendChat(toolId){
  var inp = document.getElementById(toolId+'-inp');
  if(!inp) return;
  var msg = inp.value.trim(); if(!msg) return;
  inp.value = '';

  addChatMsg(toolId,'user',msg);
  chatHistories[toolId].push({role:'user',content:msg});

  var sendBtn = document.getElementById(toolId+'-send');
  if(sendBtn) sendBtn.disabled = true;
  addTyping(toolId);

  try{
    var reply = await callClaude(chatHistories[toolId]);
    removeTyping(toolId);
    addChatMsg(toolId,'ai',reply);
    chatHistories[toolId].push({role:'assistant',content:reply});
  }catch(e){
    removeTyping(toolId);
    addChatMsg(toolId,'ai','حدث خطأ بالاتصال: ' + e.message);
  }finally{
    if(sendBtn) sendBtn.disabled = false;
  }
}

// ===== PROMPTS LOGIC =====
function v(id){var el=document.getElementById(id); return el?el.value.trim():'';}

var toolPrompts = {
  cv: function(){return `صمم سيرة ذاتية (CV) احترافية ومتناسقة باللغة ${v('cv-lang')} للبيانات التالية:\nالاسم: ${v('cv-name')}\nالمسمى الوظيفي: ${v('cv-title')}\nالخبرات: ${v('cv-exp')}\nالتعليم: ${v('cv-edu')}\nالمهارات: ${v('cv-skills')}.\nأخرجها بهيكل نصي منسق جداً وجاهز للنسخ.`;},
  cover: function(){return `اكتب رسالة خطاب تقديم (Cover Letter) احترافية باللغة ${v('cl-lang')} موجهة إلى ${v('cl-company')} بخصوص وظيفة ${v('cl-job')} بناء على المهارات التالية:\n${v('cl-skills')}`;},
  interview: function(){return `أنا مقبل على مقابلة شخصية لوظيفة ${v('int-job')} بمستوى خبرة ${v('int-exp')}. اكتب لي أهم 7 أسئلة متوقعة ومثيرة للذكاء مع صياغة نموذج إجابة احترافي ومثالي لكل سؤال.`;},
  summary: function(){return `قم بتلخيص النص الأكاديمي التالي تلخيصاً ذكياً وشاملاً مع الحفاظ على المصطلحات الهامة واستخراجها كأفكار رئيسية ومرتبة بنقاط:\n\n${v('sum-text')}`;},
  questions: function(){return `بناءً على المحتوى التالي، قم بتوليد أسئلة اختبار من نوع (${v('q-type')}) لقياس الفهم والاستيعاب مع إرفاق نموذج الإجابة النموذجي لكل سؤال:\n\n${v('q-text')}`;},
  explain: function(){return `اشرح وبسط المفهوم التالي: "${v('exp-topic')}" بحيث يكون الشرح ملائماً ومخصصاً ومفهوماً لمستوى طالب (${v('exp-level')})، مع إرفاق أمثلة توضيحية لتسهيل استيعاب الفكرة الحركية للمفهوم.`;},
  slides: function(){return `أنشئ مخططاً نصياً وعناوين لبريزنتيشن يتكون من ${v('sl-count')} شرائح (Slides) حول موضوع: "${v('sl-topic')}". لكل شريحة اكتب: عنوان الشريحة، الأفكار الرئيسية المختصرة في نقاط، وملاحظات جانبية للمتحدث (Presenters notes).`;},
  script: function(){return `اكتب سكريبت إلقاء لفظي كامل ومفصل بالعامية المثقفة أو الفصحى المبسطة لعرض تقديمي حول موضوع: "${v('sc-topic')}". الشرائح المتوفرة هي:\n${v('sc-slides')}\nاكتب نص الإلقاء الذي سأقوله حرفياً أمام الحضور مع كل شريحة.`;}
};

async function runTool(toolId){
  var prompt = toolPrompts[toolId] ? toolPrompts[toolId]() : '';
  if(!prompt) return;

  // إظهار واجهة المحادثة فوراً في الجوال لمنع التداخل وحوسة الشاشات
  document.getElementById(toolId+'-chat').classList.add('active-mobile');

  initChat(toolId);
  var btn = document.querySelector('#page-'+toolId+' .run-btn');
  if(btn) btn.disabled = true;

  var msgsContainer = document.getElementById(toolId+'-msgs');
  if(msgsContainer) msgsContainer.innerHTML = ''; 

  addTyping(toolId);

  try{
    var reply = await callClaude([{role:'user',content:prompt}]);
    removeTyping(toolId);
    addChatMsg(toolId,'ai',reply);
    chatHistories[toolId] = [{role:'user',content:prompt},{role:'assistant',content:reply}];
    
    // حفظ في المكتبة تلقائياً
    saveToArchive(toolId, reply);
  }catch(e){
    removeTyping(toolId);
    addChatMsg(toolId,'ai','فشل التوليد: '+e.message);
  }finally{
    if(btn) btn.disabled = false;
  }
}

// ===== ARCHIVE & LIBRARY LIBRARY LOGIC =====
function saveToArchive(toolId, text) {
  var archive = JSON.parse(localStorage.getItem('via_ai_archive') || '[]');
  var titleMap = {cv:'سيرة ذاتية', cover:'خطاب تقديم', interview:'تحضير مقابلة', summary:'تلخيص محاضرة', questions:'أسئلة اختبار', explain:'شرح مفهوم', slides:'شرائح عرض', script:'سكريبت إلقاء'};
  var item = {
    id: Date.now(),
    tool: titleMap[toolId] || toolId,
    date: new Date().toLocaleDateString('ar-EG', {hour:'2-digit', minute:'2-digit'}),
    content: text
  };
  archive.unshift(item);
  localStorage.setItem('via_ai_archive', JSON.stringify(archive));
  renderArchive();
}

function renderArchive() {
  var container = document.getElementById('archiveContainer');
  if(!container) return;
  var archive = JSON.parse(localStorage.getItem('via_ai_archive') || '[]');
  if(archive.length === 0) {
    container.innerHTML = '<p style="font-size:13px; color:var(--t3); text-align:center; padding:20px;">المكتبة فارغة حالياً، أي عمل تقوم بتوليده سيحفظ هنا تلقائياً.</p>';
    return;
  }
  container.innerHTML = '';
  archive.forEach(function(item) {
    var div = document.createElement('div');
    div.className = 'archive-item';
    div.innerHTML = `
      <div class="archive-meta"><span>${item.tool}</span><span>${item.date}</span></div>
      <div class="archive-body" id="arch-body-${item.id}">${escHTML(item.content)}</div>
      <div class="archive-actions">
        <button class="arch-btn" onclick="copyMsg(this,\`${escAttr(item.content)}\`)">نسخ النص</button>
        <button class="arch-btn del" onclick="deleteArchive(${item.id})">حذف</button>
      </div>
    `;
    container.appendChild(div);
  });
}

function deleteArchive(id) {
  var archive = JSON.parse(localStorage.getItem('via_ai_archive') || '[]');
  archive = archive.filter(item => item.id !== id);
  localStorage.setItem('via_ai_archive', JSON.stringify(archive));
  renderArchive();
}

// ===== HELPERS =====
function copyMsg(btn,text){
  navigator.clipboard.writeText(text).then(function(){
    var old = btn.textContent; btn.textContent='تم النسخ! ✓';
    setTimeout(function(){btn.textContent = old;},2000);
  });
}
function escHTML(t){return t.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/\n/g,'<br>');}
function escAttr(t){return t.replace(/'/g,'&#39;').replace(/"/g,'&quot;').replace(/`/g,'&#96;');}
document.getElementById('gate-key').addEventListener('keydown',function(e){if(e.key==='Enter')enterApp();});
</script>
</body>
</html>
