<script lang="ts">
  import Drawer, { Content } from '@smui/drawer';
  import List, { Item, Text } from '@smui/list';
  import { goto } from '$app/navigation';

  let clicked = $state('nothing yet');
</script>

<div class="drawer-container">
  <Drawer>
    <Content>
      <List>
        <Item href="javascript:void(0)" onclick={() => goto('/')}>
          <Text>Monitoramente</Text>
        </Item>
        <!-- <Item href="javascript:void(0)" onclick={() => goto('/programacao')}>
          <Text>Programação</Text>
        </Item> -->
      </List>
    </Content>
  </Drawer>
</div>

<style>
  .drawer-container {
    position: relative;
    height: 100%;
    width: 208px;
    background: #fff;
    z-index: 100;
    display: flex;
    flex-direction: column;
    overflow: hidden;
  }
  
</style>