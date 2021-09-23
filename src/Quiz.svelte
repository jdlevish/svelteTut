<script>
	// import App from "./App.svelte";

	import questions from "../public/questions.json";
	import Spelling from "./Spelling.svelte";
	// import Fill_in from "./FillIn.svelte";
	import FillIn from "./FillIn.svelte";
	let show = false;
	let activeQuestion = 0;
	let score = 0;
	let highScore = 0;
	let currentCategory = "spelling";
	let type;

	let quiz = questions.Quiz.spelling;

	// array of quiz topics
	let topics = [
		{ title: "fill in the blank", path: questions.Quiz.fill_in },
		{ title: "spelling", path: questions.Quiz.spelling },
		{ title: "sight word flash cards", path: questions.Quiz.sight },
		{ title: "name that picture", path: questions.Quiz.picture },
		{ title: "Math", path: questions.Quiz.math },
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
	<h1 id="title">{currentCategory}</h1>
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
		<Spelling {quiz} {nextQuestion} {scorePoint} {activeQuestion} />
	{:else}
		<FillIn {quiz} {nextQuestion} {scorePoint} {activeQuestion} />
	{/if}
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
	/* Dropdown Button */
	.dropbtn {
		background-color: #3498db;
		color: white;
		padding: 16px;
		font-size: 16px;
		border: none;
		cursor: pointer;
	}

	/* Dropdown button on hover & focus */
	.dropbtn:hover,
	.dropbtn:focus {
		background-color: #2980b9;
	}

	/* The container <div> - needed to position the dropdown content */
	.dropdown {
		position: relative;
		display: inline-block;
	}

	/* Dropdown Content (Hidden by Default) */

	.dropdown-content {
		display: none;
		position: absolute;
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
		display: block;
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
