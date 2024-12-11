<script>
  import Header from './components/Header.svelte';
  import SqlFormatter from './components/SqlFormatter.svelte';
  import Tips from './components/Tips.svelte';
</script>

<Header />
<main>
  <div class="container">
    <Tips />
    <SqlFormatter />
  </div>
</main>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    background-color: #f5f5f5;
    min-height: 100vh;
  }

  main {
    padding-top: var(--header-height);
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 8px 24px;
    box-sizing: border-box;
  }

  @media (max-width: 768px) {
    .container {
      padding: 4px 16px;
    }
  }
</style>
