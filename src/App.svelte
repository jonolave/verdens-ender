<script>
  import { onMount } from "svelte";

  // Variable to store the active step index
  let activeIndex = 0;

  let observer;

  function updateChart(index) {
    activeIndex = index;
  }

  onMount(() => {
    observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            // Get the index of the intersecting element
            const index = +entry.target.dataset.index;
            updateChart(index);
          }
        });
      },
      { threshold: 0.5 } // share of element needs to be visible
    );

    // observe all 'step' elements
    document.querySelectorAll(".step").forEach((step) => {
      observer.observe(step);
    });

    return () => observer.disconnect();
  });
</script>

<section class="filler">
  <p>Scroll</p>
</section>

<section id="scrolly-secion-one" class="scrolly-section">
  <div class="scrolly">
    <!-- Sticky graphic (progress bar) -->
    <figure class="sticky">
      {#if activeIndex === 0}
        <p>Background 1</p>
      {:else if activeIndex === 1}
        <p>Background 2</p>
      {:else if activeIndex === 2}
        <p>Background 3</p>
      {/if}
    </figure>

    <!-- Step text -->
    <article>
      <div class="step" data-index="0">
        <div class="textbox">
          <p>Text box 1</p>
        </div>
      </div>
    </article>

    <!-- Step text -->
    <article>
      <div class="step" data-index="1">
        <div class="textbox">
          <p>Text box 2</p>
        </div>
      </div>
    </article>

    <!-- Step text -->
    <article>
      <div class="step" data-index="2">
        <div class="textbox">
          <p>Text box 3</p>
        </div>
      </div>
    </article>
  </div>
</section>

<style>
  /* General styling for first and last section */
  .filler {
    min-height: 300px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #f8f9fa;
  }

  /* Styling for sticky section */
  .scrolly-section {
    position: relative;
    padding: 0;
  }

  /* All section content */
  .scrolly {
    position: relative;
    margin: 0 auto;
  }

  /* Sticky background */
  .sticky {
    position: -webkit-sticky;
    position: sticky;
    width: 100%;
    top: 0;
    height: 100vh;
    z-index: -10;
    background-color: #ffcccccc;
    margin: 0 0 3rem 0;
    padding: 2rem 0 2rem 0;
  }

  /* Step element styling */
  .step {
    min-height: 70vh;
  }

  .textbox {
    background-color: white;
    max-width: 300px;
    margin: 0 auto;
    color: black;
    border-radius: 10px;
    border: 1px solid #dee2e6;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  }

  .step p {
    font-size: 1.5rem;
    text-align: center;
  }

  /* Ensure there's enough space between elements */
  article {
    padding: 1rem;
  }

  /* Responsive adjustments */
  @media (max-width: 768px) {
    .step {
      min-height: 50vh;
    }
  }
</style>
