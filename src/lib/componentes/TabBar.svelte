<script>
    import Tab, { Label } from '@smui/tab';
	import TabBar from '@smui/tab-bar';
	import { mdiPlus } from '@mdi/js';
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