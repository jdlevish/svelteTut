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
	let spell = "";

	function handleClick(answer) {
		questionRes = answer === question.correct_answer;
		isAnswered = true;
		return questionRes;
	}

	console.log(question);
</script>

<div class="question">
	{#if !isAnswered}
		<h2>{@html question.question}</h2>
		<h3>{spell}</h3>

		<form
			on:submit={() => {
				handleClick(spell.toLowerCase());
			}}
		>
			<input bind:value={spell} />
		</form>
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
	input {
		border: 2px solid black;
	}
	:global(button) {
		justify-content: stretch;
		font-family: "Source Sans Pro", sans-serif;
		font-weight: 900;
		padding: 1.25rem 2rem;
		font-size: 1rem;
		border-radius: 3.5rem / 100%;
		position: relative;
		min-width: 15rem;
		max-width: 15vw;
		height: 10vh;
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
		grid-column-start: 3;
		grid-row-start: 1;
		/* margin-left: %;
		margin-right: auto; */
	}
</style>
