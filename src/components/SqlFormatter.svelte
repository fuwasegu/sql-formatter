<script lang="ts">
  import { format } from 'sql-formatter';
  import hljs from 'highlight.js/lib/core';
  import sql from 'highlight.js/lib/languages/sql';
  import 'highlight.js/styles/atom-one-dark.css';

  // highlight.jsにSQLを登録
  hljs.registerLanguage('sql', sql);

  type Dialect = 'sql' | 'mysql' | 'postgresql' | 'sqlite' | 'bigquery' | 'db2' | 'hive' | 'mariadb' | 'n1ql' | 'plsql' | 'redshift' | 'spark' | 'tsql';

  let inputSql = '';
  let outputSql = '';
  let selectedDialect: Dialect = 'sql';
  
  const dialects = [
    { value: 'sql' as const, label: 'Standard SQL' },
    { value: 'mysql' as const, label: 'MySQL' },
    { value: 'postgresql' as const, label: 'PostgreSQL' },
    { value: 'sqlite' as const, label: 'SQLite' },
    { value: 'bigquery' as const, label: 'BigQuery' },
    { value: 'db2' as const, label: 'DB2' },
    { value: 'hive' as const, label: 'Hive' },
    { value: 'mariadb' as const, label: 'MariaDB' },
    { value: 'n1ql' as const, label: 'N1QL' },
    { value: 'plsql' as const, label: 'PL/SQL' },
    { value: 'redshift' as const, label: 'Redshift' },
    { value: 'spark' as const, label: 'Spark' },
    { value: 'tsql' as const, label: 'T-SQL' }
  ];

  function formatSql() {
    if (!inputSql) {
      outputSql = '';
      if (outputContainer) {
        outputContainer.innerHTML = '';
      }
      return;
    }
    
    try {
      outputSql = format(inputSql, {
        language: selectedDialect,
        keywordCase: 'upper',
        tabWidth: 2
      });
      
      // フォーマット後のSQLをハイライト
      const highlightedCode = hljs.highlight(outputSql, { language: 'sql' }).value;
      
      // ハイライトされたHTMLを表示エリアに設定
      if (outputContainer) {
        outputContainer.innerHTML = highlightedCode;
      }

    } catch (error) {
      console.error('Format error:', error);
      outputSql = `Error: ${error.message}`;
      if (outputContainer) {
        outputContainer.textContent = outputSql;
      }
    }
  }

  function copyToClipboard() {
    navigator.clipboard.writeText(outputSql);
  }

  function adjustTextareaHeight(textarea: HTMLTextAreaElement) {
    textarea.style.height = '0';
    textarea.style.height = `${textarea.scrollHeight}px`;
  }

  function clearInput() {
    inputSql = '';
    if (inputTextarea) {
      inputTextarea.style.height = 'auto';
    }
  }

  let outputContainer: HTMLPreElement;
  let inputTextarea: HTMLTextAreaElement;

  $: if (inputTextarea && inputSql) {
    setTimeout(() => adjustTextareaHeight(inputTextarea), 0);
  }

  $: inputSql, selectedDialect, formatSql();
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
        bind:this={inputTextarea}
        on:input={() => adjustTextareaHeight(inputTextarea)}
      ></textarea>
      <button class="clear-button" on:click={clearInput}>
        クリア
      </button>
    </div>

    <div class="editor">
      <pre
        class="output-pre"
        bind:this={outputContainer}
      ><code></code></pre>
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
    background-color: #282c34;
    color: #abb2bf;
    font-size: 1rem;
    width: 200px;
  }

  select option {
    background-color: #282c34;
    color: #abb2bf;
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
    min-height: 300px;
    padding: 1rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-family: 'Monaco', 'Menlo', 'Ubuntu Mono', 'Consolas', monospace;
    font-size: 14px;
    line-height: 1.5;
    resize: none;
    box-sizing: border-box;
    background-color: #282c34;
    color: #abb2bf;
    overflow-y: hidden;
  }

  textarea::placeholder {
    color: #6b727b;
  }

  .output-pre {
    width: 100%;
    min-height: 300px;
    padding: 1rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-family: 'Monaco', 'Menlo', 'Ubuntu Mono', 'Consolas', monospace;
    font-size: 14px;
    line-height: 1.5;
    box-sizing: border-box;
    background-color: #282c34;
    color: #abb2bf;
    overflow-y: auto;
    margin: 0;
    white-space: pre-wrap;
    text-align: left;
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

  .clear-button {
    position: absolute;
    bottom: 1rem;
    right: 1rem;
    padding: 0.5rem 1rem;
    background-color: #e74c3c;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s;
  }

  .clear-button:hover {
    background-color: #c0392b;
  }

  @media (max-width: 1280px) {
    .editor-container {
      grid-template-columns: 1fr;
    }

    textarea, .output-pre {
      min-height: 250px;
    }

    .copy-button {
      bottom: 0.5rem;
      right: 0.5rem;
    }

    .clear-button {
      bottom: 0.5rem;
      right: 0.5rem;
    }
  }

  :global(.hljs) {
    background: transparent !important;
    padding: 0 !important;
  }
</style> 