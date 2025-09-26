<script lang="ts">
	import '../app.css';
	import Cabecalho from '$lib/componentes/Cabecalho.svelte';
	import Rodape from '$lib/componentes/Rodape.svelte';
	import BarraLateral from '$lib/componentes/BarraLateral.svelte';
	import { page } from '$app/stores';
	let { children } = $props();
</script>

<div style="min-height: 100vh; display: flex; flex-direction: column;">
	{#if $page.url.pathname !== '/programacao'}
		<Cabecalho />
	{/if}
	<div style="flex: 1; display: flex; min-height: 0;">
		<BarraLateral />
		<div style="flex: 1; overflow: auto;">
			{@render children()}
		</div>
	</div>
	{#if $page.url.pathname !== '/programacao'}
		<Rodape />
	{/if}
</div>
