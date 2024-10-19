<script>
  import { slide, fly } from 'svelte/transition';

  let y;
  $: console.log(y);
</script>

<svelte:window bind:scrollY={y} />

<main>
    <div id="navbar" class:show={y >= 80}>
      <p>Navbar {y}</p>
    </div>

  <p>scroll down..</p>

</main>

<style>
  main {
    height: 200vh;
  }

  #navbar {
    position: fixed;
    top: -100px;
    left: 0;
    width: 100%;
    background-color: #333;
    color: white;
    padding: 1rem;
  }

  div#navbar.show {
    top: 0;
  }
</style>
