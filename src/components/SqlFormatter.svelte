<script>
  import { format } from 'sql-formatter';

  let inputSql = '';
  let outputSql = '';
  let selectedDialect = 'mysql';
  
  const dialects = [
    { value: 'mysql', label: 'MySQL' },
    { value: 'postgresql', label: 'PostgreSQL' },
    { value: 'sqlite', label: 'SQLite' },
    { value: 'bigquery', label: 'BigQuery' },
    { value: 'db2', label: 'DB2' },
    { value: 'hive', label: 'Hive' },
    { value: 'mariadb', label: 'MariaDB' },
    { value: 'n1ql', label: 'N1QL' },
    { value: 'plsql', label: 'PL/SQL' },
    { value: 'redshift', label: 'Redshift' },
    { value: 'spark', label: 'Spark' },
    { value: 'tsql', label: 'T-SQL' }
  ];

  function formatSql() {
    try {
      outputSql = format(inputSql, {
        language: selectedDialect,
        uppercase: true
      });
    } catch (error) {
      outputSql = `Error: ${error.message}`;
    }
  }

  function copyToClipboard() {
    navigator.clipboard.writeText(outputSql);
  }

  $: {
    if (inputSql) {
      formatSql();
    }
  }
</script>

<div class="formatter">
  <div class="controls">
    <select bind:value={selectedDialect}>
      {#each dialects as dialect}
        <option value={dialect.value}>{dialect.label}</option>
      {/each}
    </select>
  </div>

  <div class="editor-container">
    <div class="editor">
      <textarea
        placeholder="ここにSQLを入力してください..."
        bind:value={inputSql}
      ></textarea>
    </div>

    <div class="editor">
      <textarea
        placeholder="フォーマット後のSQLがここに表示されます..."
        bind:value={outputSql}
      ></textarea>
      <button class="copy-button" on:click={copyToClipboard}>
        クリップボードにコピー
      </button>
    </div>
  </div>
</div>

<style>
  .formatter {
    background-color: #fff;
    border-radius: 8px;
    padding: 1rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  }

  .controls {
    margin-bottom: 1rem;
  }

  select {
    padding: 0.5rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    background-color: white;
    font-size: 1rem;
    width: 200px;
  }

  .editor-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
  }

  .editor {
    position: relative;
  }

  textarea {
    width: 100%;
    height: 300px;
    padding: 1rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-family: 'Monaco', 'Menlo', 'Ubuntu Mono', 'Consolas', monospace;
    font-size: 14px;
    line-height: 1.5;
    resize: vertical;
    box-sizing: border-box;
    background-color: #1e1e1e;
    color: #fff;
  }

  .copy-button {
    position: absolute;
    bottom: 1rem;
    right: 1rem;
    padding: 0.5rem 1rem;
    background-color: #2c3e50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s;
  }

  .copy-button:hover {
    background-color: #34495e;
  }

  @media (max-width: 768px) {
    .editor-container {
      grid-template-columns: 1fr;
    }

    textarea {
      height: 250px;
    }

    .copy-button {
      bottom: 0.5rem;
      right: 0.5rem;
    }
  }
</style> 