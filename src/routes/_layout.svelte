<script context="module">
	import { onMount } from "svelte";
	import {checkAuthed} from '../auth/auth';
</script>

<script>
	//import SignIn from '../../components/SignIn.svelte';
	//import LoadingSpinner from '../../components/UI/LoadingSpinner.svelte';
	import Nav from '../components/Nav.svelte';

	export let segment;
	
	let authed = true;

	onMount(async () => {
		authed = await checkAuthed();
	});

</script>

<style>
	main {
		position: relative;
		max-width: 56em;
		background-color: white;
		padding: 2em;
		margin: 0 auto;
		box-sizing: border-box;
	}
</style>

<Nav {segment} {authed}/>

<main class="content">
	<slot></slot>
</main>