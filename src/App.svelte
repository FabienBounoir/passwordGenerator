<script>
  import GeneratorPassword from "./lib/GeneratorPassword.svelte";
</script>

<main>
  <div>
    <a href="https://svelte.dev" target="_blank">
      <img
        src="./passwordGenerator.svg"
        class="logo passwordLogo"
        alt="Svelte Logo"
      />
    </a>
  </div>
  <h1>Password Generator</h1>

  <div class="card">
    <GeneratorPassword />
  </div>
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
  }
  .logo.passwordLogo:hover {
    /* filter: drop-shadow(0 0 2em #ff3e00aa); */
    animation: pulse 3s infinite;
  }

  @keyframes pulse {
    0% {
      filter: drop-shadow(0 0 0 #ff3e00aa);
    }
    50% {
      filter: drop-shadow(0 0 2em #ff3e00aa);
    }
    0% {
      filter: drop-shadow(0 0 0 #ff3e00aa);
    }
  }
</style>
