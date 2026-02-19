<script>
  import { getContext } from 'svelte';

  /** @type {{ annotations: Array<{date: Date, rank: number, label: string, sublabel: string, align?: string}> }} */
  let { annotations = [] } = $props();

  // Access LayerCake context (set by Chart component)
  const lc = /** @type {any} */ (getContext('LayerCake'));
  const xScale = lc?.xScale;
  const yScale = lc?.yScale;
</script>

{#if xScale && yScale}
  {#each annotations as ann}
    {@const cx = $xScale(ann.date)}
    {@const cy = $yScale(ann.rank)}
    {@const align = ann.align ?? 'right'}

    <!-- Vertical dashed line from dot to label -->
    <line
      x1={cx}
      y1={cy}
      x2={cx}
      y2={cy - 36}
      stroke="rgba(232, 197, 71, 0.4)"
      stroke-width="1"
      stroke-dasharray="3,3"
    />

    <!-- Dot -->
    <circle {cx} {cy} r={5} fill="#e8c547" stroke="#0a0a0a" stroke-width="2" />

    <!-- Label background -->
    <rect
      x={align === 'left' ? cx - 130 : cx + 8}
      y={cy - 52}
      width="122"
      height="34"
      fill="rgba(10,10,10,0.85)"
      rx="2"
    />

    <!-- Label text -->
    <text
      x={align === 'left' ? cx - 69 : cx + 69}
      y={cy - 36}
      fill="#f0ece4"
      font-size="10"
      font-family="IBM Plex Sans, sans-serif"
      font-weight="500"
      text-anchor="middle"
      dominant-baseline="middle"
    >{ann.label}</text>
    <text
      x={align === 'left' ? cx - 69 : cx + 69}
      y={cy - 24}
      fill="#e8c547"
      font-size="10"
      font-family="IBM Plex Mono, monospace"
      text-anchor="middle"
      dominant-baseline="middle"
    >{ann.sublabel}</text>
  {/each}
{/if}
