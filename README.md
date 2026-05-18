<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Znoog Community</title>

<script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-database-compat.js"></script>

<style>
body{
margin:0;
font-family:Arial;
background:#0b0b0f;
color:white;
}

/* HEADER */
header{
text-align:center;
padding:12px;
background:#120018;
box-shadow:0 0 20px purple;
}
header h1{margin:0;color:violet;font-size:18px}

/* NAV */
.nav{
position:fixed;
bottom:0;
left:0;
right:0;
display:flex;
justify-content:space-around;
background:#120018;
padding:8px;
}

.nav button{
background:purple;
color:white;
border:none;
padding:10px;
border-radius:10px;
font-size:12px;
}

/* PAGES */
.page{display:none;padding:10px;padding-bottom:80px}
.active{display:block}

/* CARD */
.card{
background:#1b1b1b;
padding:10px;
margin:8px 0;
border-radius:10px;
box-shadow:0 0 8px purple;
}

/* INPUT */
input{
width:100%;
padding:10px;
margin:5px 0;
border:none;
border-radius:8px;
}

small{color:gray}
</style>
</head>

<body>

<header>
<h1>💜 Znoog Community</h1>
<small id="levelBox">Level 1 | XP 0</small>
</header>

<!-- HOME -->
<div id="home" class="page active">
<div class="card">
<h3>🔥 Welcome</h3>
<p>أقوى مجتمع تفاعلي عربي</p>
</div>
</div>

<!-- CHAT -->
<div id="chat" class="page">

<div class="card">
<h3>💬 الشات</h3>
<input id="name" placeholder="اسمك">
<input id="msg" placeholder="رسالتك">
<button onclick="sendMsg()">إرسال + XP</button>
</div>

<div id="chatBox"></div>
</div>

<!-- MEMBERS -->
<div id="members" class="page">
<div class="card">
<h3>👥 الأعضاء</h3>
<div id="membersBox"></div>
</div>
</div>

<!-- ADMIN -->
<div id="admin" class="page">
<div class="card">
<h3>🔐 الأدمن</h3>

<input id="adminPass" placeholder="كلمة السر">
<button onclick="loginAdmin()">دخول</button>

<div id="adminPanel" style="display:none">
<input id="target" placeholder="اسم العضو">
<input id="xpVal" placeholder="XP جديد">
<button onclick="setXP()">تحديث XP</button>
</div>

</div>
</div>

<!-- NAV -->
<div class="nav">
<button onclick="show('home')">🏠</button>
<button onclick="show('chat')">💬</button>
<button onclick="show('members')">👥</button>
<button onclick="show('admin')">🔐</button>
</div>

<script>

/* 🔥 FIREBASE CONFIG (مربوط بالكامل) */
const firebaseConfig = {
  apiKey:"AIzaSy...",
  authDomain:"velora-rp.firebaseapp.com",
  databaseURL:"https://velora-rp-default-rtdb.europe-west1.firebasedatabase.app",
  projectId:"velora-rp",
  storageBucket:"velora-rp.firebasestorage.app",
  messagingSenderId:"681356163114",
  appId:"1:681356163114:web:c40b8d7fed229ce8e7eb53"
};

firebase.initializeApp(firebaseConfig);
const db = firebase.database();

/* ================= NAV ================= */
function show(id){
document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
document.getElementById(id).classList.add("active");
}

/* ================= XP ================= */
let xp = 0;

function updateLevel(){
let level = Math.floor(xp/100)+1;
document.getElementById("levelBox").innerText =
`Level ${level} | XP ${xp}`;
}

/* ================= CHAT ================= */
function sendMsg(){
let name=document.getElementById("name").value;
let msg=document.getElementById("msg").value;

if(!name || !msg) return;

db.ref("chat").push({
name,
msg,
time:Date.now()
});

xp += 10;
updateLevel();

db.ref("members/"+name).set({
name,
xp
});
}

/* LIVE CHAT */
db.ref("chat").on("value",snap=>{
let html="";
snap.forEach(s=>{
let d=s.val();
html+=`
<div class="card">
<b>${d.name}</b>
<p>${d.msg}</p>
</div>`;
});
document.getElementById("chatBox").innerHTML=html;
});

/* LIVE MEMBERS */
db.ref("members").on("value",snap=>{
let html="";
snap.forEach(s=>{
let d=s.val();
let level=Math.floor((d.xp||0)/100)+1;
html+=`
<div class="card">
<b>${d.name}</b>
<p>XP: ${d.xp||0} | Level: ${level}</p>
</div>`;
});
document.getElementById("membersBox").innerHTML=html;
});

/* ================= ADMIN ================= */
let isAdmin=false;
const ADMIN_PASS="008877";

function loginAdmin(){
let pass=document.getElementById("adminPass").value;
if(pass===ADMIN_PASS){
isAdmin=true;
document.getElementById("adminPanel").style.display="block";
alert("تم دخول الأدمن 🔥");
}else{
alert("كلمة خطأ");
}
}

function setXP(){
if(!isAdmin) return;

let name=document.getElementById("target").value;
let xpVal=parseInt(document.getElementById("xpVal").value);

db.ref("members/"+name).update({
name,
xp:xpVal
});
}

updateLevel();
</script>

</body>
</html>
