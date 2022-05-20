<script>
    import SignIn from '../components/SignIn.svelte'
    import { goto } from '@sapper/app';
    import { getContext } from 'svelte';

    //Create alias of 'setNavBar' as we already use setAuthed to pass to sign in
    let setNavBar$ = getContext('setAuthed')

    $: setNavBar = $setNavBar$

    const setAuthed = (val) => {
        setNavBar(val);
        goto('/');
	}


</script>

<SignIn setAuthed={setAuthed} />