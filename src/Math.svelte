<script>
	export let quiz;
	export let activeQuestion;
	export let scorePoint;
	export let nextQuestion;
	import Multi from "./MultiChoice.svelte";
	import { fade } from "svelte/transition";
	console.log(quiz);
</script>

{#each quiz as question, index}
	{#if index === activeQuestion}
		<div transition:fade class="question">
			<Multi {nextQuestion} {scorePoint} {question} />
		</div>
	{/if}
{/each}

<style>
	.question {
		justify-self: center;
		grid-column: 2 / span 2;
		/* grid-column-end: 3; */
		grid-row-start: 2;
		margin-top: 5vh;
	}
</style>
