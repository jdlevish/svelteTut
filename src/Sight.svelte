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
		grid-column-start: 1;
		grid-column-end: 4;
		grid-row-start: 3;
	}
</style>
