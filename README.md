<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Via AI - انتاج سعودي </title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800;900&display=swap');

*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}

/* نظام الألوان الفخم - الوضع الداكن الملكي */
:root {
  --bg: #09090b;
  --s1: #121218;
  --s2: #181825;
  --s3: #1f1f30;
  --border: rgba(255, 255, 255, 0.05);
  --border2: rgba(255, 255, 255, 0.09);
  --p: #8b5cf6;
  --p2: #a78bfa;
  --pg: rgba(139, 92, 246, 0.15);
  --pg2: rgba(139, 92, 246, 0.05);
  --text: #f4f4f5;
  --t2: #a1a1aa;
  --t3: #71717a;
  --green: #10b981;
  --red: #ef4444;
  --card-bg: #121218;
  --glow: rgba(139, 92, 246, 0.2);
}

/* نظام الألوان الفخم - الوضع الفاتح النقي */
[data-theme="light"] {
  --bg: #f8fafc;
  --s1: #ffffff;
  --s2: #f1f5f9;
  --s3: #e2e8f0;
  --border: rgba(0, 0, 0, 0.04);
  --border2: rgba(0, 0, 0, 0.08);
  --p: #6d28d9;
  --p2: #8b5cf6;
  --pg: rgba(109, 40, 217, 0.08);
  --pg2: rgba(109, 40, 217, 0.03);
  --text: #0f172a;
  --t2: #475569;
  --t3: #94a3b8;
  --green: #059669;
  --red: #dc2626;
  --card-bg: #ffffff;
  --glow: rgba(109, 40, 217, 0.05);
}

html,body{height:100%;font-family:'Cairo',sans-serif;background:var(--bg);color:var(--text);overflow:hidden;transition: background 0.4s ease, color 0.4s ease;}

/* ===== الرموز والأيقونات المخصصة الراقية عبر الـ CSS ===== */
.icon-premium { display: inline-block; width: 18px; height: 18px; border: 2px solid currentColor; border-radius: 4px; position: relative; vertical-align: middle;}
.icon-home::before { content: ''; position: absolute; inset: 2px; background: currentColor; opacity: 0.3; }
.icon-cv { border-right: 5px solid currentColor; }
.icon-cover { border-bottom: 5px solid currentColor; }
.icon-interview { border-radius: 50%; }
.icon-summary { height: 12px; }
.icon-questions { border-style: dashed; }
.icon-explain { transform: rotate(45deg); }
.icon-slides { border-width: 2px 2px 5px 2px; }
.icon-script { border-radius: 0 4px 0 4px; }
.icon-email { background: currentColor; opacity: 0.2; }
.icon-kpi { border-width: 3px; }
.icon-ats { border-radius: 50% 0 50% 50%; }
.icon-solve { transform: scale(0.9); }

/* ===== بوابة تسجيل المفتاح الفاخرة ===== */
#gate{
  position:fixed;inset:0;z-index:9999;
  background:var(--bg);
  display:flex;align-items:center;justify-content:center;
  padding:20px;
}
.gate-card{
  width:100%;max-width:460px;
  background:var(--s1);
  border:1px solid var(--border2);
  border-radius:24px;
  padding:50px 40px;
  text-align:center;
  box-shadow: 0 25px 50px -12px rgba(0,0,0,0.5);
  position:relative;overflow:hidden;
}
.gate-card::before {
  content: ''; position: absolute; top: 0; left: 50%; transform: translateX(-50%);
  width: 150px; height: 1px; background: linear-gradient(90deg, transparent, var(--p), transparent);
}
.gate-logo{
  width:64px;height:64px;
  background: linear-gradient(135deg, var(--s2), var(--s3));
  border: 1px solid var(--border2);
  border-radius:20px;
  display:flex;align-items:center;justify-content:center;
  margin:0 auto 24px; color: var(--p); font-weight: 800; font-size: 24px;
}
.gate-title{font-size:28px;font-weight:900;margin-bottom:10px; letter-spacing: -0.5px;}
.gate-title span{
  background:linear-gradient(135deg,var(--p),#c4b5fd);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
}
.gate-sub{font-size:13px;color:var(--t2);margin-bottom:32px;line-height:1.8}
.gate-input-wrap{position:relative;margin-bottom:20px}
.gate-input-wrap input{
  width:100%;background:var(--s2);border:1px solid var(--border2);
  border-radius:14px;padding:16px 48px 16px 20px;
  font-family:'Cairo',sans-serif;font-size:14px;
  color:var(--text);direction:ltr;outline:none;transition:all 0.3s;
}
.gate-input-wrap input:focus{border-color:var(--p); box-shadow: 0 0 20px var(--glow);}
.eye-btn{
  position:absolute;left:16px;top:50%;transform:translateY(-50%);
  background:none;border:none;cursor:pointer;color:var(--t3);font-size:16px;
}
.gate-btn{
  width:100%;background: var(--p);
  border:none;border-radius:14px;padding:16px;color:white;
  font-family:'Cairo',sans-serif;font-size:15px;font-weight:700;
  cursor:pointer;transition:all 0.3s;
}
.gate-btn:hover { background: var(--p2); transform: translateY(-1px); }

/* ===== الهيكل الرئيسي للتطبيق ===== */
#app{display:none;height:100vh;overflow:hidden;flex-direction:column}
#app.show{display:flex}

.topnav{
  background:var(--s1);border-bottom:1px solid var(--border);
  padding:0 24px;height:64px;display:flex;align-items:center;
  justify-content:space-between;flex-shrink:0;position:relative;z-index:50;
}
.nav-right, .nav-left { display:flex; align-items:center; gap:16px; }
.nav-logo{display:flex;align-items:center;gap:12px;}
.nav-logo-icon{
  width:32px;height:32px;background: var(--s2); border: 1px solid var(--border2);
  border-radius:8px;display:flex;align-items:center;justify-content:center;
  color: var(--p); font-weight: 900; font-size: 14px;
}
.nav-logo-text{font-size:18px;font-weight:900; letter-spacing: -0.5px;}
.nav-logo-text span{color:var(--p)}

.hamburger{
  background:transparent; border: none;
  display:none; flex-direction:column; gap:5px;
  cursor:pointer; padding: 10px; margin-right: -10px;
}
.hamburger span{width:20px;height:2px;background:var(--text);border-radius:2px;transition:all 0.3s}
.hamburger.open span:nth-child(1){transform:rotate(45deg) translate(5px,5px)}
.hamburger.open span:nth-child(2){opacity:0}
.hamburger.open span:nth-child(3){transform:rotate(-45deg) translate(5px,-5px)}

.app-body{display:flex;flex:1;overflow:hidden;position:relative;}

/* القائمة الجانبية الفاخرة */
.sidebar{
  width:260px;min-width:260px;background:var(--s1);
  border-left:1px solid var(--border);overflow-y:auto;
  padding:20px 0;flex-shrink:0;transition:transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
.sidebar-header-mobile { display: none; padding: 0 24px 20px; border-bottom: 1px solid var(--border); margin-bottom: 10px; }
.nav-section{font-size:11px;font-weight:700;color:var(--t3);text-transform:uppercase;letter-spacing:1.5px;padding:18px 24px 8px;}
.nav-item{
  display:flex;align-items:center;gap:14px;padding:12px 24px;cursor:pointer;
  font-size:14px;font-weight:600;color:var(--t2);transition:all 0.2s;
  border-right:3px solid transparent;user-select:none;
}
.nav-item:hover{background:var(--pg2);color:var(--text)}
.nav-item.active{background:var(--pg);color:var(--p);border-right-color:var(--p);font-weight:700;}
.nav-item .ni{
  width:28px;height:28px;border-radius:6px;display:flex;align-items:center;
  justify-content:center;background:var(--s2);color: inherit; flex-shrink:0; transition: all 0.2s;
}
.nav-item.active .ni { background: var(--p); color: #fff; }

.overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.6);z-index:40;backdrop-filter:blur(4px); animation: fadeIn 0.2s ease;}
@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
.overlay.show{display:block}

/* حاويات المحتوى والأدوات */
.content{flex:1;overflow:hidden;display:flex;flex-direction:column;position:relative;background: var(--bg);}
.page{display:none;flex:1;flex-direction:column;height:100%;overflow-y:auto;}
.page.active{display:flex}

/* الصفحة الرئيسية الفخمة */
.home-wrap{padding:40px 24px; max-width:1100px; margin:0 auto; width:100%;}
.home-hero{
  background: linear-gradient(135deg, var(--s1), var(--s2));
  border:1px solid var(--border2);border-radius:20px;padding:40px;margin-bottom:40px;
  box-shadow: 0 10px 30px -10px rgba(0,0,0,0.3); position: relative; overflow: hidden;
}
.home-hero::after {
  content: ''; position: absolute; top: -50%; left: -50%; width: 100%; height: 100%;
  background: radial-gradient(circle, var(--glow) 0%, transparent 70%); pointer-events: none;
}
.home-hero h1{font-size:28px;font-weight:900;margin-bottom:12px; letter-spacing: -0.5px;}
.home-hero h1 span{color:var(--p)}
.home-hero p{font-size:14.5px;color:var(--t2);line-height:1.8; max-width: 600px;}

.tools-section h2{font-size:16px;font-weight:800;color:var(--text);margin-bottom:20px;margin-top:30px; position: relative; padding-right: 12px;}
.tools-section h2::before { content: ''; position: absolute; right: 0; top: 20%; bottom: 20%; width: 3px; background: var(--p); border-radius: 2px; }
.tools-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(240px,1fr));gap:16px;margin-bottom:30px}
.tool-btn{
  background:var(--card-bg);border:1px solid var(--border);
  border-radius:16px;padding:24px;cursor:pointer;transition:all 0.25s cubic-bezier(0.4, 0, 0.2, 1);text-align:right;
  box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1);
}
.tool-btn:hover{border-color:var(--p);background:var(--s2);transform:translateY(-3px); box-shadow: 0 12px 20px -5px rgba(0,0,0,0.2), 0 0 15px var(--glow);}
.tool-btn .tb-icon{font-size:20px; margin-bottom:16px; color: var(--p); background: var(--pg); width: 40px; height: 40px; border-radius: 10px; display: flex; align-items: center; justify-content: center;}
.tool-btn .tb-name{font-size:15px;font-weight:700;margin-bottom:6px; color: var(--text);}
.tool-btn .tb-desc{font-size:12.5px;color:var(--t2);line-height:1.6}

/* تصميم تقسيم النوافذ الذكي والمعزول */
.tool-layout{display:flex;flex:1;overflow:hidden;height:100%;width:100%;position:relative;}
.tool-form-side{
  width:380px;min-width:380px;border-left:1px solid var(--border);
  overflow-y:auto;padding:30px 24px;flex-shrink:0;background:var(--bg);
}
.tool-chat-side{
  flex:1;display:flex;flex-direction:column;overflow:hidden;background:var(--s1);
}

/* عناصر الحقول الراقية */
.tool-header{margin-bottom:24px}
.tool-header h2{font-size:20px;font-weight:800;margin-bottom:6px; letter-spacing: -0.5px;}
.tool-header p{font-size:13px;color:var(--t2); line-height: 1.6;}
.field{margin-bottom:18px}
.field label{display:block;font-size:12px;font-weight:700;color:var(--t3);margin-bottom:8px; text-transform: uppercase; letter-spacing: 0.5px;}
.field input,.field textarea,.field select{
  width:100%;background:var(--s2);border:1px solid var(--border2);
  border-radius:12px;padding:14px;font-family:'Cairo',sans-serif;
  font-size:14px;color:var(--text);outline:none;transition:all 0.2s ease;
}
.field input:focus,.field textarea:focus,.field select:focus{border-color:var(--p);box-shadow: 0 0 12px var(--glow); background: var(--s3);}
.row2{display:flex;gap:12px}
.row2 .field{flex:1}
.run-btn{
  width:100%;background: var(--p);
  border:none;border-radius:12px;padding:16px;color:white;
  font-family:'Cairo',sans-serif;font-size:15px;font-weight:700;
  cursor:pointer;transition:all 0.2s;margin-top:10px;
}
.run-btn:hover { background: var(--p2); transform: translateY(-1px); }

/* منطقة شاشة الدردشة والتوليد */
.chat-messages{flex:1;overflow-y:auto;padding:30px;display:flex;flex-direction:column;gap:20px;}
.chat-empty{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;color:var(--t3);text-align:center; padding: 20px;}
.chat-empty .ce-icon{width: 48px; height: 48px; border: 2px solid var(--border2); border-radius: 12px; display: flex; align-items: center; justify-content: center; font-size: 20px; margin-bottom: 16px; color: var(--t3);}
.msg{max-width:85%;animation:fadeUp 0.3s cubic-bezier(0.4, 0, 0.2, 1);display:flex;flex-direction:column;}
@keyframes fadeUp{from{opacity:0;transform:translateY(12px)}to{opacity:1;transform:translateY(0)}}
.msg.ai{align-self:flex-start;align-items: flex-start;}
.msg.user{align-self:flex-end;align-items: flex-end;}
.msg-label{font-size:11px;color:var(--t3);margin-bottom:6px;font-weight:700;letter-spacing: 0.5px;}
.msg-bubble{padding:16px 20px;border-radius:16px;font-size:14.5px;line-height:1.7;white-space:pre-wrap;word-break:break-word;}
.msg.ai .msg-bubble{background:var(--s2);border:1px solid var(--border2);border-radius:0px 16px 16px 16px; color: var(--text);}
.msg.user .msg-bubble{background: var(--p); color:white;border-radius:16px 0px 16px 16px;}
.msg-actions{margin-top:8px;display:flex;gap:8px;}
.msg-copy{background:var(--s2);border:1px solid var(--border2);border-radius:8px;padding:6px 12px;font-size:12px;color:var(--t2);cursor:pointer; font-family: 'Cairo';}
.msg-copy:hover { border-color: var(--p); color: var(--text); }

.chat-input-bar{border-top:1px solid var(--border);padding:16px 24px;background:var(--s1);display:flex;gap:12px;align-items:center;}
.chat-input-bar textarea{
  flex:1;background:var(--s2);border:1px solid var(--border2);border-radius:12px;
  padding:14px;font-family:'Cairo',sans-serif;font-size:14px;color:var(--text);
  resize:none;outline:none;max-height:100px;min-height:48px;line-height:1.5;
}
.send-btn{
  width:48px;height:48px;background: var(--p);
  border:none;border-radius:12px;cursor:pointer;display:flex;align-items:center;justify-content:center;color:white;font-size:14px; transition: 0.2s;
}
.send-btn:hover { background: var(--p2); transform: scale(1.02); }
.mobile-back-btn {
  display: none; background: var(--s2); border: 1px solid var(--border2);
  padding: 10px 16px; border-radius: 10px; color: var(--text); font-size: 13px;
  font-weight: 700; cursor: pointer; margin-bottom: 20px; width: fit-content; font-family: 'Cairo';
}

/* صفحة الإعدادات الفاخرة والمكتبة */
.settings-container { padding: 40px 24px; max-width: 800px; margin: 0 auto; width: 100%; }
.settings-card { background: var(--s1); border: 1px solid var(--border); border-radius: 20px; padding: 28px; margin-bottom: 24px; }
.settings-card h3 { font-size: 16px; font-weight: 800; margin-bottom: 18px; display: flex; align-items: center; gap: 10px; }
.theme-switch-box { display: flex; gap: 12px; }
.theme-btn {
  flex: 1; padding: 14px; border-radius: 12px; border: 1px solid var(--border2);
  background: var(--s2); color: var(--text); font-family: 'Cairo'; font-weight: 700; cursor: pointer; transition: 0.2s;
}
.theme-btn.active { background: var(--p); color: #fff; border-color: var(--p); box-shadow: 0 0 15px var(--glow); }

.archive-list { display: flex; flex-direction: column; gap: 14px; margin-top: 16px; }
.archive-item {
  background: var(--s2); border: 1px solid var(--border2); border-radius: 14px; padding: 20px;
  display: flex; flex-direction: column; gap: 10px; position: relative;
}
.archive-meta { display: flex; justify-content: space-between; font-size: 11px; color: var(--t3); font-weight: 800; text-transform: uppercase; letter-spacing: 0.5px; }
.archive-title { font-size: 14px; font-weight: 700; color: var(--text); }
.archive-body { font-size: 13px; color: var(--t2); line-height: 1.7; max-height: 80px; overflow: hidden; text-overflow: ellipsis; display: -webkit-box; -webkit-line-clamp: 3; -webkit-box-orient: vertical; }
.archive-actions { display: flex; gap: 8px; margin-top: 6px; }
.arch-btn { background: var(--s1); border: 1px solid var(--border2); padding: 6px 14px; border-radius: 8px; font-size: 12px; color: var(--t2); cursor: pointer; font-family: 'Cairo'; font-weight: 600; transition: 0.2s; }
.arch-btn:hover { border-color: var(--p); color: var(--text); }
.arch-btn.del { color: var(--red); }
.arch-btn.del:hover { background: rgba(239, 68, 68, 0.05); border-color: var(--red); }

/* المؤشر الذكي للـ Typing */
.typing-indicator{display:flex;gap:4px;align-items:center;padding:6px}
.typing-dot{width:6px;height:6px;background:var(--p);border-radius:50%;animation:bounce 1.2s infinite}
.typing-dot:nth-child(2){animation-delay:0.2s}
.typing-dot:nth-child(3){animation-delay:0.4s}
@keyframes bounce{0%,80%,100%{transform:translateY(0)}40%{transform:translateY(-6px)}}

/* ===== التجاوب وحل مشكلة الشاشات والجوال تماماً ===== */
@media(max-width:992px){
  .tool-layout { position: relative; }
  /* عزل تام لشاشة الدردشة حتى لا تتداخل وتخرب الحقول في الجوال */
  .tool-chat-side { position: absolute; inset: 0; z-index: 10; display: none; }
  .tool-chat-side.active-mobile { display: flex; z-index: 60; }
  .tool-form-side { width: 100%; min-width: 0; border-left: none; padding: 20px; }
  .mobile-back-btn { display: block; }
}

@media(max-width:768px){
  .hamburger{display:flex}
  /* إخفاء القائمة الجانبية تماماً وتجهيزها للظهور فوق المحتوى */
  .sidebar{
    position:fixed;top:0;bottom:0;right:0;z-index:100;
    transform:translateX(100%);width:280px; box-shadow: -10px 0 30px rgba(0,0,0,0.5);
    border-left: 1px solid var(--border2);
  }
  .sidebar.open{transform:translateX(0)}
  .sidebar-header-mobile {
    display: flex; align-items: center; justify-content: space-between; height: 64px;
  }
  .home-wrap, .settings-container{padding:24px 16px}
  .tools-grid{grid-template-columns:1fr}
  .home-hero { padding: 24px; }
  .home-hero h1 { font-size: 22px; }
}
</style>
</head>
<body>

<!-- GATE -->
<div id="gate">
  <div class="gate-card">
    <div class="gate-logo">Via</div>
    <h1 class="gate-title"><span>Via AI</span></h1>
    <p class="gate-sub">المنصة السحابية الفاخرة المخصصة للجامعات والتوظيف المستقبلي<br>أدخل مفتاح Claude API الخاص بك للعبور</p>
    <div class="gate-input-wrap">
      <input type="password" id="gate-key" placeholder="sk-ant-api03-..." autocomplete="off">
      <button class="eye-btn" onclick="toggleEye()" id="eyeBtn">👁</button>
    </div>
    <div class="gate-btn" onclick="enterApp()">تسجيل الدخول الآمن &larr;</div>
  </div>
</div>

<!-- MAIN APP -->
<div id="app">
  <!-- TOPNAV -->
  <div class="topnav">
    <div class="nav-right">
      <button class="hamburger" id="hamburger" onclick="toggleSidebar()">
        <span></span><span></span><span></span>
      </button>
      <div class="nav-logo">
        <div class="nav-logo-icon">V</div>
        <span class="nav-logo-text">Via <span>AI</span></span>
      </div>
    </div>
    <div class="nav-left">
      <div class="nav-item" style="padding:0;" onclick="goTo('settings')"><div class="ni" style="margin:0; background: var(--s2);">⚙️</div></div>
    </div>
  </div>

  <div class="app-body">
    <!-- SIDEBAR -->
    <div class="sidebar" id="sidebar">
      <!-- هيدر خاص بالجوال يظهر بداخل القائمة لمنع الحوسة وتداخل العناصر -->
      <div class="sidebar-header-mobile">
        <div class="nav-logo">
          <div class="nav-logo-icon">V</div>
          <span class="nav-logo-text">Via <span>AI</span></span>
        </div>
        <button class="arch-btn" onclick="closeSidebar()" style="padding: 4px 10px;">إغلاق ×</button>
      </div>

      <div class="nav-section">الرئيسية</div>
      <div class="nav-item active" onclick="goTo('home')"><div class="ni"><span class="icon-premium icon-home"></span></div>الرئيسية</div>

      <div class="nav-section">التتوظيف المهني</div>
      <div class="nav-item" onclick="goTo('cv')"><div class="ni"><span class="icon-premium icon-cv"></span></div>مصمم السيرة الذاتية</div>
      <div class="nav-item" onclick="goTo('cover')"><div class="ni"><span class="icon-premium icon-cover"></span></div>الخطاب التعريفي</div>
      <div class="nav-item" onclick="goTo('interview')"><div class="ni"><span class="icon-premium icon-interview"></span></div>تحضير المقابلات</div>
      <div class="nav-item" onclick="goTo('ats')"><div class="ni"><span class="icon-premium icon-ats"></span></div>فاحص الـ ATS المميز</div>

      <div class="nav-section">التعليم الأكاديمي</div>
      <div class="nav-item" onclick="goTo('summary')"><div class="ni"><span class="icon-premium icon-summary"></span></div>ملخص المحاضرات</div>
      <div class="nav-item" onclick="goTo('questions')"><div class="ni"><span class="icon-premium icon-questions"></span></div>توليد الاختبارات</div>
      <div class="nav-item" onclick="goTo('explain')"><div class="ni"><span class="icon-premium icon-explain"></span></div>تبسيط المفاهيم</div>
      <div class="nav-item" onclick="goTo('solve')"><div class="ni"><span class="icon-premium icon-solve"></span></div>مفكك عقد المسائل</div>

      <div class="nav-section">العروض والمراسلات</div>
      <div class="nav-item" onclick="goTo('slides')"><div class="ni"><span class="icon-premium icon-slides"></span></div>مخطط السلايدات</div>
      <div class="nav-item" onclick="goTo('script')"><div class="ni"><span class="icon-premium icon-script"></span></div>سكريبت الإلقاء</div>
      <div class="nav-item" onclick="goTo('email')"><div class="ni"><span class="icon-premium icon-email"></span></div>صياغة الإيميل الرسمي</div>
      <div class="nav-item" onclick="goTo('kpi')"><div class="ni"><span class="icon-premium icon-kpi"></span></div>مخطط الأهداف الذكية</div>
      
      <div class="nav-section">التحكم</div>
      <div class="nav-item" onclick="goTo('settings')"><div class="ni">⚙️</div>الإعدادات والمكتبة</div>
    </div>

    <div class="overlay" id="overlay" onclick="closeSidebar()"></div>

    <!-- CONTENT AREAS -->
    <div class="content" id="content">

      <!-- HOME PAGE -->
      <div class="page active" id="page-home">
        <div class="home-wrap">
          <div class="home-hero">
            <h1>منصة <span>Via AI</span> الفاخرة 👋</h1>
            <p>النظام الذكي المتكامل والأكثر فخامة المصمم خصيصاً لإدارة وتسهيل مسيرتك الأكاديمية وصناعة مستقبلك المهني والوظيفي بأعلى كفاءة.</p>
          </div>
          
          <div class="tools-section">
            <h2>التوظيف والمهن 💼</h2>
            <div class="tools-grid">
              <div class="tool-btn" onclick="goTo('cv')"><div class="tb-icon"><span class="icon-premium icon-cv"></span></div><div class="tb-name">مصمم السيرة الذاتية</div><div class="tb-desc">بناء سيرة ذاتية ذات هيكلية رقمية فاخرة وجاهزة.</div></div>
              <div class="tool-btn" onclick="goTo('cover')"><div class="tb-icon"><span class="icon-premium icon-cover"></span></div><div class="tb-name">الخطاب التعريفي</div><div class="tb-desc">صياغة خطابات تقديم وتغطية مخصصة للشركات الكبرى.</div></div>
              <div class="tool-btn" onclick="goTo('interview')"><div class="tb-icon"><span class="icon-premium icon-interview"></span></div><div class="tb-name">تحضير المقابلات</div><div class="tb-desc">توقع الأسئلة الذكية وبناء نماذج الإجابات النموذجية.</div></div>
              <div class="tool-btn" onclick="goTo('ats')"><div class="tb-icon"><span class="icon-premium icon-ats"></span></div><div class="tb-name">فاحص الـ ATS المميز</div><div class="tb-desc">تحليل مطابقة سيرتك الذاتية مع أنظمة الفرز الآلي للوظائف.</div></div>
            </div>

            <h2>التعليم الأكاديمي 🎓</h2>
            <div class="tools-grid">
              <div class="tool-btn" onclick="goTo('summary')"><div class="tb-icon"><span class="icon-premium icon-summary"></span></div><div class="tb-name">ملخص المحاضرات</div><div class="tb-desc">تكثيف وتلخيص المناهج والنصوص الطويلة في نقاط مركزة.</div></div>
              <div class="tool-btn" onclick="goTo('questions')"><div class="tb-icon"><span class="icon-premium icon-questions"></span></div><div class="tb-name">توليد الاختبارات</div><div class="tb-desc">صناعة نماذج اختبارات ذكية ومزيج من الأسئلة للمذاكرة.</div></div>
              <div class="tool-btn" onclick="goTo('explain')"><div class="tb-icon"><span class="icon-premium icon-explain"></span></div><div class="tb-name">تبسيط المفاهيم</div><div class="tb-desc">تفكيك وشرح النظريات المعقدة عبر أمثلة واقعية مبسطة.</div></div>
              <div class="tool-btn" onclick="goTo('solve')"><div class="tb-icon"><span class="icon-premium icon-solve"></span></div><div class="tb-name">مفكك عقد المسائل</div><div class="tb-desc">شرح المسائل والمعادلات الرياضية والعلمية خطوة بخطوة.</div></div>
            </div>

            <h2>العروض والمراسلات الرسميّة 🖥️</h2>
            <div class="tools-grid">
              <div class="tool-btn" onclick="goTo('slides')"><div class="tb-icon"><span class="icon-premium icon-slides"></span></div><div class="tb-name">مخطط السلايدات</div><div class="tb-desc">توليد الهيكل النصي وملاحظات الإلقاء لكل شريحة عرض.</div></div>
              <div class="tool-btn" onclick="goTo('script')"><div class="tb-icon"><span class="icon-premium icon-script"></span></div><div class="tb-name">سكريبت الإلقاء</div><div class="tb-desc">كتابة النص الصوتي اللفظي الكامل الذي ستقوله أثناء الإلقاء.</div></div>
              <div class="tool-btn" onclick="goTo('email')"><div class="tb-icon"><span class="icon-premium icon-email"></span></div><div class="tb-name">صياغة الإيميل الرسمي</div><div class="tb-desc">تحويل مسوداتك العادية إلى خطابات وإيميلات رسمية فاخرة.</div></div>
              <div class="tool-btn" onclick="goTo('kpi')"><div class="tb-icon"><span class="icon-premium icon-kpi"></span></div><div class="tb-name">مخطط الأهداف الذكية</div><div class="tb-desc">بناء خطط ومؤشرات قياس الأداء للأهداف الأكاديمية والمهنية.</div></div>
            </div>
          </div>
        </div>
      </div>

      <!-- CV TOOL -->
      <div class="page" id="page-cv">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>📄 مصمم السيرة الذاتية</h2><p>أنشئ هيكل نصي فاخر لسيرتك الذاتية يبرز نقاط قوتك</p></div>
            <div class="row2"><div class="field"><label>الاسم الكامل</label><input id="cv-name" placeholder="عبدالله محمد"></div><div class="field"><label>المسمى الوظيفي المستهدف</label><input id="cv-title" placeholder="محلل نظم أول"></div></div>
            <div class="field"><label>الخبرات المهنية</label><textarea id="cv-exp" placeholder="الشركة أو الجهة - المسمى - أبرز المهام والانجازات"></textarea></div>
            <div class="field"><label>المؤهلات التعليمية</label><textarea id="cv-edu" placeholder="الدرجة العلمية - التخصص - الجامعة أو الكلية"></textarea></div>
            <div class="field"><label>المهارات الفنية والشخصية</label><input id="cv-skills" placeholder="أدخل المهارات مفصولة بفاصلة"></div>
            <div class="field"><label>لغة الصياغة</label><select id="cv-lang"><option value="عربي">العربية</option><option value="إنجليزي">الإنجليزية (English)</option></select></div>
            <button class="run-btn" onclick="runTool('cv')">توليد السيرة الذاتية ✨</button>
          </div>
          <div class="tool-chat-side" id="cv-chat"></div>
        </div>
      </div>

      <!-- COVER LETTER TOOL -->
      <div class="page" id="page-cover">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>✉️ الخطاب التعريفي (Cover Letter)</h2><p>صياغة خطاب رسمي ومقنع يجذب مسؤولي التوظيف للشركة</p></div>
            <div class="field"><label>اسمك الموقر</label><input id="cl-name" placeholder="سلطان بن علي"></div>
            <div class="field"><label>الوظيفة الشاغرة</label><input id="cl-job" placeholder="أخصائي موارد بشرية"></div>
            <div class="field"><label>الجهة المستهدفة</label><input id="cl-company" placeholder="مجموعة الراجحي"></div>
            <div class="field"><label>نقاط قوتك وخبراتك البارزة</label><textarea id="cl-skills" placeholder="لماذا أنت الشخص الأنسب؟ اذكر بعض إنجازاتك الكبرى.."></textarea></div>
            <div class="field"><label>اللغة</label><select id="cl-lang"><option value="عربي">العربية</option><option value="إنجليزي">الإنجليزية</option></select></div>
            <button class="run-btn" onclick="runTool('cover')">توليد الخطاب التعريفي ✨</button>
          </div>
          <div class="tool-chat-side" id="cover-chat"></div>
        </div>
      </div>

      <!-- INTERVIEW TOOL -->
      <div class="page" id="page-interview">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>🎤 تحضير المقابلات الوظيفية</h2><p>بناء محاكاة وتوقع لأبرز الأسئلة السلوكية والفنية مع إجاباتها</p></div>
            <div class="field"><label>المسمى الوظيفي المستهدف</label><input id="int-job" placeholder="مهندس أمن سيبراني، أخصائي مالي..."></div>
            <div class="field"><label>المستوى المهني المتوقع</label><select id="int-exp"><option value="حديث تخرج">حديث تخرج / مبتدئ</option><option value="متوسط">خبرة متوسطة</option><option value="متقدم">مستوى قيادي / خبير</option></select></div>
            <button class="run-btn" onclick="runTool('interview')">توليد دليل المقابلة ✨</button>
          </div>
          <div class="tool-chat-side" id="interview-chat"></div>
        </div>
      </div>

      <!-- ATS MATCHING TOOL -->
      <div class="page" id="page-ats">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>🔍 فاحص نظام التوظيف ATS</h2><p>تأكد من مطابقة الـ CV للكلمات المفتاحية المطلوبة في نظام الفرز</p></div>
            <div class="field"><label>نص سيرة ذاتية الحالية</label><textarea id="ats-cv" placeholder="الصق نص سيرتك الذاتية هنا..."></textarea></div>
            <div class="field"><label>الوصف الوظيفي المعلن من الشركة</label><textarea id="ats-jd" placeholder="الصق متطلبات الوظيفة المعلنة هنا..."></textarea></div>
            <button class="run-btn" onclick="runTool('ats')">بدء الفحص الآلي ✨</button>
          </div>
          <div class="tool-chat-side" id="ats-chat"></div>
        </div>
      </div>

      <!-- SUMMARY TOOL -->
      <div class="page" id="page-summary">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>📝 ملخص المحاضرات والمناهج</h2><p>تكثيف المحاضرات الطويلة والمقالات الأكاديمية في نقاط تركيز رئيسية</p></div>
            <div class="field"><label>النص أو المنهج الدراسي</label><textarea id="sum-text" style="min-height:160px" placeholder="الصق محتوى الفصل أو المحاضرة هنا..."></textarea></div>
            <button class="run-btn" onclick="runTool('summary')">بدء التلخيص المعزز ✨</button>
          </div>
          <div class="tool-chat-side" id="summary-chat"></div>
        </div>
      </div>

      <!-- QUESTIONS TOOL -->
      <div class="page" id="page-questions">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>❓ مولد أسئلة ومراجعات الاختبارات</h2><p>توليد أسئلة مراجعة وتدريب بناءً على مناهجك الدراسية</p></div>
            <div class="field"><label>النص الدراسي أو محتوى الفصل المخصص</label><textarea id="q-text" style="min-height:140px" placeholder="الصق المنهج الدراسي المراد مراجعته هنا..."></textarea></div>
            <div class="field"><label>صيغة ونوع الأسئلة</label><select id="q-type"><option value="مزيج شامل">مزيج شامل (خيارات متعددة + صح وخطأ)</option><option value="شرح ومقالي">أسئلة مقالية وتفسيرية عميقة</option></select></div>
            <button class="run-btn" onclick="runTool('questions')">إنشاء بنك الأسئلة ✨</button>
          </div>
          <div class="tool-chat-side" id="questions-chat"></div>
        </div>
      </div>

      <!-- EXPLAIN TOOL -->
      <div class="page" id="page-explain">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>💡 شرح وتبسيط المفاهيم</h2><p>تحويل الأفكار والنظريات المعقدة والجافة إلى شرح ممتع ومبسط جداً</p></div>
            <div class="field"><label>المفهوم أو المصطلح الدراسي</label><input id="exp-topic" placeholder="مثال: نظرية الألعاب، الذكاء الاصطناعي التوليدي.."></div>
            <div class="field"><label>المستوى الدراسي المستهدف</label><select id="exp-level"><option value="مبتدئ">تبسيط مطلق (لشخص غير متخصص)</option><option value="جامعي">عميق ومفصل (لطالب جامعي متخصص)</option></select></div>
            <button class="run-btn" onclick="runTool('explain')">بدء الشرح والتبسيط ✨</button>
          </div>
          <div class="tool-chat-side" id="explain-chat"></div>
        </div>
      </div>

      <!-- ACADEMIC SOLVER TOOL -->
      <div class="page" id="page-solve">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>🧬 مفكك عقد المسائل العلمية</h2><p>تفكيك وفهم المسائل الرياضية أو الفيزيائية أو البرمجية المعقدة خطوة بخطوة</p></div>
            <div class="field"><label>نص أو صياغة المسألة الصعبة</label><textarea id="solve-text" style="min-height:140px" placeholder="اكتب نص المسألة أو الكود أو المعادلة هنا..."></textarea></div>
            <button class="run-btn" onclick="runTool('solve')">تفكيك وحل المسألة ✨</button>
          </div>
          <div class="tool-chat-side" id="solve-chat"></div>
        </div>
      </div>

      <!-- SLIDES TOOL -->
      <div class="page" id="page-slides">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>🖥️ مخطط السلايدات والعروض</h2><p>إنشاء المخطط الهيكلي والمحتوى المركز لكل شريحة عرض تقديمي</p></div>
            <div class="field"><label>عنوان أو موضوع العرض</label><input id="sl-topic" placeholder="مثال: التحول الرقمي في التعليم"></div>
            <div class="field"><label>العدد التقديري للشرائح</label><select id="sl-count"><option value="5 شرائح">5 شرائح</option><option value="8 شرائح">8 شرائح</option><option value="12 شريحة">12 شريحة</option></select></div>
            <button class="run-btn" onclick="runTool('slides')">توليد هيكل السلايدات ✨</button>
          </div>
          <div class="tool-chat-side" id="slides-chat"></div>
        </div>
      </div>

      <!-- SCRIPT TOOL -->
      <div class="page" id="page-script">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>🎙️ كاتب سكريبت ونص الإلقاء</h2><p>كتابة النص والسيناريو الكامل واللفظي الذي ستتحدث به أمام المايك أو الجمهور</p></div>
            <div class="field"><label>الموضوع العام للعرض</label><input id="sc-topic" placeholder="موضوع العرض الرئيسي"></div>
            <div class="field"><label>عناوين السلايدات المتوفرة لديك (سطر لكل عنوان شريحة)</label><textarea id="sc-slides" placeholder="المقدمة&#10;المشكلة الواقعية&#10;الحل المقترح&#10;التوصيات النهائية"></textarea></div>
            <button class="run-btn" onclick="runTool('script')">توليد نص الإلقاء ✨</button>
          </div>
          <div class="tool-chat-side" id="script-chat"></div>
        </div>
      </div>

      <!-- FORMAL EMAIL TOOL -->
      <div class="page" id="page-email">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>📬 صانع ومُعيد صياغة الإيميل الرسمي</h2><p>تحويل أفكارك العادية أو السريعة إلى خطابات وإيميلات رسمية عالية الاحترافية واللباقة</p></div>
            <div class="field"><label>لمن الإيميل وبخصوص ماذا؟ (الفكرة العامة والمسودة)</label><textarea id="em-text" style="min-height:140px" placeholder="مثال: إيميل للدكتور أطلب إعادة الاختبار بسبب عذر طبي.."></textarea></div>
            <div class="field"><label>نبرة الخطاب (Tone)</label><select id="em-tone"><option value="رسمية وجادة جداً">رسمية وجادة جداً (للجهات الأكاديمية والشركات)</option><option value="ودية واحترافية">ودية واحترافية (لزملاء العمل أو جهة مرنة)</option></select></div>
            <button class="run-btn" onclick="runTool('email')">صياغة البريد الرسمي ✨</button>
          </div>
          <div class="tool-chat-side" id="email-chat"></div>
        </div>
      </div>

      <!-- OKRS & KPIS PLANNER TOOL -->
      <div class="page" id="page-kpi">
        <div class="tool-layout">
          <div class="tool-form-side">
            <div class="tool-header"><h2>🎯 مخطط الأهداف الذكية ومؤشرات الأداء</h2><p>حول هدفك العادي العام إلى خطة استراتيجية مقسمة لخطوات رقمية قابلة للقياس والتحقيق</p></div>
            <div class="field"><label>ما هو هدفك الأساسي الذي تسعى لتحقيقه؟</label><textarea id="kp-target" placeholder="مثال: أريد رفع معدلي الجامعي هذا الترم، أو أريد تعلم لغة البايثون في شهرين..."></textarea></div>
            <button class="run-btn" onclick="runTool('kpi')">بناء الخطة الاستراتيجية ✨</button>
          </div>
          <div class="tool-chat-side" id="kpi-chat"></div>
        </div>
      </div>

      <!-- SETTINGS & LIBRARY PAGE -->
      <div class="page" id="page-settings">
        <div class="settings-container">
          <div class="settings-card">
            <h3>🎨 مظهر المنصة</h3>
            <div class="theme-switch-box">
              <button class="theme-btn active" id="thm-dark" onclick="setTheme('dark')">الوضع الداكن الفخم 🌙</button>
              <button class="theme-btn" id="thm-light" onclick="setTheme('light')">الوضع الفاتح النقي ☀️</button>
            </div>
          </div>

          <div class="settings-card">
            <h3>🔑 إدارة مفتاح الربط الفني (API Key)</h3>
            <div class="field" style="margin:0;"><input type="password" id="settings-key-input" placeholder="sk-ant-..." onchange="updateKeyFromSettings()"></div>
          </div>

          <div class="settings-card">
            <h3>📚 مكتبة الأعمال المحفوظة تلقائياً (Archive)</h3>
            <p style="font-size:12px; color:var(--t3); margin-bottom:16px;">يتم هنا الاحتفاظ بكل عمل أساسي تولده المنصة لمراجعته واستخدامه في أي وقت.</p>
            <div class="archive-list" id="archiveContainer"></div>
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
  if(!k || !k.startsWith('sk-ant-')){alert('يرجى إدخل مفتاح Claude API صحيح يبدأ بـ sk-ant-');return;}
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

// Initialization Check
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
  
  // إغلاق أي نافذة محادثة نشطة بالجوال عند التبديل لمنع تداخل الصفحات والحوسة
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
    body:JSON.stringify({
      model:'claude-3-7-sonnet-latest', // الترقية إلى الموديل الأحدث والأقوى
      max_tokens:4000,
      messages:messages
    })
  });
  var data = await res.json();
  if(data.error) throw new Error(data.error.message);
  return data.content.map(function(i){return i.text||'';}).join('');
}


// ===== CHAT SYSTEM =====
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
        <button class="mobile-back-btn" onclick="exitMobileChat('${toolId}')">⬅ العودة وتعديل الحقول</button>
        <div class="ce-icon">Via</div>
        <p>النتائج الفاخرة ومتابعة التحسينات الذكية ستظهر هنا</p>
      </div>
    </div>
    <div class="chat-input-bar">
      <textarea id="${toolId}-inp" placeholder="اطلب تعديل، إضافة أو تحسين على هذه النتيجة..." rows="1" onkeydown="chatKey(event,'${toolId}')"></textarea>
      <button class="send-btn" id="${toolId}-send" onclick="sendChat('${toolId}')">↩</button>
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
  var actionsHTML = role === 'ai' ? `<div class="msg-actions"><button class="msg-copy" onclick="copyMsg(this,\`${escAttr(text)}\`)">نسخ النص كاملاً</button></div>` : '';
  
  var backBtnMobile = (role==='ai' && msgsEl.children.length <= 1) ? `<button class="mobile-back-btn" onclick="exitMobileChat('${toolId}')" style="margin-top:0; margin-bottom:12px;">⬅ العودة لتغيير الحقول</button>` : '';

  div.innerHTML = backBtnMobile + '<div class="msg-label">'+label+'</div><div class="msg-bubble">'+escHTML(text)+'</div>'+actionsHTML;
  msgsEl.appendChild(div);
  msgsEl.scrollTop = msgsEl.scrollHeight;
}

function addTyping(toolId){
  var msgsEl = document.getElementById(toolId+'-msgs');
  if(!msgsEl) return;
  var div = document.createElement('div');
  div.className = 'msg ai'; div.id = toolId+'-typing';
  div.innerHTML = '<div class="msg-label">Via AI جاري التوليد بدقة...</div><div class="msg-bubble"><div class="typing-indicator"><div class="typing-dot"></div><div class="typing-dot"></div><div class="typing-dot"></div></div></div>';
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
    addChatMsg(toolId,'ai','حدث خطأ بالاتصال بالخادم: ' + e.message);
  }finally{
    if(sendBtn) sendBtn.disabled = false;
  }
}

// ===== PROMPTS ENGINEERING CONTEXT =====
function v(id){var el=document.getElementById(id); return el?el.value.trim():'';}

var toolPrompts = {
  cv: function(){return `صمم سيرة ذاتية (CV) احترافية رفيعة المستوى باللغة ${v('cv-lang')} بناءً على المعطيات التالية:\nالاسم: ${v('cv-name')}\nالمسمى الوظيفي المستهدف: ${v('cv-title')}\nالخبرات المهنية: ${v('cv-exp')}\nالتعليم والمؤهلات: ${v('cv-edu')}\nالمهارات الأساسية: ${v('cv-skills')}.\nقم بتنظيم الهيكل والفقرات بشكل فخم وجاهز ومبهر للمؤسسات والشركات الكبرى.`;},
  cover: function(){return `اكتب خطاب تعريفي (Cover Letter) رسمي وبليغ باللغة ${v('cl-lang')} موجه إلى شركة (${v('cl-company')}) للتقديم على وظيفة (${v('cl-job')}). ادمج مهاراتي المذكورة بشكل مقنع ومثير للإعجاب:\n${v('cl-skills')}`;},
  interview: function(){return `أنا مقبل على مقابلة عمل تخصصية لوظيفة (${v('int-job')}) بمستوى خبرة (${v('int-exp')}). اكتب لي أبرز 7 أسئلة متوقعة بدقة تامة مع كتابة نموذج إجابة مثالي واحترافي وعميق لكل سؤال لضمان اجتياز المقابلة بنجاح.`;},
  ats: function(){return `حلل نص السيرة ذاتية التالية وطابقها مع متطلبات الوصف الوظيفي المرفق:\nالسيرة الذاتية:\n${v('ats-cv')}\n\nالوصف الوظيفي:\n${v('ats-jd')}\nأعطني نسبة المطابقة التقديرية لأنظمة ATS، واذكر الكلمات المفتاحية المفقودة التي يجب علي إضافتها، مع تقديم نصائح لتعديل الـ CV ليصبح متوافقاً تماماً مع الأنظمة الآلية للتوظيف.`;},
  summary: function(){return `قم بتلخيص المحتوى الأكاديمي المرفق تلخيصاً ذكياً وشاملاً مع الحفاظ الدقيق على الهياكل الرئيسية واستخراج أهم الأفكار والمصطلحات الفرعية بنقاط واضحة ومرتبة:\n\n${v('sum-text')}`;},
  questions: function(){return `بناءً على المحتوى والمنهج الدراسي المرفق، قم بتوليد أسئلة اختبار تدريبية من نوع (${v('q-type')}) لقياس الفهم والاستيعاب الفعلي قبل الامتحان، مع إرفاق نموذج إجابة نموذجي دقيق ومفصل لكل سؤال:\n\n${v('q-text')}`;},
  explain: function(){return `اشرح وبسط النظرية/المفهوم التالي: "${v('exp-topic')}" بحيث يكون الأسلوب مخصصاً ومفهوماً تماماً لمستوى (${v('exp-level')})، مع إرفاق أمثلة توضيحية وتطبيقات واقعية لتسهيل استيعاب النظرية من المرة الأولى.`;},
  solve: function(){return `قم بفك وحل المسألة العلمية التالية خطوة بخطوة مع توضيح آلية الحل والمنطق العلمي المستخدم وراء كل خطوة لضمان الفهم الأكاديمي العميق للمسألة:\n\n${v('solve-text')}`;},
  slides: function(){return `أنشئ مخططاً نصياً وهيكلياً كاملاً لبريزنتيشن يتكون من (${v('sl-count')}) حول موضوع: "${v('sl-topic')}". اكتب لكل شريحة على حدة: عنوان الشريحة، النقاط والمحتوى المركز داخل الشريحة، وملاحظات المتحدث اللفظية والجانبية (Presenters notes).`;},
  script: function(){return `اكتب سكريبت إلقاء لفظي كامل وشامل ومتصل لعرض تقديمي حول موضوع: "${v('sc-topic')}". العناوين المتوفرة للشرائح هي:\n${v('sc-slides')}\nاكتب صياغة وبلاغة الإلقاء الحرفية التي سأتحدث بها شفهياً أمام الجمهور مع كل شريحة بالتفصيل لشد انتباه الحضور.`;},
  email: function(){return `أعد صياغة الفكرة والموضوع التالي في قالب إيميل/خطاب رسمي رفيع المستوى واللباقة بنبرة (${v('em-tone')}):\n\n${v('em-text')}`;},
  kpi: function(){return `بناءً على هدفي التالي: "${v('kp-target')}"، قم بوضع خطة استراتيجية ذكية ومفصلة متوافقة مع منهجية OKRs ومؤشرات قياس الأداء KPIs مقسمة لخطوات زمنية واضحة وقابلة للقياس والتحقيق ومتابعة تقدم الهدف بنجاح.`;}
};

async function runTool(toolId){
  var prompt = toolPrompts[toolId] ? toolPrompts[toolId]() : '';
  if(!prompt) return;

  // تشغيل النمط المخصص للجوال لضمان عزل النوافذ والمنع التام لتداخل وحوسة العناصر
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
    
    // الأرشفة التلقائية في مكتبة الأعمال
    saveToArchive(toolId, reply);
  }catch(e){
    removeTyping(toolId);
    addChatMsg(toolId,'ai','فشل نظام التوليد: '+e.message);
  }finally{
    if(btn) btn.disabled = false;
  }
}

// ===== ARCHIVE & LIBRARY LOGIC =====
function saveToArchive(toolId, text) {
  var archive = JSON.parse(localStorage.getItem('via_ai_archive') || '[]');
  var titleMap = {cv:'سيرة ذاتية', cover:'خطاب تقديم', interview:'تحضير مقابلة', ats:'فحص ATS الآلي', summary:'تلخيص محاضرة', questions:'أسئلة اختبار', explain:'شرح مفهوم', solve:'تفكيك مسألة علمية', slides:'شرائح عرض', script:'سكريبت إلقاء', email:'إيميل رسمي', kpi:'مخطط الأهداف'};
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
    container.innerHTML = '<p style="font-size:13px; color:var(--t3); text-align:center; padding:20px;">المكتبة السحابية فارغة حالياً. سيتم حفظ أي عمل تولده هنا تلقائياً.</p>';
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

// ===== UTILITIES & ESCAPING =====
function copyMsg(btn,text){
  navigator.clipboard.writeText(text).then(function(){
    var old = btn.textContent; btn.textContent='تم النسخ بنجاح! ✓';
    setTimeout(function(){btn.textContent = old;},2000);
  });
}
function escHTML(t){return t.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/\n/g,'<br>');}
function escAttr(t){return t.replace(/'/g,'&#39;').replace(/"/g,'&quot;').replace(/`/g,'&#96;');}
document.getElementById('gate-key').addEventListener('keydown',function(e){if(e.key==='Enter')enterApp();});
</script>
</body>
</html>
