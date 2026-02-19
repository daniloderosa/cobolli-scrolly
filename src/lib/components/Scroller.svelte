<script>
  import { onMount } from 'svelte';

  /**
   * @type {{ steps: Array<{title: string, body: string}>, chart: import('svelte').Snippet, activeStep: number }}
   */
  let { steps = [], chart, activeStep = $bindable(0) } = $props();

  /** @type {HTMLElement[]} */
  let stepEls = $state([]);

  onMount(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            const idx = Number(entry.target.dataset.step);
            activeStep = idx;
          }
        });
      },
      { rootMargin: '-35% 0px -35% 0px', threshold: 0 }
    );

    stepEls.forEach((el) => {
      if (el) observer.observe(el);
    });

    return () => observer.disconnect();
  });
</script>

<div class="scroller">
  <div class="sticky-panel">
    <div class="chart-wrap">
      {@render chart?.()}
    </div>
  </div>

  <div class="steps-panel">
    {#each steps as step, i}
      <div
        class="step"
        class:active={activeStep === i}
        data-step={i}
        bind:this={stepEls[i]}
      >
        <div class="step-card">
          <span class="step-num mono">0{i + 1}</span>
          <h3 class="step-title">{step.title}</h3>
          <p class="step-body">{step.body}</p>
        </div>
      </div>
    {/each}
    <!-- Spacer at end -->
    <div class="spacer"></div>
  </div>
</div>

<style>
  .scroller {
    position: relative;
    display: flex;
    align-items: flex-start;
    width: 100%;
  }

  .sticky-panel {
    position: sticky;
    top: 0;
    width: 55%;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
  }

  .chart-wrap {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 2rem;
  }

  .steps-panel {
    width: 45%;
    padding: 0 2rem 0 1rem;
    padding-top: 20vh;
  }

  .step {
    min-height: 85vh;
    display: flex;
    align-items: center;
    padding: 2rem 0;
  }

  .step-card {
    background: rgba(10, 10, 10, 0.7);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    border: 1px solid var(--line);
    border-left: 3px solid var(--accent);
    padding: 1.75rem 1.5rem;
    border-radius: 2px;
    opacity: 0.35;
    transition: opacity 0.4s ease, border-left-color 0.4s ease, transform 0.4s ease;
    transform: translateX(8px);
  }

  .step.active .step-card {
    opacity: 1;
    transform: translateX(0);
  }

  .step-num {
    display: block;
    font-size: 0.7rem;
    letter-spacing: 0.12em;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 0.75rem;
  }

  .step-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(1.1rem, 2vw, 1.4rem);
    font-weight: 700;
    color: var(--text);
    margin-bottom: 0.75rem;
    line-height: 1.25;
  }

  .step-body {
    font-size: 0.92rem;
    color: var(--text-muted);
    line-height: 1.7;
  }

  .spacer {
    height: 40vh;
  }

  @media (max-width: 768px) {
    .scroller {
      flex-direction: column;
    }

    .sticky-panel {
      position: sticky;
      top: 0;
      width: 100%;
      height: 50vh;
      z-index: 10;
    }

    .steps-panel {
      width: 100%;
      padding: 1rem;
      padding-top: 2rem;
    }

    .step {
      min-height: 60vh;
    }
  }
</style>
