<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>شورتات AI</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;900&display=swap');

  * { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --bg: #0a0a0f;
    --surface: #13131a;
    --card: #1a1a24;
    --border: #2a2a3a;
    --red: #ff2d55;
    --red-glow: rgba(255,45,85,0.25);
    --purple: #bf5af2;
    --text: #f0f0f5;
    --muted: #8888aa;
    --green: #34c759;
  }

  body {
    font-family: 'Cairo', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    overflow-x: hidden;
  }

  body::before {
    content: '';
    position: fixed;
    top: -200px; left: 50%;
    transform: translateX(-50%);
    width: 800px; height: 800px;
    background: radial-gradient(circle, rgba(255,45,85,0.08) 0%, transparent 70%);
    pointer-events: none;
  }

  header { text-align: center; padding: 60px 20px 40px; }

  .logo {
    display: inline-flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 16px;
  }

  .logo-icon {
    width: 48px; height: 48px;
    background: var(--red);
    border-radius: 14px;
    display: flex; align-items: center; justify-content: center;
    font-size: 24px;
    box-shadow: 0 0 30px var(--red-glow);
  }

  .logo-text { font-size: 28px; font-weight: 900; letter-spacing: -0.5px; }
  .logo-text span { color: var(--red); }

  header p {
    color: var(--muted);
    font-size: 15px;
    max-width: 420px;
    margin: 0 auto;
    line-height: 1.7;
  }

  .container { max-width: 780px; margin: 0 auto; padding: 0 20px 80px; }

  .input-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 28px;
    margin-bottom: 20px;
  }

  .api-section {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 20px 28px;
    margin-bottom: 20px;
  }

  .api-section summary {
    cursor: pointer;
    font-size: 14px;
    font-weight: 600;
    color: var(--muted);
    list-style: none;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .api-section summary::-webkit-details-marker { display: none; }
  .api-section[open] summary { color: var(--text); margin-bottom: 14px; }

  .api-hint { font-size: 12px; color: var(--muted); margin-top: 8px; line-height: 1.6; }
  .api-hint a { color: var(--red); text-decoration: none; }

  .api-status {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    font-size: 12px;
    padding: 3px 10px;
    border-radius: 20px;
    margin-right: 8px;
  }

  .api-status.ok { background: rgba(52,199,89,0.15); color: var(--green); }
  .api-status.missing { background: rgba(255,45,85,0.1); color: var(--red); }

  label {
    display: block;
    font-size: 13px;
    font-weight: 600;
    color: var(--muted);
    margin-bottom: 10px;
    letter-spacing: 0.5px;
    text-transform: uppercase;
  }

  .url-row { display: flex; gap: 12px; }

  input[type="text"], input[type="password"] {
    flex: 1;
    background: var(--bg);
    border: 1.5px solid var(--border);
    border-radius: 12px;
    padding: 14px 18px;
    font-family: 'Cairo', sans-serif;
    font-size: 15px;
    color: var(--text);
    direction: ltr;
    transition: border-color 0.2s;
    outline: none;
    width: 100%;
  }

  input:focus {
    border-color: var(--red);
    box-shadow: 0 0 0 3px var(--red-glow);
  }

  input::placeholder { color: var(--muted); }

  .btn {
    background: var(--red);
    color: white;
    border: none;
    border-radius: 12px;
    padding: 14px 24px;
    font-family: 'Cairo', sans-serif;
    font-size: 15px;
    font-weight: 700;
    cursor: pointer;
    white-space: nowrap;
    transition: all 0.2s;
    box-shadow: 0 4px 20px var(--red-glow);
  }

  .btn:hover { transform: translateY(-1px); box-shadow: 0 6px 28px var(--red-glow); }
  .btn:active { transform: translateY(0); }
  .btn:disabled { opacity: 0.5; cursor: not-allowed; transform: none; }

  .options-row { display: flex; gap: 12px; margin-top: 16px; flex-wrap: wrap; }
  .opt-group { flex: 1; min-width: 160px; }

  select {
    width: 100%;
    background: var(--bg);
    border: 1.5px solid var(--border);
    border-radius: 12px;
    padding: 12px 16px;
    font-family: 'Cairo', sans-serif;
    font-size: 14px;
    color: var(--text);
    outline: none;
    cursor: pointer;
  }

  select:focus { border-color: var(--red); }

  .loading { display: none; text-align: center; padding: 48px; }

  .spinner {
    width: 48px; height: 48px;
    border: 3px solid var(--border);
    border-top-color: var(--red);
    border-radius: 50%;
    animation: spin 0.8s linear infinite;
    margin: 0 auto 16px;
  }

  @keyframes spin { to { transform: rotate(360deg); } }
  .loading p { color: var(--muted); font-size: 15px; }

  .results { display: none; }

  .results-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 20px;
  }

  .results-header h2 { font-size: 20px; font-weight: 700; }

  .count-badge {
    background: var(--red-glow);
    color: var(--red);
    border: 1px solid var(--red);
    border-radius: 20px;
    padding: 4px 14px;
    font-size: 13px;
    font-weight: 600;
  }

  .short-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 18px;
    padding: 24px;
    margin-bottom: 16px;
    transition: border-color 0.2s, transform 0.2s;
  }

  .short-card:hover { border-color: rgba(255,45,85,0.4); transform: translateY(-2px); }

  .card-top { display: flex; align-items: flex-start; gap: 12px; margin-bottom: 16px; }

  .short-num {
    width: 36px; height: 36px;
    background: var(--red);
    border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
    font-size: 14px; font-weight: 900;
    flex-shrink: 0;
    box-shadow: 0 2px 12px var(--red-glow);
  }

  .short-title { font-size: 17px; font-weight: 700; flex: 1; line-height: 1.5; }

  .section-label {
    font-size: 11px; font-weight: 600;
    color: var(--red);
    text-transform: uppercase;
    letter-spacing: 1px;
    margin-bottom: 6px; margin-top: 14px;
  }

  .hook-box {
    background: var(--bg);
    border-right: 3px solid var(--red);
    border-radius: 8px;
    padding: 12px 16px;
    font-size: 14px; line-height: 1.7;
    color: var(--text);
  }

  .script-box {
    background: var(--bg);
    border-radius: 8px;
    padding: 12px 16px;
    font-size: 14px; line-height: 1.8;
    color: #ccc;
    white-space: pre-wrap;
  }

  .tags-row { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 8px; }

  .tag {
    background: rgba(191,90,242,0.15);
    color: var(--purple);
    border: 1px solid rgba(191,90,242,0.3);
    border-radius: 20px;
    padding: 4px 12px;
    font-size: 12px; font-weight: 600;
  }

  .copy-btn {
    background: var(--surface);
    color: var(--muted);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 6px 14px;
    font-family: 'Cairo', sans-serif;
    font-size: 12px;
    cursor: pointer;
    transition: all 0.2s;
    margin-top: 12px;
  }

  .copy-btn:hover { background: var(--border); color: var(--text); }
  .copy-btn.copied { background: rgba(52,199,89,0.15); color: var(--green); border-color: rgba(52,199,89,0.3); }

  .error-box {
    display: none;
    background: rgba(255,45,85,0.1);
    border: 1px solid rgba(255,45,85,0.3);
    border-radius: 12px;
    padding: 16px 20px;
    color: #ff6b81;
    font-size: 14px;
    text-align: center;
    margin-bottom: 20px;
  }

  @media (max-width: 520px) {
    .url-row { flex-direction: column; }
    .btn { width: 100%; }
  }
</style>
</head>
<body>

<header>
  <div class="logo">
    <div class="logo-icon">&#9889;</div>
    <div class="logo-text">شورتات <span>AI</span></div>
  </div>
  <p>أدخل رابط أي مقطع يوتيوب وسيولّد لك أفكار شورتات جاهزة بالذكاء الاصطناعي</p>
</header>

<div class="container">

  <details class="api-section" id="apiDetails">
    <summary>
      &#128273; إعداد API Key
      <span class="api-status missing" id="apiStatus">غير محدد</span>
    </summary>
    <label>Claude API Key</label>
    <input type="password" id="apiKeyInput" placeholder="sk-ant-..." oninput="saveKey()" />
    <p class="api-hint">
      احصل على مفتاحك من
      <a href="https://console.anthropic.com" target="_blank">console.anthropic.com</a>
      ← API Keys ← Create Key
    </p>
  </details>

  <div class="input-card">
    <label>&#128279; رابط المقطع</label>
    <div class="url-row">
      <input type="text" id="urlInput" placeholder="https://www.youtube.com/watch?v=..." />
      <button class="btn" id="generateBtn" onclick="generate()">توليد</button>
    </div>
    <div class="options-row">
      <div class="opt-group">
        <label>عدد الشورتات</label>
        <select id="countSelect">
          <option value="3">3 شورتات</option>
          <option value="5" selected>5 شورتات</option>
          <option value="7">7 شورتات</option>
        </select>
      </div>
      <div class="opt-group">
        <label>اللغة</label>
        <select id="langSelect">
          <option value="ar" selected>العربية</option>
          <option value="en">الإنجليزية</option>
          <option value="both">الاثنتين</option>
        </select>
      </div>
      <div class="opt-group">
        <label>نوع المحتوى</label>
        <select id="styleSelect">
          <option value="viral">فايرل</option>
          <option value="educational">تعليمي</option>
          <option value="funny">كوميدي</option>
          <option value="motivational">تحفيزي</option>
        </select>
      </div>
    </div>
  </div>

  <div class="error-box" id="errorBox"></div>

  <div class="loading" id="loading">
    <div class="spinner"></div>
    <p>يتم تحليل المقطع وتوليد الشورتات...</p>
  </div>

  <div class="results" id="results">
    <div class="results-header">
      <h2>الشورتات المقترحة</h2>
      <span class="count-badge" id="countBadge"></span>
    </div>
    <div id="cardsContainer"></div>
  </div>
</div>

<script>
window.addEventListener('DOMContentLoaded', () => {
  const saved = localStorage.getItem('claude_key');
  if (saved) {
    document.getElementById('apiKeyInput').value = saved;
    updateKeyStatus(saved);
  }
});

function saveKey() {
  const key = document.getElementById('apiKeyInput').value.trim();
  if (key) localStorage.setItem('claude_key', key);
  updateKeyStatus(key);
}

function updateKeyStatus(key) {
  const el = document.getElementById('apiStatus');
  if (key && key.startsWith('sk-ant-')) {
    el.textContent = 'تم الحفظ';
    el.className = 'api-status ok';
    document.getElementById('apiDetails').removeAttribute('open');
  } else {
    el.textContent = 'غير محدد';
    el.className = 'api-status missing';
  }
}

async function generate() {
  const apiKey = document.getElementById('apiKeyInput').value.trim() || localStorage.getItem('claude_key') || '';
  const url = document.getElementById('urlInput').value.trim();
  const count = document.getElementById('countSelect').value;
  const lang = document.getElementById('langSelect').value;
  const style = document.getElementById('styleSelect').value;

  if (!apiKey) {
    document.getElementById('apiDetails').setAttribute('open', '');
    return showError('من فضلك أدخل Claude API Key أولاً');
  }
  if (!url) return showError('من فضلك أدخل رابط اليوتيوب');
  if (!url.includes('youtube.com') && !url.includes('youtu.be')) {
    return showError('الرابط غير صحيح، تأكد أنه رابط يوتيوب');
  }

  hideError();
  setLoading(true);
  document.getElementById('results').style.display = 'none';

  const langLabel = { ar: 'العربية', en: 'English', both: 'Arabic and English' }[lang];
  const styleLabel = { viral: 'viral and engaging', educational: 'educational', funny: 'funny and comedic', motivational: 'motivational' }[style];

  const prompt = `You are an expert short-form content creator for YouTube Shorts, Reels, and TikTok.

YouTube video URL: ${url}

Generate ${count} short video ideas based on the topic of this YouTube video. Style: ${styleLabel}. Content language: ${langLabel}.

IMPORTANT: Reply with ONLY a raw JSON object. No markdown, no backticks, no explanation.

Format:
{"video_topic":"one sentence about video topic","shorts":[{"title":"catchy title","hook":"opening line to hook viewer in 3 seconds","script":"full short script with line breaks between sentences","hashtags":["tag1","tag2","tag3","tag4","tag5"],"tip":"one filming or editing tip"}]}`;

  try {
    const response = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'x-api-key': apiKey,
        'anthropic-version': '2023-06-01',
        'anthropic-dangerous-direct-browser-access': 'true'
      },
      body: JSON.stringify({
        model: 'claude-sonnet-4-6',
        max_tokens: 4000,
        messages: [{ role: 'user', content: prompt }]
      })
    });

    const data = await response.json();
    if (data.error) throw new Error(data.error.message);

    const text = data.content.map(i => i.text || '').join('');
    const jsonMatch = text.match(/\{[\s\S]*\}/);
    if (!jsonMatch) throw new Error('تنسيق الرد غير صحيح، حاول مرة ثانية');

    const parsed = JSON.parse(jsonMatch[0]);
    if (!parsed.shorts || !Array.isArray(parsed.shorts)) throw new Error('بيانات غير صحيحة');

    renderResults(parsed);
  } catch (err) {
    if (err.message && err.message.includes('401')) {
      showError('الـ API Key غير صحيح، تأكد منه');
    } else {
      showError('خطأ: ' + (err.message || 'حاول مرة ثانية'));
    }
    console.error(err);
  } finally {
    setLoading(false);
  }
}

function renderResults(data) {
  const container = document.getElementById('cardsContainer');
  const badge = document.getElementById('countBadge');
  container.innerHTML = '';
  badge.textContent = data.shorts.length + ' شورتات';

  if (data.video_topic) {
    const topicEl = document.createElement('div');
    topicEl.style.cssText = 'color:var(--muted);font-size:13px;margin-bottom:16px;text-align:center;';
    topicEl.textContent = 'موضوع المقطع: ' + data.video_topic;
    container.appendChild(topicEl);
  }

  data.shorts.forEach(function(s, i) {
    const card = document.createElement('div');
    card.className = 'short-card';
    const tags = s.hashtags.map(function(h){ return '<span class="tag">#' + h.replace(/^#/,'') + '</span>'; }).join('');
    const tip = s.tip ? '<div class="section-label">نصيحة التصوير</div><div class="hook-box" style="border-color:var(--purple)">' + s.tip + '</div>' : '';
    card.innerHTML = '<div class="card-top"><div class="short-num">' + (i+1) + '</div><div class="short-title">' + s.title + '</div></div><div class="section-label">الهوك - أول 3 ثواني</div><div class="hook-box">' + s.hook + '</div><div class="section-label">السكريبت</div><div class="script-box">' + s.script + '</div><div class="section-label">الهاشتاقات</div><div class="tags-row">' + tags + '</div>' + tip + '<button class="copy-btn" onclick="copyCard(this,' + i + ')">نسخ الكل</button>';
    container.appendChild(card);
  });

  window._shorts = data.shorts;
  document.getElementById('results').style.display = 'block';
  document.getElementById('results').scrollIntoView({ behavior: 'smooth' });
}

function copyCard(btn, idx) {
  const s = window._shorts[idx];
  const text = s.title + '\n\nالهوك:\n' + s.hook + '\n\nالسكريبت:\n' + s.script + '\n\n' + s.hashtags.map(function(h){ return '#'+h.replace(/^#/,''); }).join(' ');
  navigator.clipboard.writeText(text).then(function() {
    btn.textContent = 'تم النسخ';
    btn.classList.add('copied');
    setTimeout(function(){ btn.textContent = 'نسخ الكل'; btn.classList.remove('copied'); }, 2000);
  });
}

function setLoading(on) {
  document.getElementById('loading').style.display = on ? 'block' : 'none';
  document.getElementById('generateBtn').disabled = on;
}

function showError(msg) {
  const box = document.getElementById('errorBox');
  box.textContent = msg;
  box.style.display = 'block';
}

function hideError() {
  document.getElementById('errorBox').style.display = 'none';
}

document.getElementById('urlInput').addEventListener('keydown', function(e) {
  if (e.key === 'Enter') generate();
});
</script>
</body>
</html>
