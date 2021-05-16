<script>
	import { fade,fly } from 'svelte/transition'
	import EmojiDisplay from './EmojiDisplay.svelte';
	import EmojiDescription from './EmojiDescription.svelte';
	import Button from './Button.svelte';
	import EventButton from './EventButton.svelte';
	import Comment from './Comment.svelte';

	let isLoaded = false;
	let currentEmoji = '😃';
	const emojis = ['🤣', '🐵', '🖕', '🚀'];
	let m = { x:0, y:0};

	function randomizeEmoji() {
		return emojis[Math.floor(Math.random() * emojis.length)];
	}

	function handleRandomButton() {
		currentEmoji = randomizeEmoji()
	}

	setTimeout(function() {
		isLoaded = true;
	}, 2500);

	function handleMousemove(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}
</script>

<style>
</style>

<svelte:head>
	<link href="/terminal.min.css" rel="stylesheet" />
</svelte:head>
<div class="container">
	<div on:mousemove={handleMousemove}>
		<Comment desc={'//Event mousemove on Svelte'}/>
		<p>
			The mouse position: {m.x} x {m.y}
		</p>
		<Comment desc={'//Template each on Svelte'}/>
		<ul>
			{#each emojis as emoji}
			<li>{emoji}</li>
			{/each}
		</ul>
		<Button title={'Toggle'} on:click={() => isLoaded = !isLoaded}></Button>
		{#if isLoaded === true}
		<div in:fly={{y:200, duration:2000}} out:fade>
		<h1>Randomize Emoji</h1>
		<Comment desc={'//Binding on Svelte'}/>
		<EmojiDisplay {currentEmoji} />
		<Button on:click={handleRandomButton} title={'🔁 Randomize'} />
		<Comment desc={'//Event onclick on Svelte'}/>
		<EventButton></EventButton>
		<Comment desc={'//Reactivity on Svelte'}/>
		<EmojiDescription />
		</div>
		{:else}
		<h2>Loading...</h2>
		{/if}
	</div>
</div>