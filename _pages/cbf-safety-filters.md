---
layout: page
title: Safety Filters in Robotics
permalink: /cbf-safety-filters/
description: A visual introduction to nominal policies and safety filters.
nav: false
---

<style>
  .cbf-slide {
    --cbf-text: #202428;
    --cbf-arrow: #747b82;
    --cbf-state-fill: #edf6ea;
    --cbf-state-stroke: #61a63c;
    --cbf-state-accent: #387d1b;
    --cbf-policy-fill: #e8f6f9;
    --cbf-policy-stroke: #1fa6b8;
    --cbf-policy-accent: #087b8b;
    --cbf-filter-fill: #fff4e7;
    --cbf-filter-stroke: #dc963b;
    max-width: 960px;
    margin: 1.5rem auto;
  }

  html[data-theme="dark"] .cbf-slide {
    --cbf-text: #f5f7f8;
    --cbf-arrow: #abb2b9;
    --cbf-state-fill: #202c1f;
    --cbf-state-stroke: #91ce64;
    --cbf-state-accent: #a8db82;
    --cbf-policy-fill: #112a2f;
    --cbf-policy-stroke: #57c9d7;
    --cbf-policy-accent: #81dae3;
    --cbf-filter-fill: #302519;
    --cbf-filter-stroke: #eab35f;
  }

  .cbf-slide svg {
    display: block;
    width: 100%;
    height: auto;
    font-family: Arial, Helvetica, sans-serif;
  }

  .cbf-slide .cbf-text { fill: var(--cbf-text); }
  .cbf-slide .cbf-arrow { stroke: var(--cbf-arrow); }
  .cbf-slide .cbf-arrowhead { fill: var(--cbf-arrow); }
  .cbf-slide .cbf-state { fill: var(--cbf-state-fill); stroke: var(--cbf-state-stroke); }
  .cbf-slide .cbf-state-accent { fill: var(--cbf-state-accent); }
  .cbf-slide .cbf-policy { fill: var(--cbf-policy-fill); stroke: var(--cbf-policy-stroke); }
  .cbf-slide .cbf-policy-accent { fill: var(--cbf-policy-accent); }
  .cbf-slide .cbf-filter { fill: var(--cbf-filter-fill); stroke: var(--cbf-filter-stroke); }

  .cbf-slide figcaption {
    padding: 0.65rem 1rem;
  }
</style>

<figure class="cbf-slide">
  <svg viewBox="0 0 1698 809" role="img" aria-labelledby="cbf-diagram-title cbf-diagram-desc">
    <title id="cbf-diagram-title">Safety Filters in Robotics</title>
    <desc id="cbf-diagram-desc">State s enters a nominal policy. Its nominal action passes through a safety filter, which outputs a safe action. The nominal policy asks how to accomplish the task, while the safety filter prevents collisions.</desc>
    <defs>
      <marker id="cbf-arrowhead" markerWidth="26" markerHeight="26" refX="22" refY="13" orient="auto" markerUnits="userSpaceOnUse">
        <path class="cbf-arrowhead" d="M0 0 L26 13 L0 26 Z" />
      </marker>
    </defs>

    <text class="cbf-text" x="849" y="84" font-size="78" font-weight="700" text-anchor="middle">Safety Filters in Robotics</text>

    <rect class="cbf-state" x="2" y="338" width="250" height="210" rx="21" stroke-width="4" />
    <text class="cbf-text" x="127" y="431" font-size="48" text-anchor="middle">state</text>
    <text class="cbf-state-accent" x="127" y="490" font-size="48" font-style="italic" text-anchor="middle">s</text>

    <rect class="cbf-policy" x="430" y="338" width="385" height="210" rx="21" stroke-width="4" />
    <text class="cbf-text" x="622.5" y="431" font-size="44" text-anchor="middle">nominal policy</text>
    <text class="cbf-policy-accent" x="622.5" y="492" font-size="44" text-anchor="middle"><tspan font-style="italic">π</tspan><tspan baseline-shift="super" font-size="60%">ref</tspan>(<tspan font-style="italic">s</tspan>)</text>

    <rect class="cbf-filter" x="998" y="338" width="415" height="210" rx="21" stroke-width="4" />
    <text class="cbf-text" x="1205.5" y="462" font-size="48" text-anchor="middle">safety filter</text>

    <line class="cbf-arrow" x1="252" y1="443" x2="420" y2="443" stroke-width="6" marker-end="url(#cbf-arrowhead)" />
    <line class="cbf-arrow" x1="815" y1="443" x2="988" y2="443" stroke-width="6" marker-end="url(#cbf-arrowhead)" />
    <line class="cbf-arrow" x1="1413" y1="443" x2="1672" y2="443" stroke-width="6" marker-end="url(#cbf-arrowhead)" />
    <text class="cbf-text" x="906" y="398" font-size="34" text-anchor="middle"><tspan font-style="italic">u</tspan><tspan baseline-shift="super" font-size="60%">nom</tspan></text>
    <text class="cbf-text" x="1543" y="398" font-size="34" text-anchor="middle"><tspan font-style="italic">u</tspan><tspan baseline-shift="super" font-size="60%">safe</tspan></text>

    <text class="cbf-text" x="622" y="646" font-size="38" text-anchor="middle">“How do I</text>
    <text class="cbf-text" x="622" y="690" font-size="38" text-anchor="middle">accomplish my</text>
    <text class="cbf-text" x="622" y="734" font-size="38" text-anchor="middle">task?”</text>
    <text class="cbf-text" x="1205" y="685" font-size="38" text-anchor="middle">“Don’t hit stuff”</text>
  </svg>
  <figcaption>A nominal policy proposes an action to accomplish the task; the safety filter modifies it to avoid unsafe behavior.</figcaption>
</figure>

<style>
  .cbf-motion {
    --motion-text: #202428;
    --motion-muted: #626b73;
    --motion-axis: #79828a;
    --motion-blue: #087eaa;
    --motion-orange: #ba590c;
    --motion-red: #bf3e36;
    --motion-green: #3e7929;
    --motion-hazard: #f15b50;
    --motion-hazard-fill: #f15b502b;
    --motion-button-bg: #f1f4f6;
    --motion-button-border: #8e989f;
    max-width: 1100px;
    margin: 3rem auto 1.5rem;
    color: var(--motion-text);
  }

  html[data-theme="dark"] .cbf-motion {
    --motion-text: #f5f7f8;
    --motion-muted: #c3cbd0;
    --motion-axis: #aab2b8;
    --motion-blue: #71c9e9;
    --motion-orange: #ff9a48;
    --motion-red: #ff7770;
    --motion-green: #a0ce86;
    --motion-hazard: #ff7770;
    --motion-hazard-fill: #ff77702b;
    --motion-button-bg: #30363a;
    --motion-button-border: #aab2b8;
  }

  .cbf-motion svg {
    display: block;
    width: 100%;
    height: auto;
    overflow: visible;
    font-family: Arial, Helvetica, sans-serif;
  }

  .cbf-motion .motion-text { fill: var(--motion-text); }
  .cbf-motion .motion-muted { fill: var(--motion-muted); }
  .cbf-motion .motion-axis { stroke: var(--motion-axis); }
  .cbf-motion .motion-axis-fill { fill: var(--motion-axis); }
  .cbf-motion .motion-blue { fill: var(--motion-blue); }
  .cbf-motion .motion-blue-stroke { stroke: var(--motion-blue); }
  .cbf-motion .motion-orange { fill: var(--motion-orange); }
  .cbf-motion .motion-orange-stroke { stroke: var(--motion-orange); }
  .cbf-motion .motion-red { fill: var(--motion-red); }
  .cbf-motion .motion-green { fill: var(--motion-green); }
  .cbf-motion .motion-green-stroke { stroke: var(--motion-green); }
  .cbf-motion .motion-hazard { fill: var(--motion-hazard-fill); stroke: var(--motion-hazard); }
  .cbf-motion .motion-equation { font-family: Georgia, 'Times New Roman', serif; }
  .cbf-motion .motion-alpha-symbol,
  .cbf-motion .motion-h-symbol { fill: var(--motion-text); }
  .cbf-motion.is-started .motion-alpha-symbol { fill: var(--motion-red); }
  .cbf-motion.is-started .motion-h-symbol { fill: var(--motion-blue); }
  .cbf-motion .motion-annotation,
  .cbf-motion .motion-takeaway { opacity: 0; }
  .cbf-motion.is-started .motion-annotation,
  .cbf-motion.is-complete .motion-takeaway { opacity: 1; }

  .cbf-motion figcaption {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    gap: 0.75rem 1rem;
    padding: 0.5rem 0.75rem;
  }

  .cbf-motion button {
    padding: 0.4rem 0.8rem;
    border: 1px solid var(--motion-button-border);
    border-radius: 0.35rem;
    background: var(--motion-button-bg);
    color: var(--motion-text);
    cursor: pointer;
  }

  .cbf-motion button:focus-visible {
    outline: 3px solid var(--motion-blue);
    outline-offset: 2px;
  }
</style>

<figure class="cbf-motion" id="cbf-motion">
  <svg viewBox="0 0 1200 720" role="img" aria-labelledby="cbf-motion-title cbf-motion-desc">
    <title id="cbf-motion-title">Slow Down Near the Safety Boundary</title>
    <desc id="cbf-motion-desc">A graph shows safety value h decreasing toward zero and its derivative increasing toward zero. At the same time, a controlled system follows a curved path around an unsafe circular region instead of continuing along its nominal straight path.</desc>
    <defs>
      <marker id="cbf-motion-arrow" markerWidth="11" markerHeight="11" refX="9" refY="5.5" orient="auto" markerUnits="userSpaceOnUse">
        <path class="motion-axis-fill" d="M0 0 L11 5.5 L0 11 Z" />
      </marker>
    </defs>

    <text class="motion-text" x="600" y="57" font-size="47" font-weight="700" text-anchor="middle">Slow Down Near the Safety Boundary</text>
    <text class="motion-text motion-equation" x="250" y="129" font-size="33"><tspan font-style="italic">ḣ</tspan> ≥ −<tspan class="motion-alpha-symbol" font-style="italic">α</tspan>(<tspan class="motion-h-symbol" font-style="italic">h</tspan>)</text>
    <text class="motion-text motion-equation" x="475" y="129" font-size="33"><tspan font-style="italic">α</tspan>(<tspan font-style="italic">h</tspan>) = <tspan font-style="italic">αh</tspan></text>
    <text class="motion-text motion-equation" x="790" y="129" font-size="31">“exponential CBF”</text>
    <text class="motion-blue motion-annotation" x="108" y="185" font-size="24">“distance from unsafe set”</text>
    <text class="motion-red motion-annotation" x="244" y="220" font-size="24">“how hard do we brake”</text>

    <line class="motion-axis" x1="42" y1="575" x2="42" y2="270" stroke-width="2.5" marker-end="url(#cbf-motion-arrow)" />
    <line class="motion-axis" x1="42" y1="430" x2="555" y2="430" stroke-width="2.5" marker-end="url(#cbf-motion-arrow)" />
    <line class="motion-axis" x1="42" y1="430" x2="540" y2="430" stroke-width="2" stroke-dasharray="8 6" />
    <g class="motion-axis" stroke-width="2">
      <path d="M33 358h18 M33 502h18 M33 574h18 M143 422v16 M244 422v16 M345 422v16 M446 422v16" />
    </g>
    <path id="cbf-h-curve" class="motion-blue-stroke" fill="none" stroke-width="4" />
    <path id="cbf-hdot-curve" class="motion-orange-stroke" fill="none" stroke-width="4" />
    <text class="motion-blue motion-equation" x="123" y="300" font-size="27" font-style="italic">h(t)</text>
    <text class="motion-orange motion-equation" x="123" y="558" font-size="27" font-style="italic">ḣ(t)</text>
    <text class="motion-muted" x="550" y="438" font-size="25">time</text>
    <line id="cbf-time-cursor" class="motion-axis" x1="42" y1="270" x2="42" y2="575" stroke-width="2" stroke-dasharray="7 7" />
    <circle id="cbf-h-dot" class="motion-blue" cx="42" cy="286" r="8" />
    <circle id="cbf-hdot-dot" class="motion-orange" cx="42" cy="535" r="8" />

    <line class="motion-axis" x1="692" y1="430" x2="1125" y2="430" stroke-width="3" stroke-dasharray="11 10" />
    <path id="cbf-avoidance-path" class="motion-green-stroke" d="M692 430 C766 430 841 403 878 368 C917 326 963 325 1010 351" fill="none" stroke-width="3" />
    <circle class="motion-hazard" cx="960" cy="430" r="69" stroke-width="4" />
    <text class="motion-red" x="960" y="438" font-size="25" text-anchor="middle">unsafe set</text>
    <text class="motion-muted" x="1052" y="465" font-size="21">nominal path</text>
    <circle id="cbf-robot" cx="692" cy="430" r="22" style="fill: var(--motion-green)" />
    <text class="motion-green" x="960" y="625" font-size="25" text-anchor="middle">controlled system</text>
    <text class="motion-green motion-takeaway" x="600" y="692" font-size="21" text-anchor="middle">As h approaches zero, inward motion vanishes and the safe motion becomes tangential.</text>
  </svg>
  <figcaption>
    <button id="cbf-motion-button" type="button" aria-controls="cbf-motion" aria-label="Play safety boundary animation">Play animation</button>
    <span>The safety filter slows inward motion as the system approaches the unsafe set.</span>
  </figcaption>
</figure>

<script>
  (() => {
    const figure = document.getElementById('cbf-motion');
    if (!figure) return;

    const button = document.getElementById('cbf-motion-button');
    const hCurve = document.getElementById('cbf-h-curve');
    const hdotCurve = document.getElementById('cbf-hdot-curve');
    const cursor = document.getElementById('cbf-time-cursor');
    const hDot = document.getElementById('cbf-h-dot');
    const hdotDot = document.getElementById('cbf-hdot-dot');
    const robot = document.getElementById('cbf-robot');
    const path = document.getElementById('cbf-avoidance-path');
    const duration = 7000;
    let progress = 0;
    let playing = false;
    let frame = 0;
    let lastTime = null;

    const h = (p) => Math.exp(-3.5 * p);
    const curve = (y) => Array.from({ length: 101 }, (_, i) => {
      const p = i / 100;
      return `${i ? 'L' : 'M'}${(42 + 500 * p).toFixed(2)} ${y(p).toFixed(2)}`;
    }).join(' ');

    hCurve.setAttribute('d', curve((p) => 430 - 144 * h(p)));
    hdotCurve.setAttribute('d', curve((p) => 430 + 105 * h(p)));

    function render() {
      const x = 42 + 500 * progress;
      cursor.setAttribute('x1', x);
      cursor.setAttribute('x2', x);
      hDot.setAttribute('cx', x);
      hDot.setAttribute('cy', 430 - 144 * h(progress));
      hdotDot.setAttribute('cx', x);
      hdotDot.setAttribute('cy', 430 + 105 * h(progress));
      const point = path.getPointAtLength(progress * path.getTotalLength());
      robot.setAttribute('cx', point.x);
      robot.setAttribute('cy', point.y);
    }

    function tick(time) {
      if (lastTime !== null) progress = Math.min(1, progress + (time - lastTime) / duration);
      lastTime = time;
      render();
      if (progress < 1) {
        frame = requestAnimationFrame(tick);
      } else {
        playing = false;
        lastTime = null;
        figure.classList.add('is-complete');
        button.textContent = 'Replay animation';
        button.setAttribute('aria-label', 'Replay safety boundary animation');
      }
    }

    button.addEventListener('click', () => {
      if (playing) {
        cancelAnimationFrame(frame);
        playing = false;
        lastTime = null;
        button.textContent = 'Resume animation';
        button.setAttribute('aria-label', 'Resume safety boundary animation');
        return;
      }
      if (progress === 1) {
        progress = 0;
        render();
        figure.classList.remove('is-complete');
      }
      figure.classList.add('is-started');
      playing = true;
      button.textContent = 'Pause animation';
      button.setAttribute('aria-label', 'Pause safety boundary animation');
      frame = requestAnimationFrame(tick);
    });

    render();
  })();
</script>

<style>
  .cbf-diff {
    --diff-text: #202428;
    --diff-muted: #626b73;
    --diff-blue: #087eaa;
    --diff-gold: #a76814;
    --diff-green: #3e7929;
    --diff-contour: #2784aa;
    --diff-region: #72ab5a26;
    --diff-button-bg: #f1f4f6;
    --diff-button-border: #8e989f;
    max-width: 1100px;
    margin: 3rem auto 1.5rem;
    color: var(--diff-text);
  }

  html[data-theme="dark"] .cbf-diff {
    --diff-text: #f5f7f8;
    --diff-muted: #c3cbd0;
    --diff-blue: #71c9e9;
    --diff-gold: #f2b96e;
    --diff-green: #a0ce86;
    --diff-contour: #55afd0;
    --diff-region: #a0ce8626;
    --diff-button-bg: #30363a;
    --diff-button-border: #aab2b8;
  }

  .cbf-diff h2 {
    margin: 0;
    color: var(--diff-text);
    font-size: clamp(1.6rem, 3.4vw, 2.6rem);
    text-align: center;
  }

  .cbf-diff .diff-subtitle {
    margin: 0.2rem 0 1.2rem;
    color: var(--diff-muted);
    text-align: center;
    font-size: clamp(0.9rem, 1.7vw, 1.15rem);
  }

  .cbf-diff .diff-stage {
    display: grid;
    grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);
    align-items: start;
    min-height: 560px;
  }

  .cbf-diff .diff-formula {
    position: relative;
    min-height: 560px;
    font-size: clamp(14px, 1.8vw, 20px);
    font-family: Georgia, 'Times New Roman', serif;
  }

  .cbf-diff .diff-objective,
  .cbf-diff .diff-constraint {
    position: absolute;
    display: flex;
    align-items: center;
    gap: 0.25em;
    white-space: nowrap;
  }

  .cbf-diff .diff-objective { top: 70px; left: 0; }
  .cbf-diff .diff-constraint { top: 225px; left: 1em; }
  .cbf-diff .diff-bounds { position: absolute; top: 380px; left: 7em; white-space: nowrap; }
  .cbf-diff .diff-result { position: absolute; top: 430px; left: 5.5em; white-space: nowrap; }
  .cbf-diff .diff-chain-rule { position: absolute; top: 475px; left: 2.8em; white-space: nowrap; }
  .cbf-diff .diff-symbol-slot,
  .cbf-diff .diff-vector-slot {
    position: relative;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    flex: none;
  }

  .cbf-diff .diff-symbol-slot { width: 6.9em; height: 5.4em; }
  .cbf-diff .diff-vector-slot { width: 5.3em; height: 7.2em; }
  .cbf-diff .diff-symbol,
  .cbf-diff .diff-numeric { position: absolute; }
  .cbf-diff .diff-numeric { opacity: 0; }
  .cbf-diff.is-expanded .diff-symbol { opacity: 0; }
  .cbf-diff.is-expanded .diff-numeric { opacity: 1; }
  .cbf-diff .diff-matrix,
  .cbf-diff .diff-vector {
    display: grid;
    align-items: center;
    justify-items: center;
    gap: 0.5em 0.7em;
    padding: 0.35em 0.5em;
    border-left: 3px solid currentColor;
    border-right: 3px solid currentColor;
    line-height: 1.2;
  }
  .cbf-diff .diff-matrix { grid-template-columns: 1fr 1fr; color: var(--diff-blue); }
  .cbf-diff .diff-vector { grid-template-columns: 1fr; color: var(--diff-gold); }
  .cbf-diff .diff-zero { color: var(--diff-muted); }
  .cbf-diff .diff-blue { color: var(--diff-blue); }
  .cbf-diff .diff-gold { color: var(--diff-gold); }
  .cbf-diff .diff-green { color: var(--diff-green); }
  .cbf-diff .diff-ellipsis { display: block; line-height: 0.65; }
  .cbf-diff .diff-result,
  .cbf-diff .diff-chain-rule,
  .cbf-diff .diff-takeaway { opacity: 0; }
  .cbf-diff.is-complete .diff-result,
  .cbf-diff.is-complete .diff-chain-rule,
  .cbf-diff.is-complete .diff-takeaway { opacity: 1; }

  .cbf-diff .diff-visual { opacity: 0; }
  .cbf-diff .diff-visual svg { display: block; width: 100%; height: auto; overflow: hidden; }
  .cbf-diff .diff-region { fill: var(--diff-region); }
  .cbf-diff .diff-contour { fill: none; stroke: var(--diff-contour); stroke-width: 1.5; }
  .cbf-diff .diff-boundary { stroke: var(--diff-gold); stroke-width: 3; }
  .cbf-diff .diff-reference { fill: var(--diff-blue); }
  .cbf-diff .diff-solution { fill: var(--diff-green); }
  .cbf-diff .diff-projection { stroke: var(--diff-green); stroke-width: 3; }
  .cbf-diff .diff-svg-label { font: 20px Georgia, 'Times New Roman', serif; }
  .cbf-diff .diff-svg-caption { font: 17px Arial, Helvetica, sans-serif; }
  .cbf-diff .diff-takeaway {
    margin: 0 0 0.5rem;
    color: var(--diff-green);
    text-align: center;
    font-size: clamp(0.9rem, 1.6vw, 1.15rem);
  }
  .cbf-diff figcaption {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    gap: 0.75rem 1rem;
    padding: 0.5rem 0.75rem;
  }
  .cbf-diff button {
    padding: 0.4rem 0.8rem;
    border: 1px solid var(--diff-button-border);
    border-radius: 0.35rem;
    background: var(--diff-button-bg);
    color: var(--diff-text);
    cursor: pointer;
  }
  .cbf-diff button:focus-visible { outline: 3px solid var(--diff-blue); outline-offset: 2px; }

  @media (max-width: 800px) {
    .cbf-diff .diff-stage { grid-template-columns: minmax(0, 1fr); }
    .cbf-diff .diff-formula { min-height: 530px; font-size: clamp(12px, 3.5vw, 19px); }
    .cbf-diff .diff-objective { top: 35px; }
    .cbf-diff .diff-constraint { top: 185px; }
    .cbf-diff .diff-bounds { top: 350px; }
    .cbf-diff .diff-result { top: 405px; }
    .cbf-diff .diff-chain-rule { top: 450px; }
    .cbf-diff .diff-visual { max-width: 550px; margin: auto; }
  }
</style>

<figure class="cbf-diff" id="cbf-diff">
  <h2>Differentiating Through the Quadratic Program</h2>
  <p class="diff-subtitle">changing QP parameters changes both the optimization landscape and its solution</p>
  <div class="diff-stage">
    <div class="diff-formula">
      <div class="diff-objective">
        <span>\(u^*=\arg\min_u\;\tfrac12(u-u_{\rm ref})^\top\)</span>
        <span class="diff-symbol-slot">
          <span class="diff-symbol">\(H_\theta\)</span>
          <span class="diff-numeric diff-matrix" aria-label="Control weighting matrix">
            <span id="cbf-w1">0.63</span><span class="diff-zero">0.00</span>
            <span class="diff-zero">0.00</span><span id="cbf-w2">1.47</span>
          </span>
        </span>
        <span>\((u-u_{\rm ref})\)</span>
      </div>
      <div class="diff-constraint">
        <span>\(\begin{gathered}L_fh_1(x)+L_gh_1(x)u\\\vdots\\L_fh_k(x)+L_gh_k(x)u\end{gathered}\)</span>
        <span>\(\ge -\)</span>
        <span class="diff-vector-slot">
          <span class="diff-symbol">\(\begin{gathered}\alpha_\theta(h_1)\\\vdots\\\alpha_\theta(h_k)\end{gathered}\)</span>
          <span class="diff-numeric diff-vector" aria-label="Barrier strengths">
            <span id="cbf-a1">0.38</span><span class="diff-ellipsis">⋮</span><span id="cbf-ak">1.26</span>
          </span>
        </span>
      </div>
      <div class="diff-bounds">\(u_{\min}\le u\le u_{\max}\)</div>
      <div class="diff-result diff-green">\(\theta\longmapsto u^*(\theta)\)</div>
      <div class="diff-chain-rule">\(\displaystyle\frac{\partial\ell}{\partial\theta}=\left(\frac{\partial\ell}{\partial u^*}\right)^\top\frac{\partial u^*}{\partial\theta}\)</div>
    </div>
    <div class="diff-visual" id="cbf-diff-visual">
      <svg viewBox="0 0 560 520" role="img" aria-labelledby="cbf-diff-title cbf-diff-desc">
        <title id="cbf-diff-title">QP solution changes with the learned parameters</title>
        <desc id="cbf-diff-desc">Elliptical objective contours and the active safety constraint move as four QP parameters change. The safe solution is the weighted projection of the reference action onto the feasible half-space.</desc>
        <defs>
          <clipPath id="cbf-diff-clip"><rect x="0" y="0" width="560" height="520" /></clipPath>
          <marker id="cbf-diff-arrow" markerWidth="12" markerHeight="12" refX="9" refY="6" orient="auto" markerUnits="userSpaceOnUse">
            <path class="diff-solution" d="M0 0 L12 6 L0 12 Z" />
          </marker>
        </defs>
        <g clip-path="url(#cbf-diff-clip)">
          <polygon id="cbf-diff-region" class="diff-region" />
          <g id="cbf-diff-contours">
            <ellipse class="diff-contour" cx="230" cy="265" />
            <ellipse class="diff-contour" cx="230" cy="265" />
            <ellipse class="diff-contour" cx="230" cy="265" />
            <ellipse class="diff-contour" cx="230" cy="265" />
          </g>
          <line id="cbf-diff-boundary" class="diff-boundary" />
          <line id="cbf-diff-projection" class="diff-projection" marker-end="url(#cbf-diff-arrow)" />
          <circle class="diff-reference" cx="230" cy="265" r="9" />
          <circle id="cbf-diff-optimum" class="diff-solution" r="9" />
        </g>
        <text x="178" y="271" class="diff-svg-label diff-reference">u<tspan baseline-shift="sub" font-size="65%">ref</tspan></text>
        <text id="cbf-diff-optimum-label" class="diff-svg-label diff-solution">u*</text>
        <text x="280" y="490" class="diff-svg-caption" fill="var(--diff-gold)" text-anchor="middle">active barrier constraint</text>
      </svg>
    </div>
  </div>
  <p class="diff-takeaway">Sensitivity Analysis of the KKT system allows us to propagate gradients from u* to some outer loss function</p>
  <figcaption>
    <button id="cbf-diff-button" type="button" aria-controls="cbf-diff" aria-label="Play differentiable QP animation">Play animation</button>
    <span>The learned weights and barrier strengths change the safe control action.</span>
  </figcaption>
</figure>

<script>
  (() => {
    const figure = document.getElementById('cbf-diff');
    if (!figure) return;

    const button = document.getElementById('cbf-diff-button');
    const visual = document.getElementById('cbf-diff-visual');
    const contours = [...document.querySelectorAll('#cbf-diff-contours ellipse')];
    const region = document.getElementById('cbf-diff-region');
    const boundary = document.getElementById('cbf-diff-boundary');
    const projection = document.getElementById('cbf-diff-projection');
    const optimum = document.getElementById('cbf-diff-optimum');
    const optimumLabel = document.getElementById('cbf-diff-optimum-label');
    const values = ['cbf-w1', 'cbf-w2', 'cbf-a1', 'cbf-ak'].map((id) => document.getElementById(id));
    const initial = [0.63, 1.47, 0.38, 1.26];
    const target = [1.71, 0.34, 1.12, 0.57];
    const expansionEnd = 1800;
    const motionEnd = 6000;
    const total = 6800;
    let elapsed = 0;
    let playing = false;
    let frame = 0;
    let lastTime = null;

    function point(x, y) {
      return [230 + 78 * (x + 0.82), 265 - 78 * (y - 0.30)];
    }

    function render() {
      const expanded = elapsed >= 550;
      figure.classList.toggle('is-expanded', expanded);
      figure.classList.toggle('is-complete', elapsed >= motionEnd);
      visual.style.opacity = Math.max(0, Math.min(1, (elapsed - 550) / 1200));

      const fraction = Math.max(0, Math.min(1, (elapsed - expansionEnd) / (motionEnd - expansionEnd)));
      const [w1, w2, a1, ak] = initial.map((start, i) => start + fraction * (target[i] - start));
      [w1, w2, a1, ak].forEach((value, i) => { values[i].textContent = value.toFixed(2); });

      [0.55, 0.9, 1.25, 1.6].forEach((level, i) => {
        contours[i].setAttribute('rx', 78 * level / Math.sqrt(w1));
        contours[i].setAttribute('ry', 78 * level / Math.sqrt(w2));
      });

      const angle = 0.18 + 0.28 * (ak - a1);
      const nx = Math.cos(angle);
      const ny = Math.sin(angle);
      const offset = 0.48 + 0.22 * (a1 + ak);
      const tx = -ny;
      const ty = nx;
      const p0 = point(offset * nx - 2.25 * tx, offset * ny - 2.25 * ty);
      const p1 = point(offset * nx + 2.25 * tx, offset * ny + 2.25 * ty);
      const p2 = point(offset * nx + 2.25 * tx + 3.2 * nx, offset * ny + 2.25 * ty + 3.2 * ny);
      const p3 = point(offset * nx - 2.25 * tx + 3.2 * nx, offset * ny - 2.25 * ty + 3.2 * ny);
      region.setAttribute('points', [p0, p1, p2, p3].map((p) => p.join(',')).join(' '));
      boundary.setAttribute('x1', p0[0]);
      boundary.setAttribute('y1', p0[1]);
      boundary.setAttribute('x2', p1[0]);
      boundary.setAttribute('y2', p1[1]);

      const inverseNormal = [nx / w1, ny / w2];
      const scale = (offset - (-0.82 * nx + 0.30 * ny)) / (nx * inverseNormal[0] + ny * inverseNormal[1]);
      const safe = point(-0.82 + scale * inverseNormal[0], 0.30 + scale * inverseNormal[1]);
      optimum.setAttribute('cx', safe[0]);
      optimum.setAttribute('cy', safe[1]);
      optimumLabel.setAttribute('x', safe[0] + 14);
      optimumLabel.setAttribute('y', safe[1] - 10);
      projection.setAttribute('x1', 242);
      projection.setAttribute('y1', 265);
      projection.setAttribute('x2', safe[0] - 16);
      projection.setAttribute('y2', safe[1] + (safe[1] - 265) * 0.06);
    }

    function tick(time) {
      if (lastTime !== null) elapsed = Math.min(total, elapsed + time - lastTime);
      lastTime = time;
      render();
      if (elapsed < total) {
        frame = requestAnimationFrame(tick);
      } else {
        playing = false;
        lastTime = null;
        button.textContent = 'Replay animation';
        button.setAttribute('aria-label', 'Replay differentiable QP animation');
      }
    }

    button.addEventListener('click', () => {
      if (playing) {
        cancelAnimationFrame(frame);
        playing = false;
        lastTime = null;
        button.textContent = 'Resume animation';
        button.setAttribute('aria-label', 'Resume differentiable QP animation');
        return;
      }
      if (elapsed === total) elapsed = 0;
      playing = true;
      lastTime = null;
      render();
      button.textContent = 'Pause animation';
      button.setAttribute('aria-label', 'Pause differentiable QP animation');
      frame = requestAnimationFrame(tick);
    });

    render();
  })();
</script>

<style>
  .cbf-static {
    --static-text: #202428;
    --static-muted: #626b73;
    --static-line: #747b82;
    --static-blue: #087eaa;
    --static-gold: #a76814;
    --static-green: #3e7929;
    --static-red: #b9443e;
    --static-teal: #168477;
    --static-box: #f7f9fa;
    --static-teal-box: #e7f5f2;
    --static-blue-box: #e8f5fa;
    --static-red-box: #fff0ee;
    --static-gold-box: #fff4e5;
    max-width: 1100px;
    margin: 3rem auto 1.5rem;
    color: var(--static-text);
  }

  html[data-theme="dark"] .cbf-static {
    --static-text: #f5f7f8;
    --static-muted: #c3cbd0;
    --static-line: #aab2b8;
    --static-blue: #71c9e9;
    --static-gold: #f2b96e;
    --static-green: #a0ce86;
    --static-red: #ff7770;
    --static-teal: #75d7c5;
    --static-box: #292f32;
    --static-teal-box: #18332f;
    --static-blue-box: #162f38;
    --static-red-box: #38221f;
    --static-gold-box: #382b1d;
  }

  .cbf-static h2 {
    margin: 0 0 1.2rem;
    color: var(--static-text);
    text-align: center;
    font-size: clamp(1.6rem, 3.4vw, 2.6rem);
  }
  .cbf-static h3 {
    margin: 0;
    color: var(--static-text);
    text-align: center;
    font-size: clamp(1.2rem, 2.6vw, 1.9rem);
  }
  .cbf-static svg {
    display: block;
    width: 100%;
    height: auto;
    font-family: Arial, Helvetica, sans-serif;
  }
  .cbf-static .static-text { fill: var(--static-text); }
  .cbf-static .static-muted { fill: var(--static-muted); }
  .cbf-static .static-blue { fill: var(--static-blue); }
  .cbf-static .static-gold { fill: var(--static-gold); }
  .cbf-static .static-green { fill: var(--static-green); }
  .cbf-static .static-red { fill: var(--static-red); }
  .cbf-static .static-teal { fill: var(--static-teal); }
  .cbf-static .static-line { stroke: var(--static-line); }
  .cbf-static .static-blue-line { stroke: var(--static-blue); }
  .cbf-static .static-gold-line { stroke: var(--static-gold); }
  .cbf-static .static-green-line { stroke: var(--static-green); }
  .cbf-static .static-red-line { stroke: var(--static-red); }
  .cbf-static .static-teal-line { stroke: var(--static-teal); }
  .cbf-static .static-box { fill: var(--static-box); stroke: var(--static-line); }
  .cbf-static .static-blue-box { fill: var(--static-blue-box); stroke: var(--static-blue); }
  .cbf-static .static-red-box { fill: var(--static-red-box); stroke: var(--static-red); }
  .cbf-static .static-gold-box { fill: var(--static-gold-box); stroke: var(--static-gold); }
  .cbf-static .static-teal-box { fill: var(--static-teal-box); stroke: var(--static-teal); }
  .cbf-static .static-node { fill: var(--static-box); stroke: var(--static-red); }

  .cbf-architecture .architecture-main {
    max-width: 960px;
    margin: 0 auto;
  }
  .cbf-architecture .architecture-main > svg { max-width: 900px; margin: 0 auto; }
  .cbf-architecture .architecture-math {
    margin: 0.5rem auto 1.5rem;
    overflow-x: auto;
    font-size: clamp(0.95rem, 1.9vw, 1.2rem);
    line-height: 1.9;
    text-align: center;
  }
  .cbf-architecture .architecture-math p { margin: 0.35rem 0; white-space: nowrap; }
  .cbf-architecture .architecture-bottom {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
    align-items: center;
    margin-top: 1rem;
  }
  .cbf-architecture .architecture-bottom > div { padding: 0.5rem 1rem; }
  .cbf-architecture .architecture-bottom > div + div {
    border-left: 2px solid var(--static-line);
    text-align: center;
    font-size: clamp(1rem, 2vw, 1.4rem);
    font-weight: 700;
  }
  .cbf-architecture .architecture-bottom p { margin: 0.25rem 0; }
  .cbf-static figcaption { padding: 0.6rem 0.75rem; color: var(--static-muted); }
  @media (max-width: 800px) {
    .cbf-architecture .architecture-bottom { grid-template-columns: 1fr; }
    .cbf-architecture .architecture-bottom > div + div { border-left: 0; border-top: 2px solid var(--static-line); }
  }
</style>

<figure class="cbf-static cbf-architecture">
  <h2>Differentiable CBF-QP Architecture</h2>
  <div class="architecture-main">
    <svg viewBox="0 0 900 480" role="img" aria-labelledby="cbf-arch-title cbf-arch-desc">
      <title id="cbf-arch-title">Network predicts the parameters of a structured CBF-QP</title>
      <desc id="cbf-arch-desc">Obstacles enter a scene encoder. Its embedding joins the robot state, nominal control, and goal. A neural network predicts control weights, barrier strengths, and an affine correction term.</desc>
      <defs>
        <marker id="cbf-arch-arrow" markerWidth="10" markerHeight="10" refX="9" refY="5" orient="auto" markerUnits="userSpaceOnUse"><path class="static-muted" d="M0 0 L10 5 L0 10 Z" /></marker>
        <marker id="cbf-arch-blue-arrow" markerWidth="10" markerHeight="10" refX="9" refY="5" orient="auto" markerUnits="userSpaceOnUse"><path class="static-blue" d="M0 0 L10 5 L0 10 Z" /></marker>
        <marker id="cbf-arch-gold-arrow" markerWidth="10" markerHeight="10" refX="9" refY="5" orient="auto" markerUnits="userSpaceOnUse"><path class="static-gold" d="M0 0 L10 5 L0 10 Z" /></marker>
        <marker id="cbf-arch-green-arrow" markerWidth="10" markerHeight="10" refX="9" refY="5" orient="auto" markerUnits="userSpaceOnUse"><path class="static-green" d="M0 0 L10 5 L0 10 Z" /></marker>
      </defs>
      <text class="static-muted" x="88" y="36" font-size="20" text-anchor="middle">Observation</text>
      <g stroke-width="2.5">
        <rect class="static-box" x="10" y="55" width="155" height="55" rx="8" />
        <rect class="static-box" x="10" y="158" width="155" height="55" rx="8" />
        <rect class="static-box" x="10" y="261" width="155" height="55" rx="8" />
        <rect class="static-box" x="10" y="364" width="155" height="55" rx="8" />
        <path class="static-teal-box" d="M210 65 L350 130 Q360 135 360 145 L360 210 Q360 220 350 225 L210 290 Q200 292 200 280 L200 75 Q200 63 210 65 Z" />
        <circle class="static-box" cx="456" cy="239" r="26" />
        <rect class="static-box" x="525" y="100" width="190" height="270" rx="20" />
      </g>
      <g class="static-text" font-size="20" text-anchor="middle">
        <text x="87" y="89">Obstacles</text><text x="87" y="192">Robot state</text>
        <text x="87" y="295">Nominal control</text><text x="87" y="398">Goal</text>
        <text x="278" y="171">Scene</text><text x="278" y="196">Encoder</text>
        <text x="456" y="246" font-size="28">∥</text>
      </g>
      <text class="static-muted" x="456" y="287" font-size="17" text-anchor="middle">Concatenate</text>
      <text class="static-muted" x="620" y="90" font-size="21" text-anchor="middle">MLP</text>
      <g fill="none" stroke-width="2.5" marker-end="url(#cbf-arch-arrow)">
        <path class="static-line" d="M165 82 H195" />
        <path class="static-line" d="M165 185 H180 V310 H385 V216 H425" />
        <path class="static-line" d="M165 288 H170 V335 H398 V239 H425" />
        <path class="static-line" d="M165 391 H410 V259 H425" />
        <path class="static-line" d="M482 239 H518" />
      </g>
      <path class="static-teal-line" d="M360 177 H430 V208" fill="none" stroke-width="2.5" marker-end="url(#cbf-arch-arrow)" />
      <text class="static-teal" x="394" y="137" font-size="16" text-anchor="middle">Scene</text>
      <text class="static-teal" x="394" y="156" font-size="16" text-anchor="middle">embedding</text>
      <g class="static-line" fill="none" stroke-width="1.3">
        <path d="M552 155 L620 135 M552 155 L620 195 M552 155 L620 255 M552 155 L620 315 M552 235 L620 135 M552 235 L620 195 M552 235 L620 255 M552 235 L620 315 M552 315 L620 135 M552 315 L620 195 M552 315 L620 255 M552 315 L620 315" />
        <path d="M620 135 L688 155 M620 135 L688 235 M620 135 L688 315 M620 195 L688 155 M620 195 L688 235 M620 195 L688 315 M620 255 L688 155 M620 255 L688 235 M620 255 L688 315 M620 315 L688 155 M620 315 L688 235 M620 315 L688 315" />
      </g>
      <g class="static-box" stroke-width="2">
        <circle cx="552" cy="155" r="12" /><circle cx="552" cy="235" r="12" /><circle cx="552" cy="315" r="12" />
        <circle cx="620" cy="135" r="12" /><circle cx="620" cy="195" r="12" /><circle cx="620" cy="255" r="12" /><circle cx="620" cy="315" r="12" />
        <circle cx="688" cy="155" r="12" /><circle cx="688" cy="235" r="12" /><circle cx="688" cy="315" r="12" />
      </g>
      <path class="static-blue-line" d="M702 155 H770" fill="none" stroke-width="3" marker-end="url(#cbf-arch-blue-arrow)" />
      <path class="static-green-line" d="M702 235 H770" fill="none" stroke-width="3" marker-end="url(#cbf-arch-green-arrow)" />
      <path class="static-gold-line" d="M702 315 H770" fill="none" stroke-width="3" marker-end="url(#cbf-arch-gold-arrow)" />
      <text class="static-blue" x="795" y="162" font-size="25">Hθ</text>
      <text class="static-green" x="795" y="242" font-size="25">qθ</text>
      <text class="static-gold" x="795" y="322" font-size="25">αθ</text>
    </svg>
    <div class="architecture-math">
      <p>\(u^*=\arg\min_u\ \tfrac12(u-u_{\rm ref})^\top\) <span style="color: var(--static-blue)">\(H_\theta\)</span> \((u-u_{\rm ref})+\) <span style="color: var(--static-green)">\(q_\theta^\top u\)</span></p>
      <p>\(\mathrm{s.t.}\quad L_fh_i(x)+L_gh_i(x)u\ge-\) <span style="color: var(--static-gold)">\(\alpha_\theta\)</span> \((h_i(x)),\ i=1,\ldots,k\)</p>
      <p>\(u_{\min}\le u\le u_{\max}\)</p>
    </div>
  </div>
  <div class="architecture-bottom">
    <div>
      <strong>Network Predicts:</strong>
      <p>a) Control weight matrix entries</p>
      <p>b) Alpha values per obstacle</p>
      <p>c) Affine correction term</p>
    </div>
    <div>Combine model-based constraints<br />with the expressivity of<br />neural networks</div>
  </div>
  <figcaption>The network supplies adaptive parameters while the QP retains model-based safety constraints.</figcaption>
</figure>

<figure class="cbf-static cbf-learning">
  <h2>Learning State-Dependent CBF-QP Parameters</h2>
  <h3>Imitating an Expensive Planner</h3>
  <svg viewBox="0 0 1200 730" role="img" aria-labelledby="cbf-learning-title cbf-learning-desc">
    <title id="cbf-learning-title">Imitation learning for state-dependent CBF-QP parameters</title>
    <desc id="cbf-learning-desc">A global planner sends actions to a fast CBF-QP controller. An imitation loss compares the controller with a teacher planner and training trajectory. The loss trains a neural network whose parameters feed the differentiable QP.</desc>
    <defs>
      <marker id="cbf-learning-blue-arrow" markerWidth="13" markerHeight="13" refX="11" refY="6.5" orient="auto" markerUnits="userSpaceOnUse"><path class="static-blue" d="M0 0 L13 6.5 L0 13 Z" /></marker>
      <marker id="cbf-learning-red-arrow" markerWidth="13" markerHeight="13" refX="11" refY="6.5" orient="auto" markerUnits="userSpaceOnUse"><path class="static-red" d="M0 0 L13 6.5 L0 13 Z" /></marker>
      <marker id="cbf-learning-gold-arrow" markerWidth="13" markerHeight="13" refX="11" refY="6.5" orient="auto" markerUnits="userSpaceOnUse"><path class="static-gold" d="M0 0 L13 6.5 L0 13 Z" /></marker>
    </defs>
    <text class="static-muted" x="150" y="122" font-size="25" text-anchor="middle">Online (~1 Hz)</text>
    <text class="static-muted" x="472" y="122" font-size="25" text-anchor="middle">Controller (~100 Hz)</text>
    <g stroke-width="3">
      <rect class="static-blue-box" x="30" y="145" width="240" height="100" rx="17" />
      <rect class="static-blue-box" x="352" y="145" width="240" height="100" rx="17" />
      <rect class="static-red-box" x="815" y="145" width="245" height="100" rx="17" />
      <rect class="static-gold-box" x="829" y="365" width="217" height="100" rx="17" />
      <rect class="static-teal-box" x="280" y="300" width="460" height="145" rx="17" />
      <rect class="static-teal-box" x="375" y="520" width="270" height="140" rx="17" />
    </g>
    <g class="static-text" font-size="28" text-anchor="middle">
      <text x="150" y="189">Global</text><text x="150" y="222">Planner</text>
      <text x="472" y="207" font-size="34">CBF-QP</text>
      <text x="937" y="189">Imitation</text><text x="937" y="222">Loss</text>
      <text x="937" y="409">Teacher</text><text x="937" y="442">Planner</text>
    </g>
    <g fill="none" stroke-width="4" marker-end="url(#cbf-learning-blue-arrow)">
      <path class="static-blue-line" d="M270 195 H340" />
      <path class="static-blue-line" d="M592 195 H800" />
      <path class="static-blue-line" d="M510 300 V257" />
      <path class="static-blue-line" d="M1060 195 H1150 V590 H659" />
    </g>
    <path class="static-gold-line" d="M937 365 V258" fill="none" stroke-width="4" marker-end="url(#cbf-learning-gold-arrow)" />
    <text class="static-blue" x="1080" y="567" font-size="27">Train</text>
    <g class="static-text" text-anchor="middle" font-family="Georgia, 'Times New Roman', serif">
      <text x="510" y="357" font-size="27"><tspan font-style="italic">u</tspan>* = arg min ½ <tspan font-style="italic">u</tspan>ᵀ <tspan class="static-blue">Hθ(x)</tspan> <tspan font-style="italic">u</tspan> + <tspan class="static-red">pθ(x)</tspan>ᵀ <tspan font-style="italic">u</tspan></text>
      <text x="510" y="407" font-size="27">s.t. &nbsp; A(x)u ≤ <tspan class="static-gold">bθ(x)</tspan></text>
    </g>
    <g class="static-red-line" fill="none" stroke-width="1.8">
      <path d="M411 557 L510 546 M411 557 L510 582 M411 557 L510 618 M411 590 L510 546 M411 590 L510 582 M411 590 L510 618 M411 623 L510 546 M411 623 L510 582 M411 623 L510 618 M510 546 L609 557 M510 546 L609 590 M510 546 L609 623 M510 582 L609 557 M510 582 L609 590 M510 582 L609 623 M510 618 L609 557 M510 618 L609 590 M510 618 L609 623" />
    </g>
    <g class="static-node" stroke-width="2.5"><circle cx="411" cy="557" r="10" /><circle cx="411" cy="590" r="10" /><circle cx="411" cy="623" r="10" /><circle cx="510" cy="546" r="10" /><circle cx="510" cy="582" r="10" /><circle cx="510" cy="618" r="10" /><circle cx="609" cy="557" r="10" /><circle cx="609" cy="590" r="10" /><circle cx="609" cy="623" r="10" /></g>
    <path class="static-blue-line" d="M450 520 L470 446" fill="none" stroke-width="3" marker-end="url(#cbf-learning-blue-arrow)" />
    <path class="static-red-line" d="M510 520 L552 446" fill="none" stroke-width="3" marker-end="url(#cbf-learning-red-arrow)" />
    <path class="static-gold-line" d="M570 520 L630 446" fill="none" stroke-width="3" marker-end="url(#cbf-learning-gold-arrow)" />
    <text class="static-teal" x="510" y="700" font-size="27" text-anchor="middle">Learned CBF-QP parameters</text>
    <g transform="translate(840 12)">
      <rect class="static-box" x="0" y="0" width="205" height="104" rx="5" stroke-width="1" />
      <path class="static-line" d="M20 80 H186 M20 80 V15" fill="none" stroke-width="1.2" />
      <path class="static-line" d="M20 72 C55 66 70 43 95 48 S140 64 180 27" fill="none" stroke-width="2.5" />
      <path class="static-red-line" d="M20 71 C52 64 70 38 95 42 S142 51 180 12" fill="none" stroke-width="2.5" />
      <text class="static-muted" x="112" y="96" font-size="14">training and expected trajectories</text>
    </g>
    <path class="static-red-line" d="M942 116 V133" fill="none" stroke-width="3" marker-end="url(#cbf-learning-red-arrow)" />
  </svg>
  <figcaption>A fast learned safety filter imitates a more expensive planner while retaining a differentiable QP structure.</figcaption>
</figure>

<style>
  .cbf-videos {
    max-width: 960px;
    margin: 3rem auto 1.5rem;
  }
  .cbf-videos h2 {
    margin-bottom: 1.5rem;
    text-align: center;
    font-size: clamp(1.6rem, 3.4vw, 2.6rem);
  }
  .cbf-videos figure { margin: 0 0 2.5rem; }
  .cbf-videos h3 { margin: 0 0 0.75rem; }
  .cbf-videos video {
    display: block;
    width: 100%;
    height: auto;
    border-radius: 0.5rem;
    background: #171b1e;
  }
  .cbf-videos figcaption { padding: 0.6rem 0.75rem; }
</style>

<section class="cbf-videos" aria-label="Bimanual robot demonstrations">
  <h2>Bimanual Robot Demonstrations</h2>
  <figure>
    <h3>Simulation</h3>
    <video controls playsinline preload="metadata" poster="{{ '/assets/img/bimanual_simulation_poster.jpg' | relative_url }}">
      <source src="{{ '/assets/video/bimanual_simulation.mp4' | relative_url }}" type="video/mp4" />
      <a href="{{ '/assets/video/bimanual_simulation.mp4' | relative_url }}">Watch the simulation video</a>.
    </video>
    <figcaption>Bimanual simulation.</figcaption>
  </figure>
  <figure>
    <h3>Robot Demonstration</h3>
    <video controls playsinline preload="metadata" poster="{{ '/assets/img/bimanual_eraser_poster.jpg' | relative_url }}">
      <source src="{{ '/assets/video/bimanual_kinova_with_eraser.mp4' | relative_url }}" type="video/mp4" />
      <a href="{{ '/assets/video/bimanual_kinova_with_eraser.mp4' | relative_url }}">Watch the robot demonstration video</a>.
    </video>
    <figcaption>Bimanual Kinova demonstration.</figcaption>
  </figure>
</section>
