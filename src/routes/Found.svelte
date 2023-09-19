<script lang="ts">
	import { getTwemojiUrl } from './utils';
	import { receive } from './transitions';

	export let found: string[];
</script>

<div class="found">
	{#each found as emoji (emoji)}
		<div class="pair">
			<img in:receive={{ key: `${emoji}:a` }} alt={emoji} src={getTwemojiUrl(emoji)} />
			<img in:receive={{ key: `${emoji}:b ` }} alt={emoji} src={getTwemojiUrl(emoji)} />
		</div>
	{/each}
</div>

<style>
	.found {
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 0.5em;
		height: 100%;
		filter: drop-shadow(0.2em 0.2em 0.5em rgba(0, 0, 0, 0.2));
	}

	.pair {
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: white;
		padding: 1em;
		border-radius: 50%;
		width: 6em;
		height: 6em;
	}

	img {
		position: absolute;
		width: 4em;
		height: 4em;
	}
</style>
