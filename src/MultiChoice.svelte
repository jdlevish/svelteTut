<script>
	import True from "./True.svelte";
	import False from "./False.svelte";
	import { fade } from "svelte/transition";

	export let question;
	export let nextQuestion;
	export let scorePoint;
	let correctAnswer = question.correct_answer;
	let isAnswered = false;
	let questionRes;
	let answers = question.answers;

	function handleClick(answer) {
		questionRes = answer === question.correct_answer;
		isAnswered = true;
		return questionRes;
	}
	// function shuffleAnswers(answers) {
	// 	answers.push(question.correct_answer);
	// 	answers.sort(() => Math.random() - 0.5);
	// }
	// shuffleAnswers(answers);
	console.log(question);
</script>

<div>
	{#if !isAnswered}
		<h2 class="question">{@html question.question}</h2>
		<div class="answers">
			{#each answers as answer}
				<button
					class="btn"
					on:click={() => {
						handleClick(answer);
					}}>{@html answer}</button
				>
			{/each}
		</div>
		<br />
	{:else if questionRes}
		<True
			{nextQuestion}
			{scorePoint}
			{isAnswered}
		/>{:else if questionRes === false}<False
			{nextQuestion}
			{correctAnswer}
			{isAnswered}
		/>
	{/if}
</div>

<style>
	:global(button) {
		justify-content: stretch;
		font-family: "Source Sans Pro", sans-serif;
		font-weight: 900;
		padding: 0.5rem 2rem;
		font-size: 1rem;
		border-radius: 10px;
		box-shadow: 1px 2px rgb(199, 187, 204);
		position: relative;
		min-width: 10rem;
		max-width: 15vw;
		height: 5vh;
		overflow: hidden;
		border: 0;
		cursor: pointer;
		text-transform: uppercase;
		letter-spacing: 0.05em;
		background-color: white;
		color: black;
	}
	:global(button:hover) {
		background-color: white;
		color: black;
	}
	:global(img) {
		height: 20vh;
		width: 17vw;
	}
	.question {
		font-size: 1.2rem;
		text-align: center;
		/* justify-self: stretch; */
		grid-column: 2 / span 2;
		/* grid-column-end: 4; */
		grid-row-start: 2;
		/* margin-top: 13vh;
		margin-left: 10vw; */
	}
	.answers {
		justify-items: center;
		grid-column: 3 / span 2;
		grid-row-start: 2;
	}
</style>
