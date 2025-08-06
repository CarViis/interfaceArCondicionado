<script lang="ts">
	import '../app.css';
	import Cabecalho from '$lib/componentes/Cabecalho.svelte';
	import Rodape from '$lib/componentes/Rodape.svelte';
	import { page } from '$app/stores';
	let { children } = $props();
</script>

{#if $page.url.pathname !== '/programacao'}
	<Cabecalho />
{/if}
{@render children()}
{#if $page.url.pathname !== '/programacao'}
	<Rodape />
{/if}