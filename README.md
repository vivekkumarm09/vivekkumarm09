<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<style>
  @import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=JetBrains+Mono:wght@300;400;700&display=swap');

  *{margin:0;padding:0;box-sizing:border-box}
  :root{
    --c1:#00f5ff;--c2:#7c3aed;--c3:#06b6d4;--c4:#8b5cf6;
    --bg:#020617;--bg2:#0a0f1e;--bg3:#0d1526;
    --card:#0f172a;--card2:#111827;
    --border:rgba(0,245,255,0.15);
    --glow:0 0 20px rgba(0,245,255,0.3);
  }
  body{background:var(--bg);color:#e2e8f0;font-family:'Space Grotesk',sans-serif;overflow-x:hidden}

  /* PARTICLE CANVAS */
  #particles{position:fixed;top:0;left:0;width:100%;height:100%;pointer-events:none;z-index:0;opacity:0.4}

  /* HERO */
  .hero{position:relative;z-index:1;min-height:340px;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:48px 24px 32px;overflow:hidden;background:radial-gradient(ellipse 80% 60% at 50% 0%,rgba(124,58,237,0.18) 0%,transparent 70%)}
  .hero::before{content:'';position:absolute;inset:0;background:linear-gradient(180deg,transparent 60%,var(--bg) 100%);z-index:0}
  .grid-overlay{position:absolute;inset:0;background-image:linear-gradient(rgba(0,245,255,0.04) 1px,transparent 1px),linear-gradient(90deg,rgba(0,245,255,0.04) 1px,transparent 1px);background-size:40px 40px;z-index:0}
  .hero-inner{position:relative;z-index:1;text-align:center}

  /* GLITCH NAME */
  .glitch{font-family:'Space Grotesk',sans-serif;font-size:clamp(32px,5vw,56px);font-weight:700;letter-spacing:-1px;color:#fff;position:relative;display:inline-block}
  .glitch::before,.glitch::after{content:attr(data-text);position:absolute;left:0;top:0;width:100%;height:100%}
  .glitch::before{color:var(--c1);animation:glitch1 3s infinite;clip-path:polygon(0 0,100% 0,100% 35%,0 35%);transform:translateX(-2px)}
  .glitch::after{color:var(--c2);animation:glitch2 3s infinite;clip-path:polygon(0 65%,100% 65%,100% 100%,0 100%);transform:translateX(2px)}
  @keyframes glitch1{0%,90%,100%{transform:translateX(-2px)}92%{transform:translateX(2px) skewX(1deg)}94%{transform:translateX(-3px)}}
  @keyframes glitch2{0%,90%,100%{transform:translateX(2px)}93%{transform:translateX(-2px) skewX(-1deg)}95%{transform:translateX(3px)}}

  .role-badge{display:inline-flex;align-items:center;gap:8px;background:rgba(0,245,255,0.08);border:1px solid rgba(0,245,255,0.25);border-radius:100px;padding:6px 18px;font-size:13px;color:var(--c1);margin:16px 0;letter-spacing:0.5px;font-family:'JetBrains Mono',monospace}
  .role-badge::before{content:'';width:7px;height:7px;border-radius:50%;background:var(--c1);animation:pulse 1.5s infinite;flex-shrink:0}
  @keyframes pulse{0%,100%{opacity:1;box-shadow:0 0 0 0 rgba(0,245,255,0.4)}50%{opacity:0.7;box-shadow:0 0 0 6px rgba(0,245,255,0)}}

  .tagline{font-size:clamp(13px,2vw,16px);color:#94a3b8;max-width:560px;line-height:1.7;margin:0 auto 24px}

  .badge-row{display:flex;flex-wrap:wrap;gap:8px;justify-content:center;margin-bottom:8px}
  .badge{display:inline-flex;align-items:center;gap:5px;padding:5px 12px;border-radius:6px;font-size:11px;font-weight:500;letter-spacing:0.3px;font-family:'JetBrains Mono',monospace;text-transform:uppercase}
  .badge-cyan{background:rgba(0,245,255,0.08);border:1px solid rgba(0,245,255,0.3);color:var(--c1)}
  .badge-purple{background:rgba(124,58,237,0.12);border:1px solid rgba(124,58,237,0.4);color:#a78bfa}
  .badge-green{background:rgba(16,185,129,0.08);border:1px solid rgba(16,185,129,0.3);color:#34d399}

  /* SECTIONS */
  .section{position:relative;z-index:1;padding:32px 20px;max-width:860px;margin:0 auto}
  .section-label{font-family:'JetBrains Mono',monospace;font-size:10px;letter-spacing:2px;text-transform:uppercase;color:var(--c1);margin-bottom:8px;opacity:0.7}
  .section-title{font-size:22px;font-weight:600;color:#f1f5f9;margin-bottom:4px}

  /* DIVIDER */
  .divider{height:1px;background:linear-gradient(90deg,transparent,var(--border),transparent);margin:8px 20px}

  /* FLAGSHIP CARDS */
  .flagship{display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-top:20px}
  @media(max-width:600px){.flagship{grid-template-columns:1fr}}
  .flag-card{background:var(--card);border:1px solid var(--border);border-radius:16px;padding:24px;position:relative;overflow:hidden;transition:transform 0.3s,border-color 0.3s,box-shadow 0.3s;cursor:default}
  .flag-card:hover{transform:translateY(-4px) scale(1.01);border-color:rgba(0,245,255,0.4);box-shadow:0 0 30px rgba(0,245,255,0.1),0 20px 40px rgba(0,0,0,0.4)}
  .flag-card::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:linear-gradient(90deg,var(--c2),var(--c1));opacity:0.8}
  .flag-card.purple::before{background:linear-gradient(90deg,var(--c4),#c084fc)}
  .card-num{font-family:'JetBrains Mono',monospace;font-size:10px;color:var(--c1);letter-spacing:2px;margin-bottom:8px;opacity:0.6}
  .card-title{font-size:16px;font-weight:600;color:#f1f5f9;margin-bottom:6px;display:flex;align-items:center;gap:8px}
  .card-desc{font-size:13px;color:#64748b;line-height:1.6;margin-bottom:14px}
  .code-snippet{background:#020917;border:1px solid rgba(255,255,255,0.06);border-radius:8px;padding:12px;font-family:'JetBrains Mono',monospace;font-size:10.5px;line-height:1.6;color:#94a3b8;margin-bottom:14px;overflow:hidden}
  .kw{color:#c084fc}.fn{color:var(--c1)}.str{color:#86efac}.cm{color:#475569}.v{color:#fb923c}
  .tag-row{display:flex;flex-wrap:wrap;gap:5px}
  .tag{font-size:10px;padding:3px 8px;border-radius:4px;font-family:'JetBrains Mono',monospace;font-weight:500;text-transform:uppercase;letter-spacing:0.3px}
  .t-py{background:rgba(59,130,246,0.12);color:#60a5fa;border:1px solid rgba(59,130,246,0.2)}
  .t-lc{background:rgba(16,185,129,0.1);color:#34d399;border:1px solid rgba(16,185,129,0.2)}
  .t-hf{background:rgba(251,191,36,0.1);color:#fbbf24;border:1px solid rgba(251,191,36,0.2)}
  .t-tf{background:rgba(239,68,68,0.1);color:#f87171;border:1px solid rgba(239,68,68,0.2)}
  .t-sp{background:rgba(99,102,241,0.1);color:#818cf8;border:1px solid rgba(99,102,241,0.2)}
  .t-cv{background:rgba(20,184,166,0.1);color:#2dd4bf;border:1px solid rgba(20,184,166,0.2)}

  /* ARCH DIAGRAM */
  .arch{background:#020917;border:1px solid rgba(255,255,255,0.05);border-radius:10px;padding:14px;margin-bottom:14px;font-family:'JetBrains Mono',monospace;font-size:10px;line-height:1.7;color:#475569}
  .arch .node{color:var(--c1)}.arch .arrow{color:#334155}.arch .label{color:#94a3b8}

  /* STATS GRID */
  .stats-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-top:20px}
  @media(max-width:600px){.stats-grid{grid-template-columns:repeat(2,1fr)}}
  .stat-card{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:16px;text-align:center;transition:border-color 0.3s,transform 0.3s}
  .stat-card:hover{border-color:rgba(0,245,255,0.35);transform:translateY(-2px)}
  .stat-num{font-size:28px;font-weight:700;color:var(--c1);font-family:'JetBrains Mono',monospace;line-height:1}
  .stat-label{font-size:11px;color:#475569;margin-top:4px;letter-spacing:0.5px;text-transform:uppercase}

  /* SKILL MATRIX */
  .skill-matrix{margin-top:20px;display:grid;gap:8px}
  .skill-row{display:grid;grid-template-columns:140px 1fr 50px;align-items:center;gap:12px}
  .skill-name{font-size:12px;color:#94a3b8;font-family:'JetBrains Mono',monospace}
  .skill-bar-bg{height:5px;background:rgba(255,255,255,0.05);border-radius:100px;overflow:hidden}
  .skill-bar{height:100%;border-radius:100px;background:linear-gradient(90deg,var(--c2),var(--c1));width:0%;transition:width 1.2s cubic-bezier(0.16,1,0.3,1)}
  .skill-pct{font-size:11px;color:#475569;font-family:'JetBrains Mono',monospace;text-align:right}

  /* PROJECT GRID */
  .proj-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-top:20px}
  @media(max-width:600px){.proj-grid{grid-template-columns:1fr}}
  .proj-card{background:var(--card);border:1px solid rgba(255,255,255,0.06);border-radius:12px;padding:18px;transition:border-color 0.3s,transform 0.3s}
  .proj-card:hover{border-color:rgba(0,245,255,0.25);transform:translateY(-3px)}
  .proj-icon{font-size:22px;margin-bottom:8px}
  .proj-title{font-size:14px;font-weight:600;color:#e2e8f0;margin-bottom:4px}
  .proj-desc{font-size:12px;color:#475569;line-height:1.5;margin-bottom:10px}
  .proj-flow{font-family:'JetBrains Mono',monospace;font-size:9.5px;color:#334155;background:#020917;border-radius:6px;padding:8px;margin-bottom:10px;line-height:1.6}
  .proj-flow .h{color:#60a5fa}.proj-flow .g{color:#34d399}

  /* TECH CLOUD */
  .tech-cloud{display:flex;flex-wrap:wrap;gap:8px;margin-top:16px}
  .tech-pill{display:inline-flex;align-items:center;gap:6px;padding:6px 12px;background:var(--card);border:1px solid rgba(255,255,255,0.07);border-radius:8px;font-size:12px;color:#94a3b8;transition:border-color 0.3s,color 0.3s,transform 0.2s;cursor:default}
  .tech-pill:hover{border-color:var(--c1);color:var(--c1);transform:translateY(-2px)}
  .tech-dot{width:6px;height:6px;border-radius:50%}

  /* CONNECT */
  .connect-row{display:flex;flex-wrap:wrap;gap:10px;margin-top:20px;justify-content:center}
  .connect-btn{display:inline-flex;align-items:center;gap:8px;padding:10px 20px;border-radius:10px;font-size:13px;font-weight:500;text-decoration:none;transition:all 0.25s;border:1px solid}
  .btn-linkedin{background:rgba(10,102,194,0.12);border-color:rgba(10,102,194,0.35);color:#60a5fa}
  .btn-linkedin:hover{background:rgba(10,102,194,0.22);border-color:rgba(10,102,194,0.6);transform:translateY(-2px)}
  .btn-github{background:rgba(255,255,255,0.04);border-color:rgba(255,255,255,0.12);color:#e2e8f0}
  .btn-github:hover{background:rgba(255,255,255,0.08);border-color:rgba(255,255,255,0.25);transform:translateY(-2px)}
  .btn-email{background:rgba(239,68,68,0.08);border-color:rgba(239,68,68,0.25);color:#f87171}
  .btn-email:hover{background:rgba(239,68,68,0.15);transform:translateY(-2px)}

  /* FOOTER */
  .footer{text-align:center;padding:32px 20px 40px;position:relative;z-index:1}
  .footer-line{height:1px;background:linear-gradient(90deg,transparent,rgba(0,245,255,0.2),transparent);margin-bottom:24px}
  .footer-quote{font-family:'JetBrains Mono',monospace;font-size:12px;color:#334155;font-style:italic}
  .footer-sig{font-size:11px;color:#1e293b;margin-top:8px;letter-spacing:1px;text-transform:uppercase}

  /* ANIMATE IN */
  .reveal{opacity:0;transform:translateY(24px);transition:opacity 0.6s ease,transform 0.6s ease}
  .reveal.visible{opacity:1;transform:translateY(0)}

  /* NEURAL NET SVG */
  .neural-wrap{display:flex;justify-content:center;margin:20px 0 4px}
</style>
</head>
<body>

<canvas id="particles"></canvas>

<!-- HERO -->
<div class="hero">
  <div class="grid-overlay"></div>
  <div class="hero-inner">
    <div style="font-family:'JetBrains Mono',monospace;font-size:11px;color:#475569;letter-spacing:2px;margin-bottom:16px;text-transform:uppercase">
      &lt; DATA SCIENCE ENGINEER /&gt;
    </div>
    <div class="glitch" data-text="Vivek Kumar Mishra">Vivek Kumar Mishra</div>
    <div style="margin-top:16px">
      <span class="role-badge">Available for AI/ML Opportunities</span>
    </div>
    <p class="tagline">Building autonomous AI systems that think, learn, and act.<br>From raw data to real-world intelligence.</p>
    <div class="badge-row">
      <span class="badge badge-cyan">⚡ Agentic AI</span>
      <span class="badge badge-purple">📄 Document Intelligence</span>
      <span class="badge badge-cyan">🧠 Deep Learning</span>
      <span class="badge badge-green">🏥 Medical AI</span>
      <span class="badge badge-purple">💬 NLP / LLMs</span>
      <span class="badge badge-cyan">🌾 AgriTech AI</span>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- STATS -->
<div class="section reveal">
  <div class="section-label">// metrics</div>
  <div class="section-title">By the Numbers</div>
  <div class="stats-grid">
    <div class="stat-card">
      <div class="stat-num" id="s1">0</div>
      <div class="stat-label">Projects</div>
    </div>
    <div class="stat-card">
      <div class="stat-num" id="s2">0</div>
      <div class="stat-label">Repos</div>
    </div>
    <div class="stat-card">
      <div class="stat-num" id="s3">0</div>
      <div class="stat-label">ML Models</div>
    </div>
    <div class="stat-card">
      <div class="stat-num" id="s4">0</div>
      <div class="stat-label">Domains</div>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- FLAGSHIP -->
<div class="section reveal">
  <div class="section-label">// flagship [ pinned ]</div>
  <div class="section-title">Agentic AI &amp; Document Intelligence</div>
  <div class="flagship">

    <!-- CARD 1: AGENTIC -->
    <div class="flag-card">
      <div class="card-num">01 &mdash; AGENTIC AI</div>
      <div class="card-title">🤖 Autonomous Reasoning Pipeline</div>
      <div class="card-desc">Multi-step AI agent that plans, acts, self-critiques, and iterates — zero human in the loop.</div>
      <div class="code-snippet"><span class="kw">class</span> <span class="fn">AgenticPipeline</span>:<br>&nbsp;&nbsp;<span class="kw">def</span> <span class="fn">run</span>(<span class="v">self</span>, goal):<br>&nbsp;&nbsp;&nbsp;&nbsp;plan = <span class="v">self</span>.planner.decompose(goal)<br>&nbsp;&nbsp;&nbsp;&nbsp;act&nbsp; = <span class="v">self</span>.executor.run(plan)<br>&nbsp;&nbsp;&nbsp;&nbsp;<span class="kw">return</span> <span class="v">self</span>.reflector.iterate(act)<br><span class="cm"># ∞ loop until confident</span></div>
      <div class="arch"><span class="label">GOAL</span> <span class="arrow">──►</span> <span class="node">PLANNER</span> <span class="arrow">──►</span> <span class="node">EXECUTOR</span><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="arrow">│&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;▲</span><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="arrow">▼</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="arrow">│</span><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="node">CRITIC</span>&nbsp;&nbsp;<span class="arrow">──┘</span></div>
      <div class="tag-row">
        <span class="tag t-py">Python</span>
        <span class="tag t-lc">LangChain</span>
        <span class="tag t-hf">LLM</span>
        <span class="tag t-sp">VectorDB</span>
      </div>
    </div>

    <!-- CARD 2: DOCUMENT -->
    <div class="flag-card purple">
      <div class="card-num">02 &mdash; DOCUMENT INTELLIGENCE</div>
      <div class="card-title">📄 Information Extraction Engine</div>
      <div class="card-desc">OCR → NER → table extraction → classification → structured JSON. Any document format.</div>
      <div class="code-snippet"><span class="kw">class</span> <span class="fn">DocIntelligence</span>:<br>&nbsp;&nbsp;<span class="kw">def</span> <span class="fn">process</span>(<span class="v">self</span>, doc) <span class="kw">-&gt;</span> dict:<br>&nbsp;&nbsp;&nbsp;&nbsp;text&nbsp; = <span class="v">self</span>.ocr.extract(doc)<br>&nbsp;&nbsp;&nbsp;&nbsp;ents&nbsp; = <span class="v">self</span>.ner.predict(text)<br>&nbsp;&nbsp;&nbsp;&nbsp;tbls&nbsp; = <span class="v">self</span>.parser.tables(text)<br>&nbsp;&nbsp;&nbsp;&nbsp;<span class="kw">return</span> {<span class="str">"entities"</span>: ents, <span class="str">"tables"</span>: tbls}</div>
      <div class="arch"><span class="label">PDF/IMG</span> <span class="arrow">──►</span> <span class="node">OCR</span> <span class="arrow">──►</span> <span class="node">NER</span> <span class="arrow">──►</span> <span class="node">JSON</span><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="arrow">▼</span><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="node">CLASSIFY</span>&nbsp;<span class="arrow">+</span>&nbsp;<span class="node">SUMMARIZE</span></div>
      <div class="tag-row">
        <span class="tag t-hf">HuggingFace</span>
        <span class="tag t-sp">spaCy</span>
        <span class="tag t-py">PyMuPDF</span>
        <span class="tag t-cv">OCR</span>
      </div>
    </div>

  </div>
</div>

<div class="divider"></div>

<!-- OTHER PROJECTS -->
<div class="section reveal">
  <div class="section-label">// projects</div>
  <div class="section-title">Full Portfolio</div>
  <div class="proj-grid">

    <div class="proj-card">
      <div class="proj-icon">🏥</div>
      <div class="proj-title">Chest X-Ray Medical Diagnosis</div>
      <div class="proj-desc">CNN detecting pneumonia &amp; pulmonary conditions with clinical-grade accuracy.</div>
      <div class="proj-flow"><span class="h">Input</span>: X-Ray 256×256<br><span class="h">Model</span>: ResNet50 + Custom Head<br><span class="g">Output</span>: Pathology Map ✓</div>
      <div class="tag-row"><span class="tag t-tf">TensorFlow</span><span class="tag t-cv">OpenCV</span><span class="tag t-tf">Keras</span></div>
    </div>

    <div class="proj-card">
      <div class="proj-icon">💬</div>
      <div class="proj-title">NLP Sentiment Analysis Engine</div>
      <div class="proj-desc">Transformer-based opinion mining — VADER, TF-IDF, DistilBERT pipeline.</div>
      <div class="proj-flow"><span class="h">Input</span>: Raw Text<br><span class="h">Model</span>: Bi-LSTM / DistilBERT<br><span class="g">Output</span>: Sentiment + Score ✓</div>
      <div class="tag-row"><span class="tag t-hf">HuggingFace</span><span class="tag t-sp">NLTK</span><span class="tag t-py">Sklearn</span></div>
    </div>

    <div class="proj-card">
      <div class="proj-icon">✈️</div>
      <div class="proj-title">Airlines Price Prediction</div>
      <div class="proj-desc">XGBoost ensemble ML for real-time fare forecasting. 10K+ flight records, R² 0.91+.</div>
      <div class="proj-flow"><span class="h">Features</span>: Route, Airline, Season<br><span class="h">Model</span>: XGBoost + RF Ensemble<br><span class="g">R²</span>: 0.91+ Optimized ✓</div>
      <div class="tag-row"><span class="tag t-py">XGBoost</span><span class="tag t-cv">Pandas</span><span class="tag t-sp">Sklearn</span></div>
    </div>

    <div class="proj-card">
      <div class="proj-icon">🌾</div>
      <div class="proj-title">Agricultural Optimization Engine</div>
      <div class="proj-desc">AI-driven crop recommendation using soil, climate &amp; geospatial inputs.</div>
      <div class="proj-flow"><span class="h">Inputs</span>: N, P, K, pH, Rainfall<br><span class="h">Model</span>: SVM + Decision Tree<br><span class="g">Output</span>: Optimal Crop ✓</div>
      <div class="tag-row"><span class="tag t-py">Sklearn</span><span class="tag t-sp">Seaborn</span><span class="tag t-lc">EDA</span></div>
    </div>

    <div class="proj-card">
      <div class="proj-icon">🏠</div>
      <div class="proj-title">Bangalore House Price Regression</div>
      <div class="proj-desc">Full regression pipeline with GridSearchCV tuning for real estate pricing.</div>
      <div class="proj-flow"><span class="h">Process</span>: EDA → OHE → Ridge/Lasso<br><span class="h">Tuning</span>: GridSearchCV<br><span class="g">Result</span>: Best Model Selected ✓</div>
      <div class="tag-row"><span class="tag t-py">Sklearn</span><span class="tag t-cv">Matplotlib</span><span class="tag t-sp">Pandas</span></div>
    </div>

    <div class="proj-card">
      <div class="proj-icon">💓</div>
      <div class="proj-title">Heart Disease Classification</div>
      <div class="proj-desc">SHAP-explainable cardiac risk classification — Random Forest + Logistic Reg.</div>
      <div class="proj-flow"><span class="h">Features</span>: Age, BP, Cholesterol<br><span class="h">Model</span>: RF + SHAP Explainer<br><span class="g">Output</span>: Risk Score + Reason ✓</div>
      <div class="tag-row"><span class="tag t-tf">SHAP</span><span class="tag t-py">Sklearn</span><span class="tag t-sp">Seaborn</span></div>
    </div>

  </div>
</div>

<div class="divider"></div>

<!-- SKILLS -->
<div class="section reveal">
  <div class="section-label">// expertise</div>
  <div class="section-title">Skill Matrix</div>
  <div class="skill-matrix" id="skills">
    <div class="skill-row"><span class="skill-name">Machine Learning</span><div class="skill-bar-bg"><div class="skill-bar" data-w="95"></div></div><span class="skill-pct">95%</span></div>
    <div class="skill-row"><span class="skill-name">Data Visualization</span><div class="skill-bar-bg"><div class="skill-bar" data-w="95"></div></div><span class="skill-pct">95%</span></div>
    <div class="skill-row"><span class="skill-name">Deep Learning</span><div class="skill-bar-bg"><div class="skill-bar" data-w="88"></div></div><span class="skill-pct">88%</span></div>
    <div class="skill-row"><span class="skill-name">Agentic AI</span><div class="skill-bar-bg"><div class="skill-bar" data-w="85"></div></div><span class="skill-pct">85%</span></div>
    <div class="skill-row"><span class="skill-name">Document AI</span><div class="skill-bar-bg"><div class="skill-bar" data-w="83"></div></div><span class="skill-pct">83%</span></div>
    <div class="skill-row"><span class="skill-name">NLP / LLMs</span><div class="skill-bar-bg"><div class="skill-bar" data-w="80"></div></div><span class="skill-pct">80%</span></div>
    <div class="skill-row"><span class="skill-name">Computer Vision</span><div class="skill-bar-bg"><div class="skill-bar" data-w="78"></div></div><span class="skill-pct">78%</span></div>
    <div class="skill-row"><span class="skill-name">Feature Engineering</span><div class="skill-bar-bg"><div class="skill-bar" data-w="92"></div></div><span class="skill-pct">92%</span></div>
  </div>
</div>

<div class="divider"></div>

<!-- TECH STACK -->
<div class="section reveal">
  <div class="section-label">// stack</div>
  <div class="section-title">Tech Arsenal</div>
  <div class="tech-cloud">
    <span class="tech-pill"><span class="tech-dot" style="background:#3b82f6"></span>Python</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#ef4444"></span>TensorFlow</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#f97316"></span>PyTorch</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#d00000"></span>Keras</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#f59e0b"></span>HuggingFace</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#06b6d4"></span>spaCy</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#10b981"></span>LangChain</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#6366f1"></span>Scikit-Learn</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#8b5cf6"></span>XGBoost</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#ec4899"></span>Pandas</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#14b8a6"></span>NumPy</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#0ea5e9"></span>OpenCV</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#84cc16"></span>Matplotlib</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#f43f5e"></span>Seaborn</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#a855f7"></span>Plotly</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#64748b"></span>SQL</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#f37626"></span>Jupyter</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#f9ab00"></span>Google Colab</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#20beff"></span>Kaggle</span>
    <span class="tech-pill"><span class="tech-dot" style="background:#f05032"></span>Git</span>
  </div>
</div>

<div class="divider"></div>

<!-- CONNECT -->
<div class="section reveal" style="text-align:center">
  <div class="section-label" style="text-align:center">// connect</div>
  <div class="section-title">Let's Build Something Intelligent</div>
  <p style="font-size:13px;color:#475569;margin:8px 0 0">Open to impactful AI/ML projects, research collaborations, and data science roles.</p>
  <div class="connect-row">
    <a href="https://www.linkedin.com/in/vivek-mishra-2619542a2" class="connect-btn btn-linkedin">LinkedIn</a>
    <a href="https://github.com/vivekkumarm09" class="connect-btn btn-github">GitHub</a>
    <a href="mailto:vivekkumarm09@gmail.com" class="connect-btn btn-email">Email</a>
  </div>
</div>

<!-- FOOTER -->
<div class="footer">
  <div class="footer-line"></div>
  <div class="footer-quote">"Every dataset holds a truth. My job is to find it."</div>
  <div class="footer-sig">Vivek Kumar Mishra &bull; Data Science Engineer &bull; India</div>
</div>

<script>
// PARTICLES
const canvas = document.getElementById('particles');
const ctx = canvas.getContext('2d');
let W, H, pts = [];
function resize(){W=canvas.width=window.innerWidth;H=canvas.height=Math.max(document.body.scrollHeight,window.innerHeight)}
resize();window.addEventListener('resize',resize);
for(let i=0;i<90;i++) pts.push({x:Math.random()*2000,y:Math.random()*2000,vx:(Math.random()-.5)*0.3,vy:(Math.random()-.5)*0.3,r:Math.random()*1.5+0.5,o:Math.random()*0.5+0.2});
function drawParticles(){
  ctx.clearRect(0,0,W,H);
  pts.forEach(p=>{
    p.x+=p.vx;p.y+=p.vy;
    if(p.x<0||p.x>2000)p.vx*=-1;
    if(p.y<0||p.y>2000)p.vy*=-1;
    const sx=p.x*(W/2000),sy=p.y*(H/Math.max(H,2000));
    ctx.beginPath();ctx.arc(sx,sy,p.r,0,Math.PI*2);
    ctx.fillStyle=`rgba(0,245,255,${p.o})`;ctx.fill();
  });
  requestAnimationFrame(drawParticles);
}
drawParticles();

// COUNT UP
function countUp(el,target,dur){
  let start=0,step=target/dur*16;
  let t=setInterval(()=>{
    start+=step;
    if(start>=target){start=target;clearInterval(t)}
    el.textContent=Math.round(start)+(target>50?'%':'+');
  },16);
}
setTimeout(()=>{
  countUp(document.getElementById('s1'),7,800);
  countUp(document.getElementById('s2'),6,800);
  countUp(document.getElementById('s3'),10,800);
  countUp(document.getElementById('s4'),5,800);
},400);

// REVEAL ON SCROLL
const reveals=document.querySelectorAll('.reveal');
const obs=new IntersectionObserver(entries=>{
  entries.forEach(e=>{if(e.isIntersecting){e.target.classList.add('visible')}});
},{threshold:0.12});
reveals.forEach(r=>obs.observe(r));

// SKILL BARS
const skillObs=new IntersectionObserver(entries=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      e.target.querySelectorAll('.skill-bar').forEach(b=>{
        setTimeout(()=>{b.style.width=b.dataset.w+'%'},100);
      });
    }
  });
},{threshold:0.3});
document.querySelectorAll('#skills').forEach(s=>skillObs.observe(s));
</script>
</body>
</html>
