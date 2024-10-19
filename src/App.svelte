<script>
  import { onMount } from "svelte";

  let steps = [
    { index: 0, width: "10%", text: "Text 1" },
    { index: 1, width: "90%", text: "Bar is 90%" },
    { index: 2, width: "50%", text: "Bar is 50%" },
  ];

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
            const index = +entry.target.dataset.index;
            updateChart(index);
          }
        });
      },
      { threshold: 0.5 }
    );

    document.querySelectorAll(".step").forEach((step) => {
      observer.observe(step);
    });

    return () => observer.disconnect();
  });
</script>

<section class="filler">
  <p>Scroll</p>
</section>

<section id="scrolly-overlay">
  <div class="scrolly">
    <!-- Sticky graphic (progress bar) -->
    <figure class="sticky">
      <div class="bar-outer">
        <div class="bar-inner" style="width: {steps[activeIndex].width};"></div>
      </div>
      <p>This is the sticky background</p>
      <p>With textbox {activeIndex + 1}</p>
    </figure>

    <!-- Step text -->
    <article>
      {#each steps as step (step.index)}
        <div class="step" data-index={step.index}>
          <div class="textbox {activeIndex === step.index ? 'is-active' : ''}">
            <p>{step.text}</p>
          </div>
        </div>
      {/each}
    </article>
  </div>
</section>

<section class="filler">
  <p>End</p>
</section>

<style>
  /* General styling for first and last section */
  .filler {
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #f8f9fa;
  }

  /* Styling for sticky element */
  #scrolly-overlay {
    position: relative;
    padding: 2rem 0;
  }

  .scrolly {
    position: relative;
    margin: 0 auto;
  }

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

  /* Progress bar styling */
  .bar-outer {
    width: 100%;
    height: 5px;
    background-color: #ddd;
    position: relative;
  }

  .bar-inner {
    height: 100%;
    background-color: #007bff;
    width: 0; /* This will be updated dynamically */
    transition: width 250ms ease-in-out;
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

  /* Add when active */
  .textbox.is-active {
    background-color: #007bff;
    color: white;
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

    .bar-outer {
      height: 4px;
    }
  }
</style>
