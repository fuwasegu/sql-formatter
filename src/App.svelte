<script>
  import Header from './components/Header.svelte';
  import SqlFormatter from './components/SqlFormatter.svelte';
  import Tips from './components/Tips.svelte';
</script>

<Header />
<main>
  <Tips />
  <SqlFormatter />
</main>


<style>
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    background-color: #f5f5f5;
  }

  main {
    max-width: 1280px;
    margin: calc(var(--header-height) + 16px) auto 0;
    padding: 0 24px;
  }

  @media (max-width: 768px) {
    main {
      padding: 0 16px;
    }
  }
</style>
