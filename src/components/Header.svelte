<script>
  export let seconds = 0;
</script>

<nav>
  <img src="formula1.png" alt="Svelte logo" width="100vw" height="100vh" />

  <div class="highScore" on:click>Voir le tableaux des scores</div>

  <p>Timer: <b>{seconds}</b></p>
</nav>

<style>
  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
    background-color: #ce1212;
    color: #fff;
  }

  .highScore {
    cursor: pointer;
  }

  .highScore:hover {
    font-weight: bold;
  }
</style>
