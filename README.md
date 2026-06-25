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
  text-transform:uppercase;letter-spacing:1.5px;
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

/* API KEY */
.api-bar{
  margin:auto 16px 0;
  background:var(--card);
  border:1px solid var(--border);
  border-radius:12px;
  padding:14px;
}
.api-bar label{font-size:11px;color:var(--muted);font-weight:700;text-transform:uppercase}
.api-bar input{
  width:100%;background:var(--bg);
  border:1.5px solid var(--border);
  border-radius:8px;padding:9px 12px;
  font-family:'Cairo',sans-serif;font-size:13px;
  color:var(--text);direction:ltr;
}
.api-status{font-size:11px;margin-top:6px;text-align:center}
.api-status.ok{color:var(--green)}
.api-status.bad{color:var(--red)}

/* MAIN */
.main{margin-right:260px;flex:1;padding:40px 36px;max-width:860px}

.page{display:none}
.page.active{display:block}

/* باقي CSS بدون تغيير */
</style>
</head>

<body>
<div class="layout">

<div class="sidebar">
  <div class="sidebar-logo">
    <div class="sidebar-logo-icon"></div>
    <div class="sidebar-logo-text">مساعد AI<span>الجامعة والتوظيف</span></div>
  </div>

  <div class="section-title">التوظيف</div>
  <div class="nav-item" onclick="goTo('home')"><span class="icon"></span> الرئيسية</div>
  <div class="nav-item" onclick="goTo('cv')"><span class="icon"></span> مصمم CV</div>
  <div class="nav-item" onclick="goTo('cover')"><span class="icon"></span> Cover Letter</div>
  <div class="nav-item" onclick="goTo('interview')"><span class="icon"></span> تحضير مقابلة</div>
  <div class="nav-item" onclick="goTo('jobdesc')"><span class="icon"></span> تحليل وصف وظيفي</div>

  <div class="section-title">الجامعة</div>
  <div class="nav-item" onclick="goTo('summary')"><span class="icon"></span> ملخص محاضرات</div>
  <div class="nav-item" onclick="goTo('questions')"><span class="icon"></span> أسئلة اختبار</div>
  <div class="nav-item" onclick="goTo('essay')"><span class="icon"></span> تصحيح مقالات</div>
  <div class="nav-item" onclick="goTo('explain')"><span class="icon"></span> شرح مفاهيم</div>

  <div class="section-title">البريزنتيشن</div>
  <div class="nav-item" onclick="goTo('slides')"><span class="icon"></span> مولّد سلايدات</div>
  <div class="nav-item" onclick="goTo('script')"><span class="icon"></span> سكريبت العرض</div>
  <div class="nav-item" onclick="goTo('trainer')"><span class="icon"></span> مدرّب عروض</div>
</div>

<div class="main">
  <div class="page active" id="page-home">
    <h1>مرحباً</h1>
  </div>
</div>

</div>

<script>
// بدون تغيير
</script>

</body>
</html>
