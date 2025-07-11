<script>
    import Button from '@smui/button';
	import Tab, { Label } from '@smui/tab';
	import TabBar from '@smui/tab-bar';
	import { mdiPlus } from '@mdi/js';
	function cliquei() {
		alert('Você clicou no botão!');
	}
</script>

<div>
  <TabBar tabs={[...Array(5)].map((_v, i) => i + 1)}>
    {#snippet tab(tab)}
      <Tab {tab}>
        <Label>Tab {tab}</Label>
      </Tab>
    {/snippet}
  </TabBar>
</div>
<Button onclick={cliquei} variant="raised" color="primary">Teste</Button>
<Button onclick={cliquei} variant="raised" color="primary">Teste</Button>
<style>
    h1{
        color: orange
    }
</style>