<script>
  import Header from './components/Header.svelte';
  import Start from './components/Start.svelte';
  import Quiz from './components/Quiz.svelte';
  import Result from './components/Result.svelte';
  import Loading from './components/Loading.svelte';
  import Board from './components/Board.svelte';

  import { onDestroy } from 'svelte';

  let seconds = 0;
  let interval;

  const startTimer = () => {
    interval = setInterval(() => {
      seconds = seconds + 1;
    }, 1000);
  };

  onDestroy(() => clearInterval(interval));

  let arr;
  let index = 0;
  let score = 0;

  let state = 'start';

  const startQuiz = async () => {
    state = 'quiz';



    arr = [
    {
      "type": "multiple",
      "difficulty": "easy",
      "category": "Sports: Formula 1",
      "question": "Quelle écurie a remporté le championnat du monde de Formule 1 en 2021 ?",
      "correct_answer": "Mercedes",
      "incorrect_answers": ["Red Bull Racing", "Ferrari", "McLaren"]
    },
    {
      "type": "multiple",
      "difficulty": "medium",
      "category": "Sports: Formula 1",
      "question": "Qui a remporté le Grand Prix de Monaco en 2021 ?",
      "correct_answer": "Max Verstappen",
      "incorrect_answers": ["Lewis Hamilton", "Charles Leclerc", "Valtteri Bottas"]
    },
    {
      "type": "multiple",
      "difficulty": "hard",
      "category": "Sports: Formula 1",
      "question": "Quel pilote de Formule 1 a remporté le plus grand nombre de titres mondiaux ?",
      "correct_answer": "Michael Schumacher",
      "incorrect_answers": ["Ayrton Senna", "Lewis Hamilton", "Alain Prost"]
    },
    {
      "type": "multiple",
      "difficulty": "medium",
      "category": "Sports: Formula 1",
      "question": "En quelle année a eu lieu le premier Grand Prix de Formule 1 ?",
      "correct_answer": "1950",
      "incorrect_answers": ["1948", "1962", "1975"]
    },
    {
      "type": "multiple",
      "difficulty": "easy",
      "category": "Sports: Formula 1",
      "question": "Quelle écurie est souvent associée au pilote Ayrton Senna dans les années 1980 et 1990 ?",
      "correct_answer": "McLaren",
      "incorrect_answers": ["Ferrari", "Williams", "Benetton"]
    },
    {
      "type": "multiple",
      "difficulty": "hard",
      "category": "Sports: Formula 1",
      "question": "Quel circuit est surnommé 'l'enfer vert' et est réputé pour sa difficulté et son tracé exigeant ?",
      "correct_answer": "Nürburgring Nordschleife",
      "incorrect_answers": ["Monaco", "Spa-Francorchamps", "Suzuka"]
    },
    {
      "type": "multiple",
      "difficulty": "medium",
      "category": "Sports: Formula 1",
      "question": "Quel pilote de Formule 1 est surnommé 'The Iceman' ?",
      "correct_answer": "Kimi Räikkönen",
      "incorrect_answers": ["Sebastian Vettel", "Fernando Alonso", "Nico Rosberg"]
    },
    {
      "type": "multiple",
      "difficulty": "easy",
      "category": "Sports: Formula 1",
      "question": "Quelle équipe a remporté le premier championnat du monde de Formule 1 en 1950 ?",
      "correct_answer": "Alfa Romeo",
      "incorrect_answers": ["Ferrari", "Mercedes", "Lotus"]
    }
  ];

    startTimer();
  };

  const answered = ({ detail: answer }) => {
    if (answer === arr[index].correct_answer) {
      score++;
    }
    index++;

    if (index === arr.length) {
      state = 'done';
      clearInterval(interval);
    }
  };

  const saveScore = ({ detail: userName }) => {
    console.log(userName);
    const arr = localStorage.getItem('board')
      ? JSON.parse(localStorage.getItem('board'))
      : [];

    const curScore = arr.find((s) => s.name === userName);
    if (!curScore) {
      arr.push({
        name: userName,
        score,
      });
    } else {
      if (score > curScore.score) {
        curScore.score = score;
      }
    }

    localStorage.setItem('board', JSON.stringify(arr));

    state = 'start';
    seconds = 0;
  };

  const toggleBoard = () => {
    if (state !== 'board') {
      state = 'board';
    } else {
      state = 'start';
    }
  };
</script>

<main>
  <Header on:click={toggleBoard} {seconds} />

  {#if state === 'board'}
    <Board />
  {/if}

  {#if state === 'start'}
    <Start on:click={startQuiz} />
  {/if}

  {#if state !== 'board' && state !== 'start' && !arr}
    <Loading />
  {/if}

  {#if arr && index < arr.length}
    <Quiz question={arr[index]} on:choose={answered} />
  {/if}

  {#if state === 'done'}
    <Result {score} {seconds} on:save={saveScore} />
  {/if}
</main>

<style>
</style>
