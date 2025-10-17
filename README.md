<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>What Drives Compositional Generalization in Visual Generative Models?</title>
  <meta name="description" content="Project page for 'What Drives Compositional Generalization in Visual Generative Models?' — a systematic study of how objectives and conditioning affect compositionality in image and video generation." />
  <meta property="og:title" content="What Drives Compositional Generalization in Visual Generative Models?" />
  <meta property="og:description" content="Continuous objectives + full conditioning drive robust compositionality; discrete categorical losses hinder it. JEPA-style auxiliary loss improves MaskGIT." />
  <meta property="og:image" content="figs/teaser.jpg" />
  <meta property="og:type" content="website" />
  <meta name="twitter:card" content="summary_large_image" />
  <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 128 128'><text y='1em' font-size='96'>🧩</text></svg>">
  <style>
    /* ===== Base ===== */
    :root { --bg:#0b0c10; --text:#e5e7eb; --muted:#9ca3af; --card:#111317; --border:#1f2937; --accent:#60a5fa; --maxw:980px; }
    @media (prefers-color-scheme: light) {
      :root { --bg:#ffffff; --text:#111827; --card:#f8fafc; --border:#e5e7eb; --muted:#6b7280; }
    }
    * { box-sizing: border-box; }
    html, body { margin:0; padding:0; background:var(--bg); color:var(--text); font-family: system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial,Apple Color Emoji,Noto Color Emoji; }
    a { color:var(--accent); text-decoration:none; } a:hover { text-decoration:underline; }
    img, video { max-width:100%; height:auto; display:block; }

    /* ===== Nav (RAE-ish) ===== */
    nav { position:sticky; top:0; z-index:50; background:rgba(11,12,16,0.85); backdrop-filter:blur(6px); border-bottom:1px solid var(--border); }
    nav .wrap { max-width:var(--maxw); margin:auto; padding:10px 16px; display:flex; align-items:center; justify-content:space-between; gap:14px; }
    nav .brand { font-weight:700; letter-spacing:.2px; color:var(--text); }
    nav .links { display:flex; gap:14px; font-size:.95rem; }

    /* ===== Header / Hero ===== */
    header { max-width:var(--maxw); margin:auto; padding:24px 24px 10px; }
    .hero { display:grid; grid-template-columns:1.2fr 1fr; gap:16px; align-items:center; }
    .authors, .affils { color:var(--muted); font-size:.95rem; }
    .badges { margin-top:12px; display:flex; flex-wrap:wrap; gap:8px; }
    .badge { display:inline-flex; align-items:center; gap:8px; background:#0f131a; border:1.5px solid #2a3442; border-radius:12px; padding:8px 14px; margin:6px 8px 0 0; box-shadow:0 2px 0 #0a0d12; font-weight:600; }
    .badge:hover { transform:translateY(-1px); box-shadow:0 4px 10px rgba(0,0,0,.25); }

    /* ===== Sections ===== */
    main { max-width:var(--maxw); margin:auto; padding:0 24px 50px; }
    section { margin-top:32px; background:var(--card); padding:20px; border-radius:12px; border:1px solid var(--border); }
    h1 { font-size:clamp(28px,4.2vw,42px); margin:0 0 8px; letter-spacing:-0.02em; }
    h2 { margin:0 0 12px; font-size:1.25rem; letter-spacing:-0.01em; }
    h3 { margin:0 0 6px; font-size:1.05rem; }
    .cap { color:var(--muted); font-size:.9rem; margin-top:6px; }
    .foot { text-align:center; color:var(--muted); font-size:.8rem; margin:36px 0; }

    /* ===== Tables ===== */
    table { width:100%; border-collapse:collapse; font-size:0.92rem; margin-top:10px; }
    th, td { border:1px solid var(--border); padding:6px 8px; text-align:center; }
    th { background:#1f2937; color:#d1d5db; }

    /* ===== Cards / Figures ===== */
    .fig-block { border:1px solid var(--border); border-radius:10px; padding:10px; background:#0d1117; }
    .grid-1 { display:grid; grid-template-columns:1fr; gap:14px; }
    .grid-2 { display:grid; grid-template-columns:1fr; gap:14px; }
    @media (min-width: 860px){ .grid-2 { grid-template-columns:1fr 1fr; } }

    /* ===== Animated Figure Widget ===== */
    .anim-fig { border:1px solid var(--border); border-radius:12px; padding:12px; background:#0d1117; }
    .anim-viewport { position:relative; width:100%; overflow:hidden; border-radius:10px; }
    .anim-step { display:none; width:100%; height:auto; position:relative; opacity:0; transition:opacity 280ms ease; }
    .anim-step.active { display:block; opacity:1; }
    .anim-controls { display:flex; align-items:center; gap:10px; justify-content:center; padding:8px 6px 2px; flex-wrap:wrap; }
    .anim-btn { background:#0f131a; border:1.5px solid #2a3442; color:var(--text); padding:6px 10px; border-radius:8px; font-weight:600; cursor:pointer; box-shadow:0 2px 0 #0a0d12; }
    .anim-btn:hover { transform:translateY(-1px); box-shadow:0 4px 10px rgba(0,0,0,.25); }
    .anim-dots { display:flex; gap:8px; }
    .anim-dot { width:10px; height:10px; border-radius:50%; border:1.5px solid #2a3442; background:#0f131a; cursor:pointer; }
    .anim-dot.active { background:#60a5fa; border-color:#60a5fa; }
    .anim-step-label { color:var(--muted); font-size:.9rem; margin-left:6px; }
    @media (prefers-reduced-motion: reduce) { .anim-step { transition:none; } }

    /* Code block (BibTeX) */
    pre { background:#0b1220; color:#e2e8f0; border:1px solid #0b1730; border-radius:12px; padding:12px 14px; overflow:auto; font-size:13px; line-height:1.5; }
  </style>
</head>
<body id="top">
  <!-- Sticky Nav -->
  <nav>
    <div class="wrap">
      <a class="brand" href="#top">Compositionality</a>
      <div class="links">
        <a href="#overview">Overview</a>
        <a href="#results">Results</a>
        <a href="#figures">Figures</a>
        <a href="#bibtex">BibTeX</a>
        <a href="#contact">Contact</a>
      </div>
    </div>
  </nav>

  <!-- Hero -->
  <header id="overview">
    <div class="hero">
      <div>
        <h1>What Drives Compositional Generalization in Visual Generative Models?</h1>
        <div class="authors">Karim Farid · Rajat Sahay* · Yumna Ali Alnaggar* · Simon Schrodi · Volker Fischer · Cordelia Schmid · Thomas Brox</div>
        <div class="affils">University of Freiburg · Bosch Center for AI · Inria/ENS/PSL/CNRS <span style="margin-left:8px;color:var(--muted);font-size:.85rem;">*equal contribution</span></div>
        <div class="badges">
          <a class="badge" href="https://arxiv.org/abs/2510.03075">📄 arXiv</a>
          <a class="badge" href="https://arxiv.org/pdf/2510.03075.pdf">🧾 PDF</a>
          <a class="badge" href="#results">📊 Results</a>
          <a class="badge" href="#figures">🖼️ Figures</a>
          <a class="badge" id="code" href="#">💻 Code (soon)</a>
        </div>
      </div>
      <div>
        <img src="figs/teaser.jpg" alt="Teaser of compositional generalization" />
      </div>
    </div>
  </header>

  <main>
    <!-- Abstract -->
    <section>
      <h2>Abstract</h2>
      <p>Compositional generalization—the ability to recombine known factors into novel configurations—is essential for reliable image and video generation. We conduct controlled experiments that vary (i) the <em>distribution type</em> optimized by the training objective (continuous vs. categorical), and (ii) the <em>information content</em> of the conditioning signal during training (full, quantized, or partially missing). Our findings are consistent across datasets and modalities: continuous objectives (DiT, MAR, GIVT) yield robust Level-2 compositionality; categorical objectives (MaskGIT) struggle. Full, precise conditioning during training is critical; a JEPA-style auxiliary loss improves discrete models.</p>
    </section>

    <!-- Key Findings -->
    <section>
      <h2>Key Findings</h2>
      <ul>
        <li><strong>Tokenizer choice is not decisive</strong>: DiT performs similarly with VAE or VQ-VAE tokenizers.</li>
        <li><strong>Continuous &gt; Categorical objectives</strong>: Switching from categorical NLL (MaskGIT) to continuous (GIVT/MAR/DiT) yields large compositional gains.</li>
        <li><strong>Conditioning information matters</strong>: Quantized or missing conditioning harms generalization—even if all factors are provided at generation time.</li>
        <li><strong>JEPA auxiliary loss helps MaskGIT</strong>: Improves Level-2 compositions and factor disentanglement.</li>
        <li><strong>Real-world videos</strong>: On CoVLA, Orbis-DiT hits Hit@1 <b>0.47</b> vs <b>0.18</b> for MaskGIT.</li>
      </ul>
    </section>

    <!-- Results — CRA table -->
    <section id="results">
      <h2>Results — CRA Retrieval (CoVLA)</h2>
      <table>
        <tr><th>Novel Split</th><th>Model</th><th>Left</th><th>Straight</th><th>Right</th><th>Hit@1 (Target)</th></tr>
        <tr><td>Day→Right</td><td>DiT</td><td>0.19</td><td>0.06</td><td><b>0.47</b></td><td><b>0.47</b></td></tr>
        <tr><td>Day→Right</td><td>MaskGIT</td><td>0.38</td><td>0.11</td><td>0.18</td><td>0.18</td></tr>
        <tr><td>Night→Left</td><td>DiT</td><td><b>0.43</b></td><td>0.04</td><td>0.04</td><td><b>0.43</b></td></tr>
        <tr><td>Night→Left</td><td>MaskGIT</td><td>0.56</td><td>0.10</td><td>0.14</td><td>0.14</td></tr>
      </table>
      <div class="cap">CRA metric (V-JEPA2 features) for generated videos vs. real splits. Higher Hit@1 indicates stronger compositional alignment.</div>
    </section>

    <!-- Figures -->
    <section id="figures">
      <h2>Main Figures</h2>

      <!-- Animated Figure (Tokenizer Study: (a) then arrows then (b)) -->
      <!-- Replace sources with the exact names as in your paper repository -->
      <article style="margin-bottom:26px;">
        <h3>Figure 1 — Tokenizer Study (Step-by-Step Animation)</h3>
        <p class="cap">Sequential reveal: (a) → arrows → (b).</p>

        <div id="fig-anim-1" class="anim-fig" data-dwell="1400">
          <div class="anim-viewport" aria-live="polite">
            <!-- Step 1: panel (a) — VAE tokenizer -->
            <img class="anim-step" data-step="0" src="figures/diffusion_vae.pdf" alt="(a) VAE tokenizer results with DiT" />
            <!-- Step 2: overlay arrows (transparent SVG/PNG) from (a) to (b) -->
            <img class="anim-step" data-step="1" src="figures/fig1/fig1_arrow_ab.svg" alt="Arrows from (a) to (b)" />
            <!-- Step 3: panel (b) — VQ-VAE tokenizer -->
            <img class="anim-step" data-step="2" src="figures/diffusion_token.pdf" alt="(b) VQ-VAE tokenizer results with DiT" />
          </div>
          <div class="anim-controls">
            <button class="anim-btn" data-action="prev" aria-label="Previous step">◀︎ Prev</button>
            <div class="anim-dots" role="tablist" aria-label="Figure steps"></div>
            <button class="anim-btn" data-action="next" aria-label="Next step">Next ▶︎</button>
            <button class="anim-btn" data-action="toggle" aria-label="Play or pause" style="margin-left:8px;">▶︎ Play</button>
            <span class="anim-step-label" aria-hidden="true"></span>
          </div>
          <div class="cap">Note: If your browser doesn’t render PDF images inline, export them to PNGs with the same names and update the <code>src</code> paths.</div>
        </div>
      </article>

      <!-- Figure 2: Conditioning completeness (step-by-step multi-panels) -->
      <article style="margin-bottom:26px;">
        <h3>Figure 2 — Conditioning Completeness</h3>
        <p class="cap">Full, precise conditioning during training is critical; quantized or dropped factors impair recombination.</p>
        <div class="grid-1">
          <div class="fig-block">
            <div class="cap"><b>2a — Full vs. secondary label</b></div>
            <img src="figures/DiT_cont_label_sec_run.pdf" alt="Full vs secondary label runs" />
          </div>
          <div class="fig-block">
            <div class="cap"><b>2b — Conditioning dropout</b></div>
            <img src="figures/diff_cont_dropout.pdf" alt="Effect of conditioning dropout" />
          </div>
          <div class="fig-block">
            <div class="cap"><b>2c — Discrete (quantized) conditioning</b></div>
            <img src="figures/discrete_DiT_XAI3.pdf" alt="Discrete/quantized conditioning" />
          </div>
          <div class="fig-block">
            <div class="cap"><b>2d — Average over seeds</b></div>
            <img src="figures/diffusion_real_dropout_avg_3seeds.pdf" alt="Averaged results across seeds for dropout" />
          </div>
        </div>
      </article>

      <!-- Figure 3: JEPA-augmented MaskGIT -->
      <article style="margin-bottom:26px;">
        <h3>Figure 3 — JEPA-Augmented MaskGIT</h3>
        <p class="cap">Adding a JEPA-style continuous objective improves compositional performance while preserving discrete sampling advantages.</p>
        <div class="fig-block">
          <img src="figures/figure_jepa.drawio.pdf" alt="JEPA objective added to MaskGIT with stop-gradient" />
        </div>
      </article>

      <!-- Figure 4: CoVLA qualitative -->
      <article>
        <h3>Figure 4 — CoVLA Qualitative Examples</h3>
        <p class="cap">Held-out day/night × turn splits. Orbis-DiT (continuous) vs Orbis-MaskGIT (categorical).</p>
        <div class="fig-block">
          <img src="figures/orbis/orbis_50.png" alt="Qualitative CoVLA generations" />
        </div>
      </article>
    </section>

    <!-- BibTeX -->
    <section id="bibtex">
      <h2>Cite</h2>
      <pre>@article{farid2025compositional,
  title   = {What Drives Compositional Generalization in Visual Generative Models?},
  author  = {Farid, Karim and Sahay, Rajat and Alnaggar, Yumna Ali and Schrodi, Simon and Fischer, Volker and Schmid, Cordelia and Brox, Thomas},
  journal = {arXiv preprint arXiv:2510.03075},
  year    = {2025},
  url     = {https://arxiv.org/abs/2510.03075}
}</pre>
    </section>

    <!-- Contact -->
    <section id="contact">
      <h2>Contact</h2>
      <p>📧 <a href="mailto:faridk@cs.uni-freiburg.de">faridk@cs.uni-freiburg.de</a></p>
    </section>

    <div class="foot">© 2025 The Authors — Static HTML. Place as <b>index.html</b> at repo root and enable GitHub Pages.</div>
  </main>

  <!-- Animated Figure Script (no dependencies) -->
  <script>
  (function(){
    function mountAnimFigure(rootId){
      const root = document.getElementById(rootId);
      if(!root) return;
      const steps = Array.from(root.querySelectorAll('.anim-step'));
      const dotsWrap = root.querySelector('.anim-dots');
      const btnPrev = root.querySelector('[data-action="prev"]');
      const btnNext = root.querySelector('[data-action="next"]');
      const btnToggle = root.querySelector('[data-action="toggle"]');
      const label = root.querySelector('.anim-step-label');
      const dwell = parseInt(root.getAttribute('data-dwell') || '1400', 10);

      let idx = 0, playing = false, timer = null;

      function set(i){
        idx = (i + steps.length) % steps.length;
        steps.forEach((el, k) => el.classList.toggle('active', k === idx));
        dotsWrap.querySelectorAll('.anim-dot').forEach((d, k) => d.classList.toggle('active', k === idx));
        if(label) label.textContent = `Step ${idx+1} / ${steps.length}`;
      }
      function next(){ set(idx + 1); }
      function prev(){ set(idx - 1); }
      function buildDots(){
        steps.forEach((_, k) => {
          const d = document.createElement('button');
          d.className = 'anim-dot';
          d.setAttribute('role','tab');
          d.setAttribute('aria-label', `Go to step ${k+1}`);
          d.addEventListener('click', ()=>{ pause(); set(k); });
          dotsWrap.appendChild(d);
        });
      }
      function play(){
        if (playing) return;
        playing = true; btnToggle.textContent = '⏸ Pause';
        timer = setInterval(next, dwell);
      }
      function pause(){
        playing = false; btnToggle.textContent = '▶︎ Play';
        if (timer) { clearInterval(timer); timer = null; }
      }
      function toggle(){ playing ? pause() : play(); }

      btnPrev.addEventListener('click', ()=>{ pause(); prev(); });
      btnNext.addEventListener('click', ()=>{ pause(); next(); });
      btnToggle.addEventListener('click', toggle);

      buildDots(); set(0);
    }

    // Mount the animated figure(s)
    mountAnimFigure('fig-anim-1');
  })();
  </script>
</body>
</html>