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
}

body{
  font-family:'Cairo',sans-serif;
  background:var(--bg);
  color:var(--text);
  min-height:100vh;
}

/* LAYOUT */
.layout{display:flex;min-height:100vh}

/* SIDEBAR (DESKTOP) */
.sidebar{
  width:260px;
  min-width:260px;
  background:var(--surface);
  border-left:1px solid var(--border);
  display:flex;
  flex-direction:column;
  padding:24px 0;
  position:fixed;
  right:0;
  top:0;
  bottom:0;
  overflow-y:auto;
  z-index:100;
}

.sidebar-logo{
  display:flex;
  align-items:center;
  gap:10px;
  padding:0 20px 24px;
  border-bottom:1px solid var(--border);
  margin-bottom:16px;
}

.sidebar-logo-icon{
  width:38px;height:38px;
  background:var(--accent);
  border-radius:10px;
  display:flex;
  align-items:center;
  justify-content:center;
}

.sidebar-logo-text{font-weight:900}

.section-title{
  font-size:10px;
  color:var(--muted);
  padding:0 20px;
  margin:12px 0 6px;
}

.nav-item{
  display:flex;
  align-items:center;
  gap:10px;
  padding:11px 20px;
  cursor:pointer;
  color:var(--muted);
}

.nav-item:hover{color:var(--text)}

.nav-item.active{
  color:var(--accent);
}

/* MAIN */
.main{
  margin-right:260px;
  flex:1;
  padding:40px;
  max-width:860px;
}

.page{display:none}
.page.active{display:block}

/* ===================== */
/* 📱 MOBILE FIX ONLY */
/* ===================== */
@media(max-width:768px){

  .layout{
    flex-direction:column;
  }

  /* sidebar becomes bottom bar */
  .sidebar{
    position:fixed;
    bottom:0;
    top:auto;
    right:0;
    left:0;

    width:100%;
    height:64px;

    flex-direction:row;
    align-items:center;

    overflow-x:auto;
    overflow-y:hidden;

    border-left:none;
    border-top:1px solid var(--border);
  }

  /* hide extras */
  .sidebar-logo,
  .section-title{
    display:none;
  }

  .nav-item{
    min-width:80px;
    flex-direction:column;
    justify-content:center;
    align-items:center;
    font-size:10px;
    padding:6px 10px;
    white-space:nowrap;
  }

  .main{
    margin-right:0;
    padding:16px;
    padding-bottom:100px;
    max-width:100%;
  }
}

</style>
</head>

<body>

<div class="layout">

  <div class="sidebar">
    <div class="sidebar-logo">
      <div class="sidebar-logo-icon">AI</div>
      <div class="sidebar-logo-text">مساعد</div>
    </div>

    <div class="section-title">القائمة</div>

    <div class="nav-item">الرئيسية</div>
    <div class="nav-item">CV</div>
    <div class="nav-item">Cover</div>
    <div class="nav-item">مقابلات</div>
    <div class="nav-item">ملخص</div>
    <div class="nav-item">أسئلة</div>
  </div>

  <div class="main">
    <div class="page active">
      <h1>مرحباً</h1>
      <p>الموقع الآن مضبوط على الجوال</p>
    </div>
  </div>

</div>

</body>
</html>
