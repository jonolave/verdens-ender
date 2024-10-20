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
            console.log("Active index: ", activeIndex);
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

<section class="top-section">
  <!-- Heading -->
  <article>
    <div class="step top-step" data-index="0">
      <div>
        <h1 style="">
          <span style="font-size: 1.5rem; line-height: 1;">Det handler om å få</span>
          <br />
          <span style="font-size: 5rem;line-height: 0.9; letter-spacing: 0.06em">ENDENE</span>
          <br />
          <span style="font-size: 1.5rem; line-height: 1.6;">til å møtes</span>
        </h1>
      </div>
    </div>
  </article>

  <!-- Text box 1 -->
  <article>
    <div class="step top-step" data-index="1">
      <div class="textbox">
        <p>Hvor begynner endene, og hvor ender begynnelsen?</p>
      </div>
    </div>
  </article>

  <!-- Text box 2 and ducks crossing -->
  <article style="margin: 0; width: 100%; box-sizing: border-box;">
    <div class="step top-step" data-index="2">
      <div class="textbox">
        <p>Er det noen ender i nærheten?</p>
      </div>
      <div style="width: 100%; height: 8rem; margin: 12rem 0; position:relative;">
        {#if activeIndex === 2}
          <img src="duck.png" alt="gul plastand" class="crossing-duck" />
          <img src="duck.png" alt="gul plastand" class="crossing-duck second-duck" />
        {/if}
      </div>
    </div>
  </article>
</section>

<section id="scrolly-secion-one" class="scrolly-section">
  <div class="scrolly">
    <!-- Sticky graphic -->
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
      <div class="step" data-index="3">
        <div class="textbox">
          <p>Text box 1</p>
        </div>
      </div>
    </article>

    <!-- Step text -->
    <article>
      <div class="step" data-index="4">
        <div class="textbox">
          <p>Text box 2</p>
        </div>
      </div>
    </article>

    <!-- Step text -->
    <article>
      <div class="step" data-index="5">
        <div class="textbox">
          <p>Text box 3</p>
        </div>
      </div>
    </article>
  </div>
</section>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Bree+Serif&display=swap");

  :root {
    --black-color: #120908;
    --yellow-color: #ffe431;
  }

  /* Top section */
  .top-section {
    /* min-height: 300vh; */
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 32px;
    background: rgb(251, 227, 67);
    background: linear-gradient(
      180deg,
      rgba(251, 227, 67, 1) 0%,
      rgba(254, 185, 2, 1) 33%,
      rgba(227, 119, 95, 1) 60%,
      rgba(122, 66, 135, 1) 90%
    );
  }

  .top-step {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  h1 {
    font-family: "Bree Serif", serif;
    text-align: center;
    font-weight: 400;
    font-style: normal;
    color: var(--black-color);
  }

  .crossing-duck {
    position: absolute;
    right: -5rem;
    width: 5rem;
    height: auto;
    animation:
      duck-crossing 5s linear 1s infinite,
      duck-waggle 1s ease-in-out infinite;
  }

  .crossing-duck.second-duck {
    top: 2em;
    animation-delay: 3.5s;
  }

  @media (min-width: 1024px) {
    .crossing-duck {
      animation:
        duck-crossing 10s linear 1s infinite,
        duck-waggle 1s ease-in-out infinite;
    }


  }

  

  @keyframes duck-crossing {
    0% {
      right: -5rem;
    }
    100% {
      right: 100%;
    }
  }

  @keyframes duck-waggle {
    0%,
    100% {
      transform: rotate(0deg);
    }
    25% {
      transform: rotate(-5deg);
    }
    75% {
      transform: rotate(5deg);
    }
  }

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
    min-height: 100vh;
  }

  .textbox {
    background-color: var(--black-color);
    padding: 1rem 2rem;
    max-width: 300px;
    margin: 0 auto;
    color: var(--yellow-color);
    border-radius: 10px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
  }

  .step p {
    font-size: 1.5rem;
    text-align: center;
  }

  /* Ensure there's enough space between elements */
  article {
    padding: 0;
  }

  /* Responsive adjustments */
  @media (max-width: 768px) {
    .step {
      min-height: 70vh;
    }
  }
</style>
