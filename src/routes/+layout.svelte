<script lang="ts">
	import '../app.css';
	import Cabecalho from '$lib/componentes/Cabecalho.svelte';
	import Rodape from '$lib/componentes/Rodape.svelte';
	import BarraLateral from '$lib/componentes/BarraLateral.svelte';
</script>

<div style="min-height: 100vh; display: flex; flex-direction: column;">
	<Cabecalho />
	<div style="flex: 1; display: flex; min-height: 0;">
		<BarraLateral />
		<div style="flex: 1; overflow: auto;">
			<slot />
		</div>
	</div>
	<Rodape />
</div>
