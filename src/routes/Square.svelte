<script lang="ts">
	import { getTwemojiUrl } from './utils';

	export let emoji: string;
	export let selected: boolean;
	export let found: boolean;
</script>

<div class="square" class:flipped={selected || found}>
	<button on:click />

	<div class="background" />

	{#if !found}
		<img alt={emoji} src={getTwemojiUrl(emoji)} />
	{/if}
</div>

<style>
	.square {
		display: flex;
		justify-content: center;
		align-items: center;
		transform-style: preserve-3d;
		transition: transform 0.4s;
	}

	.flipped {
		transform: rotateY(180deg);
	}

	button {
		position: absolute;
		width: 100%;
		height: 100%;
		backface-visibility: hidden;
		background-color: #eee;
		border: 0;
		border-radius: 1em;
		font-size: inherit;
	}

	.background {
		position: absolute;
		background-color: #fff;
		transform: rotateY(180deg);
		backface-visibility: hidden;
		width: 100%;
		height: 100%;
		border-radius: 1em;
		border: 0.5em solid #eee;
	}

	img {
		width: 6em;
		height: 6em;
		pointer-events: none;
		transform: rotateY(180deg);
		backface-visibility: hidden;
	}
</style>
