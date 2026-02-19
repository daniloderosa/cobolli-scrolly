<script>
  const tiers = [
    {
      label: 'Top 10',
      career: 5.9,
      careerLabel: '5.9%',
      careerNote: '1/17 partite',
      recent: 12.5,
      recentLabel: '12.5%',
      recentNote: '2/16 partite',
    },
    {
      label: 'Top 20',
      career: 29.4,
      careerLabel: '29.4%',
      careerNote: '',
      recent: 28.6,
      recentLabel: '28.6%',
      recentNote: '',
    },
    {
      label: 'Top 50',
      career: null,
      careerLabel: 'n.d.',
      careerNote: '',
      recent: 44.8,
      recentLabel: '44.8%',
      recentNote: '',
    },
  ];
</script>

<div class="opponents-chart">
  <div class="chart-header">
    <span class="chart-label mono">Win Rate vs Avversari</span>
  </div>

  <div class="legend">
    <span class="legend-item">
      <span class="legend-dot gray"></span>
      <span>Carriera</span>
    </span>
    <span class="legend-item">
      <span class="legend-dot yellow"></span>
      <span>Ult. 52 settimane</span>
    </span>
  </div>

  <div class="axis-area">
    <div class="axis-line">
      <div class="axis-ref" style="left: 50%">
        <div class="ref-tick"></div>
        <span class="ref-label mono">50%</span>
      </div>
      <div class="axis-ref" style="left: 0%">
        <div class="ref-tick"></div>
        <span class="ref-label mono">0%</span>
      </div>
      <div class="axis-ref" style="left: 100%">
        <div class="ref-tick"></div>
        <span class="ref-label mono">100%</span>
      </div>
    </div>
  </div>

  <div class="rows">
    {#each tiers as tier}
      <div class="tier-row">
        <div class="tier-label">{tier.label}</div>

        <div class="lollipop-area">
          <!-- 50% reference line -->
          <div class="v-ref"></div>

          <!-- Connecting line between career and recent -->
          {#if tier.career !== null && tier.career !== tier.recent}
            <div
              class="connector"
              style="left: {Math.min(tier.career, tier.recent)}%; width: {Math.abs(tier.recent - tier.career)}%"
            ></div>
          {/if}

          <!-- Career dot -->
          {#if tier.career !== null}
            <div
              class="dot career-dot"
              style="left: {tier.career}%"
              title="Carriera: {tier.careerLabel}"
            >
              <div class="dot-label career-dotlabel mono">{tier.careerLabel}</div>
            </div>
          {:else}
            <div class="dot career-dot nd" style="left: {tier.recent}%">
              <div class="dot-label career-dotlabel mono nd-label">{tier.careerLabel}</div>
            </div>
          {/if}

          <!-- Recent dot -->
          <div
            class="dot recent-dot"
            style="left: {tier.recent}%"
            title="Recente: {tier.recentLabel}"
          >
            <div class="dot-label recent-dotlabel mono">{tier.recentLabel}</div>
          </div>
        </div>
      </div>
    {/each}
  </div>
</div>

<style>
  .opponents-chart {
    width: 100%;
    padding: 0 1rem;
    display: flex;
    flex-direction: column;
    gap: 1.25rem;
  }

  .chart-header {
    display: flex;
    align-items: center;
  }

  .chart-label {
    font-size: 0.7rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--text-muted);
  }

  .legend {
    display: flex;
    gap: 1.5rem;
    font-size: 0.78rem;
    color: var(--text-muted);
    font-family: 'IBM Plex Mono', monospace;
  }

  .legend-item {
    display: flex;
    align-items: center;
    gap: 0.4rem;
  }

  .legend-dot {
    width: 10px;
    height: 10px;
    border-radius: 50%;
    display: inline-block;
  }

  .legend-dot.gray {
    background: var(--text-dim);
  }

  .legend-dot.yellow {
    background: var(--accent);
  }

  .axis-area {
    padding: 0 0 0.5rem;
  }

  .axis-line {
    position: relative;
    height: 12px;
    border-bottom: 1px solid var(--line);
  }

  .axis-ref {
    position: absolute;
    bottom: 0;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .ref-tick {
    width: 1px;
    height: 6px;
    background: var(--line);
  }

  .ref-label {
    font-size: 0.62rem;
    color: var(--text-dim);
    position: absolute;
    bottom: -16px;
    transform: translateX(-50%);
    white-space: nowrap;
  }

  .rows {
    display: flex;
    flex-direction: column;
    gap: 2.5rem;
    padding-top: 1.25rem;
  }

  .tier-row {
    display: flex;
    flex-direction: column;
    gap: 0.6rem;
  }

  .tier-label {
    font-size: 0.82rem;
    font-weight: 600;
    color: var(--text);
    letter-spacing: 0.04em;
  }

  .lollipop-area {
    position: relative;
    height: 28px;
  }

  .v-ref {
    position: absolute;
    left: 50%;
    top: 0;
    bottom: 0;
    width: 1px;
    border-left: 1px dashed rgba(240, 236, 228, 0.15);
  }

  .connector {
    position: absolute;
    top: 50%;
    height: 2px;
    background: rgba(240, 236, 228, 0.1);
    transform: translateY(-50%);
  }

  .dot {
    position: absolute;
    top: 50%;
    transform: translate(-50%, -50%);
    width: 12px;
    height: 12px;
    border-radius: 50%;
    cursor: default;
  }

  .career-dot {
    background: var(--text-dim);
  }

  .career-dot.nd {
    background: transparent;
    border: 1px dashed var(--text-dim);
    transform: translate(-50%, -50%);
  }

  .nd-label {
    color: var(--text-dim);
    top: -28px;
  }

  .recent-dot {
    width: 14px;
    height: 14px;
    background: var(--accent);
    box-shadow: 0 0 10px rgba(232, 197, 71, 0.4);
  }

  .dot-label {
    position: absolute;
    top: 18px;
    font-size: 0.68rem;
    white-space: nowrap;
  }

  .career-dotlabel {
    color: var(--text-dim);
    left: 50%;
    transform: translateX(-50%);
  }

  .recent-dotlabel {
    color: var(--accent);
    left: 50%;
    transform: translateX(-50%);
  }
</style>
