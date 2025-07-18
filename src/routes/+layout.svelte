<script lang="ts">
	import '../app.css';
	import Cabecalho from '$lib/componentes/Cabecalho.svelte';
	import Rodape from '$lib/componentes/Rodape.svelte';
	let { children } = $props();
</script>

<Cabecalho />
{@render children()}

<Rodape/>