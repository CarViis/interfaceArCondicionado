<script lang="ts">
    import TabelaHorario from "$lib/componentes/TabelaHorario.svelte";
    import { page } from '$app/stores';

    let salaId: string = '';
    $: salaId = String($page.params.salaId) ?? '';
</script>


<div style="text-align: center;">
    <h2>Campus YYYYYYY - Sala {salaId}</h2>
</div>
<TabelaHorario/>
