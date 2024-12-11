<script>
</script>

<header>
  <h1>Simple SQL Formatter</h1>
</header>

<style>
  :global(:root) {
    --header-height: 4rem;
  }

  header {
    background-color: #2c3e50;
    color: white;
    padding: 1rem;
    text-align: center;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    height: var(--header-height);
    box-sizing: border-box;
    display: flex;
    align-items: center;
    justify-content: center;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 1001;
  }

  h1 {
    margin: 0;
    font-size: 2rem;
    font-weight: 600;
  }

  @media (max-width: 768px) {
    :global(:root) {
      --header-height: 3rem;
    }

    h1 {
      font-size: 1.5rem;
    }
  }
</style> 