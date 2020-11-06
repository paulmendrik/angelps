<script>
import Nav from '../components/Nav.svelte';

export let segment;
</script>


<main>
<Nav {segment}/>
    <slot></slot>
</main>

<style>
    @media (max-width: 414px) {
        main { padding-top: 0 !important;}
    }

    @media (max-width: 375px) {
        main { padding-top: 0 !important;}
    }

    @media (max-width: 320px) {
        main { padding-top: 0 !important;}
    }

</style>