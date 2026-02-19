<script>
  const events = [
    {
      month: 'Maggio',
      year: '2025',
      title: 'Titolo Amburgo',
      desc: 'Primo titolo ATP 500. Batte Zverev in finale sulla terra rossa.',
      color: 'var(--clay)',
      tag: 'CLAY · ATP 500',
      rank: '#34 → #30',
    },
    {
      month: 'Giugno',
      year: '2025',
      title: 'Roland Garros — Terzo Turno',
      desc: 'Migliore risultato in uno Slam sulla terra. Sconfitto da Alcaraz.',
      color: 'var(--clay)',
      tag: 'CLAY · GRAND SLAM',
      rank: null,
    },
    {
      month: 'Luglio',
      year: '2025',
      title: 'Quarti di finale Wimbledon',
      desc: "Prima volta nei quarti di uno Slam. Sull'erba di Londra, il miglior risultato in carriera.",
      color: 'var(--grass)',
      tag: 'GRASS · GRAND SLAM',
      rank: null,
    },
    {
      month: 'Luglio',
      year: '2025',
      title: 'Career High #17',
      desc: 'Raggiunge il 17° posto nel ranking ATP — il massimo della carriera.',
      color: 'var(--accent)',
      tag: 'RANKING MILESTONE',
      rank: '#17',
    },
    {
      month: 'Novembre',
      year: '2025',
      title: 'Davis Cup — Vittoria Italia',
      desc: "Contribuisce al titolo dell'Italia in Coppa Davis. La ciliegina sulla torta di un anno straordinario.",
      color: 'var(--accent)',
      tag: 'TEAM ITALY',
      rank: null,
    },
  ];
</script>

<div class="timeline">
  <div class="chart-header">
    <span class="chart-label mono">2025 — Anno di Svolta</span>
  </div>

  <div class="events">
    {#each events as event, i}
      <div class="event">
        <!-- Left: date -->
        <div class="event-date mono">
          <span class="event-month">{event.month}</span>
          <span class="event-year">{event.year}</span>
        </div>

        <!-- Center: timeline line + dot -->
        <div class="event-spine">
          <div class="spine-line" class:first={i === 0} class:last={i === events.length - 1}></div>
          <div class="spine-dot" style="background: {event.color}; box-shadow: 0 0 10px {event.color}50"></div>
        </div>

        <!-- Right: content -->
        <div class="event-content">
          <span class="event-tag mono" style="color: {event.color}">{event.tag}</span>
          <h4 class="event-title">{event.title}</h4>
          <p class="event-desc">{event.desc}</p>
          {#if event.rank}
            <span class="event-rank mono" style="color: {event.color}">{event.rank}</span>
          {/if}
        </div>
      </div>
    {/each}
  </div>
</div>

<style>
  .timeline {
    width: 100%;
    padding: 0 0.5rem;
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
  }

  .chart-header {
    padding: 0 0.5rem;
  }

  .chart-label {
    font-size: 0.7rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--text-muted);
  }

  .events {
    display: flex;
    flex-direction: column;
  }

  .event {
    display: grid;
    grid-template-columns: 68px 24px 1fr;
    gap: 0 0.75rem;
    min-height: 80px;
  }

  .event-date {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    padding-top: 0.25rem;
  }

  .event-month {
    font-size: 0.72rem;
    color: var(--text);
    font-weight: 500;
    line-height: 1.3;
  }

  .event-year {
    font-size: 0.62rem;
    color: var(--text-dim);
  }

  .event-spine {
    display: flex;
    flex-direction: column;
    align-items: center;
    position: relative;
  }

  .spine-line {
    width: 1px;
    flex: 1;
    background: var(--line);
    min-height: 8px;
  }

  .spine-line.first {
    background: transparent;
    min-height: 6px;
    flex: 0 0 6px;
  }

  .spine-dot {
    width: 10px;
    height: 10px;
    border-radius: 50%;
    border: 2px solid var(--bg);
    flex-shrink: 0;
    z-index: 1;
  }

  .spine-line.last {
    background: linear-gradient(to bottom, var(--line), transparent);
  }

  .event-content {
    padding: 0 0 1.5rem 0;
    padding-top: 0.1rem;
  }

  .event-tag {
    display: block;
    font-size: 0.62rem;
    letter-spacing: 0.1em;
    margin-bottom: 0.3rem;
  }

  .event-title {
    font-family: 'Playfair Display', serif;
    font-size: 1rem;
    font-weight: 700;
    color: var(--text);
    margin-bottom: 0.4rem;
    line-height: 1.3;
  }

  .event-desc {
    font-size: 0.8rem;
    color: var(--text-muted);
    line-height: 1.6;
  }

  .event-rank {
    display: inline-block;
    margin-top: 0.4rem;
    font-size: 0.78rem;
    font-weight: 500;
    letter-spacing: 0.05em;
  }
</style>
