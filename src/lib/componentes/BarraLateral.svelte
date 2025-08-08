<script lang="ts">
  import Drawer, { Content } from '@smui/drawer';
  import List, { Item, Text } from '@smui/list';

  let clicked = $state('nothing yet');
</script>

<div class="drawer-container">
  <Drawer>
    <Content>
      <List>
        <Item href="javascript:void(0)" onclick={() => (clicked = 'Gray Kittens')}>
          <Text>Gray Kittens</Text>
        </Item>
        <Item href="javascript:void(0)" onclick={() => (clicked = 'Gray Kittens')}>
          <Text>Gray Kittens</Text>
        </Item>
        <Item href="javascript:void(0)" onclick={() => (clicked = 'Gray Kittens')}>
          <Text>Gray Kittens</Text>
        </Item>
        <Item href="javascript:void(0)" onclick={() => (clicked = 'Gray Kittens')}>
          <Text>Gray Kittens</Text>
        </Item>
        <Item href="javascript:void(0)" onclick={() => (clicked = 'Gray Kittens')}>
          <Text>Gray Kittens</Text>
        </Item>
        <Item href="javascript:void(0)" onclick={() => (clicked = 'Gray Kittens')}>
          <Text>Gray Kittens</Text>
        </Item>
        <Item href="javascript:void(0)" onclick={() => (clicked = 'Gray Kittens')}>
          <Text>Gray Kittens</Text>
        </Item>
        <Item href="javascript:void(0)" onclick={() => (clicked = 'A Space Rocket')}>
          <Text>A Space Rocket</Text>
        </Item>
        <Item href="javascript:void(0)" onclick={() => (clicked = '100 Pounds of Gravel')}>
          <Text>100 Pounds of Gravel</Text>
        </Item>
        <Item href="javascript:void(0)" onclick={() => (clicked = 'All of the Shrimp')}>
          <Text>All of the Shrimp</Text>
        </Item>
        <Item href="javascript:void(0)" onclick={() => (clicked = 'A Planet with a Mall')}>
          <Text>A Planet with a Mall</Text>
        </Item>
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