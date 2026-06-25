<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AI Workspace</title>

<style>
body{
margin:0;
font-family:Arial;
background:#0f0f14;
color:white;
}

/* LAYOUT */
.container{
display:flex;
height:100vh;
}

/* SIDEBAR */
.sidebar{
width:260px;
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

.sidebar button:hover{
background:#333;
}

/* MAIN */
.main{
flex:1;
display:flex;
flex-direction:column;
}

/* CHAT */
.chat{
flex:1;
padding:15px;
overflow:auto;
}

.msg{
padding:10px;
margin:8px 0;
border-radius:8px;
white-space:pre-wrap;
}

.user{background:#2a2a3a}
.ai{background:#1c1c24}

/* INPUT */
.inputBar{
display:flex;
padding:10px;
gap:10px;
border-top:1px solid #222;
}

input{
flex:1;
padding:10px;
background:#111;
border:1px solid #333;
color:white;
}

button{
padding:10px 15px;
background:#6c63ff;
border:0;
color:white;
cursor:pointer;
}

/* LANDING */
.landing{
display:flex;
flex-direction:column;
justify-content:center;
align-items:center;
height:100vh;
text-align:center;
}

.card{
background:#181820;
padding:20px;
border-radius:10px;
width:300px;
}

.hidden{display:none}

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

<!-- LANDING -->
<div id="landing" class="landing">
  <div class="card">
    <h2>AI Workspace</h2>
    <p>Enter your API Key to start</p>
    <input id="key" placeholder="sk-ant-...">
    <button onclick="enter()">Enter</button>
  </div>
</div>

<!-- APP -->
<div id="app" class="container hidden">

  <!-- SIDEBAR -->
  <div class="sidebar">
    <button onclick="setMode('chat')">Chat</button>
    <button onclick="setMode('cv')">CV</button>
    <button onclick="setMode('cover')">Cover</button>
    <button onclick="setMode('interview')">Interview</button>
    <button onclick="setMode('summary')">Summary</button>
    <button onclick="openLibrary()">Library</button>
  </div>

  <!-- MAIN -->
  <div class="main">

    <div id="chat" class="chat"></div>

    <div id="library" class="chat hidden"></div>

    <div class="inputBar">
      <input id="input" placeholder="Type here...">
      <button onclick="send()">Send</button>
    </div>

  </div>

</div>

<script>
let apiKey="";
let mode="chat";
let memory=[];

/* ENTER */
function enter(){
apiKey=document.getElementById("key").value;
if(!apiKey) return;
localStorage.setItem("key",apiKey);
document.getElementById("landing").classList.add("hidden");
document.getElementById("app").classList.remove("hidden");
}

/* LOAD KEY */
if(localStorage.getItem("key")){
apiKey=localStorage.getItem("key");
document.getElementById("landing").classList.add("hidden");
document.getElementById("app").classList.remove("hidden");
}

/* MODE */
function setMode(m){
mode=m;
}

/* CHAT UI */
function addMsg(text,type){
let div=document.createElement("div");
div.className="msg "+type;
div.innerText=text;
document.getElementById("chat").appendChild(div);
document.getElementById("chat").scrollTop=999999;
}

/* CALL AI */
async function ask(prompt){
let res=await fetch("https://api.anthropic.com/v1/messages",{
method:"POST",
headers:{
"content-type":"application/json",
"x-api-key":apiKey,
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

/* ROUTER */
function route(text){

text=text.toLowerCase();

if(text.includes("cv")) return "cv";
if(text.includes("cover")) return "cover";
if(text.includes("interview")) return "interview";
if(text.includes("summary")||text.includes("تلخيص")) return "summary";

return "chat";
}

/* SAVE TO LIBRARY */
function save(item){
memory.push(item);
localStorage.setItem("lib",JSON.stringify(memory));
}

/* LOAD LIB */
if(localStorage.getItem("lib")){
memory=JSON.parse(localStorage.getItem("lib"));
}

/* LIBRARY */
function openLibrary(){
document.getElementById("chat").classList.add("hidden");
document.getElementById("library").classList.remove("hidden");

let html="";
memory.forEach((m,i)=>{
html+=`<div class="msg ai">${m}</div>`;
});

document.getElementById("library").innerHTML=html;
}

/* SEND */
async function send(){
let input=document.getElementById("input");
let text=input.value;
input.value="";

addMsg(text,"user");

let detected=route(text);

let prompt="";

if(detected==="cv"){
prompt="Create professional CV:\n"+text;
}
else if(detected==="cover"){
prompt="Write cover letter:\n"+text;
}
else if(detected==="interview"){
prompt="Create interview questions:\n"+text;
}
else if(detected==="summary"){
prompt="Summarize:\n"+text;
}
else{
prompt=text;
}

let reply=await ask(prompt);

addMsg(reply,"ai");

save("Q: "+text+"\nA: "+reply);
}
</script>

</body>
</html>
