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
.api-bar label{font-size:11px;color:var(--muted);font-weight:700;text-transform:uppercase;letter-spacing:0.5px;margin-bottom:8px;display:block}
.api-bar input{
  width:100%;background:var(--bg);
  border:1.5px solid var(--border);
  border-radius:8px;padding:9px 12px;
  font-family:'Cairo',sans-serif;font-size:13px;
  color:var(--text);direction:ltr;outline:none;
}
.api-bar input:focus{border-color:var(--accent)}
.api-status{font-size:11px;margin-top:6px;text-align:center}
.api-status.ok{color:var(--green)}
.api-status.bad{color:var(--red)}

/* MAIN */
.main{margin-right:260px;flex:1;padding:40px 36px;max-width:860px}

.page{display:none}
.page.active{display:block}

.page-header{margin-bottom:28px}
.page-header h1{font-size:26px;font-weight:900;margin-bottom:6px}
.page-header p{color:var(--muted);font-size:14px;line-height:1.7}

/* FORM */
.form-card{
  background:var(--surface);
  border:1px solid var(--border);
  border-radius:18px;
  padding:28px;
  margin-bottom:20px;
}
.field{margin-bottom:18px}
.field label{display:block;font-size:12px;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:0.5px;margin-bottom:8px}
.field input,.field textarea,.field select{
  width:100%;
  background:var(--bg);
  border:1.5px solid var(--border);
  border-radius:10px;
  padding:12px 16px;
  font-family:'Cairo',sans-serif;font-size:14px;
  color:var(--text);outline:none;
  transition:border-color 0.2s;
}
.field textarea{resize:vertical;min-height:100px;line-height:1.7}
.field input:focus,.field textarea:focus,.field select:focus{border-color:var(--accent);box-shadow:0 0 0 3px var(--accent-glow)}
.field input::placeholder,.field textarea::placeholder{color:var(--muted)}

.row{display:flex;gap:14px}
.row .field{flex:1}

.btn{
  background:var(--accent);color:white;border:none;
  border-radius:10px;padding:13px 28px;
  font-family:'Cairo',sans-serif;font-size:15px;font-weight:700;
  cursor:pointer;transition:all 0.2s;
  box-shadow:0 4px 20px var(--accent-glow);
}
.btn:hover{transform:translateY(-1px);box-shadow:0 6px 28px var(--accent-glow)}
.btn:disabled{opacity:0.5;cursor:not-allowed;transform:none}

/* LOADING */
.loading{display:none;text-align:center;padding:40px}
.spinner{
  width:44px;height:44px;
  border:3px solid var(--border);
  border-top-color:var(--accent);
  border-radius:50%;
  animation:spin 0.8s linear infinite;
  margin:0 auto 14px;
}
@keyframes spin{to{transform:rotate(360deg)}}
.loading p{color:var(--muted);font-size:14px}

/* RESULT */
.result-box{
  display:none;
  background:var(--surface);
  border:1px solid var(--border);
  border-radius:18px;
  padding:28px;
}
.result-box h3{font-size:16px;font-weight:700;margin-bottom:16px;color:var(--accent)}
.result-content{
  background:var(--bg);
  border-radius:10px;padding:18px;
  font-size:14px;line-height:1.9;
  color:#ddd;white-space:pre-wrap;
}
.result-actions{display:flex;gap:10px;margin-top:16px}
.btn-outline{
  background:transparent;
  border:1.5px solid var(--border);
  color:var(--muted);
  border-radius:10px;padding:9px 20px;
  font-family:'Cairo',sans-serif;font-size:13px;font-weight:600;
  cursor:pointer;transition:all 0.2s;
}
.btn-outline:hover{border-color:var(--accent);color:var(--accent)}
.btn-outline.copied{border-color:var(--green);color:var(--green)}

/* ERROR */
.error-box{
  display:none;
  background:rgba(255,59,92,0.1);
  border:1px solid rgba(255,59,92,0.3);
  border-radius:10px;padding:14px 18px;
  color:#ff6b81;font-size:14px;
  margin-bottom:16px;
}

/* HOME */
.tools-grid{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(200px,1fr));
  gap:14px;
  margin-top:8px;
}
.tool-card{
  background:var(--surface);
  border:1px solid var(--border);
  border-radius:14px;padding:20px;
  cursor:pointer;transition:all 0.2s;
}
.tool-card:hover{border-color:var(--accent);transform:translateY(-2px);background:rgba(108,99,255,0.05)}
.tool-card .t-icon{font-size:28px;margin-bottom:10px}
.tool-card .t-name{font-size:14px;font-weight:700;margin-bottom:4px}
.tool-card .t-desc{font-size:12px;color:var(--muted);line-height:1.5}

/* SLIDES RESULT */
.slides-container{display:flex;flex-direction:column;gap:12px}
.slide-card{
  background:var(--bg);border:1px solid var(--border);
  border-radius:10px;padding:16px 20px;
}
.slide-num{font-size:11px;color:var(--accent);font-weight:700;text-transform:uppercase;margin-bottom:6px}
.slide-title{font-size:15px;font-weight:700;margin-bottom:8px}
.slide-content{font-size:13px;color:#ccc;line-height:1.7;white-space:pre-wrap}
.slide-notes{font-size:12px;color:var(--muted);margin-top:8px;padding-top:8px;border-top:1px solid var(--border)}

@media(max-width:768px){
  .sidebar{width:100%;min-width:0;position:fixed;bottom:0;top:auto;right:0;left:0;flex-direction:row;padding:0;border-left:none;border-top:1px solid var(--border);height:60px;overflow-x:auto;overflow-y:hidden}
  .sidebar-logo,.section-title,.api-bar{display:none}
  .nav-item{flex-direction:column;gap:3px;padding:8px 14px;font-size:10px;border-right:none;border-top:3px solid transparent;white-space:nowrap}
  .nav-item.active{border-right-color:transparent;border-top-color:var(--accent)}
  .nav-item .icon{font-size:18px}
  .main{margin-right:0;padding:20px 16px 80px}
}
</style>
</head>
<body>
<div class="layout">

<!-- SIDEBAR -->
<div class="sidebar">
  <div class="sidebar-logo">
    <div class="sidebar-logo-icon">🎓</div>
    <div class="sidebar-logo-text">مساعد AI<span>الجامعة والتوظيف</span></div>
  </div>

  <div class="section-title">التوظيف</div>
  <div class="nav-item" onclick="goTo('home')"><span class="icon">🏠</span> الرئيسية</div>
  <div class="nav-item" onclick="goTo('cv')"><span class="icon">📄</span> مصمم CV</div>
  <div class="nav-item" onclick="goTo('cover')"><span class="icon">✉️</span> Cover Letter</div>
  <div class="nav-item" onclick="goTo('interview')"><span class="icon">🎤</span> تحضير مقابلة</div>
  <div class="nav-item" onclick="goTo('jobdesc')"><span class="icon">🔍</span> تحليل وصف وظيفي</div>

  <div class="section-title">الجامعة</div>
  <div class="nav-item" onclick="goTo('summary')"><span class="icon">📝</span> ملخص محاضرات</div>
  <div class="nav-item" onclick="goTo('questions')"><span class="icon">❓</span> أسئلة اختبار</div>
  <div class="nav-item" onclick="goTo('essay')"><span class="icon">✍️</span> تصحيح مقالات</div>
  <div class="nav-item" onclick="goTo('explain')"><span class="icon">💡</span> شرح مفاهيم</div>

  <div class="section-title">البريزنتيشن</div>
  <div class="nav-item" onclick="goTo('slides')"><span class="icon">🖥️</span> مولّد سلايدات</div>
  <div class="nav-item" onclick="goTo('script')"><span class="icon">🎙️</span> سكريبت العرض</div>
  <div class="nav-item" onclick="goTo('trainer')"><span class="icon">🏋️</span> مدرّب عروض</div>

  <div class="api-bar">
    <label>Claude API Key</label>
    <input type="password" id="apiKey" placeholder="sk-ant-..." oninput="saveKey()">
    <div class="api-status bad" id="apiStatus">غير محدد</div>
  </div>
</div>

<!-- MAIN -->
<div class="main">

  <!-- HOME -->
  <div class="page active" id="page-home">
    <div class="page-header">
      <h1>مرحباً 👋</h1>
      <p>اختر الأداة اللي تحتاجها من القائمة أو من البطاقات أدناه</p>
    </div>
    <div class="section-title" style="padding:0;margin-bottom:12px;font-size:11px;color:var(--muted)">التوظيف</div>
    <div class="tools-grid">
      <div class="tool-card" onclick="goTo('cv')"><div class="t-icon">📄</div><div class="t-name">مصمم CV</div><div class="t-desc">أدخل معلوماتك واحصل على CV احترافي</div></div>
      <div class="tool-card" onclick="goTo('cover')"><div class="t-icon">✉️</div><div class="t-name">Cover Letter</div><div class="t-desc">رسالة تقديم مخصصة للوظيفة</div></div>
      <div class="tool-card" onclick="goTo('interview')"><div class="t-icon">🎤</div><div class="t-name">تحضير مقابلة</div><div class="t-desc">أسئلة متوقعة مع نماذج إجابات</div></div>
      <div class="tool-card" onclick="goTo('jobdesc')"><div class="t-icon">🔍</div><div class="t-name">تحليل وصف وظيفي</div><div class="t-desc">افهم وش يبحثون عنه بالضبط</div></div>
    </div>
    <div class="section-title" style="padding:0;margin:20px 0 12px;font-size:11px;color:var(--muted)">الجامعة</div>
    <div class="tools-grid">
      <div class="tool-card" onclick="goTo('summary')"><div class="t-icon">📝</div><div class="t-name">ملخص محاضرات</div><div class="t-desc">لخّص أي نص بنقاط واضحة</div></div>
      <div class="tool-card" onclick="goTo('questions')"><div class="t-icon">❓</div><div class="t-name">أسئلة اختبار</div><div class="t-desc">أسئلة متوقعة للمذاكرة</div></div>
      <div class="tool-card" onclick="goTo('essay')"><div class="t-icon">✍️</div><div class="t-name">تصحيح مقالات</div><div class="t-desc">صحّح وحسّن كتابتك الأكاديمية</div></div>
      <div class="tool-card" onclick="goTo('explain')"><div class="t-icon">💡</div><div class="t-name">شرح مفاهيم</div><div class="t-desc">اشرح أي موضوع صعب ببساطة</div></div>
    </div>
    <div class="section-title" style="padding:0;margin:20px 0 12px;font-size:11px;color:var(--muted)">البريزنتيشن</div>
    <div class="tools-grid">
      <div class="tool-card" onclick="goTo('slides')"><div class="t-icon">🖥️</div><div class="t-name">مولّد سلايدات</div><div class="t-desc">محتوى كامل لكل سلايد</div></div>
      <div class="tool-card" onclick="goTo('script')"><div class="t-icon">🎙️</div><div class="t-name">سكريبت العرض</div><div class="t-desc">كلام تقوله مع كل سلايد</div></div>
      <div class="tool-card" onclick="goTo('trainer')"><div class="t-icon">🏋️</div><div class="t-name">مدرّب عروض</div><div class="t-desc">تدرّب على تقديم بريزنتيشنك</div></div>
    </div>
  </div>

  <!-- CV -->
  <div class="page" id="page-cv">
    <div class="page-header"><h1>📄 مصمم CV</h1><p>أدخل معلوماتك ويطلع لك CV احترافي جاهز</p></div>
    <div class="form-card">
      <div class="row"><div class="field"><label>الاسم الكامل</label><input id="cv-name" placeholder="محمد عبدالله الغامدي"></div><div class="field"><label>المسمى الوظيفي المطلوب</label><input id="cv-title" placeholder="مهندس برمجيات"></div></div>
      <div class="row"><div class="field"><label>البريد الإلكتروني</label><input id="cv-email" placeholder="email@example.com" dir="ltr"></div><div class="field"><label>رقم الجوال</label><input id="cv-phone" placeholder="+966 5X XXX XXXX" dir="ltr"></div></div>
      <div class="field"><label>الخبرات العملية</label><textarea id="cv-exp" placeholder="شركة X - مطور ويب - 2022 إلى 2024&#10;شركة Y - متدرب - 2021"></textarea></div>
      <div class="field"><label>التعليم</label><textarea id="cv-edu" placeholder="بكالوريوس علوم حاسب - جامعة الملك سعود - 2020&#10;GPA: 4.2"></textarea></div>
      <div class="field"><label>المهارات</label><input id="cv-skills" placeholder="Python, React, SQL, إدارة المشاريع..."></div>
      <div class="field"><label>اللغة</label><select id="cv-lang"><option value="ar">عربي</option><option value="en">إنجليزي</option></select></div>
      <div class="error-box" id="cv-error"></div>
      <button class="btn" onclick="runTool('cv')">توليد CV</button>
    </div>
    <div class="loading" id="cv-loading"><div class="spinner"></div><p>جاري إنشاء CV احترافي...</p></div>
    <div class="result-box" id="cv-result"><h3>CV جاهز</h3><div class="result-content" id="cv-output"></div><div class="result-actions"><button class="btn-outline" onclick="copyResult('cv-output',this)">نسخ</button></div></div>
  </div>

  <!-- COVER LETTER -->
  <div class="page" id="page-cover">
    <div class="page-header"><h1>✉️ Cover Letter</h1><p>رسالة تقديم مخصصة تناسب الوظيفة اللي تتقدم لها</p></div>
    <div class="form-card">
      <div class="field"><label>اسمك</label><input id="cl-name" placeholder="محمد عبدالله"></div>
      <div class="field"><label>المسمى الوظيفي</label><input id="cl-job" placeholder="مطور تطبيقات موبايل"></div>
      <div class="field"><label>اسم الشركة</label><input id="cl-company" placeholder="شركة أرامكو"></div>
      <div class="field"><label>خبراتك ومهاراتك الرئيسية</label><textarea id="cl-skills" placeholder="3 سنوات خبرة في Flutter و React Native، عملت في مشاريع..."></textarea></div>
      <div class="field"><label>لماذا تريد هذه الوظيفة؟</label><textarea id="cl-why" placeholder="أريد الانضمام لأن..."></textarea></div>
      <div class="field"><label>اللغة</label><select id="cl-lang"><option value="ar">عربي</option><option value="en">إنجليزي</option></select></div>
      <div class="error-box" id="cover-error"></div>
      <button class="btn" onclick="runTool('cover')">توليد الرسالة</button>
    </div>
    <div class="loading" id="cover-loading"><div class="spinner"></div><p>جاري كتابة رسالة التقديم...</p></div>
    <div class="result-box" id="cover-result"><h3>Cover Letter جاهزة</h3><div class="result-content" id="cover-output"></div><div class="result-actions"><button class="btn-outline" onclick="copyResult('cover-output',this)">نسخ</button></div></div>
  </div>

  <!-- INTERVIEW -->
  <div class="page" id="page-interview">
    <div class="page-header"><h1>🎤 تحضير مقابلة</h1><p>أسئلة متوقعة مع نماذج إجابات احترافية</p></div>
    <div class="form-card">
      <div class="field"><label>الوظيفة المتقدم لها</label><input id="int-job" placeholder="محلل بيانات في بنك الرياض"></div>
      <div class="field"><label>سنوات خبرتك</label><select id="int-exp"><option value="طالب/حديث تخرج">طالب / حديث تخرج</option><option value="1-3 سنوات">1-3 سنوات</option><option value="3-7 سنوات">3-7 سنوات</option><option value="أكثر من 7 سنوات">أكثر من 7 سنوات</option></select></div>
      <div class="field"><label>عدد الأسئلة</label><select id="int-count"><option value="5">5 أسئلة</option><option value="10" selected>10 أسئلة</option><option value="15">15 سؤال</option></select></div>
      <div class="error-box" id="interview-error"></div>
      <button class="btn" onclick="runTool('interview')">توليد الأسئلة</button>
    </div>
    <div class="loading" id="interview-loading"><div class="spinner"></div><p>جاري تحضير أسئلة المقابلة...</p></div>
    <div class="result-box" id="interview-result"><h3>أسئلة المقابلة</h3><div class="result-content" id="interview-output"></div><div class="result-actions"><button class="btn-outline" onclick="copyResult('interview-output',this)">نسخ</button></div></div>
  </div>

  <!-- JOB DESC -->
  <div class="page" id="page-jobdesc">
    <div class="page-header"><h1>🔍 تحليل وصف وظيفي</h1><p>الصق وصف الوظيفة وافهم وش يبحثون عنه بالضبط</p></div>
    <div class="form-card">
      <div class="field"><label>وصف الوظيفة (Job Description)</label><textarea id="jd-text" style="min-height:180px" placeholder="الصق نص الوظيفة هنا..."></textarea></div>
      <div class="error-box" id="jobdesc-error"></div>
      <button class="btn" onclick="runTool('jobdesc')">تحليل الوظيفة</button>
    </div>
    <div class="loading" id="jobdesc-loading"><div class="spinner"></div><p>جاري تحليل الوصف الوظيفي...</p></div>
    <div class="result-box" id="jobdesc-result"><h3>نتيجة التحليل</h3><div class="result-content" id="jobdesc-output"></div><div class="result-actions"><button class="btn-outline" onclick="copyResult('jobdesc-output',this)">نسخ</button></div></div>
  </div>

  <!-- SUMMARY -->
  <div class="page" id="page-summary">
    <div class="page-header"><h1>📝 ملخص محاضرات</h1><p>الصق نص المحاضرة ويطلع ملخص بنقاط واضحة</p></div>
    <div class="form-card">
      <div class="field"><label>نص المحاضرة أو المادة</label><textarea id="sum-text" style="min-height:200px" placeholder="الصق نص المحاضرة هنا..."></textarea></div>
      <div class="field"><label>طول الملخص</label><select id="sum-len"><option value="قصير (نقاط رئيسية فقط)">قصير - نقاط رئيسية</option><option value="متوسط" selected>متوسط</option><option value="تفصيلي">تفصيلي</option></select></div>
      <div class="error-box" id="summary-error"></div>
      <button class="btn" onclick="runTool('summary')">تلخيص</button>
    </div>
    <div class="loading" id="summary-loading"><div class="spinner"></div><p>جاري تلخيص المحتوى...</p></div>
    <div class="result-box" id="summary-result"><h3>الملخص</h3><div class="result-content" id="summary-output"></div><div class="result-actions"><button class="btn-outline" onclick="copyResult('summary-output',this)">نسخ</button></div></div>
  </div>

  <!-- QUESTIONS -->
  <div class="page" id="page-questions">
    <div class="page-header"><h1>❓ مولّد أسئلة اختبار</h1><p>أدخل المادة ويطلع أسئلة متوقعة للمذاكرة</p></div>
    <div class="form-card">
      <div class="field"><label>محتوى المادة</label><textarea id="q-text" style="min-height:180px" placeholder="الصق محتوى الفصل أو الموضوع هنا..."></textarea></div>
      <div class="row">
        <div class="field"><label>نوع الأسئلة</label><select id="q-type"><option value="اختيار متعدد">اختيار متعدد</option><option value="مقالي">مقالي</option><option value="صح وخطأ">صح وخطأ</option><option value="مزيج من الأنواع" selected>مزيج</option></select></div>
        <div class="field"><label>عدد الأسئلة</label><select id="q-count"><option value="5">5</option><option value="10" selected>10</option><option value="20">20</option></select></div>
      </div>
      <div class="error-box" id="questions-error"></div>
      <button class="btn" onclick="runTool('questions')">توليد الأسئلة</button>
    </div>
    <div class="loading" id="questions-loading"><div class="spinner"></div><p>جاري توليد الأسئلة...</p></div>
    <div class="result-box" id="questions-result"><h3>أسئلة الاختبار</h3><div class="result-content" id="questions-output"></div><div class="result-actions"><button class="btn-outline" onclick="copyResult('questions-output',this)">نسخ</button></div></div>
  </div>

  <!-- ESSAY -->
  <div class="page" id="page-essay">
    <div class="page-header"><h1>✍️ تصحيح مقالات أكاديمية</h1><p>يصحح أخطاءك ويحسّن أسلوبك الأكاديمي</p></div>
    <div class="form-card">
      <div class="field"><label>نص المقالة</label><textarea id="essay-text" style="min-height:200px" placeholder="الصق نص مقالتك هنا..."></textarea></div>
      <div class="field"><label>اللغة</label><select id="essay-lang"><option value="عربي">عربي</option><option value="إنجليزي">إنجليزي</option></select></div>
      <div class="error-box" id="essay-error"></div>
      <button class="btn" onclick="runTool('essay')">تصحيح وتحسين</button>
    </div>
    <div class="loading" id="essay-loading"><div class="spinner"></div><p>جاري تصحيح المقالة...</p></div>
    <div class="result-box" id="essay-result"><h3>المقالة المحسّنة</h3><div class="result-content" id="essay-output"></div><div class="result-actions"><button class="btn-outline" onclick="copyResult('essay-output',this)">نسخ</button></div></div>
  </div>

  <!-- EXPLAIN -->
  <div class="page" id="page-explain">
    <div class="page-header"><h1>💡 شرح مفاهيم</h1><p>اكتب أي موضوع صعب ويشرحه لك بطريقة مبسطة</p></div>
    <div class="form-card">
      <div class="field"><label>الموضوع أو المفهوم</label><input id="exp-topic" placeholder="مثال: نظرية النسبية، الذكاء الاصطناعي، قانون فاراداي..."></div>
      <div class="field"><label>مستواك</label><select id="exp-level"><option value="مبتدئ">مبتدئ - اشرح ببساطة شديدة</option><option value="متوسط" selected>متوسط - طالب جامعي</option><option value="متقدم">متقدم - تفاصيل أكثر</option></select></div>
      <div class="error-box" id="explain-error"></div>
      <button class="btn" onclick="runTool('explain')">شرح الموضوع</button>
    </div>
    <div class="loading" id="explain-loading"><div class="spinner"></div><p>جاري شرح الموضوع...</p></div>
    <div class="result-box" id="explain-result"><h3>الشرح</h3><div class="result-content" id="explain-output"></div><div class="result-actions"><button class="btn-outline" onclick="copyResult('explain-output',this)">نسخ</button></div></div>
  </div>

  <!-- SLIDES -->
  <div class="page" id="page-slides">
    <div class="page-header"><h1>🖥️ مولّد سلايدات</h1><p>أدخل موضوعك ويطلع محتوى كامل لكل سلايد</p></div>
    <div class="form-card">
      <div class="field"><label>موضوع البريزنتيشن</label><input id="sl-topic" placeholder="مثال: تأثير الذكاء الاصطناعي على سوق العمل"></div>
      <div class="row">
        <div class="field"><label>عدد السلايدات</label><select id="sl-count"><option value="5">5 سلايدات</option><option value="8" selected>8 سلايدات</option><option value="12">12 سلايد</option></select></div>
        <div class="field"><label>اللغة</label><select id="sl-lang"><option value="عربي">عربي</option><option value="إنجليزي">إنجليزي</option></select></div>
      </div>
      <div class="field"><label>ملاحظات إضافية (اختياري)</label><input id="sl-notes" placeholder="مثال: للجمهور الأكاديمي، تضمّن إحصاءات..."></div>
      <div class="error-box" id="slides-error"></div>
      <button class="btn" onclick="runTool('slides')">توليد السلايدات</button>
    </div>
    <div class="loading" id="slides-loading"><div class="spinner"></div><p>جاري إنشاء السلايدات...</p></div>
    <div class="result-box" id="slides-result"><h3>السلايدات جاهزة</h3><div id="slides-output"></div><div class="result-actions"><button class="btn-outline" onclick="copyResult('slides-output',this)">نسخ الكل</button></div></div>
  </div>

  <!-- SCRIPT -->
  <div class="page" id="page-script">
    <div class="page-header"><h1>🎙️ سكريبت العرض</h1><p>يكتب لك كلام تقوله مع كل سلايد</p></div>
    <div class="form-card">
      <div class="field"><label>موضوع البريزنتيشن</label><input id="sc-topic" placeholder="موضوع عرضك"></div>
      <div class="field"><label>عناوين السلايدات (سطر لكل سلايد)</label><textarea id="sc-slides" placeholder="مقدمة&#10;الخلفية التاريخية&#10;التحديات الحالية&#10;الحلول المقترحة&#10;الخلاصة"></textarea></div>
      <div class="field"><label>مدة العرض</label><select id="sc-time"><option value="5 دقائق">5 دقائق</option><option value="10 دقائق" selected>10 دقائق</option><option value="20 دقيقة">20 دقيقة</option></select></div>
      <div class="error-box" id="script-error"></div>
      <button class="btn" onclick="runTool('script')">توليد السكريبت</button>
    </div>
    <div class="loading" id="script-loading"><div class="spinner"></div><p>جاري كتابة السكريبت...</p></div>
    <div class="result-box" id="script-result"><h3>سكريبت العرض</h3><div class="result-content" id="script-output"></div><div class="result-actions"><button class="btn-outline" onclick="copyResult('script-output',this)">نسخ</button></div></div>
  </div>

  <!-- TRAINER -->
  <div class="page" id="page-trainer">
    <div class="page-header"><h1>🏋️ مدرّب عروض</h1><p>تدرّب على تقديم بريزنتيشنك مع ذكاء اصطناعي يقيّم أداءك</p></div>
    <div class="form-card" id="trainer-setup">
      <div class="field"><label>موضوع بريزنتيشنك</label><input id="tr-topic" placeholder="موضوع عرضك"></div>
      <div class="error-box" id="trainer-error"></div>
      <button class="btn" onclick="startTrainer()">ابدأ التدريب</button>
    </div>
    <div id="trainer-chat" style="display:none">
      <div id="trainer-messages" style="min-height:200px;margin-bottom:16px"></div>
      <div class="form-card" style="margin-bottom:0">
        <div class="field" style="margin-bottom:0">
          <textarea id="trainer-input" placeholder="اكتب إجابتك هنا..." style="min-height:80px"></textarea>
        </div>
        <div style="margin-top:12px;display:flex;gap:10px">
          <button class="btn" onclick="sendTrainer()">إرسال</button>
          <button class="btn-outline" onclick="resetTrainer()">إعادة البدء</button>
        </div>
      </div>
    </div>
    <div class="loading" id="trainer-loading"><div class="spinner"></div><p>...</p></div>
  </div>

</div><!-- end main -->
</div><!-- end layout -->

<script>
// API KEY
window.addEventListener('DOMContentLoaded', function(){
  var saved = localStorage.getItem('claude_key_v2');
  if(saved){ document.getElementById('apiKey').value = saved; updateStatus(saved); }
});
function saveKey(){
  var k = document.getElementById('apiKey').value.trim();
  if(k) localStorage.setItem('claude_key_v2', k);
  updateStatus(k);
}
function updateStatus(k){
  var el = document.getElementById('apiStatus');
  if(k && k.startsWith('sk-ant-')){ el.textContent='محفوظ'; el.className='api-status ok'; }
  else{ el.textContent='غير محدد'; el.className='api-status bad'; }
}
function getKey(){ return document.getElementById('apiKey').value.trim() || localStorage.getItem('claude_key_v2') || ''; }

// NAVIGATION
function goTo(id){
  document.querySelectorAll('.page').forEach(function(p){ p.classList.remove('active'); });
  document.querySelectorAll('.nav-item').forEach(function(n){ n.classList.remove('active'); });
  document.getElementById('page-'+id).classList.add('active');
  document.querySelectorAll('.nav-item').forEach(function(n){
    if(n.getAttribute('onclick') && n.getAttribute('onclick').includes("'"+id+"'")) n.classList.add('active');
  });
}

// CLAUDE API
async function callClaude(prompt, tool){
  var key = getKey();
  if(!key){ showErr(tool, 'أدخل API Key أولاً من أسفل القائمة'); return null; }
  var response = await fetch('https://api.anthropic.com/v1/messages',{
    method:'POST',
    headers:{
      'Content-Type':'application/json',
      'x-api-key': key,
      'anthropic-version':'2023-06-01',
      'anthropic-dangerous-direct-browser-access':'true'
    },
    body: JSON.stringify({ model:'claude-sonnet-4-6', max_tokens:4000, messages:[{role:'user',content:prompt}] })
  });
  var data = await response.json();
  if(data.error) throw new Error(data.error.message);
  return data.content.map(function(i){ return i.text||''; }).join('');
}

function showErr(tool, msg){
  var el = document.getElementById(tool+'-error');
  if(el){ el.textContent=msg; el.style.display='block'; }
}
function hideErr(tool){
  var el = document.getElementById(tool+'-error');
  if(el) el.style.display='none';
}
function setLoad(tool, on){
  document.getElementById(tool+'-loading').style.display = on?'block':'none';
}
function showResult(tool, html, isHTML){
  var el = document.getElementById(tool+'-result');
  var out = document.getElementById(tool+'-output');
  el.style.display='block';
  if(isHTML) out.innerHTML=html;
  else out.textContent=html;
  el.scrollIntoView({behavior:'smooth'});
}

// TOOLS
var prompts = {
  cv: function(){
    var lang = document.getElementById('cv-lang').value;
    return 'اكتب CV احترافي '+lang+' للشخص التالي:\nالاسم: '+v('cv-name')+'\nالمسمى المطلوب: '+v('cv-title')+'\nالبريد: '+v('cv-email')+'\nالجوال: '+v('cv-phone')+'\nالخبرات: '+v('cv-exp')+'\nالتعليم: '+v('cv-edu')+'\nالمهارات: '+v('cv-skills')+'\n\nاكتب CV كامل ومنظم وجاهز للاستخدام.';
  },
  cover: function(){
    return 'اكتب Cover Letter '+v('cl-lang')+' احترافية:\nالاسم: '+v('cl-name')+'\nالوظيفة: '+v('cl-job')+'\nالشركة: '+v('cl-company')+'\nالخبرات والمهارات: '+v('cl-skills')+'\nسبب التقديم: '+v('cl-why')+'\n\nاكتب رسالة تقديم مقنعة ومخصصة.';
  },
  interview: function(){
    return 'أنا أتقدم لوظيفة: '+v('int-job')+'\nمستوى خبرتي: '+v('int-exp')+'\n\nاكتب '+v('int-count')+' سؤال مقابلة متوقع مع نموذج إجابة احترافية لكل سؤال. رقّم الأسئلة ووضح الإجابة بعد كل سؤال.';
  },
  jobdesc: function(){
    return 'حلّل وصف الوظيفة التالي وأخبرني:\n1. المهارات الأساسية المطلوبة\n2. المهارات الإضافية (ميزة)\n3. نوع الشخصية التي يبحثون عنها\n4. أهم الكلمات المفتاحية للـ CV\n5. نصيحة للتقديم\n\nوصف الوظيفة:\n'+v('jd-text');
  },
  summary: function(){
    return 'لخّص النص التالي تلخيصاً '+v('sum-len')+' بنقاط واضحة ومرقمة:\n\n'+v('sum-text');
  },
  questions: function(){
    return 'من المحتوى التالي، أنشئ '+v('q-count')+' سؤال من نوع "'+v('q-type')+'" مع الإجابات الصحيحة:\n\n'+v('q-text');
  },
  essay: function(){
    return 'صحّح وحسّن المقالة الأكاديمية التالية باللغة '+v('essay-lang')+'.\nأذكر الأخطاء ثم أعد كتابة النص المحسّن:\n\n'+v('essay-text');
  },
  explain: function(){
    return 'اشرح "'+v('exp-topic')+'" لشخص مستواه '+v('exp-level')+'. استخدم أمثلة وتشبيهات مبسطة. نظّم الشرح بشكل واضح.';
  },
  script: function(){
    return 'اكتب سكريبت عرض تقديمي مدته '+v('sc-time')+' عن موضوع: '+v('sc-topic')+'\nعناوين السلايدات:\n'+v('sc-slides')+'\n\nاكتب الكلام الذي يقوله المقدّم مع كل سلايد بالتفصيل.';
  }
};

function v(id){ var el=document.getElementById(id); return el ? el.value.trim() : ''; }

async function runTool(tool){
  hideErr(tool);
  document.getElementById(tool+'-result').style.display='none';
  var prompt = prompts[tool]();
  setLoad(tool, true);
  try{
    var result = await callClaude(prompt, tool);
    if(!result) return;
    if(tool==='slides'){
      renderSlides(result);
    } else {
      showResult(tool, result, false);
    }
  } catch(e){
    showErr(tool, 'خطأ: ' + e.message);
  } finally {
    setLoad(tool, false);
  }
}

// SLIDES special render
async function runTool(tool){
  hideErr(tool);
  document.getElementById(tool+'-result').style.display='none';

  var prompt;
  if(tool==='slides'){
    var topic = v('sl-topic');
    var count = v('sl-count');
    var lang = v('sl-lang');
    var notes = v('sl-notes');
    prompt = 'أنشئ '+count+' سلايد بريزنتيشن عن: '+topic+'\nاللغة: '+lang+(notes?'\nملاحظات: '+notes:'')+'\n\nلكل سلايد اكتب:\nSLIDE [رقم]: [عنوان السلايد]\nالمحتوى: [نقاط المحتوى]\nملاحظات المقدّم: [ما يقوله المقدّم]\n---\n\nاكتب '+count+' سلايدات كاملة.';
  } else {
    prompt = prompts[tool]();
  }

  setLoad(tool, true);
  try{
    var result = await callClaude(prompt, tool);
    if(!result) return;
    if(tool==='slides'){
      var parts = result.split('---');
      var html = '<div class="slides-container">';
      parts.forEach(function(part, i){
        if(part.trim()){
          var lines = part.trim().split('\n');
          var title = lines[0] || ('سلايد '+(i+1));
          var content = lines.slice(1).join('\n');
          html += '<div class="slide-card"><div class="slide-num">سلايد '+(i+1)+'</div><div class="slide-title">'+title.replace(/^SLIDE \d+:\s*/,'').replace(/^السلايد \d+:\s*/,'')+'</div><div class="slide-content">'+content+'</div></div>';
        }
      });
      html += '</div>';
      showResult('slides', html, true);
    } else {
      showResult(tool, result, false);
    }
  } catch(e){
    showErr(tool, 'خطأ: ' + e.message);
  } finally {
    setLoad(tool, false);
  }
}

// COPY
function copyResult(id, btn){
  var el = document.getElementById(id);
  var text = el.innerText || el.textContent;
  navigator.clipboard.writeText(text).then(function(){
    btn.textContent='تم النسخ';
    btn.classList.add('copied');
    setTimeout(function(){ btn.textContent='نسخ'; btn.classList.remove('copied'); }, 2000);
  });
}

// TRAINER
var trainerHistory = [];
var trainerTopic = '';

async function startTrainer(){
  trainerTopic = v('tr-topic');
  if(!trainerTopic){ showErr('trainer','أدخل موضوع بريزنتيشنك'); return; }
  if(!getKey()){ showErr('trainer','أدخل API Key'); return; }
  hideErr('trainer');
  trainerHistory = [];
  document.getElementById('trainer-setup').style.display='none';
  document.getElementById('trainer-chat').style.display='block';
  document.getElementById('trainer-messages').innerHTML='';
  await trainerAsk('أنت مدرّب عروض تقديمية محترف. سأقدم بريزنتيشن عن: '+trainerTopic+'. ابدأ بسؤالي سؤالاً واحداً لتقييم استعدادي، وبعد كل إجابة قيّمها وأعطني سؤالاً جديداً. ابدأ الآن.');
}

async function sendTrainer(){
  var msg = document.getElementById('trainer-input').value.trim();
  if(!msg) return;
  document.getElementById('trainer-input').value='';
  addMsg('user', msg);
  trainerHistory.push({role:'user',content:msg});
  await trainerAsk(null);
}

async function trainerAsk(initMsg){
  document.getElementById('trainer-loading').style.display='block';
  try{
    var messages = initMsg ? [{role:'user',content:initMsg}] : trainerHistory;
    var key = getKey();
    var res = await fetch('https://api.anthropic.com/v1/messages',{
      method:'POST',
      headers:{'Content-Type':'application/json','x-api-key':key,'anthropic-version':'2023-06-01','anthropic-dangerous-direct-browser-access':'true'},
      body: JSON.stringify({model:'claude-sonnet-4-6',max_tokens:1000,messages:messages})
    });
    var data = await res.json();
    if(data.error) throw new Error(data.error.message);
    var reply = data.content.map(function(i){return i.text||'';}).join('');
    addMsg('ai', reply);
    trainerHistory.push({role:'user',content:initMsg||''});
    trainerHistory.push({role:'assistant',content:reply});
    if(initMsg) trainerHistory = [{role:'user',content:initMsg},{role:'assistant',content:reply}];
  } catch(e){
    addMsg('ai','خطأ: '+e.message);
  } finally {
    document.getElementById('trainer-loading').style.display='none';
  }
}

function addMsg(role, text){
  var el = document.getElementById('trainer-messages');
  var div = document.createElement('div');
  div.style.cssText = 'margin-bottom:12px;padding:14px 18px;border-radius:12px;font-size:14px;line-height:1.7;white-space:pre-wrap;';
  if(role==='user'){
    div.style.background='rgba(108,99,255,0.12)';
    div.style.borderRight='3px solid var(--accent)';
    div.textContent = text;
  } else {
    div.style.background='var(--card)';
    div.style.border='1px solid var(--border)';
    div.textContent = text;
  }
  el.appendChild(div);
  el.scrollTop = el.scrollHeight;
}

function resetTrainer(){
  trainerHistory=[];
  document.getElementById('trainer-setup').style.display='block';
  document.getElementById('trainer-chat').style.display='none';
  document.getElementById('trainer-messages').innerHTML='';
}

// Set home as active nav
document.querySelector('.nav-item').classList.add('active');
</script>
</body>
</html>
