<script>
  import List from "./lib/List.svelte";
</script>

<main>
  <header>
    <div class="container">
      <h1>MC Mirrors</h1>
      <h2>Пользовательские зеркала для лаунчеров Minecraft</h2>
    </div>
  </header>
  <div class="container content">
    <h3>Добро пожаловать!</h3>
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Ex adipisci totam
      non ea, facilis officiis saepe consequatur. Praesentium perferendis
      laboriosam dolores? Ut nam ea eum numquam autem veritatis corrupti iusto.
    </p>
    <h3>Список поддерживаемых нами зеркал</h3>
    <List />
    <h3>Хотите создать своё зеркало?</h3>
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Ex adipisci totam
      non ea, facilis officiis saepe consequatur. Praesentium perferendis
      laboriosam dolores? Ut nam ea eum numquam autem veritatis corrupti iusto.
    </p>
  </div>
</main>

<style>
  header {
    padding: 12rem 0;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    background-color: #f4f5f6;
  }
  .content {
    padding: 6rem;
  }
</style>
