<script lang="ts">
	import Game from './Game.svelte';
	import '../styles.css';
	import Modal from './Modal.svelte';
	import { levels } from './levels';
	import { confetti } from '@neoconfetti/svelte';

	let state: 'waiting' | 'playing' | 'paused' | 'won' | 'lost' = 'waiting';

	let game: Game;
</script>

<Game
	bind:this={game}
	on:play={() => {
		state = 'playing';
	}}
	on:pause={() => {
		state = 'paused';
	}}
	on:lose={() => {
		state = 'lost';
	}}
	on:win={() => {
		state = 'won';
	}}
/>

{#if state !== 'playing'}
	<Modal>
		<header>
			<h1>e<span>match</span>i</h1>
			<p>the emoji matching game</p>
		</header>

		{#if state === 'won' || state === 'lost'}
			<p>you {state} the game!</p>
		{:else if state === 'paused'}
			<p>game paused</p>
		{:else if state === 'waiting'}
			<p>Choose a level:</p>
		{/if}

		<div class="buttons">
			{#if state === 'paused'}
				<button>resume</button>
				<button>quite</button>
			{:else}
				{#each levels as level}
					<button
						on:click={() => {
							game.start(level);
						}}>{level.label}</button
					>
				{/each}
			{/if}
		</div>
	</Modal>
{/if}

{#if state === 'won'}
	<div
		class="confetti"
		use:confetti={{
			stageWidth: innerWidth,
			stageHeight: innerHeight
		}}
	/>
{/if}

<style>
	h1 {
		font-size: 6em;
		margin: 0.3em;
	}

	h1 span {
		color: blueviolet;
	}

	p {
		text-align: center;
		font-size: 1.5em;
	}

	header p {
		font-family: 'Grandstander', sans-serif;
		font-size: 2em;
	}

	.confetti {
		position: fixed;
		width: 100%;
		height: 100%;
		left: 50%;
		top: 30%;
		pointer-events: none;
	}

	.buttons {
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 0.5em;
	}

	.buttons button {
		border: 0;
		background-color: blueviolet;
		padding: 1em;
		color: white;
		border-radius: 0.5em;
		font-size: inherit;
	}
</style>
