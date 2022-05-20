<svelte:head>
	<title>About</title>
</svelte:head>

<script>
    import { onMount } from "svelte";
    import { goto } from '@sapper/app';
    import { getContext } from 'svelte';

    onMount(() => {
        if(localStorage.getItem('access_token')) {
            localStorage.removeItem('access_token');
        }
        goto('/');
    });

    let setAuthed$ = getContext('setAuthed')

    $: setAuthed = $setAuthed$

    $: setAuthed(false);

</script>