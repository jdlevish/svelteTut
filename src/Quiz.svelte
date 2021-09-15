<script>
	import App from "./App.svelte";
	import Question from "./Question.svelte";
	import { fade } from "svelte/transition";

	let quiz = getQuiz();
	let activeQuestion = 0;
	let score = 0;
	let highScore = 0;
	// api queries
	let science =
		"https://opentdb.com/api.php?amount=10&category=17&type=multiple";
	let movies =
		"https://opentdb.com/api.php?amount=10&category=11&type=multiple";
	let music = "https://opentdb.com/api.php?amount=10&category=12&type=multiple";
	let TV = "https://opentdb.com/api.php?amount=10&category=14&type=multiple";
	let videoGames =
		"https://opentdb.com/api.php?amount=10&category=15&type=multiple";
	let computers =
		"https://opentdb.com/api.php?amount=10&category=18&type=multiple";
	let math = "https://opentdb.com/api.php?amount=10&category=19&type=multiple";
	let mythology =
		"https://opentdb.com/api.php?amount=10&category=20&type=multiple";
	let sports =
		"https://opentdb.com/api.php?amount=10&category=21&type=multiple";
	let geography =
		"https://opentdb.com/api.php?amount=10&category=22&type=multiple";
	let history =
		"https://opentdb.com/api.php?amount=10&category=23&type=multiple";
	let politics =
		"https://opentdb.com/api.php?amount=10&category=24&type=multiple";
	let art = "https://opentdb.com/api.php?amount=10&category=25&type=multiple";
	let celebrities =
		"https://opentdb.com/api.php?amount=10&category=26&type=multiple";
	let animals =
		"https://opentdb.com/api.php?amount=10&category=27&type=multiple";
	let vehicles =
		"https://opentdb.com/api.php?amount=10&category=28&type=multiple";
	let comics =
		"https://opentdb.com/api.php?amount=10&category=29&type=multiple";

	// array of quiz topics
	let topics = [
		"science",
		"movies",
		"music",
		"tv",
		"video games",
		"computers",
		"mythology",
		"sports",
		"geography",
		"history",
		"politics",
		"art",
		"celebrities",
		"animals",
		"vehicles",
		"comics",
	];

	function scorePoint() {
		score++;
	}

	function nextQuestion() {
		activeQuestion = activeQuestion + 1;
	}
	function resetActiveQuestion() {
		activeQuestion = 0;
	}
	function resetScore() {
		score = 0;
	}
	function checkHighScore() {
		let high = localStorage.getItem("high");
		if (high != undefined) {
			highScore = high;
		}
	}

	async function getQuiz() {
		const res = await fetch(
			"https://opentdb.com/api.php?amount=10&category=17&type=multiple"
		);
		const quiz = await res.json();
		console.log(quiz);
		return quiz;
	}

	function resetQuiz() {
		if (score > highScore) {
			highScore = score;
			localStorage.setItem("high", highScore);
		}
		resetActiveQuestion();
		resetScore();
		quiz = getQuiz();
	}
	checkHighScore();
</script>

<div class="main">
	<h1 id="title">Science trivia</h1>

	<button id="newQuiz" on:click={resetQuiz}>Start new Quiz</button>
	<h3 id="score">My Score: {score}</h3>
	<h3 id="highScore">High Score: {highScore}</h3>

	{#await quiz}
		loading........
	{:then data}
		<!-- <h3>{data.results[0].question}</h3> -->

		{#each data.results as question, index}
			{#if index === activeQuestion}
				<div transition:fade class="question">
					<Question {nextQuestion} {scorePoint} {question} />
				</div>
			{/if}
		{/each}
	{/await}
</div>
<br />

<style>
	:global(body) {
		color: purple;
		background-color: aqua;
	}
	.main {
		color: purple;
		background-color: aqua;
		display: grid;
		grid-template-columns: 1fr 1fr 1fr 1fr;
		grid-template-rows: 20vh 20vh 20vh 20vh;
		grid-gap: 20px;
	}
	#title {
		justify-self: center;
		grid-column-start: 2;
		grid-column-end: 3;
		grid-row-start: 1;
	}
	#newQuiz {
		/* max-height: 8vh; */
		justify-self: end;
		/* max-width: 20vw; */
		grid-column-start: 1;
		grid-column-end: 1;
		grid-row-start: 2;
	}
	#score {
		justify-self: center;
		grid-column-start: 2;
		grid-column-end: 3;
		grid-row-start: 2;
	}
	#highScore {
		justify-self: start;
		grid-column-start: 3;
		grid-column-end: 4;
		grid-row-start: 2;
	}
	.question {
		justify-self: center;
		grid-column-start: 1;
		grid-column-end: 4;
		grid-row-start: 3;
	}
</style>
