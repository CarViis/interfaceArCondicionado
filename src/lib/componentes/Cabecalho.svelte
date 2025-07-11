<script>
    import Button from '@smui/button';
	import TabBar from './TabBar.svelte';
    function cliquei() {
		alert('Você clicou no botão!');
	}
</script>

<TabBar/>
<Button onclick={cliquei} variant="raised" color="primary">Teste</Button>
<Button onclick={cliquei} variant="raised" color="primary">Teste</Button>
<style>
    h1{
        color: orange
    }
</style>