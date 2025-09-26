<script>
  import Tab, { Label } from '@smui/tab';
	import TabBar from '@smui/tab-bar';

  // Define the tabs you want to display
  let tabs = [
    { id: 1, label: 'Salas', permissao: true},
    { id: 2, label: 'Laboratorio', permissao: true},
    { id: 3, label: 'Auditório', permissao: true},
    { id: 4, label: 'Administrativo', permissao: true}
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

    display: flex;
    align-items: center;
  }
  :global(.mdc-tab-bar) {
    width: 100%;
    min-width: 0;
    justify-content: flex-start;
  }
  :global(.mdc-tab__text-label) {
    font-size: 1.08rem; /* agradável e legível */
    white-space: nowrap;
  }
  :global(.mdc-tab) {
    min-width: 110px;
  }
  :global(.mdc-tab-indicator__content--underline) {
    background-color: #2ecc40 !important;
  }
  :global(.mdc-tab .mdc-tab__ripple) {
    --mdc-ripple-color: #2ecc40;
    --mdc-ripple-pressed-color: #27ae60;
  }
  :global(.mdc-tab--active .mdc-tab__text-label) {
    color: #2ecc40 !important;

  }
</style>