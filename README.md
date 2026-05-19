<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Znoog Community</title>

<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;900&family=Tajawal:wght@400;700;800;900&display=swap" rel="stylesheet">

<script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-database-compat.js"></script>

<style>
:root{
  --bg:#08080f;--sidebar:#0c0c18;--surface:#111120;--surface2:#181830;--surface3:#1e1e3a;
  --border:#1f1f3a;--border2:#2a2a50;
  --accent:#5865f2;--accent2:#7c8ff5;--teal:#00d4aa;
  --gold:#f0b429;--danger:#f04747;--muted:#5a5a80;--muted2:#8888aa;
  --sw:60px;--sideW:230px;--hh:52px;
}

*{box-sizing:border-box;margin:0;padding:0}

html,body{
  height:100%;
  overflow:hidden;
  font-family:'Cairo',sans-serif;
  background:var(--bg);
  color:var(--text);
}

.app{
  display:flex;
  height:100dvh;
  overflow:hidden;
}

/* FIX MOBILE LAYOUT */
.main{
  flex:1;
  display:flex;
  flex-direction:column;
  min-width:0;
  min-height:0;
}

.page{
  flex:1;
  display:none;
  flex-direction:column;
  min-height:0;
  overflow:hidden;
}

.page.active{display:flex}

.feed,.m-pg,.ev-pg,.adm-pg,.media-grid{
  min-height:0;
}

/* باقي تصميمك بدون تغيير كبير */
.sidebar{width:230px;background:var(--sidebar);display:flex;flex-direction:column}
.strip{width:60px;background:#06060e}

/* chat fix */
.feed{
  flex:1;
  overflow-y:auto;
  padding:12px;
  min-height:0;
}

/* admin fix */
.adm-pg{
  flex:1;
  overflow-y:auto;
  min-height:0;
  padding-bottom:100px;
}

/* media fix */
.media-grid{
  flex:1;
  overflow-y:auto;
  min-height:0;
}

/* باقي ستايلك كما هو (مختصر عشان ما ينكسر) */
</style>
</head>

<body>

<div class="app">

<!-- SIDEBAR (مختصر) -->
<div class="sidebar">
  <div style="padding:12px;color:#fff;font-weight:900">Znoog</div>

  <button onclick="goTo('general')" class="ch-btn">عام</button>
  <button onclick="goTo('admch')" class="ch-btn">الادمن</button>
  <button onclick="goTo('media')" class="ch-btn">الميديا</button>
  <button onclick="goTo('admin')" class="ch-btn">لوحة التحكم</button>
</div>

<!-- MAIN -->
<div class="main">

<!-- GENERAL -->
<div class="page active" id="page-general">
  <div class="feed" id="feed-general"></div>

  <div style="padding:10px">
    <input id="ci-general" placeholder="اكتب..." style="width:80%">
    <button onclick="sendMsg('general')">ارسال</button>
  </div>
</div>

<!-- ADM -->
<div class="page" id="page-admch">
  <div id="admch-lock">
    <input id="admch-pass" placeholder="كلمة السر">
    <button onclick="unlockAdmCh()">دخول</button>
  </div>

  <div id="admch-body" style="display:none;flex:1;flex-direction:column">
    <div class="feed" id="feed-admch"></div>
    <input id="ci-admch">
    <button onclick="sendMsg('admch')">ارسال</button>
  </div>
</div>

<!-- MEDIA -->
<div class="page" id="page-media">
  <input type="file" onchange="uploadMedia(this)">
  <div class="media-grid" id="media-grid"></div>
</div>

<!-- ADMIN -->
<div class="page" id="page-admin">

<div id="adm-login">
  <input id="adm-pass" placeholder="password">
  <button onclick="loginAdm()">login</button>
</div>

<div id="adm-panel" style="display:none">

  <button onclick="clearCh('general')">مسح العام</button>

  <input id="newPass" placeholder="new pass">
  <button onclick="changePass()">تغيير الباسورد</button>

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

/* ===== OWNER SYSTEM ===== */
const OWNER_NAME="rv";
let isOwner=false;
let isAdmin=false;
let ADMIN_PASS="008877";

db.ref('config/adminPass').on('value',s=>{
 if(s.val()) ADMIN_PASS=s.val();
});

/* ===== NAV ===== */
function goTo(id){
 document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
 document.getElementById('page-'+id).classList.add('active');
}

/* ===== PROFILE ===== */
let prof={name:"user"+Math.floor(Math.random()*9999)};

/* ===== CHAT ===== */
function sendMsg(ch){
 const inp=document.getElementById('ci-'+ch);
 const text=inp.value;
 if(!text)return;

 db.ref('msgs/'+ch).push({
  name:prof.name,
  text,
  time:Date.now(),
  isAdmin:isAdmin||isOwner
 });

 inp.value='';
}

function listenCh(ch){
 db.ref('msgs/'+ch).on('value',snap=>{
  const feed=document.getElementById('feed-'+ch);
  let h="";

  snap.forEach(s=>{
   const d=s.val();
   h+=`<div style="padding:6px">
   <b>${d.name}</b>: ${d.text}
   </div>`;
  });

  feed.innerHTML=h;
 });
}

listenCh('general');

/* ===== ADM CH ===== */
function unlockAdmCh(){
 const p=document.getElementById('admch-pass').value;
 if(p===ADMIN_PASS||p===OWNER_NAME){
  document.getElementById('admch-lock').style.display='none';
  document.getElementById('admch-body').style.display='flex';
  listenCh('admch');
 }
}

/* ===== ADMIN ===== */
function loginAdm(){
 const v=document.getElementById('adm-pass').value;

 if(prof.name===OWNER_NAME){
  isOwner=true;isAdmin=true;
 }
 else if(v===ADMIN_PASS){
  isAdmin=true;
 }else return;

 document.getElementById('adm-login').style.display='none';
 document.getElementById('adm-panel').style.display='block';
}

/* CHANGE PASS */
function changePass(){
 if(!isOwner)return;
 db.ref('config/adminPass').set(document.getElementById('newPass').value);
}

/* CLEAR */
function clearCh(ch){
 if(!isAdmin)return;
 db.ref('msgs/'+ch).remove();
}

/* MEDIA */
function uploadMedia(inp){
 const f=inp.files[0];
 const r=new FileReader();

 r.onload=e=>{
  db.ref('media').push({
   b64:e.target.result,
   name:prof.name
  });
 };

 r.readAsDataURL(f);
}

db.ref('media').on('value',snap=>{
 const g=document.getElementById('media-grid');
 let h="";

 snap.forEach(s=>{
  const d=s.val();
  h+=`<img src="${d.b64}" style="width:100px">`;
 });

 g.innerHTML=h;
});

</script>

</body>
</html>
