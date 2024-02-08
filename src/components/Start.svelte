<script>
  import { fly } from "svelte/transition";
</script>

<section class="start">
  <div
    class="card"
    in:fly={{ x: 200, duration: 200 }}
    out:fly={{ x: -200, duration: 200 }}
  >
    <h2>Challenge du Quizz de Formule 1</h2>
    <p>
      Essayez de répondre aux questions liées à la formule 1 dans la limite de
      temps.
    </p>
    <p>
      Gardez à l'esprit que des réponses incorrectes pénaliseront votre
      score/temps de dix secondes !
    </p>

    <button on:click>Commencer le quizz</button>
  </div>
  <div class="formule1center">
    <img
      src="https://gp-explorer.fr/wp-content/themes/nc/static/svg/formule-4-bleu.svg"
      class="formule-4 js-reveal hidden m:block absolute -top-6 left-[68%] m:w-[280px] l:w-[354px] is-visible"
      alt=""
    />
  </div>
</section>

<style>
  .start {
    margin: 50px;
  }
</style>
