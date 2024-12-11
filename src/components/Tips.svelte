<script>
</script>

<div class="tips">
  <div class="icon">🔒</div>
  <p>
    このSQLフォーマッタは完全にクライアントサイドで動作します。
    外部との通信は一切行わないため、機密性の高いSQLも安心して整形できます。
  </p>
</div>

<style>
  .tips {
    background-color: #fff;
    border-radius: 8px;
    padding: 12px 16px;
    margin-bottom: 8px;
    display: flex;
    align-items: center;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  }

  .icon {
    font-size: 1.5rem;
    margin-right: 16px;
  }

  p {
    margin: 0;
    color: #2c3e50;
    line-height: 1.5;
  }

  @media (max-width: 768px) {
    .tips {
      flex-direction: column;
      text-align: center;
      padding: 8px 12px;
    }

    .icon {
      margin-right: 0;
      margin-bottom: 8px;
    }
  }
</style> 