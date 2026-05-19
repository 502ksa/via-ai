<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>Znoog Community</title>

<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;900&family=Tajawal:wght@400;700;800;900&display=swap" rel="stylesheet">

<script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-database-compat.js"></script>

<style>
:root{
  --bg:#08080f;--sidebar:#0c0c18;--surface:#111120;--surface2:#181830;--surface3:#1e1e3a;
  --border:#1f1f3a;--border2:#2a2a50;
  --accent:#5865f2;--accent2:#7c8ff5;--teal:#00d4aa;
  --gold:#f0b429;--danger:#f04747;--success:#43b581;
  --text:#e8e8f5;--muted:#5a5a80;--muted2:#8888aa;
  --sw:60px;--sideW:230px;--hh:52px;
}

*{box-sizing:border-box;margin:0;padding:0}

/* ✅ FIX MOBILE SCROLL */
html,body{
  height:100%;
  overflow:hidden;
}

body{
  font-family:'Cairo',sans-serif;
  background:var(--bg);
  color:var(--text);
  display:flex;
  flex-direction:column;
}

/* APP */
.app{display:flex;height:100vh;overflow:hidden}

/* SERVER STRIP */
.strip{width:var(--sw);flex-shrink:0;background:#06060e;display:flex;flex-direction:column;align-items:center;padding:10px 0;gap:6px;border-left:1px solid var(--border);overflow-y:auto}
.s-icon{width:44px;height:44px;border-radius:50%;background:var(--accent);display:flex;align-items:center;justify-content:center;font-weight:900;cursor:pointer}
.s-icon.active{border-radius:14px;background:var(--teal);color:#000}

/* SIDEBAR */
.sidebar{width:var(--sideW);flex-shrink:0;background:var(--sidebar);display:flex;flex-direction:column;border-left:1px solid var(--border);overflow:hidden}

/* MAIN */
.main{flex:1;display:flex;flex-direction:column;overflow:hidden;min-width:0}

/* PAGES */
.page{display:none;flex:1;overflow:hidden;flex-direction:column}
.page.active{display:flex}

/* FEED FIX */
.feed{
  flex:1;
  overflow-y:auto;
  padding:12px 16px;
  display:flex;
  flex-direction:column;
  gap:1px;
  -webkit-overflow-scrolling:touch; /* ✅ مهم للجوال */
}

/* INPUT FIX */
.ci-wrap{padding:10px 14px;flex-shrink:0}

/* ================= MOBILE FIX ================= */
@media(max-width:900px){
  .app{flex-direction:column}

  .strip{display:none}

  .sidebar{
    width:100%;
    height:auto;
  }

  .main{
    height:100%;
  }

  .ch-hdr{
    padding:10px;
  }

  .ci-inp{
    font-size:16px; /* يمنع زوم الآيفون */
  }
}

@media(max-width:500px){
  .sidebar{display:none}

  .ci-box{
    flex-wrap:wrap;
  }
}
</style>
</head>

<body>

<div class="app">

<!-- SERVER STRIP -->
<div class="strip">
  <div class="s-icon active">Z</div>
  <div class="s-icon" style="background:var(--surface2)">+</div>
</div>

<!-- SIDEBAR -->
<div class="sidebar">
  <div class="sb-hdr">
    <div class="sb-title">Znoog Community</div>
    <div class="sb-sub" id="online-count">جاري التحميل...</div>
  </div>

  <div class="ch-btn active" onclick="goTo('general',this)"># عام</div>
  <div class="ch-btn" onclick="goTo('admch',this)">🔒 الادمن</div>
</div>

<!-- MAIN -->
<div class="main">

<!-- GENERAL -->
<div class="page active" id="page-general">
  <div class="feed" id="feed-general"></div>

  <div class="ci-wrap">
    <div class="ci-box">
      <input class="ci-inp" id="ci-general" placeholder="اكتب رسالة..." maxlength="400">
      <button class="send-b" onclick="sendMsg('general')">ارسال</button>
    </div>
  </div>
</div>

</div>

</div>

<script>
/* ===== FIREBASE ===== */
const fbCfg={
  apiKey:"AIzaSy...",
  authDomain:"velora-rp.firebaseapp.com",
  databaseURL:"https://velora-rp-default-rtdb.europe-west1.firebasedatabase.app",
  projectId:"velora-rp"
};

firebase.initializeApp(fbCfg);
const db=firebase.database();

/* ===== FIX: ENSURE CHAT WORKS ===== */
function listenCh(ch){
  db.ref('msgs/'+ch).orderByChild('time').limitToLast(60).on('value',snap=>{
    const feed=document.getElementById('feed-'+ch);
    if(!feed) return;

    let msgs=[];
    snap.forEach(s=>msgs.push(s.val()));

    feed.innerHTML = msgs.map(m=>
      `<div style="padding:8px;border-bottom:1px solid #222">
        <b>${m.name||'user'}:</b> ${m.text||''}
      </div>`
    ).join('');

    feed.scrollTop = feed.scrollHeight;
  });
}

/* NAV */
function goTo(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
}

/* SEND */
function sendMsg(ch){
  const inp=document.getElementById('ci-'+ch);
  if(!inp.value.trim()) return;

  db.ref('msgs/'+ch).push({
    name:"user",
    text:inp.value,
    time:Date.now()
  });

  inp.value='';
}

/* INIT CHAT */
listenCh('general');
</script>

</body>
</html>
