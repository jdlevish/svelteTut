<script>
	export let quiz;
	export let nextQuestion;
	export let activeQuestion;
	import FlashCard from "./FlashCard.svelte";

	import { fade } from "svelte/transition";
	console.log(quiz);
	console.log("active " + activeQuestion);
</script>

{#each quiz as word, index}
	{#if index === activeQuestion}
		<div transition:fade class="question">
			<FlashCard class="question" {nextQuestion} {word} />
		</div>
	{/if}
{/each}

<style>
	.question {
		justify-self: center;
		grid-column: 2 / span 2;
		/* grid-column-end: 3; */
		grid-row-start: 2;
	}
</style>
