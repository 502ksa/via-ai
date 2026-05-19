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
  --gold:#f0b429;--danger:#f04747;--success:#43b581;
  --text:#e8e8f5;--muted:#5a5a80;--muted2:#8888aa;
  --sw:60px;--sideW:230px;--hh:52px;
}
*{box-sizing:border-box;margin:0;padding:0}
html,body{height:100%;overflow:hidden}
body{font-family:'Cairo',sans-serif;background:var(--bg);color:var(--text);display:flex;flex-direction:column}
.app{display:flex;height:100vh;overflow:hidden}

/* SERVER STRIP */
.strip{width:var(--sw);flex-shrink:0;background:#06060e;display:flex;flex-direction:column;align-items:center;padding:10px 0;gap:6px;border-left:1px solid var(--border);overflow-y:auto}
.s-icon{width:44px;height:44px;border-radius:50%;background:var(--accent);display:flex;align-items:center;justify-content:center;font-family:'Tajawal',sans-serif;font-weight:900;font-size:16px;cursor:pointer;transition:border-radius .2s,filter .2s;flex-shrink:0}
.s-icon.active{border-radius:14px;background:var(--teal);color:#000}
.s-icon:hover:not(.active){border-radius:14px;filter:brightness(1.2)}
.s-div{width:30px;height:1px;background:var(--border);margin:2px 0}

/* SIDEBAR */
.sidebar{width:var(--sideW);flex-shrink:0;background:var(--sidebar);display:flex;flex-direction:column;border-left:1px solid var(--border);overflow:hidden}
.sb-hdr{padding:14px 14px 10px;border-bottom:1px solid var(--border);flex-shrink:0}
.sb-title{font-family:'Tajawal',sans-serif;font-weight:900;font-size:17px;background:linear-gradient(135deg,var(--accent2),var(--teal));-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.sb-sub{font-size:11px;color:var(--muted);margin-top:2px}
.sb-sec{padding:12px 10px 4px;font-size:10px;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:1px}
.ch-btn{display:flex;align-items:center;gap:8px;padding:7px 10px;border-radius:8px;cursor:pointer;transition:background .15s,color .15s;color:var(--muted2);font-size:13px;font-weight:600;margin:1px 6px;position:relative}
.ch-btn:hover{background:var(--surface2);color:var(--text)}
.ch-btn.active{background:var(--surface3);color:var(--text)}
.ch-icon{font-size:14px;width:18px;text-align:center;flex-shrink:0}
.ch-notif{margin-right:auto;background:var(--danger);width:17px;height:17px;border-radius:50%;font-size:10px;font-weight:700;color:#fff;display:flex;align-items:center;justify-content:center}
.ch-notif.hidden{display:none}

/* SIDEBAR PROFILE */
.sb-prof{margin-top:auto;padding:8px 10px;border-top:1px solid var(--border);display:flex;align-items:center;gap:8px;cursor:pointer;transition:background .2s;border-radius:8px;flex-shrink:0;margin:auto 6px 6px}
.sb-prof:hover{background:var(--surface2)}
.sp-av{width:34px;height:34px;border-radius:50%;object-fit:cover;flex-shrink:0;background:var(--surface2)}
.sp-info{flex:1;min-width:0}
.sp-name{font-size:13px;font-weight:700;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.sp-lvl{font-size:10px;color:var(--muted2)}

/* MAIN */
.main{flex:1;display:flex;flex-direction:column;overflow:hidden;min-width:0}
.ch-hdr{height:var(--hh);flex-shrink:0;background:rgba(8,8,15,.85);backdrop-filter:blur(16px);border-bottom:1px solid var(--border);display:flex;align-items:center;gap:10px;padding:0 16px}
.ch-hdr-icon{font-size:17px}
.ch-hdr-name{font-family:'Tajawal',sans-serif;font-weight:800;font-size:16px}
.ch-hdr-desc{font-size:12px;color:var(--muted);margin-right:8px;padding-right:8px;border-right:1px solid var(--border2)}

/* PAGES */
.page{display:none;flex:1;overflow:hidden;flex-direction:column}
.page.active{display:flex}

/* CHAT */
.feed{flex:1;overflow-y:auto;padding:12px 16px;display:flex;flex-direction:column;gap:1px}
.feed::-webkit-scrollbar{width:4px}
.feed::-webkit-scrollbar-thumb{background:var(--border2);border-radius:2px}

.msg-g{display:flex;gap:10px;padding:5px 8px;border-radius:10px;transition:background .15s;position:relative}
.msg-g:hover{background:rgba(255,255,255,.025)}
.msg-g:hover .msg-acts{opacity:1}
.msg-av{flex-shrink:0;padding-top:2px}
.msg-body{flex:1;min-width:0}
.msg-meta{display:flex;align-items:center;gap:7px;margin-bottom:3px;flex-wrap:wrap}
.msg-nm{font-weight:700;font-size:14px}
.msg-nm.adm{color:var(--gold)}
.msg-nm.vip{color:var(--accent2)}
.msg-nm.mod{color:var(--teal)}
.mbadge{font-size:9px;padding:2px 6px;border-radius:50px;font-weight:800}
.b-adm{background:rgba(240,180,41,.15);color:var(--gold);border:1px solid rgba(240,180,41,.4)}
.b-vip{background:rgba(88,101,242,.15);color:var(--accent2);border:1px solid rgba(88,101,242,.4)}
.b-mod{background:rgba(0,212,170,.1);color:var(--teal);border:1px solid rgba(0,212,170,.3)}
.msg-time{font-size:10px;color:var(--muted)}
.msg-txt{font-size:14px;line-height:1.65;word-break:break-word}
.msg-img{max-width:280px;max-height:200px;border-radius:10px;margin-top:5px;cursor:pointer;object-fit:cover;display:block}

/* REACTIONS */
.rx-row{display:flex;flex-wrap:wrap;gap:4px;margin-top:5px;position:relative}
.rx-chip{background:var(--surface3);border:1px solid var(--border2);border-radius:50px;padding:3px 9px;font-size:12px;cursor:pointer;transition:all .15s;display:flex;align-items:center;gap:3px}
.rx-chip:hover,.rx-chip.mine{background:rgba(88,101,242,.2);border-color:var(--accent)}
.rx-chip span{font-size:11px;font-weight:700;color:var(--muted2)}
.rx-add{background:var(--surface2);border:1px solid var(--border);border-radius:50px;padding:3px 9px;font-size:13px;cursor:pointer;color:var(--muted2);transition:all .15s}
.rx-add:hover{border-color:var(--accent);color:var(--accent2)}
.rx-picker{position:absolute;bottom:28px;right:0;background:var(--surface2);border:1px solid var(--border2);border-radius:12px;padding:8px;display:flex;gap:8px;z-index:50;box-shadow:0 4px 20px rgba(0,0,0,.4)}
.rx-picker span{font-size:20px;cursor:pointer;transition:transform .15s}
.rx-picker span:hover{transform:scale(1.3)}

/* MSG ACTIONS */
.msg-acts{position:absolute;top:-12px;left:8px;background:var(--surface2);border:1px solid var(--border2);border-radius:10px;padding:4px 6px;display:flex;gap:4px;opacity:0;transition:opacity .15s;z-index:10}
.act-b{background:none;border:none;cursor:pointer;font-size:13px;padding:3px 5px;border-radius:6px;transition:background .15s;color:var(--muted2)}
.act-b:hover{background:var(--surface3);color:var(--text)}
.act-b.del{color:var(--danger)}

/* PINNED */
.pin-bar{background:rgba(88,101,242,.08);border-bottom:1px solid rgba(88,101,242,.2);padding:7px 16px;display:flex;align-items:center;gap:8px;font-size:12px;color:var(--accent2);flex-shrink:0}

/* CHAT INPUT */
.ci-wrap{padding:10px 14px;flex-shrink:0}
.ci-box{background:var(--surface2);border:1px solid var(--border2);border-radius:12px;padding:9px 12px;display:flex;align-items:center;gap:8px;transition:border-color .2s}
.ci-box:focus-within{border-color:var(--accent)}
.ci-inp{flex:1;background:none;border:none;outline:none;color:var(--text);font-family:'Cairo',sans-serif;font-size:14px}
.ci-inp::placeholder{color:var(--muted)}
.ci-icon{background:none;border:none;color:var(--muted2);cursor:pointer;font-size:17px;padding:2px;transition:color .2s}
.ci-icon:hover{color:var(--accent2)}
.send-b{background:var(--accent);color:#fff;border:none;padding:7px 16px;border-radius:9px;font-family:'Cairo',sans-serif;font-weight:700;font-size:13px;cursor:pointer;transition:opacity .2s,transform .1s;white-space:nowrap}
.send-b:active{transform:scale(.95);opacity:.8}
.spam-w{background:rgba(240,71,71,.1);border:1px solid var(--danger);color:var(--danger);border-radius:8px;padding:6px 14px;font-size:12px;font-weight:700;text-align:center;margin-bottom:6px;display:none}

/* MEDIA */
.upload-area{border:2px dashed var(--border2);border-radius:14px;padding:20px;text-align:center;cursor:pointer;transition:border-color .2s,background .2s;margin:14px;flex-shrink:0}
.upload-area:hover{border-color:var(--accent);background:rgba(88,101,242,.04)}
.upload-area h4{font-family:'Tajawal',sans-serif;font-weight:800;font-size:14px;margin-bottom:3px}
.upload-area p{font-size:11px;color:var(--muted)}
.media-grid{flex:1;overflow-y:auto;padding:0 14px 14px;display:grid;grid-template-columns:repeat(auto-fill,minmax(150px,1fr));gap:10px;align-content:start}
.media-grid::-webkit-scrollbar{width:4px}
.media-grid::-webkit-scrollbar-thumb{background:var(--border2);border-radius:2px}
.mc{background:var(--surface);border:1px solid var(--border);border-radius:12px;overflow:hidden;position:relative;aspect-ratio:1;cursor:pointer;transition:transform .2s,border-color .2s}
.mc:hover{transform:scale(1.02);border-color:var(--accent)}
.mc img,.mc video{width:100%;height:100%;object-fit:cover}
.mc-ov{position:absolute;inset:0;background:linear-gradient(to top,rgba(0,0,0,.8),transparent);opacity:0;transition:opacity .2s;display:flex;align-items:flex-end;padding:8px}
.mc:hover .mc-ov{opacity:1}
.mc-name{font-size:11px;font-weight:700;color:#fff}
.mc-saved{position:absolute;top:7px;left:7px;background:rgba(240,180,41,.9);color:#000;border-radius:50px;padding:2px 7px;font-size:9px;font-weight:800}
.mc-exp{position:absolute;top:7px;right:7px;background:rgba(240,71,71,.8);color:#fff;border-radius:50px;padding:2px 7px;font-size:9px;font-weight:700}
.save-btn{background:rgba(240,180,41,.85);border:none;border-radius:6px;padding:3px 7px;font-size:10px;font-weight:800;cursor:pointer;color:#000;margin-top:4px;display:block}

/* MEMBERS */
.m-pg{flex:1;overflow-y:auto;padding:14px}
.m-pg::-webkit-scrollbar{width:4px}
.m-pg::-webkit-scrollbar-thumb{background:var(--border2);border-radius:2px}
.m-tabs{display:flex;gap:8px;margin-bottom:14px}
.m-tab{flex:1;background:var(--surface);border:1px solid var(--border);color:var(--muted2);padding:8px;border-radius:10px;font-family:'Cairo',sans-serif;font-size:13px;font-weight:700;cursor:pointer;transition:all .2s}
.m-tab.active{background:var(--surface3);border-color:var(--accent);color:var(--accent2)}
.sec-hdr{font-family:'Tajawal',sans-serif;font-weight:800;font-size:14px;margin-bottom:10px;display:flex;align-items:center;gap:8px}
.sec-hdr::after{content:'';flex:1;height:1px;background:linear-gradient(90deg,var(--accent),transparent)}
.m-row{display:flex;align-items:center;gap:10px;background:var(--surface);border:1px solid var(--border);border-radius:12px;padding:10px 12px;margin-bottom:8px;transition:border-color .2s;cursor:pointer}
.m-row:hover{border-color:var(--accent)}
.rk{font-family:'Tajawal',sans-serif;font-weight:900;font-size:14px;min-width:22px;text-align:center;color:var(--muted)}
.r1{color:var(--gold);text-shadow:0 0 8px var(--gold)}.r2{color:#9ca3af}.r3{color:#b45309}
.m-info{flex:1;min-width:0}
.m-nm{font-weight:700;font-size:13px}
.m-sb{font-size:11px;color:var(--muted2);margin-top:1px}
.xb-w{background:var(--surface2);border-radius:50px;height:4px;margin-top:4px;overflow:hidden}
.xb{height:100%;border-radius:50px;background:linear-gradient(90deg,var(--accent),var(--accent2));transition:width .5s}
.m-xp{font-family:'Tajawal',sans-serif;font-weight:800;font-size:12px;color:var(--accent2);min-width:50px;text-align:left}
.feat-row{display:flex;align-items:center;gap:12px;background:linear-gradient(135deg,rgba(88,101,242,.1),rgba(0,212,170,.05));border:1px solid rgba(88,101,242,.3);border-radius:14px;padding:12px;margin-bottom:8px}
.f-info{flex:1}
.f-nm{font-weight:800;font-size:14px}
.f-desc{font-size:11px;color:var(--muted2);margin-top:2px}
.f-badges{display:flex;gap:5px;margin-top:5px;flex-wrap:wrap}

/* EVENTS */
.ev-pg{flex:1;overflow-y:auto;padding:14px}
.ev-pg::-webkit-scrollbar{width:4px}
.ev-pg::-webkit-scrollbar-thumb{background:var(--border2);border-radius:2px}
.ev-card{background:var(--surface);border:1px solid var(--border);border-radius:14px;padding:14px;margin-bottom:10px;transition:border-color .2s}
.ev-card:hover{border-color:var(--teal)}
.ev-top{display:flex;align-items:flex-start;gap:10px;margin-bottom:10px}
.ev-date{background:var(--surface2);border:1px solid var(--border2);border-radius:10px;padding:7px 10px;text-align:center;flex-shrink:0;min-width:48px}
.ev-day{font-family:'Tajawal',sans-serif;font-weight:900;font-size:22px;color:var(--teal);line-height:1}
.ev-mon{font-size:10px;color:var(--muted2)}
.ev-title{font-family:'Tajawal',sans-serif;font-weight:800;font-size:15px}
.ev-desc{font-size:12px;color:var(--muted2);margin-top:3px}
.ev-foot{display:flex;align-items:center;gap:8px;flex-wrap:wrap}
.ev-time{font-size:12px;color:var(--muted2)}
.att-btn{margin-right:auto;background:rgba(0,212,170,.1);border:1px solid var(--teal);color:var(--teal);padding:5px 14px;border-radius:8px;font-family:'Cairo',sans-serif;font-size:12px;font-weight:700;cursor:pointer;transition:all .2s}
.att-btn:hover,.att-btn.yes{background:var(--teal);color:#000}

/* ADMIN */
.adm-pg{flex:1;overflow-y:auto;padding:14px}
.adm-pg::-webkit-scrollbar{width:4px}
.adm-pg::-webkit-scrollbar-thumb{background:var(--border2);border-radius:2px}
.a-card{background:var(--surface);border:1px solid var(--border);border-radius:14px;padding:14px;margin-bottom:10px}
.a-card h4{font-family:'Tajawal',sans-serif;font-weight:800;font-size:14px;color:var(--accent2);margin-bottom:10px}
.inp{width:100%;background:var(--surface2);border:1px solid var(--border2);color:var(--text);padding:8px 12px;border-radius:9px;font-family:'Cairo',sans-serif;font-size:13px;outline:none;transition:border-color .2s;margin-bottom:8px}
.inp:focus{border-color:var(--accent)}
.inp::placeholder{color:var(--muted)}
.btn-p{background:linear-gradient(135deg,var(--accent),var(--accent2));border:none;color:#fff;padding:9px;border-radius:9px;font-family:'Cairo',sans-serif;font-weight:700;font-size:13px;cursor:pointer;width:100%;margin-top:2px}
.btn-p:active{opacity:.8}
.btn-d{background:rgba(240,71,71,.1);border:1px solid var(--danger);color:var(--danger);padding:8px;border-radius:9px;font-family:'Cairo',sans-serif;font-weight:700;font-size:13px;cursor:pointer;width:100%;margin-bottom:6px}
.lock-wrap{display:flex;flex:1;align-items:center;justify-content:center;flex-direction:column;gap:14px;padding:20px;text-align:center}
.lock-wrap h3{font-family:'Tajawal',sans-serif;font-weight:900;font-size:18px;color:var(--gold)}

/* PROFILE MODAL */
.mo{position:fixed;inset:0;background:rgba(0,0,0,.75);backdrop-filter:blur(8px);z-index:1000;display:flex;align-items:center;justify-content:center;padding:16px}
.mo.h{display:none}
.mo-box{background:var(--surface);border:1px solid var(--border2);border-radius:20px;width:100%;max-width:400px;max-height:90vh;overflow-y:auto;padding:22px;animation:moIn .25s ease}
@keyframes moIn{from{opacity:0;transform:scale(.95)}to{opacity:1;transform:scale(1)}}
.mo-box h2{font-family:'Tajawal',sans-serif;font-weight:900;font-size:19px;text-align:center;margin-bottom:18px}
.av-pick{display:flex;flex-wrap:wrap;gap:7px;margin-bottom:14px;justify-content:center}
.av-op{width:52px;height:52px;border-radius:50%;cursor:pointer;border:2px solid transparent;transition:border-color .2s,transform .2s;display:flex;align-items:center;justify-content:center;font-size:22px}
.av-op.sel{border-color:var(--accent);transform:scale(1.08)}
.av-ul{width:52px;height:52px;border-radius:50%;cursor:pointer;border:2px dashed var(--border2);background:var(--surface2);display:flex;align-items:center;justify-content:center;font-size:22px;color:var(--muted);transition:border-color .2s}
.av-ul:hover{border-color:var(--accent)}
.mo-lbl{font-size:11px;font-weight:700;color:var(--muted2);margin-bottom:5px}
.st-row{display:flex;gap:7px;margin-bottom:12px;flex-wrap:wrap}
.st-chip{background:var(--surface2);border:1px solid var(--border2);color:var(--muted2);padding:5px 12px;border-radius:50px;font-size:12px;font-weight:700;cursor:pointer;transition:all .2s}
.st-chip.active{background:rgba(88,101,242,.2);border-color:var(--accent);color:var(--accent2)}

/* LIGHTBOX */
.lb{position:fixed;inset:0;background:rgba(0,0,0,.93);z-index:2000;display:flex;align-items:center;justify-content:center}
.lb.h{display:none}
.lb img,.lb video{max-width:95vw;max-height:88vh;border-radius:10px;object-fit:contain}
.lb-close{position:absolute;top:14px;left:14px;background:var(--surface2);border:1px solid var(--border2);color:var(--text);padding:6px 14px;border-radius:8px;cursor:pointer;font-family:'Cairo',sans-serif;font-weight:700;font-size:12px}

/* LEVEL UP */
.lvlup{position:fixed;top:50%;left:50%;transform:translate(-50%,-50%) scale(.8);background:linear-gradient(135deg,var(--surface2),var(--surface3));border:2px solid var(--gold);border-radius:20px;padding:28px 34px;text-align:center;z-index:3000;opacity:0;pointer-events:none;transition:all .4s}
.lvlup.show{opacity:1;transform:translate(-50%,-50%) scale(1);pointer-events:auto}
.lvlup h2{font-family:'Tajawal',sans-serif;font-weight:900;font-size:24px;color:var(--gold)}

/* TOAST */
.toast{position:fixed;bottom:18px;left:50%;transform:translateX(-50%);background:var(--surface3);border:1px solid var(--border2);color:var(--text);padding:8px 18px;border-radius:50px;font-size:12px;font-weight:700;z-index:9999;opacity:0;transition:opacity .3s;pointer-events:none;white-space:nowrap}
.toast.show{opacity:1}

@media(max-width:680px){.strip{display:none}}
@media(max-width:500px){.sidebar{display:none}}
</style>
</head>
<body>

<!-- PROFILE MODAL -->
<div class="mo" id="mo">
  <div class="mo-box">
    <h2 id="mo-title">مرحبا، انشئ بروفايلك</h2>
    <div class="mo-lbl">اختر أفاتار</div>
    <div class="av-pick" id="av-pick"></div>
    <div class="mo-lbl">الاسم</div>
    <input class="inp" id="pName" placeholder="اسمك في المجتمع" maxlength="20">
    <div class="mo-lbl">Bio</div>
    <input class="inp" id="pBio" placeholder="عبارة قصيرة عنك..." maxlength="80">
    <div class="mo-lbl">الحالة</div>
    <div class="st-row">
      <div class="st-chip active" onclick="setSt(this,'اونلاين')">اونلاين</div>
      <div class="st-chip" onclick="setSt(this,'مشغول')">مشغول</div>
      <div class="st-chip" onclick="setSt(this,'غايب')">غايب</div>
    </div>
    <button class="btn-p" onclick="saveProf()">حفظ البروفايل</button>
  </div>
</div>

<!-- LIGHTBOX -->
<div class="lb h" id="lb" onclick="closeLb()">
  <button class="lb-close">اغلاق</button>
  <img id="lb-img" src="" style="display:none">
  <video id="lb-vid" controls style="display:none"></video>
</div>

<!-- LEVEL UP -->
<div class="lvlup" id="lvlup">
  <div style="font-size:38px">🏆</div>
  <h2>ترقيت!</h2>
  <p id="lvlup-txt" style="color:var(--muted2);margin-top:6px"></p>
  <button class="btn-p" style="margin-top:14px;width:auto;padding:8px 24px" onclick="document.getElementById('lvlup').classList.remove('show')">رائع!</button>
</div>

<div class="app">

<!-- SERVER STRIP -->
<div class="strip">
  <div class="s-icon active">Z</div>
  <div class="s-div"></div>
  <div class="s-icon" style="background:var(--surface2);font-size:20px;color:var(--muted)">+</div>
</div>

<!-- SIDEBAR -->
<div class="sidebar">
  <div class="sb-hdr">
    <div class="sb-title">Znoog Community</div>
    <div class="sb-sub" id="online-count">جاري التحميل...</div>
  </div>

  <div class="sb-sec">القنوات</div>
  <div class="ch-btn active" id="cbtn-general" onclick="goTo('general',this)">
    <span class="ch-icon">#</span>عام
    <span class="ch-notif hidden" id="notif-general"></span>
  </div>
  <div class="ch-btn" id="cbtn-admch" onclick="goTo('admch',this)">
    <span class="ch-icon">🔒</span>الادمن
  </div>
  <div class="ch-btn" id="cbtn-events" onclick="goTo('events',this)">
    <span class="ch-icon">🗓</span>فعاليات
  </div>
  <div class="ch-btn" id="cbtn-media" onclick="goTo('media',this)">
    <span class="ch-icon">🖼</span>صور و مقاطع
  </div>

  <div class="sb-sec">المجتمع</div>
  <div class="ch-btn" id="cbtn-members" onclick="goTo('members',this)">
    <span class="ch-icon">🏆</span>الأعضاء
  </div>
  <div class="ch-btn" id="cbtn-admin" onclick="goTo('admin',this)">
    <span class="ch-icon">⚙️</span>لوحة التحكم
  </div>

  <div class="sb-prof" onclick="openEdit()">
    <div id="sp-av"></div>
    <div class="sp-info">
      <div class="sp-name" id="sp-nm">...</div>
      <div class="sp-lvl" id="sp-lv">Lvl 1 · 0 XP</div>
    </div>
    <span style="font-size:13px;color:var(--muted)">✏️</span>
  </div>
</div>

<!-- MAIN -->
<div class="main">

  <!-- GENERAL -->
  <div class="page active" id="page-general">
    <div class="ch-hdr">
      <span class="ch-hdr-icon">#</span>
      <span class="ch-hdr-name">عام</span>
      <span class="ch-hdr-desc">الشات العام للجميع</span>
    </div>
    <div id="pin-general" style="display:none" class="pin-bar">📌 <b>مثبت:</b> <span id="pin-general-txt"></span></div>
    <div class="feed" id="feed-general"></div>
    <div class="ci-wrap">
      <div class="spam-w" id="spamW">انتظر قبل الارسال</div>
      <div class="ci-box">
        <button class="ci-icon" onclick="document.getElementById('fi-general').click()">📎</button>
        <input type="file" id="fi-general" accept="image/*,video/*" style="display:none" onchange="attachFile(this,'general')">
        <input class="ci-inp" id="ci-general" placeholder="اكتب رسالة في #عام..." maxlength="400">
        <button class="send-b" onclick="sendMsg('general')">ارسال</button>
      </div>
    </div>
  </div>

  <!-- ADMIN CH -->
  <div class="page" id="page-admch">
    <div class="ch-hdr">
      <span class="ch-hdr-icon">🔒</span>
      <span class="ch-hdr-name">الادمن</span>
      <span class="ch-hdr-desc">قناة خاصة بالإدارة</span>
    </div>
    <div id="admch-lock" class="lock-wrap">
      <div style="font-size:44px">🔒</div>
      <h3>قناة خاصة</h3>
      <input class="inp" id="admch-pass" type="password" placeholder="كلمة سر القناة" style="max-width:260px">
      <button class="btn-p" style="max-width:260px" onclick="unlockAdmCh()">دخول</button>
    </div>
    <div id="admch-body" style="display:none;flex:1;flex-direction:column;overflow:hidden">
      <div class="feed" id="feed-admch"></div>
      <div class="ci-wrap">
        <div class="ci-box">
          <input class="ci-inp" id="ci-admch" placeholder="رسالة للادمن..." maxlength="400">
          <button class="send-b" onclick="sendMsg('admch')">ارسال</button>
        </div>
      </div>
    </div>
  </div>

  <!-- EVENTS -->
  <div class="page" id="page-events">
    <div class="ch-hdr">
      <span class="ch-hdr-icon">🗓</span>
      <span class="ch-hdr-name">فعاليات</span>
      <span class="ch-hdr-desc">الفعاليات القادمة</span>
    </div>
    <div class="ev-pg" id="ev-list"></div>
  </div>

  <!-- MEDIA -->
  <div class="page" id="page-media">
    <div class="ch-hdr">
      <span class="ch-hdr-icon">🖼</span>
      <span class="ch-hdr-name">صور و مقاطع</span>
      <span class="ch-hdr-desc">تُحذف تلقائيا بعد 24 ساعة · الأدمن يقدر يحفظ</span>
    </div>
    <label class="upload-area" for="media-up">
      <h4>ارفع صورة أو مقطع</h4>
      <p>اضغط هنا · أقصى حجم 5MB</p>
      <input type="file" id="media-up" accept="image/*,video/*" style="display:none" onchange="uploadMedia(this)">
    </label>
    <div class="media-grid" id="media-grid"></div>
  </div>

  <!-- MEMBERS -->
  <div class="page" id="page-members">
    <div class="ch-hdr">
      <span class="ch-hdr-icon">🏆</span>
      <span class="ch-hdr-name">الأعضاء</span>
    </div>
    <div class="m-pg">
      <div class="m-tabs">
        <button class="m-tab active" onclick="mTab(this,'mt-all')">الكل</button>
        <button class="m-tab" onclick="mTab(this,'mt-vip')">المتميزون</button>
        <button class="m-tab" onclick="mTab(this,'mt-adm')">الادمن</button>
      </div>
      <div id="mt-all"><div class="sec-hdr">ترتيب الأعضاء</div><div id="rank-list"></div></div>
      <div id="mt-vip" style="display:none"><div class="sec-hdr">الأعضاء المتميزون</div><div id="vip-list"></div></div>
      <div id="mt-adm" style="display:none"><div class="sec-hdr">فريق الإدارة</div><div id="adm-list"></div></div>
    </div>
  </div>

  <!-- ADMIN PANEL -->
  <div class="page" id="page-admin">
    <div class="ch-hdr">
      <span class="ch-hdr-icon">⚙️</span>
      <span class="ch-hdr-name">لوحة التحكم</span>
    </div>
    <div id="adm-login" class="lock-wrap">
      <div style="font-size:44px">⚙️</div>
      <h3>لوحة الأدمن</h3>
      <input class="inp" id="adm-pass" type="password" placeholder="كلمة السر" style="max-width:260px">
      <button class="btn-p" style="max-width:260px" onclick="loginAdm()">دخول</button>
    </div>
    <div id="adm-panel" style="display:none" class="adm-pg">

      <div class="a-card">
        <h4>تحديث XP عضو</h4>
        <input class="inp" id="a-target" placeholder="اسم العضو">
        <input class="inp" id="a-xp" type="number" placeholder="XP الجديد">
        <button class="btn-p" onclick="setXP()">تحديث</button>
      </div>

      <div class="a-card">
        <h4>اضافة VIP</h4>
        <input class="inp" id="a-vipnm" placeholder="اسم العضو">
        <input class="inp" id="a-vipdesc" placeholder="وصف قصير">
        <button class="btn-p" onclick="addVIP()">اضافة VIP</button>
      </div>

      <div class="a-card">
        <h4>اضافة ادمن للقائمة</h4>
        <input class="inp" id="a-admnm" placeholder="اسم الادمن">
        <input class="inp" id="a-admrole" placeholder="الرتبة (مثال: مشرف)">
        <button class="btn-p" onclick="addAdmToList()">اضافة</button>
      </div>

      <div class="a-card">
        <h4>اضافة فعالية</h4>
        <input class="inp" id="a-evtitle" placeholder="عنوان الفعالية">
        <input class="inp" id="a-evdesc" placeholder="وصف">
        <input class="inp" id="a-evdate" type="date">
        <input class="inp" id="a-evtime" type="time">
        <button class="btn-p" onclick="addEvent()">نشر الفعالية</button>
      </div>

      <div class="a-card">
        <h4>تثبيت رسالة في العام</h4>
        <input class="inp" id="a-pin" placeholder="نص الرسالة">
        <button class="btn-p" onclick="pinMsg()">تثبيت</button>
      </div>

      <div class="a-card">
        <h4>إجراءات</h4>
        <button class="btn-d" onclick="clearCh('general')">مسح شات العام</button>
        <button class="btn-d" onclick="clearCh('admch')">مسح شات الادمن</button>
      </div>

    </div>
  </div>

</div><!-- /main -->
</div><!-- /app -->

<div class="toast" id="toast"></div>

<script>
/* ===== FIREBASE ===== */
const fbCfg={
  apiKey:"AIzaSy...",
  authDomain:"velora-rp.firebaseapp.com",
  databaseURL:"https://velora-rp-default-rtdb.europe-west1.firebasedatabase.app",
  projectId:"velora-rp",
  storageBucket:"velora-rp.firebasestorage.app",
  messagingSenderId:"681356163114",
  appId:"1:681356163114:web:c40b8d7fed229ce8e7eb53"
};
firebase.initializeApp(fbCfg);
const db=firebase.database();

/* ===== CONFIG ===== */
const ADMIN_PASS="008877";
const ADMCH_PASS="znoog_admin";
const SPAM_DELAY=5000;
const SPAM_LIMIT=3;
const SPAM_WIN=10000;
const MEDIA_TTL=86400000;
const MAX_FILE=5*1024*1024;
const EMOJIS=['❤️','😂','🔥','👏','😮','💯'];
const PRESET_AVS=[
  {e:'🐉',c:'#5865f2'},{e:'🦊',c:'#f0b429'},{e:'🐺',c:'#00d4aa'},
  {e:'🦅',c:'#a855f7'},{e:'🐯',c:'#f04747'},{e:'🌙',c:'#06b6d4'},
  {e:'⚡',c:'#10b981'},{e:'🔮',c:'#ec4899'},
];

/* ===== STATE ===== */
let prof={name:'',bio:'',avatar:'',status:'اونلاين',xp:0,level:1,joinDate:0};
let isAdmin=false,admChOpen=false;
let spamWin=[],lastMsg=0;
let selSt='اونلاين',selAv='';
let pendB64='',pendType='';
let curCh='general';
let unread=0;

/* ===== HELPERS ===== */
const AVC=['#5865f2','#00d4aa','#f0b429','#f04747','#a855f7','#06b6d4','#10b981','#ec4899'];
function avc(n){let h=0;for(let c of(n||''))h=c.charCodeAt(0)+h;return AVC[h%AVC.length];}
function mkAv(n,b64,sz=38){
  if(b64&&b64.startsWith('data:'))return`<img style="width:${sz}px;height:${sz}px;border-radius:50%;object-fit:cover;flex-shrink:0" src="${b64}">`;
  const c=avc(n);
  return`<div style="width:${sz}px;height:${sz}px;border-radius:50%;background:${c};display:flex;align-items:center;justify-content:center;font-weight:800;font-size:${Math.round(sz*.38)}px;color:#fff;flex-shrink:0">${(n||'?')[0].toUpperCase()}</div>`;
}
function lvlLabel(l){if(l<=2)return'Rookie';if(l<=5)return'Member';if(l<=10)return'Pro';if(l<=20)return'Elite';return'Legend';}
function esc(s){return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');}
function toast(m){const t=document.getElementById('toast');t.textContent=m;t.classList.add('show');clearTimeout(t._t);t._t=setTimeout(()=>t.classList.remove('show'),2500);}
function fmtTime(ts){return new Date(ts).toLocaleTimeString('ar-SA',{hour:'2-digit',minute:'2-digit'});}

/* ===== PROFILE ===== */
function initAvPick(){
  const w=document.getElementById('av-pick');
  let h=PRESET_AVS.map((a,i)=>`<div class="av-op" id="avop${i}" style="background:${a.c}" onclick="pickAv(${i},'${a.e}','${a.c}')">${a.e}</div>`).join('');
  h+=`<label class="av-ul">+<input type="file" accept="image/*" style="display:none" onchange="avUpload(this)"></label>`;
  w.innerHTML=h;
}
function pickAv(i,e,c){
  document.querySelectorAll('.av-op').forEach(el=>el.classList.remove('sel'));
  const op=document.getElementById('avop'+i);if(op)op.classList.add('sel');
  const cv=document.createElement('canvas');cv.width=80;cv.height=80;
  const ctx=cv.getContext('2d');ctx.fillStyle=c;ctx.fillRect(0,0,80,80);
  ctx.font='44px serif';ctx.textAlign='center';ctx.textBaseline='middle';ctx.fillText(e,40,42);
  selAv=cv.toDataURL();
}
function avUpload(inp){
  const f=inp.files[0];if(!f)return;
  if(f.size>1*1024*1024){toast('الصورة أكبر من 1MB');return;}
  const r=new FileReader();r.onload=e=>{selAv=e.target.result;toast('تم تحميل الصورة');};r.readAsDataURL(f);
}
function setSt(el,v){document.querySelectorAll('.st-chip').forEach(e=>e.classList.remove('active'));el.classList.add('active');selSt=v;}
function saveProf(){
  const n=document.getElementById('pName').value.trim();
  if(!n){toast('ادخل اسمك');return;}
  prof.name=n;prof.bio=document.getElementById('pBio').value.trim();
  prof.avatar=selAv||'';prof.status=selSt;
  if(!prof.joinDate)prof.joinDate=Date.now();
  localStorage.setItem('znoog_p',JSON.stringify(prof));
  document.getElementById('mo').classList.add('h');
  updSbProf();toast('تم حفظ البروفايل');
}
function openEdit(){
  document.getElementById('mo-title').textContent='تعديل البروفايل';
  document.getElementById('pName').value=prof.name;
  document.getElementById('pBio').value=prof.bio||'';
  document.getElementById('mo').classList.remove('h');
}
function loadProf(){
  const s=localStorage.getItem('znoog_p');
  if(s){prof={...prof,...JSON.parse(s)};document.getElementById('mo').classList.add('h');updSbProf();}
  else{initAvPick();document.getElementById('mo').classList.remove('h');}
}
function updSbProf(){
  document.getElementById('sp-nm').textContent=prof.name||'...';
  document.getElementById('sp-lv').textContent=`Lvl ${prof.level||1} · ${prof.xp||0} XP`;
  document.getElementById('sp-av').innerHTML=mkAv(prof.name,prof.avatar,34);
}

/* ===== NAV ===== */
function goTo(id,btn){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.ch-btn').forEach(b=>b.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
  if(btn)btn.classList.add('active');
  curCh=id;
  if(id==='general'){unread=0;updNotif();}
  if(id==='media')cleanMedia();
}
function updNotif(){
  const el=document.getElementById('notif-general');
  if(!el)return;
  if(unread>0){el.classList.remove('hidden');el.textContent=unread;}
  else el.classList.add('hidden');
}

/* ===== XP ===== */
function addXP(n){
  const old=prof.level;
  prof.xp=(prof.xp||0)+n;
  prof.level=Math.floor(prof.xp/100)+1;
  localStorage.setItem('znoog_p',JSON.stringify(prof));
  updSbProf();
  db.ref('members/'+prof.name).transaction(d=>{
    if(!d)return{name:prof.name,avatar:prof.avatar,xp:prof.xp,level:prof.level};
    return{...d,name:prof.name,avatar:prof.avatar,xp:prof.xp,level:prof.level};
  });
  if(prof.level>old){
    document.getElementById('lvlup-txt').textContent=`وصلت للمستوى ${prof.level} · ${lvlLabel(prof.level)}`;
    document.getElementById('lvlup').classList.add('show');
  }
}

/* ===== SPAM ===== */
function chkSpam(){
  const n=Date.now();
  spamWin=spamWin.filter(t=>n-t<SPAM_WIN);
  if(n-lastMsg<SPAM_DELAY)return false;
  if(spamWin.length>=SPAM_LIMIT)return false;
  return true;
}

/* ===== SEND MSG ===== */
function sendMsg(ch){
  if(!prof.name){toast('انشئ بروفايلك أولا');openEdit();return;}
  const inp=document.getElementById('ci-'+ch);
  const txt=inp.value.trim();
  const hasMed=!!pendB64;
  if(!txt&&!hasMed)return;
  const sw=document.getElementById('spamW');
  if(!chkSpam()){if(sw){sw.style.display='block';setTimeout(()=>sw.style.display='none',3000);}return;}
  lastMsg=Date.now();spamWin.push(Date.now());
  const d={name:prof.name,avatar:prof.avatar||'',text:txt||'',time:Date.now(),isAdmin};
  if(hasMed){d.mediaB64=pendB64;d.mediaType=pendType;}
  db.ref('msgs/'+ch).push(d);
  inp.value='';pendB64='';pendType='';
  addXP(10);
}

/* ===== ATTACH FILE ===== */
function attachFile(inp,ch){
  const f=inp.files[0];if(!f)return;
  if(f.size>MAX_FILE){toast('الملف أكبر من 5MB');return;}
  const r=new FileReader();
  r.onload=e=>{pendB64=e.target.result;pendType=f.type.startsWith('video')?'video':'image';toast('تم الاختيار، اضغط ارسال');};
  r.readAsDataURL(f);inp.value='';
}

/* ===== REACTIONS ===== */
function toggleRx(k,ch,em){
  if(!prof.name){toast('انشئ بروفايلك أولا');return;}
  const uk=prof.name.replace(/[.#$/\[\]]/g,'_');
  const ref=db.ref(`rx/${ch}/${k}/${em}/${uk}`);
  ref.once('value',s=>{if(s.exists())ref.remove();else ref.set(true);});
}
function mkRxHtml(k,ch,rxd){
  let h='';
  const uk=prof.name.replace(/[.#$/\[\]]/g,'_');
  for(const em of EMOJIS){
    const users=rxd&&rxd[em]?rxd[em]:{};
    const cnt=Object.keys(users).length;
    if(cnt>0){
      const mine=!!users[uk];
      h+=`<div class="rx-chip${mine?' mine':''}" onclick="toggleRx('${k}','${ch}','${em}')">${em}<span>${cnt}</span></div>`;
    }
  }
  h+=`<div class="rx-add" onclick="showRxPicker('${k}','${ch}')">+</div>`;
  return h;
}
function showRxPicker(k,ch){
  const old=document.getElementById('rxp-'+k);if(old){old.remove();return;}
  const row=document.getElementById('rxr-'+k);if(!row)return;
  const p=document.createElement('div');p.className='rx-picker';p.id='rxp-'+k;
  p.innerHTML=EMOJIS.map(e=>`<span onclick="toggleRx('${k}','${ch}','${e}');document.getElementById('rxp-${k}').remove()">${e}</span>`).join('');
  row.appendChild(p);
  setTimeout(()=>{const el=document.getElementById('rxp-'+k);if(el)el.remove();},4000);
}

/* ===== RENDER MSG ===== */
function renderMsg(k,d,ch,rxd){
  const badge=d.isAdmin?`<span class="mbadge b-adm">أدمن</span>`:'';
  const nc=d.isAdmin?'adm':'';
  const med=d.mediaB64?(d.mediaType==='video'
    ?`<video class="msg-img" src="${d.mediaB64}" controls onclick="event.stopPropagation()"></video>`
    :`<img class="msg-img" src="${d.mediaB64}" onclick="openLb('${k}','${d.mediaB64}','image')">`)
    :'';
  const del=isAdmin?`<button class="act-b del" onclick="delMsg('${k}','${ch}')">🗑</button>`:'';
  return`<div class="msg-g" id="mg-${k}">
    <div class="msg-av">${mkAv(d.name,d.avatar,38)}</div>
    <div class="msg-body">
      <div class="msg-meta"><span class="msg-nm ${nc}">${esc(d.name)}</span>${badge}<span class="msg-time">${fmtTime(d.time)}</span></div>
      ${d.text?`<div class="msg-txt">${esc(d.text)}</div>`:''}${med}
      <div class="rx-row" id="rxr-${k}">${mkRxHtml(k,ch,rxd)}</div>
    </div>
    <div class="msg-acts">${del}</div>
  </div>`;
}

/* ===== LISTEN CHANNEL ===== */
function listenCh(ch){
  db.ref('msgs/'+ch).orderByChild('time').limitToLast(60).on('value',snap=>{
    const feed=document.getElementById('feed-'+ch);if(!feed)return;
    const msgs=[];snap.forEach(s=>msgs.push({k:s.key,...s.val()}));
    db.ref('rx/'+ch).once('value',rs=>{
      const rxd=rs.val()||{};
      feed.innerHTML=msgs.map(d=>renderMsg(d.k,d,ch,rxd[d.k]||{})).join('');
      feed.scrollTop=feed.scrollHeight;
    });
    if(ch==='general'&&curCh!=='general'){unread=msgs.length;updNotif();}
  });
  db.ref('rx/'+ch).on('value',rs=>{
    const rxd=rs.val()||{};
    Object.keys(rxd).forEach(k=>{
      const row=document.getElementById('rxr-'+k);
      if(row)row.innerHTML=mkRxHtml(k,ch,rxd[k]);
    });
  });
}
function delMsg(k,ch){
  if(!isAdmin)return;
  if(!confirm('حذف؟'))return;
  db.ref('msgs/'+ch+'/'+k).remove();
  db.ref('rx/'+ch+'/'+k).remove();
  toast('تم الحذف');
}
function clearCh(ch){
  if(!isAdmin)return;
  if(!confirm('مسح كل رسايل '+ch+'؟'))return;
  db.ref('msgs/'+ch).remove();db.ref('rx/'+ch).remove();toast('تم المسح');
}

/* ===== ADMIN CH ===== */
function unlockAdmCh(){
  const p=document.getElementById('admch-pass').value;
  if(p===ADMCH_PASS||p===ADMIN_PASS){
    admChOpen=true;
    document.getElementById('admch-lock').style.display='none';
    document.getElementById('admch-body').style.display='flex';
    listenCh('admch');
  }else toast('كلمة سر خاطئة');
}

/* ===== ADMIN ===== */
function loginAdm(){
  if(document.getElementById('adm-pass').value===ADMIN_PASS){
    isAdmin=true;
    document.getElementById('adm-login').style.display='none';
    document.getElementById('adm-panel').style.display='block';
    toast('مرحبا يا أدمن');
  }else toast('كلمة سر خاطئة');
}
function setXP(){
  if(!isAdmin)return;
  const n=document.getElementById('a-target').value.trim();
  const x=parseInt(document.getElementById('a-xp').value);
  if(!n||isNaN(x))return toast('ادخل اسم وXP');
  db.ref('members/'+n).update({xp:x,level:Math.floor(x/100)+1});toast('تم تحديث XP');
}
function addVIP(){
  if(!isAdmin)return;
  const n=document.getElementById('a-vipnm').value.trim();
  const d=document.getElementById('a-vipdesc').value.trim();
  if(!n)return toast('ادخل اسم');
  db.ref('vip').push({name:n,desc:d});toast('تم اضافة VIP');
  document.getElementById('a-vipnm').value='';document.getElementById('a-vipdesc').value='';
}
function addAdmToList(){
  if(!isAdmin)return;
  const n=document.getElementById('a-admnm').value.trim();
  const r=document.getElementById('a-admrole').value.trim();
  if(!n)return toast('ادخل اسم');
  db.ref('admins_list').push({name:n,role:r||'أدمن'});toast('تم الاضافة');
  document.getElementById('a-admnm').value='';document.getElementById('a-admrole').value='';
}
function addEvent(){
  if(!isAdmin)return;
  const t=document.getElementById('a-evtitle').value.trim();
  const d=document.getElementById('a-evdesc').value.trim();
  const dt=document.getElementById('a-evdate').value;
  const tm=document.getElementById('a-evtime').value;
  if(!t||!dt)return toast('ادخل عنوان وتاريخ');
  db.ref('events').push({title:t,desc:d,date:dt,time:tm,attendees:0});toast('تم نشر الفعالية');
  ['a-evtitle','a-evdesc','a-evdate','a-evtime'].forEach(id=>document.getElementById(id).value='');
}
function pinMsg(){
  if(!isAdmin)return;
  const t=document.getElementById('a-pin').value.trim();if(!t)return;
  db.ref('pinned/general').set({text:t});toast('تم التثبيت');
  document.getElementById('a-pin').value='';
}

/* ===== PINNED ===== */
db.ref('pinned/general').on('value',s=>{
  const el=document.getElementById('pin-general');
  const tx=document.getElementById('pin-general-txt');
  if(s.val()&&s.val().text){tx.textContent=s.val().text;el.style.display='flex';}
  else el.style.display='none';
});

/* ===== MEMBERS ===== */
function mTab(btn,id){
  document.querySelectorAll('.m-tab').forEach(b=>b.classList.remove('active'));btn.classList.add('active');
  ['mt-all','mt-vip','mt-adm'].forEach(t=>document.getElementById(t).style.display=t===id?'block':'none');
}
db.ref('members').orderByChild('xp').on('value',snap=>{
  let ms=[];snap.forEach(s=>ms.push(s.val()));ms.sort((a,b)=>(b.xp||0)-(a.xp||0));
  const maxXP=ms[0]?.xp||1;
  const el=document.getElementById('rank-list');if(!el)return;
  el.innerHTML=ms.map((d,i)=>{
    const lv=Math.floor((d.xp||0)/100)+1;const pct=Math.min(100,Math.round(((d.xp||0)/maxXP)*100));
    const rc=i===0?'r1':i===1?'r2':i===2?'r3':'';
    return`<div class="m-row"><div class="rk ${rc}">${i+1}</div>${mkAv(d.name,d.avatar,44)}
    <div class="m-info"><div class="m-nm">${esc(d.name)}</div><div class="m-sb">${lvlLabel(lv)} · Lvl ${lv}</div>
    <div class="xb-w"><div class="xb" style="width:${pct}%"></div></div></div>
    <div class="m-xp">${d.xp||0} XP</div></div>`;
  }).join('');
  document.getElementById('online-count').textContent=ms.length+' عضو مسجل';
});
db.ref('vip').on('value',snap=>{
  const el=document.getElementById('vip-list');if(!el)return;let h='';
  snap.forEach(s=>{const d=s.val();
    h+=`<div class="feat-row"><span style="font-size:20px">👑</span>${mkAv(d.name,d.avatar||'',52)}
    <div class="f-info"><div class="f-nm">${esc(d.name)}</div><div class="f-desc">${esc(d.desc||'عضو متميز')}</div>
    <div class="f-badges"><span class="mbadge b-vip">VIP</span></div></div></div>`;
  });
  el.innerHTML=h||'<div style="color:var(--muted);text-align:center;padding:30px">لا يوجد VIP بعد</div>';
});
db.ref('admins_list').on('value',snap=>{
  const el=document.getElementById('adm-list');if(!el)return;let h='';
  snap.forEach(s=>{const d=s.val();
    h+=`<div class="feat-row"><span style="font-size:20px">🛡️</span>${mkAv(d.name,d.avatar||'',52)}
    <div class="f-info"><div class="f-nm">${esc(d.name)}</div><div class="f-desc">${esc(d.role||'أدمن')}</div>
    <div class="f-badges"><span class="mbadge b-adm">أدمن</span></div></div></div>`;
  });
  el.innerHTML=h||'<div style="color:var(--muted);text-align:center;padding:30px">لا يوجد أدمن في القائمة</div>';
});

/* ===== EVENTS ===== */
db.ref('events').orderByChild('date').on('value',snap=>{
  const el=document.getElementById('ev-list');if(!el)return;
  let evs=[];snap.forEach(s=>evs.push({k:s.key,...s.val()}));
  evs.sort((a,b)=>new Date(a.date)-new Date(b.date));
  if(!evs.length){el.innerHTML='<div style="color:var(--muted);text-align:center;padding:40px">لا توجد فعاليات</div>';return;}
  el.innerHTML=evs.map(ev=>{
    const d=new Date(ev.date);
    const day=d.getDate();const mon=d.toLocaleDateString('ar-SA',{month:'short'});
    return`<div class="ev-card">
      <div class="ev-top">
        <div class="ev-date"><div class="ev-day">${day}</div><div class="ev-mon">${mon}</div></div>
        <div><div class="ev-title">${esc(ev.title)}</div><div class="ev-desc">${esc(ev.desc||'')}</div></div>
      </div>
      <div class="ev-foot">
        ${ev.time?`<span class="ev-time">⏰ ${ev.time}</span>`:''}
        <span style="font-size:12px;color:var(--muted2)">👥 ${ev.attendees||0} مسجل</span>
        <button class="att-btn${localStorage.getItem('att_'+ev.k)?' yes':''}" id="att-${ev.k}" onclick="toggleAtt('${ev.k}')">${localStorage.getItem('att_'+ev.k)?'حاضر':'سجل حضورك'}</button>
        ${isAdmin?`<button onclick="db.ref('events/${ev.k}').remove()" style="background:rgba(240,71,71,.1);border:1px solid var(--danger);color:var(--danger);border-radius:7px;padding:4px 10px;font-size:11px;cursor:pointer;font-family:'Cairo',sans-serif;font-weight:700">حذف</button>`:''}
      </div>
    </div>`;
  }).join('');
});
function toggleAtt(k){
  const key='att_'+k;const btn=document.getElementById('att-'+k);
  if(localStorage.getItem(key)){
    localStorage.removeItem(key);
    db.ref('events/'+k+'/attendees').transaction(v=>(v||1)-1);
    if(btn){btn.classList.remove('yes');btn.textContent='سجل حضورك';}
  }else{
    localStorage.setItem(key,'1');
    db.ref('events/'+k+'/attendees').transaction(v=>(v||0)+1);
    if(btn){btn.classList.add('yes');btn.textContent='حاضر';}
    toast('تم تسجيل حضورك');
  }
}

/* ===== MEDIA ===== */
function uploadMedia(inp){
  const f=inp.files[0];if(!f)return;
  if(f.size>MAX_FILE){toast('الملف أكبر من 5MB');return;}
  if(!prof.name){toast('انشئ بروفايلك أولا');return;}
  const r=new FileReader();
  r.onload=e=>{
    db.ref('media').push({name:prof.name,b64:e.target.result,type:f.type.startsWith('video')?'video':'image',uploadedAt:Date.now(),expiresAt:Date.now()+MEDIA_TTL,saved:false});
    toast('تم الرفع');
  };
  r.readAsDataURL(f);inp.value='';
}
function cleanMedia(){
  db.ref('media').once('value',snap=>{
    const now=Date.now();
    snap.forEach(s=>{const d=s.val();if(!d.saved&&d.expiresAt&&now>d.expiresAt)db.ref('media/'+s.key).remove();});
  });
}
db.ref('media').orderByChild('uploadedAt').on('value',snap=>{
  const grid=document.getElementById('media-grid');if(!grid)return;
  const now=Date.now();let h='';
  snap.forEach(s=>{
    const d=s.val();
    if(!d.saved&&d.expiresAt&&now>d.expiresAt)return;
    const hl=d.expiresAt?Math.max(0,Math.round((d.expiresAt-now)/3600000)):null;
    const med=d.type==='video'
      ?`<video src="${d.b64}" muted style="width:100%;height:100%;object-fit:cover"></video>`
      :`<img src="${d.b64}" style="width:100%;height:100%;object-fit:cover">`;
    const sv=d.saved?'<div class="mc-saved">محفوظ</div>':'';
    const ex=(!d.saved&&hl!==null)?`<div class="mc-exp">${hl}س</div>`:'';
    const sb=isAdmin&&!d.saved?`<button class="save-btn" onclick="event.stopPropagation();saveMedia('${s.key}')">💾 حفظ دائم</button>`:'';
    h+=`<div class="mc" onclick="openLb('${s.key}','${d.b64}','${d.type||'image'}')">
      ${med}${sv}${ex}
      <div class="mc-ov"><div><div class="mc-name">${esc(d.name)}</div>${sb}</div></div>
    </div>`;
  });
  grid.innerHTML=h||'<div style="color:var(--muted);text-align:center;grid-column:1/-1;padding:40px">لا يوجد محتوى بعد</div>';
});
function saveMedia(k){if(!isAdmin)return;db.ref('media/'+k).update({saved:true,expiresAt:null});toast('تم الحفظ الدائم');}

/* ===== LIGHTBOX ===== */
function openLb(_k,b64,type){
  const lb=document.getElementById('lb');
  const img=document.getElementById('lb-img');
  const vid=document.getElementById('lb-vid');
  lb.classList.remove('h');
  if(type==='video'){img.style.display='none';vid.style.display='block';vid.src=b64;}
  else{vid.style.display='none';img.style.display='block';img.src=b64;}
}
function closeLb(){
  document.getElementById('lb').classList.add('h');
  const v=document.getElementById('lb-vid');if(v.pause)v.pause();
}

/* ===== ENTER TO SEND ===== */
['general','admch'].forEach(ch=>{
  const el=document.getElementById('ci-'+ch);
  if(el)el.addEventListener('keydown',e=>{if(e.key==='Enter')sendMsg(ch);});
});

/* ===== INIT ===== */
loadProf();
listenCh('general');
cleanMedia();
</script>
</body>
</html>
