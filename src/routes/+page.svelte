<script>
	import Cabecalho from '$lib/componentes/Cabecalho.svelte';
	import Button from '@smui/button';
	import Tab, { Label } from '@smui/tab';
	import TabBar from '@smui/tab-bar';
	import Fab, { Icon } from '@smui/fab';
	import { mdiPlus } from '@mdi/js';
	function cliquei() {
		alert('Você clicou no botão!');
	}
</script>

<Cabecalho />
<Button onclick={cliquei} variant="raised" color="primary">Teste</Button>
<Button onclick={cliquei} variant="raised" color="primary">Teste</Button>
<div>
  <TabBar tabs={[...Array(5)].map((_v, i) => i + 1)}>
    {#snippet tab(tab)}
      <Tab {tab}>
        <Label>Tab {tab}</Label>
      </Tab>
    {/snippet}
  </TabBar>
</div>