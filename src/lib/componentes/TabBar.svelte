<script>
  import Tab, { Label } from '@smui/tab';
	import TabBar from '@smui/tab-bar';

  // Define the tabs you want to display
  let tabs = [
    { id: 1, label: 'Salas', permissao: true},
    { id: 2, label: 'Laboratorio', permissao: true},
    { id: 3, label: 'Auditório', permissao: true},
    { id: 4, label: 'Administrativo', permissao: true},
    { id: 5, label: 'Sala de Reuniões', permissao: true},
    { id: 6, label: 'Sala de Descanso', permissao: true}
  ];
</script>
<div>
  <TabBar tabs={tabs.map((tab, i) => tab.label)}>
    {#snippet tab(tab)}
      <Tab {tab}>
        <Label>{tab}</Label>
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