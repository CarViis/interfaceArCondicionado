<script lang="ts">
    import TabelaHorario from "$lib/componentes/TabelaHorario.svelte";
    import { page } from '$app/stores';
    import TempPadrao from "$lib/componentes/TempPadrao.svelte";

    let salaId: string = '';
    $: salaId = String($page.params.salaId) ?? '';
</script>


<div style="text-align: center;">
    <h2>Campus YYYYYYY - Sala {salaId}</h2>
    <TempPadrao/>
</div>
<TabelaHorario/>

<style>
    h2 {
        margin: 0;
        padding: 0;
        font-size: 1.5em;
        color: #333;
    }
</style>