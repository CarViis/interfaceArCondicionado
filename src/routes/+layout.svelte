<script lang="ts">
	import '../app.css';
	import Cabecalho from '$lib/componentes/Cabecalho.svelte';
	let { children } = $props();
</script>

<Cabecalho />
{@render children()}
