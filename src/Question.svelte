<script>
	import True from "./True.svelte";
	import False from "./False.svelte";
	import { fade } from "svelte/transition";
	export let question;
	export let nextQuestion;
	export let scorePoint;
	let isAnswered = false;
	let questionRes;
	let answers = question.incorrect_answers;

	function handleClick(answer) {
		questionRes = answer === question.correct_answer;
		isAnswered = true;
		return questionRes;
	}
	function shuffleAnswers(answers) {
		answers.push(question.correct_answer);
		answers.sort(() => Math.random() - 0.5);
	}
	shuffleAnswers(answers);
</script>

<h2>{@html question.question}</h2>
{#if !isAnswered}
	{#each answers as answer}
		<button
			class="btn"
			on:click={() => {
				handleClick(answer);
			}}>{@html answer}</button
		>
	{/each}
	<br />
{:else if questionRes}
	<True
		{nextQuestion}
		{scorePoint}
		{isAnswered}
	/>{:else if questionRes === false}<False {nextQuestion} {isAnswered} />{/if}

<style>
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
		background-color: yellow;
		color: palevioletred;
	}
	:global(button:hover) {
		background-color: rgb(253, 255, 144);
		color: rgb(204, 59, 108);
	}
</style>
