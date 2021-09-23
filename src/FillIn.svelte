<script>
	export let quiz;
	export let scorePoint;
	export let nextQuestion;
	export let activeQuestion;
	import Multi from "./MultiChoice.svelte";
	import { fade } from "svelte/transition";
	console.log(quiz);
	console.log(activeQuestion);
</script>

{#each quiz as question, index}
	{#if index === activeQuestion}
		<div transition:fade class="question">
			<Multi {nextQuestion} {scorePoint} {question} />
		</div>
	{/if}
{/each}
