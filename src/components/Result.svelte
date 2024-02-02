<script>
  import { fly } from 'svelte/transition';
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  export let score = 0;
  export let seconds = 0;

  let userName = '';

  const save = () => {
    dispatch('save', userName);
  };
</script>

<section class="result">
  <div
    class="card"
    in:fly={{ x: 200, duration: 200 }}
    out:fly={{ x: -200, duration: 200 }}
  >
  <h2>C'est terminé !</h2>
  <p>Vous avez réussi à obtenir un score de {score} en {seconds} secondes.</p>
  

    <div class="form">
      <label for="userName">
        Entrée votre nom: 
        <input
          type="text"
          id="userName"
          name="userName"
          bind:value={userName}
        />
      </label>
      <button on:click={save}>Envoyer</button>
    </div>
  </div>
</section>

<style>
  .result {
    margin: 50px auto;
    width: fit-content;
  }
</style>
