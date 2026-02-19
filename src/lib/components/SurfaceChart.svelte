<script>
  const surfaces = [
    {
      id: 'clay',
      label: 'Terra Rossa',
      color: 'var(--clay)',
      career: 59.6,
      recent: 73.7,
      careerLabel: '59.6%',
      recentLabel: '73.7%',
      note: '(ult. 52 sett.)',
    },
    {
      id: 'grass',
      label: 'Erba',
      color: 'var(--grass)',
      career: 56.2,
      recent: 66.7,
      careerLabel: '56.2%',
      recentLabel: '66.7%',
      note: '(ult. 52 sett.)',
    },
    {
      id: 'hard',
      label: 'Cemento',
      color: 'var(--hard)',
      career: 48.6,
      recent: 37.0,
      careerLabel: '48.6%',
      recentLabel: '37.0%',
      note: '(ult. 52 sett.)',
    },
  ];
</script>

<div class="surface-chart">
  <div class="chart-header">
    <span class="chart-label mono">Win Rate per Superficie</span>
  </div>

  <div class="legend">
    <span class="legend-item">
      <span class="dot career-dot"></span>
      <span>Carriera</span>
    </span>
    <span class="legend-item">
      <span class="dot recent-dot"></span>
      <span>Ult. 52 settimane</span>
    </span>
  </div>

  <div class="bars-container">
    {#each surfaces as s}
      <div class="surface-row">
        <div class="row-label">
          <span class="surface-icon" style="background: {s.color}"></span>
          <span class="surface-name">{s.label}</span>
        </div>

        <div class="bars-area">
          <!-- 50% reference line -->
          <div class="ref-line" style="left: 50%"></div>
          <div class="ref-label mono">50%</div>

          <!-- Career bar -->
          <div class="bar-row">
            <div class="bar-track">
              <div
                class="bar career-bar"
                style="width: {s.career}%; background: {s.color}; opacity: 0.35"
              ></div>
              <span class="bar-label career-label mono">{s.careerLabel}</span>
            </div>
          </div>

          <!-- Recent bar (lollipop) -->
          <div class="bar-row">
            <div class="bar-track">
              <div
                class="bar recent-bar"
                style="width: {s.recent}%; background: {s.color}"
              ></div>
              <!-- Lollipop circle -->
              <div
                class="lollipop"
                style="left: calc({s.recent}% - 6px); background: {s.color}; box-shadow: 0 0 8px {s.color}60"
              ></div>
              <span class="bar-label recent-label mono" style="color: {s.color}">{s.recentLabel}</span>
            </div>
          </div>
        </div>
      </div>
    {/each}
  </div>
</div>

<style>
  .surface-chart {
    width: 100%;
    padding: 0 1rem;
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
  }

  .chart-header {
    display: flex;
    align-items: center;
    gap: 0.5rem;
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

  .dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    display: inline-block;
  }

  .career-dot {
    background: var(--text-dim);
    opacity: 0.6;
  }

  .recent-dot {
    background: var(--accent);
  }

  .bars-container {
    display: flex;
    flex-direction: column;
    gap: 2rem;
  }

  .surface-row {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }

  .row-label {
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .surface-icon {
    width: 10px;
    height: 10px;
    border-radius: 2px;
    display: inline-block;
    flex-shrink: 0;
  }

  .surface-name {
    font-size: 0.85rem;
    font-weight: 500;
    color: var(--text);
    letter-spacing: 0.02em;
  }

  .bars-area {
    position: relative;
    padding-top: 0.25rem;
  }

  .ref-line {
    position: absolute;
    top: 0;
    bottom: 0;
    width: 1px;
    background: var(--line);
    border-left: 1px dashed rgba(240, 236, 228, 0.2);
    z-index: 0;
  }

  .ref-label {
    position: absolute;
    top: -1rem;
    left: calc(50% + 4px);
    font-size: 0.65rem;
    color: var(--text-dim);
  }

  .bar-row {
    padding: 3px 0;
  }

  .bar-track {
    position: relative;
    height: 14px;
    background: rgba(240, 236, 228, 0.04);
    border-radius: 2px;
    overflow: visible;
  }

  .bar {
    height: 100%;
    border-radius: 2px;
    transition: width 0.8s cubic-bezier(0.16, 1, 0.3, 1);
    position: relative;
    z-index: 1;
  }

  .lollipop {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    width: 12px;
    height: 12px;
    border-radius: 50%;
    border: 2px solid var(--bg);
    z-index: 2;
  }

  .bar-label {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    font-size: 0.72rem;
    white-space: nowrap;
  }

  .career-label {
    right: -46px;
    color: var(--text-dim);
  }

  .recent-label {
    right: -46px;
    font-weight: 500;
  }
</style>
