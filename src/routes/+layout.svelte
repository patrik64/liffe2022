<script>
  import "../app.css";
  import Footer from "../lib/Footer.svelte";
</script>

<div class="screen">
  <a href="/"  class="m-10">
    <img src="liffe_logo.png" alt="logo" />
  </a>
  <main>
    <slot />
  </main>
  <footer>
    <Footer />
  </footer>
</div>

<svelte:head>
  <title>liffe 2022</title>
  <meta name="robots" content="noindex nofollow" />
</svelte:head>

<style>
  .screen {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

  main {
    flex: 1;
  }
</style>
