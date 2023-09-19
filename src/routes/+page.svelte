<script lang="ts">
	import Game from './Game.svelte';
	import '../styles.css';
	import Modal from './Modal.svelte';
	import { levels } from './levels';

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

<style>
	h1 {
		font-size: 4em;
	}

	h1 span {
		color: purple;
	}

	p {
		font-family: 'Grandstander', sans-serif;
	}
</style>
