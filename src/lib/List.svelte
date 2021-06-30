<script>
  const list = ["mirror.samopis.ru"];
</script>

<ul>
  {#each list as el}
    <li>
      <a target="_blank" href="//{el}">{el}</a>
    </li>
  {/each}
</ul>
