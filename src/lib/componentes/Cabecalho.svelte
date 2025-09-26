<script>
    import Button from '@smui/button';
	import TabBar from './TabBar.svelte';
    function cliquei() {
		alert('Você clicou no botão!');
	}
</script>

<div class="cabecalho-container">
    <img src="src/lib/Logo.png" alt="Logo" class="logo" />
    <div class="tabbar-wrapper">
        <TabBar/>
    </div>
</div>
<!-- <Button onclick={cliquei} variant="raised" color="primary">Teste</Button>
<Button onclick={cliquei} variant="raised" color="primary">Teste</Button> -->
<style>

    .logo {
        height: 48px;
        width: auto;
        max-width: 160px;
        object-fit: contain;
        padding-left: 16px; /* Espaço da lateral */

    }
    .cabecalho-container {
        display: flex;
        align-items: center;

        gap: 32px;
        width: 100%;
        background: white;
    }
    .tabbar-wrapper {
        flex: 1;
        width: 100%;
        min-width: 0;
        display: flex;
        align-items: center;
    }

    h1{
        color: orange
    }
</style>