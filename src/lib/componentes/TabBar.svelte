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
</style>