<script lang="ts">
	import { getTwemojiUrl } from './utils';

	export let found: string[];
</script>

<div class="found">
	{#each found as emoji (emoji)}
		<img alt={emoji} src={getTwemojiUrl(emoji)} />
	{/each}
</div>

<style>
	.found {
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 0.5em;
	}
	img {
		width: 5em;
		height: 5em;
	}
</style>
