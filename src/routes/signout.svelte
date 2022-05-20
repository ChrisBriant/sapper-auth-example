<svelte:head>
	<title>About</title>
</svelte:head>

<script>
    import { createEventDispatcher,onMount, onDestroy } from "svelte";
    import { goto } from '@sapper/app';

    onMount(() => {
        if(localStorage.getItem('access_token')) {
            console.log('HAS ACCESS TOKEN');
            localStorage.removeItem('access_token');
        }
        goto('/');
    });

</script>