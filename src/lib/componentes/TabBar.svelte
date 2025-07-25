<script>
    import Tab, { Label } from '@smui/tab';
	import TabBar from '@smui/tab-bar';
	import { mdiPlus } from '@mdi/js';
</script>
<div>
  <TabBar tabs={[...Array(6)].map((_v, i) => i + 1)}>
    {#snippet tab(tab)}
      <Tab {tab}>
        <Label>Tab {tab}</Label>
      </Tab>
    {/snippet}
  </TabBar>
</div>
<style>
  div {
    width: 100%;
    height: 100%;
  }
  :global(.mdc-tab__text-label) {
    font-size: 1.5rem; /* Aumente conforme necessário */
  }
   /* Cor da barra de seleção (indicator) */
  :global(.mdc-tab-indicator__content--underline) {
    background-color: #2ecc40 !important; /* verde */
  }

  /* Cor do ripple (efeito de clique) */
  :global(.mdc-tab .mdc-tab__ripple) {
    --mdc-ripple-color: #2ecc40;
    --mdc-ripple-pressed-color: #27ae60;
  }

  /* Cor do texto ativo */
  :global(.mdc-tab--active .mdc-tab__text-label) {
    color: #2ecc40 !important;
  }
</style>