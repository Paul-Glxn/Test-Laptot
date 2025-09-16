# HIER TESTE ICH ALLES WAS ICH KANN 

<!doctype html>
<html lang="de">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Überraschungs-Playground · GitHub</title>
  <style>
    :root{--bg:#0f1724;--card:#0b1220;--muted:#94a3b8;--accent:#7c3aed;--glass:rgba(255,255,255,0.04)}
    *{box-sizing:border-box}
    html,body{height:100%;margin:0;font-family:Inter,ui-sans-serif,system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial}
    body{background:linear-gradient(180deg,#071029 0%, #071827 50%);color:#e6eef8;display:flex;align-items:center;justify-content:center;padding:24px}
    .wrap{width:100%;max-width:1100px;display:grid;grid-template-columns:420px 1fr;gap:18px}
    .panel{background:var(--card);border-radius:12px;padding:14px;box-shadow:0 6px 20px rgba(2,6,23,0.6);backdrop-filter:blur(6px)}
    header{display:flex;align-items:center;gap:12px;margin-bottom:8px}
    .logo{width:44px;height:44px;border-radius:10px;background:linear-gradient(135deg,var(--accent),#06b6d4);display:flex;align-items:center;justify-content:center;font-weight:700}
    h1{font-size:18px;margin:0}
    p.lead{margin:4px 0 12px;color:var(--muted);font-size:13px}
    label{display:block;font-size:13px;margin-bottom:6px;color:var(--muted)}
    textarea.code{width:100%;height:300px;background:transparent;border:1px solid rgba(255,255,255,0.04);padding:12px;border-radius:8px;color:#dff0ff;font-family:ui-monospace,SFMono-Regular,Menlo,Monaco,Consolas,'Liberation Mono',monospace;font-size:13px;resize:vertical}
    .controls{display:flex;gap:8px;flex-wrap:wrap}
    button{background:var(--glass);border:1px solid rgba(255,255,255,0.04);color:inherit;padding:8px 10px;border-radius:8px;cursor:pointer}
    button.primary{background:linear-gradient(90deg,var(--accent),#06b6d4);color:#041127;border:none}
    .muted{color:var(--muted);font-size:13px}
    .preview{height:640px;border-radius:10px;overflow:hidden;border:1px solid rgba(255,255,255,0.03)}
    .bottom-row{display:flex;gap:8px;align-items:center;margin-top:10px}
    .presets{display:flex;gap:8px;flex-wrap:wrap}
    .tag{padding:6px 8px;border-radius:999px;background:rgba(255,255,255,0.02);font-size:13px}
    footer{margin-top:10px;color:var(--muted);font-size:12px}
    @media (max-width:980px){.wrap{grid-template-columns:1fr;height:100%}.preview{height:420px}}
  </style>
</head>
<body>
  <div class="wrap">
    <div class="panel">
      <header>
        <div class="logo">GH</div>
        <div>
          <h1>Surprise Playground — Für GitHub Pages</h1>
          <p class="lead">Ein einzelnes index.html, das du direkt in ein GitHub-Repo legen kannst. Live-Editor, Vorschau &amp; mehrere Überraschungen.</p>
        </div>
      </header>

      <label for="code">HTML / CSS / JS (kombiniert)</label>
      <textarea id="code" class="code" spellcheck="false"></textarea>

      <div class="bottom-row">
        <div class="controls">
          <button id="liveBtn" class="primary">Live-Vorschau aktualisieren</button>
          <button id="surpriseBtn">Überrasch mich</button>
          <button id="downloadBtn">Als index.html herunterladen</button>
          <button id="copyBtn">In Zwischenablage kopieren</button>
          <button id="resetBtn">Zurücksetzen</button>
        </div>
        <div style="margin-left:auto;text-align:right">
          <div class="muted">Gespeichert: <span id="savedAt">nie</span></div>
        </div>
      </div>

      <div style="margin-top:10px;display:flex;gap:8px;align-items:center">
        <div class="presets">
          <span class="tag" data-preset="landing">Landing</span>
          <span class="tag" data-preset="clock">Uhr</span>
          <span class="tag" data-preset="galerie">SVG-Galerie</span>
          <span class="tag" data-preset="game">Mini-Game</span>
          <span class="tag" data-preset="poem">Poem</span>
        </div>
      </div>

      <footer>
        <div>Wie verwenden auf GitHub: Erstelle ein neues Repository, füge diese Datei als <code>index.html</code> hinzu und aktiviere GitHub Pages (Settings → Pages → Branch: main / gh-pages). Die Seite erscheint meistens unter <code>https://<your-username>.github.io/<repo-name>/</code>.</div>
      </footer>
    </div>

    <div class="panel">
      <header style="margin-bottom:8px">
        <h1 style="font-size:16px">Vorschau</h1>
      </header>
      <iframe id="preview" class="preview" sandbox="allow-scripts allow-same-origin"></iframe>
    </div>
  </div>

  <script>
    // --- Starter templates ---
    const TEMPLATES = {
      landing: `<!doctype html><html><head><meta charset='utf-8'><meta name='viewport' content='width=device-width,initial-scale=1'><title>Landing</title><style>body{margin:0;height:100vh;display:grid;place-items:center;background:radial-gradient(circle at 10% 10%,#0ea5a4,transparent 20%),linear-gradient(180deg,#0f1724,#071029);color:#e6eef8;font-family:system-ui,Segoe UI,Roboto}h1{font-size:clamp(20px,6vw,48px);margin:0}p{opacity:0.9}</style></head><body><div style='text-align:center;max-width:900px;padding:24px'><h1>Willkommen — eine kleine Überraschung</h1><p>Dieses Template ist responsive, minimal und bereit für GitHub Pages. Klick "Überrasch mich" für mehr Tricks.</p></div></body></html>`,

      clock: `<!doctype html><html><head><meta charset='utf-8'><meta name='viewport' content='width=device-width,initial-scale=1'><title>Uhr</title><style>body{display:grid;place-items:center;height:100vh;margin:0;background:#071827;color:#dff4ff;font-family:monospace}#time{font-size:64px;letter-spacing:2px}#date{opacity:0.8;margin-top:8px}</style></head><body><div><div id='time'>--:--:--</div><div id='date'></div></div><script>function tick(){const d=new Date();document.getElementById('time').textContent=d.toLocaleTimeString();document.getElementById('date').textContent=d.toLocaleDateString();}tick();setInterval(tick,1000);</script></body></html>`,

      galerie: `<!doctype html><html><head><meta charset='utf-8'><meta name='viewport' content='width=device-width,initial-scale=1'><title>SVG Galerie</title><style>body{margin:0;display:grid;place-items:center;min-height:100vh;background:#061426;color:#e6f7ff;font-family:system-ui}main{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:16px;width:90%;max-width:1100px;padding:24px}figure{background:rgba(255,255,255,0.02);padding:12px;border-radius:8px;display:flex;flex-direction:column;align-items:center}svg{width:100%;height:120px}</style></head><body><main>
<figure><svg viewBox='0 0 100 100'><defs><linearGradient id='g' x1='0' x2='1'><stop offset='0' stop-color='#7c3aed'/><stop offset='1' stop-color='#06b6d4'/></linearGradient></defs><rect x='5' y='5' width='90' height='90' rx='12' fill='url(#g)'/></svg><figcaption>Gradient Card</figcaption></figure>
<figure><svg viewBox='0 0 100 100'><circle cx='50' cy='50' r='40' fill='none' stroke='white' stroke-opacity='0.08' stroke-width='8'/><g transform='translate(50 50)'><path d='M0,-40 A40,40 0 0,1 40,0' stroke='white' stroke-width='6' fill='none' stroke-linecap='round' stroke='url(#g)'/></g></svg><figcaption>Arc</figcaption></figure>
<figure><svg viewBox='0 0 100 100'><g fill='none' stroke-linecap='round' stroke-linejoin='round'><path d='M10 70 Q 25 10 40 70 T 70 70' stroke='url(#g)' stroke-width='6'/></g></svg><figcaption>Waves</figcaption></figure>
</main></body></html>`,

      game: `<!doctype html><html><head><meta charset='utf-8'><meta name='viewport' content='width=device-width,initial-scale=1'><title>Mini Game</title><style>body{margin:0;height:100vh;background:#071229;color:#e6f6ff;display:flex;flex-direction:column;align-items:center;justify-content:center;font-family:system-ui}canvas{background:#042034;border-radius:8px}</style></head><body><h2>Click the moving dot!</h2><canvas id='c' width='600' height='360'></canvas><script>const c=document.getElementById('c'),ctx=c.getContext('2d');let x=50,y=50,dx=3,dy=2,r=12,score=0;function loop(){ctx.clearRect(0,0,c.width,c.height);x+=dx;y+=dy;if(x<r||x>c.width-r)dx*=-1;if(y<r||y>c.height-r)dy*=-1;ctx.beginPath();ctx.arc(x,y,r,0,Math.PI*2);ctx.fillStyle='#7c3aed';ctx.fill();requestAnimationFrame(loop)}c.addEventListener('click',e=>{const rect=c.getBoundingClientRect();const mx=e.clientX-rect.left,my=e.clientY-rect.top;const d=Math.hypot(mx-x,my-y);if(d<r){score++;r=Math.max(6,r-1);dx*=1.05;dy*=1.05;document.title='Score: '+score}});loop();</script></body></html>`,

      poem: `<!doctype html><html><head><meta charset='utf-8'><meta name='viewport' content='width=device-width,initial-scale=1'><title>Poem</title><style>body{margin:0;height:100vh;background:linear-gradient(180deg,#061426,#081024);color:#dff4ff;display:flex;align-items:center;justify-content:center;font-family:serif}article{max-width:800px;padding:40px;text-align:center}h1{margin:0 0 12px}</style></head><body><article><h1>Kurzes Poem</h1><p>Ein kleiner Code, ein leiser Plan —<br>Seiten, die wie Fenster sanft aufzieh'n.<br>Drück die Seiten, schau, was war getan,<br>und lass dich von Pixelträumen zieh'n.</p></article></body></html>`
    };

    const codeEl = document.getElementById('code');
    const preview = document.getElementById('preview');
    const savedAt = document.getElementById('savedAt');

    // Load last saved or default
    function load() {
      const last = localStorage.getItem('sg_playground_code');
      if (last) { codeEl.value = last; savedAt.textContent = new Date(localStorage.getItem('sg_playground_saved')||Date.now()).toLocaleString(); }
      else { codeEl.value = TEMPLATES.landing; }
      updatePreview();
    }

    function updatePreview() {
      const html = codeEl.value;
      preview.srcdoc = html;
      localStorage.setItem('sg_playground_code', html);
      localStorage.setItem('sg_playground_saved', Date.now());
      savedAt.textContent = new Date().toLocaleString();
    }

    document.getElementById('liveBtn').addEventListener('click', updatePreview);

    // Surprise generator: pick random template or synthesize SVG art
    document.getElementById('surpriseBtn').addEventListener('click', () => {
      const r = Math.random();
      if (r < 0.45) {
        // pick template
        const keys = Object.keys(TEMPLATES);
        const pick = keys[Math.floor(Math.random()*keys.length)];
        codeEl.value = TEMPLATES[pick];
      } else {
        // generate random SVG composition
        codeEl.value = makeRandomSVGPage();
      }
      updatePreview();
    });

    // Preset tags
    document.querySelectorAll('.tag').forEach(t=>t.addEventListener('click', e=>{
      const key = e.target.getAttribute('data-preset');
      if (TEMPLATES[key]) codeEl.value = TEMPLATES[key];
      updatePreview();
    }));

    // Download as index.html
    document.getElementById('downloadBtn').addEventListener('click', ()=>{
      const blob = new Blob([codeEl.value], {type: 'text/html'});
      const a = document.createElement('a');
      a.href = URL.createObjectURL(blob);
      a.download = 'index.html';
      a.click();
      URL.revokeObjectURL(a.href);
    });

    // Copy to clipboard
    document.getElementById('copyBtn').addEventListener('click', async ()=>{
      try { await navigator.clipboard.writeText(codeEl.value); alert('Code in Zwischenablage kopiert.'); }
      catch(e){ alert('Kopieren nicht möglich — bitte manuell markieren.'); }
    });

    // Reset
    document.getElementById('resetBtn').addEventListener('click', ()=>{
      if (confirm('Zurücksetzen: Lokale Änderungen verwerfen?')){ localStorage.removeItem('sg_playground_code'); localStorage.removeItem('sg_playground_saved'); codeEl.value = TEMPLATES.landing; updatePreview(); }
    });

    function makeRandomSVGPage(){
      const colors = ['#7c3aed','#06b6d4','#f97316','#ef4444','#10b981'];
      const c1 = colors[Math.floor(Math.random()*colors.length)];
      const c2 = colors[Math.floor(Math.random()*colors.length)];
      return `<!doctype html><html><head><meta charset='utf-8'><meta name='viewport' content='width=device-width,initial-scale=1'><title>Random Art</title><style>body{margin:0;height:100vh;background:#040b12;display:grid;place-items:center;color:#eaf8ff;font-family:system-ui}svg{width:min(92vw,1200px);height:80vh}</style></head><body><svg viewBox='0 0 1000 700' xmlns='http://www.w3.org/2000/svg'>
        <defs>
          <linearGradient id='g1' x1='0' x2='1'><stop offset='0' stop-color='${c1}'/><stop offset='1' stop-color='${c2}'/></linearGradient>
        </defs>
        <rect width='1000' height='700' rx='20' fill='url(#g1)' opacity='0.08'/>
        ${makeBlobs(6)}
        <g transform='translate(60,60)'><text x='0' y='0' font-size='42' fill='white' font-family='serif'>Ein zufälliges Bild — bereit für GitHub Pages</text></g>
      </svg></body></html>`;
    }

    function makeBlobs(n){
      let s = '';
      for(let i=0;i<n;i++){
        const x = Math.floor(Math.random()*1000);
        const y = Math.floor(Math.random()*700);
        const r = 80 + Math.floor(Math.random()*160);
        const rx = r + Math.floor(Math.random()*120);
        const ry = r + Math.floor(Math.random()*80);
        const rot = Math.floor(Math.random()*360);
        const alpha = (0.2 + Math.random()*0.35).toFixed(2);
        s += `<ellipse cx='${x}' cy='${y}' rx='${rx}' ry='${ry}' transform='rotate(${rot} ${x} ${y})' fill='white' opacity='${alpha}'/>\n`;
      }
      return s;
    }

    // auto-save every 5s
    setInterval(()=>{ localStorage.setItem('sg_playground_code', codeEl.value); localStorage.setItem('sg_playground_saved', Date.now()); savedAt.textContent = new Date().toLocaleString(); }, 5000);

    // Initialize
    load();

    // Helpful tips when running as index.html on GitHub Pages
    // (not shown in preview) — kept as comments for the user.
  </script>
</body>
</html>
