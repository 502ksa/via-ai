<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AI Tools Workspace</title>

<style>
body{
margin:0;
font-family:Arial;
background:#0f0f14;
color:white;
}

/* HERO */
.hero{
height:100vh;
display:flex;
flex-direction:column;
justify-content:center;
align-items:center;
text-align:center;
padding:20px;
}

.hero button{
padding:12px 20px;
background:#6c63ff;
border:0;
color:white;
cursor:pointer;
margin-top:10px;
border-radius:8px;
}

/* APP */
.app{display:none}

/* LAYOUT */
.container{
display:flex;
height:100vh;
}

/* SIDEBAR */
.sidebar{
width:250px;
background:#181820;
padding:15px;
display:flex;
flex-direction:column;
gap:10px;
}

.sidebar button{
padding:10px;
background:#222;
color:white;
border:0;
cursor:pointer;
border-radius:6px;
}

/* MAIN */
.main{
flex:1;
display:flex;
flex-direction:column;
}

/* TOOL */
.tool{
display:none;
padding:15px;
flex:1;
overflow:auto;
}

.active{display:block}

/* INPUT */
input,textarea{
width:100%;
padding:10px;
background:#111;
border:1px solid #333;
color:white;
margin-bottom:10px;
}

button{
padding:10px 15px;
background:#6c63ff;
border:0;
color:white;
cursor:pointer;
}

/* ASSISTANT */
.helper{
background:#1c1c24;
padding:10px;
margin-bottom:10px;
border-radius:8px;
font-size:13px;
opacity:0.9;
}

/* RESULT */
.result{
background:#2a2a3a;
padding:10px;
margin-top:10px;
white-space:pre-wrap;
}

/* MOBILE */
@media(max-width:768px){
.container{flex-direction:column;}
.sidebar{
width:100%;
flex-direction:row;
overflow:auto;
}
}
</style>
</head>

<body>

<!-- HERO -->
<div id="hero" class="hero">
  <h1>AI Tools Workspace</h1>
  <p>Professional AI tools with smart assistant inside</p>
  <input id="key" placeholder="API Key">
  <button onclick="start()">Start</button>
</div>

<!-- APP -->
<div id="app" class="app">

<div class="container">

<!-- SIDEBAR -->
<div class="sidebar">
<button onclick="show('cv')">CV</button>
<button onclick="show('cover')">Cover</button>
<button onclick="show('interview')">Interview</button>
<button onclick="show('summary')">Summary</button>
<button onclick="show('explain')">Explain</button>
<button onclick="show('slides')">Slides</button>
<button onclick="show('library')">Library</button>
</div>

<!-- MAIN -->
<div class="main">

<!-- CV -->
<div id="cv" class="tool active">
<div class="helper">Tip: اكتب بياناتك أو قول لي “ابغى CV قوي لمطور” وأنا أساعدك أرتبه</div>
<textarea id="cvInput"></textarea>
<button onclick="run('cv')">Generate CV</button>
<div id="cvOut" class="result"></div>
</div>

<!-- COVER -->
<div id="cover" class="tool">
<div class="helper">اكتب أو صف الوظيفة وأنا أرتب لك خطاب احترافي</div>
<textarea id="coverInput"></textarea>
<button onclick="run('cover')">Generate</button>
<div id="coverOut" class="result"></div>
</div>

<!-- INTERVIEW -->
<div id="interview" class="tool">
<div class="helper">صف الوظيفة وأنا أجهز لك أسئلة وإجابات</div>
<textarea id="intInput"></textarea>
<button onclick="run('interview')">Generate</button>
<div id="intOut" class="result"></div>
</div>

<!-- SUMMARY -->
<div id="summary" class="tool">
<div class="helper">الصق النص وأنا ألخصه لك</div>
<textarea id="sumInput"></textarea>
<button onclick="run('summary')">Summarize</button>
<div id="sumOut" class="result"></div>
</div>

<!-- EXPLAIN -->
<div id="explain" class="tool">
<div class="helper">اكتب أي مفهوم صعب وأنا أبسطه لك</div>
<input id="expInput">
<button onclick="run('explain')">Explain</button>
<div id="expOut" class="result"></div>
</div>

<!-- SLIDES -->
<div id="slides" class="tool">
<div class="helper">اعطني موضوع العرض وأنا أجهز لك سلايدات</div>
<textarea id="slInput"></textarea>
<button onclick="run('slides')">Create</button>
<div id="slOut" class="result"></div>
</div>

<!-- LIBRARY -->
<div id="library" class="tool">
<div class="helper">كل أعمالك محفوظة هنا</div>
<div id="libBox"></div>
</div>

</div>

</div>

</div>

<script>
let key="";
let lib=[];

/* START */
function start(){
key=document.getElementById("key").value;
if(!key) return;

localStorage.setItem("key",key);

document.getElementById("hero").style.display="none";
document.getElementById("app").style.display="block";
}

/* LOAD */
if(localStorage.getItem("key")){
key=localStorage.getItem("key");
document.getElementById("hero").style.display="none";
document.getElementById("app").style.display="block";
}

/* SHOW */
function show(id){
document.querySelectorAll(".tool").forEach(t=>t.classList.remove("active"));
document.getElementById(id).classList.add("active");
if(id==="library") loadLib();
}

/* AI */
async function ask(prompt){
let res=await fetch("https://api.anthropic.com/v1/messages",{
method:"POST",
headers:{
"content-type":"application/json",
"x-api-key":key,
"anthropic-version":"2023-06-01"
},
body:JSON.stringify({
model:"claude-sonnet-4-6",
max_tokens:2000,
messages:[{role:"user",content:prompt}]
})
});

let data=await res.json();
return data.content[0].text;
}

/* RUN */
async function run(type){

let input=document.getElementById(type+"Input").value;

/* SMART HELPER INSIDE TOOL */
let helperPrompt="ساعد المستخدم يحسن طلبه باختصار: "+input;
let refined=input;

if(input.length<20){
refined = await ask(helperPrompt);
}

/* TOOL ROUTER */
let prompt="";

if(type==="cv") prompt="Write professional CV:\n"+refined;
if(type==="cover") prompt="Write cover letter:\n"+refined;
if(type==="interview") prompt="Create interview Q&A:\n"+refined;
if(type==="summary") prompt="Summarize:\n"+refined;
if(type==="explain") prompt="Explain simply:\n"+refined;
if(type==="slides") prompt="Create presentation slides:\n"+refined;

let res=await ask(prompt);

document.getElementById(type+"Out").innerText=res;

/* SAVE */
lib.push(type.toUpperCase()+": "+res);
localStorage.setItem("lib",JSON.stringify(lib));
}

/* LIB */
function loadLib(){
if(localStorage.getItem("lib")){
lib=JSON.parse(localStorage.getItem("lib"));
}

document.getElementById("libBox").innerHTML=
lib.map(x=>"<div class='result'>"+x+"</div>").join("");
}
</script>

</body>
</html>
