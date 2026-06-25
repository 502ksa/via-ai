<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>مساعد الجامعة والتوظيف</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;900&display=swap');
*{margin:0;padding:0;box-sizing:border-box}
:root{
  --bg:#08080f;
  --surface:#111118;
  --card:#18181f;
  --border:#25253a;
  --accent:#6c63ff;
  --accent-glow:rgba(108,99,255,0.2);
  --text:#f0f0f8;
  --muted:#7777aa;
  --green:#34c759;
  --red:#ff3b5c;
}
body{font-family:'Cairo',sans-serif;background:var(--bg);color:var(--text);min-height:100vh}

/* OVERLAY API */
#apiOverlay{
  position:fixed;inset:0;
  background:rgba(0,0,0,0.85);
  display:flex;align-items:center;justify-content:center;
  z-index:9999;
}
.api-box{
  background:var(--surface);
  padding:24px;
  border:1px solid var(--border);
  border-radius:14px;
  width:320px;
}
.api-box h2{font-size:16px;margin-bottom:10px}
.api-box input{
  width:100%;
  padding:10px;
  border-radius:8px;
  border:1px solid var(--border);
  background:var(--bg);
  color:var(--text);
  direction:ltr;
}
.api-box button{
  margin-top:10px;
  width:100%;
  padding:10px;
  border:none;
  background:var(--accent);
  color:#fff;
  border-radius:8px;
  cursor:pointer;
}

/* SIDEBAR */
.layout{display:flex;min-height:100vh}
.sidebar{
  width:260px;min-width:260px;
  background:var(--surface);
  border-left:1px solid var(--border);
  display:flex;flex-direction:column;
  padding:24px 0;
  position:fixed;right:0;top:0;bottom:0;
  overflow-y:auto;z-index:100;
}
.sidebar-logo{
  display:flex;align-items:center;gap:10px;
  padding:0 20px 24px;
  border-bottom:1px solid var(--border);
  margin-bottom:16px;
}
.sidebar-logo-icon{
  width:38px;height:38px;
  background:var(--accent);
  border-radius:10px;
  display:flex;align-items:center;justify-content:center;
  font-size:18px;
  box-shadow:0 0 20px var(--accent-glow);
}
.sidebar-logo-text{font-size:15px;font-weight:900;line-height:1.3}
.sidebar-logo-text span{color:var(--accent);font-size:11px;display:block;font-weight:600}

.section-title{
  font-size:10px;font-weight:700;
  color:var(--muted);
  text-transform:uppercase;
  letter-spacing:1.5px;
  padding:0 20px;margin:12px 0 6px;
}

.nav-item{
  display:flex;align-items:center;gap:10px;
  padding:11px 20px;
  cursor:pointer;
  font-size:14px;font-weight:600;
  color:var(--muted);
  transition:all 0.2s;
  border-right:3px solid transparent;
}
.nav-item:hover{background:rgba(108,99,255,0.07);color:var(--text)}
.nav-item.active{
  background:rgba(108,99,255,0.12);
  color:var(--accent);
  border-right-color:var(--accent);
}
.nav-item .icon{font-size:16px;width:20px;text-align:center}

/* API BAR */
.api-bar{
  margin:auto 16px 0;
  background:var(--card);
  border:1px solid var(--border);
  border-radius:12px;
  padding:14px;
}
.api-bar input{width:100%;background:var(--bg);border:1px solid var(--border);color:var(--text);padding:9px;border-radius:8px;direction:ltr}

/* MAIN */
.main{margin-right:260px;flex:1;padding:40px 36px;max-width:860px}
.page{display:none}
.page.active{display:block}

/* باقي CSS بدون تغيير */
</style>
</head>

<body>

<!-- API OVERLAY -->
<div id="apiOverlay">
  <div class="api-box">
    <h2>API Key</h2>
    <input id="overlayKey" placeholder="sk-ant-...">
    <button onclick="saveOverlayKey()">دخول</button>
  </div>
</div>

<div class="layout">

<!-- SIDEBAR -->
<div class="sidebar">
  <div class="sidebar-logo">
    <div class="sidebar-logo-icon">AI</div>
    <div class="sidebar-logo-text">مساعد الجامعة<span>والتوظيف</span></div>
  </div>

  <div class="section-title">التوظيف</div>
  <div class="nav-item" onclick="goTo('home')"><span class="icon">H</span> الرئيسية</div>
  <div class="nav-item" onclick="goTo('cv')"><span class="icon">CV</span> مصمم CV</div>
  <div class="nav-item" onclick="goTo('cover')"><span class="icon">CL</span> Cover Letter</div>
  <div class="nav-item" onclick="goTo('interview')"><span class="icon">INT</span> تحضير مقابلة</div>
  <div class="nav-item" onclick="goTo('jobdesc')"><span class="icon">JD</span> تحليل وظيفة</div>

  <div class="section-title">الجامعة</div>
  <div class="nav-item" onclick="goTo('summary')"><span class="icon">SUM</span> ملخص</div>
  <div class="nav-item" onclick="goTo('questions')"><span class="icon">Q</span> أسئلة</div>
  <div class="nav-item" onclick="goTo('essay')"><span class="icon">ESS</span> تصحيح</div>
  <div class="nav-item" onclick="goTo('explain')"><span class="icon">EXP</span> شرح</div>

  <div class="section-title">العروض</div>
  <div class="nav-item" onclick="goTo('slides')"><span class="icon">SL</span> سلايدات</div>
  <div class="nav-item" onclick="goTo('script')"><span class="icon">SC</span> سكريبت</div>
  <div class="nav-item" onclick="goTo('trainer')"><span class="icon">TR</span> تدريب</div>

  <div class="api-bar">
    <input type="password" id="apiKey" placeholder="sk-ant-..." oninput="saveKey()">
  </div>
</div>

<div class="main">
  <div class="page active" id="page-home">
    <h1>مرحباً</h1>
    <p>اختر أداة</p>
  </div>
</div>

</div>

<script>

// API LOCK
function saveOverlayKey(){
  let k=document.getElementById('overlayKey').value.trim();
  if(!k.startsWith('sk-ant-')) return alert('Key غير صحيح');
  localStorage.setItem('claude_key_v2',k);
  document.getElementById('apiOverlay').style.display='none';
  document.getElementById('apiKey').value=k;
}
window.onload=function(){
  let k=localStorage.getItem('claude_key_v2');
  if(k){
    document.getElementById('apiOverlay').style.display='none';
    document.getElementById('apiKey').value=k;
  }
};

function saveKey(){
  let k=document.getElementById('apiKey').value.trim();
  if(k) localStorage.setItem('claude_key_v2',k);
}
function getKey(){
  return localStorage.getItem('claude_key_v2')||'';
}

// NAV
function goTo(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
}

</script>

</body>
</html>
