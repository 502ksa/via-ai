<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Via AI - المنصة الذكية الفاخرة</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800;900&display=swap');

*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}

:root {
  --bg: #09090b; --s1: #121218; --s2: #181825; --s3: #1f1f30;
  --border: rgba(255, 255, 255, 0.05); --border2: rgba(255, 255, 255, 0.09);
  --p: #8b5cf6; --p2: #a78bfa; --pg: rgba(139, 92, 246, 0.15);
  --text: #f4f4f5; --t2: #a1a1aa; --t3: #71717a; --red: #ef4444;
}

[data-theme="light"] {
  --bg: #f8fafc; --s1: #ffffff; --s2: #f1f5f9; --s3: #e2e8f0;
  --border: rgba(0, 0, 0, 0.04); --border2: rgba(0, 0, 0, 0.08);
  --p: #6d28d9; --text: #0f172a; --t2: #475569; --t3: #94a3b8;
}

html,body{height:100%;font-family:'Cairo',sans-serif;background:var(--bg);color:var(--text);overflow:hidden;}

#gate{position:fixed;inset:0;z-index:9999;background:var(--bg);display:flex;align-items:center;justify-content:center;padding:20px;}
.gate-card{width:100%;max-width:460px;background:var(--s1);border:1px solid var(--border2);border-radius:24px;padding:40px;text-align:center;}

#app{display:none;height:100vh;flex-direction:column;}
#app.show{display:flex;}

.app-body{display:flex;flex:1;overflow:hidden;position:relative;}

/* FIX: تصحيح العرض التجاوبي ومنع تداخل المحتوى */
.sidebar{width:260px;background:var(--s1);border-left:1px solid var(--border);flex-shrink:0;overflow-y:auto;transition:0.3s;}
.content{flex:1;display:flex;flex-direction:column;overflow:hidden;background:var(--bg);position:relative;}
.page{display:none;flex:1;overflow-y:auto;height:100%;}
.page.active{display:flex;flex-direction:column;}

.tool-layout{display:flex;flex:1;overflow:hidden;flex-direction:row;}
.tool-form-side{width:400px;border-left:1px solid var(--border);padding:20px;overflow-y:auto;}
.tool-chat-side{flex:1;display:flex;flex-direction:column;overflow:hidden;background:var(--s1);}

.chat-messages{flex:1;overflow-y:auto;padding:20px;display:flex;flex-direction:column;gap:15px;}
.msg{max-width:90%;margin-bottom:10px;padding:12px;border-radius:12px;background:var(--s2);align-self:flex-start;}

@media(max-width:768px){
  .tool-layout{flex-direction:column;}
  .tool-form-side{width:100%;height:auto;flex:none;}
  .tool-chat-side{height:400px;}
}

.run-btn{width:100%;background:var(--p);color:white;padding:15px;border-radius:12px;border:none;cursor:pointer;font-weight:bold;margin-top:20px;}
</style>
</head>
<body>

<div id="gate">
  <div class="gate-card">
    <div style="font-size:30px; font-weight:900; color:var(--p); margin-bottom:20px;">Via AI</div>
    <input type="password" id="gate-key" style="width:100%; padding:15px; background:var(--s2); border:1px solid var(--border2); border-radius:12px; color:white; margin-bottom:10px;" placeholder="API Key...">
    <button class="run-btn" onclick="enterApp()">دخول</button>
  </div>
</div>

<div id="app">
  <div class="app-body">
    <div class="sidebar" id="sidebar">
      <div style="padding:20px; font-weight:800; color:var(--p);">القائمة الرئيسية</div>
      <div class="nav-item" onclick="goTo('home')" style="padding:15px 20px; cursor:pointer;">الرئيسية</div>
      <div class="nav-item" onclick="goTo('cv')" style="padding:15px 20px; cursor:pointer;">السيرة الذاتية</div>
    </div>
    
    <div class="content">
      <div class="page active" id="page-home">
        <div style="padding:40px;"><h1>مرحباً بك في Via AI</h1></div>
      </div>
      
      <div class="page" id="page-cv">
        <div class="tool-layout">
          <div class="tool-form-side">
            <h2>مصمم السيرة الذاتية</h2>
            <textarea id="cv-data" style="width:100%; height:200px; background:var(--s2); color:white; padding:10px; border-radius:10px; margin-top:10px;"></textarea>
            <button class="run-btn" onclick="runTool('cv')">توليد الآن</button>
          </div>
          <div class="tool-chat-side" id="cv-chat">
            <div class="chat-messages" id="cv-msgs"></div>
            <div style="padding:10px; border-top:1px solid var(--border);">
               <input id="cv-inp" style="width:100%; padding:10px; background:var(--s2); color:white; border:none; border-radius:8px;" placeholder="رسالة إضافية...">
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<script>
var API_KEY = localStorage.getItem('via_ai_key') || '';

function enterApp(){
  API_KEY = document.getElementById('gate-key').value;
  localStorage.setItem('via_ai_key', API_KEY);
  document.getElementById('gate').style.display='none';
  document.getElementById('app').classList.add('show');
}

function goTo(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
}

// FIX: التوليد الفوري (Streaming)
async function runTool(toolId){
  const msgsEl = document.getElementById(toolId+'-msgs');
  msgsEl.innerHTML = '<div class="msg">جاري التوليد...</div>';
  
  const response = await fetch('https://api.anthropic.com/v1/messages', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'x-api-key': API_KEY,
      'anthropic-version': '2023-06-01',
      'anthropic-dangerous-direct-browser-access': 'true'
    },
    body: JSON.stringify({
      model: 'claude-sonnet-4-6', // التعديل المطلوب
      max_tokens: 4000,
      stream: true,
      messages: [{role: 'user', content: document.getElementById('cv-data').value}]
    })
  });

  const reader = response.body.getReader();
  const decoder = new TextDecoder();
  msgsEl.innerHTML = ''; 
  const msgDiv = document.createElement('div');
  msgDiv.className = 'msg';
  msgsEl.appendChild(msgDiv);

  while(true){
    const {done, value} = await reader.read();
    if(done) break;
    const chunk = decoder.decode(value, {stream: true});
    const lines = chunk.split('\n');
    for(const line of lines){
      if(line.startsWith('data: ')){
        try{
          const json = JSON.parse(line.substring(6));
          if(json.delta && json.delta.text) msgDiv.innerText += json.delta.text;
          msgsEl.scrollTop = msgsEl.scrollHeight;
        }catch(e){}
      }
    }
  }
}
</script>
</body>
</html>
