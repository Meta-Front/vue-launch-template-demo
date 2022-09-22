<template>
  <CollapseContainer title="新消息通知" :canExpan="false">
    <List>
      <template v-for="item in list" :key="item.key">
        <ListItem>
          <ListItemMeta>
            <template #title>
              {{ item.title }}
              <AntSwitch
                class="extra"
                checked-children="开"
                un-checked-children="关"
                default-checked
              />
            </template>
            <template #description>
              <div>{{ item.description }}</div>
            </template>
          </ListItemMeta>
        </ListItem>
      </template>
    </List>
  </CollapseContainer>
</template>
<script lang="ts">
  import { List, Switch as AntSwitch } from 'ant-design-vue'
  import { defineComponent } from 'vue'
  import { CollapseContainer } from '/@/components/Container/index'

  import { msgNotifyList } from './data'

  export default defineComponent({
    components: {
      CollapseContainer,
      List,
      ListItem: List.Item,
      ListItemMeta: List.Item.Meta,
      AntSwitch
    },
    setup() {
      return {
        list: msgNotifyList
      }
    }
  })
</script>
<style lang="less" scoped>
  .extra {
    float: right;
    margin-top: 10px;
    margin-right: 30px;
  }
</style>
