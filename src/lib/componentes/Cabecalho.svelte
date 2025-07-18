<script>
    import Button from '@smui/button';
	import TabBar from './TabBar.svelte';
    function cliquei() {
		alert('Você clicou no botão!');
	}
</script>

<div class="cabecalho-container">
    <img src="src/lib/Logo.png" alt="Logo" />
    <TabBar/>
</div>
<!-- <Button onclick={cliquei} variant="raised" color="primary">Teste</Button>
<Button onclick={cliquei} variant="raised" color="primary">Teste</Button> -->
<style>
    img {
        height: 50%;
    }
    .cabecalho-container {
        display: flex;
        align-items: center;
        gap: 24px;
    }

    h1{
        color: orange
    }
</style>