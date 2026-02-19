<script>
  import { Chart, Svg, Area, Spline, Axis, LinearGradient, Points } from 'layerchart';
  import { scaleTime } from 'd3-scale';
  import { curveMonotoneX } from 'd3-shape';
  import { timeYear } from 'd3-time';
  import { timeFormat } from 'd3-time-format';
  import RankingAnnotations from './RankingAnnotations.svelte';

  const data = [
    { date: new Date('2021-01-01'), rank: 480 },
    { date: new Date('2021-06-01'), rank: 360 },
    { date: new Date('2022-01-01'), rank: 230 },
    { date: new Date('2022-06-01'), rank: 170 },
    { date: new Date('2022-12-01'), rank: 138 },
    { date: new Date('2023-03-01'), rank: 115 },
    { date: new Date('2023-09-01'), rank: 92 },
    { date: new Date('2024-01-01'), rank: 75 },
    { date: new Date('2024-04-01'), rank: 60 },
    { date: new Date('2024-07-29'), rank: 48 },
    { date: new Date('2024-10-01'), rank: 44 },
    { date: new Date('2024-12-31'), rank: 36 },
    { date: new Date('2025-02-01'), rank: 33 },
    { date: new Date('2025-05-12'), rank: 34 },
    { date: new Date('2025-06-15'), rank: 27 },
    { date: new Date('2025-07-07'), rank: 17 },
  ];

  const annotations = [
    {
      date: new Date('2024-07-29'),
      rank: 48,
      label: 'Finale Washington',
      sublabel: '#48',
      align: 'left',
    },
    {
      date: new Date('2025-05-12'),
      rank: 34,
      label: 'Titolo Amburgo',
      sublabel: '#34',
      align: 'left',
    },
    {
      date: new Date('2025-07-07'),
      rank: 17,
      label: 'Career High · QF Wimbledon',
      sublabel: '#17',
      align: 'left',
    },
  ];

  const formatYear = timeFormat('%Y');
</script>

<div class="ranking-chart">
  <div class="chart-header">
    <span class="chart-label mono">Ranking ATP</span>
    <span class="chart-note">— asse Y: rank più basso = meglio</span>
  </div>

  <div class="chart-body">
    <Chart
      {data}
      x="date"
      y="rank"
      xScale={scaleTime()}
      yDomain={[0, 500]}
      yReverse={false}
      padding={{ top: 20, right: 16, bottom: 40, left: 52 }}
    >
      <Svg>
        <LinearGradient
          id="rankGrad"
          vertical
          stops={['rgba(232,197,71,0.45)', 'rgba(232,197,71,0.02)']}
        />

        <Area
          fill="url(#rankGrad)"
          curve={curveMonotoneX}
        />

        <Spline
          stroke="#e8c547"
          strokeWidth={2.5}
          curve={curveMonotoneX}
        />

        <Axis
          placement="left"
          ticks={[500, 400, 300, 200, 100, 50, 17]}
          format={(d) => d === 0 ? '' : `#${d}`}
          tickLength={4}
        />

        <Axis
          placement="bottom"
          ticks={{ interval: timeYear.every(1) }}
          format={formatYear}
          tickLength={4}
        />

        <RankingAnnotations {annotations} />
      </Svg>
    </Chart>
  </div>

  <div class="chart-footer mono">
    <span class="stat"><span class="val">#480</span> gen 2021</span>
    <span class="arrow">→</span>
    <span class="stat"><span class="val accent">#17</span> lug 2025</span>
  </div>
</div>

<style>
  .ranking-chart {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }

  .chart-header {
    display: flex;
    align-items: baseline;
    gap: 0.75rem;
    padding: 0 0.5rem;
  }

  .chart-label {
    font-size: 0.7rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--text-muted);
  }

  .chart-note {
    font-size: 0.7rem;
    color: var(--text-dim);
    font-family: 'IBM Plex Mono', monospace;
  }

  .chart-body {
    flex: 1;
    min-height: 0;
    height: 340px;
  }

  /* Override layerchart SVG styles for dark theme */
  .chart-body :global(svg) {
    overflow: visible;
  }

  .chart-body :global(.axis text),
  .chart-body :global(text) {
    fill: var(--text-dim);
    font-family: 'IBM Plex Mono', monospace;
    font-size: 10px;
  }

  .chart-body :global(.axis line),
  .chart-body :global(.axis path),
  .chart-body :global(line.tick),
  .chart-body :global(.rule) {
    stroke: var(--line);
  }

  .chart-body :global(.axis .domain) {
    display: none;
  }

  .chart-footer {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    padding: 0 0.5rem;
    font-size: 0.75rem;
    color: var(--text-muted);
  }

  .val {
    color: var(--text);
    font-weight: 500;
  }

  .accent {
    color: var(--accent) !important;
  }

  .arrow {
    color: var(--text-dim);
  }
</style>
