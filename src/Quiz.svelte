<script>
	// import App from "./App.svelte";

	import questions from "../public/questions.json";
	import Spelling from "./Spelling.svelte";
	import Sight from "./Sight.svelte";
	import Math from "./Math.svelte";
	import FillIn from "./FillIn.svelte";
	let show = false;
	let activeQuestion = 0;
	let score = 0;
	let highScore = 0;
	let currentCategory = "spelling";
	let quiz = questions.Quiz.spelling;

	// array of quiz topics
	let topics = [
		{ title: "fill in the blank", path: questions.Quiz.fill_in },
		{ title: "spelling", path: questions.Quiz.spelling },
		{ title: "sight word flash cards", path: questions.Quiz.sight },
		{ title: "Math", path: questions.Quiz.Math },
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

	function getQuiz(questions) {
		const quiz = questions.Quiz;
		console.log(quiz);
		return quiz;
	}
	function choseCategory(topic) {
		currentCategory = topic.title;
		quiz = topic.path;
		console.log(quiz);

		show = !show;
		return resetQuiz(quiz);
	}
	function resetQuiz(quiz) {
		resetActiveQuestion();
		resetScore();

		// getQuiz(quiz);
	}

	// getQuiz(questions);
	checkHighScore();
	$: if (score > highScore) {
		highScore = score;
		localStorage.setItem("high", highScore);
	}

	$: quiz;
</script>

<div class="main card">
	<!-- <div id="title">{currentCategory}</div> -->
	<div class="dropdown">
		<button on:click={() => (show = !show)} class="dropbtn">Quiz Type</button>

		<div
			id="myDropdown"
			class={show ? "dropdown-content show" : "dropdown-content"}
		>
			{#each topics as topic}
				<a on:click={() => choseCategory(topic)}>{topic.title}</a>
			{/each}
		</div>
	</div>
	<button id="newQuiz" on:click={() => resetQuiz()}>new Quiz</button>

	<h3 id="score">My Score: {score}</h3>
	<h3 id="highScore">High Score: {highScore}</h3>

	{#if currentCategory === "spelling"}
		<Spelling
			class="question"
			{quiz}
			{nextQuestion}
			{scorePoint}
			{activeQuestion}
		/>
	{:else if currentCategory === "sight word flash cards"}
		<Sight id="word" {quiz} {nextQuestion} {activeQuestion} />
	{:else if currentCategory === "Math"}
		<Math
			class="question"
			{quiz}
			{nextQuestion}
			{scorePoint}
			{activeQuestion}
		/>
	{:else}
		<FillIn
			class="question"
			{quiz}
			{nextQuestion}
			{scorePoint}
			{activeQuestion}
		/>
	{/if}
</div>
<br />

<style>
	:global(body) {
		background: white;
	}
	.main {
		color: black;
		background-color: whitesmoke;
	}
	.card {
		color: white;
		height: 70vh;
		width: 55vw;
		/* border: 1px solid rgb(98, 2, 143); */
		/* Created with https://www.css-gradient.com */
		background: #35879b;
		background: -webkit-linear-gradient(top, #35879b, #3f1254);
		background: -moz-linear-gradient(top, #35879b, #3f1254);
		background: linear-gradient(to bottom, #35879b, #3f1254);
		border-radius: 10px;
		margin-left: 22.5vw;
		margin-right: 22.5vw;
		margin-top: 15vh;
		box-shadow: 4px 6px rgb(210, 208, 211);
		display: grid;
		grid-template-columns: 1fr 1fr 1fr 1fr;
		grid-template-rows: 20vh 20vh 20vh 20vh;
		grid-gap: 20px;
	}

	#title {
		justify-self: center;
		grid-column-start: 2;
		grid-column-end: 2;
		grid-row-start: 1;
		font-size: 3rem;
		font-weight: 800;
	}
	#newQuiz {
		/* max-height: 8vh; */
		background-color: white;
		color: black;
		justify-self: center;
		vertical-align: top;
		/* max-w	idth: 20vw; */
		grid-column-start: 4;
		grid-column-end: 4;
		grid-row-start: 1;
		margin-top: 1rem;
		/* margin-left: 1rem; */
	}
	#newQuiz:hover {
		background-color: white;
		color: black;
	}
	#score {
		justify-self: center;
		grid-column-start: 1;
		grid-column-end: 2;
		grid-row-start: 3;
	}
	#highScore {
		justify-self: center;
		grid-column-start: 4;
		grid-column-end: 4;
		grid-row-start: 3;
	}
	.question {
		justify-self: center;
		grid-column: 2 / span 2;
		/* grid-column-end: 4; */
		grid-row-start: 2;
		padding: 0.5rem 0.5rem 0 0;
	}
	/* Dropdown Button */
	.dropbtn {
		justify-self: center;
		text-align: center;
		vertical-align: middle;
		background-color: white;
		color: black;

		font-size: 1rem;
		border: none;
		cursor: pointer;
		grid-column-start: 1;
		grid-row-start: 1;
		box-shadow: 1px 2px rgb(199, 187, 204);
		margin-left: 1rem;
		margin-top: 1rem;
		/* padding-bottom: 1rem; */
	}

	/* Dropdown button on hover & focus */
	.dropbtn:hover,
	.dropbtn:focus {
		background-color: white;
		color: darkgray;
	}

	/* The container <div> - needed to position the dropdown content */
	.dropdown {
		display: grid;
		/* position: relative; */
		/* display: inline-block; */
	}

	/* Dropdown Content (Hidden by Default) */

	.dropdown-content {
		display: none;
		grid-row-start: 2;
		background-color: white;
		min-width: 160px;
		border: 0.07rem solid rgb(56, 103, 135);
		box-shadow: 1px 2px rgb(56, 103, 135);
		z-index: 1;
		border-radius: 10px;
	}

	/* Links inside the dropdown */
	.dropdown-content a {
		color: black;
		padding: 12px 16px;
		text-decoration: none;
	}

	/* Change color of dropdown links on hover */
	.dropdown-content a:hover {
		background-color: white;
	}

	/* Show the dropdown menu (use JS to add this class to the .dropdown-content container when the user clicks on the dropdown button) */
	.show {
		display: grid;
	}
</style>
