<script>
	import App from "./App.svelte";
	import Question from "./Question.svelte";
	import { fade } from "svelte/transition";
	let show = false;
	let activeQuestion = 0;
	let score = 0;
	let highScore = 0;
	let currentCategory = "tv";
	let categoryQuery = "category=14&type=multiple";
	let quiz = getQuiz(categoryQuery);

	// array of quiz topics
	let topics = [
		{ title: "science", url: "category=17&type=multiple" },
		{ title: "movies", url: "category=11&type=multiple" },
		{ title: "music", url: "category=12&type=multiple" },
		{ title: "tv", url: "category=14&type=multiple" },
		{ title: "video games", url: "category=15&type=multiple" },
		{ title: "computers", url: "category=18&type=multiple" },
		{ title: "mythology", url: "category=20&type=multiple" },
		{ title: "sports", url: "category=21&type=multiple" },
		{ title: "geography", url: "category=22&type=multiple" },
		{ title: "history", url: "category=23&type=multiple" },
		{ title: "politics", url: "category=24&type=multiple" },
		{ title: "art", url: "category=25&type=multiple" },
		{ title: "celebrities", url: "category=26&type=multiple" },
		{ title: "animals", url: "category=27&type=multiple" },
		{ title: "vehicles", url: "category=28&type=multiple" },
		{ title: "comics", url: "category=29&type=multiple" },
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

	async function getQuiz(url) {
		let queryString = "category=17&type=multiple";
		queryString = url;
		console.log(queryString);

		const res = await fetch(
			"https://opentdb.com/api.php?amount=10&" + queryString
		);
		const quiz = await res.json();
		console.log(quiz);
		return quiz;
	}
	function choseCategory(topic) {
		currentCategory = topic.title;
		categoryQuery = topic.url;
		resetQuiz(categoryQuery);
		show = !show;
	}
	function resetQuiz(url) {
		if (score > highScore) {
			highScore = score;
			localStorage.setItem("high", highScore);
		}

		let query = url;
		console.log(query);
		resetActiveQuestion();
		resetScore();
		quiz = getQuiz(query);
	}
	checkHighScore();
</script>

<div class="main">
	<h1 id="title">{currentCategory} trivia</h1>
	<div class="dropdown">
		<button on:click={() => (show = !show)} class="dropbtn">Category</button>
		<div
			id="myDropdown"
			class={show ? "dropdown-content show" : "dropdown-content"}
		>
			{#each topics as topic}
				<a on:click={() => choseCategory(topic)}>{topic.title}</a>
			{/each}
		</div>
	</div>

	<button id="newQuiz" on:click={() => resetQuiz(categoryQuery)}
		>Start new Quiz</button
	>
	<h3 id="score">My Score: {score}</h3>
	<h3 id="highScore">High Score: {highScore}</h3>

	{#await quiz}
		loading........
	{:then data}
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
		background-color: #f1f1f1;
		min-width: 160px;
		box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
		z-index: 1;
	}

	/* Links inside the dropdown */
	.dropdown-content a {
		color: black;
		padding: 12px 16px;
		text-decoration: none;
		display: block;
	}

	/* Change color of dropdown links on hover */
	.dropdown-content a:hover {
		background-color: #ddd;
	}

	/* Show the dropdown menu (use JS to add this class to the .dropdown-content container when the user clicks on the dropdown button) */
	.show {
		display: grid;
	}
</style>
