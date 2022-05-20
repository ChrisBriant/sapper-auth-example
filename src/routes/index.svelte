<script context="module">
	import { createEventDispatcher,onMount, onDestroy } from "svelte";
	//let authed = false;
	import {checkAuthed} from '../auth/auth';
	
	
</script>

<script>
	import SignIn from '../components/SignIn.svelte';
	import LoadingSpinner from '../components/UI/LoadingSpinner.svelte';
	
	let checkingAuth = true;
	let authed;

	onMount(async () => {
		authed = await checkAuthed();
		//const accessToken = await localStorage.getItem('access_token');
		checkingAuth = false;
	});

	const setAuthed = (val) => {
		console.log('SettingAuthed');
		checkingAuth = true;
		authed = val;
		checkingAuth = false;
	}

</script>

<style>
	h1, figure, p {
		text-align: center;
		margin: 0 auto;
	}

	h1 {
		font-size: 2.8em;
		text-transform: uppercase;
		font-weight: 700;
		margin: 0 0 0.5em 0;
	}

	figure {
		margin: 0 0 1em 0;
	}

	img {
		width: 100%;
		max-width: 400px;
		margin: 0 0 1em 0;
	}

	p {
		margin: 1em auto;
	}

	@media (min-width: 480px) {
		h1 {
			font-size: 4em;
		}
	}
</style>

<svelte:head>
	<title>Sapper project template</title>
</svelte:head>

{#if checkingAuth}
	<LoadingSpinner />
{:else}
	{#if authed}
		<h1>Great success!</h1>

		<figure>
			<img alt='Borat' src='great-success.png'>
			<figcaption>HIGH FIVE!</figcaption>
		</figure>

		<p><strong>Try editing this file (src/routes/index.svelte) to test live reloading.</strong></p>
	{:else}
		<SignIn setAuthed={setAuthed} />
	{/if}
{/if}
