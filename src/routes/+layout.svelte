<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
	import { page } from '$app/stores';

	let { children } = $props();

	const isNovel = $derived($page.url.pathname.startsWith('/novel'));
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>



<div class="wrap" style={`background-image: ${isNovel ? 'none' : "url('/background.png')"}` }>
	<div class="content">
		<div class="viewport">
			{@render children?.()}
		</div>
	</div>
	
</div>


{#if isNovel}
	<div class="intro" aria-hidden="true">
		<video
			src="/onContent..mp4"
			class="intro-art"
			autoplay
			muted
			playsinline
			preload="auto"
		></video>
	</div>
{/if}


<style>
	.wrap
	{
		box-sizing: border-box;
		width: 100%;
		min-height: 100dvh;
		display: grid;
		place-items: center;
		background-color: #000000; /* fallback */
		background-size: cover;
		background-position: center;
		background-repeat: no-repeat;
		overflow: hidden; /* prevent sideways movement */
	}

	.content
	{
		position: fixed;
		inset: 0;
		display: grid;
		place-items: center;
		overflow: hidden; /* clip to screen */
		z-index: 1; /* above svg background */
	}

	.viewport
	{
		position: relative;
		width: min(92vw, 420px);
		height: 100dvh;
		padding: 18px;
		box-sizing: border-box;
		overflow-y: auto;
		overflow-x: hidden; /* no horizontal scroll */
		background-color: transparent;
	}

	.intro
	{
		position: fixed;
		inset: 0;
		z-index: 0;
		pointer-events: none;
	}

	.intro-art
	{
		position: fixed;
		inset: 0;
		width: 100vw;
		height: 100vh;
		/* ensure full-viewport coverage for embedded SVG */
		object-fit: cover; /* analogous to background-size: cover */
		object-position: center; /* analogous to background-position: center */
		display: block;
	}
</style>
