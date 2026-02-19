<script>
  import Scroller from '$lib/components/Scroller.svelte';
  import RankingChart from '$lib/components/RankingChart.svelte';
  import SurfaceChart from '$lib/components/SurfaceChart.svelte';
  import OpponentsChart from '$lib/components/OpponentsChart.svelte';
  import Timeline from '$lib/components/Timeline.svelte';

  let activeStep = $state(0);

  const steps = [
    {
      title: 'Da Subiaco al top 20 del mondo',
      body: 'Nato a Roma nel 2002, Flavio Cobolli ha bruciato le tappe. Dal ranking #480 del 2021 al #17 del luglio 2025: quattro anni di scalata inesorabile, fatta di sacrifici, clay e qualche nottata insonne.',
    },
    {
      title: 'La terra rossa è il suo regno',
      body: "Nell'ultimo anno il dato è inequivocabile: 73.7% di vittorie sulla terra rossa. Nessun italiano in attività va così forte su questa superficie. Il backhand piatto e la corsa felina lo rendono letale su ogni campo in mattone.",
    },
    {
      title: 'Il muro dei grandi avversari',
      body: "Solo 1 vittoria su 17 contro i Top 10 in carriera. Un dato che racconta i margini ancora da colmare. Ma nelle ultime 52 settimane, il tasso sale: 2/16, 12.5%. La direzione è giusta.",
    },
    {
      title: 'Il 2025: tutto è cambiato',
      body: "Titolo ad Amburgo (ATP 500), quarti di finale a Wimbledon, career high #17, Davis Cup con l'Italia. Un anno che ha ridefinito il perimetro delle ambizioni di Cobbo. Il 2026 inizia con un giocatore diverso.",
    },
  ];

  const finalStats = [
    { value: '#17', label: 'Career High', color: 'var(--accent)' },
    { value: '2', label: 'Titoli ATP 2025', color: 'var(--accent)' },
    { value: 'QF', label: 'Wimbledon 2025', color: 'var(--grass)' },
    { value: '🏆', label: 'Davis Cup', color: 'var(--accent)' },
  ];
</script>

<svelte:head>
  <title>L'ascesa di Cobbo — Flavio Cobolli</title>
  <meta name="description" content="L'ascesa di Flavio Cobolli nel tennis mondiale. Da #480 a #17 nel ranking ATP." />
</svelte:head>

<!-- ═══════════════════════════════════════ HERO ═══════════════════════════════════════ -->
<section class="hero">
  <!-- Decorative grid -->
  <div class="grid-overlay" aria-hidden="true">
    {#each Array(8) as _, i}
      <div class="grid-col"></div>
    {/each}
    {#each Array(6) as _, i}
      <div class="grid-row"></div>
    {/each}
  </div>

  <div class="hero-content">
    <div class="hero-eyebrow mono">
      <span class="dot-accent"></span>
      <span>Flavio Cobolli · Tennis · 2021–2025</span>
    </div>

    <h1 class="hero-title">
      <span class="title-normal">L'ascesa</span>
      <br />
      <span class="title-italic accent-text">di Cobbo</span>
    </h1>

    <p class="hero-sub">
      Dal ranking #480 al top 20 del mondo.<br />
      Come un ragazzo di Subiaco ha conquistato i campi di tutto il mondo.
    </p>

    <div class="scroll-hint" aria-label="Scorri per scoprire">
      <div class="scroll-line"></div>
      <span class="mono">Scorri</span>
    </div>
  </div>

  <div class="hero-stats mono">
    <div class="hstat">
      <span class="hstat-val">#480</span>
      <span class="hstat-label">Ranking gen 2021</span>
    </div>
    <div class="hstat-sep">→</div>
    <div class="hstat">
      <span class="hstat-val accent-text">#17</span>
      <span class="hstat-label">Career High lug 2025</span>
    </div>
  </div>
</section>

<!-- ═══════════════════════════════════ SCROLLYTELLING ═══════════════════════════════════ -->
<section class="story-section">
  <Scroller bind:activeStep {steps}>
    {#snippet chart()}
      <div class="chart-transition-wrap">
        <div class="chart-panel" class:visible={activeStep === 0}>
          <RankingChart />
        </div>
        <div class="chart-panel" class:visible={activeStep === 1}>
          <SurfaceChart />
        </div>
        <div class="chart-panel" class:visible={activeStep === 2}>
          <OpponentsChart />
        </div>
        <div class="chart-panel" class:visible={activeStep === 3}>
          <Timeline />
        </div>
      </div>
    {/snippet}
  </Scroller>
</section>

<!-- ═══════════════════════════════════════ OUTRO ═══════════════════════════════════════ -->
<section class="outro">
  <div class="outro-inner">
    <p class="outro-label mono">
      <span class="dot-accent"></span>
      I numeri del 2025
    </p>
    <h2 class="outro-title">Un anno che resterà</h2>

    <div class="stats-grid">
      {#each finalStats as stat}
        <div class="stat-card">
          <span class="stat-val" style="color: {stat.color}">{stat.value}</span>
          <span class="stat-label mono">{stat.label}</span>
        </div>
      {/each}
    </div>

    <p class="outro-closing">
      Flavio Cobolli ha 23 anni. Il meglio deve ancora venire.
    </p>
  </div>
</section>

<style>
  /* ─── HERO ────────────────────────────────── */
  .hero {
    position: relative;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    padding: clamp(2rem, 8vw, 6rem);
    overflow: hidden;
  }

  .grid-overlay {
    position: absolute;
    inset: 0;
    pointer-events: none;
    z-index: 0;
  }

  .grid-col {
    position: absolute;
    top: 0;
    bottom: 0;
    width: 1px;
    background: var(--line);
  }

  .grid-col:nth-child(1) { left: 12.5%; }
  .grid-col:nth-child(2) { left: 25%; }
  .grid-col:nth-child(3) { left: 37.5%; }
  .grid-col:nth-child(4) { left: 50%; }
  .grid-col:nth-child(5) { left: 62.5%; }
  .grid-col:nth-child(6) { left: 75%; }
  .grid-col:nth-child(7) { left: 87.5%; }
  .grid-col:nth-child(8) { left: 100%; }

  .grid-row {
    position: absolute;
    left: 0;
    right: 0;
    height: 1px;
    background: var(--line);
  }

  .grid-row:nth-child(9)  { top: 16.6%; }
  .grid-row:nth-child(10) { top: 33.3%; }
  .grid-row:nth-child(11) { top: 50%; }
  .grid-row:nth-child(12) { top: 66.6%; }
  .grid-row:nth-child(13) { top: 83.3%; }
  .grid-row:nth-child(14) { top: 100%; }

  .hero-content {
    position: relative;
    z-index: 1;
    max-width: 680px;
  }

  .hero-eyebrow {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 0.72rem;
    letter-spacing: 0.12em;
    color: var(--text-muted);
    text-transform: uppercase;
    margin-bottom: 1.5rem;
  }

  .dot-accent {
    display: inline-block;
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: var(--accent);
  }

  .hero-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2.33rem, 10vw, 5rem);
    font-weight: 900;
    line-height: 0.95;
    margin-bottom: 1.5rem;
    letter-spacing: -0.02em;
  }

  .title-normal {
    color: var(--text);
    display: block;
  }

  .title-italic {
    font-style: italic;
    display: block;
  }

  .accent-text {
    color: var(--accent);
  }

  .hero-sub {
    font-size: clamp(0.95rem, 2vw, 1.1rem);
    color: var(--text-muted);
    line-height: 1.7;
    max-width: 480px;
    margin-bottom: 3rem;
  }

  .scroll-hint {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 0.5rem;
    font-size: 0.72rem;
    letter-spacing: 0.1em;
    color: var(--text-dim);
    text-transform: uppercase;
  }

  .scroll-line {
    width: 1px;
    height: 40px;
    background: linear-gradient(to bottom, var(--accent), transparent);
    animation: scrollPulse 2s ease-in-out infinite;
  }

  @keyframes scrollPulse {
    0%, 100% { opacity: 0.4; transform: scaleY(1); }
    50% { opacity: 1; transform: scaleY(1.2); transform-origin: top; }
  }

  .hero-stats {
    position: relative;
    z-index: 1;
    display: flex;
    align-items: center;
    gap: 2rem;
    margin-top: 4rem;
    padding-top: 2rem;
    border-top: 1px solid var(--line);
  }

  .hstat {
    display: flex;
    flex-direction: column;
    gap: 0.25rem;
  }

  .hstat-val {
    font-size: 1.5rem;
    font-weight: 600;
    color: var(--text);
    letter-spacing: -0.02em;
  }

  .hstat-label {
    font-size: 0.68rem;
    color: var(--text-dim);
    letter-spacing: 0.06em;
    text-transform: uppercase;
  }

  .hstat-sep {
    font-size: 1.2rem;
    color: var(--text-dim);
    margin-top: -0.5rem;
  }

  /* ─── STORY SECTION ───────────────────────── */
  .story-section {
    background: var(--bg);
  }

  .chart-transition-wrap {
    position: relative;
    width: 100%;
    height: 100%;
  }

  .chart-panel {
    position: absolute;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.5s ease;
  }

  .chart-panel.visible {
    opacity: 1;
    pointer-events: auto;
  }

  /* ─── OUTRO ───────────────────────────────── */
  .outro {
    padding: clamp(4rem, 10vw, 8rem) clamp(2rem, 8vw, 6rem);
    border-top: 1px solid var(--line);
  }

  .outro-inner {
    max-width: 760px;
  }

  .outro-label {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 0.72rem;
    letter-spacing: 0.12em;
    color: var(--text-muted);
    text-transform: uppercase;
    margin-bottom: 1rem;
  }

  .outro-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(1.33rem, 5vw, 2.33rem);
    font-weight: 700;
    color: var(--text);
    margin-bottom: 3rem;
    line-height: 1.15;
  }

  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 1px;
    background: var(--line);
    border: 1px solid var(--line);
    margin-bottom: 3rem;
  }

  .stat-card {
    background: var(--bg);
    padding: 1.75rem 1.5rem;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }

  .stat-val {
    font-family: 'Playfair Display', serif;
    font-size: clamp(1.33rem, 4vw, 1.87rem);
    font-weight: 700;
    line-height: 1;
  }

  .stat-label {
    font-size: 0.72rem;
    letter-spacing: 0.08em;
    color: var(--text-muted);
    text-transform: uppercase;
  }

  .outro-closing {
    font-family: 'Playfair Display', serif;
    font-size: clamp(1.1rem, 2.5vw, 1.4rem);
    font-style: italic;
    color: var(--text-muted);
    line-height: 1.6;
    border-left: 3px solid var(--accent);
    padding-left: 1.25rem;
  }
</style>
