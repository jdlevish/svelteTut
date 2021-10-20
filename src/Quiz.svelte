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

<div class="main">
	<div id="title">{currentCategory}</div>
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
	<button id="newQuiz" on:click={() => resetQuiz()}>Start new Quiz</button>

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
		<Sight class="question" {quiz} {nextQuestion} {activeQuestion} />
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
		background-color: whitesmoke;
	}
	.main {
		color: orangered;
		background-color: whitesmoke;
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
		justify-self: center;
		/* max-width: 20vw; */
		grid-column-start: 3;
		grid-column-end: 3;
		grid-row-start: 1;
	}
	#score {
		justify-self: center;
		grid-column-start: 1;
		grid-column-end: 2;
		grid-row-start: 2;
	}
	#highScore {
		justify-self: center;
		grid-column-start: 3;
		grid-column-end: 3;
		grid-row-start: 2;
	}
	.question {
		justify-self: center;
		grid-column-start: 1;
		grid-column-end: 4;
		grid-row-start: 3;
	}
	/* Dropdown Button */
	.dropbtn {
		justify-self: center;
		background-color: #3498db;
		color: white;
		padding: 16px;
		font-size: 16px;
		border: none;
		cursor: pointer;
		grid-column-start: 1;
		grid-row-start: 1;
	}

	/* Dropdown button on hover & focus */
	.dropbtn:hover,
	.dropbtn:focus {
		background-color: #2980b9;
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
		background-color: #3498db;
		min-width: 160px;
		box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
		z-index: 1;
	}

	/* Links inside the dropdown */
	.dropdown-content a {
		color: white;
		padding: 12px 16px;
		text-decoration: none;
	}

	/* Change color of dropdown links on hover */
	.dropdown-content a:hover {
		background-color: #2980b9;
	}

	/* Show the dropdown menu (use JS to add this class to the .dropdown-content container when the user clicks on the dropdown button) */
	.show {
		display: grid;
	}
</style>
