<script>
  import { onMount } from "svelte";
  import { fade } from "svelte/transition";


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

<!-- First section, no sticky -->
<section class="top-section">
  <!-- Heading -->
  <article>
    <div class="step top-step" data-index="0">
      <div style="display: flex; flex-direction: column; align-items: center;">
        <h1 style="">
          <span style="font-size: 1.5rem; line-height: 1;">Det handler om å få</span>
          <br />
          <span style="font-size: 5rem;line-height: 0.9; letter-spacing: 0.06em">ENDENE</span>
          <br />
          <span style="font-size: 1.5rem; line-height: 1.6;">til å møtes</span>
        </h1>
        <p style="font-size: 1.2rem; margin-top: 5rem;">En scrollehistorie av Jon Olav</p>
        <img src="arrow-down.svg" alt="" class="arrow" />
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

<!-- Sticky section 1 -->
<section class="scrolly-section">
  <div class="scrolly">
    <!-- Sticky graphic -->
    <figure class="sticky">
      <div class="svg-container">
        <img src="andedam.svg" alt="Et vann med ender ved siden av en stein" class="full-width-svg" />
        <div class="overlay-content" style="display: flex; gap: 1rem;">
          <img src="duck.png" alt="gul plastand" class="static-duck" />
          <img src="duck.png" alt="gul plastand" class="static-duck" />
        </div>
      </div>
    </figure>

    <!-- Step text -->
    <article>
      <div class="step" data-index="3">
        <div class="textbox">
          <p>I andedammen vår er det ingen ender på gjestfriheten</p>
        </div>
      </div>
      <div style="height: 40vh;"></div>
    </article>
  </div>
</section>

<!-- Sticky section 2 -->
<section class="scrolly-section">
  <div class="scrolly">
    <!-- Sticky graphic -->
    <figure class="sticky">
      <div class="sticky-background-two">
        {#if activeIndex === 3 || activeIndex === 4}
          <div style="display: flex; justify-content: space-between; align-items: center; width: 60%;">
            <img src="duck.png" alt="gul plastand" class="static-duck big" style="z-index: 2;" />
            <img src="duck.png" alt="gul plastand" class="static-duck big mirror-horizontal" style="z-index: 2;" />
            <img
              src="tau.svg"
              alt="tau mellom ender"
              style=" position: absolute; width: 60%; margin: auto; z-index: 0;"
            />
          </div>
        {:else if activeIndex === 5 || activeIndex === 6 || activeIndex === 7}
          <div
            style="display: flex; flex-direction: column; justify-content: center; align-items: center;"
            transition:fade
          >
            <div
              style="width: 100%; height: 3rem; position:relative; display: flex; justify-content: center; align-items: flex-end; gap: 1rem;"
            >
              {#if activeIndex === 6 || activeIndex === 7}
                <img src="duck.png" alt="gul plastand" class="static-duck" style="width: 5rem" transition:fade />
                <img src="duck.png" alt="gul plastand" class="static-duck" style="width: 4rem" transition:fade/>
                <img src="duck.png" alt="gul plastand" class="static-duck" style="width: 3rem" transition:fade />
              {/if}
            </div>
            <div style="height: 50vh; width: 100%;">
              {#if activeIndex === 5 || activeIndex === 6}
                <img src="vise.png" alt="Noteark med vise" class="noteark" transition:fade />
              {/if}
            </div>
          </div>
        {/if}
      </div>
    </figure>

    <!-- Step text -->
    <article>
      <div class="step center-content" data-index="4">
        <div class="textbox">
          <p>Men en and i enden er tross alt bedre enn ti ender på taket</p>
        </div>
      </div>
    </article>

    <!-- Step text -->
    <article>
      <div class="step center-content" data-index="5">
        <div class="textbox">
          <p>Er det ingen ender på denne visa?</p>
        </div>
      </div>
    </article>

    <!-- Step text -->
    <article>
      <div class="step center-content" data-index="6">
        <div class="textbox">
          <p>Joda.</p>
        </div>
      </div>
    </article>

    <!-- Step text -->
    <article>
      <div class="step center-content" data-index="7">
        <div class="textbox">
          <p>Men dette er da vel ikke verdens ender?</p>
        </div>
      </div>
    </article>
  </div>
</section>

<!-- Last section, no sticky -->
<section class="footer">
  <!-- Text box 1 -->
  <article>
    <div class="step top-step" style="gap: 6rem" data-index="8">
      <div class="textbox">
        <p>Nei. Men så lenge ender er gode, er allting godt!</p>
      </div>

      <div>
        <p style="font-size: 4rem;">🍗 🍗 🍗</p>
        <p>Dette er enden.</p>
      </div>
      <p style="font-size: 1rem; opacity: 70%;">
        Illustrasjon av andedam fra <a style="color: black; opacity: 70%;" href="www.freepik.com">www.freepik.com</a>
      </p>
    </div>
  </article>
</section>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Bree+Serif&display=swap");

  :root {
    --black-color: #120908;
    --yellow-color: #ffe431;
  }

  /* Styling for all steps */
  .step {
    min-height: 100vh;
  }

  .step.center-content {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
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
      rgba(254, 185, 2, 1) 30%,
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

  .arrow {
    width: 2rem;
    height: 1rem;
    margin-top: 0.25rem;
    animation: arrow-bounce 1s ease-in-out 0s infinite;
    -webkit-animation: arrow-bounce 1s ease-in-out 0s infinite;
    -ms-animation: arrow-bounce 1s ease-in-out 0s infinite;
    -moz-animation: arrow-bounce 1s ease-in-out 0s infinite;
    -o-animation: arrow-bounce 1s ease-in-out 0s infinite;
  }

  @keyframes arrow-bounce {
    0% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(0.5rem);
    }
    100% {
      transform: translateY(0);
    }
  }

  .crossing-duck {
    position: absolute;
    right: -5rem;
    width: 5rem;
    height: auto;
    animation:
      duck-crossing 5s linear 1s infinite,
      duck-waggle 1s ease-in-out 0s infinite alternate-reverse;
    -webkit-animation:
      duck-crossing 5s linear 1s infinite,
      duck-waggle 1s ease-in-out 0s infinite alternate-reverse;
    -ms-animation:
      duck-crossing 5s linear 1s infinite,
      duck-waggle 1s ease-in-out 0s infinite alternate-reverse;
    -moz-animation:
      duck-crossing 5s linear 1s infinite,
      duck-waggle 1s ease-in-out 0s infinite alternate-reverse;
    -o-animation:
      duck-crossing 5s linear 1s infinite,
      duck-waggle 1s ease-in-out 0s infinite alternate-reverse;
  }

  .crossing-duck.second-duck {
    top: 2em;
    animation-delay: 3.5s;
  }

  @media (min-width: 1024px) {
    .crossing-duck {
      animation:
        duck-crossing 10s linear 1s infinite,
        duck-waggle 1s ease-in-out 0s infinite alternate-reverse;
      -webkit-animation:
        duck-crossing 10s linear 1s infinite,
        duck-waggle 1s ease-in-out 0s infinite alternate-reverse;
      -ms-animation:
        duck-crossing 10s linear 1s infinite,
        duck-waggle 1s ease-in-out 0s infinite alternate-reverse;
      -moz-animation:
        duck-crossing 10s linear 1s infinite,
        duck-waggle 1s ease-in-out 0s infinite alternate-reverse;
      -o-animation:
        duck-crossing 10s linear 1s infinite,
        duck-waggle 1s ease-in-out 0s infinite alternate-reverse;
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
    from {
      transform: rotate(-5deg);
    }
    to {
      transform: rotate(5deg);
    }
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
    margin: 0;
    padding: 0;
  }

  .svg-container {
    position: relative;
    width: 100%;
    height: 100vh;
    overflow: hidden;
  }

  .full-width-svg {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
    transition: object-position 0.3s ease-in-out;
  }

  .overlay-content {
    position: absolute;
    top: 72%;
    left: 50%;
    transform: translate(-50%, -50%); /* Center content (optional) */
    z-index: 1; /* Ensure content is on top */
    padding: 0.5rem;
    border-radius: 0.5rem;
  }

  .static-duck {
    width: 3rem;
    height: auto;
    animation: duck-waggle 1s ease-in-out 0s infinite alternate-reverse;
  }

  .static-duck.big {
    width: calc(100% / 4);
  }

  .static-duck.mirror-horizontal {
    animation: duck-waggle-flipped 1s ease-in-out 0s infinite alternate-reverse;
    -webkit-animation: duck-waggle-flipped 1s ease-in-out 0s infinite alternate-reverse;
    -ms-animation: duck-waggle-flipped 1s ease-in-out 0s infinite alternate-reverse;
    -moz-animation: duck-waggle-flipped 1s ease-in-out 0s infinite alternate-reverse;
    -o-animation: duck-waggle-flipped 1s ease-in-out 0s infinite alternate-reverse;
  }

  @keyframes duck-waggle-flipped {
    from {
      transform: scaleX(-1) rotate(-5deg);
    }
    to {
      transform: scaleX(-1) rotate(5deg);
    }
  }

  /* After SVG */

  .sticky-background-two {
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background: rgb(251, 227, 67);
    background: linear-gradient(180deg, #8ab041 0%, #bbb735 100%);
  }

  .noteark {
    height: 50vh;
    width: auto;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
    border-radius: 0.2rem;
  }

  /* ... */
  article {
    padding: 0;
  }

  .footer {
    min-height: 300px;
    display: flex;
    justify-content: center;
    align-items: center;
    background: #bbb735;
    background: linear-gradient(180deg, #bbb735 0%, #feb902 100%);
  }

  /* Responsive adjustments */
  @media (max-width: 768px) {
    .step {
      min-height: 90vh;
    }
    .full-width-svg {
      object-position: 20% center;
    }
    .overlay-content {
      left: 80%;
    }
  }
</style>
